Source : https://en.wikipedia.org/wiki/SQL_injection

**SQL injection** adalah teknik _code injection_ yang digunakan untuk menyerang aplikasi berbasis data (_data-driven applications_), di mana pernyataan SQL yang berbahaya dimasukkan ke dalam bidang entri (_entry field_) untuk dieksekusi (misalnya untuk membuang isi _database_ kepada penyerang). _SQL injection_ harus mengeksploitasi _security vulnerability_ pada perangkat lunak aplikasi, misalnya, ketika _user input_ tidak disaring dengan benar untuk _escape characters_ dari _string literal_ yang disematkan dalam pernyataan SQL, atau _user input_ tidak bersifat _strongly typed_ dan dieksekusi secara tak terduga. _SQL injection_ sebagian besar dikenal sebagai _attack vector_ untuk situs web tetapi dapat digunakan untuk menyerang jenis _SQL database_ apa pun.

Serangan _SQL injection_ memungkinkan penyerang untuk melakukan _spoofing_ identitas, merusak data yang ada, menyebabkan masalah repudiasi seperti membatalkan transaksi atau mengubah saldo, memungkinkan pengungkapan lengkap atas semua data di sistem, menghancurkan data atau membuatnya tidak tersedia, dan menjadi administrator dari _database server_. _NoSQL databases_ yang berorientasi dokumen juga dapat terpengaruh oleh _security vulnerability_ ini.

_SQL injection_ tetap menjadi _security risk_ yang diakui secara luas karena potensinya untuk membahayakan data sensitif. _Open Web Application Security Project_ (OWASP) mendeskripsikannya sebagai kerentanan yang terjadi ketika aplikasi membangun _database queries_ menggunakan _user input_ yang tidak divalidasi. Dengan mengeksploitasi celah ini, penyerang dapat mengeksekusi perintah _database_ yang tidak diinginkan, yang berpotensi mengakses, memodifikasi, atau menghapus data. OWASP menguraikan beberapa strategi mitigasi, termasuk _prepared statements_, _stored procedures_, dan _input validation_, untuk mencegah _user input_ disalahartikan sebagai _SQL code_ yang dapat dieksekusi.

## History

Diskusi mengenai _SQL injection_ dimulai pada akhir tahun 1990-an, termasuk dalam sebuah artikel tahun 1998 di majalah _Phrack_. _SQL injection_ menduduki peringkat dalam 10 _web application vulnerabilities_ teratas tahun 2007 dan 2010 oleh _Open Web Application Security Project_ (OWASP). Pada tahun 2013, _SQL injection_ terdaftar sebagai _web application vulnerability_ paling kritis dalam _OWASP Top 10_.

Pada tahun 2017, _OWASP Top 10 Application Security Risks_ mengelompokkan _SQL injection_ ke dalam kategori yang lebih luas yaitu "_Injection_", dan menempatkannya sebagai ancaman keamanan paling kritis ketiga. Kategori ini mencakup berbagai jenis serangan _injection_, seperti SQL, NoSQL, _OS command_, dan _LDAP injection_. Kerentanan ini muncul ketika sebuah aplikasi memproses _untrusted data_ sebagai bagian dari sebuah perintah atau _query_, yang berpotensi memungkinkan penyerang untuk mengeksekusi tindakan yang tidak diinginkan atau mendapatkan _unauthorized access_ ke data.

Menjelang tahun 2021, _injection_ tetap menjadi masalah yang tersebar luas, terdeteksi di 94% aplikasi yang dianalisis, dengan tingkat insiden yang dilaporkan mencapai hingga 19%. _OWASP Top 10_ pada tahun tersebut semakin memperluas definisi _injection vulnerabilities_ untuk mencakup serangan yang menargetkan sistem _Object Relational Mapping_ (ORM), _Expression Language_ (EL), dan _Object Graph Navigation Library_ (OGNL). Untuk mengatasi risiko ini, OWASP merekomendasikan strategi-strategi seperti menggunakan _secure APIs_, _parameterized queries_, _input validation_, dan melakukan _escaping_ pada karakter-karakter khusus untuk mencegah _malicious data_ dieksekusi sebagai bagian dari sebuah _query_.

