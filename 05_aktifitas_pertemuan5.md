# RENCANA PEMBELAJARAN SEMESTER (RPS)
## PERTEMUAN KE-5 — RENCANA PELAKSANAAN PEMBELAJARAN (RPP)
### PEMROGRAMAN BERORIENTASI OBJEK (OBJECT-ORIENTED PROGRAMMING)
### “Abstraksi dan Interface — Menyembunyikan Kompleksitas, Mendefinisikan Kontrak”

---

## A. IDENTITAS PERTEMUAN

| **Komponen** | **Keterangan** |
|---|---|
| **Pertemuan Ke-** | 5 |
| **Topik** | Abstraksi (Abstraction) — Abstract Class, Interface, Perbedaan Abstract Class vs Interface, Multiple Interface Implementation, Default Method, dan Sealed Class |
| **Durasi** | 8 Jam Praktik (480 menit) |
| **Hari/Tanggal** | [Disesuaikan] |
| **Ruang** | Laboratorium Komputer |
| **Dosen** | [Nama Dosen] |
| **Capaian Pembelajaran** | Mahasiswa memahami konsep abstraksi dalam OOP, mampu mengimplementasikan abstract class dan interface di Kotlin, memahami perbedaan keduanya, mampu mengimplementasikan multiple interface, memahami default method, serta mampu menerapkan abstraksi dalam studi kasus nyata |

---

## B. CAPAIAN PEMBELAJARAN PERTEMUAN (CPP)

Setelah mengikuti pertemuan ke-5 ini, mahasiswa mampu:

1. **CPP 5.1:** Menjelaskan konsep abstraksi dan manfaatnya dalam pemrograman berorientasi objek.
2. **CPP 5.2:** Mendefinisikan dan mengimplementasikan abstract class di Kotlin menggunakan keyword `abstract`.
3. **CPP 5.3:** Mendefinisikan dan mengimplementasikan interface di Kotlin menggunakan keyword `interface`.
4. **CPP 5.4:** Membedakan antara abstract class dan interface serta menentukan kapan menggunakan masing-masing.
5. **CPP 5.5:** Mengimplementasikan multiple interface pada sebuah kelas.
6. **CPP 5.6:** Menggunakan default method di interface (metode dengan implementasi).
7. **CPP 5.7:** Menyelesaikan konflik overriding ketika mengimplementasikan multiple interface yang memiliki metode dengan signature yang sama.
8. **CPP 5.8:** Memahami dan menggunakan sealed class untuk closed polymorphism.
9. **CPP 5.9:** Menerapkan abstraksi dalam studi kasus nyata (sistem perangkat elektronik/manajemen karyawan).

---

## C. MATERI POKOK

### 1. Pendahuluan: Apa itu Abstraksi? (Sesi 1)

#### 1.1 Definisi Abstraksi

**Abstraksi (Abstraction)** adalah salah satu dari **empat pilar utama OOP** yang berarti **menyembunyikan detail implementasi** dan **hanya menampilkan fitur-fitur esensial** dari sebuah objek.

> **Definisi Sederhana:** Abstraksi adalah kemampuan untuk **menyembunyikan kompleksitas** dan **hanya menampilkan apa yang perlu diketahui** oleh pengguna. Pengguna tidak perlu tahu *bagaimana* sesuatu bekerja, hanya *apa* yang bisa dilakukan.

#### 1.2 Analogi Abstraksi dalam Kehidupan Nyata

| **Analogi** | **Penjelasan** |
|---|---|
| **Mengemudi Mobil** | Anda tahu cara mengemudi (setir, gas, rem) tanpa perlu tahu bagaimana mesin, transmisi, atau sistem bahan bakar bekerja di dalamnya. |
| **Menggunakan ATM** | Anda tahu cara mengambil uang (masukkan kartu, PIN, pilih jumlah) tanpa perlu tahu bagaimana sistem perbankan memproses transaksi di belakang layar. |
| **Menggunakan Smartphone** | Anda tahu cara menggunakan aplikasi (geser, tap, swipe) tanpa perlu tahu kode sumber atau arsitektur sistem operasinya. |
| **Memesan Makanan di Restoran** | Anda tahu cara memesan dari menu tanpa perlu tahu bagaimana koki memasak di dapur. |

#### 1.3 Mengapa Abstraksi Penting?

| **Manfaat** | **Penjelasan** |
|---|---|
| **Menyederhanakan Kompleksitas** | Pengguna hanya perlu memahami interface, bukan implementasi |
| **Meningkatkan Maintainability** | Perubahan implementasi tidak mempengaruhi kode yang bergantung pada abstraksi |
| **Meningkatkan Reusability** | Abstraksi memungkinkan kode digunakan kembali dalam konteks yang berbeda |
| **Mendukung Polymorphism** | Abstraksi adalah fondasi untuk polimorfisme |
| **Membuat Kode Lebih Modular** | Setiap komponen memiliki tanggung jawab yang jelas |

#### 1.4 Dua Cara Menerapkan Abstraksi di Kotlin

Kotlin menyediakan **dua mekanisme** untuk menerapkan abstraksi:

| **Mekanisme** | **Keyword** | **Tujuan** |
|---|---|---|
| **Abstract Class** | `abstract class` | Menyediakan **kerangka dasar** dengan beberapa implementasi dan beberapa yang belum diimplementasikan |
| **Interface** | `interface` | Mendefinisikan **kontrak perilaku** tanpa implementasi (atau dengan default implementation) |

---

### 2. Abstract Class di Kotlin (Sesi 1-2)

#### 2.1 Apa itu Abstract Class?

**Abstract class** adalah kelas yang **tidak bisa di-instansiasi** (tidak bisa dibuat objeknya secara langsung). Abstract class digunakan sebagai **kerangka dasar** untuk kelas-kelas turunannya.

> **Definisi:** Abstract class adalah "setengah jadi" — kelas yang sudah memiliki beberapa implementasi, tetapi masih memiliki bagian-bagian yang harus dilengkapi oleh subclass.

#### 2.2 Karakteristik Abstract Class

| **Karakteristik** | **Penjelasan** | **Contoh** |
|---|---|---|
| **Tidak bisa di-instansiasi** | Tidak bisa membuat objek langsung dari abstract class | `val animal = Animal()` → ❌ ERROR |
| **Dapat memiliki constructor** | Abstract class bisa memiliki primary/secondary constructor | `abstract class Animal(val name: String)` |
| **Dapat memiliki state** | Bisa memiliki properti dengan backing field (`var`/`val`) | `var age: Int = 0` |
| **Dapat memiliki metode konkret** | Bisa memiliki metode dengan implementasi lengkap | `fun eat() { println("Eating...") }` |
| **Dapat memiliki metode abstrak** | Metode tanpa implementasi yang harus di-override oleh subclass | `abstract fun makeSound()` |
| **Single inheritance** | Sebuah kelas hanya bisa mewarisi satu abstract class | `class Dog : Animal()` |

#### 2.3 Sintaks Abstract Class

```kotlin
// Abstract class dengan constructor
abstract class Animal(val name: String) {
    // Properti dengan state — bisa memiliki backing field
    var age: Int = 0

    // Metode konkret — memiliki implementasi
    fun eat() {
        println("$name is eating...")
    }

    // Metode abstrak — tidak memiliki implementasi
    // Harus di-override oleh subclass
    abstract fun makeSound()

    // Metode abstrak dengan parameter
    abstract fun move(distance: Double)
}

// Subclass — harus mengimplementasikan semua metode abstrak
class Dog(name: String) : Animal(name) {
    override fun makeSound() {
        println("$name barks: Guk! Guk!")
    }

    override fun move(distance: Double) {
        println("$name runs $distance meters")
    }
}

fun main() {
    // val animal = Animal("Buddy")  // ❌ ERROR: Cannot create an instance of an abstract class
    val dog = Dog("Buddy")
    dog.eat()        // Output: Buddy is eating...
    dog.makeSound()  // Output: Buddy barks: Guk! Guk!
    dog.move(10.0)   // Output: Buddy runs 10.0 meters
}
```

