Source: https://en.cppreference.com/cpp/container/map

```cpp
template<
    class Key,
    class T,
    class Compare = std::less<Key>,
    class Allocator = std::allocator<std::pair<const Key, T>>
> class map;

namespace pmr {
    template<
        class Key,
        class T,
        class Compare = std::less<Key>
    > using map = std::map<Key, T, Compare,
                           std::pmr::polymorphic_allocator<std::pair<const Key, T>>>;
}
```

`std::map` adalah sebuah _sorted associative container_ yang berisi pasangan _key-value_ dengan _keys_ (kunci) yang unik. _Keys_ diurutkan menggunakan fungsi perbandingan `Compare`. Operasi pencarian, penghapusan, dan penyisipan memiliki kompleksitas logaritmik. _Maps_ biasanya diimplementasikan sebagai _Red-black trees_.

_Iterators_ dari `std::map` beriterasi dalam urutan _ascending_ (menaik) berdasarkan _keys_, di mana _ascending_ didefinisikan oleh perbandingan yang digunakan saat konstruksi. Artinya, jika diberikan:

- `m`, sebuah `std::map`
    
- `it_l` dan `it_r`, _iterators_ yang dapat didereferensi (_dereferenceable iterators_) ke `m`, dengan `it_l < it_r`.
    
    Maka `m.value_comp()(*it_l, *it_r) == true` (dari yang terkecil ke terbesar jika menggunakan perbandingan bawaan).
    

Di mana pun _standard library_ menggunakan persyaratan _Compare_, keunikan ditentukan dengan menggunakan relasi ekuivalensi (_equivalence relation_). Secara tidak baku, dua objek `a` dan `b` dianggap ekuivalen (tidak unik) jika tidak ada satu pun yang dianggap lebih kecil dari yang lain: `!comp(a, b) && !comp(b, a)`.

`std::map` memenuhi persyaratan dari _Container_, _AllocatorAwareContainer_, _AssociativeContainer_, dan _ReversibleContainer_.

### Parameter _Template_

- **`Key`**: Tipe dari _keys_ yang diurutkan.
    
- **`T`**: Tipe dari _mapped value_.
    
- **`Compare`**: Tipe _Compare_ yang menyediakan _strict weak ordering_ untuk _keys_.
    
- **`Allocator`**: Tipe _allocator_ yang digunakan untuk mengalokasikan memori pasangan _key-value_.
    

### _Member Types_ (Tipe Anggota)

|**Member type**|**Definisi**|
|---|---|
|`key_type`|`Key`|
|`mapped_type`|`T`|
|`value_type`|`std::pair<const Key, T>`|
|`size_type`|_Unsigned integer type_ (biasanya `std::size_t`)|
|`difference_type`|_Signed integer type_ (biasanya `std::ptrdiff_t`)|
|`key_compare`|`Compare`|
|`allocator_type`|`Allocator`|
|`reference`|`value_type&`|
|`const_reference`|`const value_type&`|
|`pointer`|_Pointer_ ke `value_type`|
|`const_pointer`|_Pointer_ konstan ke `value_type`|
|`iterator`|_BidirectionalIterator_|
|`const_iterator`|_Constant BidirectionalIterator_|
|`reverse_iterator`|`std::reverse_iterator<iterator>`|
|`const_reverse_iterator`|`std::reverse_iterator<const_iterator>`|
|`node_type`|_Node handle_ spesifik untuk _container_ ini|
|`insert_return_type`|Tipe yang dikembalikan oleh operasi _insert_ tertentu|

### _Member Classes_ (Kelas Anggota)

- **`value_compare`**: Membandingkan objek tipe `value_type` (pasangan _key-value_) menggunakan perbandingan _keys_.
    

### _Member Functions_ (Fungsi Anggota)

- **(Konstruktor)**: Mengonstruksi `map`.
    
- **(Destruktor)**: Menghancurkan `map`.
    
- **`operator=`**: Menetapkan nilai ke _container_.
    
- **`get_allocator`**: Mengembalikan _allocator_ yang terkait.
    

**Akses Elemen (_Element access_)**

- **`at`**: Mengakses elemen yang ditentukan dengan pengecekan batas (_bounds checking_).
    
- **`operator[]`**: Mengakses atau menyisipkan elemen yang ditentukan.
    

**Iterators**

- **`begin` / `cbegin`**: Mengembalikan _iterator_ ke awal.
    
- **`end` / `cend`**: Mengembalikan _iterator_ ke akhir.
    
- **`rbegin` / `crbegin`**: Mengembalikan _reverse iterator_ ke awal.
    
- **`rend` / `crend`**: Mengembalikan _reverse iterator_ ke akhir.
    

**Kapasitas (_Capacity_)**

- **`empty`**: Memeriksa apakah _container_ kosong.
    
- **`size`**: Mengembalikan jumlah elemen.
    
- **`max_size`**: Mengembalikan jumlah maksimum elemen yang dimungkinkan.
    

