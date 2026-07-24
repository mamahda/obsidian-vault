Source: https://en.wikipedia.org/wiki/Object-oriented_programming

_Object-oriented programming_ (OOP) adalah sebuah _programming paradigm_ yang berbasis pada _objects_, yaitu entitas perangkat lunak yang melakukan _encapsulate_ pada data dan _function_. Sebuah program komputer OOP terdiri dari _objects_ yang saling berinteraksi satu sama lain. Bahasa OOP adalah bahasa yang menyediakan fitur-fitur _object-oriented programming_, namun karena kumpulan fitur yang berkontribusi pada OOP masih sering diperdebatkan, mengklasifikasikan sebuah bahasa sebagai OOP (dan sejauh mana bahasa tersebut mendukung OOP) dapat menjadi bahan diskusi. Karena _paradigms_ tidak bersifat eksklusif satu sama lain, sebuah bahasa bisa saja merupakan _multi-paradigm_ (misalnya dikategorikan lebih dari sekadar OOP).

Bahasa-bahasa terkemuka yang memiliki dukungan OOP meliputi Ada, ActionScript, C++, Common Lisp, C#, Dart, Eiffel, Fortran 2003, Haxe, Java, JavaScript, Kotlin, Logo, MATLAB, Objective-C, Object Pascal, Perl, PHP, Python, R, Raku, Ruby, Scala, SIMSCRIPT, Simula, Smalltalk, Swift, Vala, dan Visual Basic (.NET).

## Sejarah

Gagasan tentang _objects_ dalam pemrograman dimulai oleh grup kecerdasan buatan (_artificial intelligence_) di Massachusetts Institute of Technology (MIT) pada akhir 1950-an dan awal 1960-an. Di sana, _object_ merujuk pada atom LISP dengan properti (_attributes_) yang teridentifikasi.

Contoh awal lainnya adalah Sketchpad yang diciptakan oleh Ivan Sutherland di MIT pada tahun 1960 hingga 1961. Dalam glosarium laporan teknisnya, Sutherland mendefinisikan istilah seperti _object_ dan _instance_ (dengan konsep _class_ yang dicakup oleh istilah "master" atau "definition"), meskipun dikhususkan untuk interaksi grafis. Kemudian, pada tahun 1968, AED-0, versi MIT dari _programming language_ ALGOL, menghubungkan struktur data ("plexes") dengan prosedur, yang mengawali apa yang kemudian disebut sebagai _messages_, _methods_, dan _member functions_. Topik seperti _data abstraction_ dan _modular programming_ menjadi bahan diskusi umum pada masa itu.

Sementara itu, di Norwegia, Simula dikembangkan pada tahun 1961 hingga 1967. Simula memperkenalkan ide-ide esensial _object-oriented_, seperti _classes_, _inheritance_, dan _dynamic binding_. Simula pada awalnya digunakan oleh para peneliti yang terlibat dalam pemodelan fisik, seperti pergerakan kapal dan muatannya di pelabuhan. Simula secara umum diterima sebagai bahasa pertama yang memiliki fitur utama dan _framework_ dari sebuah _object-oriented language_.

> "Saya membayangkan _objects_ seperti sel biologis dan/atau komputer individual di dalam sebuah jaringan, yang hanya dapat berkomunikasi dengan _messages_ (jadi _messaging_ muncul sejak awal; butuh waktu untuk melihat bagaimana melakukan _messaging_ dalam _programming language_ secara efisien agar berguna)."
> 
> - Alan Kay
>     

Dipengaruhi oleh MIT dan Simula, Alan Kay mulai mengembangkan ide-idenya sendiri pada bulan November 1966. Ia kemudian menciptakan Smalltalk, sebuah bahasa OOP yang sangat berpengaruh. Pada tahun 1967, Kay sudah menggunakan istilah _object-oriented programming_ dalam percakapannya. Meskipun terkadang disebut sebagai "bapak" OOP, Kay mengatakan bahwa ide-idenya berbeda dari bagaimana OOP dipahami secara umum, dan mengisyaratkan bahwa kalangan ilmu komputer (_computer science establishment_) tidak mengadopsi gagasannya.

