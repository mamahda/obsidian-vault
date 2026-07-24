Source: https://en.cppreference.com/cpp/string/basic_string

```cpp
// (1)
template<
    class CharT,
    class Traits = std::char_traits<CharT>,
    class Allocator = std::allocator<CharT>
> class basic_string;

// (2) Sejak C++17
namespace pmr {
template<
    class CharT,
    class Traits = std::char_traits<CharT>
> using basic_string =
    std::basic_string<CharT, Traits, std::pmr::polymorphic_allocator<CharT>>;
}
```

_Class template_ `basic_string` menyimpan dan memanipulasi urutan objek _character-like_, yang merupakan objek _non-array_ dari `TrivialType` dan `StandardLayoutType`. Kelas ini tidak bergantung pada tipe karakter maupun sifat operasi pada tipe tersebut. Definisi operasi disediakan melalui parameter _template_ `Traits` — sebuah spesialisasi dari `std::char_traits` atau kelas _traits_ yang kompatibel.

Elemen-elemen dari sebuah `basic_string` disimpan secara _contiguous_ (berdampingan). Artinya, untuk sebuah `basic_string` `s`, `&*(s.begin() + n) == &*s.begin() + n` untuk setiap `n` dalam rentang `0` hingga `s.size()` (sejak C++11, `*(s.begin() + s.size())` memiliki nilai `CharT()` yang merupakan _null terminator_); atau secara ekuivalen, sebuah _pointer_ ke `s[0]` dapat diteruskan ke fungsi-fungsi yang mengharapkan _pointer_ ke elemen pertama dari array _null-terminated_ dari `CharT`.

`std::basic_string` memenuhi persyaratan `AllocatorAwareContainer` (kecuali bahwa `construct`/`destroy` yang dikustomisasi tidak digunakan untuk konstruksi/destruksi elemen), `SequenceContainer`, dan `ContiguousContainer` (sejak C++17).

Jika salah satu dari `Traits::char_type` dan `Allocator::char_type` berbeda dari `CharT`, maka program tersebut bersifat _ill-formed_.

_(Dapat digunakan dalam konteks `constexpr` sejak C++20)_

### _Typedefs_ Tipe Karakter Umum

Beberapa _typedef_ untuk tipe karakter umum telah disediakan:

|**Tipe**|**Definisi**|
|---|---|
|**`std::string`**|`std::basic_string<char>`|
|**`std::wstring`**|`std::basic_string<wchar_t>`|
|**`std::u8string`** _(C++20)_|`std::basic_string<char8_t>`|
|**`std::u16string`** _(C++11)_|`std::basic_string<char16_t>`|
|**`std::u32string`** _(C++11)_|`std::basic_string<char32_t>`|
|**`std::pmr::string`** _(C++17)_|`std::pmr::basic_string<char>`|
|**`std::pmr::wstring`** _(C++17)_|`std::pmr::basic_string<wchar_t>`|
|**`std::pmr::u8string`** _(C++20)_|`std::pmr::basic_string<char8_t>`|
|**`std::pmr::u16string`** _(C++17)_|`std::pmr::basic_string<char16_t>`|
|**`std::pmr::u32string`** _(C++17)_|`std::pmr::basic_string<char32_t>`|

### Parameter _Template_

- **`CharT`**: _Character type_ (tipe karakter).
    
- **`Traits`**: Kelas _traits_ yang menspesifikasikan operasi pada tipe karakter tersebut.
    
- **`Allocator`**: Tipe `Allocator` yang digunakan untuk mengalokasikan penyimpanan internal (_internal storage_).
    

### _Nested Types_

|**Tipe**|**Definisi**|
|---|---|
|`traits_type`|`Traits`|
|`value_type`|`CharT`|
|`allocator_type`|Tipe _allocator_ `Allocator`|
|`size_type`|Tipe _unsigned integer_|
|`difference_type`|Tipe _signed integer_|
|`reference`|Referensi ke elemen|
|`const_reference`|Referensi konstan ke elemen|
|`pointer`|_Pointer_ ke elemen|
|`const_pointer`|_Pointer_ konstan ke elemen|
|`iterator`|_Iterator_|
|`const_iterator`|_Iterator_ konstan|
|`reverse_iterator`|_Reverse iterator_|
|`const_reverse_iterator`|_Reverse iterator_ konstan|

### _Data Members_

- **`npos`**: Nilai khusus yang merepresentasikan posisi tidak valid atau akhir dari _string_.
    

### _Member Functions_

- `constructor` / `destructor`
    
- `operator=`
    
- `assign` / `assign_range`
    
- `get_allocator`
    

**Akses Elemen (_Element Access_)**

- `at` / `operator[]`
    
