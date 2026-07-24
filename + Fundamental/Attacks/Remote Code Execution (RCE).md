Source: https://www.invicti.com/learn/remote-code-execution-rce

Eksekusi kode jarak jauh (_remote code execution_/RCE) adalah salah satu kerentanan paling berbahaya dalam keamanan siber. Saat dieksploitasi, hal ini memungkinkan penyerang untuk menjalankan kode arbitrer pada sistem target, sering kali dengan hak istimewa (_privileges_) yang sama dengan aplikasi yang rentan itu sendiri. Dalam banyak kasus, ini bisa berarti kompromi sistem secara penuh.

Serangan eksekusi kode jarak jauh sering kali merupakan hasil dari kerentanan injeksi (_injection vulnerabilities_) atau penanganan input tidak tepercaya (_untrusted input_) yang tidak aman dan dapat diubah menjadi senjata dalam hitungan jam setelah kerentanan diungkapkan. Penyerang mengeksploitasi sistem yang rentan dalam skala besar menggunakan eksploit RCE otomatis dan _threat intelligence feeds_ untuk mengidentifikasi target yang terekspos secara _real-time_. Konsekuensinya dapat berupa penyebaran _ransomware_, pelanggaran data (_data breaches_), akses tidak sah ke sistem internal, dan pergerakan lateral melintasi infrastruktur _cloud_.

Serangan RCE tingkat tinggi dalam beberapa tahun terakhir mengilustrasikan risikonya. Kerentanan Log4Shell pada Apache Log4j, sebuah _library_ pencatatan (_logging_) Java yang banyak digunakan, memungkinkan eksekusi kode arbitrer di ribuan organisasi. React2Shell, kerentanan eksekusi kode jarak jauh yang lebih baru dan berdampak pada implementasi berbasis React tertentu, menunjukkan bagaimana penyerang mengeksploitasi kerentanan injeksi dalam ekosistem JavaScript modern. Dalam kasus lain, kelemahan _zero-day_ kritis pada perangkat lunak perusahaan telah memungkinkan peretas untuk mendapatkan akses ke informasi sensitif dan menyebarkan _backdoors_ sebelum _patches_ (tambalan) tersedia.

### Apa itu eksekusi kode jarak jauh (RCE)?

Eksekusi kode jarak jauh (RCE) adalah kerentanan keamanan yang memungkinkan penyerang mengeksekusi kode arbitrer pada sistem jarak jauh melalui koneksi jaringan, tanpa memerlukan akses fisik.

Kerentanan eksekusi kode jarak jauh paling sering ditargetkan pada aplikasi web, API, atau layanan yang terekspos ke jaringan. Saat penyerang mengeksploitasi kerentanan yang memungkinkan RCE, mereka dapat menjalankan perintah sistem operasi, memodifikasi logika aplikasi, memasang _malware_, atau mengekstrak informasi sensitif. Karena eksekusi kode arbitrer memberikan kendali langsung atas suatu sistem, RCE diklasifikasikan sebagai tingkat keparahan kritis (_critical severity_) dalam model risiko keamanan aplikasi.

Secara praktis, serangan eksekusi kode jarak jauh yang berhasil sering kali berujung pada kompromi server secara penuh dan menciptakan jalur untuk serangan siber yang lebih luas.

### Bagaimana penyerang mencapai eksekusi kode jarak jauh

Kerentanan eksekusi kode jarak jauh dapat timbul dari penanganan input tidak tepercaya yang tidak aman, integrasi komponen pihak ketiga yang tidak aman, atau masalah kerusakan memori (_memory corruption_). Vektor serangan umum meliputi:

- **Insecure deserialization**: Kerentanan _deserialization_ memungkinkan penyerang menyediakan objek berbahaya yang mengeksekusi kode selama rekonstruksi dan terjadi saat aplikasi memproses data berseri (_serialized data_) tanpa validasi input yang ketat.
    
- **Command injection dan code injection**: Jika input pengguna diteruskan langsung ke perintah sistem atau dievaluasi secara dinamis, penyerang mungkin dapat menyuntikkan instruksi berbahaya ke dalamnya. _Code injection_ dan bahkan _SQL injection_ terkadang dapat meningkat menjadi serangan eksekusi kode jarak jauh secara penuh jika aplikasi yang rentan mengizinkan eksekusi perintah tingkat sistem (_system-level_).
    
- **Penyalahgunaan unggah file (_File upload abuse_)**: Validasi file unggahan yang tidak tepat dapat memungkinkan penyerang mengunggah skrip yang dapat dieksekusi, menimpa file yang ada, atau membuat _backdoors_ di dalam sistem yang rentan.
    