Memo MIT tahun 1976 yang ditulis bersama oleh Barbara Liskov mencantumkan Simula 67, CLU, dan Alphard sebagai bahasa _object-oriented_, tetapi tidak menyebutkan Smalltalk.

Pada 1970-an, versi pertama _programming language_ Smalltalk dikembangkan di Xerox PARC oleh Alan Kay, Dan Ingalls, dan Adele Goldberg. Smalltalk-72 menonjol karena penggunaan _objects_ di tingkat bahasa dan lingkungan pengembangan grafisnya. Smalltalk adalah sistem yang sepenuhnya dinamis, memungkinkan pengguna untuk membuat dan memodifikasi _classes_ saat mereka bekerja. Sebagian besar teori OOP dikembangkan dalam konteks Smalltalk, contohnya _multiple inheritance_.

Pada akhir 1970-an dan 1980-an, OOP mulai menonjol. The Flavors _object-oriented_ Lisp dikembangkan mulai tahun 1979, memperkenalkan _multiple inheritance_ dan _mixins_. Pada Agustus 1981, Byte Magazine menyoroti Smalltalk dan OOP, memperkenalkan ide-ide ini kepada khalayak luas. LOOPS, sistem _object_ untuk Interlisp-D, dipengaruhi oleh Smalltalk dan Flavors, dan sebuah makalah tentang hal itu diterbitkan pada tahun 1982. Pada tahun 1986, Konferensi pertama tentang Object-Oriented Programming, Systems, Languages, and Applications (OOPSLA) dihadiri oleh 1.000 orang. Konferensi ini menandai dimulainya upaya untuk mengkonsolidasikan sistem Lisp _object_, yang pada akhirnya menghasilkan Common Lisp Object System. Pada 1980-an, ada beberapa upaya untuk merancang arsitektur prosesor yang menyertakan dukungan perangkat keras untuk _objects_ di memori, tetapi upaya ini tidak berhasil. Contohnya termasuk Intel iAPX 432 dan Linn Smart Rekursiv.

Pada pertengahan 1980-an, bahasa _object-oriented_ baru seperti Objective-C, C++, dan bahasa Eiffel muncul. Objective-C dikembangkan oleh Brad Cox, yang telah menggunakan Smalltalk di ITT Inc. Bjarne Stroustrup menciptakan C++ berdasarkan pengalamannya menggunakan Simula untuk tesis PhD-nya. Bertrand Meyer merancang desain pertama bahasa Eiffel pada tahun 1985, yang berfokus pada kualitas perangkat lunak menggunakan pendekatan _design by contract_.

Pada 1990-an, OOP menjadi cara utama dalam pemrograman, terutama karena semakin banyak bahasa yang mendukungnya. Ini termasuk Visual FoxPro 3.0, C++, dan Delphi. OOP menjadi semakin populer dengan munculnya antarmuka pengguna grafis (_graphical user interfaces_ / GUI), yang menggunakan _objects_ untuk tombol, menu, dan elemen lainnya. Salah satu contoh terkenal adalah _framework_ Cocoa dari Apple, yang digunakan di macOS dan ditulis dalam Objective-C. Toolkit OOP juga meningkatkan popularitas _event-driven programming_.

Di ETH Zürich, Niklaus Wirth dan rekan-rekannya menciptakan pendekatan baru terhadap OOP. Modula-2 (1978) dan Oberon (1987) menyertakan pendekatan khas terhadap _object orientation_, _classes_, dan _type checking_ lintas batas modul. _Inheritance_ tidak terlalu kentara dalam desain Wirth karena tata namanya melihat ke arah yang berlawanan: Hal ini disebut _type extension_ dan sudut pandangnya adalah dari _parent_ ke bawah ke _inheritor_.

Banyak _programming languages_ yang awalnya dikembangkan sebelum OOP menjadi populer telah ditambahkan dengan fitur _object-oriented_, termasuk Ada, BASIC, Fortran, Pascal, dan COBOL.

## Fitur (_Features_)

Fitur OOP yang disediakan oleh bahasa bervariasi. Di bawah ini adalah beberapa fitur umum dari bahasa OOP. Membandingkan OOP dengan gaya lain, seperti _relational programming_, sulit dilakukan karena tidak ada definisi OOP yang disepakati dengan jelas.

