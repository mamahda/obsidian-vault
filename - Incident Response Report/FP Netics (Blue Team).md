[[SQL Injection]] | [[Local File Inclusion (LFI)]] | [[Remote Code Execution (RCE)]]
## Technical Analysis

### Affected Systems & Data
Serangan terjadi dalam tiga fase berurutan dan menargetkan infrastruktur yang dapat diakses dari jaringan publik. Attacker dari IP eksternal `182.8.98.74` berhasil mengakses dan mengeksploitasi tiga sistem secara berurutan.

Berikut adalah sistem-sistem dalam infrastruktur yang diserang:
* **Server Utama:** Server ini menjadi target fase reconnaissance awal. Attacker melakukan enumerasi menggunakan Nmap Scripting Engine untuk mengidentifikasi layanan aktif, endpoint sensitif, dan metode HTTP yang tersedia sebelum bergerak ke target berikutnya.
* **preprod-payroll.trick.htb:** Aplikasi payroll berbasis PHP yang berjalan di lingkungan pre-production namun dapat diakses dari internet publik. Sistem ini mengandung endpoint autentikasi `/ajax.php` yang rentan terhadap SQL Injection.
* **prod-marketing.scenario.naga:** Server produksi aplikasi marketing berbasis PHP. Parameter `page` pada `index.php` digunakan langsung dalam fungsi `include()` tanpa validasi, memungkinkan LFI. Attacker mengeksploitasi akun user `michael` melalui log poisoning untuk mendapatkan eksekusi kode jarak jauh, dan berhasil membaca file `importantCompanyData.csv`.

### Evidence Sources & Analysis

| File Name | Description |
| :--- | :--- |
| `access.log` | Log akses utama yang menunjukkan tahap pemindaian awal (Nmap). |
| `payroll.access.log` | Log akses aplikasi Payroll, merekam aktivitas SQLMap. |
| `payroll.error.log` | Log error PHP, membuktikan keberhasilan eksekusi SQLi. |
| `payroll.postdata.log` | Merekam payload HTTP POST spesifik yang dikirim penyerang ke Payroll. |
| `marketing.access.log` | Log akses aplikasi Marketing, menunjukkan injeksi LFI dan RCE. |
| `marketing.error.log` | Log error PHP aplikasi Marketing, membuktikan akses ke file sistem dan log poisoning. |

## Technical Timeline

| Time | Activity | Log File |
| :--- | :--- | :--- |
| 14:11:40 | Pencarian kerentanan dimulai menggunakan Nmap. | `access.log` |
| 15:01:20 | Serangan SQL Injection otomatis dimulai menggunakan sqlmap pada form login. | `payroll.access.log` |
| 15:14:34 | Akses file `/etc/passwd` berhasil melalui celah LFI. | `marketing.access.log` |
| 15:17:55 | Eksekusi perintah `id` berhasil via Log Poisoning (RCE). | `marketing.access.log` |
| 15:20:16 | Upaya pembuatan koneksi Reverse Shell (Bash) ke IP penyerang. | `marketing.access.log` |

## MITRE ATT&CK Technique Mapping

| Tactic | Technique ID | Technique Name | Observasi |
| :--- | :--- | :--- | :--- |
| Reconnaissance | T1595.002 | Active Scanning: Vuln Scanning | Nmap NSE pada 14:11, probe `/.git/HEAD`, `/robots.txt`, `/HNAP1`, metode HTTP non-standar. |
| Initial Access | T1190 | Exploit Public-Facing App | SQL Injection pada `/ajax.php`. |
| Initial Access | T1190 | Exploit Public-Facing App | Local File Inclusion pada `/index.php?page=` dengan path traversal `....//`. |
| Credential Access | T1110.001 | Brute Force: Password Guessing | sqlmap mengirim ratusan payload per detik ke endpoint login tanpa rate limiting. |
| Discovery | T1083 | File & Directory Discovery | `ls -lah`, `ls -lah ~/`, `cat ~/.bash_logout` - enumerasi struktur file via RCE. |
| Discovery | T1082 | System Info Discovery | `uname`, `uname -a`, `whoami` - pengumpulan info sistem dan identitas proses. |
| Collection | T1005 | Data from Local System | `cat ~/importantCompanyData.csv` - eksfiltrasi data sensitif perusahaan. |
| Execution | T1059.004 | Unix Shell Command Execution | RCE via log poisoning pada `/var/mail/michael` - eksekusi arbitrary OS command. |
| Exfiltration | T1048 | Exfiltration Over Alt Protocol | Percobaan reverse shell ke C2 `194.127.193.93:55555` via `/dev/tcp` dan `nc`. |
| Lateral Movement | T1210 | Exploitation of Remote Services | sqlmap menggunakan `LOAD_FILE()` untuk membaca file sistem server via DB privilege. |

