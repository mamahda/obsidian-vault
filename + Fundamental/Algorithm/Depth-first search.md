Source: https://en.wikipedia.org/wiki/Depth-first_search

Dalam ilmu komputer, **pencarian mendalam** atau ***depth-first search* (DFS)** adalah sebuah algoritma untuk menelusuri atau mencari pada struktur data pohon (*tree*) atau graf. Algoritma ini dimulai dari simpul akar (*root node*) (dengan memilih sembarang simpul sebagai akar dalam kasus graf) dan mengeksplorasi sejauh mungkin di sepanjang setiap cabang sebelum mundur (*backtracking*). Memori tambahan, yang biasanya berupa tumpukan (*stack*), diperlukan untuk melacak simpul-simpul yang telah ditemukan sejauh ini di sepanjang cabang tertentu guna membantu proses *backtracking* pada graf.

Sebuah versi pencarian mendalam diteliti pada abad ke-19 oleh matematikawan Prancis Charles Pierre Trémaux sebagai strategi untuk memecahkan labirin.

## Sifat-sifat
Analisis kompleksitas waktu dan ruang DFS berbeda tergantung pada area aplikasinya. Dalam ilmu komputer teoretis, DFS biasanya digunakan untuk menelusuri seluruh graf, dan membutuhkan waktu $O(\vert{}V\vert{} + \vert{}E\vert{})$, di mana $\vert{}V\vert{}$ adalah jumlah simpul (*vertices*) dan $\vert{}E\vert{}$ adalah jumlah sisi (*edges*). Hal ini berbanding lurus (linear) dengan ukuran graf. Dalam aplikasi ini, algoritma juga menggunakan ruang $O(\vert{}V\vert{})$ pada kasus terburuk untuk menyimpan tumpukan simpul di jalur pencarian saat ini serta himpunan simpul yang sudah dikunjungi. Dengan demikian, dalam pengaturan ini, batasan waktu dan ruangnya sama dengan algoritma pencarian melebar (*breadth-first search* atau BFS). Pilihan mengenai algoritma mana yang akan digunakan biasanya tidak terlalu bergantung pada kompleksitasnya, melainkan lebih pada perbedaan sifat pengurutan simpul yang dihasilkan oleh kedua algoritma tersebut.

Untuk aplikasi DFS pada domain tertentu, seperti mencari solusi dalam kecerdasan buatan (*artificial intelligence*) atau *web-crawling*, graf yang ditelusuri sering kali terlalu besar untuk dikunjungi seluruhnya atau berukuran tak terhingga (DFS dapat menderita masalah tidak pernah berhenti / *non-termination*). Dalam kasus seperti ini, pencarian hanya dilakukan hingga batas kedalaman tertentu (*depth-limited search*). Karena keterbatasan sumber daya seperti memori, seseorang biasanya tidak menggunakan struktur data untuk melacak himpunan semua simpul yang dikunjungi sebelumnya. Ketika pencarian dilakukan pada kedalaman terbatas, kompleksitas waktu tetap linier dalam hal jumlah simpul dan sisi yang diekspansi (meskipun jumlah ini tidak sama dengan ukuran seluruh graf karena beberapa simpul mungkin dicari lebih dari satu kali dan yang lain tidak sama sekali), tetapi kompleksitas ruang dari varian DFS ini hanya sebanding dengan batas kedalaman, sehingga jauh lebih kecil daripada memori yang dibutuhkan untuk mencari ke kedalaman yang sama menggunakan BFS. Untuk aplikasi semacam ini, DFS juga jauh lebih cocok digabungkan dengan metode heuristik untuk memilih cabang yang paling menjanjikan. Ketika batas kedalaman yang tepat tidak diketahui sejak awal, *iterative deepening depth-first search* menerapkan DFS berulang-ulang dengan urutan batas kedalaman yang terus meningkat.

DFS juga dapat digunakan untuk mengumpulkan sampel simpul graf. Namun, DFS yang tidak lengkap (*incomplete DFS*), mirip dengan BFS yang tidak lengkap, memiliki bias terhadap simpul yang memiliki derajat (*degree*) tinggi.