### Encapsulation dan Information Hiding

_Information hiding_ dan _encapsulation_ dapat merujuk pada beberapa konsep yang saling berkaitan:

- **Cohesion**: Menyatukan _fields_ dan _methods_ yang terkait bersama-sama. Sebuah _field_ (alias _attribute_ atau _property_) berisi informasi (alias _state_) sebagai _variable_. Sebuah _method_ (alias _function_ atau aksi) mendefinisikan _behavior_ melalui kode logika.
    
- **Decoupling**: Mengatur kode sehingga hanya bagian tertentu dari data yang digunakan oleh _functions_ terkait. _Decoupling_ mempermudah perubahan cara kerja _object_ di dalam tanpa memengaruhi bagian lain dari basis kode (_codebase_), seperti dalam _code refactoring_. _Objects_ bertindak sebagai batas antara cara kerja internal mereka dan kode konsumsi eksternal.
    
- **Data hiding**: Menjaga detail internal sebuah _object_ tersembunyi dari kode luar. Kode konsumsi hanya dapat berinteraksi dengan sebuah _object_ melalui _public members_-nya, berkat bahasa yang menyediakan _access modifiers_ yang mengontrol visibilitas.
    

Beberapa _programming languages_, seperti Java, menyediakan _information hiding_ melalui kata kunci visibilitas (`private` dan `public`). Beberapa bahasa seperti Python tidak menyediakan fitur visibilitas, tetapi pengembang (_developers_) mungkin mengikuti konvensi seperti memulai nama _private member_ dengan garis bawah (\_). Tingkat akses menengah juga ada, seperti kata kunci `protected` di Java (yang mengizinkan akses dari _class_ yang sama dan _subclasses_-nya, tetapi tidak untuk _objects_ dari _class_ yang berbeda), dan kata kunci `internal` di C#, Swift, dan Kotlin, yang membatasi akses ke file di dalam modul yang sama.

Pendukung _information hiding_ dan _data abstraction_ mengatakan hal ini membuat kode lebih mudah untuk digunakan kembali (_reuse_) dan secara intuitif mewakili situasi dunia nyata. Namun, pihak lain berpendapat bahwa OOP tidak meningkatkan keterbacaan (_readability_) atau modularitas. Eric S. Raymond menulis bahwa bahasa OOP cenderung mendorong program dengan lapisan tebal yang menghancurkan transparansi. Raymond membandingkan ini secara kurang menguntungkan dengan pendekatan yang diambil oleh Unix dan bahasa C.

SOLID mencakup _open/closed principle_, yang menyatakan bahwa _classes_ dan _functions_ harus "terbuka untuk _extension_, tetapi tertutup untuk modifikasi". Luca Cardelli menyatakan bahwa bahasa OOP memiliki sifat modularitas yang sangat buruk terkait _class extension_ dan modifikasi, serta cenderung sangat kompleks. Hal ini ditegaskan kembali oleh Joe Armstrong, penemu utama Erlang, yang dikutip mengatakan:

> "Masalah dengan bahasa _object-oriented_ adalah mereka membawa semua _implicit environment_ ini ke mana-mana bersama mereka. Anda menginginkan pisang tetapi yang Anda dapatkan adalah gorila yang memegang pisang tersebut beserta seluruh hutannya."

Leo Brodie mengatakan bahwa _information hiding_ dapat menyebabkan duplikasi kode, yang bertentangan dengan aturan "don't repeat yourself" (DRY) dalam pengembangan perangkat lunak.

### Inheritance

_Inheritance_ dapat didukung melalui _class_ atau _prototype_, yang memiliki perbedaan namun menggunakan istilah serupa seperti _object_ dan _instance_.

#### Class-based

Dalam _class-based programming_ (tipe OOP yang paling umum), sebuah _object_ adalah sebuah _instance_ dari sebuah _class_. _Class_ tersebut mendefinisikan data (_variables_) dan _methods_ (logika). Sebuah _object_ dibuat menggunakan _constructor_. Setiap _instance_ dari _class_ memiliki set _variables_ dan _methods_ yang sama. Elemen-elemen yang mungkin ada meliputi:

