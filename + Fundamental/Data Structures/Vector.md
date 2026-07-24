Source: https://en.cppreference.com/cpp/container/vector

```cpp
template<
    class T,
    class Allocator = std::allocator<T>
> class vector;

namespace pmr {
    template< class T >
    using vector = std::vector<T, std::pmr::polymorphic_allocator<T>>;
}
```

`std::vector` adalah sebuah _sequence container_ yang merangkum _array_ dengan ukuran dinamis (_dynamic size arrays_).

`std::pmr::vector` adalah sebuah _alias template_ yang menggunakan _polymorphic allocator_.

Elemen-elemen disimpan secara berdekatan (_contiguously_), yang berarti elemen tidak hanya dapat diakses melalui _iterators_, tetapi juga menggunakan _offsets_ pada _regular pointers_ ke elemen. Hal ini berarti bahwa _pointer_ ke suatu elemen dari sebuah _vector_ dapat diteruskan ke fungsi apa pun yang mengharapkan _pointer_ ke elemen dari sebuah _array_.

Penyimpanan _vector_ ditangani secara otomatis dan diperluas sesuai kebutuhan. _Vectors_ biasanya menempati lebih banyak ruang daripada _static arrays_, karena lebih banyak memori dialokasikan untuk menangani pertumbuhan di masa depan. Dengan cara ini, sebuah _vector_ tidak perlu melakukan realokasi (_reallocate_) setiap kali sebuah elemen disisipkan, tetapi hanya ketika memori tambahan telah habis. Total jumlah memori yang dialokasikan dapat diketahui menggunakan fungsi `capacity()`. Memori ekstra dapat dikembalikan ke sistem melalui pemanggilan fungsi `shrink_to_fit()`.

Realokasi biasanya merupakan operasi yang mahal dalam hal performa. Fungsi `reserve()` dapat digunakan untuk mengeliminasi realokasi jika jumlah elemen sudah diketahui sebelumnya.

Kompleksitas (efisiensi) dari operasi umum pada _vectors_ adalah sebagai berikut:

- Akses acak (_Random access_) - konstan $O(1)$.
    
- Penyisipan atau penghapusan elemen di bagian akhir - konstan diamortisasi (_amortized constant_) $O(1)$.
    
- Penyisipan atau penghapusan elemen - linier sebanding dengan jarak ke akhir _vector_ $O(n)$.
    

### Parameter _Template_

- **`T`**: Tipe dari elemen yang disimpan.
    
- **`Allocator`**: Tipe _allocator_ yang digunakan untuk mengalokasikan memori dan mengonstruksi elemen.
    

### Spesialisasi (_Specializations_)

_Standard library_ menyediakan spesialisasi dari `std::vector` untuk tipe `bool`, yang mungkin dioptimalkan untuk efisiensi ruang (_space efficiency_).

- **`std::vector<bool>`**: Spesialisasi hemat ruang untuk _boolean_.
    

### Pembatalan Iterator (_Iterator invalidation_)

|**Operasi**|**Yang Dibatalkan (Invalidated)**|
|---|---|
|Semua operasi _read-only_|Tidak pernah.|
|`swap`, `std::swap`|`end()`|
|`clear`, `operator=`, `assign`|Selalu.|
|`reserve`, `shrink_to_fit`|Jika _vector_ mengubah kapasitas, semuanya. Jika tidak, tidak ada.|
|`erase`|Elemen yang dihapus dan semua elemen setelahnya (termasuk `end()`).|
|`push_back`, `emplace_back`|Jika _vector_ mengubah kapasitas, semuanya. Jika tidak, hanya `end()`.|
|`insert`, `emplace`|Jika _vector_ mengubah kapasitas, semuanya.<br><br>  <br><br>Jika tidak, hanya elemen pada atau setelah titik penyisipan (termasuk `end()`).|
|`resize`|Jika _vector_ mengubah kapasitas, semuanya. Jika tidak, hanya `end()` dan elemen apa pun yang dihapus.|
|`pop_back`|Elemen yang dihapus dan `end()`.|

### _Member Types_ (Tipe Anggota)

