Source: https://en.wikipedia.org/wiki/Constraint_satisfaction_problem

**Constraint satisfaction problems** (**CSPs**) adalah pertanyaan matematis yang didefinisikan sebagai sekumpulan objek yang keadaannya (_state_) harus memenuhi sejumlah _constraint_ atau _limitation_. CSPs merepresentasikan entitas dalam sebuah masalah sebagai kumpulan homogen dari _finite constraints_ atas variabel-variabel, yang diselesaikan dengan metode _constraint satisfaction_. CSPs menjadi subjek penelitian baik dalam _artificial intelligence_ maupun _operations research_, karena keteraturan dalam formulasinya memberikan dasar umum untuk menganalisis dan menyelesaikan masalah dari banyak rumpun yang tampaknya tidak berkaitan. CSPs sering kali menunjukkan kompleksitas yang tinggi, sehingga membutuhkan kombinasi _heuristics_ dan metode _combinatorial search_ agar dapat diselesaikan dalam waktu yang wajar. _Constraint programming_ (CP) adalah bidang penelitian yang secara khusus berfokus pada penyelesaian masalah semacam ini. Selain itu, _Boolean satisfiability problem_ (SAT), _satisfiability modulo theories_ (SMT), _mixed integer programming_ (MIP), dan _answer set programming_ (ASP) adalah bidang penelitian yang berfokus pada penyelesaian bentuk-bentuk khusus dari _constraint satisfaction problem_.

Contoh masalah yang dapat dimodelkan sebagai _constraint satisfaction problem_ meliputi:

- _Type inference_
    
- _Eight queens puzzle_
    
- _Map coloring problem_
    
- _Maximum cut problem_
    
- Sudoku, _crosswords_, futoshiki, Kakuro (Cross Sums), Numbrix/Hidato, Zebra Puzzle, dan banyak _logic puzzles_ lainnya
    

Berbagai masalah ini sering kali disertakan dalam tutorial _solvers_ CP, ASP, Boolean SAT, dan SMT. Secara umum, _constraint problems_ bisa jadi jauh lebih sulit, dan mungkin tidak dapat diekspresikan dalam beberapa sistem yang lebih sederhana tersebut. Contoh kehidupan nyata meliputi _automated planning_, _lexical disambiguation_, _musicology_, _product configuration_, dan _resource allocation_.

Keberadaan solusi untuk sebuah CSP dapat dipandang sebagai _decision problem_. Hal ini dapat diputuskan dengan menemukan sebuah solusi, atau gagal menemukan solusi setelah _exhaustive search_ (_stochastic algorithms_ biasanya tidak pernah mencapai kesimpulan yang mendalam, sedangkan _directed searches_ sering kali bisa melakukannya pada masalah yang cukup kecil). Dalam beberapa kasus, CSP mungkin telah diketahui memiliki solusi sebelumnya melalui beberapa proses _mathematical inference_ lainnya.

## Definisi formal

Secara formal, _constraint satisfaction problem_ didefinisikan sebagai sebuah _triple_:

$$\langle X,D,C \rangle$$

di mana:

- $X = \{X_1, \ldots,X_n\}$ adalah himpunan variabel,
    
- $D = \{D_1, \ldots, D_n\}$ adalah himpunan dari masing-masing _domains of values_ variabel tersebut, dan
    
- $C = \{C_1, \ldots, C_m\}$ adalah himpunan _constraints_.
    

Setiap variabel $X_i$ dapat mengambil nilai dalam _domain_ yang tidak kosong $D_i$.

Setiap _constraint_ $C_j \in C$ pada gilirannya adalah pasangan $\langle t_j,R_j \rangle$, di mana $t_j \subseteq \{1, 2, \ldots, n\}$ adalah himpunan dari $k$ indeks dan $R_j$ adalah _$k$-ary relation_ pada perkalian _domain_ yang sesuai $\times_{i \in t_j} D_i$ di mana perkalian diambil dengan indeks dalam urutan menaik. Sebuah _evaluation_ variabel adalah fungsi dari subset variabel ke sekumpulan nilai tertentu dalam subset _domain_ yang sesuai. Sebuah _evaluation_ $v$ memenuhi _constraint_ $\langle t_j, R_j \rangle$ jika nilai yang diberikan ke variabel $t_j$ memenuhi relasi $R_j$.