- **Class variable**: Milik _class_ itu sendiri; semua _objects_ dari _class_ berbagi satu salinan.
    
- **Instance variable**: Milik sebuah _object_; setiap _object_ memiliki versinya sendiri dari _variables_ ini.
    
- **Member variable**: Merujuk pada _class variable_ maupun _instance variable_ dari sebuah _class_.
    
- **Class method**: Hanya dapat menggunakan _class variables_.
    
- **Instance method**: Milik sebuah _object_; dapat menggunakan _instance variables_ maupun _class variables_.
    

_Classes_ dapat melakukan _inherit_ (mewarisi) dari _classes_ lain, menciptakan hierarki _classes_: sebuah kasus di mana _subclass_ melakukan _inherit_ dari _super-class_. Contohnya, sebuah _class Employee_ mungkin melakukan _inherit_ dari _class Person_ yang memberikan _object Employee_ akses ke _variables_ dari _Person_. _Subclass_ dapat menambahkan _variables_ dan _methods_ yang tidak memengaruhi _super-class_. Sebagian besar bahasa juga mengizinkan _subclass_ untuk melakukan _override_ pada _methods super-class_. Beberapa bahasa mendukung _multiple inheritance_, di mana sebuah _class_ dapat melakukan _inherit_ dari lebih dari satu _class_, dan bahasa lain mendukung hal serupa seperti _mixins_ atau _traits_. Misalnya, sebuah _mixin_ bernama `UnicodeConversionMixin` mungkin menambahkan _method_ `unicode_to_ascii()` ke _class_ `FileReader` maupun `WebPageScraper`.

Sebuah _abstract class_ tidak dapat secara langsung di-_instantiate_ sebagai sebuah _object_. _Class_ ini hanya digunakan sebagai _super-class_. _Classes_ lainnya adalah _utility classes_ yang hanya berisi _class variables_ dan _methods_ serta tidak dimaksudkan untuk di-_instantiate_ atau dijadikan _subclass_.

#### Prototype-based

Alih-alih menggunakan konsep _class_, dalam _prototype-based programming_, sebuah _object_ ditautkan ke _object_ lain, yang disebut _prototype_ atau _parent_-nya. Dalam Self, sebuah _object_ bisa memiliki banyak atau tidak ada _parent_, tetapi dalam bahasa _prototype-based_ paling populer, JavaScript, sebuah _object_ memiliki tepat satu tautan _prototype_, hingga ke _base object_ yang _prototype_-nya adalah `null`.

Sebuah _prototype_ bertindak sebagai model untuk _objects_ baru. Misalnya, jika Anda memiliki _object_ `fruit`, Anda dapat membuat dua _objects_ `apple` dan `orange` yang berbagi _traits_ dari _prototype_ `fruit`. Bahasa _prototype-based_ juga mengizinkan _objects_ untuk memiliki properti unik mereka sendiri, sehingga _object_ `apple` mungkin memiliki atribut `sugar_content`, sedangkan _object_ `orange` atau `fruit` tidak.

#### Tanpa Inheritance

Dalam semua bahasa OOP, melalui _object composition_, sebuah _object_ dapat berisi _objects_ lainnya. Contohnya, _object Employee_ mungkin berisi _object Address_, bersama dengan informasi lain seperti nama dan posisi. _Composition_ adalah hubungan "has-a", seperti "seorang karyawan memiliki sebuah alamat". Beberapa bahasa, seperti Go, tidak mendukung _inheritance_. Sebagai gantinya, mereka mendorong pendekatan _"composition over inheritance"_, di mana _objects_ dibangun menggunakan bagian-bagian yang lebih kecil alih-alih hubungan _parent-child_. Misalnya, alih-alih melakukan _inherit_ dari _class Person_, _class Employee_ bisa saja cukup menampung sebuah _object Person_. Hal ini membiarkan _class Employee_ mengontrol seberapa banyak bagian _Person_ yang di-_expose_ ke bagian lain dari program. _Delegation_ adalah fitur bahasa lain yang dapat digunakan sebagai alternatif untuk _inheritance_.

