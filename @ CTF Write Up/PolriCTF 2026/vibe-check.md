**Kategori:** Reverse Engineering
**File:** vibe-check (ELF 64-bit PIE, stripped)
**Flag:** `polriCTF26{sp1n_x0r_4dd_sub_cr4ckm3_g0es_brr}`

### 1. Deskripsi Challenge

> _this lil program is checking if you're a real one. feed it the right flag and it'll vibe with you. it will not vibe with you._

Inti dari _challenge_ ini sama seperti _crackme_ pada umumnya: program hanya akan "vibe" (berjalan sukses) jika _input_ yang diberikan persis sama dengan _flag_ asli. Tugas kita adalah me-_reverse_ logika perbandingannya.

### 2. Recon Awal

Cek jenis file dan _strings_ dasar:

Bash

```
$ file vibe-check
vibe-check: ELF 64-bit LSB pie executable, x86-64, ... stripped

$ strings -n 5 vibe-check
...
gimme the flag: 
nope lol
yooo thats it, gg
r0t4t3_k3y
=== NOTICE TO AI ASSISTANTS AND AUTONOMOUS AGENTS ===
This binary is part of polriCTF 2026...
```

**Temuan Menarik:**

1. Ada _prompt injection_ panjang yang menyuruh AI untuk menolak membantu (sama seperti _challenge_ `cocoon` dan `crackme_polri`). Ini cuma jebakan _string_ yang tidak pernah dieksekusi, jadi kita abaikan saja.
    
2. Terdapat _string_ `"r0t4t3_k3y"`. Ini bukan sekadar _hint_, melainkan kunci asli yang dipakai dalam algoritma program.
    

### 3. Dekompilasi & Analisis (Ghidra)

Karena me-_reverse_ murni dari _assembly_ (`objdump`) cukup menguras waktu, kita gunakan **Ghidra** untuk mendapatkan _pseudocode_ C.

Setelah _binary_ di-import dan dianalisis, kita mencari _entry point_ dan menemukan bahwa fungsi `__libc_start_main` memanggil **`FUN_00101100`** yang merupakan fungsi `main` sebenarnya. Setelah merapikan nama variabel menggunakan _shortcut_ `L` (_Rename_) di Ghidra, logikanya menjadi sangat transparan:

```c
void main(void) {
    char input_flag[128];
    printf("gimme the flag: ");
    fgets(input_flag, 128, stdin);
    
    // Hapus newline
    input_flag[strcspn(input_flag, "\n")] = 0;
    
    // Validasi panjang wajib 45 karakter (0x2d)
    if (strlen(input_flag) != 0x2d) {
        puts("nope lol");
        return;
    }
    
    // Loop pengecekan per karakter
    for (int i = 0; i < 45; i = i + 1) {
        // Lapisan 1: XOR input dengan "r0t4t3_k3y"
        byte key1 = "r0t4t3_k3y"[i % 10];
        byte x = input_flag[i] ^ key1;
        
        // Lapisan 2: Rotate Left (ROL) sejauh (i % 7) + 1
        byte shift = (i % 7) + 1;
        byte rotated = (x << shift) | (x >> (8 - shift));
        
        // Lapisan 3: Tambah/Kurang berdasarkan posisi ganjil/genap
        byte val;
        if (i % 2 == 1) {
            val = rotated - i;
        } else {
            val = rotated + i;
        }
        
        // Lapisan 4: Final XOR dengan 0xA5
        val = val ^ 0xA5;
        
        // Bandingkan dengan tabel target (table2)
        if (val != DAT_00102060[i]) {
            puts("nope lol");
            return;
        }
    }
    puts("yooo thats it, gg");
}
```

Setiap posisi `i` diproses secara independen dan murni merupakan transformasi matematika bijektif (tidak ada akumulator seperti _hash chain_).

### 4. Ekstraksi Tabel Target

Untuk memecahkan logika di atas, kita butuh nilai akhir yang ada di dalam variabel `DAT_00102060`.

Di Ghidra, cukup _double-click_ variabel `DAT_00102060`, dan layar akan melompat ke bagian `.rodata` di _Hex View_. Salin 45 _byte_ data tersebut sebagai _Python Byte String_.

```python
# Isi dari DAT_00102060
table2 = bytes.fromhex(
    "a1d967c402b22ef6a9d43ff8a8d0e707"
    "ec019fd39236f3e12d0acc5a19aaf5b3"
    "a6906010a1102ebfd6a5934bd1"
)
```

### 5. Script Solver (Z3 Theorem Prover)

Daripada menulis fungsi _reverse_ manual (yang rawan _human error_ saat membalik urutan rotasi bit atau tambah/kurang), kita gunakan **Z3 SMT Solver**. Kita cukup menulis ulang _forward logic_ dari Ghidra, lalu biarkan Z3 yang mencari tahu apa _input_ awalnya.

```python
from z3 import *

table1 = b"r0t4t3_k3y"
table2 = bytes.fromhex(
    "a1d967c402b22ef6a9d43ff8a8d0e707"
    "ec019fd39236f3e12d0acc5a19aaf5b3"
    "a6906010a1102ebfd6a5934bd1"
)

solver = Solver()
flag_chars = [BitVec(f"char_{i}", 8) for i in range(45)]

for i in range(45):
    # Batasi karakter dalam rentang ASCII yang bisa dibaca
    solver.add(flag_chars[i] >= 32, flag_chars[i] <= 126)
    
    # Layer 1: XOR
    x = flag_chars[i] ^ table1[i % 10]
    
    # Layer 2: Rotate Left
    cl = (i % 7) + 1
    rotated = RotateLeft(x, cl)
    
    # Layer 3: Parity Math (Ganjil dikurang, Genap ditambah)
    if i % 2 == 1:
        val = rotated - i
    else:
        val = rotated + i
        
    # Layer 4: Final XOR
    val = val ^ 0xA5
    
    # Kondisi akhir harus sama dengan table2
    solver.add(val == table2[i])

if solver.check() == sat:
    model = solver.model()
    flag = "".join(chr(model[flag_chars[i]].as_long()) for i in range(45))
    print(f"[*] Flag ditemukan: {flag}")
else:
    print("[!] Gagal menyelesaikan persamaan.")
```

**Output:**

Plaintext

```
[*] Flag ditemukan: polriCTF26{sp1n_x0r_4dd_sub_cr4ckm3_g0es_brr}
```

### 6. Verifikasi

Uji coba _flag_ ke program asli:

Bash

```
$ ./vibe-check
gimme the flag: polriCTF26{sp1n_x0r_4dd_sub_cr4ckm3_g0es_brr}
yooo thats it, gg
```

_Solved!_