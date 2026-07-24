[[Markov Chain]] | [[Gaussian Elimination]] | [[Breadth-First Search]]

- [[#1 Pendahuluan|1 Pendahuluan]]
    - [[#1 Pendahuluan#1.1 Latar Belakang|1.1 Latar Belakang]]
    - [[#1 Pendahuluan#1.2 Relevansi dengan Teori Rantai Markov|1.2 Relevansi dengan Teori Rantai Markov]]
    - [[#1 Pendahuluan#1.3 Tujuan Laporan|1.3 Tujuan Laporan]]
- [[#2 Spesifikasi Problem|2 Spesifikasi Problem]]
    - [[#2 Spesifikasi Problem#2.1 Deskripsi Masalah|2.1 Deskripsi Masalah]]
        - [[#2.1 Deskripsi Masalah#Batasan|Batasan]]
        - [[#2.1 Deskripsi Masalah#Format Input/Output|Format Input/Output]]
        - [[#2.1 Deskripsi Masalah#Contoh|Contoh]]
    - [[#2 Spesifikasi Problem#2.2 Definisi Formal|2.2 Definisi Formal]]
    - [[#2 Spesifikasi Problem#2.3 Analisis Struktur Problem|2.3 Analisis Struktur Problem]]
- [[#3 Landasan Teori|3 Landasan Teori]]
    - [[#3 Landasan Teori#3.1 Random Walk sebagai Discrete-Time Markov Chain|3.1 Random Walk sebagai Discrete-Time Markov Chain]]
    - [[#3 Landasan Teori#3.2 Expected Hitting Time dan Sistem Persamaan Linear|3.2 Expected Hitting Time dan Sistem Persamaan Linear]]
    - [[#3 Landasan Teori#3.3 Gaussian Elimination dengan Partial Pivoting|3.3 Gaussian Elimination dengan Partial Pivoting]]
    - [[#3 Landasan Teori#3.4 Breadth-First Search untuk Reachability dan Degree|3.4 Breadth-First Search untuk Reachability dan Degree]]
- [[#4 Analisis Problem: Proses Penemuan Solusi|4 Analisis Problem: Proses Penemuan Solusi]]
    - [[#4 Analisis Problem: Proses Penemuan Solusi#4.1 Observasi Awal|4.1 Observasi Awal]]
    - [[#4 Analisis Problem: Proses Penemuan Solusi#4.2 Eksplorasi Simulasi Langsung dan Kegagalannya|4.2 Eksplorasi Simulasi Langsung dan Kegagalannya]]
    - [[#4 Analisis Problem: Proses Penemuan Solusi#4.3 Penemuan Kunci Transformasi: Dari Rekursi ke Sistem Linear|4.3 Penemuan Kunci Transformasi: Dari Rekursi ke Sistem Linear]]
    - [[#4 Analisis Problem: Proses Penemuan Solusi#4.4 Reformulasi sebagai Masalah Aljabar Linear|4.4 Reformulasi sebagai Masalah Aljabar Linear]]
    - [[#4 Analisis Problem: Proses Penemuan Solusi#4.5 Derivasi Persamaan per Sel|4.5 Derivasi Persamaan per Sel]]
    - [[#4 Analisis Problem: Proses Penemuan Solusi#4.6 Penentuan Struktur Data: Graph dan LinearSystem|4.6 Penentuan Struktur Data: Graph dan LinearSystem]]
    - [[#4 Analisis Problem: Proses Penemuan Solusi#4.7 Optimasi: Inline Degree Computation dan Partial Pivoting|4.7 Optimasi: Inline Degree Computation dan Partial Pivoting]]
- [[#5 Pembuktian Kebenaran Algoritma|5 Pembuktian Kebenaran Algoritma]]
    - [[#5 Pembuktian Kebenaran Algoritma#5.1 Teorema Utama|5.1 Teorema Utama]]
    - [[#5 Pembuktian Kebenaran Algoritma#5.2 Bukti Eksistensi dan Ketunggalan Solusi|5.2 Bukti Eksistensi dan Ketunggalan Solusi]]
    - [[#5 Pembuktian Kebenaran Algoritma#5.3 Bukti Kebenaran Konstruksi Sistem Persamaan|5.3 Bukti Kebenaran Konstruksi Sistem Persamaan]]
- [[#6 Pseudokode|6 Pseudokode]]
    - [[#6 Pseudokode#6.1 Penjelasan Alur Algoritma|6.1 Penjelasan Alur Algoritma]]
    - [[#6 Pseudokode#6.2 Catatan Implementasi Kritis|6.2 Catatan Implementasi Kritis]]
- [[#7 Implementasi C++|7 Implementasi C++]]
    - [[#7 Implementasi C++#7.1 Kode Lengkap|7.1 Kode Lengkap]]
    - [[#7 Implementasi C++#7.2 Analisis Baris per Baris|7.2 Analisis Baris per Baris]]
        - [[#7.2 Analisis Baris per Baris#7.2.1 Class LinearSystem|7.2.1 Class LinearSystem]]
        - [[#7.2 Analisis Baris per Baris#7.2.2 Class Graph|7.2.2 Class Graph]]
        - [[#7.2 Analisis Baris per Baris#7.2.3 Main Program Flow|7.2.3 Main Program Flow]]
- [[#8 Analisis Kompleksitas|8 Analisis Kompleksitas]]
    - [[#8 Analisis Kompleksitas#8.1 Kompleksitas Waktu|8.1 Kompleksitas Waktu]]
    - [[#8 Analisis Kompleksitas#8.2 Kompleksitas Ruang|8.2 Kompleksitas Ruang]]
    - [[#8 Analisis Kompleksitas#8.3 Analisis Worst Case|8.3 Analisis Worst Case]]
    - [[#8 Analisis Kompleksitas#8.4 Perbandingan dengan Pendekatan Lain|8.4 Perbandingan dengan Pendekatan Lain]]
- [[#9 Verifikasi Contoh|9 Verifikasi Contoh]]
    - [[#9 Verifikasi Contoh#9.1 Contoh: Grid 1×3 "T.W"|9.1 Contoh: Grid 1×3 "T.W"]]
        - [[#9.1 Contoh: Grid 1×3 "T.W"#9.1.1 BFS dan Index Assignment|9.1.1 BFS dan Index Assignment]]
        - [[#9.1 Contoh: Grid 1×3 "T.W"#9.1.2 Pembangunan Sistem Persamaan|9.1.2 Pembangunan Sistem Persamaan]]
        - [[#9.1 Contoh: Grid 1×3 "T.W"#9.1.3 Gaussian Elimination|9.1.3 Gaussian Elimination]]
        - [[#9.1 Contoh: Grid 1×3 "T.W"#9.1.4 Verifikasi Hasil|9.1.4 Verifikasi Hasil]]
- [[#10 Kesimpulan|10 Kesimpulan]]
    - [[#10 Kesimpulan#10.1 Ringkasan Temuan Utama|10.1 Ringkasan Temuan Utama]]
        - [[#10.1 Ringkasan Temuan Utama#10.1.1 Lapisan 1 — Mengapa Rekursi Langsung Tidak Bisa Dihitung Berurutan|10.1.1 Lapisan 1 — Mengapa Rekursi Langsung Tidak Bisa Dihitung Berurutan]]
        - [[#10.1 Ringkasan Temuan Utama#10.1.2 Lapisan 2 — Ubah Rekursi Menjadi Sistem Persamaan Linear|10.1.2 Lapisan 2 — Ubah Rekursi Menjadi Sistem Persamaan Linear]]
        - [[#10.1 Ringkasan Temuan Utama#10.1.3 Lapisan 3 — Manfaatkan Struktur Absorbing Chain, Selesaikan dengan Gaussian Elimination|10.1.3 Lapisan 3 — Manfaatkan Struktur Absorbing Chain, Selesaikan dengan Gaussian Elimination]]
    - [[#10 Kesimpulan#10.2 Pelajaran Algoritmik dan Desain OOP|10.2 Pelajaran Algoritmik dan Desain OOP]]
        - [[#10.2 Pelajaran Algoritmik dan Desain OOP#10.2.1 Tabel Ringkasan Konsep Kunci|10.2.1 Tabel Ringkasan Konsep Kunci]]
        - [[#10.2 Pelajaran Algoritmik dan Desain OOP#10.2.2 Keunggulan Pendekatan OOP|10.2.2 Keunggulan Pendekatan OOP]]
        - [[#10.2 Pelajaran Algoritmik dan Desain OOP#10.2.3 Potential Improvements|10.2.3 Potential Improvements]]
- [[#11 Referensi|11 Referensi]]

## 1 Pendahuluan

### 1.1 Latar Belakang

Permasalahan **random walk** (jalan acak) pada graf merupakan salah satu topik klasik dalam teori probabilitas dan ilmu komputer, dengan aplikasi luas mulai dari algoritma PageRank, model difusi pada jaringan, teori rangkaian listrik (electrical network theory), hingga permainan papan sederhana seperti _Snakes and Ladders_. Pertanyaan yang umum diajukan pada seluruh domain tersebut serupa: **berapa lama (secara ekspektasi) suatu proses acak membutuhkan waktu untuk mencapai suatu keadaan target?**

Problem **SPOJ VALENTINE MAZE** hadir sebagai instansiasi konkret dari pertanyaan tersebut. Tjandra, karakter dalam problem ini, berjalan pada sebuah maze berukuran $m \times n$ dan pada setiap langkah memilih salah satu arah yang valid (atas/bawah/kiri/kanan) dengan **probabilitas seragam**. Kita diminta menghitung **expected number of steps** yang dibutuhkan Tjandra untuk berpindah dari posisi awal `T` menuju posisi tujuan `W`.

Yang membuat problem ini menarik secara algoritmik adalah sifat siklis dari graf maze: posisi-posisi pada maze umumnya saling terhubung membentuk siklus (cycle), sehingga nilai ekspektasi pada satu sel bergantung pada nilai ekspektasi sel-sel tetangganya, yang pada gilirannya bergantung balik pada sel tersebut. Ketergantungan melingkar ini membuat pendekatan dynamic programming standar (top-down memoization berbasis DAG) **tidak dapat langsung diterapkan**, dan menuntut transformasi masalah ke ranah aljabar linear.

### 1.2 Relevansi dengan Teori Rantai Markov

Dalam teori probabilitas stokastik, problem VALENTINE MAZE dapat diklasifikasikan secara formal sebagai **absorbing Markov chain** (rantai Markov dengan keadaan penyerap), dengan:

- Ruang keadaan (_state space_) berupa seluruh sel maze yang dapat dijangkau dari posisi start.
- Sebuah **absorbing state** tunggal, yaitu sel tujuan `W` — begitu proses mencapai keadaan ini, proses berhenti.
- Seluruh keadaan lainnya bersifat **transient** (sementara), dan probabilitas transisi antar keadaan transient bersifat seragam terhadap tetangga validnya.

Kuantitas yang dicari — expected number of steps — dikenal dalam literatur sebagai **expected hitting time** atau **expected absorption time**, dan dihitung melalui **fundamental matrix** dari rantai Markov tersebut. Relevansi teoritis ini menjadikan problem ini bukan sekadar latihan graf biasa, melainkan jembatan konkret antara teori probabilitas, aljabar linear numerik (Gaussian elimination), dan graph traversal (BFS) — tiga pilar yang seluruhnya dibutuhkan untuk mendapatkan solusi yang benar dan efisien.

### 1.3 Tujuan Laporan

Laporan ini bertujuan untuk:

1. Mendeskripsikan problem VALENTINE MAZE secara formal dan lengkap, beserta batasan dan sifat-sifatnya.
2. Menelusuri proses penemuan solusi secara sistematis: mengapa simulasi langsung dan DP rekursif gagal, dan bagaimana masalah ini direduksi menjadi sistem persamaan linear.
3. Membuktikan kebenaran algoritma secara matematis, mencakup eksistensi dan ketunggalan solusi sistem persamaan berdasarkan teori absorbing Markov chain.
4. Menjelaskan arsitektur OOP dari solusi (`Graph` dan `LinearSystem`) beserta analisis baris-per-baris implementasinya.
5. Menganalisis kompleksitas waktu dan ruang solusi, serta melakukan verifikasi manual menggunakan contoh sederhana untuk mengonfirmasi kebenaran implementasi.

---

## 2 Spesifikasi Problem

### 2.1 Deskripsi Masalah

**Valentine Maze Game**: Tjandra berjalan random di maze untuk bertemu kekasihnya. Setiap step, dia memilih salah satu arah valid (up/down/left/right) dengan **probabilitas sama**. Hitung **expected number of steps** untuk mencapai tujuan.

Grid direpresentasikan dengan karakter berikut:

- `'T'`: Posisi awal (Tjandra)
- `'W'`: Posisi tujuan (Woman/destination)
- `'.'`: Jalur yang dapat dilalui
- `'#'`: Tembok (tidak bisa dilalui)

#### Batasan

- Ukuran grid $m \times n$, dengan $m, n \le 50$
- Tepat satu sel `T` dan satu sel `W` pada grid
- Output harus memiliki presisi 12 desimal

#### Format Input/Output

- Baris pertama: banyaknya test case
- Untuk setiap test case: baris pertama berisi $m$ dan $n$ (dimensi grid), diikuti $m$ baris berisi grid
- Output: satu baris per test case berisi expected number of steps dengan presisi 12 desimal, atau `Mission Failed!` jika `W` tidak reachable dari `T`

#### Contoh

```
Input:
1
1 3
T.W

Output:
4.000000000000
```

### 2.2 Definisi Formal

Misalkan kita definisikan notasi berikut:

- $S$: himpunan seluruh sel maze yang **reachable** dari posisi start (ditentukan lewat BFS)
- $N(i) \subseteq S$: himpunan tetangga valid dari sel $i$ (4 arah, bukan tembok, dalam batas grid)
- $d(i) = |N(i)|$: derajat (degree) sel $i$
- $g \in S$: sel tujuan `W`, satu-satunya **absorbing state**
- $X_0, X_1, X_2, \ldots$: barisan posisi Tjandra pada waktu $0, 1, 2, \ldots$ (proses stokastik / rantai Markov)
- $P(i \to j) = 1/d(i)$ jika $j \in N(i)$, dan $0$ jika sebaliknya (kecuali $i = g$, di mana proses berhenti)

**Definisi Hitting Time:** Untuk setiap sel $i \in S$, didefinisikan

$$\tau_i = \min{ t \ge 0 \mid X_t = g,\ X_0 = i }$$

sebagai waktu (dalam langkah) pertama kali proses mencapai $g$ ketika dimulai dari $i$.

**Tujuan (Formal):** Tentukan

$$E[i] = \mathbb{E}[\tau_i]$$

untuk $i = $ posisi start `T`. Jika $g$ tidak reachable dari `T`, maka $E[i] = \infty$ (dilaporkan sebagai `Mission Failed!`).

### 2.3 Analisis Struktur Problem

Sebelum merancang algoritma, penting untuk memahami struktur fundamental problem ini.

**Sifat 1 — Struktur Absorbing Chain:** Karena $g$ adalah satu-satunya absorbing state dan seluruh sel lain bersifat transient, $E[i]$ selalu berhingga **jika dan hanya jika** $g$ reachable dari $i$. Reachability harus diverifikasi terlebih dahulu (via BFS) sebelum solusi numerik dicari.

**Sifat 2 — Ketergantungan Melingkar (Coupled Dependencies):** Berbeda dengan problem DP klasik yang dependency graph-nya berbentuk DAG, di sini $E[i]$ bergantung pada $E[j]$ untuk $j \in N(i)$, dan sangat mungkin $i \in N(j)$ juga — menciptakan siklus ketergantungan. Konsekuensinya, $E[i]$ untuk seluruh sel **tidak bisa dihitung satu per satu secara berurutan**; seluruhnya harus diselesaikan **secara simultan**.

**Sifat 3 — Linearitas Ekspektasi:** Meskipun ketergantungannya melingkar, hubungan antar $E[i]$ tetap bersifat **linear** (bukan non-linear), sebagai konsekuensi langsung dari linearitas operator ekspektasi. Sifat inilah yang memungkinkan seluruh sistem ketergantungan melingkar tersebut direduksi menjadi **sistem persamaan linear** yang dapat diselesaikan dengan Gaussian elimination — bukan optimasi non-linear yang jauh lebih sulit.

---

## 3 Landasan Teori

### 3.1 Random Walk sebagai Discrete-Time Markov Chain

Proses jalan Tjandra pada maze adalah **discrete-time Markov Chain**, dengan properti Markov: posisi berikutnya hanya bergantung pada posisi saat ini, tidak pada riwayat sebelumnya. Formalnya:

$$\mathbb{P}(X_{t+1} = j \mid X_t = i, X_{t-1}, \ldots, X_0) = \mathbb{P}(X_{t+1} = j \mid X_t = i) = P(i \to j)$$

dengan transition probability $P(i \to j) = 1/d(i)$ untuk $j$ tetangga valid dari $i$, dan $g$ sebagai **absorbing state** ($P(g \to g) = 1$).

### 3.2 Expected Hitting Time dan Sistem Persamaan Linear

Teknik standar untuk menghitung expected hitting time pada rantai Markov adalah **first-step analysis**: kondisikan pada langkah pertama yang diambil dari $i$, lalu gunakan hukum ekspektasi total.

Untuk setiap sel $(i,j)$ yang bukan goal:

```
E[i,j] = Expected steps dari (i,j) ke goal
       = 1 + Σ (1/d) × E[neighbor]
         ↑     ↑
         |     └─ Weighted average dari neighbors
         └─ One step to move
```

Dimana `d` = degree = jumlah neighbor valid, dan **base case:** $E[\text{goal}] = 0$.

Dalam notasi matriks, jika $Q$ adalah matriks transisi terbatas pada state transient (baris/kolom dihapus untuk state absorbing) dan $\mathbf{1}$ adalah vektor satu, maka seluruh sistem persamaan ini setara dengan:

$$(I - Q), \mathbf{x} = \mathbf{1}$$

dengan $\mathbf{x} = (E[i])_{i \in S \setminus {g}}$. Inilah **fundamental matrix equation** dari absorbing Markov chain — bentuk umum yang mendasari seluruh solusi problem ini.

### 3.3 Gaussian Elimination dengan Partial Pivoting

Sistem $(I-Q)\mathbf{x} = \mathbf{1}$ (setelah diskalakan dengan degree agar bebas pecahan) diselesaikan dengan **Gaussian Elimination**, terdiri dari dua tahap:

**Forward Elimination** — mengubah matriks augmented $[A \mid b]$ menjadi bentuk upper triangular, dengan **partial pivoting** (memilih baris dengan nilai absolut terbesar pada kolom aktif sebagai pivot) untuk menjaga stabilitas numerik dan menghindari pembagian oleh nilai yang sangat kecil.

**Back Substitution** — menyelesaikan variabel dari baris terakhir menuju baris pertama, mengurangi kontribusi variabel yang telah diketahui.

Kompleksitas metode ini adalah $O(k^3)$ untuk sistem berukuran $k \times k$, di mana $k$ adalah jumlah sel non-goal yang reachable.

### 3.4 Breadth-First Search untuk Reachability dan Degree

Sebelum sistem persamaan dapat dibangun, dua hal harus dipastikan lewat **BFS**:

1. **Reachability** — apakah `W` dapat dicapai dari `T`? Jika tidak, expected time tidak berhingga (`Mission Failed!`).
2. **Degree tiap sel** — $d(i)$, jumlah tetangga valid (bukan tembok, dalam batas grid), yang menjadi koefisien pada persamaan linear masing-masing sel.

BFS dipilih (bukan DFS) karena secara alami mengeksplorasi seluruh **connected component** dari `T` dalam $O(V+E)$, sekaligus memungkinkan komputasi degree dilakukan **inline** saat kunjungan pertama pada tiap sel — sebuah optimasi yang dibahas lebih lanjut pada Bagian 4.7.

---

## 4 Analisis Problem: Proses Penemuan Solusi

### 4.1 Observasi Awal

Titik awal yang paling natural adalah bertanya: _jika saya berada di sel $i$, berapa expected steps hingga mencapai $W$?_ Dengan mengondisikan pada langkah pertama, jawabannya adalah 1 langkah ditambah rata-rata expected steps dari tetangga yang dipilih secara seragam — inilah fondasi first-step analysis pada Bagian 3.2.

### 4.2 Eksplorasi Simulasi Langsung dan Kegagalannya

Pendekatan naif pertama yang mungkin terpikirkan adalah **simulasi Monte Carlo**: jalankan random walk sebanyak $K$ kali dari `T`, catat jumlah langkah hingga mencapai `W`, lalu rata-ratakan hasilnya sebagai estimasi $E[T]$.

Pendekatan ini gagal karena dua alasan:

- **Presisi tidak terjamin.** Problem menuntut presisi 12 desimal — sesuatu yang secara fundamental tidak dapat dijamin oleh estimasi statistik berbasis sampling, betapapun besar $K$ yang digunakan.
- **Variansi tinggi & waktu tak terduga.** Pada maze dengan lorong sempit atau struktur seperti "dead end", satu jalan acak dapat mengembara sangat lama sebelum mencapai tujuan, membuat estimasi rata-rata konvergen sangat lambat (berdasarkan Central Limit Theorem, error estimasi menyusut hanya sebesar $O(1/\sqrt{K})$).

Alternatif kedua yang mungkin terpikirkan adalah **DP rekursif memoized** langsung dari rumus $E[i] = 1 + \frac{1}{d(i)}\sum_{j \in N(i)} E[j]$. Namun ini pun gagal: karena graf maze pada umumnya mengandung siklus (bukan DAG), menghitung $E[i]$ membutuhkan $E[j]$ yang belum diketahui, yang pada gilirannya membutuhkan $E[i]$ kembali — **ketergantungan melingkar** yang tidak dapat diselesaikan dengan memoization top-down biasa.

**Kesimpulan:** Baik simulasi maupun DP rekursif langsung tidak layak. Diperlukan pendekatan yang menyelesaikan seluruh ketergantungan **secara simultan**, bukan satu per satu.

### 4.3 Penemuan Kunci Transformasi: Dari Rekursi ke Sistem Linear

Perhatikan kembali persamaan first-step analysis:

$$E[i] = 1 + \sum_{j \in N(i)} \frac{1}{d(i)} E[j]$$

Meskipun $E[i]$ tidak dapat dihitung secara berurutan (karena siklus), persamaan ini tetaplah **linear** terhadap seluruh $E[j]$ yang belum diketahui. Insight kuncinya: kumpulan seluruh persamaan untuk setiap sel non-goal membentuk **sistem persamaan linear** berukuran $k \times k$ (dengan $k$ = banyak sel non-goal reachable), yang dapat diselesaikan **sekaligus** menggunakan aljabar linear numerik — bukan rekursi.

### 4.4 Reformulasi sebagai Masalah Aljabar Linear

Alih-alih bertanya "berapa $E[i]$ untuk tiap sel, dihitung satu per satu?", kita reformulasikan menjadi: **bangun matriks augmented $[A \mid b]$ yang merepresentasikan seluruh persamaan sekaligus, lalu selesaikan dengan Gaussian elimination.** Baris ke-$k$ dari matriks ini merepresentasikan persamaan untuk sel ke-$k$, dan solusi $\mathbf{x}$ yang dihasilkan memberikan $E[i]$ untuk seluruh sel secara bersamaan — termasuk sel start yang kita cari.

### 4.5 Derivasi Persamaan per Sel

Untuk cell (i,j) dengan degree d, mulai dari:

$$E[i,j] = 1 + \frac{1}{d} \sum_{\text{neighbor}} E[\text{neighbor}]$$

Kalikan kedua ruas dengan $d$ agar bebas pecahan (penting untuk stabilitas numerik Gaussian elimination):

$$d \times E[i,j] = d + \sum_{\text{neighbor}} E[\text{neighbor}]$$

$$d \times E[i,j] - \sum_{\text{neighbor}} E[\text{neighbor}] = d$$

Bentuk inilah yang langsung dipetakan menjadi satu baris pada matriks augmented: koefisien diagonal $d$ pada kolom sel itu sendiri, koefisien $-1$ pada kolom tiap tetangga non-goal, dan RHS $= d$. Jika tetangga adalah goal, kontribusinya nol (karena $E[\text{goal}]=0$), sehingga tidak perlu ditambahkan ke matriks sama sekali.

### 4.6 Penentuan Struktur Data: Graph dan LinearSystem

Solusi dipecah menjadi dua kelas dengan tanggung jawab terpisah (_separation of concerns_):

```
┌─────────────────────────────────────────┐
│           Main Program                  │
│  ┌───────────────────────────────────┐  │
│  │  1. Read input                    │  │
│  │  2. Create Graph object           │  │
│  │  3. Explore & validate            │  │
│  │  4. Build LinearSystem            │  │
│  │  5. Solve & output                │  │
│  └───────────────────────────────────┘  │
└─────────────────────────────────────────┘
         │                    │
         ▼                    ▼
  ┌─────────────┐      ┌──────────────┐
  │   Graph     │      │ LinearSystem │
  │   Class     │      │    Class     │
  └─────────────┘      └──────────────┘
```

- **Graph Class:** menangani representasi maze, BFS, dan pemetaan sel ke indeks variabel.
- **LinearSystem Class:** menangani matriks augmented dan Gaussian elimination — sama sekali tidak mengetahui bahwa datanya berasal dari maze.

Satu keputusan desain penting: **sel goal tidak diberi indeks variabel**, karena $E[\text{goal}] = 0$ adalah _known constant_, bukan sesuatu yang perlu diselesaikan — ini mengurangi ukuran sistem sebesar satu variabel dan menyederhanakan persamaan tetangga yang bersebelahan dengan goal.

### 4.7 Optimasi: Inline Degree Computation dan Partial Pivoting

Dua optimasi kunci diterapkan:

1. **Inline degree computation** — degree tiap sel dihitung **saat first visit** selama BFS berjalan, bukan pada pass terpisah setelahnya. Ini menghindari traversal ganda atas grid.
2. **Partial pivoting** pada Gaussian elimination — memilih baris dengan nilai absolut terbesar sebagai pivot pada tiap kolom, mencegah pembagian dengan angka yang sangat kecil yang dapat memperbesar galat pembulatan (_numerical instability_) secara signifikan pada sistem berukuran ribuan variabel.

---

## 5 Pembuktian Kebenaran Algoritma

### 5.1 Teorema Utama

**Teorema:** Misalkan $S$ adalah himpunan sel reachable dari `T`, dengan `W` $\in S$ sebagai satu-satunya absorbing state, dan seluruh sel di $S \setminus {W}$ bersifat transient. Jika `W` reachable dari setiap sel transient (dijamin oleh konstruksi $S$ via BFS dari `T`), maka sistem persamaan linear yang dibangun pada Bagian 4.5 memiliki **solusi unik**, dan solusi tersebut sama dengan expected hitting time $E[i]$ yang sebenarnya untuk setiap $i \in S \setminus {W}$.

**Bukti (sketsa):** Diperlukan dua klaim:

1. Sistem persamaan linear tidak singular (matriks koefisien invertible), sehingga solusi ada dan unik.
2. Solusi tersebut memenuhi definisi hitting time secara probabilistik, bukan sekadar solusi aljabar formal.

### 5.2 Bukti Eksistensi dan Ketunggalan Solusi

Misalkan $Q$ adalah matriks transisi yang dibatasi pada state transient $S \setminus {W}$, yaitu $Q_{ij} = 1/d(i)$ jika $j$ tetangga dari $i$ dan $j \ne W$, dan $0$ jika sebaliknya.

Karena `W` reachable dari setiap $i \in S \setminus {W}$ (dijamin oleh BFS pada Graph class — semua sel di `cells[]` diverifikasi terhubung dari start, dan `W` termasuk di dalamnya), rantai Markov ini adalah **absorbing chain yang proper**: dari setiap state transient, terdapat lintasan berhingga menuju absorbing state dengan probabilitas positif.

Dari teori absorbing Markov chain (lih. Kemeny & Snell, _Finite Markov Chains_), sifat ini menjamin bahwa **spectral radius** dari $Q$ kurang dari 1, sehingga matriks $(I - Q)$ **invertible** (non-singular). Akibatnya:

$$\mathbf{x} = (I - Q)^{-1} \mathbf{1}$$

ada dan **unik**. Matriks $N = (I-Q)^{-1}$ dikenal sebagai **fundamental matrix** dari rantai Markov, dan $\mathbf{x} = N\mathbf{1}$ tepat sama dengan vektor expected hitting time. Karena matriks pada Gaussian elimination di kelas `LinearSystem` adalah representasi skala-degree dari $(I-Q)$ (dikalikan diagonal $D = \text{diag}(d(i))$ agar bebas pecahan, yaitu $D(I-Q)$), matriks ini tetap non-singular selama $D$ non-singular (yaitu selama tidak ada sel dengan degree nol) — kondisi yang otomatis terjamin karena setiap sel reachable non-goal pasti punya minimal satu tetangga (jika tidak, ia tidak mungkin reachable). Inilah alasan `solve()` mengembalikan $-1$ (gagal) hanya ketika pivot mendekati nol — yang menandakan struktur maze yang secara matematis tidak mungkin terjadi pada sel reachable yang valid, sekaligus safeguard numerik.

### 5.3 Bukti Kebenaran Konstruksi Sistem Persamaan

**Klaim:** Baris matriks yang dibangun oleh `buildLinearSystem()` — yaitu $d \times E[i] - \sum_{\text{neighbor} \ne \text{goal}} E[\text{neighbor}] = d$ — secara aljabar ekuivalen dengan definisi hitting time pada Bagian 3.2.

**Bukti:** Dari definisi,

$$E[i] = 1 + \sum_{j \in N(i)} \frac{1}{d(i)} E[j] = 1 + \frac{1}{d(i)}\left(\sum_{j \in N(i),, j \ne g} E[j] + E[g]\right)$$

Karena $E[g] = 0$ (base case, absorbing state), suku tersebut lenyap:

$$E[i] = 1 + \frac{1}{d(i)}\sum_{j \in N(i),, j \ne g} E[j]$$

Kalikan kedua ruas dengan $d(i)$:

$$d(i), E[i] - \sum_{j \in N(i),, j \ne g} E[j] = d(i)$$

yang persis merupakan baris yang dibangun oleh kode (diagonal $d$, koefisien $-1$ untuk tiap tetangga non-goal, RHS $= d$). Karena transformasi ini murni aljabar (perkalian dan substitusi nilai konstan), **tidak ada informasi yang hilang atau berubah** — solusi sistem yang dibangun identik dengan solusi definisi asli. Dikombinasikan dengan ketunggalan solusi pada Bagian 5.2 dan korektnya Gaussian elimination sebagai metode solve sistem linear non-singular (fakta standar aljabar linear numerik), maka nilai $E[\text{start}]$ yang dikembalikan oleh `ls.solve(graph.getStartIndex())` benar secara matematis. $\blacksquare$

---

## 6 Pseudokode

### 6.1 Penjelasan Alur Algoritma

```
Fungsi EXPLORE(grid, start):
    BFS dari start, tandai seluruh sel reachable
    untuk tiap sel yang baru dikunjungi:
        hitung degree(sel) inline
    kembalikan daftar sel reachable, degree tiap sel

Fungsi ASSIGN_INDICES(cells, goal):
    k ← 0
    untuk tiap sel dalam cells:
        jika sel ≠ goal:
            idx[sel] ← k
            k ← k + 1
    kembalikan k  // ukuran sistem

Fungsi BUILD_SYSTEM(cells, goal, degree, idx, k):
    inisialisasi matriks A berukuran k × (k+1) dengan nol
    untuk tiap sel i dalam cells, i ≠ goal:
        row ← idx[i]
        A[row][row] ← degree[i]
        A[row][k]   ← degree[i]        // RHS
        untuk tiap tetangga j dari i:
            jika j ≠ goal:
                A[row][idx[j]] ← A[row][idx[j]] - 1
    kembalikan A

Fungsi GAUSSIAN_SOLVE(A, k, target):
    // Forward elimination dengan partial pivoting
    untuk col dari 0 hingga k-1:
        cari baris dengan |A[row][col]| terbesar, tukar ke posisi col
        jika pivot ≈ 0: kembalikan GAGAL (singular)
        eliminasi seluruh baris di bawah col
    // Back substitution
    untuk i dari k-1 turun ke 0:
        x[i] ← (A[i][k] - Σ A[i][j]·x[j] untuk j > i) / A[i][i]
    kembalikan x[target]

Fungsi SOLVE(grid):
    jika T atau W tidak ada di grid: kembalikan "Mission Failed!"
    jika T == W: kembalikan 0
    cells, degree ← EXPLORE(grid, T)
    jika W tidak ada dalam cells: kembalikan "Mission Failed!"
    k ← ASSIGN_INDICES(cells, W)
    A ← BUILD_SYSTEM(cells, W, degree, idx, k)
    hasil ← GAUSSIAN_SOLVE(A, k, idx[T])
    jika hasil == GAGAL: kembalikan "Mission Failed!"
    kembalikan hasil
```

### 6.2 Catatan Implementasi Kritis

Beberapa catatan penting terkait implementasi:

1. **Tipe data `double`:** Seluruh perhitungan menggunakan floating point (bukan integer seperti pada problem berbasis counting), karena hasil berupa expected value real dengan presisi 12 desimal.
2. **EPS untuk deteksi singular:** Nilai pivot yang mendekati nol (`< EPS`) harus dideteksi eksplisit sebagai sinyal kegagalan (`Mission Failed!` atau struktur maze yang tidak valid), bukan dibiarkan menyebabkan pembagian dengan nol.
3. **Ukuran array `MAXN` dan `A[MAXN][MAXN]`:** Dengan grid maksimum $50 \times 50 = 2500$ sel, matriks augmented berukuran hingga $2500 \times 2501$ — signifikan dari sisi memori (~50 MB), sehingga harus dialokasikan dengan hati-hati (biasanya sebagai array global, bukan pada stack).
4. **Skip goal saat build system:** Baris dan kolom untuk sel goal **tidak pernah dibuat**, sehingga indeksnya harus divalidasi (`idx != -1`) sebelum ditambahkan sebagai koefisien.

---

## 7 Implementasi C++

### 7.1 Kode Lengkap

```cpp
#include <cstdio>
#include <cmath>
#include <algorithm>
using namespace std;

const double EPS = 1e-9;
const int MAXN = 2505;

class LinearSystem {
private:
  double A[MAXN][MAXN]; // Augmented matrix [A|b]
  int size;             // Jumlah variabel (N)

public:
  void initialize(int n) {
    size = n;
    for (int i = 0; i < n; ++i)
      for (int j = 0; j <= n; ++j)
        A[i][j] = 0;
  }

  void setCoefficient(int row, int col, double value) {
    A[row][col] = value;
  }

  void addCoefficient(int row, int col, double value) {
    A[row][col] += value;
  }

  void setRHS(int row, double value) {
    A[row][size] = value;
  }

  double solve(int targetVariable) {
    // Forward Elimination
    for (int col = 0; col < size; ++col) {
      int piv = col;
      double maxv = fabs(A[col][col]);
      for (int r = col + 1; r < size; ++r) {
        double v = fabs(A[r][col]);
        if (v > maxv) { maxv = v; piv = r; }
      }
      if (maxv < EPS) return -1;

      if (piv != col)
        for (int c = col; c <= size; ++c)
          swap(A[col][c], A[piv][c]);

      double inv_pivot = 1.0 / A[col][col];
      for (int r = col + 1; r < size; ++r) {
        double fac = A[r][col] * inv_pivot;
        if (fabs(fac) < 1e-15) continue;
        for (int c = col; c <= size; ++c)
          A[r][c] -= fac * A[col][c];
      }
    }

    // Back Substitution
    double x[MAXN];
    for (int i = size - 1; i >= 0; --i) {
      x[i] = A[i][size];
      for (int j = i + 1; j < size; ++j)
        x[i] -= A[i][j] * x[j];
      x[i] /= A[i][i];
    }
    return x[targetVariable];
  }
};

class Graph {
private:
  int m, n;
  int si, sj;
  int gi, gj;
  int cellCnt;

  char g[55][55];
  int idx[55][55];
  int vis[55][55];
  int deg[55][55];
  int cells[MAXN][2];

  const int di[4] = {-1, 1, 0, 0};
  const int dj[4] = {0, 0, -1, 1};

  bool isValidCell(int i, int j) {
    return i >= 0 && i < m && j >= 0 && j < n;
  }

  int getDegree(int i, int j) {
    int d = 0;
    for (int k = 0; k < 4; ++k) {
      int ni = i + di[k], nj = j + dj[k];
      if (isValidCell(ni, nj) && g[ni][nj] != '#') d++;
    }
    return d;
  }

public:
  Graph(int rows, int cols) : m(rows), n(cols), si(-1), sj(-1), gi(-1), gj(-1) {
    for (int i = 0; i < m; ++i)
      for (int j = 0; j < n; ++j)
        vis[i][j] = 0, idx[i][j] = -1;
  }

  void readGrid() {
    for (int i = 0; i < m; ++i) scanf("%s", g[i]);
    for (int i = 0; i < m; ++i)
      for (int j = 0; j < n; ++j) {
        if (g[i][j] == 'T') { si = i; sj = j; }
        if (g[i][j] == 'W') { gi = i; gj = j; }
      }
  }

  bool isValid() { return si != -1 && gi != -1; }
  bool isStartAtGoal() { return si == gi && sj == gj; }

  void exploreGraph() {
    static int q[MAXN][2];
    int head = 0, tail = 0;
    q[tail][0] = si; q[tail][1] = sj; tail++;
    vis[si][sj] = 1;
    cellCnt = 0;
    deg[si][sj] = getDegree(si, sj);

    while (head < tail) {
      int i = q[head][0], j = q[head][1]; head++;
      cells[cellCnt][0] = i; cells[cellCnt][1] = j; cellCnt++;

      for (int k = 0; k < 4; ++k) {
        int ni = i + di[k], nj = j + dj[k];
        if (isValidCell(ni, nj) && !vis[ni][nj] && g[ni][nj] != '#') {
          vis[ni][nj] = 1;
          q[tail][0] = ni; q[tail][1] = nj; tail++;
          deg[ni][nj] = getDegree(ni, nj);
        }
      }
    }
  }

  bool isGoalReachable() { return vis[gi][gj] == 1; }

  int assignIndices() {
    int k = 0;
    for (int c = 0; c < cellCnt; ++c) {
      int i = cells[c][0], j = cells[c][1];
      if (i != gi || j != gj) idx[i][j] = k++;
    }
    return k;
  }

  void buildLinearSystem(LinearSystem& ls, int systemSize) {
    ls.initialize(systemSize);
    for (int c = 0; c < cellCnt; ++c) {
      int i = cells[c][0], j = cells[c][1];
      if (i == gi && j == gj) continue;

      int row = idx[i][j];
      int d = deg[i][j];
      ls.setCoefficient(row, row, d);
      ls.setRHS(row, d);

      for (int dir = 0; dir < 4; ++dir) {
        int ni = i + di[dir], nj = j + dj[dir];
        if (isValidCell(ni, nj) && g[ni][nj] != '#') {
          int ncol = idx[ni][nj];
          if (ncol != -1) ls.addCoefficient(row, ncol, -1.0);
        }
      }
    }
  }

  int getStartIndex() { return idx[si][sj]; }
};

int main() {
  int tc;
  scanf("%d", &tc);

  while (tc--) {
    int m, n;
    scanf("%d %d", &m, &n);

    Graph graph(m, n);
    graph.readGrid();

    if (!graph.isValid()) { printf("Mission Failed!\n"); continue; }
    if (graph.isStartAtGoal()) { printf("0.000000000000\n"); continue; }

    graph.exploreGraph();
    if (!graph.isGoalReachable()) { printf("Mission Failed!\n"); continue; }

    int systemSize = graph.assignIndices();
    if (systemSize == 0) { printf("0.000000000000\n"); continue; }

    LinearSystem ls;
    graph.buildLinearSystem(ls, systemSize);

    double ans = ls.solve(graph.getStartIndex());
    if (ans < 0) printf("Mission Failed!\n");
    else printf("%.12f\n", ans);
  }
  return 0;
}
```

### 7.2 Analisis Baris per Baris

#### 7.2.1 Class LinearSystem

- `double A[MAXN][MAXN]`: matriks augmented $[A \mid b]$, kolom ke-`size` menyimpan RHS.
- `initialize(n)`: reset matriks $n \times (n+1)$ ke nol — dipanggil sekali per test case.
- `setCoefficient` vs `addCoefficient`: `set` untuk assignment langsung (diagonal, RHS); `add` untuk kontribusi tetangga, karena satu sel bisa memiliki hingga 4 tetangga yang masing-masing menyumbang $-1$ ke kolom berbeda.
- `solve(targetVariable)`: forward elimination dengan **partial pivoting** (baris dengan nilai absolut terbesar pada kolom aktif ditukar ke posisi pivot) untuk stabilitas numerik, dilanjutkan back substitution. Mengembalikan $-1$ jika matriks singular (`maxv < EPS`) — secara teoretis ini hanya terjadi jika ada bug pada konstruksi sistem, karena Bagian 5.2 menjamin non-singularity selama graf valid.

#### 7.2.2 Class Graph

- Array `g`, `idx`, `vis`, `deg` berukuran tetap `55×55` (batas problem $\le 50\times50$ + margin).
- `readGrid()`: membaca grid dan mencari posisi `T`/`W` sekaligus dalam satu pass $O(mn)$.
- `exploreGraph()`: BFS iteratif menggunakan array sebagai queue (bukan `std::queue`, demi kecepatan), **menghitung degree inline** saat sel pertama kali dikunjungi (`deg[ni][nj] = getDegree(ni, nj)` langsung setelah `vis[ni][nj] = 1`) — menghindari pass kedua atas seluruh sel reachable.
- `assignIndices()`: memberi indeks variabel `0..k-1` ke seluruh sel reachable **kecuali** goal — sel goal sengaja dibiarkan `idx = -1` karena nilainya konstan ($E[\text{goal}]=0$), bukan variabel yang perlu diselesaikan.
- `buildLinearSystem()`: untuk tiap sel non-goal, set diagonal dan RHS sebesar degree, lalu tambahkan $-1$ untuk tiap tetangga non-goal (tetangga goal diabaikan karena kontribusinya nol, sesuai turunan pada Bagian 4.5).

#### 7.2.3 Main Program Flow

Alur utama mengikuti lima tahap berurutan: (1) baca grid, (2) validasi keberadaan T/W dan kasus trivial T==W, (3) BFS eksplorasi dan cek reachability W, (4) bangun sistem persamaan, (5) selesaikan dan cetak hasil dengan presisi 12 desimal. Setiap tahap memiliki _early exit_ (`continue`) untuk kasus degenerate (`Mission Failed!` atau jawaban 0), menjaga logika utama tetap bersih dan mudah dibaca.

---

## 8 Analisis Kompleksitas

### 8.1 Kompleksitas Waktu

|Operasi|Kompleksitas|Catatan|
|---|---|---|
|Baca grid|$O(mn)$|$m, n \le 50$|
|BFS + degree inline|$O(V + E)$|$V \le mn$, $E \le 4V$|
|Assign indices|$O(V)$|Linear scan atas cells|
|Build system|$O(V \times 4)$|Tiap sel cek 4 tetangga|
|Gaussian elimination|$O(k^3)$|$k$ = jumlah variabel $\le 2500$|
|**Total per test case**|**$O(k^3)$**|Didominasi Gaussian elimination|

### 8.2 Kompleksitas Ruang

|Komponen|Ukuran|Estimasi Memori|
|---|---|---|
|Grid `g[55][55]`|$55^2$|~3 KB|
|Matriks `A[2505][2505]`|$2505^2 \times 8$ byte|~50 MB|
|Array pendukung lain|—|~100 KB|
|**Total**||**~50 MB**|

Komponen dominan adalah matriks augmented $A$, karena bersifat **dense** (menyimpan seluruh elemen termasuk yang bernilai nol) meskipun struktur maze umumnya sangat _sparse_ (tiap baris hanya punya maksimum 5 elemen non-nol: diagonal + 4 tetangga).

### 8.3 Analisis Worst Case

**Worst case:** $k = 2500$ (seluruh grid $50 \times 50$ reachable dan bukan tembok) → $k^3/3 \approx 5.2$ miliar operasi untuk satu test case — signifikan namun umumnya masih dalam batas waktu wajar untuk sedikit test case.

**Average case:** Pada praktiknya, sebagian besar maze tidak sepenuhnya terhubung (mengandung tembok yang cukup banyak), sehingga $k$ rata-rata berkisar 500–1000. Untuk 250 test case dengan rata-rata tersebut, total waktu eksekusi diperkirakan sekitar 3–5 detik.

### 8.4 Perbandingan dengan Pendekatan Lain

|Pendekatan|Kompleksitas|Layak untuk Batasan Problem?|
|---|---|---|
|Simulasi Monte Carlo|$O(K \cdot \text{steps})$, presisi $O(1/\sqrt{K})$|Tidak (presisi 12 desimal tak terjamin)|
|DP rekursif memoized langsung|Tidak terdefinisi (siklus tak tertangani)|Tidak (invalid untuk graf bersiklus)|
|**Gaussian Elimination (dense)**|$O(k^3)$|**Ya**, untuk $k \le 2500$|
|Sparse solver / iterative (Gauss-Seidel)|$O(k \cdot \text{iterasi} \cdot \text{nnz})$|Ya, dan lebih hemat memori untuk $k$ besar|

Keunggulan pendekatan Gaussian elimination dense adalah **kesederhanaan dan kepastian presisi** (bukan iteratif/approximate), meski dengan trade-off memori $O(k^2)$ yang signifikan pada worst case dibanding solusi berbasis sparse matrix.

---

## 9 Verifikasi Contoh

### 9.1 Contoh: Grid 1×3 "T.W"

#### 9.1.1 BFS dan Index Assignment

```
Grid:  T . W
```

- $si=0, sj=0$ (T), $gi=0, gj=2$ (W)
- BFS dari (0,0): kunjungi (0,0) [deg=1], (0,1) [deg=2], (0,2)=W [deg=1]
- Reachable cells: $[(0,0), (0,1), (0,2)]$, $W$ reachable ✓
- Assign indices: $(0,0) \to 0$, $(0,1) \to 1$, $(0,2)=W \to$ tanpa indeks (goal)
- Ukuran sistem: $k = 2$

#### 9.1.2 Pembangunan Sistem Persamaan

**Cell 0 = T (0,0):** degree $=1$, tetangga $=[(0,1)]$

$$1 \times E[0] - 1 \times E[1] = 1$$

**Cell 1 = (0,1):** degree $=2$, tetangga $=[(0,0), W]$; kontribusi $W$ nol

$$2 \times E[1] - 1 \times E[0] = 2$$

Matriks augmented:

```
[ 1  -1 | 1 ]   ← equation untuk cell 0
[-1   2 | 2 ]   ← equation untuk cell 1
```

#### 9.1.3 Gaussian Elimination

**Forward elimination** ($R_2 \leftarrow R_2 + R_1$):

```
[ 1  -1 | 1 ]
[ 0   1 | 3 ]
```

**Back substitution:**

$$E[1] = 3 / 1 = 3$$ $$E[0] = (1 - (-1)\times 3) / 1 = 4$$

#### 9.1.4 Verifikasi Hasil

Substitusi balik ke persamaan asli untuk memastikan konsistensi:

- Cell 0: $E[0] = 1 + E[1] = 1 + 3 = 4$ ✓ (sesuai first-step analysis: dari T, satu-satunya tetangga adalah cell 1)
- Cell 1: $E[1] = 1 + \frac{1}{2}(E[0] + E[W]) = 1 + \frac{1}{2}(4 + 0) = 1 + 2 = 3$ ✓

Kedua persamaan konsisten. Output akhir:

```
4.000000000000
```

sesuai dengan contoh output pada Bagian 2.1. ✓

---

## 10 Kesimpulan

### 10.1 Ringkasan Temuan Utama

Problem VALENTINE MAZE mengajarkan pola berpikir berlapis dalam mendekomposisi masalah probabilistik dengan ketergantungan melingkar menjadi masalah aljabar linear yang dapat diselesaikan secara eksak dan efisien.

#### 10.1.1 Lapisan 1 — Mengapa Rekursi Langsung Tidak Bisa Dihitung Berurutan

Persoalan pertama yang harus dikenali adalah: mengapa kita tidak bisa langsung menghitung $E[i]$ satu per satu secara top-down? Pada contoh grid `T . W`, mencoba menghitung $E[1]$ (sel tengah) membutuhkan $E[0]$ (T) yang belum diketahui, dan $E[0]$ pada gilirannya membutuhkan $E[1]$ kembali — siklus ketergantungan dua arah yang tidak dapat diselesaikan oleh memoization top-down biasa (yang mengasumsikan dependency graph berbentuk DAG).

#### 10.1.2 Lapisan 2 — Ubah Rekursi Menjadi Sistem Persamaan Linear

Alih-alih memaksa urutan komputasi, kita akui bahwa persamaan $E[i] = 1 + \frac{1}{d(i)}\sum E[\text{neighbor}]$ tetap **linear** meski melingkar, lalu kumpulkan seluruh persamaan untuk semua sel non-goal sebagai satu sistem $k \times k$. Transformasi ini mengubah masalah dari "urutan komputasi apa yang valid?" menjadi "matriks apa yang perlu diselesaikan?" — pergeseran kerangka berpikir yang esensial.

#### 10.1.3 Lapisan 3 — Manfaatkan Struktur Absorbing Chain, Selesaikan dengan Gaussian Elimination

Begitu sistem terbentuk, teori absorbing Markov chain (Bagian 5.2) menjamin sistem tersebut **non-singular** selama goal reachable dari setiap sel — kondisi yang telah diverifikasi lewat BFS sebelum sistem dibangun. Gaussian elimination dengan partial pivoting kemudian menyelesaikan sistem tersebut secara eksak dalam $O(k^3)$, menghasilkan $E[i]$ untuk seluruh sel sekaligus, termasuk sel start yang menjadi jawaban akhir.

Inilah inti solusi: **bukan hitung rekursif satu per satu, tapi selesaikan seluruh sistem ketergantungan sekaligus lewat aljabar linear.**

### 10.2 Pelajaran Algoritmik dan Desain OOP

#### 10.2.1 Tabel Ringkasan Konsep Kunci

|Konsep|Rumus / Properti|Relevansi dalam Problem|
|---|---|---|
|Expected hitting time|$E[i] = \mathbb{E}[\tau_i]$|Kuantitas yang dicari|
|First-step analysis|$E[i] = 1 + \frac{1}{d(i)}\sum_{j} E[j]$|Fondasi seluruh sistem persamaan|
|Absorbing state|$E[\text{goal}] = 0$|Base case, tidak diberi indeks variabel|
|Fundamental matrix equation|$(I-Q)\mathbf{x} = \mathbf{1}$|Bentuk matriks dari seluruh sistem|
|Non-singularity|Goal reachable dari semua sel transient|Menjamin solusi ada & unik (Bagian 5.2)|
|Degree per sel|$d(i) = \lvert N(i) \rvert$|Koefisien diagonal & pembagi first-step|
|Partial pivoting|Pilih $\max\lvert A[r][\text{col}]\rvert$|Stabilitas numerik Gaussian elimination|
|Kompleksitas total|$O(k^3)$ per test case|Layak untuk $k \le 2500$|

#### 10.2.2 Keunggulan Pendekatan OOP

Solusi OOP ini mendemonstrasikan **clean code principles** dengan:

- **Clear class responsibilities** — `Graph` tidak tahu apa-apa tentang Gaussian elimination; `LinearSystem` tidak tahu apa-apa tentang maze.
- **Encapsulation of complexity** — detail BFS dan pivoting tersembunyi di balik method dengan nama deskriptif (`exploreGraph()`, `solve()`).
- **Readable main program flow** — lima tahap linear yang mudah diikuti, masing-masing dengan early exit yang jelas.
- **Easy to test and maintain** — kedua kelas dapat diuji secara independen (mis. `LinearSystem` diuji dengan matriks buatan tangan tanpa perlu grid sama sekali).

Meskipun bukan yang tercepat, pendekatan ini sangat baik untuk **learning** (memahami struktur problem secara eksplisit), **production** (kode yang maintainable), dan **collaboration** (interface yang jelas antar tim).

#### 10.2.3 Potential Improvements

**1. Sparse Matrix** — mengingat setiap baris hanya memiliki maksimum 5 elemen non-nol, representasi sparse dapat menghemat memori signifikan dibanding matriks dense $O(k^2)$:

```cpp
class SparseLinearSystem {
  vector<map<int, double>> A;  // Only store non-zeros
};
```

**2. Iterator Pattern** — abstraksi iterasi atas sel reachable:

```cpp
class CellIterator {
  // Iterate through reachable cells
};
```

**3. Strategy Pattern untuk Solver** — memungkinkan switch antara Gaussian elimination dan iterative solver (mis. Gauss-Seidel) tanpa mengubah kode `Graph`:

```cpp
class Solver {
  virtual double solve() = 0;
};
class GaussianSolver : public Solver { ... };
class IterativeSolver : public Solver { ... };
```

**4. Builder Pattern** — mempermudah konstruksi sistem persamaan secara deklaratif:

```cpp
LinearSystem ls = LinearSystemBuilder()
                    .withSize(k)
                    .addEquation(row, coeffs, rhs)
                    .build();
```

Untuk competitive programming yang sangat ketat dari sisi waktu, kombinasi **sparse matrix + iterative solver** akan lebih optimal secara performa, namun mengorbankan sebagian keterbacaan (readability) dibanding pendekatan dense Gaussian elimination di atas.

**Final verdict:** Solusi ini memberikan keseimbangan yang sangat baik antara kebenaran (correctness), kejelasan (clarity), dan performa (performance) untuk batasan problem yang diberikan.

---

## 11 Referensi

1. Kemeny, J. G., & Snell, J. L. (1976). _Finite Markov Chains_. Springer-Verlag. — Teori fundamental matrix, absorbing Markov chain, dan expected hitting time.
2. Grinstead, C. M., & Snell, J. L. (1997). _Introduction to Probability_ (2nd ed.). American Mathematical Society. — First-step analysis dan random walk pada graf.
3. Doyle, P. G., & Snell, J. L. (1984). _Random Walks and Electric Networks_. Mathematical Association of America. — Analogi random walk dengan rangkaian listrik dan effective resistance.
4. Golub, G. H., & Van Loan, C. F. (2013). _Matrix Computations_ (4th ed.). Johns Hopkins University Press. — Gaussian elimination, partial pivoting, dan stabilitas numerik.
5. Cormen, T. H., Leiserson, C. E., Rivest, R. L., & Stein, C. (2009). _Introduction to Algorithms_ (3rd ed.). MIT Press. — Breadth-First Search dan analisis kompleksitas graf.
6. SPOJ Problem Archive. VALENTINE — Valentine Maze. [https://www.spoj.com/](https://www.spoj.com/)