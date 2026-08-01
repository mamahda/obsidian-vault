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

Karena hint sudah cukup eksplisit (operasi bitwise sederhana + angka 42), langsung dicoba hipotesis paling masuk akal dulu: **XOR tiap byte dengan konstanta 42**


## 4. Script Decode

```python
data = bytes.fromhex(
    "5a45465843697e6c181c51521a58751b5975405f1f5e751e75461a4941755d1b5e421a5f5e751e7541195357"
)

decoded = bytes(b ^ 42 for b in data)
print(decoded)
```

Hasil:

```
b'polriCTF26{x0r_1s_ju5t_4_l0ck_w1th0ut_4_k3y}'
```

Dengan key 42, hasilnya langsung berupa flag yang valid dan terbaca sempurna.

---

## 5. Verifikasi

```
polriCTF26{x0r_1s_ju5t_4_l0ck_w1th0ut_4_k3y}
```

Format flag `polriCTF26{...}` cocok, seluruh isi berupa karakter ASCII printable, dan secara tematik pesannya ("XOR itu cuma gembok tanpa kunci yang kuat") pas dengan premis soal — bahwa "enkripsi" penyerang ternyata cuma XOR sepele. 
