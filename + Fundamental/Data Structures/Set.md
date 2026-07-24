Source: https://en.cppreference.com/cpp/container/set

```cpp
template<
    class Key,
    class Compare = std::less<Key>,
    class Allocator = std::allocator<Key>
> class set;

namespace pmr {
    template<
        class Key,
        class Compare = std::less<Key>
    > using set = std::set<Key, Compare, std::pmr::polymorphic_allocator<Key>>;
}
```

`std::set` adalah sebuah _associative container_ yang berisi sekumpulan objek unik bertipe `Key` yang diurutkan (_sorted set_). Pengurutan dilakukan menggunakan fungsi perbandingan kunci (_key comparison function_) `Compare`. Operasi pencarian, penghapusan, dan penyisipan memiliki kompleksitas logaritmik. _Sets_ biasanya diimplementasikan sebagai _Red-black trees_.

Di mana pun _standard library_ menggunakan persyaratan `Compare`, keunikan ditentukan dengan menggunakan relasi ekuivalensi (_equivalence relation_). Secara tidak baku, dua objek `a` dan `b` dianggap ekuivalen (berarti nilai yang sama) jika tidak ada satu pun yang dianggap lebih kecil dari yang lain: `!comp(a, b) && !comp(b, a)`.

`std::set` memenuhi persyaratan dari _Container_, _AllocatorAwareContainer_, _AssociativeContainer_, dan _ReversibleContainer_.

### Parameter _Template_

- **`Key`**: Tipe dari elemen yang disimpan (_keys_).
    
- **`Compare`**: Tipe _Compare_ yang menyediakan _strict weak ordering_ untuk _keys_.
    
- **`Allocator`**: Tipe _allocator_ yang digunakan untuk mengalokasikan memori.
    

### _Member Types_ (Tipe Anggota)

|**Member type**|**Definisi**|
|---|---|
|`key_type`|`Key`|
|`value_type`|`Key`|
|`size_type`|_Unsigned integer type_ (biasanya `std::size_t`)|
|`difference_type`|_Signed integer type_ (biasanya `std::ptrdiff_t`)|
|`key_compare`|`Compare`|
|`value_compare`|`Compare`|
|`allocator_type`|`Allocator`|
|`reference`|`value_type&`|
|`const_reference`|`const value_type&`|
|`pointer`|_Pointer_ ke `value_type`|
|`const_pointer`|_Pointer_ konstan ke `value_type`|
|`iterator`|_Constant BidirectionalIterator_|
|`const_iterator`|_Constant BidirectionalIterator_|
|`reverse_iterator`|`std::reverse_iterator<iterator>`|
|`const_reverse_iterator`|`std::reverse_iterator<const_iterator>`|
|`node_type`|_Node handle_ spesifik untuk _container_ ini|
|`insert_return_type`|Tipe yang dikembalikan oleh operasi _insert_ tertentu|

### _Member Functions_ (Fungsi Anggota)

- **(Konstruktor)**: Mengonstruksi `set`.
    
- **(Destruktor)**: Menghancurkan `set`.
    
- **`operator=`**: Menetapkan nilai ke _container_.
    
- **`get_allocator`**: Mengembalikan _allocator_ yang terkait.
    

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
    
- **`emplace`**: Mengonstruksi elemen di tempat (_in-place_).
    
- **`emplace_hint`**: Mengonstruksi elemen di tempat menggunakan sebuah petunjuk posisi (_hint_).
    
- **`erase`**: Menghapus elemen.
    
- **`swap`**: Menukar isi.
    
- **`extract`**: Mengekstrak _node_ dari _container_ (C++17).
    
- **`merge`**: Menggabungkan _nodes_ dari _container_ lain (C++17).
    

**Pencarian (_Lookup_)**

- **`count`**: Mengembalikan jumlah elemen yang cocok dengan _key_ tertentu (selalu 1 atau 0 untuk `std::set`).
    
- **`find`**: Menemukan elemen dengan _key_ tertentu.
    
- **`contains`**: Memeriksa apakah _container_ memiliki elemen dengan _key_ tertentu (C++20).
    
- **`equal_range`**: Mengembalikan rentang elemen yang cocok dengan _key_ tertentu.
    
- **`lower_bound`**: Mengembalikan _iterator_ ke elemen pertama yang tidak kurang dari (>=) _key_ yang diberikan.
    
- **`upper_bound`**: Mengembalikan _iterator_ ke elemen pertama yang lebih besar dari (>) _key_ yang diberikan.
    

**Pengamat (_Observers_)**

- **`key_comp`**: Mengembalikan fungsi yang membandingkan _keys_.
    
- **`value_comp`**: Mengembalikan fungsi yang membandingkan _keys_ dalam objek `value_type`.
    

### Fungsi _Non-member_

- **Operator Perbandingan**: Membandingkan isi dari dua `set` secara leksikografis (`==`, `!=`, `<`, `<=`, `>`, `>=`, `<=>`).
    
- **`std::swap`** (terspesialisasi untuk `std::set`): Menukar isi dari dua `set`.
    
- **`std::erase_if`**: Menghapus semua elemen yang memenuhi kriteria tertentu (C++20).
    

### Contoh Penggunaan


```cpp
#include <algorithm>
#include <iomanip>
#include <iostream>
#include <iterator>
#include <set>
#include <string_view>

template<typename T>
std::ostream& operator<<(std::ostream& out, const std::set<T>& set)
{
    if (set.empty())
        return out << "{}";
    out << "{ " << *set.begin();
    std::for_each(std::next(set.begin()), set.end(), [&out](const T& element)
    {
        out << ", " << element;
    });
    return out << " }";
}

int main()
{
    std::set<int> set{1, 5, 3};
    std::cout << set << '\n';

    set.insert(2);
    std::cout << set << '\n';

    set.erase(1);
    std::cout << set << "\n\n";

    std::set<int> keys{3, 4};
    for (int key : keys)
    {
        if (set.contains(key))
            std::cout << set << " does contain " << key << '\n';
        else
            std::cout << set << " doesn't contain " << key << '\n';
    }
    std::cout << '\n';

    std::string_view word = "element";
    std::set<char> characters(word.begin(), word.end());
    std::cout << "There are " << characters.size() << " unique characters in "
              << std::quoted(word) << ":\n" << characters << '\n';
}
```

**Output:**


```
{ 1, 3, 5 }
{ 1, 2, 3, 5 }
{ 2, 3, 5 }

{ 2, 3, 5 } does contain 3
{ 2, 3, 5 } doesn't contain 4

There are 5 unique characters in "element":
{ e, l, m, n, t }
```