## Root cause

_SQL injection_ adalah _security vulnerability_ umum yang muncul akibat membiarkan data yang dipasok oleh penyerang menjadi _SQL code_. Hal ini terjadi ketika pemrogram merakit _SQL queries_ baik melalui _string interpolation_ maupun dengan menggabungkan (_concatenating_) perintah SQL dengan data yang dipasok oleh pengguna. Oleh karena itu, _injection_ bergantung pada fakta bahwa pernyataan SQL terdiri dari data yang digunakan oleh pernyataan SQL tersebut serta perintah yang mengontrol bagaimana pernyataan SQL itu dieksekusi. Sebagai contoh, dalam pernyataan SQL `select * from person where name = 'susan' and age = 2`, _string_ `'susan'` adalah data dan fragmen `and age = 2` adalah contoh dari sebuah perintah (nilai `2` juga merupakan data dalam contoh ini).

_SQL injection_ terjadi ketika _user input_ yang dirancang secara khusus diproses oleh program penerima dengan cara yang memungkinkan input tersebut keluar dari _data context_ dan memasuki _command context_. Hal ini memungkinkan penyerang untuk mengubah struktur pernyataan SQL yang dieksekusi.

Sebagai contoh sederhana, bayangkan bahwa data `'susan'` dalam pernyataan di atas disediakan oleh _user input_. Pengguna memasukkan _string_ `'susan'` (tanpa tanda kutip) ke dalam _text entry field_ pada formulir web, dan program menggunakan pernyataan _string concatenation_ untuk membentuk pernyataan SQL di atas dari tiga fragmen: `select * from person where name='`, _user input_ berupa `'susan'`, dan `' and age = 2`.

Sekarang bayangkan alih-alih memasukkan `'susan'`, penyerang memasukkan `' or 1=1; --`.

Program akan menggunakan pendekatan _string concatenation_ yang sama dengan 3 fragmen `select * from person where name='`, _user input_ berupa `' or 1=1; --`, dan `' and age = 2` lalu membangun pernyataan `select * from person where name='' or 1=1; --' and age = 2`. Banyak _database_ akan mengabaikan teks setelah _string_ `--` karena ini menandakan sebuah komentar (_comment_). Struktur perintah SQL sekarang menjadi `select * from person where name='' or 1=1;` dan ini akan memilih semua baris (_rows_) orang alih-alih hanya yang bernama 'susan' dengan usia 2 tahun. Penyerang telah berhasil membuat sebuah _data string_ yang keluar dari _data context_ dan memasuki _command context_.

## Ways to exploit

Meskipun akar penyebab semua _SQL injections_ adalah sama, terdapat teknik-teknik yang berbeda untuk mengeksploitasinya. Beberapa di antaranya dibahas di bawah ini:

### Getting direct output or action

Bayangkan sebuah program membuat pernyataan SQL menggunakan perintah _string assignment_ berikut:

JavaScript

```
var statement = "SELECT * FROM users WHERE name = '" + userName + "'";
```

_SQL code_ ini dirancang untuk menarik _records_ dari _username_ yang ditentukan dari tabel pengguna. Namun, jika variabel `userName` dibuat sedemikian rupa oleh pengguna jahat, pernyataan SQL dapat melakukan lebih dari yang dimaksudkan oleh pembuat kode. Misalnya, mengatur variabel `userName` sebagai:

```
' OR '1'='1
```

atau menggunakan komentar untuk memblokir sisa _query_ (ada tiga jenis komentar SQL). Ketiga baris ini memiliki spasi di akhir:

```
' OR '1'='1' --
' OR '1'='1' {
' OR '1'='1' /* 
```

menghasilkan salah satu pernyataan SQL berikut oleh bahasa induknya:

SQL

```
SELECT * FROM users WHERE name = '' OR '1'='1';
SELECT * FROM users WHERE name = '' OR '1'='1' -- ';
```

