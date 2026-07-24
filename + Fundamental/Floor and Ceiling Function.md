Source: https://en.wikipedia.org/wiki/Floor_and_ceiling_functions

Dalam _mathematics_, **floor function** adalah _function_ yang menerima _real number_ $x$ sebagai _input_ dan mengembalikan _integer_ terbesar yang lebih kecil dari atau sama dengan $x$, ditulis $\lfloor x \rfloor$ atau $\text{floor}(x)$. Secara serupa, **ceiling function** mengembalikan _integer_ terkecil yang lebih besar dari atau sama dengan $x$, ditulis $\lceil x \rceil$ atau $\text{ceil}(x)$.

Sebagai contoh, untuk _floor_: $\lfloor 2.4 \rfloor = 2$, $\lfloor -2.4 \rfloor = -3$, dan untuk _ceiling_: $\lceil 2.4 \rceil = 3$, dan $\lceil -2.4 \rceil = -2$.

_Floor_ dari $x$ juga disebut _integral part_, _integer part_, _greatest integer_, atau _entier_ dari $x$, dan secara historis dilambangkan dengan $[x]$ (di antara notasi lainnya). Namun, istilah _integer part_ bersifat ambigu, karena juga dapat berarti _truncation_ menuju nol, yang berbeda dari _floor function_ untuk bilangan negatif.

Untuk sebuah _integer_ $n$, $\lfloor n \rfloor = \lceil n \rceil = n$.

Meskipun $\text{floor}(x + 1)$ dan $\text{ceil}(x)$ bernilai sama untuk nilai $x$ yang bukan _integer_, dan dengan demikian menghasilkan grafik yang tampak persis sama, keduanya berbeda ketika $x$ adalah sebuah _integer_. Sebagai contoh, ketika $x = 2.0001$, $\lfloor 2.0001 + 1 \rfloor = \lceil 2.0001 \rceil = 3$. Namun, jika $x = 2$, maka $\lfloor 2 + 1 \rfloor = 3$ tetapi $\lceil 2 \rceil = 2$.

### Contoh

|**x**|**Floor ⌊x⌋**|**Ceiling ⌈x⌉**|**Fractional part {x}**|
|---|---|---|---|
|2|2|2|0|
|2.0001|2|3|0.0001|
|$e$|2|3|0.7182...|
|2.9|2|3|0.9|
|2.999|2|3|0.999|
|$-\pi$|-4|-3|0.8584...|
|-2|-2|-2|0|

## Notasi

_Integral part_ atau _integer part_ dari sebuah bilangan pertama kali didefinisikan pada tahun 1798 oleh Adrien-Marie Legendre dalam pembuktiannya untuk _Legendre's formula_.

Carl Friedrich Gauss memperkenalkan notasi tanda kurung siku $[x]$ dalam pembuktian ketiganya tentang _quadratic reciprocity_ (1808). Ini tetap menjadi standar dalam _mathematics_ sampai Kenneth E. Iverson memperkenalkan nama _floor_ dan _ceiling_ beserta notasi yang sesuai $\lfloor x \rfloor$ dan $\lceil x \rceil$ dalam bukunya pada tahun 1962, _A Programming Language_. Kedua notasi tersebut sekarang digunakan dalam _mathematics_, meskipun notasi Iverson akan diikuti dalam artikel ini.

_Fractional part_ adalah _sawtooth function_, dilambangkan dengan $\{x\}$ untuk _real number_ $x$ dan didefinisikan oleh rumus:

$$1 = \{x\} = x - \lfloor x \rfloor$$

Untuk semua $x$,

$$1 = 0 \leq \{x\} < 1$$

## Definisi dan Properti

Diberikan _real numbers_ $x$ dan $y$, _integers_ $m$ dan $n$, serta himpunan _integers_ $\mathbb{Z}$, _floor_ dan _ceiling_ dapat didefinisikan oleh persamaan berikut:

$$\lfloor x \rfloor = \max \{m \in \mathbb{Z} \mid m \le x\}$$

$$\lceil x \rceil = \min \{n \in \mathbb{Z} \mid n \ge x\}$$

Karena tepat ada satu _integer_ dalam sebuah _half-open interval_ dengan panjang satu, untuk sembarang _real number_ $x$, terdapat _integers_ unik $m$ dan $n$ yang memenuhi persamaan:

$$x - 1 < m \le x \le n < x + 1$$

di mana $\lfloor x \rfloor = m$ dan $\lceil x \rceil = n$ juga dapat dianggap sebagai definisi dari _floor_ dan _ceiling_.

### Ekuivalensi

Rumus-rumus ini dapat digunakan untuk menyederhanakan ekspresi yang melibatkan _floors_ dan _ceilings_.

$$\lfloor x \rfloor = m \text{ jika dan hanya jika } m \le x < m + 1$$

$$\lceil x \rceil = n \text{ jika dan hanya jika } n - 1 < x \le n$$

$$\lfloor x \rfloor = m \text{ jika dan hanya jika } x - 1 < m \le x$$

$$\lceil x \rceil = n \text{ jika dan hanya jika } x \le n < x + 1$$

Dalam bahasa _order theory_, _floor function_ adalah sebuah _residuated mapping_, yaitu bagian dari sebuah _Galois connection_: ini adalah _upper adjoint_ dari fungsi yang menyematkan _integers_ ke dalam _reals_.

$$x < n \text{ jika dan hanya jika } \lfloor x \rfloor < n$$

$$n < x \text{ jika dan hanya jika } n < \lceil x \rceil$$

$$x \le n \text{ jika dan hanya jika } \lceil x \rceil \le n$$

$$n \le x \text{ jika dan hanya jika } n \le \lfloor x \rfloor$$

Rumus-rumus ini menunjukkan bagaimana menambahkan sebuah _integer_ $n$ pada argumen memengaruhi fungsi-fungsi tersebut:

$$\lfloor x + n \rfloor = \lfloor x \rfloor + n$$

$$\lceil x + n \rceil = \lceil x \rceil + n$$

$$\{x + n\} = \{x\}$$

Hal di atas tidak pernah benar jika $n$ bukan sebuah _integer_; namun, untuk setiap $x$ dan $y$, pertidaksamaan berikut berlaku:

$$\lfloor x \rfloor + \lfloor y \rfloor \leq \lfloor x + y \rfloor \leq \lfloor x \rfloor + \lfloor y \rfloor + 1$$

$$\lceil x \rceil + \lceil y \rceil - 1 \leq \lceil x + y \rceil \leq \lceil x \rceil + \lceil y \rceil$$

### Monotonisitas (_Monotonicity_)

Baik _floor function_ maupun _ceiling function_ adalah _monotonically non-decreasing functions_:

$$x_1 \le x_2 \Rightarrow \lfloor x_1 \rfloor \le \lfloor x_2 \rfloor$$

$$x_1 \le x_2 \Rightarrow \lceil x_1 \rceil \le \lceil x_2 \rceil$$

### Relasi Antar Fungsi

Jelas dari definisinya bahwa:

$$\lfloor x \rfloor \le \lceil x \rceil$$

dengan kesamaan berlaku jika dan hanya jika $x$ adalah sebuah _integer_, yaitu:

$$\lceil x \rceil - \lfloor x \rfloor = \begin{cases} 0 & \text{jika } x \in \mathbb{Z} \\ 1 & \text{jika } x \notin \mathbb{Z} \end{cases}$$

Faktanya, untuk _integers_ $n$, baik _floor_ maupun _ceiling functions_ adalah _identity function_:

$$\lfloor n \rfloor = \lceil n \rceil = n$$

Meniadakan argumen akan menukar _floor_ dan _ceiling_ serta mengubah tandanya:

$$\lfloor x \rfloor + \lceil -x \rceil = 0$$

$$-\lfloor x \rfloor = \lceil -x \rceil$$