#### 2.4 Abstract Class dengan Constructor dan Properti

```kotlin
abstract class Vehicle(
    val brand: String,
    val model: String,
    val year: Int
) {
    // Properti dengan state
    var mileage: Double = 0.0

    // Properti abstrak — harus di-override oleh subclass
    abstract val maxSpeed: Int

    // Metode konkret
    fun displayInfo() {
        println("$brand $model ($year) - Max Speed: $maxSpeed km/h")
        println("Mileage: $mileage km")
    }

    // Metode abstrak
    abstract fun startEngine()
    abstract fun stopEngine()
    abstract fun drive(distance: Double)
}

class Car(
    brand: String,
    model: String,
    year: Int,
    override val maxSpeed: Int,
    val numberOfDoors: Int
) : Vehicle(brand, model, year) {

    private var isEngineRunning: Boolean = false

    override fun startEngine() {
        isEngineRunning = true
        println("$brand $model engine started")
    }

    override fun stopEngine() {
        isEngineRunning = false
        println("$brand $model engine stopped")
    }

    override fun drive(distance: Double) {
        if (!isEngineRunning) {
            println("Cannot drive: engine is not running")
            return
        }
        mileage += distance
        println("$brand $model drove $distance km. Total mileage: $mileage km")
    }
}

fun main() {
    val car = Car("Toyota", "Avanza", 2023, 180, 4)
    car.displayInfo()
    car.startEngine()
    car.drive(50.0)
    car.drive(30.0)
    car.stopEngine()
}
```

#### 2.5 Kapan Menggunakan Abstract Class?

| **Skenario** | **Penjelasan** |
|---|---|
| **Memiliki state yang harus dibagi** | Abstract class bisa menyimpan state (`var`/`val`) yang diwarisi oleh subclass |
| **Memiliki constructor** | Abstract class bisa memiliki constructor untuk inisialisasi |
| **Memiliki metode konkret yang reusable** | Abstract class bisa menyediakan implementasi default untuk beberapa metode |
| **Membutuhkan protected members** | Abstract class bisa memiliki member `protected` yang hanya bisa diakses oleh subclass |
| **Hubungan "IS-A" yang kuat** | Ketika subclass benar-benar adalah tipe dari superclass |

---

### 3. Interface di Kotlin (Sesi 2)

#### 3.1 Apa itu Interface?

**Interface** adalah **kontrak** atau **perjanjian** yang mendefinisikan **apa yang harus dilakukan** oleh sebuah kelas, tanpa mendefinisikan **bagaimana** melakukannya.

> **Definisi:** Interface adalah "daftar janji" — sebuah kelas yang mengimplementasikan interface berjanji untuk menyediakan implementasi untuk semua metode yang dideklarasikan di interface.

#### 3.2 Karakteristik Interface

| **Karakteristik** | **Penjelasan** | **Contoh** |
|---|---|---|
| **Tidak bisa di-instansiasi** | Tidak bisa membuat objek langsung dari interface | `val device = InputDevice()` → ❌ ERROR |
| **Tidak memiliki constructor** | Interface tidak bisa memiliki constructor | `interface InputDevice { ... }` |
| **Tidak bisa menyimpan state** | Interface tidak bisa memiliki backing field | Tidak bisa `var x: Int = 0` di interface |
| **Dapat memiliki properti** | Tapi harus abstrak atau memiliki accessor | `val version: String` atau `val name: String get() = "..."` |
| **Dapat memiliki metode abstrak** | Metode tanpa implementasi | `fun input(event: Any)` |
| **Dapat memiliki default method** | Metode dengan implementasi (sejak Kotlin 1.2/1.4) | `fun foo() { println("default") }` |
| **Multiple inheritance** | Sebuah kelas bisa mengimplementasikan banyak interface | `class C : A, B` |

#### 3.3 Sintaks Interface

```kotlin
// Mendefinisikan interface
interface InputDevice {
    // Properti abstrak — harus di-override oleh implementor
    val version: String

    // Properti dengan accessor — tidak memiliki backing field
    val name: String
        get() = "Input Device v$version"

    // Metode abstrak — tidak memiliki implementasi
    fun input(event: Any)

    // Default method — memiliki implementasi
    fun onLowPower() {
        println("⚠️ Warning: Device is running low on power")
    }
}

// Mengimplementasikan interface
class Keyboard(override val version: String) : InputDevice {
    override fun input(event: Any) {
        println("⌨️ Keyboard input: $event")
    }

    // Optional: override default method
    override fun onLowPower() {
        println("⌨️ Keyboard battery is low!")
    }
}

class Mouse(override val version: String) : InputDevice {
    override fun input(event: Any) {
        println("🖱️ Mouse input: $event")
    }
    // onLowPower() menggunakan implementasi default
}

fun main() {
    val keyboard = Keyboard("1.0")
    val mouse = Mouse("2.0")

    keyboard.input("Hello")  // Output: ⌨️ Keyboard input: Hello
    keyboard.onLowPower()    // Output: ⌨️ Keyboard battery is low!

    mouse.input("Click")     // Output: 🖱️ Mouse input: Click
    mouse.onLowPower()       // Output: ⚠️ Warning: Device is running low on power
}
```

#### 3.4 Properti di Interface

Properti di interface **tidak bisa memiliki backing field** — mereka harus abstrak atau memiliki accessor.

```kotlin
interface MyInterface {
    // ✅ Properti abstrak — harus di-override
    val id: String

    // ✅ Properti dengan getter — tidak ada backing field
    val name: String
        get() = "Item $id"

    // ✅ Properti dengan getter dan setter — tidak ada backing field
    var counter: Int
        get() = 0
        set(value) { /* custom logic */ }

    // ❌ ERROR: Property initializers are not allowed in interfaces
    // val version: String = "1.0"

    // ❌ ERROR: Backing field not allowed
    // var count: Int = 0
}

class MyClass(override val id: String) : MyInterface {
    // counter harus di-override atau menggunakan implementasi default
    override var counter: Int = 0
}
```

#### 3.5 Kapan Menggunakan Interface?

| **Skenario** | **Penjelasan** |
|---|---|
| **Mendefinisikan perilaku** | Interface mendefinisikan "apa" yang bisa dilakukan, bukan "bagaimana" |
| **Multiple inheritance** | Ketika sebuah kelas perlu memiliki perilaku dari berbagai sumber |
| **Kontrak untuk API** | Interface mendefinisikan kontrak antara berbagai komponen |
| **Polimorfisme** | Interface memungkinkan polimorfisme tanpa inheritance |
| **Dependency Injection** | Interface memungkinkan decoupling antara komponen |

---

### 4. Perbedaan Abstract Class vs Interface (Sesi 2-3)

#### 4.1 Perbandingan Mendetail

