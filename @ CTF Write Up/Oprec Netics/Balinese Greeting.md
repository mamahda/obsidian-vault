[[Server Side Template Injection (SSTI)]]

- [[#1 Summary of Findings|1 Summary of Findings]]
- [[#2 Details of Vulnerabilities|2 Details of Vulnerabilities]]
	- [[#2 Details of Vulnerabilities#2.1 - Insecure Use of render_template_string pada Input Pengguna|2.1 - Insecure Use of render_template_string pada Input Pengguna]]
	- [[#2 Details of Vulnerabilities#2.2 - Server-Side Template Injection (SSTI) via Blacklist Bypass|2.2 - Server-Side Template Injection (SSTI) via Blacklist Bypass]]
- [[#3 Discovered Flag|3 Discovered Flag]]

| Detail | Keterangan |
| :--- | :--- |
| **Target** | `http://43.129.35.148:7000` |
| **Difficulty** | **Easy** |
| **Author** | Fajar Yasodana |
| **Tech Stack** | Python Flask, Jinja2, Docker |

## 1 Summary of Findings

| No | Judul | Severity | CVSS |
| :--- | :--- | :--- | :--- |
| 1 | Insecure Use of `render_template_string` pada Input Pengguna | Critical | 9.8 |
| 2 | Server-Side Template Injection via Blacklist Bypass (SSTI) | Critical | 9.8 |

---

## 2 Details of Vulnerabilities

### 2.1 - Insecure Use of render_template_string pada Input Pengguna

| Kategori            | Keterangan                                                                                                                                                                                                                                                                                                                                                                                           |
| :------------------ | :--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Severity**        | **Critical**                                                                                                                                                                                                                                                                                                                                                                                         |
| **CVSS**            | 9.8 (AV:N/AC:L/PR:N/UI:N/S:U/C:H/I:H/A:H)                                                                                                                                                                                                                                                                                                                                                            |
| **Deskripsi**       | Akar masalah fundamental dari vulnerability 1: baris kode `formated_template = template_str.replace('--BALINESE_WELCOME--', name)` dilanjutkan dengan `return render_template_string(formated_template)` menyebabkan nilai `name` dari pengguna disisipkan langsung ke dalam string template sebelum dirender Jinja2. Setiap ekspresi Jinja2 yang ada di dalam `name` akan dievaluasi oleh template. |
| **Dampak**          | Kerentanan ini adalah root cause yang memungkinkan semua jenis SSTI. Tidak ada blacklist yang dapat secara efektif mencegah SSTI selama `render_template_string` dipanggil pada konten yang mengandung input pengguna.                                                                                                                                                                               |
| **Saran Perbaikan** | Redesain arsitektur template: gunakan `render_template()` dengan file `.html` statis dan passing nama sebagai variabel konteks. Jinja2 secara otomatis melakukan HTML-escape pada variabel konteks sehingga ekspresi template tidak bisa diinjeksikan.                                                                                                                                               |

**Proof Of Concept**
1. Akses endpoint: `POST http://43.129.35.148:7000/welcome`
![[Screenshot_20260509_180743.png]]
2. Kirim payload Jinja2 paling sederhana sebagai name: `{{7*7}}`
![[Screenshot_20260509_183838.png]]
3. Jika respons mengandung `49`, server rentan terhadap SSTI
![[Screenshot_20260509_183848.png]]
4. Dari sini, penyerang dapat mengeksplorasi objek yang tersedia dan menemukan jalur eksekusi kode


### 2.2 - Server-Side Template Injection (SSTI) via Blacklist Bypass

| Kategori | Keterangan |
| :--- | :--- |
| **Severity** | **Critical** |
| **CVSS** | 9.8 (AV:N/AC:L/PR:N/UI:N/S:U/C:H/I:H/A:H) |
| **Deskripsi** | Aplikasi menerapkan blacklist untuk mencegah kata-kata berbahaya seperti `os`, `sys`, `popen`, dan lainnya. Namun mekanisme ini hanya memeriksa parameter form `name`. Penyerang dapat melewati blacklist dengan menyisipkan kata-kata terlarang melalui query parameter URL (`request.args`) dan mereferensikannya di dalam payload template Jinja2. Karena `render_template_string()` dipanggil pada template yang sudah mengandung input pengguna, ekspresi template dievaluasi penuh sehingga terjadi Remote Code Execution. |
| **Dampak** | RCE sebagai user proses web di dalam container Docker. Penyerang dapat membaca file sembarang, mengenumerasi environment, dan mengeksfiltrasi data sensitif termasuk flag. |
| **Saran Perbaikan** | Hapus filter `\| safe` dari template Jinja2 agar auto-escaping aktif. Jika HTML diperlukan, gunakan library sanitasi seperti `bleach` atau `nh3` dengan allowlist tag ketat. Hapus `unsafe-inline` dari CSP dan gunakan nonce-based CSP. |

**Proof of Concept**
1. Pada source code terdapat array berisi list kata yang diblacklist dari input. 
![[Screenshot_20260509_212627.png]]
2. Dari vulnerability sebelumnya, dapat diketahui bahwa tidak ada filtering lain selain array blacklist tersebut. Karena itu, input masih bisa di bypass dengan memanfaatkan `request.args`, yaitu menyisipkan keyword terlarang melalui query parameter URL menggunakan Burp Suite untuk mengintercept lalu memodifikasi parameter dan request body sebelum request dikirim ke server. 
![[Screenshot_20260509_212604.png]]
3. Dengan cara ini, kita berhasil menjalankan command seperti `ls /` pada server target.
![[Screenshot_20260509_212546.png]]
4. Dari hasil `ls /`, kita bisa ketahui nama file dari flag adalah `63d93520-5ff9-404e-b262-7ba4e9d8bac1`, setelah itu tinggal jalankan command `cat 63d93520-5ff9-404e-b262-7ba4e9d8bac1`.
![[Screenshot_20260509_212438.png]]
5. Dan kita telah berhasil mendapatkan flagnya.
![[Screenshot_20260509_212444.png]]

---

## 3 Discovered Flag

> **`NETICS{come_visit_bali_sometimes_fb97e764-ea5e-4567-aba2-c0782d932111}`**