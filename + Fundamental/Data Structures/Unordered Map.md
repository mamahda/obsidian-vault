Source: https://en.cppreference.com/cpp/container/unordered_map

```cpp
template<
    class Key,
    class T,
    class Hash = std::hash<Key>,
    class KeyEqual = std::equal_to<Key>,
    class Allocator = std::allocator<std::pair<const Key, T>>
> class unordered_map;

namespace pmr {
    template<
        class Key,
        class T,
        class Hash = std::hash<Key>,
        class KeyEqual = std::equal_to<Key>
    > using unordered_map =
          std::unordered_map<Key, T, Hash, KeyEqual,
              std::pmr::polymorphic_allocator<std::pair<const Key, T>>>;
}
```

`std::unordered_map` adalah sebuah _associative container_ yang berisi pasangan _key-value_ dengan _keys_ (kunci) yang unik. Operasi pencarian (_search_), penyisipan (_insertion_), dan penghapusan (_removal_) elemen memiliki rata-rata kompleksitas waktu konstan (_average constant-time complexity_).

Secara internal, elemen-elemen tidak diurutkan dalam urutan tertentu, melainkan diorganisasikan ke dalam _buckets_. _Bucket_ mana yang akan ditempati oleh suatu elemen bergantung sepenuhnya pada nilai _hash_ dari _key_-nya. _Keys_ dengan kode _hash_ yang sama akan muncul di _bucket_ yang sama. Hal ini memungkinkan akses cepat ke elemen individual, karena setelah _hash_ dihitung, ia akan langsung merujuk ke _bucket_ yang menampung elemen tersebut.

Dua _keys_ dianggap _ekuivalen_ jika predikat kesamaan kunci (_key equality predicate_) dari _map_ mengembalikan nilai `true` saat diberikan kedua _keys_ tersebut. Jika dua _keys_ ekuivalen, fungsi _hash_ harus mengembalikan nilai yang sama untuk kedua _keys_ tersebut.

`std::unordered_map` memenuhi persyaratan dari _Container_, _AllocatorAwareContainer_, dan _UnorderedAssociativeContainer_.

### Pembatalan Iterator (_Iterator Invalidation_)

|**Operasi**|**Yang Dibatalkan (Invalidated)**|
|---|---|
|Semua operasi _read-only_, `swap`, `std::swap`|Tidak pernah (_Never_)|
|`clear`, `rehash`, `reserve`, `operator=`|Selalu (_Always_)|
|`insert`, `emplace`, `emplace_hint`, `operator[]`|Hanya jika menyebabkan _rehash_|
|`erase`|Hanya pada elemen yang dihapus|

**Catatan:**

- Fungsi `swap` tidak membatalkan _iterators_ apa pun di dalam _container_, tetapi membatalkan _iterator_ yang menandai akhir dari wilayah pertukaran (_swap region_).
    
- _References_ dan _pointers_ ke _key_ atau data yang disimpan dalam _container_ hanya dibatalkan saat elemen tersebut dihapus (_erased_), bahkan ketika _iterator_ yang sesuai dibatalkan.
    

### Parameter _Template_

- **`Key`**: Tipe dari _keys_ yang disimpan.
    
- **`T`**: Tipe dari _mapped value_.
    
- **`Hash`**: Fungsi _hash_ yang digunakan untuk menghitung nilai _hash_ dari _keys_.
    
- **`KeyEqual`**: Fungsi yang memeriksa kesetaraan (_equality_) dua _keys_.
    
- **`Allocator`**: Tipe _allocator_ yang digunakan untuk mengalokasikan memori pasangan _key-value_.
    

### _Member Types_ (Tipe Anggota)