| **Aspek** | **Abstract Class** | **Interface** |
|---|---|---|
| **Keyword** | `abstract class` | `interface` |
| **Instansiasi** | ❌ Tidak bisa | ❌ Tidak bisa |
| **Constructor** | ✅ Bisa memiliki constructor | ❌ Tidak bisa |
| **State (Backing Field)** | ✅ Bisa menyimpan state | ❌ Tidak bisa menyimpan state |
| **Properti** | Bisa memiliki properti dengan backing field | Hanya abstrak atau dengan accessor |
| **Metode Konkret** | ✅ Bisa | ✅ Bisa (default method) |
| **Metode Abstrak** | ✅ Bisa | ✅ Bisa |
| **Inheritance** | Single inheritance (satu abstract class) | Multiple inheritance (banyak interface) |
| **Access Modifier** | Bisa menggunakan `private`, `protected`, `internal`, `public` | Hanya `public` (default) dan `private` |
| **Tujuan** | Mendefinisikan "bagaimana" (How) | Mendefinisikan "apa" (What) |

#### 4.2 Kapan Menggunakan Abstract Class vs Interface?

| **Situasi** | **Pilihan** | **Alasan** |
|---|---|---|
| **Perlu menyimpan state** | Abstract Class | Interface tidak bisa menyimpan state |
| **Perlu constructor untuk inisialisasi** | Abstract Class | Interface tidak memiliki constructor |
| **Perlu multiple behavior dari berbagai sumber** | Interface | Sebuah kelas bisa mengimplementasikan banyak interface |
| **Hubungan "IS-A" yang kuat** | Abstract Class | Contoh: `Dog IS-A Animal` |
| **Hubungan "CAN-DO" (perilaku)** | Interface | Contoh: `Dog CAN-DO Swimmable` |
| **Membutuhkan protected members** | Abstract Class | Interface tidak mendukung `protected` |
| **Membutuhkan final members** | Abstract Class | Interface tidak mendukung `final` |

#### 4.3 Contoh Perbandingan

```kotlin
// ============================================================
// ABSTRACT CLASS — mendefinisikan "bagaimana" (How)
// ============================================================
abstract class Animal(val name: String) {
    // ✅ Bisa menyimpan state
    var age: Int = 0

    // ✅ Bisa memiliki constructor
    init {
        println("Animal $name created")
    }

    // ✅ Bisa memiliki metode konkret
    fun eat() {
        println("$name is eating...")
    }

    // ✅ Bisa memiliki metode abstrak
    abstract fun makeSound()
}

// ============================================================
// INTERFACE — mendefinisikan "apa" (What)
// ============================================================
interface Swimmable {
    // ❌ Tidak bisa menyimpan state
    // ❌ Tidak bisa memiliki constructor

    // ✅ Bisa memiliki properti abstrak
    val swimSpeed: Double

    // ✅ Bisa memiliki default method
    fun swim() {
        println("Swimming at $swimSpeed km/h")
    }
}

interface Flyable {
    val flySpeed: Double

    fun fly() {
        println("Flying at $flySpeed km/h")
    }
}

// ============================================================
// CLASS — mengimplementasikan kedua interface dan mewarisi abstract class
// ============================================================
class Duck(name: String) : Animal(name), Swimmable, Flyable {
    override val swimSpeed: Double = 5.0
    override val flySpeed: Double = 40.0

    override fun makeSound() {
        println("$name says: Quack! Quack!")
    }

    // Optional: override default methods
    override fun swim() {
        println("🦆 $name is swimming gracefully at $swimSpeed km/h")
    }
}

fun main() {
    val duck = Duck("Donald")
    duck.eat()          // Dari abstract class
    duck.makeSound()    // Dari abstract class (di-override)
    duck.swim()         // Dari interface (di-override)
    duck.fly()          // Dari interface (default)
}
```

---

### 5. Multiple Interface Implementation (Sesi 3)

#### 5.1 Konsep Multiple Interface

Kotlin mendukung **multiple interface implementation** — sebuah kelas bisa mengimplementasikan **lebih dari satu interface**.

```kotlin
interface A {
    fun methodA()
}

interface B {
    fun methodB()
}

interface C {
    fun methodC()
}

// Sebuah kelas bisa mengimplementasikan banyak interface
class MyClass : A, B, C {
    override fun methodA() {
        println("Method A")
    }

    override fun methodB() {
        println("Method B")
    }

    override fun methodC() {
        println("Method C")
    }
}
```

#### 5.2 Multiple Interface dengan Default Method

```kotlin
interface Printable {
    fun print() {
        println("Printing...")
    }
}

interface Scannable {
    fun scan() {
        println("Scanning...")
    }
}

interface Faxable {
    fun fax() {
        println("Faxing...")
    }
}

// Multi-function printer mengimplementasikan 3 interface
class MultiFunctionPrinter : Printable, Scannable, Faxable {
    // Semua metode menggunakan implementasi default dari interface
    // Tapi kita bisa meng-override jika perlu
    override fun print() {
        println("📄 Multi-function printer is printing in color...")
    }
}

fun main() {
    val mfp = MultiFunctionPrinter()
    mfp.print()   // Output: 📄 Multi-function printer is printing in color...
    mfp.scan()    // Output: Scanning...
    mfp.fax()     // Output: Faxing...
}
```

---

### 6. Resolving Overriding Conflicts (Sesi 3)

#### 6.1 Masalah Konflik Overriding

Ketika sebuah kelas mengimplementasikan **dua interface atau lebih** yang memiliki **metode dengan signature yang sama**, terjadi **konflik overriding**.

```kotlin
interface A {
    fun foo() {
        println("A.foo()")
    }
}

interface B {
    fun foo() {
        println("B.foo()")
    }
}

// ❌ ERROR: Class 'C' must override 'foo()' because it inherits multiple implementations
class C : A, B {
    // Harus meng-override foo() untuk menyelesaikan konflik
    override fun foo() {
        // Memanggil implementasi dari A
        super<A>.foo()
        // Memanggil implementasi dari B
        super<B>.foo()
        // Atau implementasi sendiri
        println("C.foo()")
    }
}
```

#### 6.2 Menyelesaikan Konflik dengan `super<Interface>`

Gunakan **`super<InterfaceName>`** untuk memanggil implementasi dari interface tertentu.

```kotlin
interface Printable {
    fun print() {
        println("Printable: Printing...")
    }
}

interface Loggable {
    fun print() {
        println("Loggable: Logging...")
    }
}

class Document : Printable, Loggable {
    // Solusi 1: Meng-override dengan implementasi sendiri
    override fun print() {
        println("Document: Printing document...")
    }
}

class Report : Printable, Loggable {
    // Solusi 2: Memanggil salah satu implementasi interface
    override fun print() {
        super<Printable>.print()  // Memanggil implementasi dari Printable
        // super<Loggable>.print() // Atau dari Loggable
    }
}

class Invoice : Printable, Loggable {
    // Solusi 3: Memanggil semua implementasi
    override fun print() {
        super<Printable>.print()
        super<Loggable>.print()
        println("Invoice: Printing invoice...")
    }
}

fun main() {
    Document().print()   // Output: Document: Printing document...
    Report().print()     // Output: Printable: Printing...
    Invoice().print()    // Output: Printable: Printing... \n Loggable: Logging... \n Invoice: Printing invoice...
}
```

#### 6.3 Konflik dengan Properti

```kotlin
interface Named {
    val name: String
        get() = "Default Name"
}

interface Titled {
    val name: String
        get() = "Default Title"
}

class Book : Named, Titled {
    // Harus meng-override properti name
    override val name: String
        get() = "Book: ${super<Named>.name} / ${super<Titled>.name}"
}

fun main() {
    val book = Book()
    println(book.name)  // Output: Book: Default Name / Default Title
}
```

---

### 7. Default Method di Interface (Sesi 3-4)

#### 7.1 Apa itu Default Method?

**Default method** adalah metode di interface yang **memiliki implementasi** (body). Sejak Kotlin 1.2/1.4, interface bisa memiliki default method.

