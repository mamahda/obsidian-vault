Source: https://en.wikipedia.org/wiki/Dijkstra's_algorithm

**Algoritma Dijkstra** adalah sebuah algoritma untuk menemukan jalur terpendek antara simpul-simpul (*nodes* atau *vertices*) dalam sebuah graf berbobot, yang dapat merepresentasikan, misalnya, jaringan jalan. Algoritma ini digagas oleh ilmuwan komputer Edsger W. Dijkstra pada tahun 1956 dan dipublikasikan tiga tahun kemudian.

Algoritma Dijkstra menemukan jalur terpendek dari suatu simpul sumber (awal) ke semua simpul lainnya. Algoritma ini juga dapat digunakan untuk menemukan jalur terpendek ke simpul tujuan tertentu dengan menghentikan algoritma setelah jalur terpendek ke simpul tersebut ditemukan. Sebagai contoh, jika simpul-simpul pada graf mewakili kota dan bobot sisinya (*edges*) mewakili jarak antara pasangan kota yang terhubung oleh jalan langsung, maka algoritma Dijkstra dapat digunakan untuk menemukan rute terpendek antara satu kota dengan semua kota lainnya. Aplikasi umum dari algoritma jalur terpendek adalah protokol perutean (*routing protocol*) jaringan, seperti IS-IS (*Intermediate System to Intermediate System*) dan OSPF (*Open Shortest Path First*). Algoritma ini juga digunakan sebagai subrutin dalam algoritma lain seperti algoritma Johnson.

Algoritma ini menggunakan struktur data antrean prioritas minimum (*min-priority queue*) untuk memilih jalur terpendek yang diketahui sejauh ini. Sebelum struktur antrean prioritas yang lebih maju ditemukan, algoritma asli Dijkstra berjalan dalam waktu $\Theta(\vert{}V\vert{}^2)$, di mana $\vert{}V\vert{}$ adalah jumlah simpul. Fredman dan Tarjan (1984) mengusulkan antrean prioritas menggunakan *Fibonacci heap* untuk mengoptimalkan kompleksitas waktu berjalannya menjadi $\Theta(\vert{}E\vert{} + \vert{}V\vert{} \log\vert{}V\vert{})$, di mana $\vert{}E\vert{}$ adalah jumlah sisi. Secara asimtotik, ini adalah algoritma jalur terpendek sumber-tunggal tercepat yang diketahui untuk graf berarah sembarang dengan bobot non-negatif tak terbatas. Namun, pada kasus-kasus khusus (seperti bobot bilangan bulat/terbatas, graf asiklik berarah, dll.), algoritma ini dapat lebih dioptimalkan. Jika prapemrosesan (*preprocessing*) diizinkan, algoritma seperti *contraction hierarchies* bisa lebih cepat hingga tujuh kali lipat.

Algoritma Dijkstra umumnya digunakan pada graf di mana bobot sisinya adalah bilangan bulat positif atau bilangan real. Algoritma ini dapat digeneralisasi untuk graf apa pun di mana bobot sisinya terurut sebagian (*partially ordered*), asalkan label-label berikutnya bersifat tidak menurun secara monotonik.

Dalam banyak bidang, khususnya kecerdasan buatan, algoritma Dijkstra atau variannya menawarkan pencarian biaya seragam (*uniform cost search*) dan diformulasikan sebagai bagian dari pencarian *best-first* yang lebih umum.

## Sejarah

Dijkstra memikirkan masalah jalur terpendek saat bekerja sebagai pemrogram di Mathematical Center di Amsterdam pada tahun 1956. Ia ingin mendemonstrasikan kemampuan komputer ARMAC yang baru. Tujuannya adalah memilih masalah dan solusi komputer yang dapat dipahami oleh orang awam. Ia merancang algoritma jalur terpendek dan kemudian mengimplementasikannya untuk ARMAC pada peta transportasi 64 kota di Belanda yang sedikit disederhanakan. Setahun kemudian, ia menemukan masalah lain dari para insinyur perangkat keras: meminimalkan jumlah kabel yang dibutuhkan untuk menghubungkan pin pada panel belakang mesin. Sebagai solusinya, ia menemukan kembali algoritma pohon rentang minimum (*minimum spanning tree*) Prim (yang sebelumnya telah ditemukan oleh Jarník dan Prim). Dijkstra memublikasikan algoritma ini pada tahun 1959.

