Source: https://www.invicti.com/learn/local-file-inclusion-lfi

_Local file inclusion_ (LFI) tetap menjadi _web vulnerability_ yang umum karena banyak aplikasi memuat file secara dinamis berdasarkan _user input_, mulai dari _templates_ dan gambar hingga _configuration files_ dan modul. Ketika input tersebut tidak divalidasi dengan benar, penyerang dapat memanipulasinya untuk mengakses file yang tidak semestinya pada _web server_.

Dampaknya sering kali diremehkan dan dianggap "hanya sekadar _file read_". Apa yang berawal sebagai akses file sederhana dapat dengan cepat mengekspos informasi sensitif seperti _credentials_, _API keys_, dan _application logic_. Dari sana, penyerang dapat melakukan eskalasi untuk mengakses _backend systems_, melakukan _pivot_ ke _cloud services_, atau menggabungkannya (_chain_) dengan kelemahan lain untuk mendapatkan _remote code execution_.

_Attack path_ (jalur serangan) yang lazim adalah penyerang membaca file `.env` atau memeriksa file sistem seperti `/etc/passwd` untuk memahami _environment_ Anda, mengekstrak _credentials_, dan menggunakan informasi tersebut untuk mengakses _databases_ atau infrastruktur. Dalam _environments_ modern, hal ini dapat mencakup _environment variables_ atau _cloud tokens_ serta _API tokens_, yang membuka risiko dari _local file inclusion vulnerability_ meningkat menjadi kompromi sistem yang lebih luas.

### Apa itu _local file inclusion_ (LFI)?

_Local file inclusion_ (LFI) adalah _web vulnerability_ di mana sebuah aplikasi menggunakan _user-controlled input_ yang belum disanitasi dan divalidasi (_unsanitized and unvalidated_) untuk meminta dan mengakses file. LFI yang berhasil dapat memungkinkan penyerang untuk membaca _arbitrary files_ pada server, yang mengakibatkan _information disclosure_. Dalam beberapa kasus, LFI dapat digabungkan (_chained_) dengan kelemahan lain untuk mengeksekusi _malicious code_. Perhatikan bahwa tidak seperti _remote file inclusion_ (RFI), LFI hanya mengakses file yang sudah ada pada _local system_.

### Bagaimana serangan LFI bekerja pada aplikasi nyata

Berikut adalah gambaran tingkat tinggi tentang bagaimana penyerang mungkin menyelidiki dan mengeksploitasi _local file inclusion vulnerabilities_.

#### _Entry point_: _User-controlled file paths_

Banyak _web applications_ memuat file secara dinamis berdasarkan parameter yang diteruskan pada saat _runtime_. Contoh penggunaan perilaku tersebut meliputi pemilihan halaman atau _template_, fitur _file download_ atau _preview_, tampilan gambar atau dokumen, atau komponen aplikasi modular.

Sebuah skrip PHP rentan yang lazim, yang memuat file berdasarkan nilai parameter mentah (_raw parameter_), mungkin terlihat seperti ini:

PHP

```
<?php
$file = $_GET['file'];
include($file);
?>
```

Jika input tidak dibatasi, penyerang dapat memasok _arbitrary paths_ dan memanipulasinya seperti yang dijelaskan pada langkah berikutnya. Perhatikan bahwa _user-controlled input_ dapat berasal dari banyak tempat selain _form fields_ yang paling jelas, termasuk _query parameters_, _cookies_, _headers_, atau nilai seperti _User-Agent header_.

Pendekatan yang lebih aman mungkin dengan menghindari penggunaan langsung dari _user input_ dengan mengandalkan _controlled mappings_. Contoh berikut mendefinisikan sebuah _allowlist_ dari nama halaman dan _file paths_ yang sesuai, dengan hanya nama halaman yang dikontrol oleh _user_:

PHP

```
<?php
$allowed = ['home' => 'home.php', 'about' => 'about.php'];
$page = $_GET['page'] ?? 'home';
if (array_key_exists($page, $allowed)) {
   include(__DIR__ . '/pages/' . $allowed[$page]);
} else {
   http_response_code(404);
}
?>
```