Sebuah _evaluation_ disebut _consistent_ jika tidak melanggar satupun _constraint_. Sebuah _evaluation_ disebut _complete_ jika mencakup semua variabel. Sebuah _evaluation_ adalah _solution_ jika ia _consistent_ dan _complete_; _evaluation_ semacam itu dikatakan _solve_ (menyelesaikan) _constraint satisfaction problem_.

## Solusi

_Constraint satisfaction problems_ pada _finite domains_ biasanya diselesaikan menggunakan bentuk _search_. Teknik yang paling banyak digunakan adalah varian dari _backtracking_, _constraint propagation_, dan _local search_. Teknik-teknik ini juga sering digabungkan, seperti pada metode VLNS, dan penelitian saat ini melibatkan teknologi lain seperti _linear programming_.

_Backtracking_ adalah algoritma rekursif. Algoritma ini mempertahankan _partial assignment_ dari variabel-variabel. Awalnya, semua variabel belum ditugaskan (_unassigned_). Pada setiap langkah, sebuah variabel dipilih, dan semua kemungkinan nilai ditugaskan kepadanya secara bergantian. Untuk setiap nilai, konsistensi _partial assignment_ terhadap _constraints_ akan diperiksa; jika konsisten, _recursive call_ dilakukan. Ketika semua nilai telah dicoba, algoritma akan melakukan _backtrack_. Dalam algoritma _backtracking_ dasar ini, konsistensi didefinisikan sebagai terpenuhinya semua _constraints_ yang variabelnya telah ditugaskan semua. Terdapat beberapa varian _backtracking_. _Backmarking_ meningkatkan efisiensi pemeriksaan konsistensi. _Backjumping_ memungkinkan penyimpanan sebagian pencarian dengan mundur lebih dari satu variabel dalam beberapa kasus. _Constraint learning_ menyimpulkan dan menyimpan _constraints_ baru yang nantinya dapat digunakan untuk menghindari bagian dari pencarian. _Look-ahead_ juga sering digunakan dalam _backtracking_ untuk mencoba meramalkan efek dari pemilihan variabel atau nilai, sehingga terkadang dapat menentukan lebih awal kapan suatu submasalah bersifat _satisfiable_ atau _unsatisfiable_.

Teknik _constraint propagation_ adalah metode yang digunakan untuk memodifikasi _constraint satisfaction problem_. Lebih tepatnya, ini adalah metode yang menegakkan bentuk _local consistency_, yaitu kondisi yang terkait dengan konsistensi sekelompok variabel atau _constraints_. _Constraint propagation_ memiliki berbagai kegunaan. Pertama, mengubah sebuah masalah menjadi masalah yang ekuivalen namun biasanya lebih mudah untuk diselesaikan. Kedua, metode ini dapat membuktikan _satisfiability_ atau _unsatisfiability_ dari suatu masalah. Hal ini tidak dijamin selalu terjadi secara umum; namun, hal ini selalu terjadi untuk beberapa bentuk _constraint propagation_ dan untuk jenis masalah tertentu. Bentuk _local consistency_ yang paling dikenal dan digunakan adalah _arc consistency_, _hyper-arc consistency_, dan _path consistency_. Metode _constraint propagation_ yang paling populer adalah algoritma AC-3, yang menegakkan _arc consistency_.

Metode _local search_ adalah algoritma _incomplete satisfiability_. Metode ini mungkin menemukan solusi dari sebuah masalah, tetapi bisa juga gagal meskipun masalah tersebut bersifat _satisfiable_. Cara kerjanya adalah dengan memperbaiki _complete assignment_ atas variabel-variabel secara berulang. Pada setiap langkah, sejumlah kecil variabel diubah nilainya, dengan tujuan keseluruhan untuk meningkatkan jumlah _constraints_ yang dipenuhi oleh _assignment_ ini. Algoritma _min-conflicts_ adalah algoritma _local search_ khusus untuk CSPs dan didasarkan pada prinsip tersebut. Pada praktiknya, _local search_ tampak bekerja dengan baik ketika perubahan ini juga dipengaruhi oleh pilihan acak. Integrasi antara _search_ dengan _local search_ telah dikembangkan, yang mengarah pada _hybrid algorithms_.