- **Buffer overflows dan memory corruption**: Dalam bahasa tingkat rendah (_lower-level languages_), _buffer overflow_ atau akses memori di luar batas (_out-of-bounds_) dapat memungkinkan penyerang untuk menimpa memori dan mengarahkan ulang aliran eksekusi. Teknik ini telah digunakan dalam eksploitasi historis seperti WannaCry dan serangan siber berskala besar lainnya yang menargetkan sistem yang rentan.
    
- **Vulnerable dependencies dan kerentanan yang diketahui (_known vulnerabilities_)**: Pustaka (_libraries_), _frameworks_, atau komponen yang sudah ketinggalan zaman mungkin mengandung kerentanan yang telah diketahui yang dapat dieksploitasi penyerang dalam skala besar. Saat proses penambalan (_patching_) tertunda, dependensi yang rentan tersebut dapat mengekspos aplikasi ke RCE.
    

Dalam sebagian besar kasus, penyerang mengeksploitasi kombinasi dari validasi input yang lemah, kontrol akses yang tidak memadai, dan proses penambalan yang tidak tuntas. Dependensi yang banyak digunakan merupakan target yang sangat menarik.

Perlu dicatat bahwa beberapa serangan RCE dapat terjadi dengan adanya penundaan. Misalnya, aplikasi mungkin terlebih dahulu menyimpan _payload_ RCE dalam file konfigurasi dan baru mengeksekusinya di kemudian hari, yang berpotensi terjadi berkali-kali. Jenis kerentanan RCE ini disebut _stored RCE_.

### Apa yang dapat dilakukan penyerang setelah memperoleh RCE

Eksekusi kode jarak jauh jarang menjadi tujuan akhir, melainkan sebuah batu loncatan untuk eksploitasi lebih lanjut. Setelah penyerang mencapai eksekusi kode jarak jauh, mereka berpotensi untuk:

- Menyebarkan _web shells_, _reverse shells_, atau _backdoors_ tersembunyi
    
- Membangun akses tak sah secara persisten (_persistent unauthorized access_)
    
- Mengekstrak _credentials_, _API tokens_, dan informasi sensitif lainnya
    
- Melakukan eskalasi hak istimewa (_privilege escalation_) untuk mendapatkan akses administratif atau _root_
    
- Bergerak secara lateral (_move laterally_) ke sistem rentan lainnya
    
- Menonaktifkan pencatatan log (_logging_) atau memicu kondisi _denial of service_ (DoS) untuk menghindari deteksi
    
- Menyebarkan _ransomware_ atau _malware_ eksfiltrasi data
    

Dalam lingkungan _cloud-native_, penyerang dapat melakukan _pivot_ dari satu aplikasi yang rentan ke layanan penyimpanan (_storage services_), jalur pipa CI/CD, atau sistem identitas.

### Mengapa RCE sangat berbahaya dalam lingkungan modern

Arsitektur aplikasi modern dapat meningkatkan kemungkinan maupun dampak dari serangan eksekusi kode jarak jauh, dan untuk berbagai alasan:

- **Ketergantungan pada komponen dan _frameworks_ umum**: Serangan rantai pasokan (_supply-chain attacks_) memungkinkan penyerang mengeksploitasi RCE dalam skala masif setelah komponen yang rentan diungkapkan.
    
- **Beban kerja terdistribusi dan terkontainerisasi (_Containerized and distributed workloads_)**: Kerentanan RCE dalam sebuah _container_ dapat memungkinkan penyerang lolos dari isolasi (_escape isolation_), mengakses sistem orkestrasi (_orchestration systems_), atau mengkompromikan layanan tambahan.
    
- **Eksposur CI/CD dan rantai pasokan**: Jika penyerang mengeksploitasi kerentanan pada jalur pipa pembangunan (_build pipelines_), mereka dapat menyuntikkan kode berbahaya ke dalam rilis produksi – mengubah sebuah serangan siber menjadi kompromi rantai pasokan.
    
- **Penyebaran _secrets_ dan identitas (_Secrets and identity sprawl_)**: Aplikasi sering kali menyimpan _cloud credentials_ dan kunci API (_API keys_) dalam _environment variables_. RCE menyediakan akses langsung ke informasi sensitif ini.
    
- **Permukaan serangan yang meluas (_Expanding attack surface_)**: Layanan mikro (_Microservices_), API, dan aplikasi yang berhadapan dengan internet menciptakan banyak vektor serangan. Tanpa pemindaian kerentanan (_vulnerability scanning_) dan pengujian keamanan (_security testing_) yang berkelanjutan, kerentanan eksekusi kode jarak jauh mungkin tetap tidak terdeteksi.
    

Perlu dicatat bahwa, dalam beberapa kasus, sifat terdistribusi dari aplikasi berbasis _cloud_ yang lazim mungkin pada kenyataannya dapat membatasi radius ledakan (_blast radius_) dari RCE yang berhasil dengan membatasi kompromi hanya pada satu _container_ atau beban kerja.

