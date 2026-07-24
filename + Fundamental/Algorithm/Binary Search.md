Source: https://en.wikipedia.org/wiki/Binary_search

Dalam _computer science_, **binary search**, juga dikenal sebagai _half-interval search_, _logarithmic search_, atau _binary chop_, adalah sebuah _search algorithm_ yang menemukan posisi sebuah nilai target di dalam sebuah _sorted array_. _Binary search_ membandingkan nilai target dengan elemen tengah dari _array_. Jika keduanya tidak sama, paruh di mana target tidak mungkin berada akan dieliminasi dan pencarian dilanjutkan pada paruh yang tersisa, mengambil elemen tengah lagi untuk dibandingkan dengan nilai target, dan mengulangi proses ini hingga nilai target ditemukan. Jika pencarian berakhir dengan paruh yang tersisa kosong, berarti target tidak ada di dalam _array_.

_Binary search_ berjalan dalam _logarithmic time_ pada _worst case_, melakukan $O(\log n)$ perbandingan, di mana $n$ adalah jumlah elemen dalam _array_. _Binary search_ lebih cepat daripada _linear search_ kecuali untuk _array_ berukuran kecil. Namun, _array_ harus diurutkan terlebih dahulu agar _binary search_ dapat diterapkan. Ada _data structures_ khusus yang dirancang untuk pencarian cepat, seperti _hash tables_, yang dapat dicari dengan lebih efisien daripada _binary search_. Meskipun demikian, _binary search_ dapat digunakan untuk memecahkan masalah yang lebih luas, seperti menemukan elemen terkecil berikutnya atau terbesar berikutnya dalam _array_ relatif terhadap target meskipun elemen tersebut tidak ada di dalam _array_.

Ada banyak variasi dari _binary search_. Secara khusus, _fractional cascading_ mempercepat _binary search_ untuk nilai yang sama di beberapa _array_. _Fractional cascading_ secara efisien memecahkan sejumlah masalah pencarian dalam _computational geometry_ dan berbagai bidang lainnya. _Exponential search_ memperluas _binary search_ untuk daftar yang tidak terbatas. _Data structures_ seperti _binary search tree_ dan _B-tree_ didasarkan pada _binary search_.

## Algoritma

_Binary search_ bekerja pada _sorted arrays_. _Binary search_ dimulai dengan membandingkan sebuah elemen di tengah _array_ dengan nilai target. Jika nilai target cocok dengan elemen tersebut, posisinya di dalam _array_ akan dikembalikan. Jika nilai target lebih kecil dari elemen tersebut, pencarian dilanjutkan di paruh bawah _array_. Jika nilai target lebih besar dari elemen tersebut, pencarian dilanjutkan di paruh atas _array_. Dengan melakukan ini, algoritma mengeliminasi paruh di mana nilai target tidak mungkin berada pada setiap iterasi.

### Prosedur

Diberikan sebuah _array_ $A$ yang berisi $n$ elemen dengan nilai atau _records_ $A_0, A_1, A_2, \ldots, A_{n-1}$ yang diurutkan sehingga $A_0 \leq A_1 \leq A_2 \leq \dots \leq A_{n-1}$, dan sebuah nilai target $T$, _subroutine_ berikut menggunakan _binary search_ untuk menemukan indeks dari $T$ di dalam $A$.

1. Tetapkan $L$ menjadi $0$ dan $R$ menjadi $n-1$.
    
2. Jika $L > R$, pencarian dihentikan karena tidak berhasil.
    
3. Tetapkan $m$ (posisi elemen tengah) menjadi $L$ ditambah _floor_ dari $\frac{R-L}{2}$, yang merupakan bilangan bulat terbesar yang lebih kecil dari atau sama dengan $\frac{R-L}{2}$.
    
4. Jika $A_m < T$, tetapkan $L$ menjadi $m+1$ dan kembali ke langkah 2.
    
5. Jika $A_m > T$, tetapkan $R$ menjadi $m-1$ dan kembali ke langkah 2.
    
