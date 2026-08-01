**Kategori:** Reverse Engineering 
**File:** `cocoon` (ELF 64-bit PIE, stripped) 
**Flag:** `polriCTF26{p33l_th3_l4y3rs_x0r_r0t_qu4d_ch41n}`

---

## 1. Deskripsi Challenge

> Namanya cocoon karena flag-nya dibungkus berlapis, dan program ini pelit. Dia tidak mencetak apa pun yang berguna, tidak membocorkan algoritmanya, dan tidak pernah menyimpan flag dalam bentuk terbaca. Kamu mengetik tebakan, dia membungkus tebakanmu lewat beberapa lapisan transformasi berkunci, lalu membandingkannya dengan sepotong ciphertext yang tertanam di dalam binari. Cocok berarti benar.

Tidak ada instance/server — cuma binary statis yang harus di-reverse murni secara offline.

---

## 2. Recon Awal

### 2.1 Cek jenis file

```bash
$ file cocoon
cocoon: ELF 64-bit LSB pie executable, x86-64, ... stripped
```

Binary-nya PIE dan **stripped** (tidak ada simbol fungsi), jadi tidak bisa mengandalkan nama fungsi — harus baca alamat mentah.

### 2.2 Cek section headers

```bash
$ readelf -S cocoon
```

Yang mencurigakan: ada section custom bernama **`.cocoon`** di antara `.rodata` dan `.eh_frame_hdr`, ukurannya `0x2e` = **46 byte**. Ini jelas bukan section standar ELF — kemungkinan besar di sinilah ciphertext asli disimpan (dan ternyata benar).

### 2.3 Cek strings

```bash
$ strings -n 6 cocoon
...
unpack> 
correct! that is the flag.
hanz: 2 menit? lucu. yang ini dibungkus berlapis, kupas sendiri lapisannya. wlwlwl
polriCTF26{unp4ck3d_wr0ng_l4y3r_d3c0y}
```

Ada string `polriCTF26{unp4ck3d_wr0ng_l4y3r_d3c0y}` yang terlihat seperti flag — tapi namanya sendiri sudah kasih clue (`d3c0y` = decoy). Setelah dicek lewat disassembly, string ini **tidak pernah direferensikan** oleh kode apa pun (tidak ada `lea`/instruksi lain yang menunjuk ke alamatnya). Ini jebakan murni untuk orang yang cuma `strings | grep CTF` tanpa reverse beneran. Ciphertext yang benar-benar dipakai program ada di section `.cocoon`, bukan di string ini.

---

## 3. Disassembly & Alur Program

Karena binary kecil (< 15 KB) dan tidak ada anti-debug/packing, `objdump -d -M intel` sudah cukup — tidak perlu radare2/IDA.

```bash
$ objdump -d -M intel cocoon
```

Alur `main` (di alamat `0x10a0`) secara garis besar:

```c
fwrite("unpack> ", 1, 8, stdout);
fflush(stdout);
fgets(buf, 0x80, stdin);           // buf di rsp+0x30
len = strlen(buf);
if (buf[len-1] == '\n') { buf[len-1] = 0; len--; }  // strip newline
if (len != 46) { puts("..."); return 0; }            // panjang WAJIB 46
transform(buf);                                       // <-- inti algoritma
if (memcmp(transformed_buf, &data_at_0x20a0, 46) == 0)
    puts("correct! that is the flag.");
else
    puts("...");
```

Poin penting:

- **Panjang input harus tepat 46 byte** (`cmp rax, 0x2e`).
- Hasil transformasi (disimpan balik ke `rsp`, menimpa buffer awal) dibandingkan lewat `memcmp` dengan 46 byte yang ada di `.cocoon` (alamat `0x20a0`).
- Tidak ada fungsi print debug, tidak ada dekripsi flag ke memori dulu — satu-satunya cara tahu benar/salah adalah lewat hasil `memcmp` itu sendiri. Makanya harus di-reverse penuh, tidak bisa di-brute paksa per karakter lewat oracle sederhana.