```kotlin
interface Logger {
    // Default method — memiliki implementasi
    fun log(message: String) {
        println("[${this::class.simpleName}] $message")
    }

    // Default method dengan logika lebih kompleks
    fun logError(message: String) {
        log("ERROR: $message")
    }

    fun logWarning(message: String) {
        log("WARNING: $message")
    }
}

class ApplicationLogger : Logger {
    // Menggunakan semua default method dari Logger
    // Bisa meng-override jika perlu
    override fun log(message: String) {
        println("📝 ${System.currentTimeMillis()}: $message")
    }
}

fun main() {
    val logger = ApplicationLogger()
    logger.log("Application started")        // Output: 📝 1234567890: Application started
    logger.logError("Connection failed")     // Output: 📝 1234567890: ERROR: Connection failed
    logger.logWarning("Low memory")          // Output: 📝 1234567890: WARNING: Low memory
}
```

#### 7.2 Manfaat Default Method

| **Manfaat** | **Penjelasan** |
|---|---|
| **Backward Compatibility** | Menambah metode baru ke interface tanpa merusak implementasi yang sudah ada |
| **Code Reusability** | Menyediakan implementasi default yang bisa digunakan oleh semua implementor |
| **Mengurangi Boilerplate** | Implementor tidak perlu meng-override semua metode |
| **Mendukung Evolution** | Interface bisa berevolusi seiring waktu |

#### 7.3 Default Method dengan Properti

```kotlin
interface Configurable {
    // Properti abstrak
    val configKey: String

    // Properti dengan default getter
    val configValue: String
        get() = System.getProperty(configKey) ?: "default"

    // Default method
    fun reload() {
        println("Reloading configuration for $configKey")
    }

    fun display() {
        println("$configKey = $configValue")
    }
}

class AppConfig : Configurable {
    override val configKey: String = "app.mode"
    // configValue menggunakan default getter
}

class DatabaseConfig : Configurable {
    override val configKey: String = "db.url"

    // Override configValue
    override val configValue: String
        get() = "jdbc:mysql://localhost:3306/mydb"
}

fun main() {
    val appConfig = AppConfig()
    appConfig.display()   // Output: app.mode = default
    appConfig.reload()    // Output: Reloading configuration for app.mode

    val dbConfig = DatabaseConfig()
    dbConfig.display()    // Output: db.url = jdbc:mysql://localhost:3306/mydb
}
```

---

### 8. Sealed Class — Closed Polymorphism (Sesi 4)

#### 8.1 Apa itu Sealed Class?

**Sealed class** adalah kelas yang **membatasi hierarki subclass** — semua subclass harus dideklarasikan **dalam file yang sama** dengan sealed class.

> **Closed Polymorphism:** Semua subclass dari sealed class **diketahui pada saat compile time** — compiler bisa memastikan semua kemungkinan ditangani.

#### 8.2 Sealed Class vs Abstract Class

| **Aspek** | **Sealed Class** | **Abstract Class** |
|---|---|---|
| **Subclass** | Terbatas — hanya di file yang sama | Tidak terbatas — bisa di mana saja |
| **Polymorphism** | Closed (tertutup) | Open (terbuka) |
| **`when` Expression** | Ekshaustif — compiler memastikan semua kasus ditangani | Tidak ekshaustif — perlu `else` |
| **Instansiasi** | ❌ Tidak bisa | ❌ Tidak bisa |
| **State** | ✅ Bisa | ✅ Bisa |

#### 8.3 Contoh Sealed Class

```kotlin
// Sealed class — semua subclass di file yang sama
sealed class OperationResult {
    data class Success(val data: String) : OperationResult()
    data class Error(val message: String, val code: Int) : OperationResult()
    object Loading : OperationResult()
    object Idle : OperationResult()
}

// Fungsi dengan when expression yang ekshaustif
fun handleResult(result: OperationResult): String {
    return when (result) {
        is OperationResult.Success -> "✅ Success: ${result.data}"
        is OperationResult.Error -> "❌ Error: ${result.message} (Code: ${result.code})"
        OperationResult.Loading -> "⏳ Loading..."
        OperationResult.Idle -> "💤 Idle"
        // Tidak perlu else — semua kemungkinan sudah tercakup!
    }
}

fun main() {
    val results = listOf(
        OperationResult.Success("Data loaded"),
        OperationResult.Error("Connection failed", 500),
        OperationResult.Loading,
        OperationResult.Idle
    )

    for (result in results) {
        println(handleResult(result))
    }
}
```

---

### 9. Studi Kasus: Sistem Perangkat Elektronik (Sesi 4)

Mari kita bangun sistem perangkat elektronik yang mengimplementasikan semua konsep abstraksi.

#### 9.1 Analisis Kebutuhan

| **Perangkat** | **Interface** | **Abstract Class** |
|---|---|---|
| **ElectronicDevice** | - | Abstract class dengan properti dasar |
| **Chargeable** | Interface untuk perangkat yang bisa di-charge | - |
| **Connectable** | Interface untuk perangkat yang bisa terhubung | - |
| **Smartphone** | Mewarisi ElectronicDevice, mengimplementasikan Chargeable & Connectable | - |
| **Laptop** | Mewarisi ElectronicDevice, mengimplementasikan Chargeable & Connectable | - |
| **SmartTV** | Mewarisi ElectronicDevice, mengimplementasikan Connectable | - |

#### 9.2 Implementasi Lengkap