## Contoh
Misalkan sebuah pencarian mendalam dimulai pada simpul A. Jika diasumsikan bahwa sisi ke arah kiri pada graf dipilih lebih dulu sebelum sisi kanan, dan diasumsikan algoritma mengingat simpul-simpul yang dikunjungi sebelumnya dan tidak akan mengulanginya, DFS akan mengunjungi simpul-simpul dalam urutan berikut: A, B, D, F, E, C, G. Sisi-sisi yang dilalui dalam pencarian ini membentuk sebuah pohon Trémaux, yaitu suatu struktur yang memiliki aplikasi penting dalam teori graf.

Melakukan pencarian yang sama tanpa mengingat simpul yang telah dikunjungi sebelumnya akan menghasilkan kunjungan simpul dalam urutan: A, B, D, F, E, A, B, D, F, E, dan seterusnya selamanya. Algoritma akan terjebak dalam siklus A, B, D, F, E dan tidak pernah mencapai C atau G. Pendalaman iteratif (*iterative deepening*) adalah salah satu teknik untuk menghindari perulangan tak terhingga ini agar dapat menjangkau semua simpul.

## Output dari Pencarian Mendalam
Hasil dari pencarian mendalam pada sebuah graf dapat digambarkan dengan mudah dalam bentuk pohon rentangan (*spanning tree*) dari simpul-simpul yang dicapai selama pencarian. Berdasarkan pohon rentangan ini, sisi-sisi pada graf asli dapat dibagi menjadi tiga kelas: 
* **Sisi maju (*forward edges*)**, yang menunjuk dari suatu simpul di pohon ke salah satu keturunannya.
* **Sisi mundur (*back edges*)**, yang menunjuk dari suatu simpul ke salah satu leluhurnya.
* **Sisi silang (*cross edges*)**, yang tidak menunjuk ke keduanya. 

Terkadang **sisi pohon (*tree edges*)**, yaitu sisi-sisi yang termasuk dalam pohon rentangan itu sendiri, diklasifikasikan secara terpisah dari sisi maju. Jika graf asli adalah graf tak berarah, maka semua sisinya adalah sisi pohon atau sisi mundur.

### Urutan Simpul (*Vertex Orderings*)
Pencarian mendalam juga dapat digunakan untuk mengurutkan simpul-simpul suatu graf atau pohon secara linier. Ada empat cara untuk melakukan ini:

* ***Preordering* (Urutan Awal)** adalah daftar simpul dalam urutan *pertama kali* mereka dikunjungi oleh algoritma DFS. Ini adalah cara yang ringkas dan alami untuk menggambarkan proses pencarian. *Preordering* dari sebuah pohon ekspresi adalah ekspresi dalam notasi Polandia.
* ***Postordering* (Urutan Akhir)** adalah daftar simpul dalam urutan *terakhir kali* mereka dikunjungi oleh algoritma. *Postordering* dari pohon ekspresi adalah ekspresi dalam notasi Polandia terbalik.
* ***Reverse preordering*** adalah kebalikan dari *preordering*, yaitu daftar simpul dalam urutan kebalikan dari kunjungan pertama mereka. *Reverse preordering* tidak sama dengan *postordering*.
* ***Reverse postordering*** adalah kebalikan dari *postordering*, yaitu daftar simpul dalam urutan kebalikan dari kunjungan terakhir mereka. *Reverse postordering* tidak sama dengan *preordering*.

Untuk pohon biner, terdapat tambahan *in-ordering* dan *reverse in-ordering*.

*Reverse postordering* menghasilkan pengurutan topologis (*topological sorting*) dari graf asiklik berarah (*directed acyclic graph*). Pengurutan ini juga berguna dalam analisis aliran kontrol (*control-flow analysis*) karena sering kali merepresentasikan linierisasi alami dari aliran kontrol dalam kode program.

## Pseudokode

Berikut adalah implementasi rekursif dari DFS:

```text
procedure DFS(G, v) is
    tandai v sebagai telah ditemukan (discovered)
    for all sisi berarah dari v ke w in G.adjacentEdges(v) do
        if simpul w belum ditandai sebagai telah ditemukan then
            panggil secara rekursif DFS(G, w)

```