## Aspek teoretis

### Kompleksitas komputasi

CSPs juga dipelajari dalam _computational complexity theory_, _finite model theory_, dan _universal algebra_. Ternyata pertanyaan mengenai kompleksitas CSPs dapat diterjemahkan menjadi pertanyaan _universal-algebraic_ yang penting mengenai aljabar yang mendasarinya. Pendekatan ini dikenal sebagai _algebraic approach_ untuk CSPs.

Karena setiap _computational decision problem_ ekuivalen secara _polynomial-time_ dengan CSP bertemplat tak hingga, _general CSPs_ dapat memiliki kompleksitas arbitrer. Secara khusus, terdapat juga CSPs dalam kelas masalah _NP-intermediate_, yang keberadaannya ditunjukkan oleh Ladner, di bawah asumsi bahwa P != NP.

Namun, kelas besar CSPs yang muncul dari aplikasi alami memenuhi _complexity dichotomy_, yang berarti bahwa setiap CSP di dalam kelas tersebut berada di P atau NP-complete. Oleh karena itu, CSPs ini menyediakan salah satu subset terbesar yang diketahui dari NP yang menghindari masalah _NP-intermediate_. _Complexity dichotomy_ pertama kali dibuktikan oleh Schaefer untuk _Boolean CSPs_, yaitu CSPs dengan _2-element domain_ dan semua relasi yang tersedia adalah _Boolean operators_. Hasil ini telah digeneralisasi untuk berbagai kelas CSPs, terutama untuk semua CSPs atas _finite domains_. _Finite-domain dichotomy conjecture_ ini pertama kali dirumuskan oleh Tomás Feder dan Moshe Vardi, dan akhirnya dibuktikan secara independen oleh Andrei Bulatov dan Dmitriy Zhuk pada tahun 2017.

Kelas lain di mana _complexity dichotomy_ telah dikonfirmasi adalah:

- semua _first-order reducts_ dari $(\mathbb{Q},<)$,
    
- semua _first-order reducts_ dari _countable random graph_,
    
- semua _first-order reducts_ dari _model companion_ dari kelas semua _C-relations_,
    
- semua _first-order reducts_ dari _universal homogenous poset_,
    
- semua _first-order reducts_ dari _homogenous undirected graphs_,
    
- semua _first-order reducts_ dari semua _unary structures_,
    
- semua CSPs dalam kelas kompleksitas MMSNP.
    

Sebagian besar kelas CSPs yang diketahui _tractable_ adalah kelas di mana _hypergraph_ dari _constraints_ memiliki _treewidth_ yang terbatas, atau di mana _constraints_ memiliki bentuk arbitrer tetapi ada _equationally non-trivial polymorphisms_ dari kumpulan relasi _constraint_.

Sebuah _infinite-domain dichotomy conjecture_ telah dirumuskan untuk semua CSPs _reducts_ dari _finitely bounded homogenous structures_, yang menyatakan bahwa CSP dari struktur semacam itu berada di P jika dan hanya jika _polymorphism clone_-nya secara persamaan tidak trivial, dan bersifat NP-hard jika sebaliknya.

Kompleksitas dari _infinite-domain CSPs_ tersebut serta generalisasi lainnya (_Valued CSPs_, _Quantified CSPs_, _Promise CSPs_) masih menjadi area penelitian yang aktif.

Setiap CSP juga dapat dianggap sebagai _conjunctive query containment problem_.

### Masalah fungsi

