[[Constraint Satisfaction Problem (CSP)]] | [[Greedy Algorithm]] | [[Queue]] | [[Vector]]

- [[#1 Pendahuluan|1 Pendahuluan]]
	- [[#1 Pendahuluan#1.1 Latar Belakang|1.1 Latar Belakang]]
	- [[#1 Pendahuluan#1.2 Perbedaan Paradigma Kedua Solusi|1.2 Perbedaan Paradigma Kedua Solusi]]
	- [[#1 Pendahuluan#1.3 Tujuan Laporan|1.3 Tujuan Laporan]]
- [[#2 Spesifikasi Problem|2 Spesifikasi Problem]]
	- [[#2 Spesifikasi Problem#2.1 Deskripsi Masalah|2.1 Deskripsi Masalah]]
	- [[#2 Spesifikasi Problem#2.2 Definisi Formal|2.2 Definisi Formal]]
	- [[#2 Spesifikasi Problem#2.3 Analisis Struktur Problem|2.3 Analisis Struktur Problem]]
- [[#3 Landasan Teori|3 Landasan Teori]]
	- [[#3 Landasan Teori#3.1 Refleksi Laser dan Aturan Cermin|3.1 Refleksi Laser dan Aturan Cermin]]
	- [[#3 Landasan Teori#3.2 Pemilihan Cermin "Belok Kanan"|3.2 Pemilihan Cermin "Belok Kanan"]]
	- [[#3 Landasan Teori#3.3 Non-Crossing Matching dan Bracket Sequence|3.3 Non-Crossing Matching dan Bracket Sequence]]
	- [[#3 Landasan Teori#3.4 Region Coloring dan Depth Parity|3.4 Region Coloring dan Depth Parity]]
	- [[#3 Landasan Teori#3.5 CSP, Propagasi Arc Consistency (AC3), dan Backtracking|3.5 CSP, Propagasi Arc Consistency (AC3), dan Backtracking]]
- [[#4 Solusi 1: Greedy Berbasis Non-Crossing Matching|4 Solusi 1: Greedy Berbasis Non-Crossing Matching]]
	- [[#4 Solusi 1: Greedy Berbasis Non-Crossing Matching#4.1 Ide Utama|4.1 Ide Utama]]
	- [[#4 Solusi 1: Greedy Berbasis Non-Crossing Matching#4.2 Pembuktian Kebenaran Algoritma|4.2 Pembuktian Kebenaran Algoritma]]
		- [[#4.2 Pembuktian Kebenaran Algoritma#Lemma 1 (Syarat Perlu): Jika solusi ada, matching harus non-crossing.|Lemma 1 (Syarat Perlu): Jika solusi ada, matching harus non-crossing.]]
		- [[#4.2 Pembuktian Kebenaran Algoritma#Lemma 2 (Syarat Cukup): Jika matching non-crossing, solusi selalu ada.|Lemma 2 (Syarat Cukup): Jika matching non-crossing, solusi selalu ada.]]
		- [[#4.2 Pembuktian Kebenaran Algoritma#Lemma 3 (Kebenaran Greedy Tracing):|Lemma 3 (Kebenaran Greedy Tracing):]]
		- [[#4.2 Pembuktian Kebenaran Algoritma#Teorema (Kebenaran Total Solusi 1):|Teorema (Kebenaran Total Solusi 1):]]
	- [[#4 Solusi 1: Greedy Berbasis Non-Crossing Matching#4.3 Pseudocode|4.3 Pseudocode]]
	- [[#4 Solusi 1: Greedy Berbasis Non-Crossing Matching#4.4 Implementasi C++|4.4 Implementasi C++]]
	- [[#4 Solusi 1: Greedy Berbasis Non-Crossing Matching#4.5 Analisis Kompleksitas|4.5 Analisis Kompleksitas]]
- [[#5 Solusi 2: CSP dengan AC3 dan Backtracking|5 Solusi 2: CSP dengan AC3 dan Backtracking]]
	- [[#5 Solusi 2: CSP dengan AC3 dan Backtracking#5.1 Ide Utama|5.1 Ide Utama]]
	- [[#5 Solusi 2: CSP dengan AC3 dan Backtracking#5.2 Pembuktian Kebenaran Algoritma|5.2 Pembuktian Kebenaran Algoritma]]
		- [[#5.2 Pembuktian Kebenaran Algoritma#Lemma 1 (Kebenaran Region Tree dari Perimeter Scan):|Lemma 1 (Kebenaran Region Tree dari Perimeter Scan):]]
		- [[#5.2 Pembuktian Kebenaran Algoritma#Lemma 2 (Kebenaran Depth Parity):|Lemma 2 (Kebenaran Depth Parity):]]
		- [[#5.2 Pembuktian Kebenaran Algoritma#Lemma 3 (Completeness AC3 + Backtracking):|Lemma 3 (Completeness AC3 + Backtracking):]]
	- [[#5 Solusi 2: CSP dengan AC3 dan Backtracking#5.3 Pseudocode|5.3 Pseudocode]]
	- [[#5 Solusi 2: CSP dengan AC3 dan Backtracking#5.4 Implementasi C++|5.4 Implementasi C++]]
	- [[#5 Solusi 2: CSP dengan AC3 dan Backtracking#5.5 Analisis Kompleksitas|5.5 Analisis Kompleksitas]]
- [[#6 Perbandingan dan Analisis Dua Solusi|6 Perbandingan dan Analisis Dua Solusi]]
	- [[#6 Perbandingan dan Analisis Dua Solusi#6.1 Tabel Komparatif|6.1 Tabel Komparatif]]
	- [[#6 Perbandingan dan Analisis Dua Solusi#6.2 Narasi Perbandingan|6.2 Narasi Perbandingan]]
		- [[#6.2 Narasi Perbandingan#Eksploitasi Struktur Matematika|Eksploitasi Struktur Matematika]]
		- [[#6.2 Narasi Perbandingan#Kompleksitas Praktis|Kompleksitas Praktis]]
		- [[#6.2 Narasi Perbandingan#Kapan Solusi 2 Lebih Relevan?|Kapan Solusi 2 Lebih Relevan?]]
- [[#7 Kesimpulan|7 Kesimpulan]]
	- [[#7 Kesimpulan#7.1 Pola Berpikir Sistematis dalam Memecahkan Grid Constraint Problem|7.1 Pola Berpikir Sistematis dalam Memecahkan Grid Constraint Problem]]
	- [[#7 Kesimpulan#7.2 Ringkasan Konsep Kunci|7.2 Ringkasan Konsep Kunci]]
- [[#8 Referensi|8 Referensi]]



## 1 Pendahuluan

### 1.1 Latar Belakang

Problem JC15E — _Laser Beam 2.0_ adalah problem rekonstruksi: diberikan sebuah grid $X \times Y$ yang setiap selnya berisi cermin diagonal (`/` atau `\`), dan diketahui label koneksi laser pada keempat sisi grid, tugasnya adalah menemukan penempatan cermin yang valid sehingga setiap pasang laser berlabel sama terhubung satu sama lain melalui pantulan.

Problem ini menarik karena solusinya tidak tunggal secara harfiah — ada banyak konfigurasi cermin yang mungkin memenuhi syarat — namun pada saat yang sama struktur matematisnya sangat terstruktur sehingga memungkinkan solusi yang sangat efisien jika kita mengeksploitasi sifat topologisnya.

### 1.2 Perbedaan Paradigma Kedua Solusi

Dua pendekatan yang dianalisis dalam laporan ini merepresentasikan dua paradigma yang fundamental berbeda dalam pemecahan masalah:

- **Solusi 1** mengeksploitasi properti matematika khusus problem: bahwa pasangan laser harus membentuk _non-crossing matching_ di perimeter, dan kondisi ini sudah cukup untuk membangun solusi secara greedy tanpa pencarian sama sekali.
    
- **Solusi 2** memodelkan problem sebagai _Constraint Satisfaction Problem (CSP)_ umum: setiap titik sudut sel memiliki domain nilai yang mungkin, dan solusi diperoleh melalui propagasi constraint (AC3) dan backtracking.
    

### 1.3 Tujuan Laporan

Laporan ini bertujuan untuk:

1. Mendefinisikan problem JC15E secara formal dan mengidentifikasi struktur matematisnya.
2. Menurunkan rumus-rumus yang digunakan beserta derivasinya.
3. Menjelaskan dan membuktikan kebenaran kedua solusi secara terpisah.
4. Menyajikan pseudocode dan implementasi C++ lengkap dengan komentar detail.
5. Membandingkan kedua solusi dari sisi kompleksitas, elegansitas, dan ketepatan pemodelan.
6. Menyimpulkan solusi mana yang lebih optimal beserta alasannya.

---

## 2 Spesifikasi Problem

### 2.1 Deskripsi Masalah

Diberikan grid $X \times Y$. Di setiap sisi terdapat laser dengan label angka:

- Sisi atas: $Y$ laser menembak ke **bawah**
- Sisi bawah: $Y$ laser menembak ke **atas**
- Sisi kiri: $X$ laser menembak ke **kanan**
- Sisi kanan: $X$ laser menembak ke **kiri**

Total port di perimeter:

$$|\mathcal{P}| = 2X + 2Y$$

Setiap label muncul tepat dua kali, sehingga terbentuk **perfect matching** $M$ dengan:

$$|M| = X + Y \quad \text{(jumlah pasangan)}$$

**Tujuan:** Isi setiap sel $(i,j)$ dengan `'/'` atau `'\'` sehingga untuk setiap pasangan ${p, q} \in M$ dengan $\ell(p) = \ell(q)$, jalur laser dari $p$ berakhir di $q$ (dan sebaliknya). Jika tidak memungkinkan, cetak `-1`.

### 2.2 Definisi Formal

- **Grid:** $G$ berukuran $X \times Y$, $G[i][j] \in {\{/, \text{\\}}\}$ untuk $0 \leq i < X$, $0 \leq j < Y$.
- **Port:** Himpunan $\mathcal{P}$ dari $2X + 2Y$ titik di perimeter. Tiap port $p$ memiliki: label $\ell(p) \in {1, \ldots, X+Y}$, posisi di luar grid $(r_p, c_p)$, dan arah masuk $d_p$.
- **Matching:** $M$ = himpunan pasangan ${p, q}$ dengan $\ell(p) = \ell(q)$.
- **Jalur laser:** Untuk port $p$, jejak laser $\tau(p)$ mengikuti aturan pantulan cermin hingga keluar grid.
- **Solusi valid:** Grid $G$ valid jika $\forall {p,q} \in M : \tau(p)$ berakhir di $q$.

**Constraint:**

$$1 \leq X, Y \leq 100, \quad 1 \leq \text{label} \leq X+Y, \quad \text{setiap label muncul tepat 2 kali}$$

### 2.3 Analisis Struktur Problem

**Observasi 1 (Planarity):** Karena setiap sel hanya memiliki satu cermin, tidak ada dua jalur laser berbeda yang dapat berpotongan di dalam grid. Jalur-jalur laser adalah kurva Jordan sederhana yang terpisah di bidang planar.

**Observasi 2 (Non-Crossing Necessity):** Akibat Observasi 1, pasangan-pasangan label di perimeter harus membentuk _non-crossing matching_ dalam urutan _clockwise_. Ini adalah **syarat perlu** untuk keberadaan solusi.

**Observasi 3 (Sufisiensi):** Non-crossing matching bukan hanya syarat perlu, tetapi juga **syarat cukup** — jika matching non-crossing, solusi selalu bisa dikonstruksi. Observasi ini adalah kunci yang membedakan kedua pendekatan.

**Observasi 4 (Region Tree):** Grid cermin yang valid mendefinisikan region-region yang membentuk pohon bersarang (laminar family). Struktur pohon ini bisa dibangun langsung dari perimeter scan.

---

## 3 Landasan Teori

### 3.1 Refleksi Laser dan Aturan Cermin

Laser bergerak dalam empat arah yang dikodekan sebagai bilangan bulat:

$$\text{dir} \in {0, 1, 2, 3} \quad \text{di mana } 0=\text{atas},; 1=\text{kanan},; 2=\text{bawah},; 3=\text{kiri}$$

Pergerakan laser dikodekan dengan vektor delta:

$$\Delta r = (-1,; 0,; 1,; 0), \quad \Delta c = (0,; 1,; 0,; -1)$$

**Derivasi aturan pantulan cermin:**

Bayangkan sumbu koordinat: arah 0 (atas) adalah $-y$, arah 2 (bawah) adalah $+y$, arah 1 (kanan) adalah $+x$, arah 3 (kiri) adalah $-x$.

Cermin `/` adalah garis dengan gradien $-1$ (kemiringan $135°$). Refleksi terhadap garis $y = -x$ menukar komponen dan membalik tanda, sehingga:

$$f_{/}(\text{dir}) = \begin{cases} 0 \to 1 & \text{(atas} \to \text{kanan)} \\ 1 \to 0 & \text{(kanan} \to \text{atas)} \\ 2 \to 3 & \text{(bawah} \to \text{kiri)} \\ 3 \to 2 & \text{(kiri} \to \text{bawah)} \end{cases}$$

Cermin `\` adalah garis dengan gradien $+1$ (kemiringan $45°$). Refleksi terhadap garis $y = x$ menukar komponen tanpa membalik tanda, sehingga:

$$f_{\backslash}(\text{dir}) = \begin{cases} 0 \to 3 & \text{(atas} \to \text{kiri)} \\ 3 \to 0 & \text{(kiri} \to \text{atas)} \\ 1 \to 2 & \text{(kanan} \to \text{bawah)} \\ 2 \to 1 & \text{(bawah} \to \text{kanan)} \end{cases}$$

Kedua fungsi ini dirangkum dalam tabel lookup konstan yang dapat diringkas sebagai:

$$\text{table}_{/} = [1, 0, 3, 2], \quad \text{table}_{\backslash} = [3, 2, 1, 0]$$

**Tabel pantulan lengkap:**

|Arah Masuk|Cermin `/`|Cermin `\`|
|:-:|:-:|:-:|
|Atas (0)|Kanan (1)|Kiri (3)|
|Kanan (1)|Atas (0)|Bawah (2)|
|Bawah (2)|Kiri (3)|Kanan (1)|
|Kiri (3)|Bawah (2)|Atas (0)|

### 3.2 Pemilihan Cermin "Belok Kanan"

Dalam Solusi 1, sel kosong diisi dengan cermin yang memaksa laser **belok 90° ke kanan** dari perspektif arah geraknya. Derivasinya:

- Laser bergerak **vertikal** (arah $0$ atau $2$): belok kanan berarti beralih ke arah horizontal. Cermin `/` memenuhi ini: $0 \to 1$ (atas→kanan) dan $2 \to 3$ (bawah→kiri). Maka:

$$\text{dir} \in {0, 2} \Rightarrow \text{cermin} = \text{`/'}$$

- Laser bergerak **horizontal** (arah $1$ atau $3$): belok kanan berarti beralih ke arah vertikal. Cermin `\` memenuhi ini: $1 \to 2$ (kanan→bawah) dan $3 \to 0$ (kiri→atas). Maka:

$$
\text{dir} \in {1, 3} \Rightarrow \text{cermin} = \text{`\\`}
$$

**Mengapa "belok kanan"?** Karena matching non-crossing, jalur setiap laser berbentuk "busur" yang tidak saling memotong. Konsisten belok ke satu arah menjamin laser tidak berputar tanpa akhir dan pasti mencapai tujuannya.

### 3.3 Non-Crossing Matching dan Bracket Sequence

Diberikan himpunan port di perimeter yang disusun dalam urutan _clockwise_, sebuah matching $M$ disebut **non-crossing** jika:

$$\nexists; (a,b),(c,d) \in M : a < c < b < d \quad \text{(dalam urutan clockwise)}$$

Kondisi ini setara dengan kondisi bahwa urutan label di perimeter membentuk **bracket sequence yang valid**:

$$\text{non-crossing} \iff \text{sequence label valid sebagai kurung buka-tutup}$$

**Derivasi kesetaraan:** Label yang muncul pertama kali bertindak sebagai "kurung buka", kemunculan kedua sebagai "kurung tutup". Dua pasangan $(a,b)$ dan $(c,d)$ dengan $a < c < b < d$ persis merepresentasikan pola kurung yang bersilang: `a ... c ... b ... d` = `( ... ( ... ) ... )` yang tidak valid. Stack parsing mendeteksi ini dalam $O(X+Y)$.

**Algoritma verifikasi (Stack):** Push label baru, pop jika label sama dengan top. Jika pop gagal (top berbeda) atau stack tidak kosong di akhir, matching tidak valid.

### 3.4 Region Coloring dan Depth Parity

Grid cermin membagi bidang menjadi **region** — wilayah yang terhubung tanpa menyeberangi cermin. Region-region ini membentuk **laminar family** (struktur pohon bersarang):

$$\text{region}_{i} \subset \text{region}_{j} ;\text{atau}; \text{region}_{j} \subset \text{region}_{i} ;\text{atau keduanya disjoint}$$

Properti penting dari representasi vertex:

- Setiap **vertex** (titik sudut sel, posisi $(r, c)$ untuk $0 \leq r \leq X$, $0 \leq c \leq Y$) berada tepat di batas antara dua region bertetangga.
- Jenis cermin di sel $(i, j)$ ditentukan dari region sudut kiri-atas dan kanan-bawah:
    - `region[tl] == region[br]` → cermin `\`
    - `region[tl] != region[br]` → cermin `/`

**Teorema Depth Parity:** Untuk setiap grid cermin yang valid, region di vertex $(i, j)$ memiliki kedalaman $d$ dengan:

$$d \equiv (i + j) \pmod{2}$$

**Derivasi:** Setiap langkah dari vertex $(i,j)$ ke tetangganya mengubah $(i+j)$ sebesar $\pm 1$, sehingga paritas $(i+j)$ selalu berubah. Setiap langkah juga melewati sisi sel. Jika sisi tersebut merupakan batas antar region, kedalaman berubah $\pm 1$ (paritas berubah). Dalam kedua kasus, paritas selalu sama dengan $(i+j) \bmod 2$. ∎

**Konsekuensi:** Domain vertex interior $(i,j)$ hanya mencakup region dengan kedalaman berparitas $(i+j) \bmod 2$:

$$\text{domain}(i,j) = { k \in [0,K) : d_k \equiv (i+j) \pmod{2} }$$

### 3.5 CSP, Propagasi Arc Consistency (AC3), dan Backtracking

**Constraint Satisfaction Problem (CSP)** adalah framework untuk masalah di mana setiap variabel memiliki domain nilai dan harus memenuhi sekumpulan constraint. Solusi diperoleh dengan:

**1. Propagasi constraint (AC3):** Untuk setiap arc $\langle u, v \rangle$, AC3 memastikan setiap nilai $y \in \text{dom}(v)$ memiliki _support_ di $\text{dom}(u)$:

$$\forall y \in \text{dom}(v),; \exists x \in \text{dom}(u) : (x, y) \in \text{constraints}$$

Dalam konteks region coloring, constraint adalah $x$ dan $y$ harus **bertetangga di pohon region** (hubungan parent-child). Jika $y$ tidak memiliki support, $y$ dihapus dari $\text{dom}(v)$.

**Kompleksitas AC3:**

$$T_{\text{AC3}} = O(e \cdot d^2)$$

di mana $e$ adalah jumlah arc dan $d$ adalah ukuran domain maksimum. Dalam problem ini: $e = 4N$, $d \approx K/2$, sehingga $T_{\text{AC3}} = O(N \cdot K^2)$.

**2. Backtracking dengan MRV:** Pilih variabel dengan domain terkecil (Minimum Remaining Values / _fail-first_ strategy), coba setiap nilai, jalankan AC3, rekursi. Jika kontradiksi, undo dan coba nilai lain. Trail memastikan undo benar sehingga tidak ada state yang bocor antar cabang.

---


## 4 Solusi 1: Greedy Berbasis Non-Crossing Matching

### 4.1 Ide Utama

Solusi 1 mengeksploitasi Observasi 2 dan 3: karena non-crossing matching adalah syarat **perlu sekaligus cukup**, tidak diperlukan pencarian sama sekali. Algoritma bekerja dalam tiga tahap utama:

**Tahap 1 — Validasi:** Susun semua port searah jarum jam dan verifikasi bahwa pasangan label membentuk bracket sequence yang valid (non-crossing). Jika gagal, langsung output `-1`.

**Tahap 2 — Greedy Tracing:** Untuk setiap label, trace laser dari endpoint ke-2 (yang memiliki urutan _clockwise_ lebih besar). Setiap sel kosong yang dilewati diisi dengan cermin yang membuat laser "belok kanan" terhadap arah gerak saat itu:

- Arah vertikal (atas/bawah): pasang `'/'`
- Arah horizontal (kiri/kanan): pasang `'\'`

Endpoint ke-2 diproses dari urutan _clockwise_ terkecil ke terbesar agar cermin yang sudah diisi tidak ditimpa.

**Tahap 3 — Pengisian Sisa dan Verifikasi:** Sel yang tidak dilalui laser manapun diisi dengan `'/'`. Kemudian semua jalur diverifikasi ulang sebagai _safety net_.

### 4.2 Pembuktian Kebenaran Algoritma

#### Lemma 1 (Syarat Perlu): Jika solusi ada, matching harus non-crossing.

**Bukti:** Misalkan ada dua pasangan laser $(a, b)$ dan $(c, d)$ yang _crossing_ dalam urutan _clockwise_, yaitu $a < c < b < d$. Jalur laser $a \to b$ dan $c \to d$ keduanya adalah kurva sederhana yang menghubungkan titik-titik di tepi grid. Karena $a, c, b, d$ muncul berselang-seling di perimeter, **Jordan Curve Theorem** menjamin kedua kurva harus berpotongan. Perpotongan ini berarti ada sel yang dilewati dua jalur laser berbeda — mustahil dalam grid 1 cermin/sel. Kontradiksi. ∎

#### Lemma 2 (Syarat Cukup): Jika matching non-crossing, solusi selalu ada.

**Bukti dengan induksi pada jumlah pasangan:**

_Basis (1 pasangan):_ Dengan satu pasangan laser, grid dapat selalu diisi dengan kombinasi cermin yang mengarahkan laser dari satu port ke port lainnya. Ini selalu mungkin karena jalur tunggal tidak memiliki constraint silang.

_Langkah Induksi:_ Andaikan untuk $k$ pasangan selalu ada solusi. Pada non-crossing matching dengan $k+1$ pasangan, selalu terdapat satu pasangan $(p, q)$ yang **berdekatan** (tidak ada port lain di antara $p$ dan $q$ dalam urutan _clockwise_). Pasangan ini dapat dilayani dengan jalur sederhana yang tidak memotong area yang diperlukan pasangan lain. Setelah jalur ini dibangun, sisa $k$ pasangan membentuk non-crossing matching di sub-region yang lebih kecil — dan _by induction hypothesis_, solusinya ada. ∎

#### Lemma 3 (Kebenaran Greedy Tracing):

Ketika kita memproses endpoint ke-2 dari urutan _clockwise_ terkecil ke terbesar, setiap trace laser tidak pernah melewati sel yang sudah terisi, karena sifat non-crossing menjamin jalur-jalur bersifat _nested_ (bersarang), bukan _crossing_. Cermin "belok kanan" yang dipilih secara konsisten memastikan laser tidak terjebak dalam loop tak hingga dan pasti mencapai exit yang benar. ∎

#### Teorema (Kebenaran Total Solusi 1):

Dari Lemma 1, 2, dan 3: Solusi 1 output `-1` jika dan hanya jika tidak ada solusi, dan jika ada solusi, Solusi 1 selalu berhasil mengkonstruksinya. ∎

### 4.3 Pseudocode

```
FUNCTION MAIN():
  Baca X, Y
  Baca topLabel[], leftLabel[], rightLabel[], bottomLabel[]

  // Susun port searah jarum jam
  // Urutan: Top (kiri→kanan) | Right (atas→bawah) | Bottom (kanan→kiri) | Left (bawah→atas)
  FOR j = 0 to Y-1:
    addPort(topLabel[j],    r=-1, c=j,  dir=BAWAH)
  FOR i = 0 to X-1:
    addPort(rightLabel[i],  r=i,  c=Y,  dir=KIRI)
  FOR j = Y-1 downto 0:
    addPort(bottomLabel[j], r=X,  c=j,  dir=ATAS)
  FOR i = X-1 downto 0:
    addPort(leftLabel[i],   r=i,  c=-1, dir=KANAN)

  // Validasi frekuensi label
  IF ada label dengan count ≠ 2:
    RETURN output -1

  // Validasi non-crossing (bracket sequence)
  IF NOT checkNonCrossing():
    RETURN output -1

  // Inisialisasi grid kosong
  grid[i][j] = '.' untuk semua (i, j)

  // Urutkan endpoint ke-2 tiap label berdasarkan idx clockwise (insertion sort)
  order[] = {(endpoints[v][1].idx, v)} untuk tiap label v
  insertionSort(order by idx ascending)

  // Greedy trace dari urutan clockwise terkecil ke terbesar
  FOR tiap (idx, label) dalam order:
    IF NOT traceFrom(endpoints[label][1]):
      RETURN output -1

  // Isi sel kosong dengan '/'
  FOR tiap sel (i,j) dengan grid[i][j] == '.':
    grid[i][j] = '/'

  // Verifikasi final semua jalur (safety net)
  IF NOT verifyFinal():
    RETURN output -1

  Cetak grid


FUNCTION checkNonCrossing():
  stack = kosong
  seen[v] = false untuk semua v
  FOR tiap port p dalam urutan clockwise:
    v = p.label
    IF NOT seen[v]:
      seen[v] = true
      stack.push(v)        // "kurung buka"
    ELSE:
      IF stack.empty() OR stack.top() ≠ v:
        RETURN false       // crossing terdeteksi!
      stack.pop()          // "kurung tutup"
  RETURN stack.empty()


FUNCTION traceFrom(port start):
  label = start.label
  r = start.r + dr[start.dir]   // langkah pertama masuk ke grid
  c = start.c + dc[start.dir]
  dir = start.dir
  steps = 0; maxSteps = 4*X*Y+10  // batas keamanan infinite-loop

  WHILE (r, c) masih di dalam grid:
    IF ++steps > maxSteps: RETURN false
    IF grid[r][c] == '.':
      // Sel kosong: isi dengan cermin belok kanan
      IF dir == ATAS atau BAWAH: grid[r][c] = '/'
      ELSE:                      grid[r][c] = '\'
    dir = turnDir(dir, grid[r][c])  // pantulkan arah
    r += dr[dir]; c += dc[dir]      // pindah ke sel berikutnya

  RETURN (label di port keluar (r,c)) == label


FUNCTION verifyFinal():
  FOR tiap port p:
    Trace laser dari p mengikuti grid yang sudah terisi (hanya baca, tidak ubah)
    IF label keluar ≠ p.label: RETURN false
  RETURN true
```

### 4.4 Implementasi C++

```cpp
/*
 * =============================================================================
 * SOLUSI 1: Greedy Berbasis Non-Crossing Matching
 * =============================================================================
 *
 * ALGORITMA:
 *   1. Susun semua port (titik masuk/keluar laser) searah jarum jam.
 *   2. Verifikasi bahwa pasangan label membentuk bracket sequence valid
 *      (non-crossing matching) menggunakan stack.
 *   3. Trace laser dari setiap endpoint ke-2 (urutan clockwise lebih besar),
 *      isi sel kosong dengan cermin "belok kanan".
 *   4. Isi sisa sel kosong dengan '/'.
 *   5. Verifikasi semua jalur benar sebagai safety net.
 *
 * KOMPLEKSITAS: O((X+Y)*X*Y) waktu, O(X*Y) ruang
 * =============================================================================
 */

#include <cstdio>
#include <cstring>

// ---- Batas ukuran array ----
#define MAXN     105   // batas X atau Y (maksimum 100)
#define MAXLABEL 205   // batas label berbeda = X + Y <= 200
#define MAXPERIM 405   // batas total port di perimeter = 2X + 2Y <= 400

// ============================================================
// STRUKTUR DATA PORT
// Merepresentasikan satu titik masuk/keluar laser di tepi grid.
// ============================================================
struct Port {
    int label; // nomor label laser (1 .. X+Y)
    int r, c;  // posisi "di luar" grid (r=-1 untuk sisi atas, c=Y untuk sisi kanan, dll)
    int dir;   // arah gerak laser saat masuk ke dalam grid
               //   0=atas, 1=kanan, 2=bawah, 3=kiri
    int idx;   // urutan clockwise port ini di array perimeter (0 = pertama)
};

// ---- Dimensi grid ----
int X, Y;

// ---- Label laser di setiap sisi grid ----
int topLabel[MAXN];    // sisi atas   : topLabel[j]    = label kolom j
int bottomLabel[MAXN]; // sisi bawah  : bottomLabel[j] = label kolom j
int leftLabel[MAXN];   // sisi kiri   : leftLabel[i]   = label baris i
int rightLabel[MAXN];  // sisi kanan  : rightLabel[i]  = label baris i

// ---- Representasi grid isi cermin ----
// grid[i][j] in {'.', '/', '\'}
// '.' = belum diisi, '/' = cermin diagonal atas, '\' = cermin diagonal bawah
char grid[MAXN][MAXN];

// ---- Daftar semua port, disusun clockwise ----
Port perimeter[MAXPERIM];
int  perimSize;

// ---- Untuk tiap label, simpan ke-2 port yang memiliki label tersebut ----
// endpoints[v][0] = port pertama label v (idx clockwise lebih kecil)
// endpoints[v][1] = port kedua  label v (idx clockwise lebih besar)
Port endpoints[MAXLABEL][2];
int  endpointCount[MAXLABEL];

// ============================================================
// VEKTOR DELTA ARAH
// dir: 0=atas(-1,0), 1=kanan(0,+1), 2=bawah(+1,0), 3=kiri(0,-1)
// ============================================================
int dr[4] = {-1, 0, 1, 0};
int dc[4] = { 0, 1, 0,-1};

// ============================================================
// FUNGSI: turnDir
// Hitung arah baru laser setelah menabrak cermin.
//
// DERIVASI:
// Cermin '/' = refleksi terhadap y = -x  =>  table: [1, 0, 3, 2]
// Cermin '\' = refleksi terhadap y =  x  =>  table: [3, 2, 1, 0]
// ============================================================
int turnDir(int dir, char mirror) {
    if (mirror == '/') {
        int tbl[] = {1, 0, 3, 2};
        return tbl[dir];
    } else {
        int tbl[] = {3, 2, 1, 0};
        return tbl[dir];
    }
}

// ============================================================
// FUNGSI: mirrorForRightTurn
// Pilih jenis cermin yang membuat laser belok 90 derajat ke kanan.
//
// DERIVASI:
//   dir in {0,2} (vertikal)  => '/'   (0->1, 2->3: beralih ke horizontal)
//   dir in {1,3} (horizontal) => '\'  (1->2, 3->0: beralih ke vertikal)
// ============================================================
char mirrorForRightTurn(int dir) {
    if (dir == 0 || dir == 2) return '/';
    return '\\';
}

// ============================================================
// FUNGSI: getExitLabel
// Ambil label laser di titik (r, c) yang sudah keluar dari grid.
// ============================================================
int getExitLabel(int r, int c) {
    if (r < 0)  return topLabel[c];
    if (r >= X) return bottomLabel[c];
    if (c < 0)  return leftLabel[r];
    return rightLabel[r];
}

// ============================================================
// FUNGSI: addPort
// Tambah satu port ke array perimeter dan ke array endpoints.
// ============================================================
void addPort(int label, int r, int c, int dir) {
    Port p;
    p.label = label;
    p.r     = r;
    p.c     = c;
    p.dir   = dir;
    p.idx   = perimSize;

    perimeter[perimSize++] = p;

    int cnt = endpointCount[label];
    endpoints[label][cnt] = p;
    endpointCount[label]++;
}

// ============================================================
// FUNGSI: checkNonCrossing
// Verifikasi bracket sequence yang valid menggunakan stack.
//
// BUKTI KESETARAAN dengan non-crossing:
//   Dua pasangan (a,b) dan (c,d) crossing <=> a < c < b < d
//   <=> saat b ditemukan, top stack adalah a, bukan c => gagal
//
// Kompleksitas: O(X+Y)
// ============================================================
int checkNonCrossing() {
    int  stack[MAXPERIM];
    int  stackTop = 0;
    int  seen[MAXLABEL];
    memset(seen, 0, sizeof(seen));

    for (int i = 0; i < perimSize; i++) {
        int v = perimeter[i].label;
        if (!seen[v]) {
            seen[v] = 1;
            stack[stackTop++] = v; // kurung buka
        } else {
            if (stackTop == 0 || stack[stackTop - 1] != v) return 0;
            stackTop--;            // kurung tutup
        }
    }
    return (stackTop == 0);
}

// ============================================================
// FUNGSI: traceFrom
// Trace jalur laser dari port 'start' ke dalam grid.
// Sel kosong yang dilewati diisi dengan cermin belok kanan.
// Sel berisi cermin tidak diubah.
//
// maxSteps: batas defensive untuk mencegah infinite loop.
// Seharusnya tidak pernah tercapai jika non-crossing check lulus.
// ============================================================
int traceFrom(Port start) {
    int label    = start.label;
    int r        = start.r + dr[start.dir];
    int c        = start.c + dc[start.dir];
    int dir      = start.dir;
    int steps    = 0;
    int maxSteps = 4 * X * Y + 10;

    while (r >= 0 && r < X && c >= 0 && c < Y) {
        if (++steps > maxSteps) return 0;

        if (grid[r][c] == '.') {
            grid[r][c] = mirrorForRightTurn(dir);
        }

        dir = turnDir(dir, grid[r][c]);
        r += dr[dir];
        c += dc[dir];
    }

    return (getExitLabel(r, c) == label);
}

// ============================================================
// FUNGSI: verifyFinal
// Verifikasi semua jalur laser setelah grid terisi penuh.
// Hanya membaca, tidak mengubah grid.
// ============================================================
int verifyFinal() {
    for (int i = 0; i < perimSize; i++) {
        int r   = perimeter[i].r + dr[perimeter[i].dir];
        int c   = perimeter[i].c + dc[perimeter[i].dir];
        int dir = perimeter[i].dir;
        int steps    = 0;
        int maxSteps = 4 * X * Y + 10;

        while (r >= 0 && r < X && c >= 0 && c < Y) {
            if (++steps > maxSteps) return 0;
            dir = turnDir(dir, grid[r][c]);
            r += dr[dir];
            c += dc[dir];
        }

        if (getExitLabel(r, c) != perimeter[i].label) return 0;
    }
    return 1;
}

// ============================================================
// STRUKTUR & FUNGSI: OrderItem + insertionSort
// Mengurutkan endpoint ke-2 tiap label berdasarkan idx clockwise.
//
// MENGAPA DIURUTKAN DARI idx TERKECIL?
//   Sifat nested dari non-crossing matching: endpoint dengan idx
//   clockwise terkecil memiliki jalur "terdalam" (paling bersarang).
//   Memproses dari terdalam ke terluar menjamin cermin yang sudah
//   dipasang tidak ditimpa oleh jalur berikutnya.
//
// Insertion sort dipilih karena jumlah elemen <= X+Y <= 200,
// sehingga O(n^2) = O(40.000) sudah lebih dari cukup.
// ============================================================
struct OrderItem {
    int idx;
    int label;
};

void insertionSort(OrderItem arr[], int n) {
    for (int i = 1; i < n; i++) {
        OrderItem key = arr[i];
        int j = i - 1;
        while (j >= 0 && arr[j].idx > key.idx) {
            arr[j + 1] = arr[j];
            j--;
        }
        arr[j + 1] = key;
    }
}

// ============================================================
// MAIN
// ============================================================
int main() {
    scanf("%d %d", &X, &Y);

    memset(endpointCount, 0, sizeof(endpointCount));
    perimSize = 0;

    // ---- Baca input ----
    for (int j = 0; j < Y; j++) scanf("%d", &topLabel[j]);
    for (int i = 0; i < X; i++) scanf("%d %d", &leftLabel[i], &rightLabel[i]);
    for (int j = 0; j < Y; j++) scanf("%d", &bottomLabel[j]);

    // ============================================================
    // SUSUN PORT SEARAH JARUM JAM
    //
    // Posisi port "di luar" grid:
    //   Top:    r = -1, c = j    (satu baris di atas baris 0)
    //   Right:  r = i,  c = Y    (satu kolom di kanan kolom Y-1)
    //   Bottom: r = X,  c = j    (satu baris di bawah baris X-1)
    //   Left:   r = i,  c = -1   (satu kolom di kiri kolom 0)
    // ============================================================
    for (int j = 0; j < Y; j++)
        addPort(topLabel[j],    -1, j,  2); // sisi atas, menembak ke bawah
    for (int i = 0; i < X; i++)
        addPort(rightLabel[i],  i,  Y,  3); // sisi kanan, menembak ke kiri
    for (int j = Y-1; j >= 0; j--)
        addPort(bottomLabel[j], X,  j,  0); // sisi bawah, menembak ke atas
    for (int i = X-1; i >= 0; i--)
        addPort(leftLabel[i],   i, -1,  1); // sisi kiri, menembak ke kanan

    // ---- Validasi: setiap label tepat 2 kali ----
    int possible = 1;
    for (int v = 1; v <= X + Y; v++) {
        if (endpointCount[v] != 2) { possible = 0; break; }
    }

    // ---- Validasi non-crossing ----
    if (possible && !checkNonCrossing()) possible = 0;

    if (!possible) { printf("-1\n"); return 0; }

    // ---- Inisialisasi grid kosong ----
    for (int i = 0; i < X; i++) {
        for (int j = 0; j < Y; j++) grid[i][j] = '.';
        grid[i][Y] = '\0';
    }

    // ---- Susun dan urutkan endpoint ke-2 ----
    OrderItem order[MAXLABEL];
    int orderSize = 0;
    for (int v = 1; v <= X + Y; v++) {
        order[orderSize].idx   = endpoints[v][1].idx;
        order[orderSize].label = v;
        orderSize++;
    }
    insertionSort(order, orderSize);

    // ---- Greedy trace ----
    for (int i = 0; i < orderSize && possible; i++) {
        int v = order[i].label;
        if (!traceFrom(endpoints[v][1])) possible = 0;
    }

    if (!possible) { printf("-1\n"); return 0; }

    // ---- Isi sel kosong dengan '/' ----
    // Sel yang tidak dilalui laser tidak punya constraint;
    // '/' selalu aman karena tidak akan mengganggu jalur yang ada.
    for (int i = 0; i < X; i++)
        for (int j = 0; j < Y; j++)
            if (grid[i][j] == '.') grid[i][j] = '/';

    // ---- Verifikasi final ----
    if (!verifyFinal()) { printf("-1\n"); return 0; }

    // ---- Output grid ----
    for (int i = 0; i < X; i++) printf("%s\n", grid[i]);

    return 0;
}
```

### 4.5 Analisis Kompleksitas

Rumus total kompleksitas waktu:

$$T_1 = O(X+Y) + O((X+Y)^2) + O((X+Y) \cdot X \cdot Y)$$

Karena $(X+Y)^2 \leq (X+Y) \cdot X \cdot Y$ untuk $X, Y \geq 1$, suku dominannya adalah:

$$T_1 = O!\left((X+Y) \cdot X \cdot Y\right)$$

|Tahap|Kompleksitas Waktu|Kompleksitas Ruang|
|---|---|---|
|Susun port perimeter|$O(X + Y)$|$O(X + Y)$|
|Non-crossing check (stack)|$O(X + Y)$|$O(X + Y)$|
|Insertion sort endpoint|$O((X+Y)^2)$|$O(X + Y)$|
|Greedy trace semua label|$O((X+Y) \cdot X \cdot Y)$|$O(X \cdot Y)$|
|Verifikasi final|$O((X+Y) \cdot X \cdot Y)$|$O(1)$|
|**Total**|$O((X+Y) \cdot X \cdot Y)$|$O(X \cdot Y)$|

Untuk $X = Y = 100$: $T_1 \approx 200 \times 100 \times 100 = 2{,}000{,}000$ operasi — selesai dalam milidetik.

---

## 5 Solusi 2: CSP dengan AC3 dan Backtracking

### 5.1 Ide Utama

Solusi 2 tidak memanfaatkan sifat non-crossing secara langsung. Sebaliknya, ia memodelkan problem sebagai CSP menggunakan konsep **region coloring**.

**Variabel:** Setiap vertex (titik sudut sel) $u = (i, j)$ adalah sebuah variabel dengan indeks $u = i(Y+1) + c$.

**Domain:** Himpunan region yang mungkin untuk vertex $u$. Domain dibatasi oleh depth parity: vertex $(i,j)$ hanya bisa memiliki region dengan kedalaman berparitas $(i+j) \bmod 2$.

**Constraint:** Dua vertex yang bertetangga harus memiliki region yang **bertetangga di pohon region** (hubungan parent-child).

**Decoding:** Setelah semua domain terisi satu nilai, cermin di sel $(i,j)$ ditentukan dari:

- `region[tl] == region[br]` → cermin `\`
- `region[tl] != region[br]` → cermin `/`

di mana `tl` = vertex $(i, j)$ dan `br` = vertex $(i+1, j+1)$.

Algoritma bekerja dalam empat fase:

**Fase 1 — Bangun Region Tree:** Perimeter scan menggunakan stack parsing menghasilkan pohon region (laminar family). Setiap vertex di perimeter langsung memiliki region yang diketahui.

**Fase 2 — Inisialisasi Domain:** Vertex perimeter memiliki domain singleton. Vertex interior memiliki domain berisi semua region dengan paritas kedalaman yang sesuai.

**Fase 3 — AC3:** Propagasi arc consistency dari semua vertex. Setiap nilai tanpa support di domain tetangganya dihapus.

**Fase 4 — Backtracking + MRV:** Jika AC3 belum menentukan semua vertex, pilih vertex dengan domain terkecil (MRV), coba setiap nilai, jalankan AC3, rekursi. Gunakan trail untuk undo.

### 5.2 Pembuktian Kebenaran Algoritma

#### Lemma 1 (Kebenaran Region Tree dari Perimeter Scan):

Stack parsing pada perimeter sequence menghasilkan region tree yang valid jika dan hanya jika label membentuk non-crossing matching.

**Bukti:** Parsing identik dengan validasi bracket sequence. Label pertama = open bracket (push region baru), label kedua = close bracket (pop). Jika parsing berhasil tanpa konflik, struktur bersarang terpenuhi, yang persis adalah definisi non-crossing matching. ∎

#### Lemma 2 (Kebenaran Depth Parity):

Untuk setiap grid cermin yang valid, vertex $(i, j)$ selalu memiliki region dengan kedalaman berparitas $(i+j) \bmod 2$.

**Bukti dengan induksi pada jarak dari vertex $(0,0)$:**

_Basis:_ Vertex $(0,0)$ berada di sudut grid, termasuk region luar (kedalaman $0$ = genap). Dan $(0+0) \bmod 2 = 0$. Konsisten.

_Langkah:_ Setiap langkah dari vertex ke vertex tetangga melewati sisi sel. Jika sisi tersebut merupakan batas cermin, kedalaman berubah $\pm 1$, sehingga paritas berubah. Paritas $(i+j)$ juga berubah tepat 1 setiap langkah. Maka keduanya selalu sinkron. ∎

#### Lemma 3 (Completeness AC3 + Backtracking):

Kombinasi AC3 dan backtracking adalah prosedur yang _complete_: jika solusi ada, pasti akan ditemukan; jika tidak ada, akan menghasilkan kontradiksi pada setiap cabang.

**Bukti:** AC3 bersifat _sound_ (hanya menghapus nilai yang terbukti tidak konsisten, tidak pernah menghapus nilai yang valid). Backtracking menjelajahi seluruh ruang pencarian secara sistematis. Trail memastikan undo benar sehingga tidak ada state yang bocor antar cabang. ∎

### 5.3 Pseudocode

```
FUNCTION MAIN():
  Baca X, Y, Top[], Left[], Right[], Bottom[]
  N = (X+1)*(Y+1)  // jumlah vertex

  // FASE 1: Perimeter scan → bangun region tree
  // Susun sequence searah jarum jam: Top | Right | Bottom (terbalik) | Left (terbalik)
  // Tiap entry: (label, vertex_r, vertex_c)
  K = 1  // region 0 = luar (root), parent[0] = -1, depth[0] = 0
  cur_state = 0
  stk = kosong
  region_of[r][c] = -1 untuk semua r, c

  FOR tiap (label, vertex (r,c)) dalam sequence perimeter:
    IF stk tidak kosong AND stk.top().label == label:
      stk.pop()
      cur_state = parent[cur_state]    // naik ke region parent
    ELSE:
      buat region baru dengan id K
      parent[K] = cur_state
      depth[K] = depth[cur_state] + 1
      stk.push(label, K)
      cur_state = K; K++               // masuk ke region baru

    IF region_of[r][c] sudah diset AND ≠ cur_state:
      RETURN output -1                 // konflik region
    region_of[r][c] = cur_state

  IF stk tidak kosong: RETURN output -1

  // Bangun adj_region[k]: setiap region bertetangga dengan parent & anak-anaknya
  FOR k = 1 to K-1:
    adj_region[k].add(parent[k])
    adj_region[parent[k]].add(k)

  // FASE 2: Inisialisasi domain
  FOR tiap vertex u = (i, j):
    IF region_of[i][j] diketahui:
      domain[u] = {region_of[i][j]}              // singleton (vertex perimeter)
    ELSE:
      parity = (i + j) % 2
      domain[u] = {k : 0 <= k < K AND depth[k] % 2 == parity}  // vertex interior
    IF domain[u] kosong: RETURN output -1

  // FASE 3: AC3 awal
  Queue.push(semua vertex)
  IF NOT ac3(): RETURN output -1

  // FASE 4: Backtracking + MRV
  IF NOT solve(): RETURN output -1

  // Output: decode cermin dari region assignment
  FOR tiap sel (i, j):
    tl = satu-satunya nilai di domain[i*(Y+1)+j]
    br = satu-satunya nilai di domain[(i+1)*(Y+1)+(j+1)]
    Cetak '\' jika tl == br, else '/'


FUNCTION ac3():
  WHILE Queue tidak kosong:
    u = Queue.pop()
    FOR tiap tetangga v dari u (4 arah):
      changed = false
      FOR tiap y di domain[v]:
        // Support: ada x di adj_region[y] yang juga ada di domain[u]?
        has_support = (∃ x ∈ adj_region[y] : x ∈ domain[u])
        IF NOT has_support:
          hapus y dari domain[v], catat di trail
          changed = true
          IF domain[v] kosong: RETURN false  // kontradiksi
      IF changed: Queue.push(v)
  RETURN true


FUNCTION solve() [MRV Backtracking]:
  // Cari vertex dengan domain_size > 1 terkecil (MRV / fail-first)
  u = argmin{domain_size[i] : domain_size[i] > 1}
  IF tidak ada: RETURN true        // semua vertex sudah fixed!

  candidates = semua nilai di domain[u]
  FOR tiap val di candidates:
    saved = trail.size()
    // Paksakan domain[u] = {val}: hapus semua nilai lain
    FOR k di candidates, k ≠ val:
      remove_from_domain(u, k)
    Queue.push(u)
    IF ac3() AND solve(): RETURN true
    // UNDO: kembalikan trail ke checkpoint
    Kembalikan trail ke posisi saved
    Queue.clear()

  RETURN false                     // semua kandidat gagal
```

### 5.4 Implementasi C++

```cpp
/*
 * =============================================================================
 * SOLUSI 2: CSP dengan AC3 + Backtracking (MRV Heuristic)
 * =============================================================================
 *
 * PEMODELAN:
 *   - Variabel: setiap vertex (sudut sel) u = (i,j), indeks u = i*(Y+1)+j
 *   - Domain: himpunan region yang mungkin untuk vertex u
 *   - Constraint: dua vertex bertetangga harus memiliki region yang
 *                 bertetangga di pohon region (hubungan parent-child)
 *   - Decoding: sel (i,j) => '\' jika region(tl)==region(br), else '/'
 *
 * KOMPLEKSITAS: O(B*N*K^2) waktu, O(N*K) ruang
 *   N=(X+1)(Y+1), K=jumlah region~O(X+Y), B=jumlah langkah backtracking
 * =============================================================================
 */

#include <cstdio>
#include <cstring>
#include <vector>
#include <queue>
using namespace std;

const int MAXXY = 101;
const int MAXN  = MAXXY * MAXXY;
const int MAXK  = 2 * MAXXY * 2 + 4;

int X, Y;
int N;  // jumlah vertex = (X+1)*(Y+1)
int K;  // jumlah region dari perimeter scan

// ============================================================
// DATA REGION TREE
//
// Region 0 = "luar" (root), depth=0
// Region k>0: parent_region[k], depth_region[k]
//
// Pohon ini terbentuk dari perimeter scan (stack parsing):
//   Label pertama => buka region baru (push)
//   Label kedua   => tutup region (pop)
//
// Rumus kedalaman: depth[k] = depth[parent[k]] + 1
// ============================================================
int parent_region[MAXK];
int depth_region[MAXK];

// adj_region[k] = daftar region bertetangga langsung dengan k (parent + anak)
vector<int> adj_region[MAXK];

// ============================================================
// DOMAIN SETIAP VERTEX
//
// domain[u][k] = true  => region k masih mungkin untuk vertex u
// domain_size[u]       => cacah nilai true di domain[u]
//   == 1 => fixed (singleton)
//   == 0 => kontradiksi!
// ============================================================
vector<bool> domain[MAXN];
int domain_size[MAXN];

// ============================================================
// QUEUE UNTUK AC3
// Menggunakan in_queue untuk mencegah duplikat (efisiensi).
// ============================================================
queue<int> bfs_queue;
bool in_queue[MAXN];

void queue_push(int u) {
    if (!in_queue[u]) { in_queue[u] = true; bfs_queue.push(u); }
}
int queue_pop() {
    int u = bfs_queue.front(); bfs_queue.pop();
    in_queue[u] = false; return u;
}
bool queue_empty() { return bfs_queue.empty(); }
void queue_clear() {
    while (!bfs_queue.empty()) bfs_queue.pop();
    memset(in_queue, 0, sizeof(in_queue));
}

// ============================================================
// TRAIL (untuk undo backtracking)
//
// Setiap penghapusan dari domain dicatat.
// Saat backtrack, kembalikan semua penghapusan sejak checkpoint.
// ============================================================
struct TrailEntry { int vertex; int region; };
vector<TrailEntry> trail;

// ============================================================
// FUNGSI: get_neighbor
// Kembalikan indeks vertex tetangga dari vertex u ke arah dir.
//
// RUMUS INDEKSASI:
//   Vertex (r, c) => indeks u = r * (Y+1) + c
//   Inverse: r = u / (Y+1),  c = u % (Y+1)
//
// 4 arah: 0=atas(r-1), 1=bawah(r+1), 2=kiri(c-1), 3=kanan(c+1)
// Return -1 jika di luar batas.
// ============================================================
int get_neighbor(int u, int dir) {
    int r = u / (Y + 1), c = u % (Y + 1);
    if      (dir == 0) r--;
    else if (dir == 1) r++;
    else if (dir == 2) c--;
    else               c++;
    if (r < 0 || r > X || c < 0 || c > Y) return -1;
    return r * (Y + 1) + c;
}

// ============================================================
// FUNGSI: remove_from_domain
// Hapus region 'reg' dari domain[v] dan catat di trail.
// ============================================================
void remove_from_domain(int v, int reg) {
    if (domain[v][reg]) {
        domain[v][reg] = false;
        domain_size[v]--;
        trail.push_back({v, reg});
    }
}

// ============================================================
// FUNGSI: ac3
// Propagasi Arc Consistency (AC-3).
//
// DEFINISI:
//   Untuk setiap arc (u, v), setiap y in dom(v) harus punya
//   support: ada x in dom(u) sedemikian x in adj_region[y].
//   Jika tidak ada => hapus y dari dom(v).
//
// Kompleksitas: O(N * K^2) per pass
// ============================================================
bool ac3() {
    while (!queue_empty()) {
        int u = queue_pop();
        for (int dir = 0; dir < 4; dir++) {
            int v = get_neighbor(u, dir);
            if (v == -1) continue;

            bool changed = false;
            for (int y = 0; y < K; y++) {
                if (!domain[v][y]) continue;

                // Cari support: ada x in adj_region[y] ∩ domain[u]?
                bool has_support = false;
                for (int x : adj_region[y]) {
                    if (domain[u][x]) { has_support = true; break; }
                }

                if (!has_support) {
                    remove_from_domain(v, y);
                    changed = true;
                    if (domain_size[v] == 0) return false; // kontradiksi
                }
            }
            if (changed) queue_push(v);
        }
    }
    return true;
}

// ============================================================
// FUNGSI: solve
// Backtracking dengan heuristik MRV (Minimum Remaining Values).
//
// MRV (Fail-First): Pilih vertex dengan domain terkecil > 1.
// Memaksimalkan kemungkinan menemukan kontradiksi lebih awal,
// sehingga memangkas pohon pencarian secara signifikan.
//
// UNDO MECHANISM:
//   Simpan posisi trail sebelum assignment.
//   Jika AC3 atau rekursi gagal, rollback ke checkpoint tersebut.
// ============================================================
bool solve() {
    // Cari vertex MRV
    int best = -1, best_size = K + 1;
    for (int i = 0; i < N; i++) {
        if (domain_size[i] > 1 && domain_size[i] < best_size) {
            best_size = domain_size[i]; best = i;
        }
    }
    if (best == -1) return true; // semua vertex fixed -> solusi!

    int u = best;
    vector<int> candidates;
    for (int k = 0; k < K; k++)
        if (domain[u][k]) candidates.push_back(k);

    for (int val : candidates) {
        int saved = (int)trail.size();

        // Paksakan domain[u] = {val}
        for (int k : candidates)
            if (k != val) remove_from_domain(u, k);

        queue_push(u);
        if (ac3() && solve()) return true;

        // Rollback trail
        while ((int)trail.size() > saved) {
            TrailEntry e = trail.back(); trail.pop_back();
            if (!domain[e.vertex][e.region]) {
                domain[e.vertex][e.region] = true;
                domain_size[e.vertex]++;
            }
        }
        queue_clear();
    }
    return false;
}

// ============================================================
// MAIN
// ============================================================
int main() {
    scanf("%d %d", &X, &Y);
    N = (X + 1) * (Y + 1);

    vector<int> Top(Y), Left(X), Right(X), Bottom(Y);
    for (int j = 0; j < Y; j++) scanf("%d", &Top[j]);
    for (int i = 0; i < X; i++) scanf("%d %d", &Left[i], &Right[i]);
    for (int j = 0; j < Y; j++) scanf("%d", &Bottom[j]);

    // ============================================================
    // FASE 1: PERIMETER SCAN -> BANGUN REGION TREE
    //
    // Tiap entry sequence: (label, vertex_r, vertex_c)
    // Posisi vertex di perimeter:
    //   Top[j]:    vertex (0,   j+1)  (sudut kanan-atas sel kolom j baris 0)
    //   Right[i]:  vertex (i+1, Y  )  (sudut kanan-bawah sel baris i kolom Y-1)
    //   Bottom[j]: vertex (X,   j  )  (sudut kiri-bawah sel kolom j baris X-1) [terbalik]
    //   Left[i]:   vertex (i,   0  )  (sudut kiri-atas sel baris i kolom 0)    [terbalik]
    // ============================================================
    int seq_len = 2 * X + 2 * Y;
    vector<int> seq(seq_len), vertex_r(seq_len), vertex_c(seq_len);
    int idx = 0;

    for (int j = 0; j < Y; j++) {
        seq[idx] = Top[j]; vertex_r[idx] = 0;   vertex_c[idx] = j+1; idx++;
    }
    for (int i = 0; i < X; i++) {
        seq[idx] = Right[i]; vertex_r[idx] = i+1; vertex_c[idx] = Y; idx++;
    }
    for (int j = Y-1; j >= 0; j--) {
        seq[idx] = Bottom[j]; vertex_r[idx] = X; vertex_c[idx] = j; idx++;
    }
    for (int i = X-1; i >= 0; i--) {
        seq[idx] = Left[i]; vertex_r[idx] = i; vertex_c[idx] = 0; idx++;
    }

    // ---- Stack parsing ----
    vector<vector<int>> region_of(X+1, vector<int>(Y+1, -1));
    K = 1;
    memset(parent_region, -1, sizeof(parent_region));
    memset(depth_region,   0, sizeof(depth_region));
    region_of[0][0] = 0;

    int cur_state = 0;
    bool valid = true;
    vector<int> stk_id, stk_state;

    for (int si = 0; si < seq_len && valid; si++) {
        int label = seq[si];
        if (!stk_id.empty() && stk_id.back() == label) {
            stk_id.pop_back(); stk_state.pop_back();
            cur_state = parent_region[cur_state]; // naik ke parent
        } else {
            int new_region = K++;
            parent_region[new_region] = cur_state;
            depth_region[new_region]  = depth_region[cur_state] + 1;
            stk_id.push_back(label);
            stk_state.push_back(new_region);
            cur_state = new_region; // masuk ke region baru
        }
        int r = vertex_r[si], c = vertex_c[si];
        if (region_of[r][c] != -1) {
            if (region_of[r][c] != cur_state) valid = false;
        } else {
            region_of[r][c] = cur_state;
        }
    }

    if (!valid || !stk_id.empty()) { printf("-1\n"); return 0; }

    // ---- Bangun adjacency list region tree ----
    for (int k = 1; k < K; k++) {
        int p = parent_region[k];
        adj_region[k].push_back(p);
        adj_region[p].push_back(k);
    }

    // ============================================================
    // FASE 2: INISIALISASI DOMAIN
    //
    // TEOREMA DEPTH PARITY: vertex (i,j) hanya bisa memiliki region
    // dengan kedalaman berparitas (i+j) mod 2.
    //
    // Vertex perimeter -> domain singleton
    // Vertex interior  -> domain = {k : depth[k] % 2 == (i+j) % 2}
    // ============================================================
    for (int i = 0; i <= X; i++) {
        for (int j = 0; j <= Y; j++) {
            int u = i * (Y + 1) + j;
            domain[u].assign(K, false);
            domain_size[u] = 0;

            if (region_of[i][j] != -1) {
                domain[u][region_of[i][j]] = true;
                domain_size[u] = 1;
            } else {
                int parity = (i + j) & 1;
                for (int k = 0; k < K; k++) {
                    if ((depth_region[k] & 1) == parity) {
                        domain[u][k] = true;
                        domain_size[u]++;
                    }
                }
                if (domain_size[u] == 0) { printf("-1\n"); return 0; }
            }
        }
    }

    // ============================================================
    // FASE 3: AC3 AWAL
    // Push semua vertex, propagasikan constraint ke seluruh grid.
    // ============================================================
    queue_clear();
    for (int u = 0; u < N; u++) queue_push(u);
    trail.clear();

    if (!ac3()) { printf("-1\n"); return 0; }

    // ============================================================
    // FASE 4: BACKTRACKING (jika AC3 belum cukup)
    // ============================================================
    if (!solve()) { printf("-1\n"); return 0; }

    // ============================================================
    // OUTPUT
    //
    // LOGIKA DECODING CERMIN:
    //   Sel (i,j): tl = vertex (i,j), br = vertex (i+1,j+1)
    //   Cermin '\' tidak memotong diagonal tl-br => tl dan br di region SAMA
    //   Cermin '/' memotong diagonal tl-br        => tl dan br di region BERBEDA
    //
    //   reg_tl == reg_br  =>  '\'
    //   reg_tl != reg_br  =>  '/'
    // ============================================================
    for (int i = 0; i < X; i++) {
        for (int j = 0; j < Y; j++) {
            int tl = i * (Y + 1) + j;
            int br = (i + 1) * (Y + 1) + (j + 1);

            int reg_tl = -1, reg_br = -1;
            for (int k = 0; k < K; k++) {
                if (domain[tl][k]) { reg_tl = k; break; }
            }
            for (int k = 0; k < K; k++) {
                if (domain[br][k]) { reg_br = k; break; }
            }

            printf("%c", reg_tl == reg_br ? '\\' : '/');
        }
        printf("\n");
    }

    return 0;
}
```

### 5.5 Analisis Kompleksitas

Misalkan $N = (X+1)(Y+1)$ = jumlah vertex, $K$ = jumlah region $\approx O(X+Y)$.

$$T_2 = \underbrace{O(X+Y)}_{\text{region tree}} + \underbrace{O(N \cdot K)}_{\text{init domain}} + \underbrace{O(B \cdot N \cdot K^2)}_{\text{AC3 total}} + \underbrace{O(K^N)}_{\text{backtrack worst-case}}$$

|Tahap|Kompleksitas Waktu|Kompleksitas Ruang|
|---|---|---|
|Perimeter scan & bangun region tree|$O(X + Y)$|$O(X + Y)$|
|Inisialisasi domain|$O(N \cdot K)$|$O(N \cdot K)$|
|AC3 satu pass|$O(N \cdot K^2)$|$O(N \cdot K)$|
|AC3 total selama backtracking|$O(B \cdot N \cdot K^2)$|$O(N \cdot K)$|
|Backtracking worst-case|$O(K^N)$|$O(N)$ untuk trail|
|**Total worst-case**|$O(K^N \cdot N \cdot K^2)$|$O(N \cdot K)$|

Untuk $X = Y = 100$: $N \approx 10{,}201$, $K \approx 200$. Worst-case teoritis sangat besar, namun dalam praktiknya depth parity memangkas domain hingga $\approx K/2$, dan AC3 biasanya menyelesaikan sebagian besar tanpa backtracking. Meski demikian, perbandingannya dengan Solusi 1 tetap tidak menguntungkan.

---

## 6 Perbandingan dan Analisis Dua Solusi

### 6.1 Tabel Komparatif

|Aspek|Solusi 1 (Greedy)|Solusi 2 (CSP + AC3)|
|---|---|---|
|**Paradigma**|Greedy deterministik|Search + Propagasi|
|**Pemanfaatan struktur problem**|Penuh (non-crossing → konstruksi langsung)|Parsial (depth parity saja)|
|**Perlu backtracking?**|Tidak|Ya (potentially)|
|**Kompleksitas waktu**|$O((X+Y) \cdot X \cdot Y)$|$O(K^N \cdot N \cdot K^2)$ worst-case|
|**Kompleksitas ruang**|$O(X \cdot Y)$|$O(N \cdot K) = O(X \cdot Y \cdot (X+Y))$|
|**Operasi untuk $X=Y=100$**|$\approx 2{,}000{,}000$|$\approx 400{,}000{,}000$ (AC3 satu pass saja)|
|**Deteksi `-1`**|$O(X+Y)$ — sangat cepat|Bisa lambat (exhaustive search)|
|**Dependensi library**|Tidak ada (pure C array)|`<vector>`, `<queue>` STL|
|**Panjang kode**|$\approx 200$ baris|$\approx 300$ baris|
|**Generalisabilitas**|Khusus problem ini|Mudah diadaptasi ke variasi|

### 6.2 Narasi Perbandingan

#### Eksploitasi Struktur Matematika

Perbedaan terbesar antara kedua solusi bukan pada teknik implementasinya, melainkan pada seberapa dalam mereka memahami _mengapa_ solusi ada.

Solusi 1 membuktikan dan memanfaatkan teorema kuat: **non-crossing matching adalah syarat perlu sekaligus cukup**, dan konstruksi greedy selalu berhasil jika kondisi ini terpenuhi. Akibatnya, masalah yang secara naif tampak sebagai _search problem_ berubah menjadi _construction problem_ deterministik.

Solusi 2 tidak memanfaatkan teorema ini. Ia hanya mengeksploitasi depth parity (separuh dari struktur masalah) dan menyerahkan sisanya kepada AC3 + backtracking — prosedur umum yang tidak mengetahui bahwa problem ini sebenarnya tidak memerlukan backtracking sama sekali.

#### Kompleksitas Praktis

Perbandingan kuantitatif untuk $X = Y = 100$:

$$T_1 \approx 200 \times 100 \times 100 = 2{,}000{,}000 \text{ operasi}$$

$$T_{\text{AC3 satu pass}} \approx N \cdot K^2 = 10{,}201 \times 200^2 \approx 408{,}000{,}000 \text{ operasi}$$

Solusi 1 lebih cepat $\approx 200\times$ bahkan hanya dibandingkan dengan satu pass AC3 saja. Dalam kompetisi dengan batas waktu 1–2 detik, Solusi 1 selesai dengan sangat aman, sementara Solusi 2 berpotensi TLE (Time Limit Exceeded).

Di samping itu, overhead memori dan _pointer-chasing_ pada `vector<bool>` dan STL queue di Solusi 2 juga tidak trivial dibandingkan array statis di Solusi 1.

#### Kapan Solusi 2 Lebih Relevan?

Solusi 2 (CSP) akan menjadi pilihan yang lebih tepat dalam skenario berikut:

- Problem memiliki constraint tambahan yang tidak bisa dimodelkan secara sederhana dengan greedy.
- Sifat non-crossing tidak berlaku (misalnya laser bisa bersilang di sel khusus pada variasi problem).
- Diperlukan enumerasi **semua** solusi yang valid, bukan hanya satu.
- Kode perlu mudah dimodifikasi untuk variasi problem yang berbeda.

Untuk JC15E seperti yang didefinisikan, Solusi 2 adalah solusi yang _correct_ namun _over-engineered_.

---

## 7 Kesimpulan

### 7.1 Pola Berpikir Sistematis dalam Memecahkan Grid Constraint Problem

Problem JC15E mengajarkan pola berpikir yang berlapis:

**Lapisan 1 — Kenali sifat topologis:** Apakah jalur-jalur bisa bersilang? Pada grid cermin, tidak. Ini langsung membuka pintu ke analisis non-crossing matching.

**Lapisan 2 — Tentukan syarat perlu DAN cukup:** Non-crossing matching adalah keduanya. Jika hanya syarat perlu yang diketahui, kita masih perlu search. Jika keduanya diketahui, kita bisa konstruksi langsung tanpa pencarian.

**Lapisan 3 — Pilih paradigma yang tepat:** Ketika konstruksi deterministik memungkinkan (Solusi 1), jangan gunakan search (Solusi 2). Sebaliknya, CSP/backtracking adalah alat yang tepat untuk constraint yang lebih umum dan kompleks.

### 7.2 Ringkasan Konsep Kunci

|Konsep|Rumus / Properti|Relevansi dalam Problem|
|---|---|---|
|Total port perimeter|$\|\mathcal{P}\| = 2X + 2Y$|Ukuran input yang harus diproses|
|Pantulan cermin `/`|$f_{/} = [1, 0, 3, 2]$|Lookup table $O(1)$|
|Pantulan cermin `\`|$f_{\backslash} = [3, 2, 1, 0]$|Lookup table $O(1)$|
|Non-crossing matching|$\nexists (a,b),(c,d): a < c < b < d$|**Syarat perlu dan cukup** untuk solusi|
|Bracket sequence|Stack parsing $O(X+Y)$|Verifikasi non-crossing yang efisien|
|Greedy tracing|Cermin "belok kanan" konsisten|Konstruksi deterministik jalur laser|
|Depth parity|$d_k \equiv (i+j) \pmod{2}$|Pembatasan domain vertex interior|
|Vertex indexing|$u = r(Y+1)+c$|Pemetaan 2D→1D untuk array vertex|
|Kompleksitas Solusi 1|$O((X+Y) \cdot X \cdot Y)$|$\approx 2 \times 10^6$ untuk $X=Y=100$|
|Kompleksitas AC3 satu pass|$O(N \cdot K^2)$|$\approx 4 \times 10^8$ untuk $X=Y=100$|

**Rekomendasi Akhir:** Untuk problem JC15E, **Solusi 1 adalah pilihan yang lebih optimal** — lebih cepat secara asimptotik, lebih sederhana dalam implementasi, dan secara konseptual lebih tepat karena memanfaatkan seluruh struktur matematika problem secara penuh.

---

## 8 Referensi

1. Cormen, T. H., Leiserson, C. E., Rivest, R. L., & Stein, C. (2009). _Introduction to Algorithms_ (3rd ed.). MIT Press. — Backtracking, Greedy, Dynamic Programming, CSP.
2. Mackworth, A. K. (1977). Consistency in networks of relations. _Artificial Intelligence_, 8(1), 99–118. — Fondasi Arc Consistency (AC3).
3. Golumbic, M. C. (2004). _Algorithmic Graph Theory and Perfect Graphs_ (2nd ed.). Elsevier. — Laminar family dan planar graph coloring.
4. West, D. B. (2001). _Introduction to Graph Theory_ (2nd ed.). Prentice Hall. — Jordan Curve Theorem dan planar matching.
5. SPOJ Problem Archive. _JC15E — Laser Beam 2.0_. https://www.spoj.com/