Programmer memiliki pendapat yang berbeda tentang _inheritance_. Bjarne Stroustrup, penulis C++, menyatakan bahwa melakukan OOP tanpa _inheritance_ adalah hal yang mungkin. Rob Pike telah mengkritik _inheritance_ karena dinilai menciptakan hierarki yang kompleks ketimbang solusi yang lebih sederhana.

#### Inheritance dan Behavioral Subtyping

Banyak yang sering berpikir bahwa jika satu _class_ melakukan _inherit_ dari _class_ lain, itu berarti _subclass_ "is a" (adalah versi lebih spesifik dari) _class_ aslinya. Hal ini mengasumsikan semantik program (_program semantics_) bahwa _objects_ dari _subclass_ selalu dapat menggantikan _objects_ dari _class_ aslinya tanpa masalah. Konsep ini dikenal sebagai _behavioral subtyping_, atau lebih spesifiknya, _Liskov substitution principle_.

Namun, hal ini sering kali tidak benar, terutama dalam bahasa pemrograman yang mengizinkan _mutable objects_ (_objects_ yang berubah setelah dibuat). Faktanya, _subtype polymorphism_ seperti yang ditegakkan oleh _type checker_ dalam bahasa OOP tidak dapat menjamin _behavioral subtyping_ di sebagian besar, jika tidak semua, konteks. Misalnya, masalah _circle-ellipse_ sangat sulit ditangani menggunakan konsep _inheritance_ dalam OOP. _Behavioral subtyping_ pada umumnya tidak dapat diputuskan (_undecidable_), sehingga tidak dapat dengan mudah diimplementasikan oleh sebuah _compiler_. Karena hal ini, programmer harus dengan hati-hati mendesain hierarki _class_ untuk menghindari kesalahan yang tidak dapat ditangkap oleh _programming language_ itu sendiri.

### Dynamic Dispatch

Sebuah _method_ dapat dipanggil melalui _dynamic dispatch_, sehingga _method_ tersebut dipilih pada saat _runtime_ alih-alih saat _compile time_. Jika pemilihan _method_ bergantung pada lebih dari satu tipe _object_ (seperti _objects_ lain yang diteruskan sebagai parameter), ini disebut _multiple dispatch_. Dalam konteks ini, panggilan _method_ juga dikenal sebagai _message passing_, artinya nama _method_ dan inputnya seperti sebuah pesan yang dikirim ke _object_ untuk ditindaklanjuti.

_Dynamic dispatch_ bekerja bersama dengan _inheritance_: jika sebuah _object_ tidak memiliki _method_ yang diminta, ia akan mencarinya ke _parent class_-nya (_delegation_), dan terus naik ke atas rantai untuk menemukan _method_ yang cocok.

### Polymorphism

_Polymorphism_ dalam OOP merujuk pada _subtyping_ atau _subtype polymorphism_, di mana sebuah _function_ dapat bekerja dengan antarmuka (_interface_) tertentu dan dengan demikian memanipulasi entitas dari _classes_ yang berbeda dengan cara yang seragam.

Contohnya, bayangkan sebuah program memiliki dua bangun ruang: lingkaran dan persegi. Keduanya berasal dari sebuah _class_ umum bernama "Shape." Setiap bangun memiliki caranya sendiri untuk menggambar dirinya. Dengan _subtype polymorphism_, program tidak perlu mengetahui tipe masing-masing bangun, dan cukup memanggil _method_ "Draw" untuk setiap bangun. _Runtime programming language_ akan memastikan versi _method_ "Draw" yang tepat dieksekusi untuk setiap bangun. Karena detail setiap bangun ditangani di dalam _classes_ mereka sendiri, ini membuat kode lebih sederhana dan lebih terorganisir, memungkinkan _separation of concerns_ yang kuat.

### Open Recursion

_Methods_ sebuah _object_ dapat mengakses data dari _object_ tersebut. Banyak _programming languages_ menggunakan kata khusus, seperti `this` atau `self`, untuk merujuk pada _object_ saat ini. Dalam bahasa yang mendukung _open recursion_, sebuah _method_ di dalam sebuah _object_ dapat memanggil _methods_ lain di _object_ yang sama, termasuk dirinya sendiri, menggunakan kata khusus ini. Hal ini memungkinkan sebuah _method_ di satu _class_ memanggil _method_ lain yang didefinisikan kemudian di _subclass_, sebuah fitur yang dikenal sebagai _late binding_.