Jika kode ini digunakan dalam prosedur otentikasi maka contoh ini dapat digunakan untuk memaksa pemilihan setiap _data field_ (*) dari _semua_ pengguna alih-alih dari satu nama pengguna tertentu seperti yang dimaksudkan oleh _coder_, karena evaluasi dari `'1'='1'` selalu bernilai benar (_true_).

Nilai `userName` berikut dalam pernyataan di bawah ini akan menyebabkan penghapusan tabel `users` serta pemilihan semua data dari tabel `userinfo` (pada dasarnya mengungkapkan informasi setiap pengguna), menggunakan _API_ yang memungkinkan _multiple statements_:

`a'; DROP TABLE users; SELECT * FROM userinfo WHERE 't' = 't`

Input ini menjadikan pernyataan SQL akhirnya seperti berikut dan ditentukan:

SQL

```
SELECT * FROM users WHERE name = 'a';DROP TABLE users; SELECT * FROM userinfo WHERE 't' = 't';
```

Sementara sebagian besar implementasi _SQL server_ mengizinkan _multiple statements_ untuk dieksekusi dengan satu panggilan dengan cara ini, beberapa _SQL APIs_ seperti fungsi `mysql_query()` milik PHP tidak mengizinkan hal ini karena alasan keamanan. Ini mencegah penyerang untuk menyuntikkan _queries_ yang sepenuhnya terpisah, namun tidak menghentikan mereka dari memodifikasi _queries_.

### Blind SQL injection

_Blind SQL injection_ digunakan ketika sebuah aplikasi web rentan terhadap _SQL injection_, tetapi hasil dari injeksi tersebut tidak terlihat oleh penyerang. Halaman yang memiliki kerentanan tersebut mungkin bukan halaman yang menampilkan data, tetapi akan menampilkan hal yang berbeda tergantung pada hasil dari pernyataan logis yang disuntikkan ke dalam pernyataan SQL sah yang dipanggil untuk halaman tersebut. Jenis serangan ini secara tradisional dianggap memakan waktu karena pernyataan baru perlu dirancang untuk setiap _bit_ yang dipulihkan, dan bergantung pada strukturnya, serangan tersebut mungkin terdiri dari banyak _requests_ yang tidak berhasil. Kemajuan terbaru telah memungkinkan setiap _request_ untuk memulihkan _multiple bits_, tanpa ada _requests_ yang gagal, sehingga memungkinkan ekstraksi yang lebih konsisten dan efisien. Ada beberapa _tools_ yang dapat mengotomatiskan serangan ini setelah lokasi kerentanan dan informasi target telah ditetapkan.

#### Conditional responses

Salah satu jenis _blind SQL injection_ memaksa _database_ untuk mengevaluasi sebuah pernyataan logis pada layar aplikasi biasa. Sebagai contoh, sebuah situs web ulasan buku menggunakan _query string_ untuk menentukan ulasan buku mana yang akan ditampilkan. Jadi _URL_ `[https://books.example.com/review?id=5](https://books.example.com/review?id=5)` akan menyebabkan server menjalankan _query_

SQL

```
SELECT * FROM bookreviews WHERE ID = '5';
```

dari mana ia akan mengisi halaman ulasan tersebut dengan data dari ulasan ber-_ID_ 5, yang disimpan di dalam tabel `bookreviews`. _Query_ tersebut terjadi sepenuhnya di server; pengguna tidak mengetahui nama _database_, tabel, atau _fields_, pengguna juga tidak mengetahui _query string_ tersebut. Pengguna hanya melihat bahwa URL di atas mengembalikan sebuah ulasan buku. Seorang _hacker_ dapat memuat URL `[https://books.example.com/review?id=5](https://books.example.com/review?id=5)' OR '1'='1` dan `[https://books.example.com/review?id=5](https://books.example.com/review?id=5)' AND '1'='2`, yang mungkin menghasilkan _queries_

SQL

```
SELECT * FROM bookreviews WHERE ID = '5' OR '1'='1';
SELECT * FROM bookreviews WHERE ID = '5' AND '1'='2';
```