---

## 4. Membedah "Lapisan-Lapisan" Transformasi

Bagian inti ada di alamat `0x1125`–`0x11e3`, sebuah loop tunggal yang jalan 46 kali (`i` dari 0 sampai 45). Saya baca instruksi satu-satu dan translasikan ke pseudocode:

### 4.1 Lapisan 1 — Seed generator (busy-loop palsu)

```asm
1140: imul esi, esi, 0x1000193      ; esi *= 0x01000193
1146: xor  esi, eax
1148: add  eax, 0x2545f491
114d: cmp  eax, 0xa8be9220
1152: jne  1140
```

Ini loop `while (eax != TARGET) { esi = esi*PRIME ^ eax; eax += STEP; }` mulai dari `eax=esi=0`. Terlihat seperti hash FNV-ish yang "mahal", tapi sebenarnya cuma trik obfuscation: jumlah iterasi bisa dihitung langsung tanpa iterasi literal, pakai **modular inverse mod 2³²**:

```python
MOD = 1 << 32
step, target = 0x2545f491, 0xa8be9220
inv = pow(step, -1, MOD)
n = (target * inv) % MOD   # = 32
```

Ternyata cuma **32 iterasi** — jadi tetap bisa disimulasikan literal dengan cepat untuk mendapat nilai `esi` akhir. Setelah loop selesai, `esi ^= 0xc0c0012e` → ini jadi **state awal** generator berikutnya.

### 4.2 Lapisan 2 — Xorshift32 per posisi

```asm
1180: mov edx, esi
118d: shl edx, 0xd      ; edx = esi << 13
1194: xor edx, esi      ; t1  = esi ^ (esi<<13)
1198: shr eax, 0x11     ; (eax=edx) t1 >> 17
119b: xor eax, edx      ; t2  = t1 ^ (t1>>17)
119f: shl esi, 0x5      ; (esi=t2) t2 << 5
11a2: xor esi, eax      ; state_baru = t2 ^ (t2<<5)
```

Ini persis **xorshift32** (Marsaglia): `x^=x<<13; x^=x>>17; x^=x<<5`. State ini diupdate ulang di _setiap_ dari 46 posisi — jadi tiap byte input punya "kunci" xorshift sendiri yang cuma tergantung posisi `i`, **bukan** tergantung nilai input.

### 4.3 Lapisan 3 — XOR + Rotate berbasis posisi

```asm
1185: movzx ebp, BYTE PTR [r8]     ; ebp = input[i] (zero-extended)
11ad: xor   ebp, esi               ; ebp = input[i] XOR state_baru  (full 32-bit!)
11d3: rol   bpl, cl                ; rotate LOW BYTE ebp sejauh cl bit
```

Poin krusial (dan agak jebakan) di sini: instruksi `xor ebp, esi` adalah **XOR 32-bit penuh**, bukan cuma byte rendah. Karena `ebp` awalnya _zero-extended_ (24 bit atas = 0), hasil XOR membuat 24 bit atas `ebp` **sama persis dengan 24 bit atas `state`**. Lalu `rol bpl, cl` cuma memutar **8 bit rendah** — 24 bit atas itu tetap dibawa apa adanya ke penjumlahan berikutnya. Jadi bukan cuma "byte input di-XOR-rotate", tapi seluruh register 32-bit yang terpengaruh non-trivial.

Nilai `cl` (jumlah rotasi) dihitung dari:

```asm
11a7: imul rbx              ; rax(=i) * MAGIC (0x4924924924924925)
11b3: sar rdx, 1
11b6: sub rdx, rax           ; rdx = i / 7   (division-by-7 lewat magic constant)
11c1: sub rax, rdx           ; rax = 7 * (i/7)
11c4: sub rcx, rax           ; rcx = i - 7*(i/7) = i % 7
11cc: add ecx, 1              ; cl  = (i % 7) + 1
```