Situasi serupa juga terjadi di antara kelas fungsional FP dan P. Berdasarkan generalisasi dari _Ladner's theorem_, terdapat pula masalah yang tidak berada di FP maupun P-complete asalkan FP != P. Sama seperti dalam kasus keputusan, sebuah masalah dalam CSP didefinisikan oleh sekumpulan relasi. Setiap masalah menerima _Boolean formula_ sebagai input dan tugasnya adalah menghitung jumlah _satisfying assignments_. Hal ini dapat digeneralisasi lebih lanjut dengan menggunakan ukuran _domain_ yang lebih besar serta menyematkan bobot pada setiap _satisfying assignment_, kemudian menghitung jumlah total dari bobot-bobot ini. Telah diketahui bahwa setiap masalah _weighted CSP_ yang kompleks berada di antara FP atau bersifat P-hard.

## Varian

Model klasik dari _Constraint Satisfaction Problem_ mendefinisikan model _constraints_ yang statis dan _inflexible_. Model yang kaku ini merupakan sebuah kelemahan yang membuatnya sulit untuk merepresentasikan berbagai masalah dengan mudah. Beberapa modifikasi dari definisi dasar CSP telah diusulkan untuk mengadaptasi model tersebut pada berbagai macam masalah.

### Dynamic CSPs

**Dynamic CSPs** (DCSPs) berguna ketika rumusan awal dari suatu masalah diubah dalam suatu cara, biasanya karena kumpulan _constraints_ yang perlu dipertimbangkan berkembang seiring kondisi lingkungan. DCSPs dipandang sebagai serangkaian _static CSPs_, di mana masing-masing merupakan transformasi dari yang sebelumnya, dengan variabel dan _constraints_ yang dapat ditambahkan (_restriction_) atau dihapus (_relaxation_). Informasi yang ditemukan dalam rumusan awal masalah dapat digunakan untuk menyempurnakan masalah berikutnya. Metode penyelesaiannya dapat diklasifikasikan berdasarkan cara informasi tersebut ditransfer:

- _Oracles_: solusi yang ditemukan untuk CSPs sebelumnya dalam urutan digunakan sebagai _heuristics_ untuk memandu penyelesaian CSP saat ini dari awal.
    
- _Local repair_: setiap CSP dihitung mulai dari _partial solution_ sebelumnya dan memperbaiki _constraints_ yang _inconsistent_ dengan _local search_.
    
- _Constraint recording_: _constraints_ baru didefinisikan di setiap tahap pencarian untuk merepresentasikan pembelajaran dari kelompok keputusan yang _inconsistent_. _Constraints_ tersebut dibawa ke masalah CSP yang baru.
    

### Flexible CSPs

_Classic CSPs_ memperlakukan _constraints_ sebagai batasan mutlak, yang berarti bersifat _imperative_ (setiap solusi harus memenuhi semuanya) dan _inflexible_ (dalam arti bahwa mereka harus terpenuhi sepenuhnya atau jika tidak maka akan sepenuhnya dilanggar). **Flexible CSPs** melonggarkan asumsi-asumsi tersebut dengan secara parsial melonggarkan _constraints_ dan mengizinkan solusi untuk tidak harus mematuhi semuanya. Hal ini mirip dengan preferensi dalam _preference-based planning_. Beberapa jenis _flexible CSPs_ meliputi:

- MAX-CSP, di mana sejumlah _constraints_ diizinkan untuk dilanggar, dan kualitas dari sebuah solusi diukur dari jumlah _constraints_ yang berhasil dipenuhi.
    
- _Weighted constraint satisfaction problem_ (Weighted CSP), yaitu MAX-CSP di mana setiap pelanggaran terhadap _constraint_ diberi bobot sesuai dengan preferensi yang telah ditentukan sebelumnya. Dengan demikian, memenuhi _constraint_ dengan bobot yang lebih besar akan lebih diutamakan.
    
- _Fuzzy CSP_ memodelkan _constraints_ sebagai _fuzzy relations_ di mana pemenuhan _constraint_ adalah _continuous function_ dari nilai variabel-variabelnya, yang bergerak dari terpenuhi sepenuhnya hingga dilanggar sepenuhnya.
    

### Decentralized CSPs

Dalam DCSPs, setiap _constraint variable_ dianggap memiliki lokasi geografis yang terpisah. _Strong constraints_ diterapkan pada pertukaran informasi antar variabel, yang mengharuskan penggunaan _fully distributed algorithms_ untuk menyelesaikan _constraint satisfaction problem_.