$$-\lceil x \rceil = \lfloor -x \rfloor$$

serta:

$$\lfloor x \rfloor + \lfloor -x \rfloor = \begin{cases} 0 & \text{jika } x \in \mathbb{Z} \\ -1 & \text{jika } x \notin \mathbb{Z} \end{cases}$$

$$\lceil x \rceil + \lceil -x \rceil = \begin{cases} 0 & \text{jika } x \in \mathbb{Z} \\ 1 & \text{jika } x \notin \mathbb{Z} \end{cases}$$

Meniadakan argumen melengkapi bagian _fractional part_:

$$\{x\} + \{-x\} = \begin{cases} 0 & \text{jika } x \in \mathbb{Z} \\ 1 & \text{jika } x \notin \mathbb{Z} \end{cases}$$

Fungsi _floor_, _ceiling_, dan _fractional part_ bersifat _idempotent_:

$$\big\lfloor \lfloor x \rfloor \big\rfloor = \lfloor x \rfloor$$

$$\big\lceil \lceil x \rceil \big\rceil = \lceil x \rceil$$

$$\big\{ \{x\} \big\} = \{x\}$$

Hasil dari _floor_ atau _ceiling functions_ yang bersarang adalah fungsi yang paling dalam:

$$\big\lfloor \lceil x \rceil \big\rfloor = \lceil x \rceil$$

$$\big\lceil \lfloor x \rfloor \big\rceil = \lfloor x \rfloor$$

### Hasil Bagi (_Quotients_)

Jika $m$ dan $n$ adalah _integers_ dan $n \neq 0$,

$$0 \le \left\{ \frac{m}{n} \right\} \le 1 - \frac{1}{|n|}$$

Jika $n$ positif:

$$\left\lfloor\frac{x + m}{n}\right\rfloor = \left\lfloor\frac{\lfloor x\rfloor + m}{n}\right\rfloor$$

$$\left\lceil\frac{x + m}{n}\right\rceil = \left\lceil\frac{\lceil x\rceil + m}{n}\right\rceil$$

Jika $m$ positif:

$$n = \left\lceil\frac{n}{m}\right\rceil + \left\lceil\frac{n - 1}{m}\right\rceil + \dots + \left\lceil\frac{n - m + 1}{m}\right\rceil$$

$$n = \left\lfloor\frac{n}{m}\right\rfloor + \left\lfloor\frac{n + 1}{m}\right\rfloor + \dots + \left\lfloor\frac{n + m - 1}{m}\right\rfloor$$

Untuk $m = 2$, ini mengimplikasikan:

$$n = \left\lfloor \frac{n}{2}\right \rfloor + \left\lceil\frac{n}{2}\right \rceil$$