```kotlin
/**
 * ============================================================
 * SISTEM PERANGKAT ELEKTRONIK DENGAN ABSTRAKSI
 * ============================================================
 * Demonstrasi:
 * 1. Abstract class dengan state dan constructor
 * 2. Interface dengan default method
 * 3. Multiple interface implementation
 * 4. Resolving overriding conflicts
 * 5. Sealed class untuk status perangkat
 * ============================================================
 */

// ============================================================
// SEALED CLASS: DeviceStatus
// ============================================================
sealed class DeviceStatus {
    object On : DeviceStatus()
    object Off : DeviceStatus()
    data class Error(val message: String) : DeviceStatus()
    object Charging : DeviceStatus()

    fun display(): String {
        return when (this) {
            On -> "🟢 ON"
            Off -> "🔴 OFF"
            is Error -> "❌ ERROR: ${this.message}"
            Charging -> "⚡ CHARGING"
        }
    }
}

// ============================================================
// ABSTRACT CLASS: ElectronicDevice
// ============================================================
abstract class ElectronicDevice(
    val brand: String,
    val model: String,
    val year: Int
) {
    // State — bisa disimpan di abstract class
    var status: DeviceStatus = DeviceStatus.Off
    protected var powerConsumption: Double = 0.0

    init {
        println("📱 $brand $model ($year) created")
    }

    // Metode konkret
    fun turnOn() {
        status = DeviceStatus.On
        powerConsumption = calculatePowerConsumption()
        println("✅ $brand $model turned ON (Power: ${powerConsumption}W)")
    }

    fun turnOff() {
        status = DeviceStatus.Off
        powerConsumption = 0.0
        println("✅ $brand $model turned OFF")
    }

    // Metode abstrak — harus di-override
    abstract fun calculatePowerConsumption(): Double
    abstract fun displayInfo(): String

    // Metode final — tidak bisa di-override
    final fun getStatus(): String {
        return status.display()
    }
}

// ============================================================
// INTERFACE: Chargeable
// ============================================================
interface Chargeable {
    // Properti abstrak
    val batteryLevel: Int
    val batteryCapacity: Int

    // Properti dengan default getter
    val batteryPercentage: Double
        get() = (batteryLevel.toDouble() / batteryCapacity) * 100

    // Default method
    fun charge(amount: Int) {
        println("🔋 Charging $amount%...")
        // Implementasi akan di-override di subclass
    }

    fun getBatteryStatus(): String {
        return "Battery: $batteryLevel / $batteryCapacity mAh (${"%.1f".format(batteryPercentage)}%)"
    }
}

// ============================================================
// INTERFACE: Connectable
// ============================================================
interface Connectable {
    val connectionType: String

    // Default method
    fun connect() {
        println("🔗 Connecting via $connectionType...")
    }

    fun disconnect() {
        println("🔗 Disconnecting from $connectionType...")
    }

    fun isConnected(): Boolean {
        return false  // Default: tidak terhubung
    }
}

// ============================================================
// INTERFACE: Displayable (dengan metode default)
// ============================================================
interface Displayable {
    val resolution: String

    fun display() {
        println("🖥️ Displaying at $resolution")
    }

    fun adjustBrightness(level: Int) {
        println("💡 Brightness adjusted to $level%")
    }
}

// ============================================================
// CLASS: Smartphone — mengimplementasikan multiple interfaces
// ============================================================
class Smartphone(
    brand: String,
    model: String,
    year: Int,
    override val batteryCapacity: Int,
    override val connectionType: String = "5G",
    override val resolution: String = "1080x2400"
) : ElectronicDevice(brand, model, year), Chargeable, Connectable, Displayable {

    override var batteryLevel: Int = 0
        private set

    private var connected: Boolean = false

    override fun calculatePowerConsumption(): Double {
        return when {
            status is DeviceStatus.On -> 5.0 + (batteryCapacity / 1000.0)
            status is DeviceStatus.Charging -> 10.0
            else -> 0.0
        }
    }

    override fun displayInfo(): String {
        return """
            |📱 SMARTPHONE INFO
            |Brand: $brand
            |Model: $model
            |Year: $year
            |Battery: $batteryLevel / $batteryCapacity mAh
            |Connection: $connectionType
            |Resolution: $resolution
            |Status: ${getStatus()}
        """.trimMargin()
    }

    // Implementasi Chargeable
    override fun charge(amount: Int) {
        batteryLevel = minOf(batteryLevel + amount, batteryCapacity)
        status = DeviceStatus.Charging
        println("🔋 Charging... Battery: $batteryLevel / $batteryCapacity mAh")
        if (batteryLevel >= batteryCapacity) {
            status = DeviceStatus.On
            println("✅ Battery fully charged!")
        }
    }

    // Implementasi Connectable
    override fun connect() {
        connected = true
        println("📶 Connected to $connectionType network")
    }

    override fun disconnect() {
        connected = false
        println("📶 Disconnected from $connectionType network")
    }

    override fun isConnected(): Boolean {
        return connected
    }

    // Implementasi Displayable
    override fun display() {
        println("📱 Displaying on $resolution screen")
        super.display()  // Memanggil default method dari Displayable
    }
}

// ============================================================
// CLASS: Laptop — mengimplementasikan multiple interfaces
// ============================================================
class Laptop(
    brand: String,
    model: String,
    year: Int,
    override val batteryCapacity: Int,
    override val connectionType: String = "WiFi 6",
    override val resolution: String = "1920x1080",
    val ramSize: Int
) : ElectronicDevice(brand, model, year), Chargeable, Connectable, Displayable {

    override var batteryLevel: Int = 0
        private set

    private var connected: Boolean = false

    override fun calculatePowerConsumption(): Double {
        return when {
            status is DeviceStatus.On -> 20.0 + (ramSize / 2.0)
            status is DeviceStatus.Charging -> 30.0
            else -> 0.0
        }
    }

    override fun displayInfo(): String {
        return """
            |💻 LAPTOP INFO
            |Brand: $brand
            |Model: $model
            |Year: $year
            |RAM: ${ramSize}GB
            |Battery: $batteryLevel / $batteryCapacity mAh
            |Connection: $connectionType
            |Resolution: $resolution
            |Status: ${getStatus()}
        """.trimMargin()
    }

    override fun charge(amount: Int) {
        batteryLevel = minOf(batteryLevel + amount, batteryCapacity)
        status = DeviceStatus.Charging
        println("🔋 Charging... Battery: $batteryLevel / $batteryCapacity mAh")
        if (batteryLevel >= batteryCapacity) {
            status = DeviceStatus.On
            println("✅ Battery fully charged!")
        }
    }

    override fun connect() {
        connected = true
        println("📶 Connected to $connectionType")
    }

    override fun disconnect() {
        connected = false
        println("📶 Disconnected from $connectionType")
    }

    override fun isConnected(): Boolean {
        return connected
    }

    override fun display() {
        println("💻 Displaying on $resolution screen")
    }
}

// ============================================================
// CLASS: SmartTV — mengimplementasikan Connectable dan Displayable
// ============================================================
class SmartTV(
    brand: String,
    model: String,
    year: Int,
    override val connectionType: String = "WiFi",
    override val resolution: String = "3840x2160"
) : ElectronicDevice(brand, model, year), Connectable, Displayable {

    private var connected: Boolean = false

    override fun calculatePowerConsumption(): Double {
        return when {
            status is DeviceStatus.On -> 100.0
            else -> 0.0
        }
    }

    override fun displayInfo(): String {
        return """
            |📺 SMART TV INFO
            |Brand: $brand
            |Model: $model
            |Year: $year
            |Connection: $connectionType
            |Resolution: $resolution
            |Status: ${getStatus()}
        """.trimMargin()
    }

    override fun connect() {
        connected = true
        println("📶 Connected to $connectionType")
    }

    override fun disconnect() {
        connected = false
        println("📶 Disconnected from $connectionType")
    }

    override fun isConnected(): Boolean {
        return connected
    }

    override fun display() {
        println("📺 Displaying 4K content on $resolution screen")
    }

    // Metode tambahan khusus SmartTV
    fun changeChannel(channel: Int) {
        println("📺 Changing to channel $channel")
    }
}

// ============================================================
// CLASS: DeviceManager — mengelola perangkat secara polimorfik
// ============================================================
class DeviceManager {
    private val devices = mutableListOf<ElectronicDevice>()

    fun addDevice(device: ElectronicDevice) {
        devices.add(device)
        println("✅ Device added: ${device.brand} ${device.model}")
    }

    fun turnOnAll() {
        println("🔄 Turning ON all devices...")
        for (device in devices) {
            device.turnOn()
        }
    }

    fun turnOffAll() {
        println("🔄 Turning OFF all devices...")
        for (device in devices) {
            device.turnOff()
        }
    }

    fun displayAllDevices() {
        println("=" .repeat(55))
        println("📱 ALL DEVICES")
        println("=" .repeat(55))
        for (device in devices) {
            println(device.displayInfo())
            println("-" .repeat(40))
        }
    }

    // Demonstrasi smart casting
    fun chargeAllDevices() {
        println("🔄 Charging all chargeable devices...")
        for (device in devices) {
            when (device) {
                is Smartphone -> {
                    println("📱 Charging ${device.brand} ${device.model}")
                    device.charge(20)
                }
                is Laptop -> {
                    println("💻 Charging ${device.brand} ${device.model}")
                    device.charge(15)
                }
                else -> {
                    println("⚠️ ${device.brand} ${device.model} is not chargeable")
                }
            }
        }
    }

    fun connectAllDevices() {
        println("🔄 Connecting all connectable devices...")
        for (device in devices) {
            when (device) {
                is Connectable -> {
                    device.connect()
                }
                else -> {
                    println("⚠️ ${device.brand} ${device.model} is not connectable")
                }
            }
        }
    }
}

// ============================================================
// FUNGSI UTAMA
// ============================================================
fun main() {
    println("=" .repeat(55))
    println("📱 SISTEM PERANGKAT ELEKTRONIK DENGAN ABSTRAKSI")
    println("=" .repeat(55))
    println()

    // Membuat berbagai perangkat
    val smartphone = Smartphone("Samsung", "Galaxy S24", 2024, 5000)
    val laptop = Laptop("Apple", "MacBook Pro", 2023, 6000, ramSize = 16)
    val tv = SmartTV("Sony", "BRAVIA XR", 2024)

    // Device Manager — menangani semua perangkat secara polimorfik
    val manager = DeviceManager()

    println("📥 Menambahkan perangkat...")
    println()
    manager.addDevice(smartphone)
    manager.addDevice(laptop)
    manager.addDevice(tv)

    println()
    manager.displayAllDevices()

    println()
    manager.turnOnAll()

    println()
    manager.chargeAllDevices()

    println()
    manager.connectAllDevices()

    println()
    manager.displayAllDevices()

    // Demonstrasi fitur khusus SmartTV
    println()
    println("--- FITUR KHUSUS SMART TV ---")
    tv.changeChannel(5)

    // Demonstrasi sealed class
    println()
    println("--- DEMONSTRASI SEALED CLASS ---")
    val statuses = listOf(
        DeviceStatus.On,
        DeviceStatus.Off,
        DeviceStatus.Error("Overheating"),
        DeviceStatus.Charging
    )
    for (status in statuses) {
        println(status.display())
    }

    // Demonstrasi bahwa kita bisa memeriksa tipe perangkat
    println()
    println("--- DEMONSTRASI TYPE CHECKING ---")
    val devices: List<ElectronicDevice> = listOf(smartphone, laptop, tv)
    for (device in devices) {
        when (device) {
            is Smartphone -> println("📱 ${device.brand} ${device.model} is a Smartphone")
            is Laptop -> println("💻 ${device.brand} ${device.model} is a Laptop")
            is SmartTV -> println("📺 ${device.brand} ${device.model} is a Smart TV")
        }
    }

    println()
    println("=" .repeat(55))
    println("🏁 PROGRAM SELESAI")
    println("=" .repeat(55))
}
```