berturut-turut. Jika ulasan asli dimuat dengan URL "1=1" dan halaman kosong atau _error_ dikembalikan dari URL "1=2", dan halaman yang dikembalikan tersebut belum dibuat untuk memperingatkan pengguna bahwa inputnya tidak valid, atau dengan kata lain, telah ditangkap oleh _input test script_, maka situs tersebut kemungkinan rentan terhadap serangan _SQL injection_ karena _query_ tersebut kemungkinan telah berhasil lolos dalam kedua kasus tersebut. _Hacker_ dapat melanjutkan dengan _query string_ ini yang dirancang untuk mengungkapkan nomor versi MySQL yang berjalan di server: `[https://books.example.com/review?id=5](https://books.example.com/review?id=5) AND substring(@@version, 1, INSTR(@@version, '.') - 1)=4`, yang akan menampilkan ulasan buku pada server yang menjalankan MySQL 4 dan halaman kosong atau _error_ jika tidak. _Hacker_ dapat terus menggunakan kode di dalam _query strings_ untuk mencapai tujuan mereka secara langsung, atau untuk mengumpulkan lebih banyak informasi dari server dengan harapan menemukan jalur serangan lainnya.

### Second-order SQL injection

_Second-order SQL injection_ terjadi ketika sebuah aplikasi hanya melindungi SQL-nya dari _immediate user input_, tetapi memiliki kebijakan yang kurang ketat ketika berhadapan dengan data yang sudah tersimpan di dalam sistem. Oleh karena itu, meskipun aplikasi semacam itu berhasil memproses _user input_ dengan aman dan menyimpannya tanpa masalah, aplikasi tersebut akan menyimpan pernyataan SQL yang berbahaya itu juga. Kemudian, ketika bagian lain dari aplikasi tersebut menggunakan data tersebut dalam sebuah _query_ yang tidak terlindungi dari _SQL injection_, pernyataan berbahaya ini mungkin akan tereksekusi. Serangan ini membutuhkan lebih banyak pengetahuan tentang bagaimana nilai-nilai yang dikirimkan tersebut nantinya digunakan. _Automated web application security scanners_ tidak akan dengan mudah mendeteksi jenis _SQL injection_ ini dan mungkin perlu diinstruksikan secara manual di mana mereka harus memeriksa bukti bahwa hal itu sedang dicoba.

Untuk melindungi dari jenis serangan ini, semua pemrosesan SQL harus diamankan secara seragam, apa pun sumber datanya.

## SQL injection mitigation

_SQL injection_ adalah serangan terkenal yang dapat dimitigasi dengan langkah-langkah keamanan yang sudah mapan. Namun, sebuah _cyberattack_ pada tahun 2015 terhadap perusahaan telekomunikasi Inggris TalkTalk mengeksploitasi kerentanan _SQL injection_, membahayakan data pribadi dari sekitar 400.000 pelanggan. BBC melaporkan bahwa para pakar keamanan menyatakan keterkejutannya bahwa sebuah perusahaan besar masih rentan terhadap eksploitasi semacam itu.

Ada berbagai tindakan defensif untuk memitigasi risiko _SQL injection_ dengan mencegah penyerang menyuntikkan _malicious SQL code_ ke dalam _database queries_. Strategi mitigasi inti, seperti yang diuraikan oleh OWASP, meliputi _parameterized queries_, _input validation_, dan kontrol akses _least privilege_, yang membatasi kemampuan _user input_ untuk mengubah _SQL queries_ dan mengeksekusi perintah yang tidak diinginkan. Selain tindakan pencegahan, teknik deteksi membantu mengidentifikasi potensi percobaan _SQL injection_. Metode-metode seperti _pattern matching_, _software testing_, dan _grammar analysis_ memeriksa struktur _query_ dan _user inputs_ untuk mendeteksi ketidakwajaran yang mungkin mengindikasikan adanya upaya _injection_.

### Core mitigation

#### Parameterized statements

