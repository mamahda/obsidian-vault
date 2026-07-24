Source: Gemini

_Server-Side Request Forgery_ (SSRF) adalah _security vulnerability_ di mana penyerang memanipulasi aplikasi web di sisi server agar melakukan _network request_ (permintaan jaringan) ke domain atau alamat IP arbitrer yang ditentukan oleh penyerang. Berbeda dengan _Local File Inclusion_ (LFI) yang mengeksploitasi sistem file (_file system_) secara lokal, SSRF menyalahgunakan server web untuk menjelajahi dan menyerang jaringan internal maupun eksternal via _network protocols_ (seperti HTTP).

### Bagaimana serangan SSRF bekerja pada aplikasi nyata

Berdasarkan dokumentasi PortSwigger, target eksploitasi SSRF umumnya dibagi ke dalam dua kategori utama:

#### Serangan SSRF ke server itu sendiri (_Targeting the server itself_)

Penyerang memanipulasi aplikasi untuk melakukan _request_ kembali ke server tempat aplikasi tersebut berjalan (biasanya menggunakan _hostname_ seperti `localhost` atau IP `127.0.0.1`).

- **Contoh skenario:** Sebuah fitur toko _online_ mengambil informasi stok barang menggunakan parameter: `stockApi=[http://stock.weliketoshop.net/api/stock](http://stock.weliketoshop.net/api/stock)`
    
- **Eksploitasi:** Penyerang mengubah parameter tersebut menjadi: `stockApi=http://localhost/admin`
    

**Mengapa ini berbahaya?** Sering kali, aplikasi mempercayai _request_ yang datang dari mesin lokal itu sendiri. Kontrol akses (_access controls_) seperti halaman _login_ mungkin dilewati sepenuhnya karena sistem menganggap permintaan ke panel `/admin` yang berasal dari `localhost` adalah tindakan internal yang aman.

#### Serangan SSRF ke sistem _back-end_ lain (_Targeting other back-end systems_)

Server aplikasi web biasanya memiliki akses khusus ke infrastruktur internal (seperti _databases_, _internal servers_, atau _administrative APIs_) yang dilindungi oleh _firewall_ sehingga tidak terekspos langsung ke internet umum.

- **Eksploitasi:** Penyerang menggunakan server yang rentan sebagai _internal proxy_ atau "batu loncatan" untuk memindai dan mengakses alamat IP di jaringan lokal (misalnya `stockApi=[http://192.168.0.68/admin](http://192.168.0.68/admin)`). Ini memungkinkan penyerang untuk berinteraksi dengan _internal systems_ yang seharusnya sama sekali tidak bisa dijangkau dari luar.
    

### Dampak dunia nyata dari kerentanan SSRF

PortSwigger menyoroti bahwa dampak dari SSRF bisa sangat fatal, di antaranya:

- **Akses Tidak Sah (_Unauthorized access_):** Penyerang dapat memotong _access controls_, membaca data rahasia, atau melakukan tindakan administratif yang merusak di dalam jaringan tertutup.
    
- **Kompromi infrastruktur _cloud_ (_Cloud infrastructure compromise_):** Pada lingkungan _cloud_ modern (seperti AWS, GCP, atau Azure), penyerang sering menggunakan SSRF untuk mengambil kredensial sensitif dengan mengakses _metadata endpoints_ (contohnya mengakses URL `[http://169.254.169.254/](http://169.254.169.254/)`).
    
- **Eskalasi ke RCE:** Jika SSRF berhasil menjangkau _internal services_ lain yang memiliki kerentanannya sendiri, hal ini dapat berujung pada kompromi sistem secara penuh atau _Remote Code Execution_ (RCE).
    

### Cara mencegah kerentanan SSRF

Untuk melindungi aplikasi dari _Server-Side Request Forgery_, pengembang harus menerapkan praktik pertahanan secara berlapis (_defense in depth_):

- **Gunakan _allowlists_ yang ketat:** Jangan bergantung pada _blocklists_. Validasi _user input_ hanya terhadap daftar domain, _host_, atau URL yang diizinkan secara eksplisit.
    
- **Hindari pengiriman URL mentah (_raw URLs_):** Jika memungkinkan, jangan biarkan pengguna mengirimkan URL utuh. Alihkan nilai input tersebut menjadi _internal identifiers_ yang dipetakan di sisi server.
    
- **Terapkan _network segmentation_:** Isolasi server aplikasi di dalam jaringan sehingga server tersebut hanya dapat melakukan koneksi keluar (_outbound connections_) ke layanan pihak ketiga yang benar-benar mereka butuhkan.
    
- **Nonaktifkan skema URL yang berbahaya:** Konfigurasikan klien HTTP pada aplikasi untuk hanya menerima skema `http://` dan `https://`. Nonaktifkan skema lain yang sering disalahgunakan dalam eksploitasi SSRF seperti `file://`, `dict://`, `ftp://`, atau `gopher://`.