---

## D. RINCIAN KEGIATAN PEMBELAJARAN (8 JAM)

### Sesi 1: Pengantar Abstraksi & Abstract Class (2 Jam — 120 menit)

| **Waktu** | **Kegiatan** | **Detail** | **Metode** |
|---|---|---|---|
| **0-10'** | Pembukaan & Review | • Dosen membuka perkuliahan dengan salam dan doa<br>• Review singkat materi pertemuan 4 (polimorfisme, overriding, casting)<br>• Menghubungkan polimorfisme dengan abstraksi | Ceramah interaktif, Tanya jawab |
| **10-35'** | Konsep Abstraksi | • **Definisi abstraksi** — menyembunyikan kompleksitas, menampilkan esensi<br>• **Analogi abstraksi** (mobil, ATM, smartphone, restoran)<br>• **Manfaat abstraksi** — menyederhanakan, maintainability, reusability<br>• **Dua mekanisme abstraksi di Kotlin**: abstract class dan interface<br>• **Abstract class** — "setengah jadi" dengan beberapa implementasi<br>• **Interface** — kontrak perilaku tanpa state | Ceramah, Analogi, Diskusi |
| **35-65'** | Abstract Class | • **Karakteristik abstract class**:<br>  - Tidak bisa di-instansiasi<br>  - Bisa memiliki constructor<br>  - Bisa memiliki state (backing field)<br>  - Bisa memiliki metode konkret dan abstrak<br>  - Single inheritance<br>• **Sintaks** `abstract class`<br>• **Metode abstrak** — harus di-override oleh subclass<br>• **Metode konkret** — bisa digunakan langsung oleh subclass<br>• **Demo**: Abstract class `Animal` dengan subclass `Dog` dan `Cat` | Ceramah, Demonstrasi, Live Coding |
| **65-85'** | Praktik Abstract Class | • Mahasiswa membuat abstract class `Vehicle`<br>• Membuat subclass `Car`, `Motorcycle`, `Truck`<br>• Mengimplementasikan metode abstrak dan menggunakan metode konkret<br>• Mengamati bahwa abstract class tidak bisa di-instansiasi | Praktik terbimbing |
| **85-105'** | Diskusi & Review | • Diskusi kelompok: "Kapan menggunakan abstract class?"<br>• Dosen memberikan contoh kasus nyata<br>• Q&A | Diskusi kelompok, Tanya jawab |
| **105-120'** | Persiapan Sesi 2 | • Dosen memberikan pengantar tentang interface<br>• Menjelaskan bahwa interface adalah "kontrak" perilaku | Ceramah |

---

### Sesi 2: Interface & Perbandingan dengan Abstract Class (2 Jam — 120 menit)

| **Waktu** | **Kegiatan** | **Detail** | **Metode** |
|---|---|---|---|
| **0-10'** | Review & Motivasi | • Mereview abstract class<br>• "Bagaimana jika kita ingin mendefinisikan perilaku tanpa state?" | Ceramah |
| **10-45'** | Interface | • **Karakteristik interface**:<br>  - Tidak bisa di-instansiasi<br>  - Tidak memiliki constructor<br>  - Tidak bisa menyimpan state (tidak ada backing field)<br>  - Bisa memiliki properti abstrak atau dengan accessor<br>  - Bisa memiliki metode abstrak dan default method<br>  - Multiple inheritance<br>• **Sintaks** `interface`<br>• **Properti di interface** — tidak bisa memiliki backing field<br>• **Default method** — metode dengan implementasi<br>• **Demo**: Interface `InputDevice` dengan implementasi `Keyboard` dan `Mouse` | Ceramah, Demonstrasi, Live Coding |
| **45-75'** | Perbandingan Abstract Class vs Interface | • **Tabel perbandingan** — state, constructor, inheritance, access modifier<br>• **Kapan menggunakan abstract class**:<br>  - Perlu menyimpan state<br>  - Perlu constructor<br>  - Hubungan "IS-A" yang kuat<br>• **Kapan menggunakan interface**:<br>  - Mendefinisikan perilaku (What, bukan How)<br>  - Multiple inheritance<br>  - Kontrak untuk API<br>• **Demo**: Membandingkan implementasi yang sama dengan abstract class vs interface | Ceramah, Demonstrasi, Diskusi |
| **75-95'** | Praktik Interface | • Mahasiswa membuat interface `Swimmable` dan `Flyable`<br>• Membuat kelas `Duck` yang mengimplementasikan kedua interface<br>• Mengamati penggunaan default method | Praktik mandiri, Asistensi |
| **95-120'** | Diskusi & Review | • Diskusi kelompok: "Abstract class vs Interface — kapan menggunakan masing-masing?"<br>• Dosen memberikan panduan praktis<br>• Q&A dan penyimpulan | Diskusi kelompok, Tanya jawab |

---

### Sesi 3: Multiple Interface, Overriding Conflicts, & Default Method (2 Jam — 120 menit)

