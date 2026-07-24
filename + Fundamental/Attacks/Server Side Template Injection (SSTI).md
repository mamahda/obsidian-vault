Source: Gemini

**Server-Side Template Injection (SSTI)** adalah celah keamanan aplikasi web yang terjadi ketika input pengguna secara tidak aman digabungkan langsung ke dalam sebuah _template_ di sisi server. Akibatnya, mesin pemroses _template_ (_template engine_) mengevaluasi dan mengeksekusi input tersebut sebagai bagian dari logika kode, bukan menampilkannya sebagai data teks biasa.

Jika kita menarik benang merah dari materi-materi yang sudah dibahas sebelumnya, SSTI memiliki kaitan yang sangat erat dengan konsep-konsep tersebut:

- **Satu rumpun dengan SQL Injection:** Keduanya berakar pada masalah mendasar yang sama, yaitu kegagalan sistem dalam memisahkan antara "data" dan "perintah". Jika SQL Injection memanipulasi kueri basis data, SSTI memanipulasi logika aplikasi pada _backend_.
    
- **Lebih berbahaya dari Local File Inclusion (LFI):** LFI memungkinkan penyerang membaca file lokal yang sudah ada di server atau menyertakan file berbahaya. SSTI jauh lebih fleksibel karena penyerang menyuntikkan ekspresi atau kode yang langsung dieksekusi oleh aplikasi itu sendiri pada saat proses _rendering_ halaman.
    
- **Jalur langsung menuju Remote Code Execution (RCE):** Ini adalah alasan mengapa SSTI sangat mematikan. Pada banyak mesin _template_ modern, penyerang yang berhasil menemukan celah SSTI dapat keluar dari lingkungan yang dibatasi (_sandbox escape_) dan mengeksekusi perintah sistem operasi secara langsung. SSTI adalah salah satu pintu masuk paling umum untuk mendapatkan RCE penuh pada aplikasi web.
    

### Bagaimana SSTI Bekerja

Dalam pengembangan _backend_, pengembang sering menggunakan _template engine_ untuk memisahkan logika presentasi dari logika aplikasi inti. Contoh mesin _template_ ini meliputi Jinja2 (Python), Twig (PHP), FreeMarker (Java), atau `html/template` (Go).

Kerentanan muncul ketika pengembang memasukkan input pengguna langsung ke dalam _string template_ sebelum dikompilasi.

**Contoh Kasus Rentan:**

Misalkan sebuah aplikasi menyapa pengguna menggunakan URL parameter `?name=Gilbran`. Kode rentannya mungkin terlihat seperti ini:

Plaintext

```
template_string = "Halo " + request.GET['name'] + ", selamat datang!"
render(template_string)
```

Jika penyerang mengubah parameter menjadi `?name={{7*7}}`, mesin _template_ tidak akan mencetak teks `{{7*7}}`. Sebaliknya, mesin tersebut akan memproses ekspresi matematika di dalamnya dan menghasilkan _output_:

**Halo 49, selamat datang!**

### Dampak Eksploitasi

Evaluasi matematika sederhana seperti `{{7*7}}` biasanya hanya digunakan pada tahap awal untuk mendeteksi keberadaan celah SSTI. Setelah celah terkonfirmasi, penyerang akan meningkatkan serangan (_escalation_) untuk mencapai tujuan berikut:

1. **Membaca informasi sensitif:** Membaca file konfigurasi, _environment variables_, atau rahasia aplikasi lainnya (seperti serangan LFI).
    
2. **Remote Code Execution (RCE):** Menyuntikkan perintah objek sistem yang memungkinkan penyerang mengambil alih server sepenuhnya.
    

### Cara Mencegah SSTI

1. **Pemisahan Konteks (Context Separation):** Jangan pernah menggabungkan input pengguna langsung ke dalam _string template_. Input harus selalu dilewatkan ke _template_ melalui parameter konteks (variabel) yang sudah disediakan oleh _framework_.
    
2. **Validasi dan Sanitasi Input:** Terapkan prinsip validasi input yang ketat dan pastikan karakter khusus untuk _template_ (seperti `{{`, `}}`, `<%`, `%>`) dibersihkan jika tidak diperlukan.
    
3. **Gunakan Sandboxing:** Konfigurasikan _template engine_ untuk berjalan di lingkungan _sandbox_ yang membatasi akses ke objek sistem, fungsi eksekusi _shell_, dan modul berbahaya lainnya.
    

Apakah kamu ingin melihat contoh spesifik bagaimana _payload_ SSTI sederhana dapat berkembang menjadi eksploit RCE pada sebuah lingkungan _backend_ tertentu?