## Algoritma

Algoritma ini membutuhkan simpul awal, dan menghitung jarak terpendek dari simpul awal tersebut ke setiap simpul lainnya. Algoritma Dijkstra dimulai dengan jarak tak terhingga dan mencoba memperbaikinya langkah demi langkah:

1. Buat himpunan semua simpul yang belum dikunjungi: disebut himpunan belum dikunjungi (*unvisited set*).
2. Tetapkan nilai jarak dari awal untuk setiap simpul: untuk simpul awal, nilainya nol, dan untuk semua simpul lainnya, nilainya tak terhingga ($\infty$), karena awalnya tidak ada jalur yang diketahui menuju simpul-simpul tersebut. Selama eksekusi, jarak sebuah simpul $N$ adalah panjang jalur terpendek yang ditemukan sejauh ini antara simpul awal dan $N$.
3. Dari himpunan belum dikunjungi, pilih simpul saat ini dengan jarak (berhingga) terkecil; pada awalnya, ini adalah simpul awal (berjarak nol). Jika himpunan belum dikunjungi kosong, atau hanya berisi simpul dengan jarak tak terhingga (yang berarti tidak dapat dicapai), maka algoritma berhenti dan melompat ke langkah 6. Jika kita hanya mencari jalur ke simpul tujuan tertentu, algoritma dapat dihentikan saat simpul saat ini adalah simpul tujuan. Jika tidak, algoritma berlanjut.
4. Untuk simpul saat ini, pertimbangkan semua tetangganya yang belum dikunjungi dan perbarui jarak mereka melalui simpul saat ini. Bandingkan jarak yang baru dihitung dengan jarak yang saat ini ditetapkan ke tetangga tersebut, lalu tetapkan nilai yang lebih kecil. Misalnya, jika simpul saat ini $A$ memiliki jarak 6, dan sisi yang menghubungkannya dengan tetangganya $B$ memiliki panjang 2, maka jarak ke $B$ melalui $A$ adalah 6 + 2 = 8. Jika sebelumnya $B$ ditandai dengan jarak lebih dari 8, perbarui menjadi 8. Jika tidak, pertahankan jarak saat ini.
5. Setelah mempertimbangkan semua tetangga yang belum dikunjungi dari simpul saat ini, simpul saat ini dihapus dari himpunan belum dikunjungi. Dengan demikian, simpul yang telah dikunjungi tidak akan pernah diperiksa kembali. Hal ini benar karena jarak yang tercatat pada simpul saat ini sudah minimal dan final. Ulangi dari langkah 3.
6. Setelah perulangan selesai, setiap simpul yang telah dikunjungi akan berisi jarak terpendeknya dari simpul awal.

## Deskripsi

Jalur terpendek antara dua persimpangan di peta kota dapat ditemukan menggunakan algoritma ini dengan pensil dan kertas. Setiap persimpangan (simpul) didaftar dalam baris terpisah: satu sebagai titik awal yang diberi jarak 0. Setiap persimpangan lainnya pada awalnya diberi jarak tak terhingga. Pada setiap iterasi, satu persimpangan menjadi persimpangan saat ini (awalnya adalah titik awal).

Dari persimpangan saat ini, jarak ke setiap persimpangan tetangga dinilai dengan menjumlahkan jarak persimpangan saat ini dengan jarak ke tetangga tersebut, lalu memperbarui label tetangga dengan nilai yang lebih kecil antara jumlah tersebut dan label tetangga yang sudah ada. Jika jalur melaluinya lebih pendek, tandai jalan ke tetangga tersebut dengan panah, dan hapus panah lain yang menunjuk ke sana. Setelah semua tetangga dinilai, persimpangan saat ini ditandai sebagai telah dikunjungi. Persimpangan belum dikunjungi dengan label terkecil kemudian menjadi persimpangan saat ini, dan proses ini berulang.

## Pseudokode

Dalam pseudokode berikut, `dist` adalah larik (*array*) yang berisi jarak saat ini dari `source` (sumber) ke simpul lainnya. Array `prev` berisi penunjuk ke simpul sebelumnya pada jalur terpendek dari sumber ke simpul yang diberikan.