### Beberapa insiden RCE tingkat tinggi (High-profile RCE incidents)

- **Log4Shell (CVE-2021-44228)**: Kerentanan injeksi JNDI kritis pada Apache Log4j yang memungkinkan eksekusi kode arbitrer pada server yang terekspos. Eksploitasi dimulai dalam beberapa hari setelah pengungkapan dan menyebabkan pelanggaran data secara luas di berbagai industri.
    
- **React2Shell (CVE-2025-55182)**: Kerentanan eksekusi kode jarak jauh yang berdampak pada implementasi _server-side rendering_ berbasis React tertentu. Penyerang mengeksploitasi kelemahan injeksi untuk mencapai eksekusi kode arbitrer pada aplikasi yang rentan.
    
- **WannaCry (CVE-2017-0144 / EternalBlue)**: Wabah _ransomware_ yang menyertakan kerentanan eksekusi kode jarak jauh pada protokol SMB Microsoft dalam rantai serangannya. Eksploit _wormable_ tersebut memungkinkan penyebaran yang cepat ke seluruh sistem yang rentan, menyebabkan gangguan global.
    
- **Microsoft Exchange Server (CVE-2021-26855 and related ProxyLogon chain)**: Serangkaian kerentanan _zero-day_ yang memungkinkan penyerang memperoleh akses tidak sah dan mengeksekusi kode pada server Exchange _on-premises_ sebelum _patches_ diterapkan secara luas.
    

### Cara mendeteksi dan mencegah kerentanan RCE

Mencegah serangan eksekusi kode jarak jauh memerlukan kombinasi antara _secure coding_, kontrol keamanan aplikasi yang berlapis, dan pengujian keamanan yang berkesinambungan.

#### Praktik pengkodean yang aman (_Secure coding practices_)

- Terapkan validasi input yang ketat pada semua data yang disediakan pengguna
    
- Hindari fungsi evaluasi dinamis (_dynamic evaluation functions_) yang tidak aman pada Java, PHP, dan bahasa pemrograman lainnya
    
- Terapkan prinsip hak istimewa paling rendah (_principle of least privilege_) untuk mengurangi dampak jika terjadi kompromi sistem
    
- Implementasikan kontrol akses dan autentikasi yang kuat
    

#### Manajemen dependensi dan _patch_

- Pantau _threat intelligence feeds_ untuk kerentanan yang telah diketahui
    
- Terapkan _patching_ tepat waktu untuk menghilangkan paparan terhadap eksploit RCE
    
- Simpan inventaris yang akurat mengenai komponen pihak ketiga
    
- Gunakan analisis komposisi perangkat lunak (_software composition analysis_) untuk mengidentifikasi sistem yang rentan
    

#### Kontrol perlindungan tambahan

- Sebarkan _web application firewalls_ (WAF) atau solusi keamanan serupa untuk mengurangi eksposur
    
- Konfigurasikan WAF Anda untuk mendeteksi upaya injeksi dan pola serangan RCE yang umum
    
- Pastikan tanda tangan WAF (_WAF signatures_) Anda sering diperbarui untuk mengikuti perkembangan ancaman baru
    
- Pantau sistem dan log untuk aktivitas eksekusi perintah yang tidak normal
    
- Pelihara rencana respons insiden (_incident response plan_) yang efektif
    

#### Pengujian keamanan dinamis (_Dynamic security testing_)

Pengujian keamanan aplikasi yang sistematis menggunakan perangkat statis maupun dinamis sangat penting untuk mengidentifikasi dan menghilangkan peluang bagi RCE. Namun, analisis statis (_static analysis_) saja tidak dapat mengonfirmasi apakah kerentanan tersebut benar-benar dapat dieksploitasi, yang menjadikan pengujian keamanan dinamis (baik pemindai DAST otomatis maupun uji penetrasi/_penetration testing_ manual) sangat penting untuk menyimulasikan bagaimana penyerang dapat mengeksploitasi kerentanan seperti RCE pada aplikasi yang sedang berjalan.

Pendekatan _DAST-first_ terhadap pemindaian kerentanan memberikan visibilitas waktu nyata (_runtime visibility_) atas risiko RCE nyata yang dapat dieksploitasi. Teknik _proof-based scanning_ modern dapat secara otomatis memvalidasi kerentanan eksekusi kode jarak jauh tertentu secara aman, yang membantu tim memprioritaskan masalah yang telah terkonfirmasi dan melakukan perbaikan secara efisien.

Mintalah demo _proof-of-concept_ untuk melihat bagaimana platform keamanan aplikasi _DAST-first_ dari Invicti dapat membantu Anda mengidentifikasi dan memulihkan ribuan kerentanan kritis – termasuk RCE.