Saya verifikasi konstanta magic (`0x4924924924924925`) itu memang trik compiler untuk **pembagian dengan 7**, dengan cara brute-cek di Python: hitung `rdx` untuk `i = 0..45` dan bandingkan ke `i//7` — hasilnya identik persis.

Jadi **rotate count = (i % 7) + 1**, nilainya 1–7, murni fungsi posisi.

### 4.4 Lapisan 4 — Rantai akumulator kuadratik (hash chain)

```asm
11c7: mov  eax, edi
11c9: imul eax, edi          ; eax = i*i
11d6: add  eax, ebp          ; eax = i*i + ebp_full(32-bit, sudah termasuk rotasi)
11d8: xor  r9d, eax          ; r9d = r9d XOR eax   (r9d TIDAK PERNAH DI-RESET)
11db: mov  BYTE PTR [r10-1], r9b   ; output[i] = low-byte(r9d) SETELAH update ini
```

Ini bagian paling penting untuk strategi solve: `r9d` adalah **akumulator 32-bit yang terus menumpuk** dari posisi `i=0` sampai `i=45`. Byte output di posisi `i` cuma **low-byte** dari `r9d` di titik itu — tapi 24 bit atas `r9d` tetap ikut dibawa (di-XOR terus) ke iterasi berikutnya walau tidak pernah "terlihat" langsung di output. Ini yang bikin transformasi terasa seperti **hash chain** satu arah, bukan stream cipher XOR biasa yang bisa langsung dibalik per-byte independen.

---

## 5. Kenapa Tetap Bisa Dibalik (Strategi Solve)

Kuncinya: semua nilai yang bergantung pada posisi (`state_i` dari xorshift32, `cl_i = (i%7)+1`, `i*i`) **bisa dihitung tanpa tahu input sama sekali**. Satu-satunya bagian yang bergantung pada input adalah **byte rendah** dari `ebp_full`, lewat fungsi:

```
rotated_byte = ROL8( input[i] XOR low_byte(state_i), cl_i )
```

`XOR` dengan konstanta dan `ROL` dengan jumlah tetap itu **keduanya bijektif** pada domain byte (0–255) — artinya kalau `input[i]` mencakup semua nilai 0–255, `rotated_byte` juga mencakup semua nilai 0–255, masing-masing tepat sekali. Karena penjumlahan `i*i + ebp_full` dan `XOR` ke akumulator itu linear terhadap byte rendah (24 bit atas `ebp_full` tetap/konstan per posisi), maka **low-byte hasil akhir (`r9d` baru) juga bijektif terhadap 256 kemungkinan input byte**.

Jadi strategi solve-nya, **posisi demi posisi dari kiri**:

1. Hitung `state_i` (xorshift32) dan `cl_i` — murni dari `i`, tidak butuh input.
2. Brute-force `input[i]` dari 0–255:
    - Hitung `ebp_full = (state_i & 0xFFFFFF00) | ROL8(b XOR low_byte(state_i), cl_i)`
    - Hitung `eax = i*i + ebp_full` (mod 2³²)
    - Hitung `r9d_candidate = r9d_prev XOR eax`
    - Cek apakah `low_byte(r9d_candidate)` sama dengan byte ciphertext di posisi `i` (dari section `.cocoon`)
3. Karena bijektif, **tepat satu** nilai `b` yang cocok → itu `input[i]` yang benar, dan `r9d_candidate` jadi `r9d_prev` untuk posisi berikutnya.
4. Ulangi untuk 46 posisi → seluruh flag terbentuk.

Total kerja komputasi: `46 x 256` percobaan — instan.

---

## 6. Ambil Ciphertext dari Binary

```bash
$ objdump -s -j .cocoon cocoon
Contents of section .cocoon:
 20a0 e2d8a65f 70b59830 4fb5ef81 2d3eb087
 20b0 33330965 b8611dca c42d75ea 91b0054e
 20c0 aa5eccd8 d1b74795 ba635707 8a29
```

