Source: https://en.wikipedia.org/wiki/Gaussian_elimination

Dalam matematika, **eliminasi Gauss**, juga dikenal sebagai **reduksi baris**, adalah sebuah algoritma untuk menyelesaikan sistem persamaan linear. Algoritma ini terdiri dari serangkaian operasi baris yang dilakukan pada matriks koefisien yang sesuai. Metode ini juga dapat digunakan untuk menghitung peringkat (rank) dari sebuah matriks, determinan dari matriks persegi, dan invers dari matriks yang dapat dibalik (*invertible*). Metode ini dinamai dari Carl Friedrich Gauss (1777–1855).

Untuk melakukan reduksi baris pada sebuah matriks, kita menggunakan serangkaian operasi baris elementer untuk memodifikasi matriks hingga sudut kiri bawah matriks terisi dengan angka nol sebanyak mungkin. Ada tiga jenis operasi baris elementer:
* menukar dua baris,
* mengalikan sebuah baris dengan angka bukan nol, dan
* menambahkan kelipatan dari satu baris ke baris lainnya.

Dengan menggunakan operasi-operasi ini, sebuah matriks selalu dapat diubah menjadi *bentuk eselon baris tereduksi*: setiap baris bukan nol berada di atas setiap baris nol, setiap baris bukan nol memiliki entri bukan nol paling kiri yang bernilai 1 (disebut angka 1 utama), kolom-kolom yang mengandung angka 1 utama ini memiliki semua entri lainnya 0, dan angka 1 utama di setiap baris bukan nol berada di sebelah kanan angka 1 utama di baris sebelumnya. Bentuk akhir ini unik; dengan kata lain, terlepas dari urutan operasi baris yang digunakan. 

Sebagai contoh, dalam urutan operasi baris berikut, matriks ketiga dan keempat berada dalam bentuk eselon baris, dan matriks akhir adalah bentuk eselon baris tereduksi yang unik:

$$\begin{bmatrix} 1 & 3 & 1 & 9 \\ 1 & 1 & -1 & 1 \\ 3 & 11 & 5 & 35 \end{bmatrix} \to \begin{bmatrix} 1 & 3 & 1 & 9 \\ 0 & -2 & -2 & -8 \\ 0 & 2 & 2 & 8 \end{bmatrix} \to \begin{bmatrix} 1 & 3 & 1 & 9 \\ 0 & -2 & -2 & -8 \\ 0 & 0 & 0 & 0 \end{bmatrix} \to \begin{bmatrix} 1 & 0 & -2 & -3 \\ 0 & 1 & 1 & 4 \\ 0 & 0 & 0 & 0 \end{bmatrix}$$

Menggunakan operasi baris untuk mengubah sebuah matriks menjadi bentuk eselon baris tereduksi kadang-kadang disebut **eliminasi Gauss-Jordan**. Dalam hal ini, istilah *eliminasi Gauss* merujuk pada proses hingga ia mencapai bentuk eselon baris atas (segitiga atas, tidak tereduksi). Untuk alasan komputasi saat menyelesaikan sistem persamaan linear, kadang-kadang lebih disukai untuk menghentikan operasi baris sebelum matriks sepenuhnya tereduksi.

## Definisi dan Contoh Algoritma

Proses reduksi baris memanfaatkan operasi baris elementer dan dapat dibagi menjadi dua bagian. Bagian pertama (kadang-kadang disebut eliminasi maju) mereduksi sistem yang diberikan menjadi bentuk eselon baris, di mana kita dapat mengetahui apakah ada solusi yang tidak terhingga, solusi unik, atau tidak ada solusi sama sekali. Bagian kedua (kadang-kadang disebut substitusi balik) terus menggunakan operasi baris hingga solusi ditemukan; dengan kata lain, langkah ini mengubah matriks ke dalam bentuk eselon baris tereduksi.

### Operasi Baris
Ada tiga jenis operasi baris elementer yang dapat dilakukan pada baris-baris matriks:
1. Menukar dua baris.
2. Mengalikan sebuah baris dengan skalar bukan nol.
3. Menambahkan kelipatan skalar dari satu baris ke baris lainnya.

Jika matriks tersebut diasosiasikan dengan sebuah sistem persamaan linear, maka operasi-operasi ini tidak akan mengubah himpunan solusinya.