Meskipun sering dikaitkan dengan PHP, masalah akses file serupa dapat terjadi dalam bahasa lain, seperti Python (`send_file`), Node.js (`fs.readFile`), atau pemuatan _resource_ di Java ketika _user input_ tidak divalidasi dengan benar.

#### Eksploitasi: Penyerang memanipulasi _path_

Penyerang mengeksploitasi _LFI vulnerabilities_ menggunakan _path traversal_ (juga dikenal sebagai _directory traversal_) dan teknik terkait. Sebuah _payload_ sederhana yang disertakan dalam _query parameter_ mungkin terlihat seperti:

`?page=../../../../etc/passwd`

Teknik-teknik umum meliputi:

- _Path traversal_ menggunakan urutan seperti `../`
    
- _Encoded payloads_ untuk melewati (_bypass_) penyaringan (misalnya, `%2e%2e%2f`)
    
- _Null byte injection_ (`%00`) di beberapa _environments_ lama (PHP sebelum 5.3.4)
    
- Penyalahgunaan (_Abusing_) _PHP wrappers_ seperti `php://filter`, `php://input`, atau `data://`
    

_PHP wrappers_ pada khususnya memberikan banyak kemungkinan. Sebagai contoh penyalahgunaan `php://filter`, penyerang mungkin dapat menggunakan filter _Base64 encoding_ untuk membaca _source code_ dari sebuah file PHP tanpa mengeksekusinya:

`?file=php://filter/convert.base64-encode/resource=index.php`

_Wrappers_ lain seperti `php://input` dan `data://` lebih berbahaya karena memungkinkan penyerang untuk memasok konten file (bukan hanya _path_) secara langsung dalam _request body_ atau URL. Hal ini dapat mengubah _LFI vulnerability_ menjadi _remote code execution_ tanpa perlu menggunakan teknik seperti _log poisoning_ atau _file uploads_, karena aplikasi mungkin secara langsung menyertakan (_include_) dan mengeksekusi _attacker-controlled input_ sebagai kode PHP.

Seperti halnya banyak serangan lain, _basic sanitization_ atau _blocklists_ mungkin dapat menangkap beberapa _exploits_ tetapi tidak pernah menjadi perlindungan yang memadai dengan sendirinya – penyerang dapat melewati (_bypass_) metode ini menggunakan _encoding_, trik pemotongan (_truncation tricks_), atau representasi _path_ alternatif.

#### Pengintaian (_Recon_): Pembacaan file sensitif dan eksposur data

Setelah _path_ berhasil dikontrol, penyerang dapat mencoba mengambil file sensitif spesifik-_environment_ seperti:

- `/etc/passwd` dan file sistem lainnya di Linux
    
- _Application files_ di bawah `/var/www`
    
- _Configuration files_ yang berisi _credentials_
    
- _Logs_ seperti `/var/log/apache2/access.log` atau `error.log`
    
- _Runtime data_ seperti `/proc/self/environ` yang dapat mengekspos _environment variables_ dan _secrets_
    

Pada tahap ini, penyerang memperoleh wawasan tentang aplikasi, ketergantungannya (_dependencies_), dan _execution environment_-nya.

#### Eskalasi: Menggabungkan (_Chaining_) LFI menjadi kompromi yang lebih besar

_Information disclosure_ sudah cukup berbahaya, tetapi penyerang dapat meningkatkan eskalasi dari sekadar mengumpulkan data menjadi menggunakannya untuk serangan lain. _Escalation paths_ yang umum meliputi:

- LFI ke _sensitive data exposure_ dengan mengekstrak _credentials_ dan _secrets_
    
- LFI ke _cross-site scripting_ (XSS) dengan menyertakan HTML atau JavaScript yang merupakan _attacker-controlled_
    
- LFI ke _remote code execution_ (RCE) dengan menyertakan _malicious file_ seperti _web shell_
    

Karena LFI terbatas pada file yang disimpan secara lokal, serangan yang lebih canggih memerlukan beberapa cara untuk menempatkan _attacker-controlled file_ pada server. Dua teknik umum yang digunakan terhadap aplikasi PHP adalah:

- _Log poisoning_ dengan menyuntikkan (_injecting_) _malicious PHP code_ ke dalam _web server logs_ (misalnya melalui _User-Agent header_) dan kemudian menyertakan _logfile_ seperti `/var/log/apache2/access.log`
    