|**Member type**|**Definisi**|
|---|---|
|`value_type`|`T`|
|`allocator_type`|`Allocator`|
|`size_type`|_Unsigned integer type_ (biasanya `std::size_t`)|
|`difference_type`|_Signed integer type_ (biasanya `std::ptrdiff_t`)|
|`reference`|`value_type&`|
|`const_reference`|`const value_type&`|
|`pointer`|_Pointer_ ke elemen|
|`const_pointer`|_Pointer_ konstan ke elemen|
|`iterator`|_RandomAccessIterator_|
|`const_iterator`|_Constant RandomAccessIterator_|
|`reverse_iterator`|`std::reverse_iterator<iterator>`|
|`const_reverse_iterator`|`std::reverse_iterator<const_iterator>`|

### _Member Functions_ (Fungsi Anggota)

- **(Konstruktor)**: Mengonstruksi `vector`.
    
- **(Destruktor)**: Menghancurkan `vector`.
    
- **`operator=`**: Menetapkan nilai ke _container_.
    
- **`assign`**: Menetapkan nilai ke _container_.
    
- **`assign_range`**: Menetapkan rentang elemen ke _container_ (C++23).
    
- **`get_allocator`**: Mengembalikan _allocator_ yang terkait.
    

**Akses Elemen (_Element access_)**

- **`at`**: Mengakses elemen yang ditentukan dengan pengecekan batas (_bounds checking_).
    
- **`operator[]`**: Mengakses elemen yang ditentukan.
    
- **`front`**: Mengakses elemen pertama.
    
- **`back`**: Mengakses elemen terakhir.
    
- **`data`**: Akses langsung ke _underlying array_.
    

**Iterators**

- **`begin` / `cbegin`**: Mengembalikan _iterator_ ke awal.
    
- **`end` / `cend`**: Mengembalikan _iterator_ ke akhir.
    
- **`rbegin` / `crbegin`**: Mengembalikan _reverse iterator_ ke awal.
    
- **`rend` / `crend`**: Mengembalikan _reverse iterator_ ke akhir.
    

**Kapasitas (_Capacity_)**

- **`empty`**: Memeriksa apakah _container_ kosong.
    
- **`size`**: Mengembalikan jumlah elemen.
    
- **`max_size`**: Mengembalikan jumlah maksimum elemen yang dimungkinkan.
    
- **`reserve`**: Memesan ruang penyimpanan (mengubah _capacity_).
    
- **`capacity`**: Mengembalikan jumlah elemen yang dapat ditampung saat ini dalam ruang yang dialokasikan.
    
- **`shrink_to_fit`**: Mengurangi penggunaan memori dengan membebaskan ruang yang tidak terpakai.
    

**Modifikator (_Modifiers_)**

- **`clear`**: Menghapus semua elemen.
    
- **`insert`**: Menyisipkan (_insert_) elemen.
    
- **`insert_range`**: Menyisipkan rentang elemen (C++23).
    
- **`emplace`**: Mengonstruksi elemen di tempat (_in-place_).
    
- **`erase`**: Menghapus elemen.
    
- **`push_back`**: Menambahkan elemen ke bagian akhir.
    
- **`emplace_back`**: Mengonstruksi elemen di tempat pada bagian akhir.
    
- **`append_range`**: Menambahkan rentang elemen ke bagian akhir (C++23).
    
- **`pop_back`**: Menghapus elemen terakhir.
    
- **`resize`**: Mengubah jumlah elemen yang disimpan.
    
- **`swap`**: Menukar isi.
    

### Fungsi _Non-member_

- **Operator Perbandingan**: Membandingkan isi dari dua `vector` secara leksikografis (`==`, `!=`, `<`, `<=`, `>`, `>=`, `<=>`).
    
- **`std::swap`** (terspesialisasi untuk `std::vector`): Menukar isi dari dua `vector`.
    
- **`std::erase` / `std::erase_if`**: Menghapus semua elemen yang memenuhi kriteria tertentu (C++20).
    

### Contoh Penggunaan

```cpp
#include <iostream>
#include <vector>

int main()
{
    // Membuat vector yang berisi integers
    std::vector<int> v = {8, 4, 5, 9};
 
    // Menambahkan dua integer lagi ke vector
    v.push_back(6);
    v.push_back(9);
    
    // Menimpa elemen pada posisi indeks 2
    v[2] = -1;
 
    // Mencetak isi vector
    for (int n : v)
        std::cout << n << ' ';
    std::cout << '\n';
}
```

**Output:**

```
8 4 -1 9 6 9
```