46 byte ciphertext (gabungkan semua jadi satu hex string).

---

## 7. Script Solver (Python)

```python
MOD32 = (1 << 32) - 1

def xorshift32(s):
    s &= 0xFFFFFFFF
    t1 = (s ^ ((s << 13) & MOD32)) & MOD32
    t2 = (t1 ^ (t1 >> 17)) & MOD32
    return (t2 ^ ((t2 << 5) & MOD32)) & MOD32

def rol8(x, n):
    x &= 0xFF
    n &= 7
    if n == 0:
        return x
    return ((x << n) | (x >> (8 - n))) & 0xFF

# --- Lapisan 1: hitung state awal lewat seed loop (cukup 32 iterasi) ---
eax, esi = 0, 0
step, target, prime = 0x2545f491, 0xa8be9220, 0x1000193
while True:
    esi = (esi * prime) & MOD32
    esi ^= eax
    eax = (eax + step) & MOD32
    if eax == target:
        break
state = (esi ^ 0xc0c0012e) & MOD32

# --- Ciphertext dari section .cocoon ---
hexstr = ("e2d8a65f70b598304fb5ef812d3eb087"
          "33330965b8611dcac42d75ea91b0054e"
          "aa5eccd8d1b74795ba6357078a29")
ciphertext = bytes.fromhex(hexstr)
assert len(ciphertext) == 46

r9d = 0
flag = bytearray()

for i in range(46):
    state = xorshift32(state)               # Lapisan 2
    cl = (i % 7) + 1                          # rotate count posisi ke-i
    upper = state & 0xFFFFFF00
    low_state = state & 0xFF

    for b in range(256):                      # brute force 1 byte flag
        rotated = rol8(b ^ low_state, cl)     # Lapisan 3
        ebp_full = upper | rotated
        eax_val = (i * i + ebp_full) & 0xFFFFFFFF   # Lapisan 4
        cand = r9d ^ eax_val
        if (cand & 0xFF) == ciphertext[i]:
            flag.append(b)
            r9d = cand
            break

print(bytes(flag).decode())
```

---

## 8. Verifikasi

Output script:

```
polriCTF26{p33l_th3_l4y3rs_x0r_r0t_qu4d_ch41n}
```

Cek langsung ke binary asli:

```bash
$ printf 'polriCTF26{p33l_th3_l4y3rs_x0r_r0t_qu4d_ch41n}\n' | ./cocoon
unpack> correct! that is the flag.
```

Solved!. 

---

## 9. Kesimpulan / Ringkasan Lapisan

|Lapisan|Nama|Sifat|
|---|---|---|
|1|Seed generator (busy-loop FNV-ish)|Konstan, tidak tergantung input — cuma 32 iterasi asli di balik "obfuscation"|
|2|Xorshift32 per posisi|State berubah tiap `i`, murni fungsi posisi|
|3|XOR (32-bit) + ROL8 byte rendah|Satu-satunya titik yang bergantung pada input, tapi bijektif → bisa di-brute per byte|
|4|Akumulator kuadratik (`i*i`) + XOR chain tanpa reset|Membuat tiap output byte bergantung pada seluruh riwayat sebelumnya (hash chain), memaksa solve dilakukan berurutan dari kiri ke kanan|

**Insight kunci:** walau terlihat seperti cipher yang "tidak bisa dibalik" karena akumulasinya tidak pernah direset, setiap lapisan tetap **bijektif per posisi** terhadap byte input — sehingga transformasi bisa dipecah dan diselesaikan **byte-per-byte secara berurutan**, bukan dibalik sekaligus secara aljabar.

String decoy `polriCTF26{unp4ck3d_wr0ng_l4y3r_d3c0y}` yang muncul di `strings` sengaja dipasang dan tidak pernah direferensikan kode — pengingat untuk selalu verifikasi lewat disassembly, bukan cuma grep string.