Sebagian besar platform pengembangan mendukung _parameterized statements_, yang juga dikenal sebagai _placeholders_ atau _bind variables_, untuk menangani _user input_ secara aman alih-alih menyematkannya ke dalam _SQL queries_. _Placeholders_ ini hanya menyimpan nilai dari tipe yang ditentukan, mencegah input untuk mengubah struktur _query_. Akibatnya, upaya _SQL injection_ diproses sebagai input yang tidak terduga alih-alih kode yang dapat dieksekusi. Dengan _parameterized queries_, _SQL code_ tetap terpisah dari _user input_, dan setiap parameter diteruskan sebagai nilai yang berbeda, mencegahnya ditafsirkan sebagai bagian dari pernyataan SQL.

#### Allow-list input validation

_Allow-list input validation_ memastikan bahwa hanya input yang secara eksplisit didefinisikan yang diterima, mengurangi risiko serangan _injection_. Tidak seperti _deny-lists_, yang mencoba memblokir pola-pola berbahaya yang diketahui namun bisa di-_bypass_, _allow-lists_ menentukan input yang valid dan menolak hal-hal lainnya. Pendekatan ini sangat efektif untuk _structured data_, seperti tanggal dan alamat email, di mana aturan validasi yang ketat dapat diterapkan. Meskipun _input validation_ saja tidak dapat mencegah _SQL injection_ dan serangan lainnya, hal ini dapat bertindak sebagai pengamanan tambahan dengan mengidentifikasi dan menyaring input yang tidak sah sebelum mencapai sebuah _SQL query_.

#### Least privilege

Menurut OWASP, _principle of least privilege_ membantu memitigasi risiko _SQL injection_ dengan memastikan bahwa akun-akun _database_ hanya memiliki _permissions_ minimum yang diperlukan. Akun _read-only_ tidak boleh memiliki _modification privileges_, dan akun aplikasi tidak boleh sama sekali memiliki _administrative access_. Membatasi _database permissions_ adalah bagian utama dari pendekatan ini, karena membatasi akses ke tabel-tabel sistem dan membatasi _user roles_ dapat mengurangi risiko serangan _SQL injection_. Memisahkan _database users_ untuk fungsi-fungsi yang berbeda, seperti otentikasi dan modifikasi data, semakin membatasi potensi kerusakan akibat serangan _SQL injection_.

Membatasi _database permissions_ pada _database login_ milik aplikasi web semakin mengurangi dampak dari kerentanan _SQL injection_. Memastikan bahwa akun-akun hanya memiliki akses yang diperlukan, seperti membatasi _SELECT permissions_ pada tabel sistem yang kritis, dapat memitigasi eksploitasi yang potensial.

Pada Microsoft SQL Server, membatasi akses `SELECT` ke tabel sistem dapat mencegah serangan _SQL injection_ yang mencoba memodifikasi skema _database_ atau menyuntikkan _malicious scripts_. Sebagai contoh, _permissions_ berikut membatasi seorang _database user_ untuk mengakses objek sistem:

Transact-SQL

```
deny select on sys.sysobjects to webdatabaselogon;
deny select on sys.objects to webdatabaselogon;
deny select on sys.tables to webdatabaselogon;
deny select on sys.views to webdatabaselogon;
deny select on sys.packages to webdatabaselogon;
```

### Supplementary mitigation

#### Object relational mappers

_Frameworks Object-relational mapping_ (ORM) menyediakan sebuah _object-oriented interface_ untuk berinteraksi dengan _relational databases_. Meskipun ORM biasanya menawarkan perlindungan bawaan terhadap _SQL injection_, mereka masih bisa rentan jika tidak diimplementasikan dengan benar. Beberapa _queries_ yang dihasilkan oleh ORM mungkin mengizinkan _unsanitized input_, sehingga menimbulkan risiko _injection_. Selain itu, banyak ORM yang memungkinkan para pengembang untuk mengeksekusi _raw SQL queries_, yang jika ditangani dengan tidak semestinya dapat memunculkan kerentanan _SQL injection_.

### Deprecated/secondary approaches