### Bentuk Eselon
Untuk setiap baris dalam sebuah matriks, jika baris tersebut tidak hanya terdiri dari angka nol, maka entri bukan nol paling kiri disebut *entri utama* (atau *pivot*) dari baris tersebut. Dengan menggunakan operasi penukaran baris, kita selalu dapat mengurutkan baris sedemikian rupa sehingga untuk setiap baris bukan nol, entri utamanya berada di sebelah kanan entri utama dari baris di atasnya. Jika ini tercapai, matriks tersebut dikatakan berada dalam *bentuk eselon baris*. 

Sebagai contoh, matriks berikut berada dalam bentuk eselon baris, dan entri utamanya ditampilkan secara tebal:

$$\begin{bmatrix}   0 & \mathbf{2} & 1 & -1 \\   0 & 0 & \mathbf{3} & 1 \\   0 & 0 & 0 & 0 \end{bmatrix}$$

Matriks tersebut berada dalam bentuk eselon karena baris nol ada di bagian bawah dan entri utama baris kedua berada di sebelah kanan entri utama baris pertama.

### Contoh Algoritma
Misalkan kita ingin mencari solusi untuk sistem persamaan linear berikut:

$$\begin{align*}   2x + y - z &= 8 \quad (L_1) \\  -3x - y + 2z &= -11 \quad (L_2) \\  -2x + y + 2z &= -3 \quad (L_3) \end{align*}$$

Prosedur reduksi baris diterapkan pada matriks yang diperbesar (*augmented matrix*). Pertama-tama, kita eliminasi $x$ dari semua persamaan di bawah $L_1$, dan kemudian eliminasi $y$ dari semua persamaan di bawah $L_2$. 

**Matriks Diperbesar Awal:**
$$\left[\begin{array}{rrr\|r}   2 &  1 & -1 &  8 \\  -3 & -1 &  2 & -11 \\  -2 &  1 &  2 & -3 \end{array}\right]$$

**Langkah 1:** Eliminasi $x$ dari $L_2$ dan $L_3$.
Lakukan operasi $L_2 + \frac{3}{2} L_1 \to L_2$ dan $L_3 + L_1 \to L_3$:
$$\left[\begin{array}{rrr\|r}  2 & 1 & -1 & 8 \\  0 & \frac{1}{2} & \frac{1}{2} & 1 \\  0 & 2 & 1 & 5 \end{array}\right]$$

**Langkah 2:** Eliminasi $y$ dari baris ketiga.
Lakukan operasi $L_3 - 4 L_2 \to L_3$:
$$\left[\begin{array}{rrr\|r}  2 & 1 & -1 & 8 \\  0 & \frac{1}{2} & \frac{1}{2} & 1 \\  0 & 0 & -1 & 1 \end{array}\right]$$
*(Matriks sekarang berada dalam bentuk eselon baris/bentuk segitiga).*

**Langkah 3:** Substitusi balik (menuju bentuk eselon baris tereduksi).
Lakukan operasi $L_1 - L_3 \to L_1$ dan $L_2 + \frac{1}{2} L_3 \to L_2$:
$$\left[\begin{array}{rrr\|r}  2 & 1 & 0 & 7 \\  0 & \frac{1}{2} & 0 & \frac{3}{2} \\  0 & 0 & -1 & 1 \end{array}\right]$$

**Langkah 4:** Jadikan entri utama menjadi 1.
Lakukan operasi $2 L_2 \to L_2$ dan $-L_3 \to L_3$:
$$\left[\begin{array}{rrr\|r}  2 & 1 & 0 & 7 \\  0 & 1 & 0 & 3 \\  0 & 0 & 1 & -1 \end{array}\right]$$

**Langkah 5:** Eliminasi entri di atas angka 1 utama.
Lakukan operasi $L_1 - L_2 \to L_1$, kemudian $\frac{1}{2} L_1 \to L_1$:
$$\left[\begin{array}{rrr\|r}  1 & 0 & 0 & 2 \\  0 & 1 & 0 & 3 \\  0 & 0 & 1 & -1 \end{array}\right]$$
Solusi dari sistem di atas adalah $x = 2$, $y = 3$, dan $z = -1$.

## Sejarah
Metode eliminasi Gauss muncul pertama kali tanpa pembuktian dalam teks matematika Tiongkok Kuno "Bab Delapan: Susunan Persegi Panjang" dari *Sembilan Bab tentang Seni Matematika*. Penyelesaian persamaan linear dengan metode eliminasi ini ditemukan secara terpisah di beberapa budaya di Eurasia.