6. Sekarang $A_m = T$, pencarian selesai; kembalikan $m$.
    

Prosedur iteratif ini melacak batas-batas pencarian menggunakan dua variabel $L$ dan $R$. Prosedur ini dapat diekspresikan dalam bentuk _pseudocode_ sebagai berikut, di mana nama dan tipe variabel tetap sama seperti di atas, `floor` adalah fungsi _floor_, dan `unsuccessful` mengacu pada nilai spesifik yang menandakan kegagalan pencarian.

Plaintext

```
function binary_search(A, n, T) is
     L := 0
     R := n - 1
     while L <= R do
         m := L + floor((R - L) / 2)
         if A[m] < T then
             L := m + 1
         else if A[m] > T then
             R := m - 1
         else:
             return m
     return unsuccessful
```

Secara alternatif, algoritma ini dapat mengambil nilai _ceiling_ dari $\frac{R-L}{2}$. Hal ini mungkin akan mengubah hasil jika nilai target muncul lebih dari satu kali di dalam _array_.

#### Prosedur Alternatif

Pada prosedur di atas, algoritma mengecek apakah elemen tengah ($m$) sama dengan target ($T$) pada setiap iterasi. Beberapa implementasi mengabaikan pengecekan ini pada setiap iterasi. Algoritma akan melakukan pengecekan ini hanya ketika tersisa satu elemen (ketika $L=R$). Ini menghasilkan _loop_ perbandingan yang lebih cepat, karena satu perbandingan dieliminasi per iterasi, sementara ia hanya membutuhkan satu iterasi tambahan secara rata-rata (Hermann Bottenbruch menerbitkan implementasi pertama yang mengabaikan pengecekan ini pada tahun 1962).

1. Tetapkan $L$ menjadi $0$ dan $R$ menjadi $n-1$.
    
2. Selama $L \neq R$,
    
    - Tetapkan $m$ (posisi elemen tengah) menjadi $L$ ditambah _ceiling_ dari $\frac{R-L}{2}$, yang merupakan bilangan bulat terkecil yang lebih besar dari atau sama dengan $\frac{R-L}{2}$.
        
    - Jika $A_m > T$, tetapkan $R$ menjadi $m-1$.
        
    - Jika tidak, $A_m \leq T$; tetapkan $L$ menjadi $m$.
        
3. Sekarang $L=R$, pencarian selesai. Jika $A_L=T$, kembalikan $L$. Jika tidak, pencarian dihentikan karena tidak berhasil.
    

Di mana `ceil` adalah fungsi _ceiling_, _pseudocode_ untuk versi ini adalah:

Plaintext

```
function binary_search_alternative(A, n, T) is
     L := 0
     R := n - 1
     while L != R do
         m := L + ceil((R - L) / 2)
         if A[m] > T then
             R := m - 1
         else:
             L := m
     if A[L] = T then
         return L
     return unsuccessful
```

### Elemen Duplikat

Prosedur dapat mengembalikan indeks mana pun yang elemennya sama dengan nilai target, meskipun ada elemen duplikat di dalam _array_. Misalnya, jika _array_ yang akan dicari adalah $[1,2,3,4,4,5,6,7]$ dan targetnya adalah $4$, maka algoritma akan benar jika mengembalikan elemen ke-4 (indeks 3) atau ke-5 (indeks 4). Kadang-kadang perlu untuk menemukan elemen paling kiri (_leftmost element_) atau elemen paling kanan (_rightmost element_) untuk nilai target yang diduplikasi dalam _array_.

#### Prosedur untuk menemukan elemen paling kiri (_leftmost element_)

Plaintext

```
function binary_search_leftmost(A, n, T):
     L := 0
     R := n
     while L < R:
         m := L + floor((R - L) / 2)
         if A[m] < T:
             L := m + 1
         else:
             R := m
     return L
```

#### Prosedur untuk menemukan elemen paling kanan (_rightmost element_)

Plaintext