**Modifikator (_Modifiers_)**

- **`clear`**: Menghapus semua elemen.
    
- **`insert`**: Menyisipkan (_insert_) elemen atau _nodes_ (diekstraksi dari _container_ lain).
    
- **`insert_range`**: Menyisipkan rentang elemen (C++23).
    
- **`insert_or_assign`**: Menyisipkan elemen atau menetapkan nilai ke elemen yang sudah ada jika _key_ tersebut sudah ada (C++17).
    
- **`emplace`**: Mengonstruksi elemen di tempat (_in-place_).
    
- **`emplace_hint`**: Mengonstruksi elemen di tempat menggunakan sebuah petunjuk posisi (_hint_).
    
- **`try_emplace`**: Menyisipkan elemen di tempat jika _key_ belum ada, dan tidak melakukan apa-apa jika sudah ada (C++17).
    
- **`erase`**: Menghapus elemen.
    
- **`swap`**: Menukar isi.
    
- **`extract`**: Mengekstrak _node_ dari _container_ (C++17).
    
- **`merge`**: Menggabungkan _nodes_ dari _container_ lain (C++17).
    

**Pencarian (_Lookup_)**

- **`count`**: Mengembalikan jumlah elemen yang cocok dengan _key_ tertentu.
    
- **`find`**: Menemukan elemen dengan _key_ tertentu.
    
- **`contains`**: Memeriksa apakah _container_ memiliki elemen dengan _key_ tertentu (C++20).
    
- **`equal_range`**: Mengembalikan rentang elemen yang cocok dengan _key_ tertentu.
    
- **`lower_bound`**: Mengembalikan _iterator_ ke elemen pertama yang tidak kurang dari (>=) _key_ yang diberikan.
    
- **`upper_bound`**: Mengembalikan _iterator_ ke elemen pertama yang lebih besar dari (>) _key_ yang diberikan.
    

**Pengamat (_Observers_)**

- **`key_comp`**: Mengembalikan fungsi yang membandingkan _keys_.
    
- **`value_comp`**: Mengembalikan fungsi yang membandingkan _keys_ dalam objek `value_type`.
    

### Fungsi _Non-member_

- **Operator Perbandingan**: Membandingkan isi dari dua `map` secara leksikografis (`==`, `!=`, `<`, `<=`, `>`, `>=`, `<=>`).
    
- **`std::swap`** (terspesialisasi untuk `std::map`): Menukar isi dari dua `map`.
    
- **`std::erase_if`**: Menghapus semua elemen yang memenuhi kriteria tertentu (C++20).
    

### Contoh Penggunaan


```cpp
#include <iostream>
#include <map>
#include <string>
#include <string_view>

void print_map(std::string_view comment, const std::map<std::string, int>& m)
{
    std::cout << comment;
    // Iterasi menggunakan fitur C++17
    for (const auto& [key, value] : m)
        std::cout << '[' << key << "] = " << value << "; ";
    
// Alternatif C++11:
//  for (const auto& n : m)
//      std::cout << n.first << " = " << n.second << "; ";
//
// Alternatif C++98:
//  for (std::map<std::string, int>::const_iterator it = m.begin(); it != m.end(); ++it)
//      std::cout << it->first << " = " << it->second << "; ";
    
    std::cout << '\n';
}

int main()
{
    // Membuat sebuah map berisi tiga pasangan (string, int)
    std::map<std::string, int> m{{"CPU", 10}, {"GPU", 15}, {"RAM", 20}};

    print_map("1) Initial map: ", m);

    m["CPU"] = 25; // memperbarui nilai yang sudah ada
    m["SSD"] = 30; // menyisipkan nilai baru
    print_map("2) Updated map: ", m);

    // Menggunakan operator[] dengan key yang tidak ada akan selalu melakukan penyisipan (insert)
    std::cout << "3) m[UPS] = " << m["UPS"] << '\n';
    print_map("4) Updated map: ", m);

    m.erase("GPU");
    print_map("5) After erase: ", m);

    std::erase_if(m, [](const auto& pair){ return pair.second > 25; });
    print_map("6) After erase: ", m);
    std::cout << "7) m.size() = " << m.size() << '\n';

    m.clear();
    std::cout << std::boolalpha << "8) Map is empty: " << m.empty() << '\n';
}
```

**Output:**

```
1) Initial map: [CPU] = 10; [GPU] = 15; [RAM] = 20; 
2) Updated map: [CPU] = 25; [GPU] = 15; [RAM] = 20; [SSD] = 30; 
3) m[UPS] = 0
4) Updated map: [CPU] = 25; [GPU] = 15; [RAM] = 20; [SSD] = 30; [UPS] = 0; 
5) After erase: [CPU] = 25; [RAM] = 20; [SSD] = 30; [UPS] = 0; 
6) After erase: [CPU] = 25; [RAM] = 20; [UPS] = 0; 
7) m.size() = 3
8) Map is empty: true
```