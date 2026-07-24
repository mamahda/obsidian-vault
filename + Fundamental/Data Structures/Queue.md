Source: https://en.cppreference.com/cpp/container/queue

```cpp
template<
    class T,
    class Container = std::deque<T>
> class queue;
```

Kelas _template_ `std::queue` adalah sebuah _container adaptor_ yang memberikan fungsionalitas dari sebuah _queue_ - secara spesifik, struktur data FIFO (_first-in, first-out_).

Kelas _template_ ini bertindak sebagai _wrapper_ untuk _underlying container_ - hanya serangkaian fungsi spesifik yang disediakan. _Queue_ memasukkan (_pushes_) elemen di bagian belakang _underlying container_ dan mengeluarkannya (_pops_) dari bagian depan.

### Parameter _Template_

- **`T`**: Tipe dari elemen yang disimpan. Program akan menjadi _ill-formed_ jika `T` bukan tipe yang sama dengan `Container::value_type`.
    
- **`Container`**: Tipe dari _underlying container_ yang digunakan untuk menyimpan elemen-elemen. _Container_ tersebut harus memenuhi persyaratan dari _SequenceContainer_. Selain itu, ia harus menyediakan fungsi-fungsi berikut dengan semantik biasa (_usual semantics_):
    
    - `back()`, contohnya `std::deque::back()`,
        
    - `front()`, contohnya `std::list::front()`,
        
    - `push_back()`, contohnya `std::deque::push_back()`,
        
    - `pop_front()`, contohnya `std::list::pop_front()`.
        
    
    _Standard containers_ `std::deque` dan `std::list` memenuhi persyaratan ini.
    

### _Member Types_ (Tipe Anggota)

|**Member type**|**Definisi**|
|---|---|
|`container_type`|`Container`|
|`value_type`|`Container::value_type`|
|`size_type`|`Container::size_type`|
|`reference`|`Container::reference`|
|`const_reference`|`Container::const_reference`|

### _Member Objects_ (Objek Anggota)

|**Nama Anggota**|**Definisi**|
|---|---|
|`c`|_underlying container_ (container yang mendasarinya)|

### _Member Functions_ (Fungsi Anggota)

- **(Konstruktor)**: Mengonstruksi `queue`.
    
- **(Destruktor)**: Menghancurkan `queue`.
    
- **`operator=`**: Menetapkan nilai ke _container adaptor_.
    

**Akses Elemen (_Element access_)**

- **`front`**: Mengakses elemen pertama.
    
- **`back`**: Mengakses elemen terakhir.
    

**Kapasitas (_Capacity_)**

- **`empty`**: Memeriksa apakah _container_ kosong.
    
- **`size`**: Mengembalikan jumlah elemen.
    

**Modifikator (_Modifiers_)**

- **`push`**: Menyisipkan (_insert_) elemen di bagian akhir.
    
- **`push_range`**: Menyisipkan rentang elemen di bagian akhir (C++23).
    
- **`emplace`**: Mengonstruksi elemen di tempat (_in-place_) di bagian akhir.
    
- **`pop`**: Menghapus elemen pertama.
    
- **`swap`**: Menukar isi.
    

### Fungsi _Non-member_

- **Operator Perbandingan**: Membandingkan isi dari dua `queue` secara leksikografis.
    
- **`std::swap`** (terspesialisasi untuk `std::queue`): Menukar isi dari dua `queue`.
    

### Kelas Pembantu (_Helper classes_)

- **`std::uses_allocator`**: Terspesialisasi untuk `std::queue`.
    
- **`std::formatter`**: Adaptor _formatter_ untuk dukungan _formatting_ (C++23).
    

### Contoh Penggunaan

```cpp
#include <cassert>
#include <iostream>
#include <queue>

int main()
{
    std::queue<int> q;

    q.push(0); // memasukkan 0 di bagian belakang
    q.push(1); // q = 0 1
    q.push(2); // q = 0 1 2
    q.push(3); // q = 0 1 2 3

    assert(q.front() == 0);
    assert(q.back() == 3);
    assert(q.size() == 4);

    q.pop(); // menghapus elemen paling depan, yaitu 0
    assert(q.size() == 3);

    // Mencetak dan menghapus semua elemen. Perhatikan bahwa std::queue
    // tidak mendukung begin()/end(), sehingga range-for-loop tidak dapat digunakan.
    std::cout << "q: ";
    for (; !q.empty(); q.pop())
        std::cout << q.front() << ' ';
    std::cout << '\n';
    assert(q.size() == 0);
}
```

**Output:**

```
q: 1 2 3
```