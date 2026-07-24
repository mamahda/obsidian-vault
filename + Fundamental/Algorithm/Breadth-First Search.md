Source: https://en.wikipedia.org/wiki/Depth-first_search

Dalam ilmu komputer, **pencarian melebar** atau ***breadth-first search* (BFS)** adalah sebuah algoritma untuk menelusuri struktur data pohon guna menemukan simpul (*node*) yang memenuhi kriteria tertentu. Algoritma ini dimulai dari akar pohon dan mengeksplorasi semua simpul pada tingkat kedalaman saat ini sebelum berlanjut ke simpul-simpul di tingkat kedalaman berikutnya. Memori tambahan, yang biasanya berupa antrean (*queue*), diperlukan untuk melacak simpul-simpul anak yang telah ditemukan tetapi belum dieksplorasi.

Sebagai contoh, dalam babak akhir permainan catur, sebuah mesin catur dapat membangun pohon permainan dari posisi saat ini dengan menerapkan semua kemungkinan langkah, lalu menggunakan pencarian melebar untuk menemukan posisi kemenangan bagi Putih. Pohon implisit (seperti pohon permainan atau pohon pemecahan masalah lainnya) bisa berukuran tak terhingga; pencarian melebar dijamin akan menemukan simpul solusi jika memang ada.

Sebaliknya, pencarian mendalam atau *depth-first search* (DFS) biasa, yang mengeksplorasi cabang simpul sejauh mungkin sebelum mundur (*backtracking*) dan memperluas simpul lain, bisa tersesat di cabang yang tak terhingga dan tidak pernah mencapai simpul solusi. *Iterative deepening depth-first search* menghindari kelemahan ini, dengan konsekuensi harus mengeksplorasi bagian atas pohon berulang-ulang. Di sisi lain, kedua algoritma *depth-first* tersebut biasanya membutuhkan memori tambahan yang jauh lebih sedikit dibandingkan pencarian melebar.

Pencarian melebar dapat digeneralisasi untuk graf tak berarah maupun graf berarah dengan simpul awal tertentu (kadang disebut sebagai 'kunci pencarian'). Dalam pencarian ruang keadaan pada kecerdasan buatan, pencarian berulang pada simpul sering kali diizinkan, sementara dalam analisis teoretis algoritma yang berbasis pencarian melebar, langkah pencegahan biasanya dilakukan untuk menghindari pengulangan.

BFS dan aplikasinya dalam menemukan komponen terhubung (*connected components*) dari graf diciptakan pada tahun 1945 oleh Konrad Zuse, dalam tesis Ph.D.-nya (yang ditolak) tentang bahasa pemrograman Plankalkül, tetapi ini tidak diterbitkan hingga tahun 1972. Algoritma ini ditemukan kembali pada tahun 1959 oleh Edward F. Moore, yang menggunakannya untuk menemukan jalur terpendek keluar dari labirin, dan kemudian dikembangkan oleh C. Y. Lee menjadi algoritma perutean kabel (diterbitkan pada tahun 1961).

## Pseudokode
Pseudokode di bawah ini menemukan jalur terpendek dari sebuah simpul $root$ (akar) ke semua simpul lainnya di dalam graf menggunakan BFS.

**Input**: Sebuah graf $G$ dan simpul awal $root$ dari $G$.
**Output**: Keadaan tujuan (*Goal state*). Tautan *parent* (induk) melacak jalur terpendek kembali ke $root$.

