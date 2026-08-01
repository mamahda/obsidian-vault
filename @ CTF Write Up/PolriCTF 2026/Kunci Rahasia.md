**Kategori:** Forensics / Crypto 
**File:** `leaked.hex` 
**Flag:** `polriCTF26{x0r_1s_ju5t_4_l0ck_w1th0ut_4_k3y}`

---

## 1. Deskripsi Challenge

> Sebuah startup keamanan siber, NovaSec, baru saja mengalami kebocoran data internal. Tim forensik menemukan satu file mencurigakan yang tertinggal di server log setelah insiden — sepertinya sang penyerang buru-buru kabur dan lupa menghapus jejaknya. File tersebut berisi deretan angka heksadesimal yang menurut tim SOC "terlihat acak, tapi terlalu rapi untuk acak". Salah satu junior analyst curiga ini bukan enkripsi kuat — cuma disamarkan dengan operasi bitwise sederhana yang sering dipakai malware murahan untuk menyembunyikan string dari antivirus. Sebelum insiden terjadi, log akses mencatat sang penyerang login menggunakan kode OTP "42" berkali-kali — entah itu kebetulan atau bukan. Sebagai bagian dari tim forensik, tugasmu: ungkap pesan asli di balik data ini.

Ada dua clue eksplisit di narasi:

1. **"operasi bitwise sederhana yang sering dipakai malware murahan untuk menyembunyikan string"** → ini deskripsi klasik untuk **single-byte XOR obfuscation**, teknik paling umum dipakai malware untuk menyamarkan string dari signature-based AV.
2. **"kode OTP 42 berkali-kali"** → hint langsung ke arah **key XOR = 42**.

---

## 2. Lihat Isi File

```bash
$ cat leaked.hex
5a45465843697e6c181c51521a58751b5975405f1f5e751e75461a4941755d1b5e421a5f5e751e7541195357
```

Satu baris hex string, panjangnya genap (bisa dipasangkan jadi byte). Ini konsisten dengan komentar tim SOC: "terlihat acak, tapi terlalu rapi untuk acak" — bukan enkripsi kuat (yang biasanya benar-benar uniform/acak secara statistik), tapi lebih terlihat seperti hasil operasi sederhana terhadap teks ASCII asli (pola byte-byte yang berulang/mirip khas XOR terhadap teks dengan struktur, misalnya banyak karakter berulang seperti pada flag format `polriCTF26{...}`).

---

## 3. Hipotesis: Single-byte XOR

Karena hint sudah cukup eksplisit (operasi bitwise sederhana + angka 42), langsung dicoba hipotesis paling masuk akal dulu: **XOR tiap byte dengan konstanta 42** — dengan dua kemungkinan interpretasi angka "42":

- `42` sebagai desimal → `0x2A`
- `42` sebagai heksadesimal → `0x42`

## 4. Script Decode

```python
data = bytes.fromhex(
    "5a45465843697e6c181c51521a58751b5975405f1f5e751e75461a4941755d1b5e421a5f5e751e7541195357"
)

for key in (0x2A, 0x42):   # 42 desimal vs 42 heksadesimal
    decoded = bytes(b ^ key for b in data)
    print(hex(key), decoded)
```

Hasil:

```
0x2a b'polriCTF26{x0r_1s_ju5t_4_l0ck_w1th0ut_4_k3y}'
0x42 b'\x18\x07\x04\x1a\x01+<.Z^\x13\x10X\x1a7Y...'   (bukan teks valid)
```

Dengan key **`0x2A` (42 desimal)**, hasilnya langsung berupa flag yang valid dan terbaca sempurna. Interpretasi `0x42` menghasilkan byte-byte non-printable — jelas salah.

---

## 5. Verifikasi

```
polriCTF26{x0r_1s_ju5t_4_l0ck_w1th0ut_4_k3y}
```

Format flag `polriCTF26{...}` cocok, seluruh isi berupa karakter ASCII printable, dan secara tematik pesannya ("XOR itu cuma gembok tanpa kunci yang kuat") pas dengan premis soal — bahwa "enkripsi" penyerang ternyata cuma XOR sepele. 

---

## 6. Kesimpulan

| Aspek                                    | Detail                                                                                                                                                                                                                                                                               |
| ---------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| Teknik obfuscation                       | Single-byte XOR                                                                                                                                                                                                                                                                      |
| Key                                      | `0x2A` (= 42 desimal — sesuai hint OTP di narasi)                                                                                                                                                                                                                                    |
| Kenapa "terlihat acak tapi terlalu rapi" | XOR satu-byte terhadap teks ASCII menghasilkan byte yang terlihat non-random di mata orang awam tapi punya pola statistik jelas (mis. distribusi frekuensi byte yang bisa dikorelasikan ke frekuensi huruf bahasa Inggris) — beda jauh dari ciphertext hasil enkripsi kuat sungguhan |
| Pelajaran                                | Saat clue narasi menyebut angka spesifik berulang kali (di sini "OTP 42"), itu hampir selalu langsung jadi kandidat key — coba dulu sebelum brute-force 256 kemungkinan byte                                                                                                         |

Challenge ini jauh lebih sederhana dibanding tiga crackme binary sebelumnya (`cocoon`, `crackme_polri`, `vibe-check`) — di sini fokusnya pada literasi forensik dasar: mengenali pola obfuscation umum lewat konteks narasi, bukan reverse-engineering binary.