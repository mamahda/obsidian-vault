Source: https://en.cppreference.com/cpp/container/deque

```cpp
template<
    class T,
    class Allocator = std::allocator<T>
> class deque;

namespace pmr {
    template< class T >
    using deque = std::deque<T, std::pmr::polymorphic_allocator<T>>;
}
```

`std::deque` (_double-ended queue_) adalah sebuah _indexed sequence container_ yang memungkinkan penyisipan (_insertion_) dan penghapusan (_deletion_) yang cepat di bagian awal maupun akhirnya. Selain itu, penyisipan dan penghapusan di kedua ujung _deque_ tidak pernah membatalkan (_invalidate_) _pointers_ atau _references_ ke elemen-elemen lainnya.

Berbeda dengan `std::vector`, elemen-elemen dari sebuah _deque_ tidak disimpan secara berdekatan (_contiguously_): implementasi tipikal menggunakan serangkaian _fixed-size arrays_ yang dialokasikan secara individual, dengan pembukuan (_bookkeeping_) tambahan. Ini berarti akses terindeks ke _deque_ harus melakukan dua dereferensi _pointer_, dibandingkan dengan akses terindeks pada _vector_ yang hanya melakukan satu.

Penyimpanan _deque_ diperluas dan disusutkan secara otomatis sesuai kebutuhan. Perluasan sebuah _deque_ lebih murah daripada perluasan `std::vector` karena tidak melibatkan penyalinan (_copying_) elemen-elemen yang ada ke lokasi memori baru. Di sisi lain, _deques_ umumnya memiliki biaya memori minimal yang besar; sebuah _deque_ yang hanya menampung satu elemen harus mengalokasikan _internal array_ secara penuh (misalnya 8 kali ukuran objek pada libstdc++ 64-bit; 16 kali ukuran objek atau 4096 bytes, mana yang lebih besar, pada libc++ 64-bit).

Kompleksitas (efisiensi) dari operasi umum pada _deques_ adalah sebagai berikut:

- Akses acak (_Random access_) - konstan O(1).
    
- Penyisipan atau penghapusan elemen di bagian akhir atau awal - konstan O(1).
    
- Penyisipan atau penghapusan elemen - linier O(n).
    

`std::deque` memenuhi persyaratan dari _Container_, _AllocatorAwareContainer_, _SequenceContainer_, dan _ReversibleContainer_.

### Parameter _Template_

- **`T`**: Tipe dari elemen yang disimpan.
    
- **`Allocator`**: Tipe _allocator_ yang digunakan untuk mengalokasikan memori dan mengonstruksi elemen.
    

### Pembatalan Iterator (_Iterator Invalidation_)

|**Operasi**|**Yang Dibatalkan (Invalidated)**|
|---|---|
|Semua operasi _read-only_.|Tidak pernah.|
|`swap`, `std::swap`|_Past-the-end iterator_ mungkin dibatalkan (tergantung implementasi / _implementation defined_).|
|`shrink_to_fit`, `clear`, `insert`,<br><br>  <br><br>`emplace`, `push_front`, `push_back`,<br><br>  <br><br>`emplace_front`, `emplace_back`|Selalu.|
|`erase`|Jika menghapus di awal (`begin`) - hanya elemen yang dihapus.<br><br>  <br><br>Jika menghapus di akhir (`end`) - hanya elemen yang dihapus dan _past-the-end iterator_.<br><br>  <br><br>Selain itu - semua _iterators_ dibatalkan.|
|`resize`|Jika ukuran baru lebih kecil dari ukuran lama - hanya elemen yang dihapus dan _past-the-end iterator_.<br><br>  <br><br>Jika ukuran baru lebih besar dari ukuran lama - semua _iterators_ dibatalkan.<br><br>  <br><br>Selain itu - tidak ada _iterators_ yang dibatalkan.|
|`pop_front`, `pop_back`|Elemen yang dihapus dan _past-the-end iterator_.|

**Catatan Pembatalan:**

- Saat menyisipkan di kedua ujung _deque_, _references_ tidak dibatalkan oleh `insert` dan `emplace`.
    
- `push_front`, `push_back`, `emplace_front` dan `emplace_back` tidak membatalkan _references_ apa pun ke elemen-elemen dari _deque_.
    
- Saat menghapus di kedua ujung _deque_, _references_ ke elemen yang tidak dihapus tidak dibatalkan oleh `erase`, `pop_front` dan `pop_back`.
    
- Pemanggilan `resize` dengan ukuran yang lebih kecil tidak membatalkan _references_ ke elemen yang tidak dihapus.
    
- Pemanggilan `resize` dengan ukuran yang lebih besar tidak membatalkan _references_ ke elemen-elemen dari _deque_.
    

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

- **(Konstruktor)**: Mengonstruksi `deque`.
    
- **(Destruktor)**: Menghancurkan `deque`.
    
- **`operator=`**: Menetapkan nilai ke _container_.
    
- **`assign`**: Menetapkan nilai ke _container_.
    
- **`assign_range`**: Menetapkan rentang elemen ke _container_ (C++23).
    
- **`get_allocator`**: Mengembalikan _allocator_ yang terkait.
    

**Akses Elemen (_Element access_)**

- **`at`**: Mengakses elemen yang ditentukan dengan pengecekan batas (_bounds checking_).
    
- **`operator[]`**: Mengakses elemen yang ditentukan.
    
- **`front`**: Mengakses elemen pertama.
    
- **`back`**: Mengakses elemen terakhir.
    

**Iterators**

- **`begin` / `cbegin`**: Mengembalikan _iterator_ ke awal.
    
- **`end` / `cend`**: Mengembalikan _iterator_ ke akhir.
    
- **`rbegin` / `crbegin`**: Mengembalikan _reverse iterator_ ke awal.
    
- **`rend` / `crend`**: Mengembalikan _reverse iterator_ ke akhir.
    

**Kapasitas (_Capacity_)**

- **`empty`**: Memeriksa apakah _container_ kosong.
    
- **`size`**: Mengembalikan jumlah elemen.
    
- **`max_size`**: Mengembalikan jumlah maksimum elemen yang dimungkinkan.
    
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
    
- **`push_front`**: Menambahkan elemen ke bagian awal.
    
- **`emplace_front`**: Mengonstruksi elemen di tempat pada bagian awal.
    
- **`prepend_range`**: Menambahkan rentang elemen ke bagian awal (C++23).
    
- **`pop_front`**: Menghapus elemen pertama.
    
- **`resize`**: Mengubah jumlah elemen yang disimpan.
    
- **`swap`**: Menukar isi.
    

### Fungsi _Non-member_

- **Operator Perbandingan**: Membandingkan isi dari dua `deque` secara leksikografis (`==`, `!=`, `<`, `<=`, `>`, `>=`, `<=>`).
    
- **`std::swap`** (terspesialisasi untuk `std::deque`): Menukar isi dari dua `deque`.
    
- **`std::erase` / `std::erase_if`**: Menghapus semua elemen yang memenuhi kriteria tertentu (C++20).
    

### Contoh Penggunaan

```cpp
#include <deque>
#include <iostream>

int main()
{
    // Membuat deque yang berisi integers
    std::deque<int> d = {7, 5, 16, 8};
    
    // Menambahkan sebuah integer ke bagian awal dan akhir dari deque
    d.push_front(13);
    d.push_back(25);
    
    // Melakukan iterasi dan mencetak nilai-nilai deque
    for (int n : d)
        std::cout << n << ' ';
    std::cout << '\n';
}
```

**Output:**

```
13 7 5 16 8 25
```