```text
  1  function Dijkstra(Graph, source):
  2      
  3      for each vertex v in Graph.Vertices:
  4          dist[v] ← INFINITY
  5          prev[v] ← UNDEFINED
  6          tambahkan v ke Q
  7      dist[source] ← 0
  8      
  9      while Q tidak kosong:
 10          u ← simpul di Q dengan nilai dist[u] minimum
 11          Q.remove(u)
 12          
 13          for each edge (u, v) in Graph:
 14              alt ← dist[u] + Graph.Distance(u, v)
 15              if alt < dist[v]:
 16                  dist[v] ← alt
 17                  prev[v] ← u
 18
 19      return dist[], prev[]
````

Jika kita hanya ingin mencari jalur terpendek antara simpul `source` dan `target`, pencarian dapat dihentikan setelah baris 10 jika `u == target`. Jalur terpendek kemudian dapat direkonstruksi melalui iterasi mundur:

Plaintext

```
 1  S ← urutan kosong (empty sequence)
 2  u ← target
 3  if prev[u] terdefinisi or u = source: 
 4      while u terdefinisi:
 5          S.push(u)       // Masukkan simpul ke dalam tumpukan
 6          u ← prev[u]     // Bergerak mundur dari target ke source
```

### Menggunakan Antrean Prioritas

Untuk mempercepat waktu komputasi, struktur data antrean prioritas (_priority queue_) yang menyediakan operasi `add_with_priority()`, `decrease_priority()`, dan `extract_min()` bisa digunakan. _Fibonacci heap_ menawarkan implementasi optimal untuk ketiga operasi tersebut.

Plaintext

```
  1  function Dijkstra(Graph, source):
  2      Q ← Antrean untuk menyimpan prioritas simpul
  3      
  4      dist[source] ← 0 
  5      Q.add_with_priority(source, 0) 
  6
  7      for each vertex v in Graph.Vertices:
  8          if v ≠ source
  9              prev[v] ← UNDEFINED 
 10              dist[v] ← INFINITY 
 11              Q.add_with_priority(v, INFINITY)
 12
 13      while Q tidak kosong:
 14          u ← Q.extract_min() 
 15          for each edge (u, v):
 16              alt ← dist[u] + Graph.Distance(u, v)
 17              if alt < dist[v]:
 18                  prev[v] ← u
 19                  dist[v] ← alt
 20                  Q.decrease_priority(v, alt)
 21
 22      return (dist, prev)
```

## Pembuktian

Kebenaran algoritma Dijkstra dapat dibuktikan menggunakan induksi matematika pada jumlah simpul yang dikunjungi.

**Hipotesis invarian**: Untuk setiap simpul `v` yang dikunjungi, `dist[v]` adalah jarak terpendek dari `source` ke `v`. Untuk setiap simpul `u` yang belum dikunjungi, `dist[u]` adalah jarak terpendek dari `source` ke `u` melalui simpul-simpul yang telah dikunjungi saja, atau tak terhingga jika tidak ada jalur seperti itu.

**Kasus dasar**: Saat hanya ada satu simpul yang dikunjungi, yaitu `source`. Jaraknya didefinisikan nol, yang merupakan jarak terpendek karena bobot negatif tidak diizinkan.

**Induksi**: Asumsikan hipotesis berlaku untuk $k$ simpul yang dikunjungi. Untuk $k+1$ simpul, biarkan `u` menjadi simpul berikutnya yang dikunjungi (simpul dengan `dist[u]` minimum). Jika ada jalur yang lebih pendek menuju `u`, jalur tersebut pasti melewati simpul belum dikunjungi lainnya (katakanlah `w`). Namun, karena semua bobot sisi bernilai positif, jarak ke `w` pasti lebih kecil dari `u`, sehingga `w` seharusnya dipilih sebelum `u`. Ini menghasilkan kontradiksi, sehingga membuktikan bahwa `dist[u]` adalah jarak terpendek yang sebenarnya.

## Waktu Eksekusi

Batas kompleksitas waktu algoritma Dijkstra pada graf dengan sisi $E$ dan simpul $V$ sangat bergantung pada struktur data yang digunakan untuk merepresentasikan himpunan $Q$.

Waktu eksekusi dapat dinyatakan sebagai:

$$\Theta(\vert{}E\vert{} \cdot T_\mathrm{dk} + \vert{}V\vert{} \cdot T_\mathrm{em})$$

di mana $T_\mathrm{dk}$ dan $T_\mathrm{em}$ masing-masing adalah kompleksitas operasi _decrease-key_ dan _extract-minimum_ dalam $Q$.

- Menggunakan senarai berantai (_linked list_) atau larik (_array_): Waktu pencarian minimum linear, menghasilkan waktu total $\Theta(\vert{}V\vert{}^2)$.
    
- Menggunakan _binary heap_ atau pohon pencarian biner seimbang: Algoritma membutuhkan $\Theta((\vert{}E\vert{} + \vert{}V\vert{}) \log \vert{}V\vert{})$ waktu, atau $\Theta(\vert{}E\vert{} \log \vert{}V\vert{})$ pada graf yang terhubung.
    
- Menggunakan _Fibonacci heap_: Kompleksitasnya meningkat menjadi $\Theta(\vert{}E\vert{} + \vert{}V\vert{} \log\vert{}V\vert{})$.
    

### Optimasi Praktis dan Graf Tak Terhingga

Daripada memasukkan semua simpul ke dalam antrean di awal, algoritma dapat dimulai dengan antrean prioritas yang hanya berisi satu item (sumber), lalu menyisipkan item baru saat mereka ditemukan. Hal ini disebut **pencarian biaya seragam (UCS)** dalam literatur kecerdasan buatan, yang berguna untuk graf tak terhingga atau yang terlalu besar untuk disimpan dalam memori:

Plaintext

```
 procedure uniform_cost_search(start) is
     node ← start
     frontier ← antrean prioritas hanya berisi node
     expanded ← himpunan kosong
     do
         if frontier kosong then return gagal
         node ← frontier.pop()
         if node adalah tujuan then return solusi(node)
         expanded.add(node)
         for each tetangga n dari node do
             if n tidak ada di expanded dan frontier then
                 frontier.add(n)
             else if n ada di frontier dengan biaya lebih tinggi
                 ganti simpul yang ada dengan n