## Design Patterns

_Design patterns_ adalah solusi umum untuk masalah-masalah dalam desain perangkat lunak. Beberapa _design patterns_ sangat berguna untuk OOP, dan _design patterns_ biasanya diperkenalkan dalam konteks OOP.

### Pemodelan Dunia Nyata dan Hubungannya

Terkadang, _objects_ merepresentasikan hal-hal dan proses di dunia nyata dalam bentuk digital. Misalnya, program grafis mungkin memiliki _objects_ seperti lingkaran, persegi, dan menu. Sistem belanja online mungkin memiliki _objects_ seperti _shopping cart_, _customer_, dan _product_. Niklaus Wirth berkata, "Paradigma [OOP] ini sangat mencerminkan struktur sistem di dunia nyata dan karena itu sangat cocok untuk memodelkan sistem kompleks dengan perilaku (_behavior_) yang kompleks".

Namun, lebih sering, _objects_ merepresentasikan entitas abstrak, seperti file yang terbuka atau konverter unit. Tidak semua orang setuju bahwa OOP memudahkan untuk meniru dunia nyata secara persis atau bahwa melakukan hal itu bahkan diperlukan. Bob Martin berpendapat bahwa karena _classes_ adalah perangkat lunak, hubungan mereka tidak cocok dengan hubungan dunia nyata yang mereka representasikan. Bertrand Meyer berargumen bahwa program bukanlah model dunia melainkan model dari _sebagian_ dunia; "Realitas adalah sepupu yang jauh". Steve Yegge mencatat bahwa bahasa alami tidak memiliki pendekatan OOP yang menamai benda (_object_) sebelum tindakan (_method_), berbeda dengan _functional programming_ yang melakukan sebaliknya. Hal ini dapat membuat solusi OOP lebih kompleks daripada solusi yang ditulis melalui _procedural programming_.

### Object Patterns

Berikut adalah pola desain perangkat lunak (_software design patterns_) terkemuka untuk _objects_ OOP:

- **Function object**: _Class_ dengan satu _method_ utama yang bertindak seperti _anonymous function_ (dalam C++, merupakan _function operator_, `operator()`).
    
- **Immutable object**: Tidak mengubah _state_ setelah diciptakan.
    
- **First-class object**: Dapat digunakan tanpa batasan.
    
- **Container object**: Berisi _objects_ lainnya.
    
- **Factory object**: Menciptakan _objects_ lainnya.
    
- **Metaobject**: Digunakan untuk membuat _objects_ lain (mirip dengan _class_, tetapi merupakan sebuah _object_).
    
- **Prototype object**: _Metaobject_ khusus yang menciptakan _objects_ baru dengan menyalin dirinya sendiri.
    
- **Singleton object**: Satu-satunya _instance_ dari _class_-nya selama program berjalan.
    
- **Filter object**: Menerima aliran data sebagai inputnya dan mengubahnya menjadi output _object_.
    

_Anti-pattern_ yang umum adalah _God object_, sebuah _object_ yang mengetahui atau melakukan terlalu banyak hal.

### Gang of Four Design Patterns

_Design Patterns: Elements of Reusable Object-Oriented Software_ adalah buku terkenal yang diterbitkan pada tahun 1994 oleh empat penulis: Erich Gamma, Richard Helm, Ralph Johnson, dan John Vlissides. Orang-orang sering menyebut mereka sebagai "Gang of Four". Buku ini membahas tentang kekuatan dan kelemahan OOP serta menjelaskan 23 cara umum untuk memecahkan masalah pemrograman.

Solusi-solusi ini, yang disebut _design patterns_, dikelompokkan ke dalam tiga tipe:

1. **Creational patterns (5)**: _Factory method pattern, Abstract factory pattern, Singleton pattern, Builder pattern, Prototype pattern_.
    
