Source: https://en.wikipedia.org/wiki/Markov_chain

Dalam teori probabilitas dan statistika, **rantai Markov** (atau **proses Markov**) adalah proses stokastik yang mendeskripsikan urutan kemungkinan kejadian di mana probabilitas setiap kejadian hanya bergantung pada keadaan yang dicapai pada kejadian sebelumnya. Secara informal, hal ini dapat dibayangkan sebagai, "Apa yang terjadi selanjutnya hanya bergantung pada keadaan _saat ini_." Sebuah urutan tak terhingga yang dapat dihitung, di mana rantai berpindah keadaan pada langkah-langkah waktu diskrit, disebut rantai Markov waktu-diskrit (DTMC). Sedangkan proses waktu-kontinu disebut rantai Markov waktu-kontinu (CTMC). Proses Markov dinamai untuk menghormati matematikawan Rusia Andrey Markov.

Rantai Markov memiliki banyak aplikasi sebagai model statistik dari proses dunia nyata. Mereka memberikan dasar untuk metode simulasi stokastik umum yang dikenal sebagai Monte Carlo rantai Markov (MCMC), yang digunakan untuk menyimulasikan pengambilan sampel dari distribusi probabilitas kompleks, dan telah menemukan aplikasi di berbagai bidang termasuk statistika Bayesian, biologi, kimia, ekonomi, keuangan, teori informasi, fisika, pemrosesan sinyal, dan pemrosesan ucapan.

Kata sifat _Markovian_ dan _Markov_ digunakan untuk mendeskripsikan sesuatu yang berkaitan dengan proses Markov.

## Prinsip Dasar

### Definisi

Proses Markov adalah proses stokastik yang memenuhi sifat Markov (terkadang dikarakterisasi sebagai "tanpa memori" atau _memorylessness_). Dalam istilah yang lebih sederhana, ini adalah proses di mana prediksi tentang hasil masa depan dapat dibuat hanya berdasarkan keadaannya saat ini—dan yang terpenting—prediksi tersebut sama baiknya dengan prediksi yang dibuat jika kita mengetahui seluruh riwayat proses tersebut. Dengan kata lain, dengan syarat keadaan sistem saat ini, keadaan masa depan dan masa lalunya adalah independen.

Rantai Markov adalah jenis proses Markov yang memiliki ruang keadaan diskrit atau himpunan indeks diskrit (sering mewakili waktu), namun definisi pasti dari rantai Markov bisa bervariasi. Misalnya, sangat umum untuk mendefinisikan rantai Markov sebagai proses Markov dalam waktu diskrit atau kontinu dengan ruang keadaan yang dapat dihitung, tetapi juga umum untuk mendefinisikan rantai Markov sebagai proses yang memiliki waktu diskrit dalam ruang keadaan yang dapat dihitung atau kontinu.

### Jenis-jenis Rantai Markov

Ruang keadaan dan indeks parameter waktu sistem perlu ditentukan. Tabel berikut memberikan gambaran umum tentang berbagai instansiasi proses Markov untuk tingkat generalitas ruang keadaan yang berbeda, baik untuk waktu diskrit maupun kontinu:

||**Ruang keadaan terhitung (Countable)**|**Ruang keadaan kontinu atau umum**|
|---|---|---|
|**Waktu-diskrit**|Rantai Markov (waktu-diskrit) pada ruang keadaan terhitung atau berhingga|Rantai Markov pada ruang keadaan terukur (misalnya, rantai Harris)|
|**Waktu-kontinu**|Proses Markov waktu-kontinu atau proses lompatan Markov|Setiap proses stokastik kontinu dengan sifat Markov (misalnya, proses Wiener)|

