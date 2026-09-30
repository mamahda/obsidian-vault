**Kategori:** Reverse Engineering  <br>
**File:** `chall.js` (Node.js crackme) <br>
**Flag:** `HCS{$el@M4t_nA8IL_afri2@l_AD41AH_s0$OK_4511_PRes1D3N_84yAN6AN_hcS}`  <br>
**AI Chat:** https://chat.ragita.net/s/698d2710-d29f-4b46-82e3-b3459ac1a5ed <br>

---

## 1. Deskripsi Challenge

Crackme berbasis JavaScript: program membaca input flag lewat `stdin`, menjalankannya melalui rangkaian transformasi berkunci, lalu membandingkan hasilnya dengan array target yang tertanam di source. Cocok → `Gacor`.

---

## 2. Analisis `chall.js`

Ada dua variabel penting:

- `_k` → **key enkripsi** (3 byte, dipakai berulang).
- `_d` → **ciphertext target** (66 byte) — sekaligus menentukan panjang flag.

```js
const _k = [13, 37, 42];
const _d = [33, 61, 50, 3, 56, 254, 35, 200, 245, 26, 8, 226, 184, 29,
    227, 182, 251, 211, 237, 209, 237, 5, 2, 193, 157, 143, 181, 238,
    228, 181, 126, 130, 232, 220, 209, 173, 121, 108, 161, 192, 204,
    176, 182, 96, 170, 155, 131, 169, 175, 160, 120, 67, 146, 142,
    157, 118, 91, 134, 129, 122, 101, 20, 134, 134, 112, 76];
```

Algoritma enkripsinya:

```js
for (let i = 0; i < flag.length; i++) {
    let c = flag.charCodeAt(i);
    c = c ^ _k[i % _k.length];       // 1) XOR dengan key (siklus 3)
    c = (c + i * 3 + 7) & 0xFF;      // 2) tambah (i*3+7), mod 256
    enc.push(c);
}
enc.reverse();                        // 3) balik seluruh array
// lalu enc dibandingkan byte-per-byte dengan _d
```

Tiga langkah: **XOR → add (i*3+7) mod 256 → reverse**. Panjang flag wajib `_d.length` = **66 karakter**.

---

## 3. Membalik Algoritma

Semua operasi bersifat **bijektif**, tinggal dibalik urutannya. Karena ada `enc.reverse()`, byte pada posisi `i` di `flag` berkorespondensi dengan `_d[n-1-i]`:

```
enc[i]   = ((flag[i] ^ _k[i%3]) + i*3 + 7) & 0xFF
_d[j]    = enc[n-1-j]           # akibat reverse
=> flag[i] = ( (_d[n-1-i] - (i*3 + 7)) & 0xFF ) ^ _k[i%3]
```

> **Catatan:** karena di rules tidak ada larangan *one-shot*, solver awal dibuat lewat AI. Tapi hasil AI ada **1 variabel yang ketukar** (indeks key setelah `reverse()`) sehingga outputnya salah; setelah dibetulkan pemetaan indeksnya, solver di bawah langsung memuntahkan flag yang benar.

---

## 4. Solver (Python)

```python
#!/usr/bin/env python3

k = [13, 37, 42]
d = [
    33, 61, 50, 3, 56, 254, 35, 200, 245, 26, 8, 226, 184, 29,
    227, 182, 251, 211, 237, 209, 237, 5, 2, 193, 157, 143, 181,
    238, 228, 181, 126, 130, 232, 220, 209, 173, 121, 108, 161,
    192, 204, 176, 182, 96, 170, 155, 131, 169, 175, 160, 120,
    67, 146, 142, 157, 118, 91, 134, 129, 122, 101, 20, 134,
    134, 112, 76
]

def decode_flag() -> str:
    n = len(d)
    flag_bytes = [0] * n
    for j in range(n):
        i = n - 1 - j              # indeks di _d setelah reverse()
        enc_val   = d[i]
        key_idx   = j % len(k)
        tmp       = (enc_val - (j * 3 + 7)) & 0xFF   # undo add
        orig_code = tmp ^ k[key_idx]                 # undo XOR
        flag_bytes[j] = orig_code
    return bytes(flag_bytes).decode('latin1')

if __name__ == "__main__":
    print("Flag yang ditemukan:")
    print(decode_flag())
```

---

## 5. Verifikasi

```
$ python3 solver.py
Flag yang ditemukan:
HCS{$el@M4t_nA8IL_afri2@l_AD41AH_s0$OK_4511_PRes1D3N_84yAN6AN_hcS}
```

Panjang 66 karakter sesuai `_d.length`, format `HCS{...}` cocok. 
_Solved!_