```
function binary_search_rightmost(A, n, T):
     L := 0
     R := n
     while L < R:
         m := L + floor((R - L) / 2)
         if A[m] > T:
             R := m
         else:
             L := m + 1
     return R - 1
```

### Pencocokan Perkiraan (_Approximate matches_)

Prosedur di atas hanya melakukan pencocokan tepat (_exact matches_), yaitu menemukan posisi nilai target. Namun, sangat mudah untuk memperluas _binary search_ untuk melakukan pencocokan perkiraan karena _binary search_ beroperasi pada _sorted arrays_. Sebagai contoh, _binary search_ dapat digunakan untuk menghitung _rank_ (jumlah elemen yang lebih kecil), _predecessor_ (elemen terkecil berikutnya), _successor_ (elemen terbesar berikutnya), dan _nearest neighbor_ (tetangga terdekat). _Range queries_ (mencari jumlah elemen di antara dua nilai) juga dapat dilakukan dengan dua operasi pencarian _rank_.

## Performa

Dalam hal jumlah perbandingan, performa _binary search_ dapat dianalisis dengan melihat jalannya prosedur pada sebuah _binary tree_. _Root node_ dari _tree_ adalah elemen tengah dari _array_. Pada _worst case_, _binary search_ melakukan $\lfloor \log_2 (n) + 1 \rfloor$ iterasi dari _loop_ perbandingan. _Worst case_ juga dapat dicapai ketika elemen target tidak ada di dalam _array_.

Secara rata-rata (_average case_), dengan asumsi setiap elemen memiliki kemungkinan yang sama untuk dicari, _binary search_ membutuhkan sekitar $\log_2(n) - 1$ iterasi. Pada _best case_, di mana nilai target adalah elemen tengah dari _array_, posisinya dikembalikan setelah satu iterasi, yaitu $O(1)$.

### Kompleksitas Ruang (_Space complexity_)

_Binary search_ memerlukan tiga _pointers_ ke elemen, yang mungkin berupa indeks _array_ atau _pointers_ ke lokasi memori, terlepas dari ukuran _array_. Oleh karena itu, _space complexity_ dari _binary search_ adalah $O(1)$ dalam _model of computation_ berbasis _word RAM_.

### Pertimbangan Tambahan

- **Biaya Perbandingan (_Cost of comparison_):** Waktu yang diperlukan untuk membandingkan dua elemen meningkat secara linier dengan panjang _encoding_ (biasanya jumlah _bit_) dari elemen tersebut. Membandingkan nilai _floating-point_ seringkali lebih mahal daripada membandingkan _integers_ atau _strings_ pendek.
    
- **Prediksi Cabang (_Branch prediction_):** _Binary search_ menghasilkan sangat sedikit kegagalan prediksi cabang (_branch mispredictions_) karena sebagian besar logikanya dapat diekspresikan sebagai perpindahan kondisional (_conditional moves_) alih-alih percabangan biasa.
    
- **Penggunaan Cache (_Cache usage_):** Karena _binary search_ dapat melompat ke lokasi memori yang jauh (berbeda dengan urutan akses _locality of reference_ pada _linear search_), hal ini dapat memengaruhi memori _cache_ di CPU. Pada _array_ besar dengan ukuran pangkat dua, bisa terjadi _aliasing_ pada _Translation Lookaside Buffer_ (TLB), menyebabkan _TLB thrashing_. Hal ini dapat dicegah dengan menggeser titik bagi dari tengah eksak.
    

## Binary Search versus Skema Lainnya

### Linear Search

_Linear search_ adalah _search algorithm_ sederhana yang mengecek setiap _record_ sampai menemukan nilai target. _Binary search_ lebih cepat daripada _linear search_ untuk _sorted arrays_ kecuali jika _array_-nya sangat kecil. Namun, semua _sorting algorithms_ berbasis perbandingan seperti _quicksort_ dan _merge sort_ memerlukan setidaknya $O(n \log n)$ perbandingan sebelumnya.

### Trees

