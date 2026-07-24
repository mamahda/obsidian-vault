Source: https://en.wikipedia.org/wiki/Greedy_algorithm

 **greedy algorithm** adalah _algorithm_ yang, pada setiap langkah, membuat pilihan yang bersifat _locally optimal_, dan selanjutnya tidak mempertimbangkan kembali pilihan-pilihan di masa lalu. _Greedy algorithms_ sering digunakan untuk menyelesaikan masalah _combinatorial optimization_. Jika sebuah _optimization problem_ hanya bergantung pada _partial solution_ dari penyelesaiannya untuk satu _subproblem_, kita dapat menyelesaikan masalah ini secara "greedily" dengan hanya mempertimbangkan _subproblem_ yang _locally optimal_. Dalam pengertian ini, _greedy algorithm_ adalah kasus khusus dari _dynamic programming algorithm_. Uriel Feige mencatat bahwa:

> [_Greedy algorithms_] dapat dipandang sebagai bentuk pamungkas dari _dynamic programming_, di mana hanya satu _partial solution_ yang dipertahankan. Masalahnya harus memiliki struktur yang jauh lebih banyak agar pendekatan ini dapat berhasil.

Dalam banyak kasus, _greedy algorithm_ tidak menghasilkan _exact solution_, tetapi dapat menghasilkan solusi yang meng-_approximate_ (mendekati) _exact solution_ dalam jumlah waktu yang wajar.

Contoh masalah yang menerima _exact greedy solution_ adalah _activity selection problem_. Diberikan sekumpulan tugas yang dapat diselesaikan di antara interval waktu yang dialokasikan, masalahnya adalah menentukan jumlah maksimum tugas yang dapat diselesaikan. Sebuah _greedy algorithm_ dalam $O(\log(n))$ yang menyelesaikan masalah ini mengurutkan tugas-tugas berdasarkan waktu selesai (_end time_) dan kemudian berulang kali memilih tugas pertama yang dimulai setelah tugas terakhir selesai.

Banyak algoritma klasik dalam ilmu komputer seperti _Huffman coding algorithm_, _Prim's algorithm_, _Kruskal's algorithm_, dan _Dijkstra's algorithm_ semuanya menggunakan _greedy properties_ dalam desainnya. Para matematikawan juga sering menggunakan _greedy strategies_ dalam pembuktian. Contoh klasik adalah apa yang disebut oleh Raphael Yuster sebagai _greedy proof_ bahwa setiap _tournament_ dalam graf mengandung _Hamiltonian path_.

## Characterizations

Karena tidak ada definisi formal tentang apa itu _greedy algorithm_, karakterisasi lengkap tentang kapan suatu masalah menerima _greedy algorithm_ sebagai solusi belum diketahui. Namun, kasus-kasus khusus telah diidentifikasi. Jack Edmonds menunjukkan bahwa _greedy algorithm_ dapat digunakan untuk menyelesaikan kelas masalah _linear combinatorial optimization_ dengan struktur _matroid_.

Kemudian Bernhard Korte dan László Lovász mengkarakterisasi kelas _optimization problems_ yang lebih luas dengan memperkenalkan gagasan _greedoid_. Hal ini memungkinkan, misalnya, pembuktian optimalitas dari _Prim's algorithm_.

Algoritma yang membatalkan (_undo_) langkah masa lalu bukanlah _greedy_. Sebagai contoh, _Gale-Shapley algorithm_ bukanlah _greedy algorithm_ karena meskipun algoritma ini membangun sebuah solusi dengan memilih pasangan terbaik saat ini, dalam prosesnya, solusi yang sudah ada dapat dimodifikasi.

## Correctness

Salah satu teknik yang digunakan untuk membuktikan optimalitas dari _greedy algorithms_ adalah _exchange argument_. _Exchange argument_ menunjukkan bahwa setiap solusi yang berbeda dari _greedy solution_ paling banter hanya sebaik _greedy solution_. Pola pembuktian ini biasanya mengikuti langkah-langkah berikut:

1. Asumsikan terdapat _optimal solution_ yang berbeda dari _greedy solution_.
    
2. Pertimbangkan titik pertama di mana _optimal solution_ dan _greedy solution_ berbeda.
    
3. Buktikan bahwa menukar pilihan optimal dengan pilihan _greedy_ pada titik ini tidak akan memperburuk _greedy solution_.
    
4. Simpulkan dengan induksi bahwa _greedy solution_ adalah optimal.
    

## Further examples

- Dalam _fractional knapsack problem_, seseorang diberikan daftar barang dengan berat (_weights_) dan nilai (_values_). Tujuannya adalah memilih jumlah pecahan dari setiap barang sedemikian rupa sehingga total nilainya maksimal, dan beratnya berada di bawah batasan yang ditetapkan. Berbeda dengan _knapsack problem_, yang diketahui bersifat _NP-hard_, _fractional knapsack problem_ menerima _greedy algorithm_ dalam waktu polinomial (_polynomial time_).
    
- Contoh-contoh dari _Frobenius coin problem_ menerima _greedy solutions_. Namun, dalam beberapa kasus _greedy algorithm_ tidak menghasilkan _optimal solution_.
    