```text
  1  procedure BFS(G, root) is
  2      jadikan Q sebagai sebuah antrean (queue)
  3      tandai root sebagai telah dieksplorasi
  4      Q.enqueue(root)
  5      while Q tidak kosong do
  6          v := Q.dequeue()
  7          if v adalah tujuan then
  8              return v
  9          for all edge (sisi) dari v ke w in G.adjacentEdges(v) do
 10              if w belum ditandai sebagai telah dieksplorasi then
 11                  tandai w sebagai telah dieksplorasi
 12                  w.parent := v
 13                  Q.enqueue(w)
````

### Detail Lebih Lanjut

Implementasi non-rekursif ini mirip dengan implementasi non-rekursif dari _depth-first search_ (DFS), tetapi berbeda dalam dua hal:

1. Menggunakan antrean (_queue_) dengan prinsip _First In First Out_ (FIFO) alih-alih tumpukan (_stack_) dengan prinsip _Last In First Out_ (LIFO).
    
2. Algoritma ini memeriksa apakah suatu simpul telah dieksplorasi _sebelum_ memasukkannya ke dalam antrean, bukan menunda pemeriksaan tersebut sampai simpul dikeluarkan dari antrean.
    

Jika $G$ adalah sebuah pohon, mengganti antrean dari algoritma pencarian melebar ini dengan tumpukan (_stack_) akan menghasilkan algoritma pencarian mendalam (DFS). Untuk graf umum, mengganti tumpukan pada implementasi DFS iteratif dengan sebuah antrean juga akan menghasilkan algoritma pencarian melebar, meskipun dalam bentuk yang sedikit tidak standar.

Antrean $Q$ berisi batasan (_frontier_) di mana algoritma sedang melakukan pencarian saat ini. Simpul dapat ditandai sebagai telah dieksplorasi dengan menyimpannya dalam sebuah himpunan (_set_), atau melalui atribut pada setiap simpul, tergantung pada implementasinya.

Atribut _parent_ (induk) pada setiap simpul berguna untuk mengakses simpul-simpul dalam jalur terpendek, misalnya dengan merunut mundur dari simpul tujuan hingga ke simpul awal, setelah BFS selesai dijalankan dan simpul pendahulu telah ditetapkan. Hasil dari pencarian ini adalah sebuah _breadth-first tree_ (pohon pencarian melebar).

## Analisis

### Kompleksitas Waktu dan Ruang

Kompleksitas waktu dapat diekspresikan sebagai $O(|V| + |E|)$, karena setiap simpul dan setiap sisi akan dieksplorasi dalam kasus terburuk. $|V|$ adalah jumlah simpul dan $|E|$ adalah jumlah sisi dalam graf. Perlu dicatat bahwa $O(|E|)$ dapat bervariasi antara $O(1)$ dan $O(|V|^2)$, tergantung pada seberapa jarang (_sparse_) graf masukannya.

Ketika jumlah simpul dalam graf diketahui sebelumnya, dan struktur data tambahan digunakan untuk menentukan simpul mana yang telah ditambahkan ke antrean, kompleksitas ruang dapat diekspresikan sebagai $O(|V|)$. Hal ini merupakan tambahan dari ruang yang dibutuhkan untuk menyimpan graf itu sendiri, yang dapat bervariasi tergantung pada representasi graf yang digunakan oleh implementasi algoritma.

Ketika bekerja dengan graf yang terlalu besar untuk disimpan secara eksplisit (atau graf tak terhingga), lebih praktis untuk mendeskripsikan kompleksitas pencarian melebar dalam istilah yang berbeda: untuk menemukan simpul yang berada pada jarak $d$ dari simpul awal (diukur dalam jumlah traversal sisi), BFS membutuhkan waktu dan memori sebesar $O(b^{d + 1})$, di mana $b$ adalah "faktor percabangan" (_branching factor_) dari graf tersebut (rata-rata derajat keluar).

### Kelengkapan (Completeness)

Dalam analisis algoritma, input untuk pencarian melebar diasumsikan sebagai graf berhingga, yang direpresentasikan sebagai senarai ketetanggaan (_adjacency list_), matriks ketetanggaan, atau representasi serupa. Namun, dalam aplikasi metode traversal graf pada kecerdasan buatan, inputnya mungkin merupakan representasi implisit dari graf tak terhingga. Dalam konteks ini, suatu metode pencarian disebut lengkap (_complete_) jika dijamin akan menemukan keadaan tujuan jika memang ada. Pencarian melebar bersifat lengkap, tetapi pencarian mendalam tidak. Ketika diterapkan pada graf tak terhingga yang direpresentasikan secara implisit, pencarian melebar pada akhirnya akan menemukan keadaan tujuan, tetapi pencarian mendalam bisa tersesat di bagian graf yang tidak memiliki tujuan dan tidak pernah kembali.

## Urutan BFS

Sebuah enumerasi dari simpul-simpul pada suatu graf dikatakan sebagai urutan BFS jika enumerasi tersebut adalah output yang mungkin dari penerapan BFS pada graf ini.

Misalkan $G=(V,E)$ adalah sebuah graf dengan $n$ simpul. Ingat bahwa $N(v)$ adalah himpunan tetangga dari $v$. Misalkan $\sigma=(v_1,\dots,v_m)$ adalah sebuah daftar dari elemen-elemen berbeda pada $V$, dan untuk $v\in V\setminus\{v_1,\dots,v_m\}$, misalkan $\nu_{\sigma}(v)$ adalah indeks $i$ terkecil sedemikian rupa sehingga $v_i$ adalah tetangga dari $v$, jika $i$ tersebut ada, dan bernilai $\infty$ jika sebaliknya.

Misalkan $\sigma=(v_1,\dots,v_n)$ adalah enumerasi dari simpul-simpul $V$. Enumerasi $\sigma$ dikatakan sebagai urutan BFS (dengan sumber $v_1$) jika, untuk semua $1 < i \le n$, $v_i$ adalah simpul $w \in V\setminus\{v_1,\dots,v_{i-1}\}$ sedemikian rupa sehingga $\nu_{(v_1,\dots,v_{i-1})}(w)$ bernilai minimal. Secara ekuivalen, $\sigma$ adalah urutan BFS jika, untuk semua $1 \le i < j < k \le n$ dengan $v_i \in N(v_k)\setminus N(v_j)$, terdapat sebuah tetangga $v_m$ dari $v_j$ sedemikian rupa sehingga $m < i$.

## Aplikasi

Pencarian melebar dapat digunakan untuk memecahkan banyak masalah dalam teori graf, sebagai contoh:

- Pengumpulan sampah (_garbage collection_) penyalinan, Algoritma Cheney.
    
- Menemukan jalur terpendek antara dua simpul $u$ dan $v$, dengan panjang jalur yang diukur dari jumlah sisi (merupakan keunggulan dibandingkan pencarian mendalam).
    
- Penomoran jaring Cuthill–McKee (dan kebalikannya).
    
- Metode Ford–Fulkerson untuk menghitung aliran maksimum (_maximum flow_) dalam suatu jaringan aliran.
    
- Serialisasi/Deserialisasi pohon biner berbanding terbalik dengan serialisasi dalam urutan yang disortir, memungkinkan pohon untuk dikonstruksi kembali dengan efisien.
    
- Konstruksi _failure function_ dari pencocok pola Aho-Corasick.
    
- Menguji bipartisi sebuah graf.
    
- Implementasi algoritma paralel untuk menghitung penutupan transitif (_transitive closure_) suatu graf.