- Menyalahgunakan fitur _file upload_ dengan mengunggah _malicious PHP file_ dan memaksa aplikasi untuk menyertakannya
    

Dalam kedua kasus tersebut, penyerang mungkin dapat mengubah _file read access_ menjadi eksekusi kode PHP di server.

### Apa yang dicari penyerang dengan LFI

Meskipun terkadang diremehkan sebagai kelemahan berisiko rendah, _local file inclusion_ dapat mengekspos berbagai macam sumber daya (_resources_) sensitif, termasuk:

- **Environment and secrets files:** File seperti `.env` sering kali berisi _database credentials_, _API keys_, dan _cloud tokens_.
    
- **Framework and application configuration:** _Configuration files_ menyimpan _connection strings_, sandi autentikasi (_authentication secrets_), dan _internal endpoints_.
    
- **Source code and application logic:** Akses ke _source code_ dapat mengungkapkan fungsionalitas tersembunyi dan _vulnerabilities_ tambahan.
    
- **Logs and writable files:** _Logs_ dan direktori unggahan (_upload directories_) sangat berharga untuk melakukan _chaining attacks_, terutama dalam skenario _log poisoning_.
    
- **Cloud and container-era targets:** _Environments_ modern memperkenalkan target bernilai tinggi yang dapat memberikan akses langsung ke _cloud infrastructure_, seperti _cloud credential files_, _container-mounted secrets_, dan _Kubernetes service account tokens_.
    

### LFI vs. kerentanan terkait

#### LFI vs. remote file inclusion (RFI)

Dalam serangan LFI, file disertakan (_included_) dari _local server_. Dalam RFI, aplikasi memuat file dari sumber eksternal (_external source_), yang sering kali memungkinkan eksekusi kode langsung (_direct code execution_). Namun, LFI terkadang dapat diekskalasi hingga memberikan dampak serupa.

#### LFI vs. path traversal

_Path traversal_ memungkinkan penyerang untuk mengakses file yang tidak ditujukan untuk akses _user_ dengan memanipulasi _file paths_. LFI mengacu pada penyertaan (_inclusion_) atau akses file yang tidak aman dalam _application logic_. Kedua masalah ini sering tumpang tindih dan memiliki akar penyebab (_root cause_) yang sama – _input validation_ yang tidak memadai dan penanganan file yang tidak tepat. Definisinya mungkin bervariasi, tetapi dalam praktiknya, LFI dan _path traversal_ sering muncul bersamaan.

### Dampak dunia nyata dari kerentanan LFI

_LFI vulnerabilities_ dapat memiliki konsekuensi bisnis yang serius, termasuk:

- Eksposur informasi sensitif
    
- Kompromi dari _credentials_ dan _backend systems_
    
- _Unauthorized access_ ke infrastruktur
    
- Pengambilalihan server penuh (_Full server takeover_) melalui _chained attacks_
    
- Pelanggaran kepatuhan (_Compliance violations_) dan kerusakan reputasi (_reputational damage_)
    

Sebagai contoh, _vulnerabilities_ dalam komponen seperti TimThumb memungkinkan penyerang untuk membaca _arbitrary files_ dan mengeksekusi kode, yang mengakibatkan kompromi situs web secara luas. Masalah serupa telah mengekspos _configuration files_ dan _credentials_, memungkinkan penyerang untuk melakukan _pivot_ ke _databases_ dan _backend services_.

### Cara mencegah kerentanan LFI

Tidak ada satu perbaikan pun yang akan mencegah semua _LFI vectors_. Terapkan praktik terbaik (_best practices_) berikut untuk meminimalkan risiko _local file inclusion_ yang berhasil:

- **Hindari _dynamic file includes_:** Jangan gunakan _user input_ secara langsung untuk menentukan file mana yang akan dimuat. Alihkan nilai input ke _known resources_ sebagai gantinya.
    
- **Gunakan _allowlists_ alih-alih _blocklists_:** Batasi akses file menggunakan _whitelist_ (_allowlist_) dari nilai-nilai yang diizinkan. _Blocklists_ tidak efektif sebagai perlindungan satu-satunya karena pada akhirnya penyerang biasanya dapat melewatinya.
    
