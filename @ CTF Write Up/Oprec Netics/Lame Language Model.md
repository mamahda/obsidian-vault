[[Remote Code Execution (RCE)]] | [[Server-side request forgery (SSRF)]]

- [[#1 Summary of Findings|1 Summary of Findings]]
- [[#2 Details of Vulnerabilities|2 Details of Vulnerabilities]]
	- [[#2 Details of Vulnerabilities#2.1 - Hardcoded Credentials pada Endpoint Autentikasi|2.1 - Hardcoded Credentials pada Endpoint Autentikasi]]
	- [[#2 Details of Vulnerabilities#2.2 - JWT Secret Hardcoded|2.2 - JWT Secret Hardcoded]]
	- [[#2 Details of Vulnerabilities#2.3 - OS Shell Command Injection via Tag Filter (RCE)|2.3 - OS Shell Command Injection via Tag Filter (RCE)]]
	- [[#2 Details of Vulnerabilities#2.4 - Server-Side Request Forgery (SSRF) via Parameter Model Chat|2.4 - Server-Side Request Forgery (SSRF) via Parameter Model Chat]]
	- [[#2 Details of Vulnerabilities#2.5 - Hardcoded Passphrase pada Internal Service|2.5 - Hardcoded Passphrase pada Internal Service]]
- [[#3 Discovered Flag|3 Discovered Flag]]


| Detail | Keterangan |
| :--- | :--- |
| **Target** | `http://43.129.35.148:7000` |
| **Difficulty** | **Medium** |
| **Author** | Athallah Rajendra |
| **Tech Stack** | PHP 8, Apache, PostgreSQL 14, Docker Compose |

## 1 Summary of Findings

| No | Judul | Target | Severity | CVSS |
| :--- | :--- | :--- | :--- | :--- |
| 1 | Hardcoded Credentials di Login | Lame Language Model | High | 7.5 |
| 2 | JWT Secret Hardcoded | Lame Language Model | Critical | 9.8 |
| 3 | OS Command Injection via Tag Filter (RCE) | Lame Language Model | Critical | 9.8 |
| 4 | SSRF via Parameter Model Chat | Lame Language Model | High | 8.6 |
| 5 | Hardcoded Passphrase Internal Service | Lame Language Model | High | 7.5 |

---

## 2 Details of Vulnerabilities

### 2.1 - Hardcoded Credentials pada Endpoint Autentikasi

| Kategori | Keterangan |
| :--- | :--- |
| **Severity** | **High** |
| **CVSS Score** | 7.5 (AV:N/AC:L/PR:N/UI:N/S:U/C:H/I:N/A:N) |
| **Deskripsi** | File `api/login.php` mengandung credential hardcoded (username: `tillkrump`, password: `iamwhitelisted`) yang dibandingkan langsung menggunakan equality check. Form HTML `login.php` juga meng-pre-populate credential kedua (`analyst` / `oracle123`) dalam plaintext yang terlihat di page source. |
| **Dampak** | Penyerang yang memiliki akses source code dapat langsung autentikasi ke aplikasi tanpa brute-force. Token JWT yang dihasilkan memiliki role `guest`. |
| **Saran Perbaikan** | Hapus semua hardcoded credential dari source code. Simpan di environment variable atau secrets manager. Gunakan hashing bcrypt/argon2 untuk password. Hapus nilai pre-filled dari form HTML. |

**Proof of Concept**
1. Bisa kita lihat dari source code langsung.
![[Screenshot_20260509_215034.png]]
2. Lalu pada tampilan web awal terdapat input untuk login ke user akun.
![[Screenshot_20260509_220314.png]]
3. Dari credential yang di hard code pada source code, kita bisa login ke dalam user akun. Akan tetapi user hanya memiliki role `guest`.
![[Screenshot_20260509_220319.png]]

### 2.2 - JWT Secret Hardcoded

| Kategori | Keterangan |
| :--- | :--- |
| **Severity** | **Critical** |
| **CVSS Score** | 9.8 (AV:N/AC:L/PR:N/UI:N/S:U/C:H/I:H/A:H) |
| **Deskripsi** | Secret HMAC-SHA256 untuk key JWT di-hardcode sebagai string `'memory-oracle-dev-secret'` di `auth.php`. Karena secret diketahui, penyerang dapat memalsukan JWT payload sembarang, termasuk mengubah role dari `'guest'` menjadi `'user'` dengan signature valid yang diterima server. |
| **Dampak** | Eskalasi privilege penuh dari unauthenticated menjadi role `'user'`. Semua fungsionalitas yang dibatasi role, termasuk manajemen memori dan endpoint chat/SSRF, menjadi dapat diakses. |
| **Saran Perbaikan** | Buat JWT secret secara acak saat deploy menggunakan CSPRNG. Simpan eksklusif di environment variable. Jangan pernah commit secret ke source code atau version control. |

**Proof of Concept**
1. Bisa kita lihat dari source code langsung.
![[Screenshot_20260509_215512.png]]
2. Dari source code kita juga mendapatkan informasi bahwa untuk masuk ke page utama kita memerlukan token dengan role `user`.
![[Screenshot_20260509_220727.png]]
3. Dari JWT Secret tersebut, attacker dapat melakukan generate JWT token baru dengan role `user` sesuai kebutuhan. Setelah itu, request diintercept menggunakan Burp Suite lalu token lama diganti dengan token hasil generate sebelum request dikirim kembali ke server.
![[Screenshot_20260509_221051.png]]
4. Lalu kita berhasil masuk ke page `user`.
![[Screenshot_20260509_221307.png]]


### 2.3 - OS Shell Command Injection via Tag Filter (RCE)

| Kategori | Keterangan |
| :--- | :--- |
| **Severity** | **Critical** |
| **CVSS Score** | 9.8 (AV:N/AC:L/PR:L/UI:N/S:C/C:H/I:H/A:H) |
| **Deskripsi** | Di `db.php`, parameter tag yang disuplai pengguna diinterpolasi langsung ke dalam string bash double-quoted yang diteruskan ke `system()`. Meskipun `pg_escape_string()` dipanggil, fungsi ini hanya meng-escape karakter SQL. Metacharacter shell seperti `$()`, backtick, dan titik koma tidak dineutralisir, memungkinkan command substitution sembarang. |
| **Dampak** | Remote code execution sebagai user `www-data` di dalam container Docker webapp. Penyerang dapat membaca file sembarang, mengenumerasi environment, pivot ke container lain, dan mengeksfiltrasi database. |
| **Saran Perbaikan** | Ganti wrapper `psql()` berbasis shell sepenuhnya dengan ekstensi PDO PostgreSQL PHP menggunakan parameterized queries. Jika eksekusi shell diperlukan, gunakan `escapeshellarg()` pada setiap variabel yang diinterpolasi. |

**Proof of Concept**
1. Karena pada input SQL hanya disanitasi karakter `'`, payload masih bisa di bypass menggunakan `$()` untuk menjalankan RCE. Contohnya `$(ls />/var/www/html/out.txt)` yang akan mengeksekusi perintah `ls /`.
![[Screenshot_20260512_123024.png]]
2. Output command diarahkan ke file `out.txt` karena hasil query di halaman hanya menampilkan data tabel, sehingga output dari command `ls /` tidak akan terlihat langsung pada response aplikasi. Dengan menyimplannya ke file di web root, hasil eksekusi bisa diakses lewat browser.
![[Screenshot_20260512_123158.png]]
3. Dari hasil `ls /` sebelumnya diketahui bahwa file flag berada di `/flag.txt`. Setelah itu, file dapat dibaca menggunakan payload dengan metode yang sama, yaitu `$(cat /flag.txt>/var/www/html/out.txt)` untuk menyimpan isi flag ke file yang bisa diakses melalui browser.
![[Screenshot_20260512_123104.png]]
4. Dan kita telah berhasil mendapatkan flagnya.
![[Screenshot_20260512_123142.png]]

### 2.4 - Server-Side Request Forgery (SSRF) via Parameter Model Chat

| Kategori | Keterangan |
| :--- | :--- |
| **Severity** | **High** |
| **CVSS Score** | 8.6 (AV:N/AC:L/PR:L/UI:N/S:C/C:H/I:N/A:N) |
| **Deskripsi** | Di `chat.php`, parameter model dari request body diinterpolasi langsung ke URL target: `$target = 'http://' . $model . ':8090'`. Hanya nilai `'gemini'` dan `'grok'` yang diblokir secara eksplisit. String lain apapun, termasuk nama service Docker internal diteruskan sebagai HTTP request. |
| **Dampak** | Penyerang dapat menjangkau service 'internal' yang tidak diekspos ke host. |
| **Saran Perbaikan** | Implementasikan allowlist ketat untuk parameter model, hanya tiga nilai yang diketahui. Tolak semua input lain sebelum membuat request jaringan. Tempatkan service internal di jaringan Docker terpisah yang tidak dapat dijangkau container webapp. |

**Proof of Concept**
1. Bisa kita lihat dari source code langsung.
![[Screenshot_20260512_130111.png]]
### 2.5 - Hardcoded Passphrase pada Internal Service

| Kategori | Keterangan |
| :--- | :--- |
| **Severity** | **High** |
| **CVSS Score** | 7.5 (AV:N/AC:L/PR:N/UI:N/S:U/C:H/I:N/A:N) |
| **Deskripsi** | Internal service (`internal/index.php`) hanya memberikan akses ke flag ketika request body mengandung passphrase hardcoded yang tepat: `'give me flag right NOW 26354OklA3bdsy27-dhSUDH28GH-663asd2'`. Passphrase ini tertanam dalam plaintext di source code. |
| **Dampak** | Pihak manapun yang memiliki akses source code dapat memanggil internal service melalui SSRF (RT-07) dan mengambil flag secara langsung. |
| **Saran Perbaikan** | Ganti passphrase hardcoded dengan mekanisme autentikasi yang proper (mutual TLS, network policy allowlist, atau secret yang diinjeksi saat runtime via environment variable). |

**Proof of Concept**
1. Bisa kita lihat dari source code langsung.
![[Screenshot_20260509_215817.png]]
---

## 3 Discovered Flag

> **`NETICS{w45-1t-S5RF-0r-w4s-1t-n0t-7703ca38-981b-4cd6-8b38-30711c5a1a17}`**