```

### Dijkstra Dua Arah (_Bidirectional Dijkstra_)

Varian ini dirancang untuk menghitung jalur terpendek antara simpul sumber $s$ dan tujuan $t$ secara efisien. Dua pencarian dilakukan serentak: satu maju dari $s$ pada graf asli, dan satu mundur dari $t$ pada graf dengan sisi yang dibalik.

Algoritma ini mempertahankan dua larik jarak, $d_f[v]$ dan $d_b[v]$, serta melacak variabel $\mu$ yang merepresentasikan panjang jalur $s-t$ terbaik yang ditemukan sejauh ini. $\mu$ diperbarui kapan pun koneksi antara dua himpunan ditemukan:

$$ \mu \leftarrow \min(\mu,; d_f[u] + w(u,x) + d_b[x]) $$

Pencarian berhenti saat jumlah dari prioritas minimum pada kedua antrean mencapai setidaknya $\mu$.

### Varian Khusus

Ketika bobot busur berupa bilangan bulat kecil (dibatasi oleh parameter $C$), antrean khusus seperti _bucket queue_ (Algoritma Dial) dapat memberikan kompleksitas $O(|E|+|V|C)$. Menggunakan pohon Van Emde Boas menghasilkan waktu $O(|E|+|V|\log C/\log\log |V|C)$.

## Masalah dan Algoritma Terkait

- **Algoritma Bellman-Ford** dapat digunakan pada graf dengan bobot sisi negatif, asalkan tidak ada siklus negatif.
    
- **Algoritma A*** adalah generalisasi dari Dijkstra yang mengurangi ukuran subgraf yang dieksplorasi dengan menggunakan heuristik (perkiraan batas bawah jarak ke target).
    
- **Algoritma Prim** digunakan untuk menemukan pohon rentang minimum (_minimum spanning tree_), beroperasi mirip Dijkstra tetapi hanya mengevaluasi bobot sisi individual tanpa mengakumulasi jarak dari titik awal.
    
- **Pencarian Melebar (BFS)** bisa dianggap sebagai kasus khusus algoritma Dijkstra pada graf tanpa bobot, di mana antrean prioritas merosot menjadi antrean FIFO biasa.
    

### Perspektif Pemrograman Dinamis

Dari sudut pandang pemrograman dinamis, algoritma Dijkstra adalah skema aproksimasi suksesif yang memecahkan persamaan fungsional untuk masalah jalur terpendek. Penjelasan logika di balik algoritma ini sebenarnya merupakan parafrase dari prinsip optimalitas Bellman.