Source: https://en.cppreference.com/cpp/container/priority_queue

```cpp
template<
    class T,
    class Container = std::vector<T>,
    class Compare = std::less<typename Container::value_type>
> class priority_queue;
```

**Priority queue** adalah sebuah _container adaptor_ yang menyediakan _lookup_ waktu konstan untuk menemukan elemen terbesar (secara _default_), dengan mengorbankan waktu logaritmik untuk operasi _insertion_ dan _extraction_.

Sebuah tipe `Compare` yang disediakan oleh pengguna dapat diberikan untuk mengubah aturan pengurutan, contohnya menggunakan `std::greater<T>` akan menyebabkan elemen terkecil muncul saat memanggil `top()`.

Bekerja dengan `priority_queue` mirip dengan mengelola sebuah _heap_ di dalam suatu _random access container_, dengan keuntungan bahwa Anda tidak dapat membatalkan validitas (_invalidate_) _heap_ tersebut secara tidak sengaja.

### Parameter _Template_

- **`T`**: Tipe dari elemen yang disimpan. Program akan menjadi _ill-formed_ jika `T` bukan tipe yang sama dengan `Container::value_type`.
    
- **`Container`**: Tipe dari _underlying container_ yang digunakan untuk menyimpan elemen-elemen. _Container_ tersebut harus memenuhi persyaratan dari _SequenceContainer_, dan _iterators_-nya harus memenuhi persyaratan dari _RandomAccessIterator_. Selain itu, ia harus menyediakan fungsi-fungsi berikut dengan semantik biasa (_usual semantics_):
    
    - `front()`, contohnya `std::vector::front()`,
        
    - `push_back()`, contohnya `std::deque::push_back()`,
        
    - `pop_back()`, contohnya `std::vector::pop_back()`.
        
    
    _Standard containers_ `std::vector` (tidak termasuk `std::vector<bool>`) dan `std::deque` memenuhi persyaratan ini.
    
- **`Compare`**: Sebuah tipe _Compare_ yang menyediakan _strict weak ordering_.
    
    Perhatikan bahwa parameter _Compare_ didefinisikan sedemikian rupa sehingga ia mengembalikan `true` jika argumen pertamanya muncul _sebelum_ argumen keduanya dalam sebuah _weak ordering_. Namun karena _priority queue_ mengeluarkan elemen terbesar terlebih dahulu, elemen yang "muncul sebelum" sebenarnya akan dikeluarkan paling akhir. Artinya, bagian depan dari _queue_ berisi elemen "terakhir" menurut aturan _weak ordering_ yang diterapkan oleh _Compare_.
    

### _Member Types_ (Tipe Anggota)

|**Member type**|**Definisi**|
|---|---|
|`container_type`|`Container`|
|`value_compare`|`Compare`|
|`value_type`|`Container::value_type`|
|`size_type`|`Container::size_type`|
|`reference`|`Container::reference`|
|`const_reference`|`Container::const_reference`|

### _Member Objects_ (Objek Anggota)

|**Nama Anggota**|**Definisi**|
|---|---|
|`c`|_underlying container_ (container yang mendasarinya)|
|`comp`|objek fungsi perbandingan (_comparison function object_)|

### _Member Functions_ (Fungsi Anggota)

- **(Konstruktor)**: Mengonstruksi `priority_queue`.
    
- **(Destruktor)**: Menghancurkan `priority_queue`.
    
- **`operator=`**: Menetapkan nilai ke _container adaptor_.
    

**Akses Elemen (_Element access_)**

- **`top`**: Mengakses elemen teratas.
    

**Kapasitas (_Capacity_)**

- **`empty`**: Memeriksa apakah _container_ kosong.
    
- **`size`**: Mengembalikan jumlah elemen.
    

**Modifikator (_Modifiers_)**

- **`push`**: Menyisipkan (_insert_) elemen dan mengurutkan _underlying container_.
    
- **`push_range`**: Menyisipkan rentang elemen (C++23).
    
- **`emplace`**: Mengonstruksi elemen di tempat (_in-place_) dan mengurutkan _underlying container_.
    
- **`pop`**: Menghapus elemen teratas.
    
- **`swap`**: Menukar isi.
    

### Fungsi _Non-member_

- **`std::swap`** (terspesialisasi untuk `std::priority_queue`): Menukar isi dari dua `priority_queue`.
    

### Kelas Pembantu (_Helper classes_)

- **`std::uses_allocator`**: Terspesialisasi untuk `std::priority_queue`.
    
- **`std::formatter`**: Adaptor _formatter_ untuk dukungan _formatting_ (C++23).
    

### Contoh Penggunaan

```cpp
#include <functional>
#include <iostream>
#include <queue>
#include <string_view>
#include <vector>

template<typename T>
void pop_println(std::string_view rem, T& pq)
{
    std::cout << rem << ": ";
    for (; !pq.empty(); pq.pop())
        std::cout << pq.top() << ' ';
    std::cout << '\n';
}

template<typename T>
void println(std::string_view rem, const T& v)
{
    std::cout << rem << ": ";
    for (const auto& e : v)
        std::cout << e << ' ';
    std::cout << '\n';
}

int main()
{
    const auto data = {1, 8, 5, 6, 3, 4, 0, 9, 7, 2};
    println("data", data);

    std::priority_queue<int> max_priority_queue;

    // Mengisi priority queue.
    for (int n : data)
        max_priority_queue.push(n);

    pop_println("max_priority_queue", max_priority_queue);

    // std::greater<int> membuat max priority queue bertindak sebagai min priority queue.
    std::priority_queue<int, std::vector<int>, std::greater<int>>
        min_priority_queue1(data.begin(), data.end());

    pop_println("min_priority_queue1", min_priority_queue1);

    // Cara kedua untuk mendefinisikan min priority queue.
    std::priority_queue min_priority_queue2(data.begin(), data.end(), std::greater<int>());

    pop_println("min_priority_queue2", min_priority_queue2);

    // Menggunakan custom function object untuk membandingkan elemen.
    struct
    {
        bool operator()(const int l, const int r) const { return l > r; }
    } customLess;

    std::priority_queue custom_priority_queue(data.begin(), data.end(), customLess);

    pop_println("custom_priority_queue", custom_priority_queue);

    // Menggunakan lambda untuk membandingkan elemen.
    auto cmp = [](int left, int right) { return (left ^ 1) < (right ^ 1); };
    std::priority_queue<int, std::vector<int>, decltype(cmp)> lambda_priority_queue(cmp);

    for (int n : data)
        lambda_priority_queue.push(n);

    pop_println("lambda_priority_queue", lambda_priority_queue);
}
```

**Output:**

```
data: 1 8 5 6 3 4 0 9 7 2
max_priority_queue: 9 8 7 6 5 4 3 2 1 0
min_priority_queue1: 0 1 2 3 4 5 6 7 8 9
min_priority_queue2: 0 1 2 3 4 5 6 7 8 9
custom_priority_queue: 0 1 2 3 4 5 6 7 8 9
lambda_priority_queue: 8 9 6 7 4 5 2 3 0 1
```