Lebih umum lagi, untuk $m$ positif (Lihat _Hermite's identity_):

$$\lceil mx \rceil = \left\lceil x \right\rceil + \left\lceil x - \frac{1}{m} \right\rceil + \dots + \left\lceil x - \frac{m - 1}{m} \right\rceil$$

$$\lfloor mx \rfloor = \left\lfloor x \right\rfloor + \left\lfloor x + \frac{1}{m} \right\rfloor + \dots + \left\lfloor x + \frac{m - 1}{m} \right\rfloor$$

Berikut ini dapat digunakan untuk mengonversi _floors_ menjadi _ceilings_ dan sebaliknya (dengan $m$ bernilai positif):

$$\left\lceil \frac{n}{m} \right\rceil = \left\lfloor \frac{n + m - 1}{m} \right\rfloor = \left\lfloor \frac{n - 1}{m} \right\rfloor + 1$$

$$\left\lfloor \frac{n}{m} \right\rfloor = \left\lceil \frac{n - m + 1}{m} \right\rceil = \left\lceil \frac{n + 1}{m} \right\rceil - 1$$

Untuk semua $m$ dan $n$ _integers_ bernilai positif ketat:

$$\sum_{k = 1}^{n - 1} \left\lfloor \frac{k m}{n} \right\rfloor = \frac{(m - 1)(n - 1) + \gcd(m, n) - 1}{2}$$

yang untuk $m$ dan $n$ positif serta _coprime_, direduksi menjadi:

$$\sum_{k=1}^{n-1} \left\lfloor \frac{km}{n} \right\rfloor = \frac{1}{2}(m - 1)(n - 1)$$

### Pembagian Bersarang (_Nested divisions_)

Untuk sebuah _integer_ positif $n$, dan _real numbers_ arbitrer $m$ dan $x$:

$$\left\lfloor \frac{\left\lfloor \frac{x}{m} \right\rfloor}{n} \right\rfloor = \left\lfloor \frac{x}{mn} \right\rfloor$$

$$\left\lceil \frac{\left\lceil \frac{x}{m} \right\rceil}{n} \right\rceil = \left\lceil \frac{x}{mn} \right\rceil$$

### Kontinuitas dan Ekspansi Deret (_Continuity and series expansions_)

Tidak ada satu pun dari fungsi yang dibahas dalam artikel ini yang merupakan _continuous function_, namun semuanya adalah _piecewise linear function_: fungsi $\lfloor x \rfloor$, $\lceil x \rceil$, dan $\{x\}$ memiliki diskontinuitas pada nilai _integers_.

Fungsi $\lfloor x \rfloor$ adalah _upper semi-continuous_ dan $\lceil x \rceil$ serta $\{x\}$ adalah _lower semi-continuous_.

Karena tidak ada fungsi yang kontinu, tidak ada yang memiliki ekspansi _power series_. Karena _floor_ dan _ceiling_ tidak periodik, keduanya tidak memiliki ekspansi _Fourier series_ yang konvergen secara seragam. Fungsi _fractional part_ memiliki ekspansi _Fourier series_:

$$\{x\} = \frac{1}{2} - \frac{1}{\pi} \sum_{k=1}^\infty \frac{\sin(2 \pi k x)}{k}$$

untuk $x$ yang bukan _integer_.

Menggunakan rumus $\lfloor x\rfloor = x - \{x\}$ memberikan:

$$\lfloor x\rfloor = x - \frac{1}{2} + \frac{1}{\pi} \sum_{k=1}^\infty \frac{\sin(2 \pi k x)}{k}$$

untuk $x$ yang bukan _integer_.

## Aplikasi

### Operator Mod (_Mod operator_)

Untuk sebuah _integer_ $x$ dan _integer_ positif $y$, _modulo operation_, dilambangkan dengan $x \bmod y$, memberikan nilai sisa ketika $x$ dibagi dengan $y$. Definisi ini dapat diperluas untuk $x$ dan $y$ berupa _real number_ dengan $y \neq 0$, melalui rumus:

$$x \bmod y = x - y\left\lfloor \frac{x}{y}\right\rfloor$$

### Resiprositas Kuadratik (_Quadratic reciprocity_)

Pembuktian ketiga Gauss mengenai _quadratic reciprocity_, seperti yang dimodifikasi oleh Eisenstein, memiliki dua langkah dasar. Misalkan $p$ dan $q$ adalah _prime numbers_ ganjil positif yang berbeda, dan misalkan $m = \frac{1}{2}(p - 1)$ dan $n = \frac{1}{2}(q - 1)$. Langkah pertama menggunakan _Gauss's lemma_ untuk menunjukkan _Legendre symbols_, kemudian argumen geometris digunakan untuk menggabungkan rumus guna memberikan _quadratic reciprocity_.

### Pembulatan (_Rounding_)

Untuk sembarang _real number_ $x$, membulatkan $x$ ke _integer_ terdekat dengan pemecahan seri (_tie breaking_) menuju _positive infinity_ diberikan oleh:

$$\text{rpi}(x) = \left\lfloor x + \frac{1}{2} \right\rfloor = \left\lceil \frac{1}{2}\lfloor 2x \rfloor \right\rceil$$

pembulatan menuju _negative infinity_ diberikan oleh:

$$\text{rni}(x) = \left\lceil x - \frac{1}{2} \right\rceil = \left\lfloor \frac{1}{2} \lceil 2x \rceil \right\rfloor$$

### Jumlah Digit (_Number of digits_)

Jumlah digit dalam _radix_ basis $b$ dari _integer_ positif $k$ adalah:

$$\lfloor \log_{b}{k} \rfloor + 1 = \lceil \log_{b}{(k + 1)} \rceil$$

### Faktor dari Faktorial (_Factors of factorials_)

Misalkan $n$ adalah _integer_ positif dan $p$ adalah _prime number_ positif. Eksponen dari pangkat tertinggi $p$ yang membagi $n!$ diberikan oleh sebuah versi dari _Legendre's formula_:

$$\left\lfloor\frac{n}{p}\right\rfloor + \left\lfloor\frac{n}{p^2}\right\rfloor + \left\lfloor\frac{n}{p^3}\right\rfloor + \dots = \frac{n - \sum_{k}a_k}{p - 1}$$

di mana $n = \sum_{k}a_kp^k$ adalah cara menuliskan $n$ dalam basis $p$.

### Konstanta Euler (_Euler's constant_ $\gamma$)

Terdapat rumus-rumus untuk _Euler's constant_ $\gamma = 0.5772156649\dots$ yang melibatkan _floor_ dan _ceiling_, contohnya:

$$\gamma = \int_1^\infty\left(\frac{1}{\lfloor x\rfloor} - \frac{1}{x}\right)\,dx$$

$$\gamma = \lim_{n \to \infty} \frac{1}{n} \sum_{k=1}^n \left( \left \lceil \frac{n}{k} \right \rceil - \frac{n}{k} \right)$$

### Fungsi Zeta Riemann (_Riemann zeta function_ $\zeta$)

Fungsi _fractional part_ juga muncul dalam representasi integral dari _Riemann zeta function_. Jika digabungkan dengan ekspansi _Fourier_ untuk $\{x\}$, ini dapat digunakan untuk memperluas fungsi zeta ke seluruh _complex plane_.

### Rumus untuk Bilangan Prima (_Formulas for prime numbers_)

_Floor function_ muncul dalam beberapa rumus yang mengkarakterisasi _prime numbers_. Sebagai contoh, _integer_ positif $n$ adalah sebuah bilangan prima jika dan hanya jika:

$$\sum_{m=1}^\infty \left(\left\lfloor\frac{n}{m}\right\rfloor - \left\lfloor\frac{n - 1}{m}\right\rfloor\right) = 2$$

## Implementasi Komputer (_Computer implementations_)

Dalam sebagian besar bahasa pemrograman, metode paling sederhana untuk mengonversi _floating point number_ menjadi _integer_ tidak melakukan _floor_ atau _ceiling_, melainkan _truncate_.

Sebuah _arithmetic right-shift_ dari _signed integer_ $x$ sebesar $n$ sama dengan $\left\lfloor \frac{x}{2^n} \right\rfloor$.

Banyak bahasa pemrograman (termasuk C, C++, C#, Java, Julia, PHP, R, dan Python) menyediakan _standard functions_ untuk _floor_ dan _ceiling_, yang biasanya dinamakan `floor` dan `ceil`, atau yang lebih jarang `ceiling`.

Dalam Microsoft Excel, fungsi `INT` membulatkan ke bawah alih-alih menuju nol, sementara `FLOOR` membulatkan menuju nol, kebalikan dari apa yang dilakukan `int` dan `floor` dalam bahasa lain. Namun sejak 2010, `FLOOR` telah diubah agar menghasilkan pesan kesalahan jika bilangannya negatif. Pada format _OpenDocument_ yang digunakan oleh LibreOffice dan lain-lain, `INT` dan `FLOOR` keduanya berfungsi melakukan _floor_.