|**Member type**|**Definisi**|
|---|---|
|`key_type`|`Key`|
|`mapped_type`|`T`|
|`value_type`|`std::pair<const Key, T>`|
|`size_type`|_Unsigned integer type_ (biasanya `std::size_t`)|
|`difference_type`|_Signed integer type_ (biasanya `std::ptrdiff_t`)|
|`hasher`|`Hash`|
|`key_equal`|`KeyEqual`|
|`allocator_type`|`Allocator`|
|`reference`|`value_type&`|
|`const_reference`|`const value_type&`|
|`pointer`|_Pointer_ ke `value_type`|
|`const_pointer`|_Pointer_ konstan ke `value_type`|
|`iterator`|_ForwardIterator_|
|`const_iterator`|_Constant ForwardIterator_|
|`local_iterator`|_ForwardIterator_ yang iterasi di dalam satu _bucket_|
|`const_local_iterator`|_Constant ForwardIterator_ yang iterasi di dalam satu _bucket_|
|`node_type`|_Node handle_ spesifik untuk _container_ ini|
|`insert_return_type`|Tipe yang dikembalikan oleh operasi _insert_ tertentu|

### _Member Functions_ (Fungsi Anggota)

- **(Konstruktor)**: Mengonstruksi `unordered_map`.
    
- **(Destruktor)**: Menghancurkan `unordered_map`.
    
- **`operator=`**: Menetapkan nilai ke _container_.
    
- **`get_allocator`**: Mengembalikan _allocator_ yang terkait.
    

**Iterators**

- **`begin` / `cbegin`**: Mengembalikan _iterator_ ke awal.
    
- **`end` / `cend`**: Mengembalikan _iterator_ ke akhir.
    

**Kapasitas (_Capacity_)**

- **`empty`**: Memeriksa apakah _container_ kosong.
    
- **`size`**: Mengembalikan jumlah elemen.
    
- **`max_size`**: Mengembalikan jumlah maksimum elemen yang dimungkinkan.
    

**Modifikator (_Modifiers_)**

- **`clear`**: Menghapus semua elemen.
    
- **`insert`**: Menyisipkan (_insert_) elemen atau _nodes_.
    
- **`insert_range`**: Menyisipkan rentang elemen (C++23).
    
- **`insert_or_assign`**: Menyisipkan elemen atau menetapkan nilai ke elemen yang sudah ada jika _key_ tersebut sudah ada (C++17).
    
- **`emplace`**: Mengonstruksi elemen di tempat (_in-place_).
    
- **`emplace_hint`**: Mengonstruksi elemen di tempat menggunakan sebuah petunjuk posisi (_hint_).
    
- **`try_emplace`**: Menyisipkan elemen di tempat jika _key_ belum ada (C++17).
    
- **`erase`**: Menghapus elemen.
    
- **`swap`**: Menukar isi.
    
- **`extract`**: Mengekstrak _node_ dari _container_ (C++17).
    
- **`merge`**: Menggabungkan _nodes_ dari _container_ lain (C++17).
    

**Pencarian (_Lookup_)**

- **`at`**: Mengakses elemen yang ditentukan dengan pengecekan batas (_bounds checking_).
    
- **`operator[]`**: Mengakses atau menyisipkan elemen yang ditentukan.
    
- **`count`**: Mengembalikan jumlah elemen yang cocok dengan _key_ tertentu (selalu 1 atau 0 untuk `unordered_map`).
    
- **`find`**: Menemukan elemen dengan _key_ tertentu.
    
- **`contains`**: Memeriksa apakah _container_ memiliki elemen dengan _key_ tertentu (C++20).
    
- **`equal_range`**: Mengembalikan rentang elemen yang cocok dengan _key_ tertentu.
    

**Antarmuka Bucket (_Bucket interface_)**

- **`begin(int)` / `cbegin(int)`**: Mengembalikan _iterator_ lokal ke awal _bucket_ yang ditentukan.
    
- **`end(int)` / `cend(int)`**: Mengembalikan _iterator_ lokal ke akhir _bucket_ yang ditentukan.
    
- **`bucket_count`**: Mengembalikan jumlah _buckets_.
    
- **`max_bucket_count`**: Mengembalikan jumlah maksimum _buckets_ yang dimungkinkan.
    
- **`bucket_size`**: Mengembalikan jumlah elemen dalam _bucket_ tertentu.
    
- **`bucket`**: Mengembalikan indeks _bucket_ untuk _key_ tertentu.
    

**Kebijakan Hash (_Hash policy_)**

- **`load_factor`**: Mengembalikan rasio jumlah elemen per _bucket_ saat ini.
    