- **Gunakan referensi tidak langsung (_indirect references_):** Ganti nama file langsung dengan pengidentifikasi internal (_internal identifiers_) yang diselesaikan di server.
    
- **Lakukan _normalize_ dan _validate paths_ dengan cermat:** Lakukan _canonicalize_ pada _file paths_ dan tegakkan batas-batas direktori. Sadarilah bahwa _encoding_, pemotongan (_truncation_), atau format _path_ campuran dapat melewati logika _validation_ yang lemah jika pemeriksaan tidak diterapkan secara konsisten.
    
- **Batasi _file access_ dan perizinan (_permissions_):** Terapkan prinsip _least-privilege_, pisahkan direktori _writable_ dan _executable_, tegakkan _file permissions_ yang ketat, dan gunakan kontrol seperti `open_basedir` di lingkungan PHP. Mekanisme isolasi seperti _containers_ atau lingkungan _chroot_ dapat lebih membatasi dampak jika terjadi eksploitasi.
    
- **Patch dan perbarui _dependencies_:** Perbarui pustaka (_libraries_) dan kerangka kerja (_frameworks_) yang rentan. Sebuah _web application firewall_ (WAF) dapat membantu memblokir _traversal payloads_ umum dan pola serangan yang diketahui, tetapi tidak dapat secara andal menghentikan semua varian, terutama ketika penyerang menggunakan _encoding_, _application-specific logic_, atau teknik berbasis _wrapper_.
    
- **Uji terus-menerus dalam SDLC:** Gunakan _automated vulnerability scanning_ yang dikombinasikan dengan _penetration testing_ (manual dan agentic) untuk mengidentifikasi masalah LFI dalam lingkungan _development_ dan _production_.
    

### Cara mendeteksi kerentanan LFI

Mendeteksi _local file inclusion vulnerability_ dengan meyakinkan memerlukan pengujian bagaimana aplikasi berperilaku pada saat _runtime_. Untuk perangkat lunak rentan yang diketahui dengan laporan CVE, pemeriksaan versi menggunakan alat SCA dapat mengidentifikasi masalah yang diketahui. Untuk aplikasi kustom, Anda memerlukan pengujian yang ditargetkan pada logika penanganan file (_file-handling logic_).

_Static analysis_ menggunakan alat SAST adalah langkah pertama yang berharga tetapi sering kali tidak cukup jika berdiri sendiri karena tidak dapat menentukan dengan andal bagaimana _user input_ diselesaikan ke dalam _file paths_ selama eksekusi. Sebagai bagian dari _code review_, pengembang (_developers_) harus mencari _dangerous sinks_ di mana _user input_ mengalir tanpa validasi yang tepat, misalnya `include`, `require`, atau `file_get_contents` di PHP, dan fungsi akses file serupa dalam bahasa lain.

_Automated vulnerability scanning_ pada saat _runtime_ adalah cara paling andal untuk mengidentifikasi _LFI vulnerabilities_ yang dapat diakses.

### Bagaimana pemindai otomatis mendeteksi LFI

Alat _Dynamic application security testing_ (DAST) mengidentifikasi LFI dengan berinteraksi dengan aplikasi yang sedang berjalan. Hal ini mencakup melakukan perayapan (_crawling_) pada aplikasi untuk menemukan input, menyuntikkan _payloads_ yang mencoba membaca _local files_, dan menganalisis respons untuk mencari bukti adanya akses file.

Alat tingkat lanjut (_Advanced tools_) seperti Invicti DAST dapat menggunakan _proof-based scanning_ untuk mengonfirmasi kemampuan eksploitasi dan memberikan bukti mengenai dampaknya. Hal ini mengurangi _false positives_ dan membantu tim keamanan (_security teams_) fokus pada _vulnerabilities_ nyata yang dapat dieksploitasi daripada risiko teoretis. Pelajari selengkapnya tentang pendekatan _DAST-first_ Invicti yang memprioritaskan apa yang benar-benar dapat dieksploitasi oleh penyerang, dan minta demo untuk melihat bagaimana alat ini dapat membantu Anda mengurangi risiko nyata dengan lebih cepat – untuk LFI dan ribuan _vulnerabilities_ lainnya.