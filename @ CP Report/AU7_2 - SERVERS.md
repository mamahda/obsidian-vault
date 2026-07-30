[[Binary Search]] | [[Floor and Ceiling Function]] 

- [[#1 Pendahuluan|1 Pendahuluan]]
	- [[#1 Pendahuluan#1.1 Latar Belakang|1.1 Latar Belakang]]
	- [[#1 Pendahuluan#1.2 Relevansi dengan Teori Penjadwalan|1.2 Relevansi dengan Teori Penjadwalan]]
	- [[#1 Pendahuluan#1.3 Tujuan Laporan|1.3 Tujuan Laporan]]
- [[#2 Spesifikasi Problem|2 Spesifikasi Problem]]
	- [[#2 Spesifikasi Problem#2.1 Deskripsi Masalah|2.1 Deskripsi Masalah]]
		- [[#2.1 Deskripsi Masalah#Batasan|Batasan]]
		- [[#2.1 Deskripsi Masalah#Format Input/Output|Format Input/Output]]
		- [[#2.1 Deskripsi Masalah#Contoh|Contoh]]
	- [[#2 Spesifikasi Problem#2.2 Definisi Formal|2.2 Definisi Formal]]
	- [[#2 Spesifikasi Problem#2.3 Analisis Struktur Problem|2.3 Analisis Struktur Problem]]
- [[#3 Landasan Teori|3 Landasan Teori]]
	- [[#3 Landasan Teori#3.1 Binary Search on Answer|3.1 Binary Search on Answer]]
	- [[#3 Landasan Teori#3.2 Teori Kapasitas Server|3.2 Teori Kapasitas Server]]
	- [[#3 Landasan Teori#3.3 Prinsip Penjadwalan Optimal|3.3 Prinsip Penjadwalan Optimal]]
	- [[#3 Landasan Teori#3.4 Struktur Matematika Kunci: Fungsi Lantai|3.4 Struktur Matematika Kunci: Fungsi Lantai]]
- [[#4 Analisis Problem: Proses Penemuan Solusi|4 Analisis Problem: Proses Penemuan Solusi]]
	- [[#4 Analisis Problem: Proses Penemuan Solusi#4.1 Observasi Awal|4.1 Observasi Awal]]
	- [[#4 Analisis Problem: Proses Penemuan Solusi#4.2 Eksplorasi Brute Force dan Kegagalannya|4.2 Eksplorasi Brute Force dan Kegagalannya]]
	- [[#4 Analisis Problem: Proses Penemuan Solusi#4.3 Penemuan Properti Monoton: Kunci Transformasi|4.3 Penemuan Properti Monoton: Kunci Transformasi]]
	- [[#4 Analisis Problem: Proses Penemuan Solusi#4.4 Reformulasi sebagai Masalah Keputusan|4.4 Reformulasi sebagai Masalah Keputusan]]
	- [[#4 Analisis Problem: Proses Penemuan Solusi#4.5 Derivasi Formula Kapasitas|4.5 Derivasi Formula Kapasitas]]
	- [[#4 Analisis Problem: Proses Penemuan Solusi#4.6 Penentuan Batas Pencarian Biner|4.6 Penentuan Batas Pencarian Biner]]
	- [[#4 Analisis Problem: Proses Penemuan Solusi#4.7 Optimasi Kelayakan: Early Termination|4.7 Optimasi Kelayakan: Early Termination]]
- [[#5 Pembuktian Kebenaran Algoritma|5 Pembuktian Kebenaran Algoritma]]
	- [[#5 Pembuktian Kebenaran Algoritma#5.1 Teorema Utama|5.1 Teorema Utama]]
	- [[#5 Pembuktian Kebenaran Algoritma#5.2 Bukti Invariant Binary Search|5.2 Bukti Invariant Binary Search]]
	- [[#5 Pembuktian Kebenaran Algoritma#5.3 Bukti Ekuivalensi Kelayakan|5.3 Bukti Ekuivalensi Kelayakan]]
- [[#6 Pseudokode|6 Pseudokode]]
	- [[#6 Pseudokode#6.1 Penjelasan Alur Algoritma|6.1 Penjelasan Alur Algoritma]]
	- [[#6 Pseudokode#6.2 Catatan Implementasi Kritis|6.2 Catatan Implementasi Kritis]]
- [[#7 Implementasi C++|7 Implementasi C++]]
	- [[#7 Implementasi C++#7.1 Kode Lengkap|7.1 Kode Lengkap]]
	- [[#7 Implementasi C++#7.2 Analisis Baris per Baris|7.2 Analisis Baris per Baris]]
		- [[#7.2 Analisis Baris per Baris#7.2.1 Typedef dan Konstanta Global|7.2.1 Typedef dan Konstanta Global]]
		- [[#7.2 Analisis Baris per Baris#7.2.2 Fungsi `enough`|7.2.2 Fungsi `enough`]]
		- [[#7.2 Analisis Baris per Baris#7.2.3 Ekspresi Binary Search Elegan|7.2.3 Ekspresi Binary Search Elegan]]
		- [[#7.2 Analisis Baris per Baris#7.2.4 Kondisi Loop|7.2.4 Kondisi Loop]]
- [[#8 Analisis Kompleksitas|8 Analisis Kompleksitas]]
	- [[#8 Analisis Kompleksitas#8.1 Kompleksitas Waktu|8.1 Kompleksitas Waktu]]
	- [[#8 Analisis Kompleksitas#8.2 Kompleksitas Ruang|8.2 Kompleksitas Ruang]]
	- [[#8 Analisis Kompleksitas#8.3 Analisis Iterasi Binary Search|8.3 Analisis Iterasi Binary Search]]
	- [[#8 Analisis Kompleksitas#8.4 Perbandingan dengan Pendekatan Lain|8.4 Perbandingan dengan Pendekatan Lain]]
- [[#9 Verifikasi Contoh|9 Verifikasi Contoh]]
	- [[#9 Verifikasi Contoh#9.1 Contoh: N = 2, M = 6, T[0] = 7, T[1] = 10|9.1 Contoh: N = 2, M = 6, T[0] = 7, T[1] = 10]]
		- [[#9.1 Contoh: N = 2, M = 6, T[0] = 7, T[1] = 10#9.1.1 Proses Binary Search|9.1.1 Proses Binary Search]]
		- [[#9.1 Contoh: N = 2, M = 6, T[0] = 7, T[1] = 10#9.1.2 Verifikasi Kelayakan τ = 28|9.1.2 Verifikasi Kelayakan τ = 28]]
		- [[#9.1 Contoh: N = 2, M = 6, T[0] = 7, T[1] = 10#9.1.3 Verifikasi Ketidaklayakan τ = 27|9.1.3 Verifikasi Ketidaklayakan τ = 27]]
		- [[#9.1 Contoh: N = 2, M = 6, T[0] = 7, T[1] = 10#9.1.4 Rekonstruksi Jadwal Optimal|9.1.4 Rekonstruksi Jadwal Optimal]]
- [[#10 Kesimpulan|10 Kesimpulan]]
	- [[#10 Kesimpulan#10.1 Ringkasan Temuan Utama|10.1 Ringkasan Temuan Utama]]
		- [[#10.1 Ringkasan Temuan Utama#10.1.1 Lapisan 1 — Kenali Mengapa Simulasi Langsung Gagal|10.1.1 Lapisan 1 — Kenali Mengapa Simulasi Langsung Gagal]]
		- [[#10.1 Ringkasan Temuan Utama#10.1.2 Lapisan 2 — Ubah Pertanyaan: Dari "Berapa?" Menjadi "Apakah Cukup?"|10.1.2 Lapisan 2 — Ubah Pertanyaan: Dari "Berapa?" Menjadi "Apakah Cukup?"]]
		- [[#10.1 Ringkasan Temuan Utama#10.1.3 Lapisan 3 — Manfaatkan Monotonisitas untuk Binary Search|10.1.3 Lapisan 3 — Manfaatkan Monotonisitas untuk Binary Search]]
	- [[#10 Kesimpulan#10.2 Pelajaran Algoritmik|10.2 Pelajaran Algoritmik]]
		- [[#10.2 Pelajaran Algoritmik#10.2.1 Tabel Ringkasan Konsep Kunci|10.2.1 Tabel Ringkasan Konsep Kunci]]
		- [[#10.2 Pelajaran Algoritmik#10.2.2 Greedy Langsung Tidak Optimal: Penjelasan Formal|10.2.2 Greedy Langsung Tidak Optimal: Penjelasan Formal]]
		- [[#10.2 Pelajaran Algoritmik#10.2.3 Mengapa `enough(time)` Benar secara Matematis|10.2.3 Mengapa `enough(time)` Benar secara Matematis]]
- [[#11 Referensi|11 Referensi]]



## 1 Pendahuluan

### 1.1 Latar Belakang

Permasalahan penjadwalan (_scheduling_) merupakan salah satu topik yang paling banyak dijumpai dalam dunia ilmu komputer, baik secara teoritis maupun praktis. Dari antrian proses pada sistem operasi, distribusi pekerjaan pada _cluster_ komputasi awan, hingga pengelolaan permintaan pada server web — semua pada dasarnya bermuara pada pertanyaan yang sama: **bagaimana mengalokasikan pekerjaan ke sumber daya secara efisien?**

Problem AU7_2 — SERVERS hadir sebagai representasi formal dari pertanyaan tersebut. Diberikan $N$ buah server, masing-masing dengan waktu pemrosesan tetap $T_i$ per task, dan sejumlah $M$ task yang harus diselesaikan, kita diminta menentukan **berapa waktu minimum** yang diperlukan agar seluruh $M$ task dapat tuntas diproses.

Yang membuat problem ini menarik secara algoritmik adalah adanya kebebasan dalam penugasan: sebuah task tidak harus langsung diberikan ke server yang sedang kosong. Jika menunggu sebentar memungkinkan task tersebut diproses oleh server yang lebih cepat, maka menunggu adalah pilihan yang valid. Kebebasan ini memperkenalkan trade-off yang tidak trivial, yang tidak dapat diselesaikan hanya dengan pendekatan greedy sederhana.

Solusi optimal problem ini memanfaatkan teknik **Binary Search on Answer** — sebuah paradigma yang mengubah pertanyaan optimasi menjadi serangkaian pertanyaan keputusan yang lebih mudah dijawab. Teknik ini merupakan salah satu contoh paling elegan dari transformasi masalah dalam algoritma kompetitif.

### 1.2 Relevansi dengan Teori Penjadwalan

Dalam teori penjadwalan (_scheduling theory_), problem AU7\_2 dapat diklasifikasikan sebagai varian dari **parallel machine scheduling**. Secara khusus, ia menyerupai model $P|p_j = T_i|C_{\max}$ dalam notasi Graham, di mana:

- Terdapat $N$ mesin paralel (_parallel machines_) yang tidak identik (_unrelated_), karena setiap server $i$ memiliki laju pemrosesan yang berbeda (invers dari $T_i$).
- Setiap task memiliki waktu pemrosesan yang bergantung pada mesin yang menanganinya — task yang diberikan ke server $i$ akan membutuhkan waktu tepat $T_i$.
- Tujuannya adalah meminimalkan _makespan_ $C_{\max}$, yaitu waktu penyelesaian task terakhir.

Relevansi teoritis inilah yang menjadikan problem ini bukan sekadar soal kompetitif, melainkan juga jembatan antara analisis algoritma dan aplikasi dunia nyata dalam sistem terdistribusi dan komputasi paralel.

### 1.3 Tujuan Laporan

Laporan ini bertujuan untuk:

1. Mendeskripsikan problem AU7_2 secara formal dan lengkap, beserta batasan dan sifat-sifatnya.
2. Menelusuri proses penemuan solusi secara sistematis, dari observasi awal hingga derivasi algoritma final.
3. Membuktikan kebenaran algoritma secara matematis, mencakup sifat monoton fungsi kelayakan dan invariant binary search.
4. Menganalisis kompleksitas waktu dan ruang solusi secara menyeluruh.
5. Melakukan verifikasi manual menggunakan contoh yang diberikan untuk mengonfirmasi kebenaran implementasi.

---

## 2 Spesifikasi Problem

### 2.1 Deskripsi Masalah

Diberikan $N$ server dan $M$ task. Setiap server $i$ (untuk $1 \le i \le N$) memiliki waktu pemrosesan tetap $T_i$, artinya server $i$ membutuhkan waktu tepat $T_i$ satuan waktu untuk menyelesaikan satu task, terlepas dari task mana yang sedang diproses.

Setiap task hanya dapat diproses oleh satu server, dan satu server hanya dapat memproses satu task dalam satu waktu. Namun, **task tidak harus langsung diberikan ke server yang kosong**. Jika pada suatu saat ada server $i$ yang kosong tetapi kita memilih untuk tidak memberikan task kepadanya, itu adalah keputusan yang sah — misalnya karena menunggu agar task tersebut dapat diberikan ke server $j$ yang lebih cepat (dengan $T_j < T_i$) yang sebentar lagi akan selesai.

Tujuan kita adalah menentukan **total waktu minimum** (dihitung dari waktu mulai hingga task terakhir selesai) untuk menyelesaikan seluruh $M$ task.

#### Batasan

- $1 \le N \le 100,000$
- $1 \le M \le 1,000,000,000$
- $T_i$ adalah bilangan bulat positif
- Gunakan tipe data `long long` (64-bit signed integer)

#### Format Input/Output

- Baris pertama: $T$ (jumlah test case)
- Untuk setiap test case: baris pertama berisi $N$ dan $M$, baris berikutnya berisi $N$ nilai $T_i$
- Output: satu baris per test case, berisi jawaban minimum

#### Contoh

```
Input:
1
2 6
7 10

Output:
28
```

### 2.2 Definisi Formal

Misalkan kita mendefinisikan notasi berikut:

- $[N] = {1, 2, \ldots, N}$: himpunan indeks server
- $T_i \in \mathbb{Z}^+$: waktu pemrosesan server $i$
- $M \in \mathbb{Z}^+$: jumlah task yang harus diselesaikan
- $\tau \in \mathbb{R}^+$: waktu total (makespan) yang dipertanyakan

**Definisi Kapasitas:** Dalam waktu $\tau$, server $i$ dapat menyelesaikan paling banyak $\lfloor \tau / T_i \rfloor$ task, karena ia menyelesaikan satu task setiap $T_i$ satuan waktu dan waktu yang tersedia adalah $\tau$.

**Definisi Kelayakan:** Waktu $\tau$ dikatakan **layak** (_feasible_) jika dan hanya jika total kapasitas seluruh server dalam waktu $\tau$ paling sedikit $M$:

$$\text{feasible}(\tau) \iff \sum_{i=1}^{N} \left\lfloor \frac{\tau}{T_i} \right\rfloor \ge M$$

**Tujuan (Formal):** Tentukan:

$$\tau^* = \min{\tau \in \mathbb{Z}^+ \mid \text{feasible}(\tau)}$$

yaitu nilai integer positif terkecil sedemikian sehingga seluruh $M$ task dapat diselesaikan.

### 2.3 Analisis Struktur Problem

Sebelum merancang algoritma, penting untuk memahami struktur fundamental problem ini.

**Sifat 1 — Diskretisasi Alami:** Meskipun $\tau$ secara teknis bisa berupa bilangan real, jawaban optimalnya selalu berupa kelipatan bulat dari salah satu $T_i$. Ini karena setiap penambahan kapasitas terjadi secara diskret: kapasitas server $i$ bertambah tepat satu task setiap kali $\tau$ naik melewati kelipatan $T_i$.

**Sifat 2 — Independensi Antar Server:** Kapasitas total adalah penjumlahan kapasitas individual, dan kapasitas setiap server bergantung hanya pada $T_i$ dan $\tau$, bukan pada server lain. Ini memungkinkan kita menghitung feasibility dalam $O(N)$.

**Sifat 3 — Kebebasan Penugasan:** Karena task bisa menunggu, jadwal optimal tidak harus bersifat _work-conserving_ (langsung memberikan task ke server yang kosong). Ini adalah poin paling kritis yang membedakan problem ini dari problem penjadwalan standar.

---

## 3 Landasan Teori

### 3.1 Binary Search on Answer

**Binary Search on Answer** (kadang disebut _parametric search_) adalah teknik algoritmik yang mengubah sebuah masalah optimasi menjadi serangkaian masalah keputusan dengan memanfaatkan sifat monoton pada domain jawaban.

Secara umum, teknik ini diterapkan ketika:

1. Jawaban yang dicari berada dalam suatu rentang $[lo, hi]$ yang terurut.
2. Terdapat fungsi predikat $P(\tau)$ yang bersifat **monoton**: jika $P(\tau)$ bernilai benar, maka $P(\tau')$ juga bernilai benar untuk semua $\tau' \ge \tau$.
3. Fungsi $P(\tau)$ dapat dievaluasi dalam waktu yang efisien.

Jika ketiga kondisi terpenuhi, kita dapat "membagi dua" ruang pencarian secara berulang:

```
low = batas_bawah, high = batas_atas
while (high - low > 1):
    mid = (low + high) / 2
    if P(mid):
        high = mid
    else:
        low = mid
return high
```

Invariant yang dijaga: $P(\text{high})$ selalu bernilai benar dan $P(\text{low})$ selalu bernilai salah. Ketika $\text{high} - \text{low} = 1$, `high` adalah jawaban terkecil yang memenuhi $P$.

Jumlah iterasi adalah $O(\log(\text{high} - \text{low}))$, sehingga total kompleksitas adalah $O(f(N) \cdot \log(\text{range}))$ di mana $f(N)$ adalah biaya evaluasi $P$.

### 3.2 Teori Kapasitas Server

Misalkan kita memberi server $i$ waktu sebesar $\tau$ satuan. Karena setiap task membutuhkan $T_i$ waktu dan server bekerja secara kontinu (tanpa idle di antara task yang diberikan kepadanya), maka:

$$\text{kapasitas}(i, \tau) = \left\lfloor \frac{\tau}{T_i} \right\rfloor$$

Ini adalah konsekuensi langsung dari fakta bahwa $\tau / T_i$ mungkin bukan bilangan bulat. Server tidak dapat menyelesaikan task "setengah jalan" — sebuah task hanya dihitung selesai jika proses penuh $T_i$ telah berlalu.

**Total kapasitas** seluruh sistem dalam waktu $\tau$:

$$C(\tau) = \sum_{i=1}^{N} \left\lfloor \frac{\tau}{T_i} \right\rfloor$$

Fungsi $C(\tau)$ bersifat **non-decreasing** (monoton tidak menurun) terhadap $\tau$: menambah waktu tidak pernah mengurangi kapasitas.

### 3.3 Prinsip Penjadwalan Optimal

Klaim kunci dalam problem ini adalah: **jadwal optimal selalu dapat direalisasikan tanpa konflik** selama $C(\tau^*) \ge M$.

Mengapa ini benar? Karena kita memiliki kebebasan penuh dalam penugasan. Secara konstruktif, jadwal optimal dapat dibangun sebagai berikut:

1. Urutkan task dari 1 hingga $M$.
2. Untuk setiap task, berikan ke server yang akan selesai paling awal (dengan mempertimbangkan task-task sebelumnya yang sudah diberikan ke server tersebut).
3. Karena total slot yang tersedia dalam waktu $\tau^*$ adalah tepat $\ge M$, setiap task akan mendapatkan slot.

Prinsip ini analog dengan **Hall's Marriage Theorem** dalam teori kombinatorika: matching yang valid selalu ada selama kondisi kapasitas terpenuhi secara global.

### 3.4 Struktur Matematika Kunci: Fungsi Lantai

Fungsi lantai $\lfloor x \rfloor$ (floor function) mendefinisikan bilangan bulat terbesar yang tidak melebihi $x$. Beberapa properti yang relevan:

- $\lfloor x \rfloor \le x < \lfloor x \rfloor + 1$
- $\lfloor a \cdot k \rfloor \ge k \cdot \lfloor a \rfloor$ untuk $a, k \ge 0$
- $\sum_{i} \lfloor \tau / T_i \rfloor$ adalah fungsi tangga yang nilainya bertambah tepat satu setiap kali $\tau$ melewati kelipatan salah satu $T_i$

Sifat terakhir ini menjelaskan mengapa jawaban selalu berupa kelipatan dari salah satu $T_i$: hanya di titik-titik itulah total kapasitas bisa bertambah.

---

## 4 Analisis Problem: Proses Penemuan Solusi

### 4.1 Observasi Awal

Titik awal yang paling natural adalah bertanya: _kapan sebuah waktu $\tau$ cukup untuk menyelesaikan $M$ task?_

Jika kita memiliki waktu sebesar $\tau$, server $i$ dapat menyelesaikan $\lfloor \tau / T_i \rfloor$ task. Jika kita menjumlahkan seluruh kapasitas ini dan hasilnya $\ge M$, maka $\tau$ cukup — kita tinggal mendistribusikan $M$ task ke slot-slot yang ada.

Jika kita menyebut pertanyaan "apakah $\tau$ cukup?" sebagai **masalah keputusan**, maka:

$$P(\tau) \iff \sum_{i=1}^{N} \left\lfloor \frac{\tau}{T_i} \right\rfloor \ge M$$

Observasi ini adalah fondasi seluruh solusi.

### 4.2 Eksplorasi Brute Force dan Kegagalannya

Pendekatan naif pertama yang mungkin terpikirkan adalah simulasi langsung:

- Gunakan priority queue berisi pasangan $(t_{\text{selesai}}, i)$ untuk setiap server $i$.
- Awalnya, semua server siap di $t = 0$.
- Untuk setiap task, ambil server yang selesai paling awal, berikan task, dan masukkan kembali dengan $t_{\text{selesai}} + T_i$.

Kompleksitas pendekatan ini adalah $O(M \log N)$. Dengan $M$ hingga $10^9$, ini menghasilkan hingga $10^9 \cdot \log(10^5) \approx 1.7 \times 10^{10}$ operasi — jauh melewati batas waktu yang wajar (biasanya $10^8$ hingga $10^9$ operasi per detik).

Bahkan jika kita mengoptimalkan dengan batch assignment (berikan beberapa task sekaligus ke server yang sama), kompleksitasnya masih tidak dapat direduksi secara signifikan tanpa perubahan paradigma.

**Kesimpulan:** Simulasi langsung tidak layak untuk constraint problem ini. Kita perlu pendekatan yang sama sekali berbeda.

### 4.3 Penemuan Properti Monoton: Kunci Transformasi

Perhatikan fungsi $C(\tau) = \sum_{i=1}^{N} \lfloor \tau / T_i \rfloor$. Untuk $\tau_1 \le \tau_2$:

$$\left\lfloor \frac{\tau_1}{T_i} \right\rfloor \le \left\lfloor \frac{\tau_2}{T_i} \right\rfloor \quad \forall i$$

Karena setiap suku tidak menurun, jumlahnya juga tidak menurun:

$$C(\tau_1) \le C(\tau_2)$$

Konsekuensinya, jika $P(\tau)$ bernilai benar (yaitu $C(\tau) \ge M$), maka untuk semua $\tau' > \tau$:

$$C(\tau') \ge C(\tau) \ge M \implies P(\tau') \text{ juga benar}$$

Dan jika $P(\tau)$ bernilai salah ($C(\tau) < M$), maka untuk semua $\tau'' < \tau$:

$$C(\tau'') \le C(\tau) < M \implies P(\tau'') \text{ juga salah}$$

Ini adalah **properti monoton** yang dibutuhkan untuk binary search: fungsi predikat $P$ berbentuk $[\text{false}, \text{false}, \ldots, \text{false}, \text{true}, \text{true}, \ldots, \text{true}]$ pada domain integer yang terurut. Kita tinggal mencari titik transisi pertamanya.

### 4.4 Reformulasi sebagai Masalah Keputusan

Alih-alih bertanya "berapa nilai minimum $\tau^*$?", kita reformulasikan menjadi:

**Untuk nilai $\tau$ tertentu, apakah mungkin menyelesaikan $M$ task dalam waktu $\tau$?**

Dengan binary search, kita cari $\tau^*$ terkecil yang membuat jawaban pertanyaan keputusan ini adalah "ya". Karena sifat monoton telah dibuktikan, binary search bekerja dengan benar.

### 4.5 Derivasi Formula Kapasitas

Mengapa kapasitas server $i$ dalam waktu $\tau$ adalah tepat $\lfloor \tau / T_i \rfloor$?

Bayangkan garis waktu dari $0$ hingga $\tau$. Server $i$ menyelesaikan task pertamanya pada $T_i$, task kedua pada $2T_i$, task ketiga pada $3T_i$, dan seterusnya. Task ke-$k$ selesai pada $k \cdot T_i$.

Task ke-$k$ tersebut diselesaikan dalam waktu $\tau$ jika dan hanya jika $k \cdot T_i \le \tau$, yaitu $k \le \tau / T_i$. Karena $k$ harus bilangan bulat positif, jumlah maksimum task yang dapat diselesaikan adalah:

$$\max{k \in \mathbb{Z}^+ \mid k \le \tau / T_i} = \left\lfloor \frac{\tau}{T_i} \right\rfloor$$

Ini valid karena task-task diproses secara berurutan tanpa jeda (server tidak pernah idle secara sukarela di antara task yang diberikan kepadanya).

### 4.6 Penentuan Batas Pencarian Biner

Kita perlu menentukan interval $[\text{low}, \text{high}]$ untuk binary search.

**Batas bawah (`low`):** Nilai $\tau = 0$ jelas tidak layak untuk $M \ge 1$ (tidak ada task yang bisa diselesaikan). Jadi `low = 0`.

**Batas atas (`high`):** Kita membutuhkan nilai yang pasti layak. Dalam kasus terburuk, kita hanya menggunakan server pertama ($i = 0$, yang merupakan server dengan indeks pertama dalam input). Server ini membutuhkan $T_0 \cdot M$ waktu untuk menyelesaikan semua $M$ task sendiri. Oleh karena itu, `high = T[0] * M` adalah upper bound yang valid.

Perlu dicatat bahwa `T[0]` tidak harus merupakan server tercepat. Namun, ini tetap menjadi upper bound yang valid karena selalu mungkin menyelesaikan $M$ task hanya dengan satu server.

**Pertimbangan Overflow:** Dengan $T_i$ bisa besar dan $M$ hingga $10^9$, perkalian `T[0] * M` bisa melampaui kapasitas `int` (sekitar $2.1 \times 10^9$). Oleh karena itu, cast ke `long long` sebelum perkalian adalah wajib: `(LL)t[0] * m`.

### 4.7 Optimasi Kelayakan: Early Termination

Dalam fungsi `enough(time)`, begitu kita menemukan bahwa total kapasitas yang terkumpul sudah $\ge M$, tidak ada gunanya melanjutkan iterasi ke server-server berikutnya. Ini adalah optimasi _early termination_ yang dapat secara signifikan mempercepat eksekusi dalam kasus rata-rata.

Kondisi terminasi dini yang digunakan dalam kode adalah:

```cpp
if (here >= m || here + cnt >= m)
    return true;
```

- `here >= m`: server ini saja sudah cukup untuk memenuhi seluruh $M$ task — tidak perlu menjumlah dengan server lain.
- `here + cnt >= m`: kapasitas server ini ditambah kapasitas yang sudah terkumpul sebelumnya sudah mencukupi $M$ task.

Kedua kondisi ini setara dengan `cnt + here >= m`, tetapi dengan pemeriksaan `here >= m` lebih dulu untuk menghindari potensi overflow saat `cnt + here` dihitung.

---

## 5 Pembuktian Kebenaran Algoritma

### 5.1 Teorema Utama

**Teorema:** Algoritma binary search pada jawaban, dengan fungsi predikat $\text{feasible}(\tau) \iff \sum_{i=1}^{N} \lfloor \tau / T_i \rfloor \ge M$, menghasilkan nilai minimum $\tau^*$ sedemikian sehingga seluruh $M$ task dapat diselesaikan dalam waktu $\tau^*$.

**Bukti (sketsa):**

Diperlukan dua klaim:

1. $\text{feasible}(\tau^*)$ bernilai benar.
2. Untuk semua $\tau < \tau^*$, $\text{feasible}(\tau)$ bernilai salah.
3. Binary search dengan invariant yang benar menghasilkan $\tau^*$.

Klaim 1 dan 2 berikut langsung dari definisi $\tau^*$ sebagai nilai minimum yang layak. Klaim 3 dibuktikan melalui invariant di bawah.

### 5.2 Bukti Invariant Binary Search

**Invariant:** Pada setiap iterasi, berlaku bahwa $\text{feasible}(\text{high})$ benar dan $\text{feasible}(\text{low})$ salah.

**Basis (sebelum iterasi pertama):**

- `low = 0`: $C(0) = \sum_i \lfloor 0 / T_i \rfloor = 0 < M$ (karena $M \ge 1$), jadi $\text{feasible}(0)$ salah. ✓
- `high = T[0] * M`: $C(T_0 \cdot M) \ge \lfloor T_0 \cdot M / T_0 \rfloor = M$, jadi $\text{feasible}(T_0 \cdot M)$ benar. ✓

**Langkah Induktif:** Misalkan invariant terpenuhi sebelum iterasi. Kita hitung $\text{mid} = (\text{low} + \text{high}) / 2$.

- Jika $\text{feasible}(\text{mid})$ benar: kita set `high = mid`. Invariant baru: $\text{feasible}(\text{high}) = \text{feasible}(\text{mid})$ benar ✓; $\text{feasible}(\text{low})$ masih salah (tidak berubah) ✓.
- Jika $\text{feasible}(\text{mid})$ salah: kita set `low = mid`. Invariant baru: $\text{feasible}(\text{high})$ masih benar (tidak berubah) ✓; $\text{feasible}(\text{low}) = \text{feasible}(\text{mid})$ salah ✓.

**Terminasi:** Ketika `high - low = 1`, loop berhenti. Pada titik ini, `low` adalah nilai terbesar yang tidak layak dan `high` adalah nilai terkecil yang layak. Karena `high - low = 1` dan keduanya integer, `high` adalah nilai integer minimum yang layak, yaitu $\tau^*$. $\blacksquare$

### 5.3 Bukti Ekuivalensi Kelayakan

**Klaim:** Waktu $\tau$ layak (dalam artian ada penjadwalan yang valid menyelesaikan $M$ task) jika dan hanya jika $\sum_{i=1}^{N} \lfloor \tau / T_i \rfloor \ge M$.

**Arah ($\Rightarrow$):** Jika ada jadwal valid, maka setiap task diselesaikan oleh tepat satu server dalam waktu $\tau$. Server $i$ menyelesaikan paling banyak $\lfloor \tau / T_i \rfloor$ task dalam waktu $\tau$ (karena setiap task butuh $T_i$ waktu). Total task yang diselesaikan semua server $\le \sum_i \lfloor \tau / T_i \rfloor$. Agar jadwal valid dengan $M$ task, perlu $\sum_i \lfloor \tau / T_i \rfloor \ge M$.

**Arah ($\Leftarrow$):** Jika $\sum_i \lfloor \tau / T_i \rfloor \ge M$, kita perlu menunjukkan bahwa jadwal valid ada. Konstruksi eksplisit:

Urutkan server berdasarkan $T_i$. Definisikan slot-slot sebagai pasangan $(i, k)$ di mana $1 \le k \le \lfloor \tau / T_i \rfloor$, yang merepresentasikan "task ke-$k$ pada server $i$ selesai pada waktu $k \cdot T_i$". Slot ini valid karena $k \cdot T_i \le \tau$.

Karena total slot yang tersedia $\ge M$, kita dapat memetakan $M$ task ke $M$ slot berbeda. Tidak ada konflik karena setiap server mengerjakan task-tasknya secara sekuensial, dan $k$-th task server $i$ hanya membutuhkan task ke-$(k-1)$ dari server yang sama selesai terlebih dahulu (bukan dari server lain). $\blacksquare$

---

## 6 Pseudokode

### 6.1 Penjelasan Alur Algoritma

```
Fungsi ENOUGH(time, T[1..N], M):
    cnt ← 0                        // akumulator kapasitas yang terkumpul
    untuk i dari 1 hingga N:
        here ← floor(time / T[i])  // kapasitas server i dalam waktu 'time'
        jika here ≥ M atau cnt + here ≥ M:
            kembalikan BENAR        // early termination
        cnt ← cnt + here
    kembalikan (cnt ≥ M)

Fungsi SOLVE(N, M, T[1..N]):
    low  ← 0                       // pasti tidak layak
    high ← T[1] × M                // pasti layak (server pertama saja sudah cukup)
    
    selama (high - low > 1):
        mid ← (low + high) / 2
        jika ENOUGH(mid, T, M):
            high ← mid             // mid layak, perbaiki upper bound
        selain itu:
            low ← mid              // mid tidak layak, perbaiki lower bound
    
    kembalikan high                // nilai integer minimum yang layak
```

### 6.2 Catatan Implementasi Kritis

Beberapa catatan penting terkait implementasi:

1. **Tipe data `long long`:** Variabel `cnt`, `here`, `low`, `high`, dan `mid` harus bertipe `long long`. Nilai `cnt` bisa mencapai $N \cdot M / T_{\min}$ yang bisa sangat besar. Nilai `high` bisa mencapai $T_0 \cdot M \approx 10^{18}$ dalam kasus ekstrem.
    
2. **Overflow pada `cnt + here`:** Meskipun keduanya `long long`, penjumlahan tetap bisa overflow jika $N = 10^5$ dan setiap server memiliki kapasitas $10^9$. Kondisi `here >= m` yang diperiksa lebih dulu berperan sebagai safeguard.
    
3. **Inisialisasi `high`:** Menggunakan `(LL)t[0] * m` bukan `t[0] * m` untuk mencegah integer overflow sebelum assignment ke `high`.
    
4. **Kondisi loop `high - low > 1`:** Bukan `low < high`. Ini memastikan loop berhenti tepat ketika `high` dan `low` adalah dua nilai berurutan, dan `high` adalah jawaban.
    

---

## 7 Implementasi C++

### 7.1 Kode Lengkap

```cpp
#include <cstdio>
typedef long long LL;
#define MAXN 100002
int n, m;
int t[MAXN];

bool enough(LL time)
{
  LL cnt = 0;
  for (int i = 0; i < n; ++i)
  {
    LL here = time / t[i];
    if (here >= m || here + cnt >= m)
      return true;
    cnt += here;
  }
  return cnt >= m;
}

int main()
{
  int T;
  scanf("%d", &T);
  while (T--)
  {
    scanf("%d%d", &n, &m);
    for (int i = 0; i < n; ++i)
      scanf("%d", &t[i]);
    LL low = 0, high = (LL)t[0] * m;
    while (high - low > 1)
    {
      LL mid = (low + high) / 2;
      (enough(mid) ? high : low) = mid;
    }
    printf("%lld\n", high);
  }
  return 0;
}
```

### 7.2 Analisis Baris per Baris

#### 7.2.1 Typedef dan Konstanta Global

```cpp
typedef long long LL;
#define MAXN 100002
int n, m;
int t[MAXN];
```

- `typedef long long LL`: Alias untuk tipe 64-bit signed integer. Rentangnya mencakup $[-2^{63}, 2^{63}-1] \approx [-9.2 \times 10^{18}, 9.2 \times 10^{18}]$. Ini penting karena nilai `high` bisa mencapai $T_{\max} \cdot M \approx 10^{18}$.
- `#define MAXN 100002`: Array global dengan ukuran $N_{\max} + 2$ sebagai buffer keamanan.
- `int n, m`: Variabel global untuk menghindari overhead passing argumen berulang ke fungsi `enough`. Pada problem dengan $T$ test case, ini adalah pola umum di competitive programming.
- `int t[MAXN]`: Array waktu pemrosesan. Tipe `int` cukup karena $T_i$ tidak disebutkan batasnya secara eksplisit, tapi umumnya dalam rentang `int`.

#### 7.2.2 Fungsi `enough`

```cpp
bool enough(LL time)
{
  LL cnt = 0;
  for (int i = 0; i < n; ++i)
  {
    LL here = time / t[i];
    if (here >= m || here + cnt >= m)
      return true;
    cnt += here;
  }
  return cnt >= m;
}
```

Fungsi ini mengimplementasikan predikat $\text{feasible}(\tau)$ secara langsung.

- `LL cnt = 0`: Akumulator kapasitas. Bertipe `long long` karena bisa mencapai nilai besar.
- `LL here = time / t[i]`: Menghitung $\lfloor \tau / T_i \rfloor$ menggunakan pembagian integer. Karena `time` bertipe `LL` dan `t[i]` bertipe `int`, C++ secara otomatis melakukan integer division dengan hasil tipe `LL` — yaitu $\lfloor \tau / T_i \rfloor$ tanpa perlu `floor()` eksplisit.
- Kondisi `here >= m`: Jika server $i$ saja sudah cukup menyelesaikan $M$ task, langsung return. Kondisi ini juga mencegah overflow pada `here + cnt` jika `here` sendiri sudah sangat besar.
- Kondisi `here + cnt >= m`: Jika kapasitas kumulatif sudah mencukupi, return true. Ini adalah early termination.
- `cnt += here`: Akumulasi kapasitas.
- `return cnt >= m`: Jika loop selesai tanpa early termination, periksa apakah total kapasitas mencukupi.

Satu hal yang perlu dicatat: fungsi ini bekerja dengan asumsi `t[i] > 0`, yang terjamin oleh constraint problem.

#### 7.2.3 Ekspresi Binary Search Elegan

```cpp
(enough(mid) ? high : low) = mid;
```

Ini adalah cara yang sangat ringkas untuk mengekspresikan logika binary search. Ekspresi ternary `(enough(mid) ? high : low)` menghasilkan _lvalue_ (reference) ke salah satu variabel. Kemudian `= mid` mengassign nilai `mid` ke variabel tersebut.

Secara semantik, ini setara dengan:

```cpp
if (enough(mid))
    high = mid;
else
    low = mid;
```

Keeleganan idiom ini sering ditemui dalam solusi competitive programming. Keduanya benar secara fungsional; pilihan adalah gaya penulisan.

#### 7.2.4 Kondisi Loop

```cpp
while (high - low > 1)
```

Kondisi ini memastikan loop berjalan selama `high` dan `low` bukan dua nilai berurutan. Ketika `high - low = 1`, kita sudah mendapatkan dua nilai: satu yang tidak layak (`low`) dan satu yang layak (`high`). Nilai minimum yang layak adalah `high`.

Variasi umum lainnya adalah `while (low < high)` dengan logika berbeda, tetapi versi `high - low > 1` lebih langsung untuk kasus di mana kita mencari "nilai integer minimum yang memenuhi P".

---

## 8 Analisis Kompleksitas

### 8.1 Kompleksitas Waktu

**Per evaluasi `enough(time)`:** Fungsi ini melakukan iterasi atas $N$ server. Dalam kasus terburuk (tidak ada early termination), ini adalah $O(N)$.

**Jumlah iterasi binary search:** Rentang pencarian adalah $[\text{low}, \text{high}] = [0, T_0 \cdot M]$. Panjang rentang awal adalah $T_0 \cdot M$. Setiap iterasi membagi rentang menjadi setengahnya. Jumlah iterasi adalah:

$$\left\lceil \log_2(T_0 \cdot M) \right\rceil$$

Dengan $T_0$ dan $M$ paling besar $\sim 10^9$, nilai ini adalah $\lceil \log_2(10^{18}) \rceil = \lceil 59.8 \rceil = 60$ iterasi.

**Total kompleksitas per test case:** $O(N \log(T_{\max} \cdot M))$

Dengan $N = 10^5$ dan $\log(T_{\max} \cdot M) \approx 60$, ini berarti sekitar $6 \times 10^6$ operasi per test case — sangat efisien.

**Catatan Tentang Early Termination:** Dalam praktiknya, early termination dalam `enough` bisa mengurangi jumlah iterasi rata-rata secara signifikan, terutama ketika ada server yang sangat cepat (nilai $T_i$ kecil) yang saja dapat memenuhi kapasitas.

### 8.2 Kompleksitas Ruang

- Array `t[MAXN]`: $O(N)$ ruang.
- Variabel lokal (low, high, mid, cnt, here): $O(1)$ ruang tambahan.
- **Total:** $O(N)$ per test case (ruang array di-reuse antar test case).

Tidak ada alokasi dinamis, sehingga tidak ada overhead dari heap allocation.

### 8.3 Analisis Iterasi Binary Search

Untuk contoh yang diberikan ($N = 2, M = 6, T = [7, 10]$):

- Rentang awal: $[0, 7 \times 6] = [0, 42]$
- Panjang rentang: 42
- Iterasi maksimum: $\lceil \log_2(42) \rceil = 6$ iterasi

Tabel iterasi:

|Iter|low|high|mid|enough(mid)|Aksi|
|---|---|---|---|---|---|
|1|0|42|21|Salah|low = 21|
|2|21|42|31|Benar|high = 31|
|3|21|31|26|Salah|low = 26|
|4|26|31|28|Benar|high = 28|
|5|26|28|27|Salah|low = 27|
|6|27|28|—|—|Stop (27+1=28)|

Setelah 5 iterasi efektif, `high = 28 = low + 1`, loop berhenti, output `28`. ✓

### 8.4 Perbandingan dengan Pendekatan Lain

|Pendekatan|Kompleksitas Waktu|Layak untuk $M = 10^9$?|
|---|---|---|
|Simulasi greedy dengan PQ|$O(M \log N)$|Tidak ($\sim 10^{10}$ ops)|
|Iterasi semua kelipatan $T_i$|$O(N \cdot M / T_{\min})$|Tidak|
|DP pada waktu|$O(T_{\max} \cdot M)$|Tidak|
|**Binary Search on Answer**|$O(N \log(T_{\max} \cdot M))$|**Ya** ($\sim 6 \times 10^6$ ops)|

Keunggulan binary search on answer sangat jelas: kompleksitasnya hanya logaritmik terhadap $M$, sehingga tidak terpengaruh secara signifikan oleh besarnya $M$.

---

## 9 Verifikasi Contoh

### 9.1 Contoh: N = 2, M = 6, T[0] = 7, T[1] = 10

#### 9.1.1 Proses Binary Search

Inisialisasi: `low = 0`, `high = 7 × 6 = 42`.

**Iterasi 1:** `mid = (0 + 42) / 2 = 21`

`enough(21)`:

- Server 0: $\lfloor 21 / 7 \rfloor = 3$, cnt = 3 (< 6)
- Server 1: $\lfloor 21 / 10 \rfloor = 2$, cnt = 5 (< 6)
- Selesai, total = 5 < 6 → **Salah**

Aksi: `low = 21`

**Iterasi 2:** `mid = (21 + 42) / 2 = 31`

`enough(31)`:

- Server 0: $\lfloor 31 / 7 \rfloor = 4$, cnt = 4 (< 6)
- Server 1: $\lfloor 31 / 10 \rfloor = 3$, cnt + here = 4 + 3 = 7 ≥ 6 → **Benar**

Aksi: `high = 31`

**Iterasi 3:** `mid = (21 + 31) / 2 = 26`

`enough(26)`:

- Server 0: $\lfloor 26 / 7 \rfloor = 3$, cnt = 3 (< 6)
- Server 1: $\lfloor 26 / 10 \rfloor = 2$, cnt = 5 (< 6)
- Total = 5 < 6 → **Salah**

Aksi: `low = 26`

**Iterasi 4:** `mid = (26 + 31) / 2 = 28`

`enough(28)`:

- Server 0: $\lfloor 28 / 7 \rfloor = 4$, cnt = 4 (< 6)
- Server 1: $\lfloor 28 / 10 \rfloor = 2$, cnt + here = 4 + 2 = 6 ≥ 6 → **Benar**

Aksi: `high = 28`

**Iterasi 5:** `mid = (26 + 28) / 2 = 27`

`enough(27)`:

- Server 0: $\lfloor 27 / 7 \rfloor = 3$, cnt = 3 (< 6)
- Server 1: $\lfloor 27 / 10 \rfloor = 2$, cnt = 5 (< 6)
- Total = 5 < 6 → **Salah**

Aksi: `low = 27`

**Loop berhenti:** `high - low = 28 - 27 = 1`, kondisi `high - low > 1` tidak terpenuhi.

**Output: `high = 28`** ✓

#### 9.1.2 Verifikasi Kelayakan τ = 28

Kita verifikasi bahwa $\tau = 28$ memang cukup untuk 6 task:

$$C(28) = \left\lfloor \frac{28}{7} \right\rfloor + \left\lfloor \frac{28}{10} \right\rfloor = 4 + 2 = 6 \ge 6 \checkmark$$

Total kapasitas tepat $M = 6$, sehingga layak.

#### 9.1.3 Verifikasi Ketidaklayakan τ = 27

$$C(27) = \left\lfloor \frac{27}{7} \right\rfloor + \left\lfloor \frac{27}{10} \right\rfloor = 3 + 2 = 5 < 6$$

Total kapasitas hanya 5, kurang dari $M = 6$. Tidak layak. ✓

Ini mengonfirmasi bahwa $\tau^* = 28$ adalah nilai minimum yang layak.

#### 9.1.4 Rekonstruksi Jadwal Optimal

Berikut adalah jadwal konkret yang menyelesaikan 6 task dalam waktu 28:

|Task|Diberikan ke Server|Mulai|Selesai|
|---|---|---|---|
|1|Server 0 ($T_0=7$)|0|7|
|2|Server 1 ($T_1=10$)|0|10|
|3|Server 0 ($T_0=7$)|7|14|
|4|Server 0 ($T_0=7$)|14|21|
|5|Server 1 ($T_1=10$)|10|20|
|6|Server 0 ($T_0=7$)|21|28|

Server 0 menyelesaikan task pada $t = 7, 14, 21, 28$ (4 task total). Server 1 menyelesaikan task pada $t = 10, 20$ (2 task total). Total: 6 task, makespan = 28. ✓

Perhatikan bahwa jadwal ini adalah **greedy optimal**: selalu berikan task ke server yang paling awal selesai. Namun penting untuk dipahami bahwa kita tidak perlu mensimulasikan jadwal ini — kita hanya perlu memverifikasi bahwa kapasitas total mencukupi.

---

## 10 Kesimpulan

### 10.1 Ringkasan Temuan Utama

Problem AU7_2 SERVERS mengajarkan pola berpikir yang berlapis dalam mendekomposisi masalah optimasi yang tampaknya membutuhkan simulasi eksplisit menjadi masalah keputusan yang dapat diselesaikan secara efisien.

#### 10.1.1 Lapisan 1 — Kenali Mengapa Simulasi Langsung Gagal

Pertanyaan pertama yang harus diajukan adalah: **mengapa kita tidak bisa langsung mensimulasikan penugasan task ke server?**

Perhatikan contoh dengan $N = 2$, $M = 6$, $T = [7, 10]$. Pendekatan greedy naif adalah: setiap kali ada task yang belum diproses, berikan ke server yang paling cepat selesai menggunakan priority queue. Tracing-nya:

|Waktu|Event|PQ setelah event|
|---|---|---|
|0|Task 1 → Server 0 (T=7)|{(7,0), (∞,1)}|
|0|Task 2 → Server 1 (T=10)|{(7,0), (10,1)}|
|7|Server 0 selesai, Task 3 → Server 0|{(10,1), (14,0)}|
|10|Server 1 selesai, Task 4 → Server 1|{(14,0), (20,1)}|
|14|Server 0 selesai, Task 5 → Server 0|{(20,1), (21,0)}|
|20|Server 1 selesai, Task 6 → Server 1|{(21,0), (30,1)}|
|30|Server 1 selesai|selesai|

Simulasi greedy menghasilkan makespan $= 30$, **bukan 28**. Mengapa? Karena greedy work-conserving langsung memberikan task ke server yang kosong tanpa mempertimbangkan apakah menunggu server lebih cepat akan menghasilkan makespan lebih kecil. Pada $t = 20$, Task 6 diberikan ke Server 1 ($T=10$) padahal Server 0 ($T=7$) akan selesai di $t = 21$ — selisih hanya 1 satuan — dan jika Task 6 menunggu Server 0, ia selesai di $t = 28 < 30$.

Dengan $M$ hingga $10^9$, bahkan simulasi yang "benar" pun tidak layak secara komputasional — kompleksitasnya $O(M \log N)$ menghasilkan hingga $\sim 10^{10}$ operasi.

#### 10.1.2 Lapisan 2 — Ubah Pertanyaan: Dari "Berapa?" Menjadi "Apakah Cukup?"

Daripada bertanya _berapa waktu minimum yang dibutuhkan_, tanyakan: **apakah waktu $\tau$ cukup untuk menyelesaikan seluruh $M$ task?**

Kunci dari transformasi ini adalah fungsi kapasitas. Dalam waktu $\tau$, server $i$ dapat menyelesaikan tepat $\lfloor \tau / T_i \rfloor$ task — satu task setiap $T_i$ satuan waktu, dan hanya task yang sepenuhnya selesai yang dihitung. Untuk contoh $\tau = 28$:

$$C(28) = \left\lfloor \frac{28}{7} \right\rfloor + \left\lfloor \frac{28}{10} \right\rfloor = 4 + 2 = 6 \geq M \checkmark$$

Untuk $\tau = 27$:

$$C(27) = \left\lfloor \frac{27}{7} \right\rfloor + \left\lfloor \frac{27}{10} \right\rfloor = 3 + 2 = 5 < M \times$$

Transformasi ini mengubah masalah yang memerlukan simulasi $O(M)$ menjadi sebuah pengecekan $O(N)$.

#### 10.1.3 Lapisan 3 — Manfaatkan Monotonisitas untuk Binary Search

Begitu fungsi predikat $\text{feasible}(\tau) \iff C(\tau) \geq M$ terdefinisi, sifat monotonik $C(\tau)$ menjamin bahwa struktur nilai `feasible` pada domain integer membentuk pola: $[\texttt{false}, \ldots, \texttt{false}, \texttt{true}, \ldots, \texttt{true}]$. Binary search menemukan titik transisi pertama dalam $O(\log(T_0 \cdot M))$ iterasi, masing-masing dengan biaya $O(N)$.

Inilah inti solusi: **bukan simulasikan jadwalnya, tapi binary search pada jawabannya**.

---

### 10.2 Pelajaran Algoritmik

#### 10.2.1 Tabel Ringkasan Konsep Kunci

|Konsep|Rumus / Properti|Relevansi dalam Problem|
|---|---|---|
|Kapasitas server $i$|$\lfloor \tau / T_i \rfloor$|Berapa task dapat diselesaikan server $i$ dalam waktu $\tau$|
|Total kapasitas sistem|$C(\tau) = \sum_{i=1}^{N} \lfloor \tau / T_i \rfloor$|Fungsi predikat kelayakan|
|Sifat monoton $C(\tau)$|$\tau_1 \leq \tau_2 \Rightarrow C(\tau_1) \leq C(\tau_2)$|Menjamin binary search bekerja|
|Predikat kelayakan|$\text{feasible}(\tau) \iff C(\tau) \geq M$|Inti masalah keputusan|
|Batas bawah binary search|$\text{low} = 0$|$C(0) = 0 < M$, pasti tidak layak|
|Batas atas binary search|$\text{high} = T_0 \cdot M$|Server 0 saja cukup untuk $M$ task|
|Kondisi loop|$\text{high} - \text{low} > 1$|Berhenti saat $\text{high}$ adalah jawaban minimum|
|Early termination|`if (here >= m \| here + cnt >= m)`|Percepat evaluasi `enough` rata-rata|
|Pencegahan overflow|`(LL)t[0] * m`|Cast sebelum perkalian, bukan setelah|
|Kompleksitas total|$O(N \log(T_0 \cdot M))$ per test case|Layak untuk $N = 10^5$, $M = 10^9$|

#### 10.2.2 Greedy Langsung Tidak Optimal: Penjelasan Formal

Greedy work-conserving (selalu berikan task ke server yang paling cepat kosong) gagal karena ia hanya mengoptimalkan keputusan _lokal_ — meminimalkan waktu tunggu task saat ini — tanpa mempertimbangkan dampak _global_ terhadap makespan.

Secara formal, misalkan $t_{\text{free}}(i)$ adalah waktu server $i$ kembali kosong. Greedy memilih $\arg\min_i t_{\text{free}}(i)$ untuk setiap task. Namun ini tidak menjamin makespan minimum karena keputusan memberikan task ke server yang lebih lambat "sekarang" bisa memblokir server cepat dari menerima task di masa depan dalam urutan yang lebih menguntungkan.

Pada contoh kita, greedy memberikan Task 6 ke Server 1 ($t_{\text{free}} = 20$) padahal hanya menunggu 1 satuan untuk Server 0 ($t_{\text{free}} = 21$) menghasilkan penghematan 2 satuan pada makespan akhir.

#### 10.2.3 Mengapa `enough(time)` Benar secara Matematis

Fungsi `enough` mengklaim: jika $\sum_i \lfloor \tau / T_i \rfloor \geq M$, maka ada jadwal valid yang menyelesaikan $M$ task dalam waktu $\tau$. Ini tidak intuitif — bagaimana kita yakin $M$ task bisa di-schedule tanpa konflik hanya dari jumlah kapasitas?

Buktinya konstruktif: definisikan slot $(i, k)$ sebagai "task ke-$k$ pada server $i$, selesai pada waktu $k \cdot T_i \leq \tau$". Total slot yang tersedia adalah $\sum_i \lfloor \tau / T_i \rfloor \geq M$. Karena tidak ada dua slot berbagi server di waktu yang sama (slot $(i, k)$ dan $(i, k')$ dengan $k \neq k'$ memiliki waktu selesai berbeda), kita tinggal memetakan $M$ task ke $M$ slot berbeda — selalu mungkin karena jumlah slot $\geq M$.

---

## 11 Referensi

1. Cormen, T. H., Leiserson, C. E., Rivest, R. L., & Stein, C. (2009). _Introduction to Algorithms_ (3rd ed.). MIT Press. — Backtracking, Greedy, Dynamic Programming, CSP, dan analisis kompleksitas asimptotik.

2. Mackworth, A. K. (1977). Consistency in networks of relations. _Artificial Intelligence_, _8_(1), 99–118. — Fondasi Arc Consistency (AC3) dan propagasi constraint.

3. Golumbic, M. C. (2004). _Algorithmic Graph Theory and Perfect Graphs_ (2nd ed.). Elsevier. — Laminar family, planar matching, dan non-crossing matching pada circle graph.

4. West, D. B. (2001). _Introduction to Graph Theory_ (2nd ed.). Prentice Hall. — Jordan Curve Theorem dan planar matching pada grid.

5. Kumar, V. (1992). Algorithms for constraint-satisfaction problems: A survey. _AI Magazine_, _13_(1), 32–44. — Survei kerangka CSP dan posisi AC3 dalam hierarki propagasi constraint.

6. SPOJ Problem Archive. JC15E — Laser Beam 2.0. [https://www.spoj.com/](https://www.spoj.com/)