- **`max_load_factor`**: Mengelola rasio elemen per _bucket_ maksimum (ambang batas untuk memicu _rehash_ otomatis).
    
- **`rehash`**: Memesan setidaknya jumlah _buckets_ yang ditentukan dan meregenerasi _hash table_.
    
- **`reserve`**: Memesan ruang untuk setidaknya elemen sejumlah yang ditentukan dan meregenerasi _hash table_.
    

**Pengamat (_Observers_)**

- **`hash_function`**: Mengembalikan fungsi _hash_ yang digunakan.
    
- **`key_eq`**: Mengembalikan fungsi perbandingan _keys_ yang digunakan.
    

### Fungsi _Non-member_

- **Operator Perbandingan**: Membandingkan isi dari dua `unordered_map` (`==`, `!=`).
    
- **`std::swap`** (terspesialisasi untuk `std::unordered_map`): Menukar isi dari dua `unordered_map`.
    
- **`std::erase_if`**: Menghapus semua elemen yang memenuhi kriteria tertentu (C++20).
    

### Contoh Penggunaan



```cpp
#include <iostream>
#include <string>
#include <unordered_map>

int main()
{
    // Membuat unordered_map berisi tiga strings (yang memetakan ke strings)
    std::unordered_map<std::string, std::string> u =
    {
        {"RED", "#FF0000"},
        {"GREEN", "#00FF00"},
        {"BLUE", "#0000FF"}
    };
    
    // Fungsi lambda pembantu untuk mencetak pasangan key-value
    auto print_key_value = [](const auto& key, const auto& value)
    {
        std::cout << "Key:[" << key << "] Value:[" << value << "]\n";
    };
    
    std::cout << "Iterasi dan cetak pasangan key-value dari unordered_map, "
                 "secara eksplisit dengan tipenya:\n";
    for (const std::pair<const std::string, std::string>& n : u)
        print_key_value(n.first, n.second);
    
    std::cout << "\nIterasi dan cetak pasangan key-value menggunakan structured binding C++17:\n";
    for (const auto& [key, value] : u)
        print_key_value(key, value);
    
    // Menambahkan dua entri baru ke unordered_map
    u["BLACK"] = "#000000";
    u["WHITE"] = "#FFFFFF";
    
    std::cout << "\nOutput nilai berdasarkan key:\n"
                 "Kode HEX dari warna RED adalah:[" << u["RED"] << "]\n"
                 "Kode HEX dari warna BLACK adalah:[" << u["BLACK"] << "]\n\n";
    
    std::cout << "Gunakan operator[] dengan key yang tidak ada untuk menyisipkan pasangan baru:\n";
    print_key_value("new_key", u["new_key"]);
    
    std::cout << "\nIterasi dan cetak pasangan key-value, menggunakan `auto`;\n"
                 "new_key sekarang menjadi salah satu key di dalam map:\n";
    for (const auto& n : u)
        print_key_value(n.first, n.second);
}
```

**Output:**

```
Iterasi dan cetak pasangan key-value dari unordered_map, secara eksplisit dengan tipenya:
Key:[BLUE] Value:[#0000FF]
Key:[GREEN] Value:[#00FF00]
Key:[RED] Value:[#FF0000]

Iterasi dan cetak pasangan key-value menggunakan structured binding C++17:
Key:[BLUE] Value:[#0000FF]
Key:[GREEN] Value:[#00FF00]
Key:[RED] Value:[#FF0000]

Output nilai berdasarkan key:
Kode HEX dari warna RED adalah:[#FF0000]
Kode HEX dari warna BLACK adalah:[#000000]

Gunakan operator[] dengan key yang tidak ada untuk menyisipkan pasangan baru:
Key:[new_key] Value:[]

Iterasi dan cetak pasangan key-value, menggunakan `auto`;
new_key sekarang menjadi salah satu key di dalam map:
Key:[new_key] Value:[]
Key:[WHITE] Value:[#FFFFFF]
Key:[BLACK] Value:[#000000]
Key:[BLUE] Value:[#0000FF]
Key:[GREEN] Value:[#00FF00]
Key:[RED] Value:[#FF0000]
```