## Indicators of Compromise (IoCs)

* **IP Attacker:** `182.8.98.74`
* **IP Tambahan:** `34.44.29.180`
* **C2:** `194.127.193.93:55555`
* **User-Agent:** sqlmap, curl, Nmap
* **Endpoint:** `/ajax.php?action=login`, `/index.php?page=`
* **Pola:** `....//`

## Nature of the Attack

### Phase 0: Reconnaissance
Pada 14:10:52 UTC, mulai terlihat request awal ke server utama yang mengindikasikan probing. 
![[Screenshot_20260505_213239.png]]
Aktivitas kemudian meningkat pada 14:11:40 UTC ketika attacker menjalankan Nmap scanning, terlihat dari user-agent dan pola request seperti `/nmaplowercheck` serta method HTTP yang tidak umum.
![[Screenshot_20260505_203627.png]]

### Phase 1: SQL Injection
Serangan SQL Injection dimulai pada 15:01:20 UTC oleh IP `34.44.29.180` dengan payload sederhana untuk bypass login. 
![[Screenshot_20260505_211653.png]]

Serangan ini dilakukan secara otomatis menggunakan sqlmap, dengan aktivitas yang mulai terdeteksi secara intensif pada pukul 15:01:20 UTC.
![[Screenshot_20260505_215640.png]]
### Phase 2: LFI + RCE
Pada 15:14:34 UTC, attacker berhasil melakukan LFI pertama dengan membaca `/etc/passwd` di server marketing. Setelah itu, pada rentang 15:14:53 - 15:16:19 UTC, attacker melakukan enumerasi file sistem seperti `/proc/self` dan `/etc/hostname`.
![[Screenshot_20260505_212453.png]]

Pada 15:17:27 UTC, attacker mengakses file `/var/mail/michael`, yang kemudian digunakan untuk mail poisoning. 
![[Screenshot_20260505_213046.png]]
RCE terkonfirmasi pada 15:17:55 UTC, ketika attacker berhasil mengeksekusi command `id`. Aktivitas eksplorasi sistem berlanjut hingga sekitar 15:18 - 15:19 UTC.

![[Screenshot_20260505_213113.png]]
Puncaknya terjadi pada 15:19:59 UTC, ketika file sensitif `importantCompanyData.csv` berhasil diakses. Setelah itu, pada 15:24:02 - 15:32:20 UTC, attacker mencoba beberapa kali membuat reverse shell ke server eksternal, namun tidak berhasil.
![[Screenshot_20260505_212820.png]]

---

## Response and Recovery Analysis

### Tindakan Jangka Pendek (0-24 Jam)
* **ISOLASI**
  * Blokir IP `182.8.98.74`, `34.44.29.180`, dan `194.127.193.93` di firewall/WAF.
  * Nonaktifkan akses publik ke `preprod-payroll.trick.htb` dan `prod-marketing.scenario.naga` sementara investigasi berlangsung.
* **FORENSIK**
  * Backup dan preserve semua log sebelum melakukan perubahan apapun pada sistem.
* **INVESTIGASI**
  * Verifikasi apakah reverse shell sempat berhasil dengan menganalisis network flow ke `194.127.193.93:55555`.
  * Identifikasi isi dan nilai data `importantCompanyData.csv` yang dieksfiltrasi.

### Tindakan Jangka Menengah (24-72 Jam)
* **MITIGASI SQLi**
  * Gunakan prepared statements dengan PDO atau MySQLi.
  * Nonaktifkan `FILE` privilege untuk user database web.
* **MITIGASI LFI**
  * Validasi parameter `page` menggunakan allowlist file yang diizinkan.
  * Aktifkan `open_basedir` di `php.ini`.
* **HARDENING**
  * Implementasikan WAF untuk deteksi SQLi, LFI, dan RCE.
  * Jalankan proses PHP-FPM dengan user dedicated tanpa akses ke `/var/mail` dan home directory pengguna sistem.
* **MONITORING**
  * Aktifkan alerting pada pola akses anomali seperti frekuensi tinggi dari IP tunggal, payload dengan karakter khusus SQL, dan pattern path traversal.

### Tindakan Jangka Panjang (> 1 Minggu)
* **ARSITEKTUR**
  * Pisahkan environment production dan pre-production. Pre-production tidak boleh dapat diakses dari internet publik.
  * Terapkan network segmentation, database server tidak boleh dapat diakses langsung dari web server.
* **PROSES**
  * Security code review wajib sebelum deployment.
  * Security awareness training untuk developer terkait SQLi dan LFI.
* **MONITORING**
  * Deploy SIEM untuk korelasi log lintas sistem dan deteksi anomali secara otomatis.