Perlu dicatat bahwa tidak ada kesepakatan definitif dalam literatur mengenai penggunaan beberapa istilah yang menandakan kasus khusus dari proses Markov. Biasanya istilah "rantai Markov" dicadangkan untuk proses dengan kumpulan waktu diskrit (DTMC), tetapi beberapa penulis menggunakan istilah "proses Markov" untuk merujuk pada rantai Markov waktu-kontinu (CTMC) tanpa menyebutkannya secara eksplisit.

### Transisi

Perubahan keadaan sistem disebut transisi. Probabilitas yang terkait dengan berbagai perubahan keadaan disebut probabilitas transisi. Proses ini dikarakterisasi oleh ruang keadaan, matriks transisi yang mendeskripsikan probabilitas transisi tertentu, dan keadaan awal (atau distribusi awal) di seluruh ruang keadaan. Berdasarkan konvensi, kita mengasumsikan bahwa semua kemungkinan keadaan dan transisi telah disertakan dalam definisi proses, sehingga selalu ada keadaan berikutnya, dan proses tidak pernah berhenti.

Karena sistem berubah secara acak, pada umumnya tidak mungkin untuk memprediksi dengan pasti keadaan rantai Markov pada suatu titik di masa depan. Namun, sifat statistik masa depan sistem dapat diprediksi.

## Sejarah

Andrey Markov mempelajari proses Markov pada awal abad ke-20, menerbitkan makalah pertamanya tentang topik ini pada tahun 1906. Proses Markov dalam waktu kontinu ditemukan jauh sebelum karyanya pada awal abad ke-20 dalam bentuk proses Poisson. Markov tertarik untuk mempelajari perluasan dari urutan acak independen, dimotivasi oleh perselisihan dengan Pavel Nekrasov yang mengklaim bahwa independensi diperlukan agar hukum lemah bilangan besar (_weak law of large numbers_) berlaku. Dalam makalah pertamanya tentang rantai Markov, Markov menunjukkan bahwa di bawah kondisi tertentu, hasil rata-rata rantai Markov akan konvergen ke vektor nilai tetap, sehingga membuktikan hukum lemah bilangan besar tanpa asumsi independensi.

Andrei Kolmogorov pada tahun 1931 mengembangkan sebagian besar teori awal proses Markov waktu-kontinu. Kolmogorov terinspirasi sebagian oleh karya Louis Bachelier pada tahun 1900 tentang fluktuasi pasar saham serta karya Norbert Wiener tentang model pergerakan Brownian Einstein. Dia memperkenalkan dan mempelajari kumpulan proses Markov tertentu yang dikenal sebagai proses difusi. Matematikawan lain yang memberikan kontribusi signifikan pada fondasi proses Markov termasuk William Feller (mulai tahun 1930-an) dan Eugene Dynkin (mulai tahun 1950-an).

## Contoh

