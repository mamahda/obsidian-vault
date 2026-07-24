Source: https://en.cppreference.com/cpp/container/stack

``` cpp
template<
    class T,
    class Container = std::deque<T>
> class stack;
```

Kelas `std::stack` adalah sebuah _container adaptor_ yang memberikan pemrogram fungsionalitas dari sebuah _stack_ - secara spesifik, struktur data LIFO (_last-in, first-out_).

Kelas _template_ ini bertindak sebagai _wrapper_ untuk _underlying container_ - hanya serangkaian fungsi spesifik yang disediakan. _Stack_ memasukkan (_pushes_) dan mengeluarkan (_pops_) elemen dari bagian belakang _underlying container_, yang dikenal sebagai bagian atas _stack_ (_top of the stack_).

### Parameter _Template_

- **`T`**: Tipe dari elemen yang disimpan. Program akan menjadi _ill-formed_ jika `T` bukan tipe yang sama dengan `Container::value_type`.
    
- **`Container`**: Tipe dari _underlying container_ yang digunakan untuk menyimpan elemen-elemen. _Container_ tersebut harus memenuhi persyaratan dari _SequenceContainer_. Selain itu, ia harus menyediakan fungsi-fungsi berikut dengan semantik biasa (_usual semantics_):
    
    - `back()`, contohnya `std::vector::back()`,
        
    - `push_back()`, contohnya `std::deque::push_back()`,
        
    - `pop_back()`, contohnya `std::list::pop_back()`.
        
    
    _Standard containers_ `std::vector` (termasuk `std::vector<bool>`), `std::deque` dan `std::list` memenuhi persyaratan ini. Secara _default_, jika tidak ada kelas _container_ yang ditentukan untuk instansiasi kelas _stack_ tertentu, _standard container_ `std::deque` akan digunakan.
    

### _Member Types_ (Tipe Anggota)

|**Member type**|**Definisi**|
|---|---|
|`container_type`|`Container`|
|`value_type`|`Container::value_type`|
|`size_type`|`Container::size_type`|
|`reference`|`Container::reference`|
|`const_reference`|`Container::const_reference`|

### _Member Objects_ (Objek Anggota)

|**Nama Anggota**|**Deskripsi**|
|---|---|
|`c`|_underlying container_ (container yang mendasarinya)|

### _Member Functions_ (Fungsi Anggota)

- **(Konstruktor)**: Mengonstruksi `stack`.
    
- **(Destruktor)**: Menghancurkan `stack`.
    
- **`operator=`**: Menetapkan nilai ke _container adaptor_.
    

**Akses Elemen (_Element access_)**

- **`top`**: Mengakses elemen teratas.
    

**Kapasitas (_Capacity_)**

- **`empty`**: Memeriksa apakah _container_ kosong.
    
- **`size`**: Mengembalikan jumlah elemen.
    

**Modifikator (_Modifiers_)**

- **`push`**: Menyisipkan (_insert_) elemen di bagian atas.
    
- **`push_range`**: Menyisipkan rentang elemen di bagian atas (C++23).
    
- **`emplace`**: Mengonstruksi elemen di tempat (_in-place_) di bagian atas.
    
- **`pop`**: Menghapus elemen teratas.
    
- **`swap`**: Menukar isi.
    

### Fungsi _Non-member_

- **Operator Perbandingan**: Membandingkan isi dari dua `stack` secara leksikografis (`==`, `!=`, `<`, `<=`, `>`, `>=`, `<=>`).
    
- **`std::swap`** (terspesialisasi untuk `std::stack`): Menukar isi dari dua `stack`.
    

### Kelas Pembantu (_Helper classes_)

- **`std::uses_allocator`**: Terspesialisasi untuk `std::stack`.
    
- **`std::formatter`**: Adaptor _formatter_ untuk dukungan _formatting_ (C++23).