Di Eropa, metode ini bersumber dari catatan Isaac Newton (1669–1670). Ia melengkapi buku-buku aljabar saat itu yang belum memiliki tata cara penyelesaian persamaan simultan. Carl Friedrich Gauss pada tahun 1810 merancang notasi untuk eliminasi simetris yang kemudian diadopsi pada abad ke-19 oleh *human computer* (petugas penghitung) untuk menyelesaikan persamaan normal dari masalah kuadrat terkecil. Algoritma ini baru dinamai menggunakan nama Gauss pada tahun 1950-an.

## Aplikasi

### Menghitung Determinan
Eliminasi Gauss memungkinkan perhitungan determinan dari sebuah matriks persegi. Saat reduksi baris dilakukan, determinan dipengaruhi oleh aturan berikut:
* Menukar baris akan mengalikan determinan dengan -1.
* Mengalikan baris dengan skalar akan mengalikan determinan dengan skalar tersebut.
* Menambahkan kelipatan suatu baris ke baris lain tidak mengubah determinan.

Jika eliminasi Gauss pada matriks $A$ menghasilkan matriks eselon $B$, dan $d$ adalah hasil kali skalar-skalar yang telah memengaruhi determinan, maka:
$$\det(A) = \frac{\prod\operatorname{diag}(B)}{d}$$
Secara komputasi, metode ini jauh lebih efisien untuk matriks berukuran besar ($O(n^3)$) dibandingkan menggunakan rumus Leibniz.

### Mencari Invers Matriks
Varian eliminasi Gauss-Jordan dapat digunakan untuk menemukan invers dari matriks persegi $A$. Kita cukup menyejajarkan matriks $A$ dengan matriks identitas $I$ sehingga membentuk matriks yang diperbesar $[A \mid I]$. Dengan menggunakan reduksi baris, matriks ini diubah menjadi bentuk eselon baris tereduksi. Jika blok kiri berhasil menjadi matriks identitas $I$, maka blok kanan otomatis menjadi inversnya, $A^{-1}$.

### Menghitung Peringkat (Rank) dan Basis
Algoritma ini bisa mereduksi matriks $m \times n$ apa pun ke dalam bentuk eselon. Banyaknya baris yang tidak seluruhnya nol pada bentuk eselon tersebut menunjukkan peringkat (*rank*) dari matriks aslinya. Selain itu, posisi kolom-kolom yang mengandung *entri utama* (*pivot*) menunjukkan kolom-kolom mana dari matriks asli yang membentuk basis untuk ruang kolomnya.

## Efisiensi Komputasi
Algoritma eliminasi Gauss untuk sistem $n$ persamaan memiliki kompleksitas aritmatika sekitar $O(n^3)$. Ini berarti metode ini sangat efisien untuk menghitung solusi dari matriks dengan elemen tipe data *floating-point* atau di dalam *finite field*. Namun, untuk matriks bernilai bilangan rasional, ada risiko *exponential growth* (pembengkakan eksponensial) dari nilai-nilai pecahannya selama proses komputasi. Varian yang disebut **Algoritma Bareiss** menyelesaikan masalah ini dengan membatasi kompleksitas bit pada tingkat *strongly-polynomial* $O(n^5)$.

Satu masalah penting saat menggunakan algoritma ini pada komputer adalah ketidakstabilan numerik (*numerical instability*), terutama jika algoritma mencoba membagi dengan angka yang sangat dekat dengan nol. Masalah ini biasanya diatasi dengan teknik pemivotaan parsial (*partial pivoting*).

## Pseudokode
Berikut adalah algoritma *in-place* standar untuk eliminasi Gauss dengan *partial pivoting* untuk mengonversi matriks $A$ ($m \times n$) ke bentuk eselon baris.

```text
h := 1 /* Inisialisasi baris pivot */
k := 1 /* Inisialisasi kolom pivot */

while h ≤ m and k ≤ n:
    /* Temukan pivot ke-k: */
    i_max := argmax (i = h ... m, abs(A[i, k]))
    
    if A[i_max, k] = 0:
        /* Tidak ada pivot di kolom ini, lanjut ke kolom berikutnya */
        k := k + 1
    else:
        swap rows(h, i_max)
        /* Lakukan untuk semua baris di bawah pivot: */
        for i = h + 1 ... m:
            f := A[i, k] / A[h, k]
            /* Isi dengan nol untuk bagian bawah kolom pivot: */
            A[i, k] := 0
            /* Lakukan untuk sisa elemen di baris saat ini: */
            for j = k + 1 ... n:
                A[i, j] := A[i, j] - A[h, j] * f
                
        /* Lanjut ke baris dan kolom pivot berikutnya */
        h := h + 1
        k := k + 1