- **Jalan acak** (_Random walks_) yang berbasis pada bilangan bulat dan masalah kebangkrutan penjudi (_gambler's ruin_) adalah contoh proses Markov. Dua contoh penting lainnya adalah proses Wiener (gerak Brown) dan proses Poisson.
    
- Rantai Markov yang terkenal adalah "jalan pemabuk" (_drunkard's walk_), sebuah jalan acak pada garis bilangan di mana, pada setiap langkah, posisinya dapat berubah sebesar +1 atau -1 dengan probabilitas yang sama.
    
- Serangkaian keadaan independen (misalnya, lemparan koin berulang) memenuhi definisi formal rantai Markov. Namun, teori ini biasanya hanya diterapkan ketika probabilitas distribusi keadaan berikutnya bergantung pada keadaan saat ini.
    

### Contoh Bukan Markov

Misalkan ada sebuah dompet berisi lima koin bernilai 25¢, lima koin 10¢, dan lima koin 5¢. Koin diambil secara acak satu per satu dari dompet dan diletakkan di atas meja. Jika $X_n$ mewakili nilai total koin yang diletakkan di atas meja setelah $n$ kali pengambilan, dengan $X_0 = 0$, maka barisan $\{X_n : n\in\mathbb{N}\}$ _bukanlah_ proses Markov.

Mengapa demikian? Misalkan dalam enam pengambilan pertama, kelima koin 5¢ dan satu koin 25¢ terambil, sehingga $X_6 = \$0.50$. Jika kita tidak hanya mengetahui $X_6$, tetapi juga nilai-nilai sebelumnya, kita dapat mengetahui koin mana saja yang telah terambil, dan kita tahu pasti koin berikutnya bukan 5¢; sehingga kita bisa memastikan $X_7 \geq \$0.60$ dengan probabilitas 1. Namun, jika kita _tidak_ mengetahui riwayat sebelumnya, hanya berdasarkan $X_6 = \$0.50$, kita mungkin menebak bahwa kita telah mengambil empat koin 10¢ dan dua koin 5¢, yang berarti koin 5¢ masih bisa terambil. Jadi, tebakan kita tentang $X_7$ sangat dipengaruhi oleh pengetahuan tentang kejadian sebelum $X_6$.

## Definisi Formal

### Rantai Markov Waktu-Diskrit

Rantai Markov waktu-diskrit adalah urutan variabel acak $X_1, X_2, X_3, \ldots$ dengan sifat Markov, yaitu probabilitas berpindah ke keadaan berikutnya hanya bergantung pada keadaan saat ini dan bukan pada keadaan sebelumnya:

$$\Pr(X_{n+1}=x\mid X_1=x_1, X_2=x_2, \ldots, X_n=x_n) = \Pr(X_{n+1}=x\mid X_n=x_n)$$

dengan asumsi probabilitas bersyarat tersebut terdefinisi dengan baik. Nilai-nilai yang mungkin dari $X_i$ membentuk suatu himpunan terhitung $S$ yang disebut ruang keadaan (_state space_) rantai tersebut.

**Variasi:**

- **Rantai Markov homogen-waktu**: Proses di mana probabilitas transisi tidak bergantung pada $n$.
    
    $$\Pr(X_{n+1}=x\mid X_n=y) = \Pr(X_n = x \mid X_{n-1} = y)$$
    
- **Rantai Markov berorde $m$ (dengan memori)**: Proses di mana keadaan masa depan bergantung pada $m$ keadaan di masa lalu.
    

### Ruang Keadaan Berhingga

Jika ruang keadaan berhingga, distribusi probabilitas transisi dapat direpresentasikan oleh sebuah matriks, yang disebut matriks transisi $\mathbf{P}$, dengan elemen ke-$(i, j)$ sama dengan:

$$p_{ij} = \Pr(X_{n+1}=j\mid X_n=i)$$

Karena jumlah setiap baris matriks $\mathbf{P}$ bernilai satu dan semua elemennya non-negatif, $\mathbf{P}$ adalah matriks stokastik kanan.

**Distribusi Stasioner**

Distribusi stasioner $\pi$ adalah sebuah vektor (baris) dengan elemen non-negatif yang jumlahnya sama dengan 1, dan tidak berubah oleh operasi matriks transisi $\mathbf{P}$. Didefinisikan sebagai:

$$\pi\mathbf{P} = \pi$$

Ini menunjukkan bahwa $\pi$ berelasi dengan vektor eigen kiri dari matriks transisi $\mathbf{P}$ yang memiliki nilai eigen sebesar 1.

### Rantai Markov Waktu-Kontinu

Sebuah rantai Markov waktu-kontinu $(X_t)_{t\geq 0}$ didefinisikan oleh ruang keadaan terbatas atau terhitung $S$, matriks laju transisi $Q$ dengan dimensi yang sama dengan ruang keadaan, dan probabilitas distribusi awal. Untuk $i \neq j$, elemen $q_{ij}$ bersifat non-negatif dan mendeskripsikan laju transisi dari keadaan $i$ ke keadaan $j$.

Jika proses berada pada keadaan $i$ pada waktu $t$, maka saat $h \to 0$:

$$\Pr(X(t+h) = j \mid X(t) = i) = \delta_{ij} + q_{ij}h + o(h)$$

di mana $\delta_{ij}$ adalah delta Kronecker.

## Sifat-sifat

- **Berkomunikasi (Communicate):** Dua keadaan saling berkomunikasi jika keduanya dapat dicapai dari satu sama lain melalui urutan transisi yang memiliki probabilitas positif.
    
- **Tertutup (Closed):** Sebuah kelas keadaan disebut tertutup jika probabilitas meninggalkan kelas tersebut adalah nol.
    
- **Tak-tereduksi (Irreducible):** Sebuah rantai Markov dikatakan tak-tereduksi jika hanya ada satu kelas komunikasi, yaitu seluruh ruang keadaan itu sendiri.
    
- **Periodik/Aperiodik:** Keadaan $i$ memiliki periode $k$ jika $k$ adalah pembagi persekutuan terbesar (FPB) dari jumlah transisi yang diperlukan untuk kembali ke $i$. Jika $k > 1$, keadaan itu _periodik_; jika $k = 1$, disebut _aperiodik_.
    
- **Sementara (Transient) vs Berulang (Recurrent):** Keadaan $i$ bersifat sementara jika ada kemungkinan proses tersebut tidak akan pernah kembali ke $i$. Jika pasti kembali, ia disebut berulang (recurrent).
    
- **Ergodik:** Keadaan $i$ dikatakan ergodik jika bersifat aperiodik dan berulang positif (memiliki rata-rata waktu kembali yang berhingga). Jika seluruh keadaan pada rantai Markov tak-tereduksi adalah ergodik, maka rantai itu disebut rantai ergodik.
    

## Jenis Rantai Markov Khusus

||**Keadaan sistem diamati sepenuhnya**|**Keadaan sistem diamati sebagian**|
|---|---|---|
|**Sistem Otonom**|Rantai Markov|Model Markov Tersembunyi (Hidden Markov Model)|
|**Sistem Terkendali**|Proses Keputusan Markov|Proses Keputusan Markov Teramati Sebagian|

## Aplikasi

Rantai Markov digunakan secara luas di berbagai disiplin ilmu, di antaranya:

- **Fisika:** Sistem Markovian sangat penting dalam termodinamika dan mekanika statistik untuk memodelkan proses yang dinamikanya bergantung pada distribusi acak tanpa memperhitungkan sejarah lampau.
    
- **Kimia:** Model Markov waktu-kontinu digunakan untuk menganalisis jaringan reaksi kimia, seperti dalam kinetika Michaelis-Menten pada enzim.
    
- **Biologi:** Digunakan dalam pemodelan evolusi DNA, bioinformatika, dan model kompartemen dalam penyebaran epidemiologi.
    
- **Teori Informasi & Ilmu Komputer:** Model Rantai Markov merupakan dasar dari perhitungan _PageRank_ Google. Claude Shannon menggunakan proses Markov untuk memodelkan keteraturan statistik bahasa dalam teori informasi (entropi). Algoritma kompresi data juga banyak yang memanfaatkannya.
    
- **Teori Antrean (Queueing Theory):** Sangat penting dalam telekomunikasi untuk memodelkan antrean pesan atau sumber daya jaringan, menggunakan sistem seperti antrean M/M/1.
    
- **Ekonomi & Keuangan:** Rantai Markov digunakan untuk memodelkan siklus bisnis (rezim tinggi/rendah), volatilitas aset, perubahan harga saham, dan probabilitas pergeseran peringkat kredit.
    
- **Pembuatan Teks (Text Generators):** Rantai Markov bisa digunakan untuk menghasilkan teks buatan yang tampak otentik (generator parodi, prediksi teks) dengan menghitung probabilitas transisi sebuah kata dari kata sebelumnya berdasarkan dokumen sampel.