- _Matching pursuit_ adalah contoh _greedy algorithm_ yang diterapkan pada _signal approximation_.
    
- Sebuah _greedy algorithm_ menemukan _optimal solution_ untuk _Malfatti's problem_, yaitu menemukan tiga lingkaran saling lepas (_disjoint circles_) di dalam sebuah segitiga yang memaksimalkan total luas lingkaran-lingkaran tersebut; diduga bahwa _greedy algorithm_ yang sama juga optimal untuk sejumlah lingkaran berapa pun.
    
- Dalam _decision tree learning_, _greedy algorithms_ umum digunakan, namun tidak dijamin menemukan _optimal solution_.
    
    - Salah satu algoritma populer semacam itu adalah _ID3 algorithm_ untuk konstruksi _decision tree_.
        
- Sebuah _greedy algorithm_ mengkonstruksi _Zeckendorf representation_ (atau _Fibonacci coding_) dari sebuah bilangan asli. Mengurangi bilangan Fibonacci terbesar yang kurang dari atau sama dengan bilangan asli tersebut secara berulang-ulang akan memberikan _Zeckendorf representation_-nya. _Greedy algorithm_ diekstraksi dari pembuktian keberadaan _Zeckendorf representation_. Keunikan dari _Zeckendorf representation_ menjamin bahwa tidak ada jumlah Fibonacci tidak berurutan lainnya yang dapat memberikan output yang berbeda.
    
- Fibonacci mendeskripsikan sebuah _greedy algorithm_ untuk menghitung _Egyptian fractions_.
    
- _Greedy algorithms_ muncul dalam _network routing_. Menggunakan _greedy routing_, sebuah pesan diteruskan ke simpul tetangga (_neighbouring node_) yang "terdekat" dengan tujuan. Gagasan tentang lokasi simpul (dan karenanya "kedekatan") dapat ditentukan oleh lokasi fisiknya, seperti dalam _geographic routing_ yang digunakan oleh _ad hoc networks_. Lokasi juga bisa merupakan konstruksi buatan sepenuhnya seperti dalam _small world routing_ dan _distributed hash table_.
    

## Greedy algorithms on graphs

Teori graf (_Graph theory_) adalah sumber yang kaya akan _greedy algorithms_. Ilmuwan komputer sering menggunakan _greedy algorithms_ untuk menghitung _graph invariants_.

- _Dijkstra's algorithm_ dan _A* search algorithm_ yang terkait adalah _greedy algorithms_ yang terverifikasi optimal untuk _graph search_ dan _shortest path finding_.
    
    - _A* search_ bersifat optimal bersyarat (_conditionally optimal_), membutuhkan "_admissible heuristic_" yang tidak akan melebih-lebihkan perkiraan biaya jalur (_path costs_).
        
- _Kruskal's algorithm_ dan _Prim's algorithm_ adalah _greedy algorithms_ untuk membangun _minimum spanning trees_ dari sebuah _connected graph_. Algoritma ini selalu menemukan _optimal solution_, yang mungkin tidak unik secara umum.
    
- Sebuah _greedy algorithm_ membangun _Huffman tree_ dalam _Huffman coding_.
    
- Algoritma _Sequitur_ dan _Lempel-Ziv-Welch_ adalah _greedy algorithms_ untuk _grammar induction_.
    
- Sebuah _greedy algorithm_ menemukan _maximum independent set_ dalam sebuah _tree_.
    

_Greedy algorithms_ juga digunakan untuk mencari batas atas (_upper bounds_) bagi _chromatic numbers_. Contoh sederhananya adalah batas $\chi(G) \leq \Delta(G) + 1$ yang diperoleh melalui _greedy algorithm_. Kita mulai dengan mengambil sebuah _vertex_ (simpul) yang belum diwarnai. Karena _vertex_ ini memiliki paling banyak $\Delta(G)$ tetangga, maksimal ada $\Delta(G)$ warna yang digunakan pada _vertices_ yang berdekatan, menyisakan satu warna bebas untuk _vertex_ yang sedang dipertimbangkan.

## Greedy approximation algorithms

Sebuah solusi untuk _travelling salesman problem_ yang bersifat _NP-complete_ dapat di-_approximate_ dengan memulai dari himpunan sisi (_edge set_) yang kosong dan kemudian menambahkan sisi termurah berikutnya yang merupakan _subgraph_ dari _complete tour_. _Greedy algorithm_ ini telah terbukti menghasilkan solusi paling banyak $\Theta (\log n)$ kali lebih panjang dari _optimal tour_.

Contoh lain adalah bahwa solusi untuk _0-1 knapsack problem_ dapat di-_approximate_ dengan menggunakan _greedy algorithm_ untuk _fractional knapsack problem_. _Greedy algorithm_ ini telah terbukti menghasilkan solusi bernilai setidaknya setengah dari _optimal solution_.

Solusi untuk _submodular maximization_ di-_approximate_ menggunakan _greedy algorithm_ yang menghasilkan solusi setidaknya setengah dari _optimal solution_.

Masalah-masalah di mana _greedy algorithms_ digunakan untuk menyediakan _approximation algorithms_ meliputi masalah _set cover_, _load balancing_, _Steiner tree_, dan _independent set_.