2. **Structural patterns (7)**: _Adapter pattern, Bridge pattern, Composite pattern, Decorator pattern, Facade pattern, Flyweight pattern, Proxy pattern_.
    
3. **Behavioral patterns (11)**: _Chain-of-responsibility pattern, Command pattern, Interpreter pattern, Iterator pattern, Mediator pattern, Memento pattern, Observer pattern, State pattern, Strategy pattern, Template method pattern, Visitor pattern_.
    

## Object-orientation dan Databases

Baik OOP maupun Relational Database Management Systems (RDBMS) banyak digunakan dalam perangkat lunak saat ini. Namun, basis data relasional tidak menyimpan _objects_ secara langsung, yang menciptakan tantangan saat menggunakannya secara bersamaan. Masalah ini disebut _object-relational impedance mismatch_.

Untuk memecahkan masalah ini, para pengembang menggunakan metode yang berbeda-beda, tetapi tidak ada yang sempurna. Salah satu solusi paling umum adalah _Object-Relational Mapping_ (ORM), yang membantu menghubungkan program _object-oriented_ ke basis data relasional. Contoh alat ORM termasuk Visual FoxPro, Java Data Objects, dan Ruby on Rails ActiveRecord.

Beberapa basis data, yang disebut _object databases_, dirancang khusus untuk bekerja dengan OOP. Namun, mereka belum sepopuler atau sesukses basis data relasional.

Date dan Darwen telah mengusulkan dasar teoretis yang menggunakan OOP sebagai semacam sistem tipe (_type system_) yang dapat disesuaikan untuk mendukung RDBMS, tetapi ini melarang _objects_ yang berisi _pointers_ ke _objects_ lain.

## Responsibility- vs. Data-driven Design

Dalam _responsibility-driven design_, _classes_ dibangun di sekitar apa yang harus mereka lakukan dan informasi yang mereka bagikan, dalam bentuk sebuah kontrak (_contract_). Hal ini berbeda dengan _data-driven design_, di mana _classes_ dibangun berdasarkan data yang perlu mereka simpan. Menurut Wirfs-Brock dan Wilkerson, pencetus _responsibility-driven design_, pendekatan _responsibility-driven design_ merupakan pendekatan yang lebih baik.

## Panduan SOLID dan GRASP

**SOLID** adalah seperangkat lima aturan untuk mendesain perangkat lunak yang baik, dibuat oleh Michael Feathers:

- **Single responsibility principle**: Sebuah _class_ seharusnya hanya memiliki satu alasan untuk berubah.
    
- **Open/closed principle**: Entitas perangkat lunak harus terbuka untuk ekstensi (_extension_), tetapi tertutup untuk modifikasi.
    
- **Liskov substitution principle**: _Functions_ yang menggunakan _pointers_ atau referensi ke _base classes_ harus dapat menggunakan _objects_ dari _derived classes_ tanpa menyadarinya.
    
- **Interface segregation principle**: _Clients_ tidak boleh dipaksa untuk bergantung pada antarmuka (_interfaces_) yang tidak mereka gunakan.
    
- **Dependency inversion principle**: Bergantung pada abstraksi (_abstractions_), bukan pada konkrit (_concretes_).
    

**GRASP** (General Responsibility Assignment Software Patterns) adalah set aturan desain perangkat lunak lain, diciptakan oleh Craig Larman, yang membantu pengembang menetapkan tanggung jawab ke berbagai bagian program:

- **Creator Principle**: Memungkinkan _classes_ menciptakan _objects_ yang berhubungan erat dengan mereka.
    
- **Information Expert Principle**: Menugaskan tugas kepada _classes_ dengan informasi yang dibutuhkan.
    
- **Low Coupling Principle**: Mengurangi ketergantungan _class_ (_class dependencies_) untuk meningkatkan fleksibilitas dan kemudahan pemeliharaan (_maintainability_).
    
- **High Cohesion Principle**: Mendesain _classes_ dengan tanggung jawab tunggal dan fokus.
    
- **Controller Principle**: Menugaskan operasi sistem ke _classes_ terpisah yang mengelola alur dan interaksi.
    