_String escaping_ pada umumnya tidak disarankan sebagai pertahanan utama terhadap _SQL injection_. OWASP menggambarkan pendekatan ini sebagai sesuatu yang "rapuh dibandingkan dengan pertahanan lain" dan mencatat bahwa hal itu mungkin tidak efektif dalam semua situasi. Sebagai gantinya, OWASP merekomendasikan penggunaan "_parameterized queries_, _stored procedures_, atau semacam _Object Relational Mapper_ (ORM) yang membangun _queries_ untuk Anda" sebagai metode yang lebih andal untuk memitigasi risiko _SQL injection_.

#### String escaping

Salah satu cara tradisional untuk mencegah _injections_ adalah dengan menambahkan _setiap bagian data sebagai quoted string_ dan melakukan _escape_ pada semua karakter, yang memiliki arti khusus dalam _SQL strings_, di dalam data tersebut. Manual untuk sebuah _SQL DBMS_ menjelaskan karakter mana saja yang memiliki arti khusus, yang memungkinkan pembuatan _blacklist_ komprehensif atas karakter-karakter yang memerlukan terjemahan. Misalnya, setiap kemunculan kutipan tunggal (`'`) di dalam parameter _string_ harus diawali dengan garis miring terbalik (`\`) sehingga _database_ memahami bahwa kutipan tunggal tersebut adalah bagian dari suatu _string_, bukan sebagai terminatornya. Modul MySQLi milik PHP menyediakan fungsi `mysqli_real_escape_string()` untuk melakukan _escape strings_ sesuai dengan semantik MySQL; dalam contoh berikut, _username_ adalah parameter _string_, dan oleh karena itu ia dapat dilindungi melalui _string escaping_:

PHP

```
$mysqli = new mysqli('hostname', 'db_username', 'db_password', 'db_name');
$query = sprintf("SELECT * FROM `Users` WHERE UserName='%s'",
                  $mysqli->real_escape_string($username),
$mysqli->query($query);
```

Selain itu, tidak semua data dapat ditambahkan ke SQL sebagai _string literal_ (contohnya argumen klausa `LIMIT` MySQL atau nama tabel/kolom) dan dalam kasus ini melakukan _escaping_ pada karakter khusus yang terkait _string_ tidak akan memberikan manfaat apa pun, sehingga SQL yang dihasilkan tetap terbuka terhadap _injections_.

## Examples

- Pada bulan Februari 2002, Jeremiah Jacks menemukan bahwa Guess.com rentan terhadap serangan _SQL injection_, yang memungkinkan siapa saja yang dapat menyusun URL secara tepat untuk menarik lebih dari 200.000 nama, nomor kartu kredit, dan tanggal kedaluwarsa dalam _customer database_ situs tersebut.
    
- Pada tanggal 1 November 2005, seorang peretas remaja menggunakan _SQL injection_ untuk membobol situs majalah keamanan informasi Taiwan dari grup Tech Target dan mencuri informasi pelanggan.
    
- Pada tanggal 13 Januari 2006, penjahat komputer Rusia membobol situs web pemerintah Rhode Island dan diduga mencuri data kartu kredit dari individu yang telah melakukan bisnis _online_ dengan lembaga negara bagian tersebut.
    
- Pada 19 September 2007 dan 26 Januari 2009 grup peretas Turki "m0sted" menggunakan _SQL injection_ untuk mengeksploitasi SQL Server Microsoft guna meretas server web masing-masing milik Pangkalan Amunisi Angkatan Darat McAlester dan Korps Insinyur Angkatan Darat AS.
    
- Pada tanggal 13 April 2008, Registri Pelanggar Seksual dan Kekerasan Oklahoma menutup situs webnya untuk "pemeliharaan rutin" setelah diberi tahu bahwa 10.597 Nomor Jaminan Sosial milik pelanggar seksual telah diunduh melalui serangan _SQL injection_.
    
- Pada 17 Agustus 2009, Departemen Kehakiman Amerika Serikat mendakwa seorang warga negara Amerika, Albert Gonzalez, dan dua orang Rusia yang tidak disebutkan namanya atas pencurian 130 juta nomor kartu kredit menggunakan serangan _SQL injection_. Dalam apa yang dilaporkan sebagai "kasus pencurian identitas terbesar dalam sejarah Amerika", pria tersebut mencuri kartu dari sejumlah korban korporat setelah meneliti sistem pemrosesan pembayaran mereka. Di antara perusahaan yang terkena dampaknya adalah pemroses kartu kredit Heartland Payment Systems, jaringan toko serba ada 7-Eleven, dan jaringan supermarket Hannaford Brothers.
    
- Pada bulan Juli 2010, seorang peneliti keamanan Amerika Selatan yang menggunakan _handle_ "Ch Russo" memperoleh informasi pengguna yang sensitif dari situs BitTorrent populer The Pirate Bay. Ia mendapatkan akses ke panel kontrol administratif situs dan mengeksploitasi kerentanan _SQL injection_ yang memungkinkannya mengumpulkan informasi akun pengguna, termasuk _IP addresses_, _password hashes_ MD5, dan catatan _torrents_ mana yang telah diunggah oleh pengguna individu.
    
- Dari 24 hingga 26 Juli 2010, penyerang dari Jepang dan Tiongkok menggunakan _SQL injection_ untuk mendapatkan akses ke data kartu kredit pelanggan dari Neo Beat, sebuah perusahaan berbasis di Osaka yang menjalankan situs supermarket _online_ besar. Serangan tersebut juga memengaruhi tujuh mitra bisnis termasuk jaringan supermarket Izumiya Co, Maruetsu Inc, dan Ryukyu Jusco Co. Pencurian data memengaruhi 12.191 pelanggan yang dilaporkan. Dilaporkan bahwa telah terjadi lebih dari 300 kasus informasi kartu kredit digunakan oleh pihak ketiga untuk membeli barang dan jasa di Tiongkok.
    
- Pada tanggal 19 September selama pemilihan umum Swedia 2010, seorang pemilih mencoba sebuah _code injection_ dengan menuliskan perintah SQL dengan tangan sebagai bagian dari pemungutan suara _write-in_.
    
- Pada 8 November 2010, situs web Royal Navy Inggris dikompromikan oleh seorang peretas Rumania bernama TinKode menggunakan _SQL injection_.
    
- Pada tanggal 11 April 2011, Barracuda Networks dikompromikan menggunakan kelemahan _SQL injection_. Alamat email dan nama pengguna dari karyawan termasuk di antara informasi yang diperoleh.
    
- Selama periode 4 jam pada tanggal 27 April 2011, serangan _SQL injection_ otomatis terjadi di situs web Broadband Reports yang mampu mengekstrak 8% pasangan nama pengguna/kata sandi: 8.000 akun acak dari 9.000 akun aktif dan 90.000 akun lama atau tidak aktif.
    
- Pada tanggal 1 Juni 2011, kelompok _hacktivists_ LulzSec dituduh menggunakan _SQL injection_ untuk mencuri kupon, kunci unduhan, dan kata sandi yang disimpan dalam _plaintext_ pada situs web Sony, mengakses informasi pribadi satu juta pengguna.
    
- Pada bulan Juni 2011, PBS diretas oleh LulzSec, kemungkinan besar melalui penggunaan _SQL injection_; proses penuh yang digunakan oleh peretas untuk mengeksekusi _SQL injections_ dijelaskan di blog Imperva.
    
- Pada bulan Juli 2012 sebuah kelompok peretas dilaporkan telah mencuri 450.000 kredensial _login_ dari Yahoo!. _Logins_ tersebut disimpan dalam bentuk _plain text_ dan diduga diambil dari subdomain Yahoo, Yahoo! Voices. Grup tersebut menembus keamanan Yahoo dengan menggunakan "teknik _union-based SQL injection_".
    
- Pada 1 Oktober 2012, kelompok peretas bernama "Team GhostShell" menerbitkan catatan pribadi dari para mahasiswa, fakultas, karyawan, dan alumni dari 53 universitas, termasuk Harvard, Princeton, Stanford, Cornell, Johns Hopkins, dan Universitas Zurich di pastebin.com. Para peretas mengklaim bahwa mereka mencoba untuk "meningkatkan kesadaran terhadap perubahan yang terjadi dalam pendidikan saat ini", meratapi perubahan undang-undang pendidikan di Eropa dan kenaikan biaya kuliah di Amerika Serikat.
    
- Pada tanggal 4 November 2013, grup peretas "RaptorSwag" diduga mengkompromikan 71 _databases_ pemerintah Tiongkok menggunakan serangan _SQL injection_ pada Kamar Dagang Internasional Tiongkok. Data yang bocor tersebut diunggah secara publik bekerja sama dengan Anonymous.
    
- Pada bulan Agustus 2014, perusahaan keamanan komputer yang berbasis di Milwaukee, Hold Security, mengungkapkan bahwa mereka menemukan pencurian informasi rahasia dari hampir 420.000 situs web melalui _SQL injections_. The New York Times mengonfirmasi temuan ini dengan mempekerjakan seorang pakar keamanan untuk memeriksa klaim tersebut.
    
- Pada bulan Oktober 2015, serangan _SQL injection_ digunakan untuk mencuri detail pribadi dari 156.959 pelanggan dari server milik perusahaan telekomunikasi Inggris TalkTalk, mengeksploitasi kerentanan pada _legacy web portal_.
    
- Pada awal 2021, 70 gigabita data di-_exfiltrate_ dari situs web sayap kanan Gab melalui serangan _SQL injection_. Kerentanan tersebut dimasukkan ke dalam _codebase_ Gab oleh Fosco Marotto, CTO Gab. Serangan kedua terhadap Gab diluncurkan minggu berikutnya menggunakan _OAuth2 tokens_ yang dicuri selama serangan pertama.
    
- Pada bulan Mei 2023, serangan _SQL injection_ yang meluas menargetkan MOVEit, sebuah layanan transfer fail yang banyak digunakan. Serangan tersebut, yang dikaitkan dengan kelompok penjahat dunia maya berbahasa Rusia, Clop, membahayakan beberapa organisasi global, termasuk penyedia penggajian Zellis, British Airways, BBC, dan peritel Inggris Boots. Para penyerang mengeksploitasi kerentanan kritis, memasang sebuah _webshell_ kustom bernama "LemurLoot" untuk dengan cepat mengakses dan melakukan _exfiltration_ terhadap volume data yang besar.
    
- Pada tahun 2024, sepasang peneliti keamanan menemukan kerentanan _SQL injection_ dalam sistem FlyCASS, yang digunakan oleh Transportation Security Administration (TSA) untuk memverifikasi anggota kru maskapai penerbangan. Mengeksploitasi kelemahan ini memberikan akses administratif yang tidak sah, yang berpotensi memungkinkan penambahan catatan kru palsu. TSA menyatakan bahwa prosedur verifikasi mereka tidak semata-mata bergantung pada _database_ ini.
    

## In popular culture

- Kartun _xkcd_ tahun 2007 melibatkan karakter bernama `Robert'); DROP TABLE Students;--` untuk melakukan sebuah _SQL injection_. Sebagai hasil dari kartun ini, _SQL injection_ terkadang secara informal disebut sebagai "Bobby Tables".
    
- Akses masuk yang tidak sah ke situs web melalui _SQL injection_ membentuk dasar salah satu subplot dalam novel tahun 2012 karya J.K. Rowling, _The Casual Vacancy_.
    
- Pada tahun 2014, seorang individu di Polandia secara legal mengganti nama bisnisnya menjadi `Dariusz Jakubowski x'; DROP TABLE users; SELECT '1` dalam upaya untuk mengganggu operasi _harvesting bots_ milik para _spammers_.
    
- Permainan _Hacknet_ (2015) memiliki program peretasan yang disebut SQL_MemCorrupt. Ini digambarkan sebagai menyuntikkan entri tabel yang menyebabkan _corruption error_ di dalam _SQL database_, kemudian melakukan _query_ pada tabel tersebut, yang menyebabkan kerusakan _SQL database_ dan _core dump_.