_Binary search tree_ adalah struktur data _binary tree_ yang bekerja berdasarkan prinsip _binary search_. Struktur ini menawarkan penyisipan (_insertion_) dan penghapusan (_deletion_) dalam waktu logaritmik rata-rata, lebih cepat daripada _array_. B-trees menggeneralisasi metode ini dan sering digunakan untuk sistem file (_filesystems_) dan basis data (_databases_).

### Hashing

Untuk mengimplementasikan _associative arrays_, _hash tables_ umumnya lebih cepat dari _binary search_ untuk _record_ yang tepat dengan waktu amortisasi konstan $O(1)$. Namun, _hashing_ tidak berguna untuk _approximate matches_ (seperti mencari _predecessor_ atau _successor_).

### Algoritma Keanggotaan Himpunan (_Set membership algorithms_)

Sebuah _bit array_ sangat cepat untuk keanggotaan dengan kunci terbatas dalam waktu $O(1)$. Untuk hasil perkiraan, _Bloom filters_ sangat efisien dalam hal ruang namun rentan terhadap positif palsu (_false positives_).

## Variasi

- **Uniform binary search:** Menyimpan selisih antara indeks tengah saat ini dan yang berikutnya di dalam sebuah _lookup table_, daripada menyimpan batas spesifik.
    
- **Exponential search:** Memperluas pencarian ke _array_ yang tidak terbatas dengan mencari batas atas yang merupakan pangkat dua terlebih dahulu, kemudian beralih ke _binary search_ standar.
    
- **Interpolation search:** Mengestimasi posisi target menggunakan interpolasi (seperti _linear interpolation_) alih-alih memotong tepat di tengah, mencapai komputasi rata-rata $O(\log \log n)$ pada distribusi yang seragam.
    
- **Fractional cascading:** Sebuah teknik untuk mempercepat pencarian elemen yang sama di beberapa _array_ yang diurutkan.
    
- **Generalisasi pada Graf (_Generalization to graphs_):** _Binary search_ diperluas untuk bekerja pada jenis graf tertentu, tempat nilai target disimpan di _vertex_ dan bukan di elemen _array_.
    
- **Noisy binary search:** Menangani kasus di mana algoritma perbandingan dapat mengembalikan hasil yang salah dengan probabilitas tertentu.
    
- **Quantum binary search:** _Quantum algorithms_ dapat menjalankan pencarian ini dengan kompleksitas waktu yang diturunkan pada komputer kuantum (_quantum computing_).
    

## Masalah Implementasi

Meskipun logika dasarnya terlihat sederhana, mengimplementasikan _binary search_ dapat memunculkan _edge cases_ yang merepotkan.

Salah satu bug terkenal adalah _integer overflow_ saat menghitung indeks tengah:

Menghitung `(L + R) / 2` dapat menyebabkan batas _integer_ terlampaui jika _array_ sangat besar. Praktik yang benar adalah menghitung _midpoint_ sebagai `L + (R - L) / 2`. Selain itu, _infinite loop_ dapat terjadi jika kondisi keluar (_exit conditions_) untuk perulangan tidak didefinisikan dengan tepat.

## Dukungan Library

Berbagai bahasa pemrograman memiliki rutinitas _binary search_ di _standard library_ mereka:

- **C:** Menyediakan fungsi `bsearch()`.
    
- **C++:** Menyediakan `binary_search()`, `lower_bound()`, `upper_bound()`, dan `equal_range()`.
    
- **Java:** Menyediakan metode statis _overloaded_ `binarySearch()` pada kelas `Arrays` dan `Collections`.
    
- **Python:** Menyediakan modul `bisect` untuk operasi logaritmik dan penyisipan data.
    
- **Go:** Menyediakan paket `sort` dengan implementasi `Search`, `SearchInts`, `SearchFloat64s`, dll.
    
- **Rust:** Tipe _slice_ primitif menyediakan `binary_search()`, `binary_search_by()`, dan fungsi terkait.
    
- Bahasa lain seperti **Ruby**, **C# / .NET**, **Objective-C / Cocoa**, dan **D** juga memiliki implementasi _built-in_ khusus untuk operasi _binary search_.