- **Polymorphism**: Memungkinkan _classes_ berbeda untuk digunakan melalui _interface_ umum, mempromosikan fleksibilitas dan _reuse_.
    
- **Pure Fabrication Principle**: Membuat _helper classes_ untuk memperbaiki desain, meningkatkan _cohesion_, dan mengurangi _coupling_.
    

## Formal Semantics

Para peneliti telah mencoba mendefinisikan semantik dari OOP secara formal. _Inheritance_ menghadirkan kesulitan, terutama dengan interaksi antara _open recursion_ dan _encapsulated state_. Peneliti telah menggunakan _recursive types_ dan _co-algebraic data types_ untuk menggabungkan fitur-fitur penting dari OOP. Abadi dan Cardelli mendefinisikan beberapa ekstensi dari System F<: yang menangani _mutable objects_, mengizinkan baik _subtype polymorphism_ maupun _parametric polymorphism_ (_generics_), dan mampu secara formal memodelkan banyak konsep dan konstruksi OOP. Meskipun jauh dari sepele, _static analysis_ dari bahasa pemrograman _object-oriented_ seperti Java merupakan bidang yang sudah matang (_mature_), dengan beberapa alat komersial yang tersedia.

## Popularitas dan Penerimaan

Banyak _programming languages_ populer, seperti C++, Java, dan Python, menggunakan OOP. Di masa lalu, OOP diterima secara luas, namun baru-baru ini, beberapa programmer mengkritiknya dan lebih memilih _functional programming_. Sebuah studi oleh Potok et al. tidak menemukan perbedaan produktivitas yang besar antara OOP dan _procedural programming_.

Beberapa orang percaya bahwa OOP terlalu fokus pada penggunaan _objects_ daripada algoritma dan struktur data. Misalnya, programmer Rob Pike menunjukkan bahwa OOP dapat membuat programmer lebih memikirkan hierarki tipe (_type hierarchy_) daripada _composition_. Dia menyebut OOP sebagai "angka romawi dalam komputasi". Rich Hickey, pencipta Clojure, menggambarkan OOP terlalu sederhana, terutama ketika datang untuk merepresentasikan hal-hal dunia nyata yang berubah seiring waktu. Alexander Stepanov mengatakan bahwa OOP mencoba memasukkan semuanya ke dalam satu tipe, yang dapat membatasi. Dia berpendapat bahwa terkadang kita membutuhkan _multisorted algebras_: kelompok _interfaces_ yang mencakup berbagai tipe, seperti dalam _generic programming_. Stepanov juga mengatakan bahwa menyebut segala sesuatu sebagai "_object_" tidak menambah banyak pemahaman.

OOP diciptakan untuk membuat kode lebih mudah digunakan kembali (_reuse_) dan dipelihara. Namun, itu tidak dirancang untuk secara jelas menunjukkan alur instruksi program; tugas tersebut diserahkan kepada _compiler_. Seiring dengan semakin banyaknya penggunaan _parallel processing_ dan _multiple threads_ oleh komputer, menjadi lebih penting untuk memahami dan mengontrol bagaimana aliran instruksi. Hal ini dinilai sulit dilakukan dengan OOP.

Paul Graham percaya perusahaan besar menyukai OOP karena hal itu membantu mengelola tim besar yang terdiri dari programmer rata-rata. Ia berargumen bahwa OOP menambahkan struktur, membuat lebih sulit bagi satu orang untuk membuat kesalahan serius, tetapi pada saat yang sama menahan (_restrains_) programmer yang cerdas. Eric S. Raymond, seorang programmer Unix dan advokat perangkat lunak sumber terbuka (_open-source_), berargumen bahwa OOP bukanlah cara terbaik untuk menulis program.

Richard Feldman mengatakan bahwa, meskipun fitur OOP membantu beberapa bahasa tetap terorganisir, popularitas mereka berasal dari alasan lain. Lawrence Krubner berpendapat bahwa OOP tidak menawarkan keuntungan khusus dibandingkan dengan gaya lain, seperti _functional programming_, dan dapat merumitkan pengkodean. Luca Cardelli mengatakan bahwa OOP lebih lambat dan membutuhkan waktu _compile_ yang lebih lama dibandingkan dengan _procedural programming_.