- `front` / `back`
    
- `data` / `c_str`
    
- `operator string_view`
    

**_Iterators_**

- `begin` / `end`
    
- `rbegin` / `rend`
    

**Kapasitas (_Capacity_)**

- `empty` / `size` / `max_size`
    
- `reserve` / `capacity` / `shrink_to_fit`
    

**Modifikasi (_Modifiers_)**

- `clear`
    
- `insert` / `insert_range`
    
- `erase`
    
- `push_back` / `pop_back`
    
- `append` / `append_range`
    
- `operator+=`
    
- `replace` / `replace_with_range`
    
- `copy`
    
- `resize` / `resize_and_overwrite`
    
- `swap`
    

**Pencarian (_Search_)**

- `find` / `rfind`
    
- `find_first_of` / `find_first_not_of`
    
- `find_last_of` / `find_last_not_of`
    

**Operasi (_Operations_)**

- `compare`
    
- `starts_with` / `ends_with`
    
- `contains`
    
- `substr`
    

### _Non-member Functions_

- `operator+`
    
- `operator<=>` _(Comparison operators)_
    
- `swap`
    
- `erase` / `erase_if`
    

**Input/Output**

- `operator<<` / `operator>>`
    
- `getline`
    

**Konversi Numerik (_Numeric Conversions_)**

- `stol` / `stoul` / `stof`
    
- `to_string` / `to_wstring`
    

### _Literals_

_(Berada di dalam `std::literals::string_literals`)_

- `operator""s`
    

### _Helper Classes_

- `std::hash<std::basic_string>`
    

### Panduan Deduksi (_Deduction Guides_)

_(Tersedia sejak C++17)_

### _Iterator Invalidation_

Referensi, _pointer_, dan _iterator_ yang merujuk pada elemen-elemen dari sebuah `basic_string` dapat mengalami _invalidation_ apabila ada fungsi dari _standard library_ yang menggunakan referensi ke `basic_string` _non-const_ sebagai argumen, contohnya `std::getline`, `std::swap`, atau `operator>>`. Memanggil _non-const member functions_ juga akan memicu _invalidation_, kecuali untuk fungsi-fungsi berikut: `operator[]`, `at`, `data`, `front`, `back`, `begin`, `rbegin`, `end`, dan `rend`.

### Catatan (_Notes_)

Meskipun hingga standar C++23 penggunaan `construct` atau `destroy` yang dikustomisasi diwajibkan saat membuat atau menghancurkan elemen dari `std::basic_string`, semua implementasi pada praktiknya hanya menggunakan mekanisme _default_. Persyaratan ini telah diperbaiki melalui **P1072R10** agar selaras dengan _existing practice_ (praktik yang sudah berjalan).

|**Standar**|**Macro Pengujian (Feature-test Macro)**|**Nilai**|**Penjelasan**|
|---|---|---|---|
|C++14|`__cpp_lib_string_udls`|`201304L`|_User-defined literals_ untuk tipe string|
|C++20|`__cpp_lib_starts_ends_with`|`201711L`|`starts_with`, `ends_with`|
|C++20|`__cpp_lib_constexpr_string`|`201907L`|`constexpr` untuk `std::basic_string`|
|C++20|`__cpp_lib_char8_t`|`201907L`|`std::u8string`|
|C++20|`__cpp_lib_erase_if`|`202002L`|`erase`, `erase_if`|
|C++23|`__cpp_lib_string_contains`|`202011L`|`contains`|
|C++23|`__cpp_lib_string_resize_and_overwrite`|`202110L`|`resize_and_overwrite`|
|C++23|`__cpp_lib_containers_ranges`|`202202L`|_Member functions_ untuk konstruksi, insersi, dan penggantian yang menerima _container compatible range_|

### Contoh (_Example_)


```cpp
#include <iostream>
#include <string>

int main()
{
    using namespace std::literals;
    
    // Membuat string dari const char*
    std::string str1 = "hello";
    
    // Membuat string menggunakan string literal
    auto str2 = "world"s;
    
    // Menggabungkan string (Concatenating)
    std::string str3 = str1 + " " + str2;
    
    // Mencetak hasil
    std::cout << str3 << '\n';
    
    std::string::size_type pos = str3.find(" ");
    str1 = str3.substr(pos + 1); // bagian setelah spasi
    str2 = str3.substr(0, pos);  // bagian sampai spasi
    
    std::cout << str1 << ' ' << str2 << '\n';
    
    // Mengakses elemen menggunakan subscript operator[]
    std::cout << str1[0] << '\n';
    str1[0] = 'W';
    std::cout << str1 << '\n';
}
```

**Output:**


```
hello world
world hello
w
World
```