| **Waktu** | **Kegiatan** | **Detail** | **Metode** |
|---|---|---|---|
| **0-10'** | Review & Motivasi | • Review interface dan perbedaannya dengan abstract class<br>• "Bagaimana jika sebuah kelas perlu mengimplementasikan banyak interface?" | Ceramah |
| **10-40'** | Multiple Interface Implementation | • **Konsep** — sebuah kelas bisa mengimplementasikan banyak interface<br>• **Sintaks** — `class MyClass : InterfaceA, InterfaceB, InterfaceC`<br>• **Demo**: Multi-function printer mengimplementasikan `Printable`, `Scannable`, `Faxable` | Ceramah, Demonstrasi, Live Coding |
| **40-70'** | Resolving Overriding Conflicts | • **Masalah** — dua interface dengan metode signature yang sama<br>• **Solusi 1**: Override dengan implementasi sendiri<br>• **Solusi 2**: Panggil salah satu implementasi dengan `super<Interface>`<br>• **Solusi 3**: Panggil semua implementasi<br>• **Demo**: Interface `A` dan `B` dengan metode `foo()` yang sama | Ceramah, Demonstrasi, Live Coding |
| **70-90'** | Default Method | • **Konsep default method** — metode dengan implementasi di interface<br>• **Manfaat**: backward compatibility, code reusability<br>• **Demo**: Interface `Logger` dengan default method `log()`, `logError()`, `logWarning()`<br>• **Properti dengan default accessor** | Ceramah, Demonstrasi |
| **90-110'** | Praktik Multiple Interface & Conflicts | • Mahasiswa membuat interface `A` dan `B` dengan metode `foo()`<br>• Membuat kelas `C` yang mengimplementasikan keduanya<br>• Menyelesaikan konflik overriding dengan berbagai cara<br>• Dosen memberikan asistensi | Praktik mandiri, Asistensi |
| **110-120'** | Diskusi & Review | • Diskusi: "Bagaimana default method membantu evolusi interface?"<br>• Q&A | Diskusi, Tanya jawab |

---

### Sesi 4: Sealed Class & Studi Kasus (2 Jam — 120 menit)

| **Waktu** | **Kegiatan** | **Detail** | **Metode** |
|---|---|---|---|
| **0-10'** | Review & Motivasi | • Review multiple interface dan default method<br>• "Bagaimana membuat hierarki yang terkontrol dan aman?" | Ceramah |
| **10-35'** | Sealed Class | • **Konsep sealed class** — semua subclass diketahui di compile time<br>• **Closed polymorphism** vs open polymorphism<br>• **Sealed class vs Abstract class** — perbedaan<br>• **Sealed interface** (Kotlin 1.5+)<br>• **Ekshaustif `when`** — compiler memastikan semua kemungkinan ditangani<br>• **Demo**: `Result` dengan `Success`, `Error`, `Loading` | Ceramah, Demonstrasi, Live Coding |
| **35-65'** | Studi Kasus: Sistem Perangkat Elektronik | • **Analisis kebutuhan** — berbagai perangkat elektronik<br>• **Hierarki** — abstract class `ElectronicDevice`, interface `Chargeable`, `Connectable`, `Displayable`<br>• **Implementasi** — `Smartphone`, `Laptop`, `SmartTV`<br>• **Sealed class `DeviceStatus`** — `On`, `Off`, `Error`, `Charging`<br>• **Live coding** bersama dosen | Demonstrasi, Live Coding, Diskusi |
| **65-85'** | Praktik Sistem Perangkat | • Mahasiswa mengimplementasikan sistem perangkat elektronik sendiri<br>• Menambahkan perangkat baru (misal: `Tablet`, `SmartWatch`)<br>• Dosen memberikan asistensi | Praktik mandiri, Asistensi |
| **85-105'** | Review & Diskusi Kasus | • Beberapa mahasiswa mempresentasikan kode mereka<br>• Diskusi: "Mengapa sealed class lebih aman untuk status?"<br>• Q&A | Presentasi, Diskusi |
| **105-120'** | Penutupan | • Dosen merangkum pencapaian pertemuan 5<br>• Preview materi pertemuan 6 (Konsep Lanjutan: Data Class, Object Declaration, Companion Object)<br>• Memberikan tugas membaca modul pertemuan 6<br>• Menutup perkuliahan dengan doa dan salam | Ceramah |

---

## E. TUGAS 5 (Dikumpulkan)

### Sistem Manajemen Transportasi dengan Abstraksi

Buatlah program lengkap sistem manajemen transportasi yang mengimplementasikan abstraksi dengan ketentuan berikut:

#### 1. Abstract Class `Transportation`

| **Komponen** | **Spesifikasi** |
|---|---|
| **Properti** | `id: String` (read-only)<br>`name: String` (read-only)<br>`capacity: Int` (read-only)<br>`isOperational: Boolean` (bisa diubah) |
| **Metode** | `calculateFuelEfficiency(): Double` (abstract)<br>`calculateMaintenanceCost(): Double` (abstract)<br>`startOperation(): Boolean` — menandai sebagai operational<br>`stopOperation(): Boolean` — menandai sebagai non-operational<br>`displayInfo(): String` — menampilkan info transportasi |

#### 2. Interface `ElectricPowered`

| **Komponen** | **Spesifikasi** |
|---|---|
| **Properti** | `batteryCapacity: Int` (dalam kWh)<br>`currentCharge: Int` (dalam %) |
| **Metode** | `charge(amount: Int): Boolean` — menambah charge<br>`getRange(): Double` — jarak tempuh berdasarkan battery capacity |

#### 3. Interface `FuelPowered`

| **Komponen** | **Spesifikasi** |
|---|---|
| **Properti** | `fuelType: String` ("Bensin", "Diesel", "CNG")<br>`fuelCapacity: Int` (dalam liter)<br>`currentFuel: Int` (dalam liter) |
| **Metode** | `refuel(amount: Int): Boolean` — menambah fuel<br>`getRange(): Double` — jarak tempuh berdasarkan fuel capacity |

#### 4. Subclass `ElectricCar` — Mewarisi Transportation, mengimplementasikan ElectricPowered

| **Komponen** | **Spesifikasi** |
|---|---|
| **Properti Tambahan** | `motorPower: Int` (dalam kW) |
| **Overriding** | `calculateFuelEfficiency()` → menggunakan konsumsi listrik<br>`calculateMaintenanceCost()` → biaya perawatan listrik |

#### 5. Subclass `GasolineCar` — Mewarisi Transportation, mengimplementasikan FuelPowered

| **Komponen** | **Spesifikasi** |
|---|---|
| **Properti Tambahan** | `engineCapacity: Int` (dalam cc) |
| **Overriding** | `calculateFuelEfficiency()` → menggunakan konsumsi bensin<br>`calculateMaintenanceCost()` → biaya perawatan mesin bensin |

#### 6. Subclass `ElectricBus` — Mewarisi Transportation, mengimplementasikan ElectricPowered

| **Komponen** | **Spesifikasi** |
|---|---|
| **Properti Tambahan** | `passengerCount: Int` |
| **Overriding** | `calculateFuelEfficiency()` → menggunakan konsumsi listrik (lebih tinggi karena beban)<br>`calculateMaintenanceCost()` → biaya perawatan bus listrik |

#### 7. Sealed Class `TripStatus`

Buat sealed class untuk status perjalanan:
- `Scheduled` — perjalanan terjadwal
- `InProgress` — perjalanan sedang berlangsung
- `Completed` — perjalanan selesai
- `Cancelled` — perjalanan dibatalkan

#### 8. Kelas `TransportationCompany`

| **Komponen** | **Spesifikasi** |
|---|---|
| **Properti** | `name: String`<br>`vehicles: MutableList<Transportation>` (private) |
| **Metode** | `addVehicle(vehicle: Transportation)`<br>`findVehicle(id: String): Transportation?`<br>`getTotalMaintenanceCost(): Double`<br>`getVehiclesByType(type: String): List<Transportation>`<br>`displayAllVehicles()`<br>`displayOperationalVehicles()` |

#### 9. Fungsi `main()`