Implementasi DFS secara non-rekursif (iteratif) dengan kompleksitas ruang kasus terburuk $O(\vert{}E\vert{})$, yang memungkinkan adanya simpul duplikat di dalam tumpukan:

```text
procedure DFS_iterative(G, v) is
    jadikan S sebagai tumpukan (stack)
    S.push(v)
    while S tidak kosong do
        v = S.pop()
        if v belum ditandai sebagai telah ditemukan then
            tandai v sebagai telah ditemukan
            for all sisi dari v ke w in G.adjacentEdges(v) do 
                S.push(w)

```

Kedua variasi DFS di atas mengunjungi tetangga dari masing-masing simpul dengan urutan yang saling berlawanan. Tetangga pertama dari $v$ yang dikunjungi oleh variasi rekursif adalah tetangga pertama di dalam senarai ketetanggaan, sedangkan pada variasi iteratif, tetangga yang pertama dikunjungi adalah tetangga terakhir dalam senarai ketetanggaan.

Implementasi non-rekursif ini mirip dengan pencarian melebar (BFS) namun berbeda dalam dua hal:

1. Menggunakan tumpukan (*stack*) alih-alih antrean (*queue*).
2. Algoritma menunda pengecekan apakah suatu simpul telah ditemukan hingga simpul tersebut dikeluarkan (*popped*) dari tumpukan, bukan melakukan pengecekan sebelum menambahkan simpul ke dalamnya.

Implementasi pencarian mendalam iteratif lainnya bisa dilakukan menggunakan tumpukan iterator dari senarai tetangga simpul, alih-alih menggunakan tumpukan simpul itu sendiri. Ini menghasilkan penelusuran yang persis sama dengan DFS rekursif:

```text
procedure DFS_iterative(G, v) is
    jadikan S sebagai tumpukan
    tandai v sebagai telah ditemukan
    S.push(iterator dari G.adjacentEdges(v))
    while S tidak kosong do
        if S.peek().hasNext() then
            w = S.peek().next()
            if w belum ditandai sebagai telah ditemukan then
                tandai w sebagai telah ditemukan
                S.push(iterator dari G.adjacentEdges(w))
        else
            S.pop()

```

## Aplikasi

Beberapa algoritma yang menggunakan pencarian mendalam sebagai fondasi dasarnya meliputi:

* Menemukan komponen terhubung (*connected components*).
* Pengurutan topologis (*Topological sorting*).
* Menemukan komponen terhubung 2-sisi atau 2-simpul (*biconnected components*).
* Menemukan komponen terhubung kuat (*strongly connected components*).
* Menemukan jembatan (*bridges*) di dalam suatu graf.
* Uji planaritas (*Planarity testing*).
* Menyelesaikan teka-teki dengan hanya satu solusi, seperti labirin (DFS dapat diadaptasi untuk mencari semua solusi dari labirin dengan hanya menyertakan simpul pada jalur pencarian saat ini ke dalam himpunan yang telah dikunjungi).
* Pembuatan labirin (*Maze generation*) dapat menggunakan variasi DFS acak.

## Kompleksitas

Kompleksitas komputasional dari DFS diteliti oleh John Reif. Lebih tepatnya, jika diberikan graf $G$, misalkan $O = (v_1, \dots, v_n)$ adalah urutan yang dihitung oleh algoritma DFS rekursif standar. Urutan ini disebut urutan *lexicographic depth-first search*. John Reif mempertimbangkan kompleksitas komputasi untuk menghasilkan urutan tersebut jika diberikan sebuah graf dan simpul sumber. Versi masalah keputusan dari pencarian ini (yaitu menguji apakah sebuah simpul $u$ muncul sebelum simpul $v$ dalam urutan tersebut) merupakan permasalahan **P-complete**, yang berarti masalah ini sangat sulit (bahkan menjadi semacam mimpi buruk) untuk diselesaikan melalui pemrosesan paralel.

Urutan pencarian mendalam (tidak harus urutan secara leksikografis) dapat dihitung dengan algoritma paralel acak yang tergolong dalam kelas kompleksitas RNC. Namun, hingga tahun 1997, masih belum diketahui apakah penelusuran *depth-first* dapat dikonstruksi secara deterministik oleh algoritma paralel di dalam kelas kompleksitas NC.

```

```