- Buat objek `TransportationCompany` dengan nama "PT Transportasi Maju"
- Tambahkan **minimal 6 kendaraan** (2 electric car, 2 gasoline car, 2 electric bus)
- Tampilkan semua kendaraan
- Tampilkan kendaraan yang operasional
- Tampilkan total biaya perawatan
- Gunakan **abstract class** untuk `Transportation`
- Gunakan **interface** untuk `ElectricPowered` dan `FuelPowered`
- Gunakan **multiple interface** pada kendaraan yang sesuai
- Gunakan **sealed class** untuk `TripStatus`

#### 10. Kriteria Penilaian Tugas 5

| **Kriteria** | **Bobot** | **Indikator** |
|---|---|---|
| **Abstract Class** | 25% | • `Transportation` sebagai abstract class<br>• Metode abstrak diimplementasikan dengan benar<br>• Metode konkret digunakan dengan benar |
| **Interface** | 20% | • `ElectricPowered` dan `FuelPowered` sebagai interface<br>• Default method diimplementasikan dengan benar |
| **Multiple Interface** | 15% | • Subclass mengimplementasikan interface yang sesuai<br>• Konflik overriding diselesaikan dengan benar |
| **Sealed Class** | 15% | • `TripStatus` sebagai sealed class<br>• `when` expression ekshaustif |
| **Fungsi main()** | 15% | • Menampilkan semua skenario yang diminta<br>• Output jelas dan informatif |
| **Kode Berkualitas** | 10% | • Kode bersih, terstruktur, diberi komentar<br>• Menggunakan naming convention yang benar |

---

## F. MEDIA DAN ALAT PEMBELAJARAN

| **Media** | **Keterangan** |
|---|---|
| **Laptop/PC** | Setiap mahasiswa menggunakan laptop/PC masing-masing |
| **IntelliJ IDEA** | IDE utama untuk pengembangan Kotlin |
| **JDK** | Java Development Kit (versi 11 atau 17) |
| **Proyektor/LCD** | Untuk presentasi dan demonstrasi dosen |
| **Whiteboard** | Untuk menjelaskan konsep dan hierarki kelas |
| **Modul Praktikum** | Modul cetak/digital pertemuan 5 |
| **Kotlin Playground** | Alternatif untuk mencoba kode tanpa instalasi |

---

## G. PENILAIAN PERTEMUAN 5

| **Komponen** | **Bobot** | **Indikator** | **Teknik** |
|---|---|---|---|
| **Keaktifan Sesi 1-3** | 15% dari total keaktifan | • Kehadiran tepat waktu<br>• Partisipasi dalam diskusi dan tanya jawab<br>• Keterlibatan dalam praktik kelompok | Observasi |
| **Tugas 5** | 100% dari nilai tugas 5 | • Lihat kriteria penilaian Tugas 5 di atas | Penilaian kode |
| **Kuis Singkat** | Bonus | • Pertanyaan tentang abstract class, interface, default method, sealed class | Tes tertulis/lisan |

---

## H. REFERENSI PERTEMUAN 5

### Referensi Utama:

1. **Kotlin Official Documentation – Interfaces** — [https://kotlinlang.org/docs/interfaces.html](https://kotlinlang.org/docs/interfaces.html)

2. **Kotlin Official Documentation – Sealed Classes and Interfaces** — [https://kotlinlang.org/docs/sealed-classes.html](https://kotlinlang.org/docs/sealed-classes.html)

3. **Kotlin Official Documentation – Inheritance** — [https://kotlinlang.org/docs/inheritance.html](https://kotlinlang.org/docs/inheritance.html)

### Referensi Pendukung:

4. **Kotlin的接口与抽象类有何区别** — [https://m.yisu.com/zixun/994021.html](https://m.yisu.com/zixun/994021.html)

5. **Kotlin的接口和抽象类有何不同** — [http://www.yisu.com/jc/1036429.html](http://www.yisu.com/jc/1036429.html)

6. **Kotlin10 - 面向对象之抽象类与接口** — [https://developer.aliyun.com/article/1628049](https://developer.aliyun.com/article/1628049)

7. **Kotlin: why use Abstract classes (vs. interfaces)?** — Stack Overflow

---

## I. LAMPIRAN

### Lampiran 1: Perbandingan Abstract Class vs Interface — Visual

```
┌─────────────────────────────────────────────────────────────────────────────┐
│                        ABSTRACT CLASS vs INTERFACE                         │
├─────────────────────────────────────────────────────────────────────────────┤
│                                                                             │
│  ┌─────────────────────────────────┐  ┌─────────────────────────────────┐  │
│  │         ABSTRACT CLASS          │  │           INTERFACE             │  │
│  │                                 │  │                                 │  │
│  │  abstract class Animal {        │  │  interface Swimmable {          │  │
│  │      val name: String           │  │      val swimSpeed: Double      │  │
│  │      var age: Int = 0     ← State│  │      fun swim() { ← Default    │  │
│  │                                 │  │          println("Swimming")    │  │
│  │      constructor(name: String)  │  │      }                          │  │
│  │           ← Constructor         │  │  }                             │  │
│  │                                 │  │                                 │  │
│  │      fun eat() { ← Concrete     │  │  // Tidak bisa menyimpan state  │  │
│  │          println("Eating")      │  │  // Tidak bisa memiliki         │  │
│  │      }                          │  │  // constructor                 │  │
│  │                                 │  │                                 │  │
│  │      abstract fun makeSound()   │  │  // Bisa diimplementasikan      │  │
│  │           ← Abstract            │  │  // oleh banyak kelas           │  │
│  │                                 │  │                                 │  │
│  │  }                              │  │  }                              │  │
│  │                                 │  │                                 │  │
│  │  class Dog : Animal()           │  │  class Duck : Swimmable,        │  │
│  │      ↑ Single inheritance       │  │      Flyable ← Multiple         │  │
│  │                                 │  │                                 │  │
│  └─────────────────────────────────┘  └─────────────────────────────────┘  │
│                                                                             │
│  Tujuan: Mendefinisikan "How" (bagaimana)  Tujuan: Mendefinisikan "What"   │
│                                (apa)                       │
└─────────────────────────────────────────────────────────────────────────────┘
```

### Lampiran 2: Checklist Pemahaman Mahasiswa

| **No** | **Konsep** | **Paham** | **Kurang Paham** | **Tidak Paham** |
|---|---|---|---|---|
| 1 | Definisi abstraksi | ☐ | ☐ | ☐ |
| 2 | Manfaat abstraksi | ☐ | ☐ | ☐ |
| 3 | Abstract class — definisi dan karakteristik | ☐ | ☐ | ☐ |
| 4 | Abstract class — constructor dan state | ☐ | ☐ | ☐ |
| 5 | Abstract class — metode abstrak dan konkret | ☐ | ☐ | ☐ |
| 6 | Interface — definisi dan karakteristik | ☐ | ☐ | ☐ |
| 7 | Interface — properti dan default method | ☐ | ☐ | ☐ |
| 8 | Perbedaan abstract class vs interface | ☐ | ☐ | ☐ |
| 9 | Kapan menggunakan abstract class vs interface | ☐ | ☐ | ☐ |
| 10 | Multiple interface implementation | ☐ | ☐ | ☐ |
| 11 | Resolving overriding conflicts | ☐ | ☐ | ☐ |
| 12 | Default method di interface | ☐ | ☐ | ☐ |
| 13 | Sealed class — closed polymorphism | ☐ | ☐ | ☐ |
| 14 | `super<Interface>` untuk mengatasi konflik | ☐ | ☐ | ☐ |
| 15 | Menerapkan abstraksi dalam kode | ☐ | ☐ | ☐ |

---

**Disusun oleh,**
[Nama Dosen Pengampu]
Dosen Program Studi D4 Teknologi Rekayasa Informatika Industri
