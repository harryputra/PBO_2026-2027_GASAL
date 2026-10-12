# RENCANA PEMBELAJARAN SEMESTER (RPS)
## PERTEMUAN KE-6 — RENCANA PELAKSANAAN PEMBELAJARAN (RPP)
### PEMROGRAMAN BERORIENTASI OBJEK (OBJECT-ORIENTED PROGRAMMING)
### “Konsep Lanjutan: Data Class, Object Declaration, dan Companion Object”

---

## A. IDENTITAS PERTEMUAN

| **Komponen** | **Keterangan** |
|---|---|
| **Pertemuan Ke-** | 6 |
| **Topik** | Konsep Lanjutan: Data Class, Object Declaration (Singleton), Companion Object |
| **Durasi** | 8 Jam Praktik (480 menit) |
| **Hari/Tanggal** | [Disesuaikan] |
| **Ruang** | Laboratorium Komputer |
| **Dosen** | [Nama Dosen] |
| **Capaian Pembelajaran** | Mahasiswa memahami dan mampu mengimplementasikan konsep lanjutan Kotlin: Data Class untuk menyimpan data secara efisien, Object Declaration untuk membuat singleton, dan Companion Object untuk mendefinisikan anggota statis setara Java |

---

## B. CAPAIAN PEMBELAJARAN PERTEMUAN (CPP)

Setelah mengikuti pertemuan ke-6 ini, mahasiswa mampu:

1. **CPP 6.1:** Menjelaskan tujuan dan manfaat penggunaan Data Class di Kotlin.
2. **CPP 6.2:** Mengimplementasikan Data Class dengan benar, termasuk penggunaan fungsi `copy()` dan destructuring declaration.
3. **CPP 6.3:** Menjelaskan konsep Object Declaration dan penerapannya untuk membuat Singleton.
4. **CPP 6.4:** Membedakan antara Object Declaration dan Object Expression.
5. **CPP 6.5:** Mengimplementasikan Companion Object untuk membuat anggota kelas (method/property) yang dapat diakses tanpa instansiasi.
6. **CPP 6.6:** Menggunakan Companion Object sebagai factory method.
7. **CPP 6.7:** Memahami konsep Data Object.
8. **CPP 6.8:** Menerapkan ketiga konsep (Data Class, Object Declaration, Companion Object) dalam studi kasus terintegrasi.

---

## C. MATERI POKOK

### 1. Data Class (Sesi 1)

#### 1.1 Apa itu Data Class?

**Data Class** adalah kelas khusus di Kotlin yang dirancang khusus untuk **menyimpan data**. Ketika sebuah kelas ditandai dengan keyword `data`, compiler secara otomatis akan menghasilkan beberapa fungsi standar yang biasanya perlu ditulis secara manual untuk kelas yang berfungsi sebagai container data.

> **Definisi Sederhana:** Data Class adalah "kelas penyimpan data" yang membebaskan Anda dari menulis boilerplate code seperti `toString()`, `equals()`, `hashCode()`, dan `copy()`.

#### 1.2 Fungsi yang Dihasilkan Secara Otomatis

Compiler Kotlin secara otomatis menghasilkan fungsi-fungsi berikut untuk setiap Data Class:

| **Fungsi** | **Kegunaan** |
|---|---|
| `toString()` | Mengembalikan representasi string yang mudah dibaca, misal: `User(name=John, age=42)` |
| `equals()` / `hashCode()` | Membandingkan dua objek berdasarkan nilai propertinya, bukan berdasarkan alamat memori |
| `copy()` | Membuat salinan objek dengan beberapa properti yang dapat diubah |
| `componentN()` | Fungsi untuk destructuring declaration (membongkar objek menjadi variabel terpisah) |

#### 1.3 Aturan Data Class

Data Class di Kotlin harus memenuhi persyaratan berikut:

| **Aturan** | **Penjelasan** |
|---|---|
| **Primary constructor minimal 1 parameter** | Data class harus memiliki setidaknya satu properti di primary constructor |
| **Semua parameter primary constructor harus `val` atau `var`** | Properti harus dideklarasikan dengan `val` (immutable, direkomendasikan) atau `var` (mutable) |
| **Tidak bisa `abstract`, `open`, `sealed`, atau `inner`** | Data class memiliki batasan dalam hal inheritance |
| **Properti di class body tidak diikutsertakan** | Hanya properti di primary constructor yang digunakan untuk `toString()`, `equals()`, `hashCode()`, dan `copy()` |

#### 1.4 Praktik Terbaik Data Class

> **Gunakan `val` (immutable) sebisa mungkin** untuk membuat data class yang aman dan mudah diprediksi.

```kotlin
// ✅ Direkomendasikan: immutable data class
data class User(val id: Int, val name: String, val email: String)

// ⚠️ Boleh tapi kurang direkomendasikan: mutable data class
data class MutableUser(var id: Int, var name: String, var email: String)
```

#### 1.5 Contoh Lengkap Data Class

```kotlin
// ============================================================
// 1. DEKLARASI DATA CLASS
// ============================================================

// Data class sederhana dengan 3 properti
data class Product(
    val id: Int,
    val name: String,
    val price: Double,
    val category: String = "General"  // Default value
)

// Data class dengan properti di class body (tidak diikutsertakan dalam toString/equals/hashCode)
data class Person(val name: String) {
    var age: Int = 0  // Properti ini TIDAK digunakan untuk equals()/hashCode()
}

// ============================================================
// 2. PENGGUNAAN DATA CLASS
// ============================================================

fun main() {
    // Membuat objek
    val product1 = Product(1, "Laptop", 15_000_000.0)
    val product2 = Product(2, "Mouse", 250_000.0, "Electronics")

    // toString() — otomatis menghasilkan output yang readable
    println(product1)
    // Output: Product(id=1, name=Laptop, price=15000000.0, category=General)

    // equals() — membandingkan berdasarkan nilai, bukan alamat memori
    val product3 = Product(1, "Laptop", 15_000_000.0)
    println(product1 == product3)  // Output: true (nilai sama)
    println(product1 === product3) // Output: false (referensi berbeda)

    // copy() — membuat salinan dengan beberapa properti diubah
    val product4 = product1.copy(price = 14_500_000.0, category = "Electronics")
    println(product4)
    // Output: Product(id=1, name=Laptop, price=14500000.0, category=Electronics)

    // Destructuring declaration — membongkar objek menjadi variabel
    val (id, name, price, category) = product1
    println("ID: $id, Name: $name, Price: $price, Category: $category")
    // Output: ID: 1, Name: Laptop, Price: 15000000.0, Category: General

    // ============================================================
    // 3. PROPERTI DI CLASS BODY TIDAK DI-IKUTSERTAKAN
    // ============================================================
    val person1 = Person("Alice")
    person1.age = 25
    val person2 = Person("Alice")
    person2.age = 30

    // equals() hanya membandingkan properti di primary constructor (name)
    println(person1 == person2)  // Output: true (name sama, age diabaikan)
    println(person1)  // Output: Person(name=Alice) (age tidak ditampilkan)
}
```

#### 1.6 Data Class dengan Inheritance

Data class dapat **mewarisi** dari kelas lain (termasuk sealed class):

```kotlin
// Data class bisa mewarisi dari sealed class
sealed class Result
data class Success(val data: String, val code: Int) : Result()
data class Error(val message: String, val errorCode: Int) : Result()
object Loading : Result()

fun handleResult(result: Result) {
    when (result) {
        is Success -> println("✅ Success: ${result.data} (Code: ${result.code})")
        is Error -> println("❌ Error: ${result.message} (Code: ${result.errorCode})")
        Loading -> println("⏳ Loading...")
    }
}
```

---

### 2. Object Declaration — Singleton Pattern (Sesi 2)

#### 2.1 Apa itu Object Declaration?

**Object Declaration** adalah cara di Kotlin untuk **mendeklarasikan kelas dan membuat satu-satunya instance-nya dalam satu langkah**. Ini adalah implementasi bawaan dari **Singleton Pattern** di Kotlin.

> **Definisi Sederhana:** Object Declaration adalah "cara termudah membuat Singleton di Kotlin" — sebuah kelas yang hanya memiliki satu instance dan bisa diakses secara global.

#### 2.2 Karakteristik Object Declaration

| **Karakteristik** | **Penjelasan** |
|---|---|
| **Singleton** | Hanya ada satu instance dari object tersebut |
| **Lazy Initialization** | Object dibuat hanya ketika pertama kali diakses (lazy) |
| **Thread-Safe** | Inisialisasi object aman untuk multi-thread |
| **Tidak bisa memiliki constructor** | Object tidak bisa memiliki constructor karena instance-nya sudah tunggal |
| **Bisa memiliki supertype** | Object bisa mewarisi class atau mengimplementasikan interface |
| **Bukan expression** | Object declaration tidak bisa digunakan di sisi kanan assignment |

#### 2.3 Sintaks Object Declaration

```kotlin
// Object declaration — singleton
object DatabaseManager {
    // Properti
    private var connectionString: String = "jdbc:mysql://localhost:3306/mydb"
    private var isConnected: Boolean = false

    // Method
    fun connect() {
        if (!isConnected) {
            println("🔗 Connecting to database: $connectionString")
            isConnected = true
        } else {
            println("✅ Already connected")
        }
    }

    fun disconnect() {
        if (isConnected) {
            println("🔌 Disconnecting from database")
            isConnected = false
        }
    }

    fun getStatus(): String {
        return if (isConnected) "🟢 Connected" else "🔴 Disconnected"
    }
}

fun main() {
    // Mengakses object — langsung menggunakan namanya
    DatabaseManager.connect()    // Output: 🔗 Connecting to database: jdbc:mysql://localhost:3306/mydb
    DatabaseManager.connect()    // Output: ✅ Already connected
    println(DatabaseManager.getStatus())  // Output: 🟢 Connected

    // ❌ Tidak bisa membuat instance baru
    // val db = DatabaseManager()  // ERROR!
}
```

#### 2.4 Object Declaration dengan Interface

```kotlin
// Interface untuk logger
interface Logger {
    fun log(message: String)
    fun logError(message: String)
    fun logWarning(message: String)
}

// Object declaration mengimplementasikan interface
object FileLogger : Logger {
    private val logFile = mutableListOf<String>()

    override fun log(message: String) {
        logFile.add("[INFO] $message")
        println("[INFO] $message")
    }

    override fun logError(message: String) {
        logFile.add("[ERROR] $message")
        println("❌ [ERROR] $message")
    }

    override fun logWarning(message: String) {
        logFile.add("[WARNING] $message")
        println("⚠️ [WARNING] $message")
    }

    fun getLogHistory(): List<String> = logFile.toList()
}

fun main() {
    FileLogger.log("Application started")
    FileLogger.logWarning("Low memory")
    FileLogger.logError("Connection failed")

    println("\n--- LOG HISTORY ---")
    FileLogger.getLogHistory().forEach { println(it) }
}
```

#### 2.5 Object Declaration dengan Inheritance

```kotlin
// Abstract class
abstract class NetworkClient {
    abstract fun sendRequest(endpoint: String, data: String)
    abstract fun getBaseUrl(): String
}

// Object declaration mewarisi abstract class
object ApiClient : NetworkClient() {
    private val baseUrl = "https://api.example.com/v1"

    override fun getBaseUrl(): String = baseUrl

    override fun sendRequest(endpoint: String, data: String) {
        println("📡 Sending request to ${getBaseUrl()}/$endpoint")
        println("   Data: $data")
        println("   Response: OK (200)")
    }

    // Method tambahan
    fun get(endpoint: String) {
        sendRequest(endpoint, "GET")
    }

    fun post(endpoint: String, data: String) {
        sendRequest(endpoint, "POST: $data")
    }
}

fun main() {
    ApiClient.get("users")
    ApiClient.post("users", "{\"name\": \"John\"}")
}
```

---

### 3. Object Expression — Anonymous Object (Sesi 2)

#### 3.1 Apa itu Object Expression?

**Object Expression** digunakan untuk membuat **objek anonim (tanpa nama)** dari sebuah kelas atau interface secara langsung, tanpa harus mendeklarasikan subclass secara eksplisit.

> **Perbedaan Utama:** Object Declaration = **bernama** (singleton), Object Expression = **anonim** (sekali pakai).

#### 3.2 Karakteristik Object Expression

| **Karakteristik** | **Penjelasan** |
|---|---|
| **Tanpa nama** | Object expression tidak memiliki nama |
| **Sekali pakai** | Digunakan untuk satu keperluan spesifik |
| **Dieksekusi segera** | Object expression diinisialisasi saat digunakan |
| **Bisa digunakan di sisi kanan assignment** | Object expression adalah expression |

#### 3.3 Contoh Object Expression

```kotlin
// Interface
interface ClickListener {
    fun onClick()
    fun onLongClick()
}

// Abstract class
abstract class EventHandler {
    abstract fun handle()
    fun log() = println("Event logged")
}

fun main() {
    // ============================================================
    // Object Expression untuk Interface
    // ============================================================
    val buttonListener = object : ClickListener {
        override fun onClick() {
            println("🖱️ Button clicked!")
        }

        override fun onLongClick() {
            println("🖱️ Button long-clicked!")
        }
    }

    buttonListener.onClick()      // Output: 🖱️ Button clicked!
    buttonListener.onLongClick()  // Output: 🖱️ Button long-clicked!

    // ============================================================
    // Object Expression untuk Abstract Class
    // ============================================================
    val handler = object : EventHandler() {
        override fun handle() {
            println("⚡ Handling event...")
        }
    }

    handler.handle()  // Output: ⚡ Handling event...
    handler.log()     // Output: Event logged

    // ============================================================
    // Object Expression dengan properti tambahan
    // ============================================================
    val tempObject = object {
        val name = "Temporary"
        val version = 1.0
        fun display() = println("$name v$version")
    }

    tempObject.display()  // Output: Temporary v1.0
}
```

#### 3.4 Perbandingan Object Declaration vs Object Expression

| **Aspek** | **Object Declaration** | **Object Expression** |
|---|---|---|
| **Nama** | Memiliki nama | Tanpa nama (anonim) |
| **Singleton** | Ya (satu instance global) | Tidak (instance baru setiap kali) |
| **Inisialisasi** | Lazy (saat pertama diakses) | Immediate (saat dibuat) |
| **Penggunaan** | Global, reusable | Sekali pakai, lokal |
| **Assignment** | Tidak bisa di sisi kanan | Bisa di sisi kanan |

---

### 4. Companion Object (Sesi 3)

#### 4.1 Apa itu Companion Object?

**Companion Object** adalah object declaration yang dideklarasikan **di dalam sebuah kelas**. Fungsinya adalah untuk menyediakan **anggota kelas (method/property) yang dapat diakses tanpa harus membuat instance dari kelas tersebut**.

> **Definisi Sederhana:** Companion Object adalah "pengganti static member di Java" — memungkinkan Anda memanggil method seperti `MyClass.method()` tanpa membuat objek.

#### 4.2 Karakteristik Companion Object

| **Karakteristik** | **Penjelasan** |
|---|---|
| **Class-level members** | Anggota companion object terikat ke kelas, bukan ke instance |
| **Akses tanpa instansiasi** | Bisa dipanggil langsung melalui nama kelas |
| **Hanya satu per kelas** | Setiap kelas hanya bisa memiliki satu companion object |
| **Bisa memiliki nama** | Bisa diberi nama (opsional) |
| **Bisa mengimplementasikan interface** | Companion object bisa mengimplementasikan interface |
| **Diinisialisasi saat kelas dimuat** | Companion object diinisialisasi ketika kelasnya dimuat |

#### 4.3 Sintaks Dasar Companion Object

```kotlin
class MyClass {
    // Companion object tanpa nama
    companion object {
        // Anggota static-equivalent
        val PI = 3.14159
        fun create(): MyClass = MyClass()
    }
}

// Akses langsung melalui nama kelas
fun main() {
    println(MyClass.PI)         // Output: 3.14159
    val instance = MyClass.create()
}
```

#### 4.4 Companion Object dengan Nama

```kotlin
class User private constructor(val name: String) {
    // Companion object dengan nama "Factory"
    companion object Factory {
        fun create(name: String): User {
            return User(name.trim())
        }

        fun createAdmin(): User {
            return User("Admin")
        }
    }
}

fun main() {
    // Akses melalui nama kelas (tanpa nama companion)
    val user1 = User.create(" John ")
    val admin = User.createAdmin()

    // Bisa juga diakses melalui nama companion (opsional)
    val user2 = User.Factory.create(" Jane ")

    println(user1.name)  // Output: John (trim otomatis)
    println(admin.name)  // Output: Admin
}
```

#### 4.5 Companion Object sebagai Factory Method

Companion object sangat berguna untuk mengimplementasikan **Factory Pattern**:

```kotlin
class Product private constructor(
    val id: String,
    val name: String,
    val price: Double
) {
    companion object {
        // Factory method dengan validasi
        fun create(id: String, name: String, price: Double): Product? {
            return if (id.isNotBlank() && name.isNotBlank() && price > 0) {
                Product(id, name, price)
            } else {
                println("❌ Invalid product data")
                null
            }
        }

        // Factory method dengan default value
        fun createDefault(): Product {
            return Product("DEFAULT", "Default Product", 0.0)
        }

        // Factory method dari Map
        fun fromMap(map: Map<String, Any>): Product? {
            val id = map["id"] as? String ?: return null
            val name = map["name"] as? String ?: return null
            val price = (map["price"] as? Number)?.toDouble() ?: return null
            return create(id, name, price)
        }
    }
}

fun main() {
    val product1 = Product.create("P001", "Laptop", 15_000_000.0)
    val product2 = Product.createDefault()
    val product3 = Product.fromMap(mapOf(
        "id" to "P002",
        "name" to "Mouse",
        "price" to 250_000
    ))

    println(product1)  // Output: Product(id=P001, name=Laptop, price=15000000.0)
    println(product2)  // Output: Product(id=DEFAULT, name=Default Product, price=0.0)
    println(product3)  // Output: Product(id=P002, name=Mouse, price=250000.0)
}
```

#### 4.6 Companion Object dengan Interface

Companion object bisa mengimplementasikan interface, memungkinkan factory yang terstandarisasi:

```kotlin
// Interface factory
interface Factory<T> {
    fun create(): T
}

class Car private constructor(val brand: String, val model: String) {
    companion object : Factory<Car> {
        override fun create(): Car {
            return Car("Toyota", "Avanza")
        }

        fun createCustom(brand: String, model: String): Car {
            return Car(brand, model)
        }
    }
}

fun main() {
    // Menggunakan interface Factory
    val defaultCar: Car = Car.create()
    println("${defaultCar.brand} ${defaultCar.model}")  // Output: Toyota Avanza

    // Menggunakan method custom
    val customCar = Car.createCustom("Honda", "Civic")
    println("${customCar.brand} ${customCar.model}")  // Output: Honda Civic
}
```

#### 4.7 Companion Object dengan Properti dan State

Companion object bisa menyimpan **state class-level** yang dibagikan di semua instance:

```kotlin
class Counter {
    companion object {
        // Class-level state — dibagikan di semua instance
        private var totalInstances = 0
        private var totalCalls = 0

        fun incrementInstances() {
            totalInstances++
        }

        fun incrementCalls() {
            totalCalls++
        }

        fun getStats(): String {
            return "Total Instances: $totalInstances, Total Calls: $totalCalls"
        }
    }

    // Instance method
    fun call() {
        println("📞 Calling...")
        Companion.incrementCalls()  // Bisa akses companion dari instance
    }

    init {
        Companion.incrementInstances()
    }
}

fun main() {
    println(Counter.getStats())  // Output: Total Instances: 0, Total Calls: 0

    val c1 = Counter()
    c1.call()
    val c2 = Counter()
    c2.call()
    c2.call()

    println(Counter.getStats())  // Output: Total Instances: 2, Total Calls: 3
}
```

#### 4.8 Companion Object Extension Functions

Kita bisa menambahkan extension function ke companion object:

```kotlin
class MyClass {
    companion object {
        // Companion object kosong
    }
}

// Extension function untuk companion object
fun MyClass.Companion.hello() {
    println("👋 Hello from companion object extension!")
}

fun MyClass.Companion.greet(name: String) {
    println("👋 Hello, $name! (from companion extension)")
}

fun main() {
    // Memanggil extension function langsung melalui nama kelas
    MyClass.hello()   // Output: 👋 Hello from companion object extension!
    MyClass.greet("Budi")  // Output: 👋 Hello, Budi! (from companion extension)
}
```

---

### 5. Data Object (Sesi 4)

#### 5.1 Apa itu Data Object?

**Data Object** adalah object declaration yang ditandai dengan keyword `data`. Mirip dengan data class, data object secara otomatis memiliki fungsi `toString()` dan `equals()`.

> **Perbedaan dengan Data Class:** Data object **tidak** memiliki fungsi `copy()` karena object declaration hanya memiliki satu instance yang tidak bisa di-copy.

#### 5.2 Contoh Data Object

```kotlin
// Data object — singleton dengan toString dan equals otomatis
data object AppConfig {
    var appName: String = "My Application"
    var version: String = "1.0.0"
    var isDebug: Boolean = true
}

data object DefaultSettings {
    val theme: String = "Dark"
    val language: String = "English"
    val fontSize: Int = 14
}

fun main() {
    // toString() otomatis
    println(AppConfig)  // Output: AppConfig

    // equals() berdasarkan identitas (hanya satu instance)
    val config1 = AppConfig
    val config2 = AppConfig
    println(config1 == config2)  // Output: true (satu instance yang sama)

    // Mengakses properti
    println(AppConfig.appName)   // Output: My Application
    AppConfig.appName = "New App"
    println(AppConfig.appName)   // Output: New App

    println(DefaultSettings)  // Output: DefaultSettings
    println(DefaultSettings.theme)  // Output: Dark
}
```

---

## D. RINCIAN KEGIATAN PEMBELAJARAN (8 JAM)

### Sesi 1: Data Class (2 Jam — 120 menit)

| **Waktu** | **Kegiatan** | **Detail** | **Metode** |
|---|---|---|---|
| **0-10'** | Pembukaan & Review | • Dosen membuka perkuliahan dengan salam dan doa<br>• Review singkat materi pertemuan 5 (abstraksi, interface, sealed class)<br>• Menghubungkan dengan topik pertemuan 6: "Bagaimana Kotlin menyederhanakan kelas penyimpan data?" | Ceramah interaktif, Tanya jawab |
| **10-40'** | Konsep Data Class | • **Definisi data class** — kelas khusus untuk menyimpan data<br>• **Fungsi yang dihasilkan otomatis**: `toString()`, `equals()`, `hashCode()`, `copy()`, `componentN()`<br>• **Aturan data class**: primary constructor minimal 1 parameter, semua parameter `val`/`var`, tidak bisa `abstract/open/sealed/inner`<br>• **Perbedaan data class vs class biasa**<br>• **Praktik terbaik**: gunakan `val` (immutable) | Ceramah, Demonstrasi, Diskusi |
| **40-70'** | Demonstrasi Data Class | • **Live coding**: membuat data class `Product`<br>• Menunjukkan `toString()` otomatis<br>• Menunjukkan `equals()` — perbandingan berdasarkan nilai<br>• Menunjukkan `copy()` — copy dengan modifikasi sebagian<br>• Menunjukkan **destructuring declaration** — `val (id, name) = product`<br>• Menunjukkan properti di class body tidak diikutsertakan | Demonstrasi, Live Coding |
| **70-90'** | Praktik Data Class | • Mahasiswa membuat data class `Student` dengan properti: `id`, `name`, `gpa`, `major`<br>• Membuat beberapa objek dan mendemonstrasikan `toString()`, `equals()`, `copy()`<br>• Menggunakan destructuring declaration | Praktik mandiri, Asistensi |
| **90-120'** | Latihan & Diskusi | • Mahasiswa mengerjakan latihan: membuat data class `Order` dengan properti `id`, `customer`, `items`, `total`<br>• Demonstrasi penggunaan `copy()` untuk membuat order baru dengan status berbeda<br>• Diskusi: "Kapan sebaiknya menggunakan data class vs class biasa?" | Praktik, Diskusi |

---

### Sesi 2: Object Declaration & Object Expression (2 Jam — 120 menit)

| **Waktu** | **Kegiatan** | **Detail** | **Metode** |
|---|---|---|---|
| **0-10'** | Review & Motivasi | • Mereview data class<br>• "Bagaimana jika kita hanya butuh satu instance dari sebuah kelas?"<br>• Pengenalan Singleton Pattern | Ceramah |
| **10-40'** | Object Declaration (Singleton) | • **Konsep object declaration** — kelas dan instance dalam satu langkah<br>• **Karakteristik**: singleton, lazy initialization, thread-safe, tidak bisa memiliki constructor<br>• **Sintaks**: `object Nama { ... }`<br>• **Bisa mengimplementasikan interface** dan mewarisi class<br>• **Demo**: `DatabaseManager` singleton | Ceramah, Demonstrasi, Live Coding |
| **40-65'** | Object Expression (Anonymous Object) | • **Konsep object expression** — object anonim tanpa nama<br>• **Karakteristik**: tanpa nama, sekali pakai, dieksekusi segera<br>• **Perbedaan** object declaration vs object expression<br>• **Demo**: membuat object expression untuk interface `ClickListener` dan abstract class `EventHandler`<br>• **Demo**: object expression dengan properti tambahan | Ceramah, Demonstrasi, Live Coding |
| **65-90'** | Praktik Object Declaration & Expression | • Mahasiswa membuat object declaration `Logger` dengan method `log()`, `logError()`, `logWarning()`<br>• Mahasiswa membuat object expression untuk interface `OnClickListener`<br>• Membandingkan perbedaan keduanya | Praktik mandiri, Asistensi |
| **90-120'** | Diskusi & Review | • Diskusi: "Kapan menggunakan object declaration vs object expression?"<br>• Studi kasus: implementasi singleton untuk koneksi database<br>• Q&A | Diskusi, Tanya jawab |

---

### Sesi 3: Companion Object (2 Jam — 120 menit)

| **Waktu** | **Kegiatan** | **Detail** | **Metode** |
|---|---|---|---|
| **0-10'** | Review & Motivasi | • Review object declaration<br>• "Bagaimana jika kita ingin method static seperti di Java?"<br>• Pengenalan Companion Object | Ceramah |
| **10-45'** | Companion Object Dasar | • **Konsep companion object** — class-level members tanpa instansiasi<br>• **Karakteristik**: hanya satu per kelas, diinisialisasi saat kelas dimuat<br>• **Sintaks**: `companion object { ... }`<br>• **Companion object dengan nama** — `companion object Nama { ... }`<br>• **Akses** melalui nama kelas: `MyClass.method()`<br>• **Demo**: companion object sederhana dengan konstanta dan factory method | Ceramah, Demonstrasi, Live Coding |
| **45-75'** | Companion Object Lanjutan | • **Companion object sebagai Factory**<br>  - Private constructor + factory method<br>  - Validasi di factory method<br>  - Named constructor (misal: `createAdmin()`)<br>• **Companion object dengan interface**<br>• **Companion object dengan state** — class-level state dibagikan antar instance<br>• **Extension function untuk companion object**<br>• **Demo**: implementasi lengkap factory pattern dengan companion object | Ceramah, Demonstrasi, Live Coding |
| **75-95'** | Praktik Companion Object | • Mahasiswa membuat kelas `User` dengan private constructor dan companion object factory<br>• Menambahkan method `create()`, `createAdmin()`, `fromMap()`<br>• Membuat companion object dengan state (counter instance)<br>• Membuat extension function untuk companion object | Praktik mandiri, Asistensi |
| **95-120'** | Diskusi & Review | • Diskusi: "Perbedaan companion object vs object declaration di luar kelas?"<br>• Studi kasus: implementasi factory pattern untuk class `Product`<br>• Q&A | Diskusi, Tanya jawab |

---

### Sesi 4: Data Object, Studi Kasus Terintegrasi & Tugas 6 (2 Jam — 120 menit)

| **Waktu** | **Kegiatan** | **Detail** | **Metode** |
|---|---|---|---|
| **0-15'** | Review & Data Object | • Rangkuman seluruh materi pertemuan 6:<br>  - Data Class — `toString()`, `equals()`, `copy()`, destructuring<br>  - Object Declaration — singleton dengan `object`<br>  - Object Expression — anonymous object<br>  - Companion Object — static members<br>• **Data Object** — `data object` untuk singleton dengan `toString()` dan `equals()` otomatis | Review, Ceramah |
| **15-45'** | Studi Kasus Terintegrasi | • Dosen menjelaskan studi kasus sistem manajemen toko (lihat bagian E)<br>• Menganalisis kebutuhan dan mendesain solusi menggunakan:<br>  - Data Class untuk `Product` dan `Order`<br>  - Object Declaration untuk `DatabaseManager`<br>  - Companion Object untuk `Order` factory<br>  - Data Object untuk `AppConfig`<br>• **Live coding** bersama dosen | Demonstrasi, Live Coding, Diskusi |
| **45-90'** | Pengerjaan Tugas 6 | • Mahasiswa mengerjakan Tugas 6 secara mandiri (lihat bagian E)<br>• Dosen berkeliling memberikan bimbingan intensif<br>• Mahasiswa dapat bertanya jika mengalami kendala | Praktik mandiri, Asistensi intensif |
| **90-105'** | Pengumpulan & Presentasi | • Mahasiswa mengumpulkan Tugas 6<br>• 2-3 mahasiswa diminta mempresentasikan kodenya<br>• Dosen memberikan feedback konstruktif | Presentasi, Feedback |
| **105-120'** | Penutupan | • Dosen merangkum pencapaian pertemuan 6<br>• Preview materi pertemuan 7 (Generic, Collection & Exception Handling)<br>• Memberikan tugas membaca modul pertemuan 7<br>• Menutup perkuliahan dengan doa dan salam | Ceramah |

---

## E. TUGAS 6 (Dikumpulkan)

### Sistem Manajemen Toko Online dengan Data Class, Object Declaration, dan Companion Object

Buatlah program lengkap sistem manajemen toko online dengan ketentuan berikut:

#### 1. Data Class `Product`

| **Komponen** | **Spesifikasi** |
|---|---|
| **Properti** | `id: String` (read-only)<br>`name: String` (read-only)<br>`price: Double` (read-only)<br>`stock: Int` (mutable) |
| **Fitur** | Gunakan data class agar mendapatkan `toString()`, `equals()`, `hashCode()`, `copy()` otomatis |

#### 2. Data Class `Order`

| **Komponen** | **Spesifikasi** |
|---|---|
| **Properti** | `id: String` (read-only)<br>`customerName: String` (read-only)<br>`items: List<Product>` (read-only)<br>`total: Double` (read-only — dihitung dari items)<br>`status: OrderStatus` (mutable) |

#### 3. Sealed Class `OrderStatus` (dari pertemuan 5)

- `Pending` — pesanan menunggu
- `Processing` — pesanan diproses
- `Shipped` — pesanan dikirim
- `Delivered` — pesanan diterima
- `Cancelled` — pesanan dibatalkan

#### 4. Object Declaration `DatabaseManager`

| **Komponen** | **Spesifikasi** |
|---|---|
| **Properti** | `products: MutableList<Product>` (private)<br>`orders: MutableList<Order>` (private)<br>`isConnected: Boolean` |
| **Metode** | `connect(): Boolean`<br>`disconnect(): Boolean`<br>`addProduct(product: Product)`<br>`addOrder(order: Order)`<br>`findProduct(id: String): Product?`<br>`findOrder(id: String): Order?`<br>`getAllProducts(): List<Product>`<br>`getAllOrders(): List<Order>`<br>`getOrdersByCustomer(customer: String): List<Order>` |

#### 5. Companion Object untuk `Order` (Factory Pattern)

| **Komponen** | **Spesifikasi** |
|---|---|
| **Method** | `create(customerName: String, items: List<Product>): Order` — membuat order baru dengan ID unik dan total otomatis<br>`createFromMap(map: Map<String, Any>): Order?` — membuat order dari Map |

#### 6. Data Object `AppConfig`

| **Komponen** | **Spesifikasi** |
|---|---|
| **Properti** | `appName: String = "Toko Online"`<br>`version: String = "1.0.0"`<br>`taxRate: Double = 0.11` (PPN 11%)<br>`isDebugMode: Boolean = true` |

#### 7. Fungsi `main()`

- Tampilkan `AppConfig` menggunakan `toString()` otomatis
- Gunakan `DatabaseManager` untuk menambah produk dan order
- Tampilkan semua produk dan order
- Tampilkan total pendapatan dari semua order
- Gunakan **data class** untuk `Product` dan `Order`
- Gunakan **object declaration** untuk `DatabaseManager`
- Gunakan **companion object** untuk `Order` factory
- Gunakan **data object** untuk `AppConfig`

#### 8. Kriteria Penilaian Tugas 6

| **Kriteria** | **Bobot** | **Indikator** |
|---|---|---|
| **Data Class** | 25% | • `Product` dan `Order` sebagai data class<br>• Menggunakan `copy()` dan destructuring<br>• Properti di primary constructor dengan `val` |
| **Object Declaration** | 20% | • `DatabaseManager` sebagai object declaration<br>• Singleton pattern diimplementasikan dengan benar<br>• Method akses data berfungsi |
| **Companion Object** | 25% | • `Order` memiliki companion object<br>• Factory method `create()` dan `createFromMap()` berfungsi<br>• Private constructor digunakan |
| **Data Object** | 10% | • `AppConfig` sebagai data object<br>• `toString()` otomatis berfungsi |
| **Fungsi main()** | 10% | • Menampilkan semua skenario yang diminta<br>• Output jelas dan informatif |
| **Kode Berkualitas** | 10% | • Kode bersih, terstruktur, diberi komentar<br>• Menggunakan naming convention yang benar |

---

## F. MEDIA DAN ALAT PEMBELAJARAN

| **Media** | **Keterangan** |
|---|---|
| **Laptop/PC** | Setiap mahasiswa menggunakan laptop/PC masing-masing |
| **IntelliJ IDEA** | IDE utama untuk pengembangan Kotlin |
| **JDK** | Java Development Kit (versi 11 atau 17) |
| **Proyektor/LCD** | Untuk presentasi dan demonstrasi dosen |
| **Whiteboard** | Untuk menjelaskan konsep dan perbandingan |
| **Modul Praktikum** | Modul cetak/digital pertemuan 6 |
| **Kotlin Playground** | Alternatif untuk mencoba kode tanpa instalasi |

---

## G. PENILAIAN PERTEMUAN 6

| **Komponen** | **Bobot** | **Indikator** | **Teknik** |
|---|---|---|---|
| **Keaktifan Sesi 1-3** | 15% dari total keaktifan | • Kehadiran tepat waktu<br>• Partisipasi dalam diskusi dan tanya jawab<br>• Keterlibatan dalam praktik | Observasi |
| **Tugas 6** | 100% dari nilai tugas 6 | • Lihat kriteria penilaian Tugas 6 di atas | Penilaian kode |
| **Kuis Singkat** | Bonus | • Pertanyaan tentang data class, object declaration, companion object | Tes tertulis/lisan |

---

## H. REFERENSI PERTEMUAN 6

### Referensi Utama:

1. **Kotlin Official Documentation – Data classes** — [https://kotlinlang.org/docs/data-classes.html](https://kotlinlang.org/docs/data-classes.html)

2. **Kotlin Official Documentation – Object declarations and expressions** — [https://kotlinlang.org/docs/object-declarations.html](https://kotlinlang.org/docs/object-declarations.html)

3. **Kotlin Official Documentation – Intermediate: Objects** — [https://kotlinlang.org/docs/kotlin-tour-intermediate-objects.html](https://kotlinlang.org/docs/kotlin-tour-intermediate-objects.html)

### Referensi Pendukung:

4. **Kotlin 伴生对象 (Companion Object)** — [https://zetcode.cn/kotlin/companion-keyword/](https://zetcode.cn/kotlin/companion-keyword/)

5. **Kotlin Data Class vs Regular Class** — Stack Overflow

---

## I. LAMPIRAN

### Lampiran 1: Perbandingan Data Class vs Class Biasa

| **Aspek** | **Data Class** | **Class Biasa** |
|---|---|---|
| **Keyword** | `data class` | `class` |
| **`toString()`** | Otomatis (format: `Class(prop=value)`) | Manual atau default (`ClassName@hashcode`) |
| **`equals()` / `hashCode()`** | Otomatis (berdasarkan properti) | Manual atau berdasarkan referensi |
| **`copy()`** | Otomatis | Manual |
| **Destructuring** | Otomatis (`component1()`, `component2()`, dst) | Manual |
| **Primary constructor** | Minimal 1 parameter | Bisa 0 parameter |
| **Tujuan** | Menyimpan data | Segala tujuan |

### Lampiran 2: Perbandingan Object Declaration vs Companion Object

| **Aspek** | **Object Declaration** | **Companion Object** |
|---|---|---|
| **Deklarasi** | Di luar kelas | Di dalam kelas |
| **Tujuan** | Singleton global | Static members untuk kelas |
| **Akses** | `NamaObject.method()` | `NamaKelas.method()` |
| **Instance** | Satu global | Satu per kelas |
| **Constructor** | Tidak bisa | Tidak bisa |

### Lampiran 3: Checklist Pemahaman Mahasiswa

| **No** | **Konsep** | **Paham** | **Kurang Paham** | **Tidak Paham** |
|---|---|---|---|---|
| 1 | Data class — tujuan dan manfaat | ☐ | ☐ | ☐ |
| 2 | Data class — `toString()`, `equals()`, `hashCode()` | ☐ | ☐ | ☐ |
| 3 | Data class — `copy()` | ☐ | ☐ | ☐ |
| 4 | Data class — destructuring declaration | ☐ | ☐ | ☐ |
| 5 | Object declaration — singleton | ☐ | ☐ | ☐ |
| 6 | Object declaration — lazy initialization | ☐ | ☐ | ☐ |
| 7 | Object expression — anonymous object | ☐ | ☐ | ☐ |
| 8 | Perbedaan object declaration vs expression | ☐ | ☐ | ☐ |
| 9 | Companion object — static members | ☐ | ☐ | ☐ |
| 10 | Companion object — factory pattern | ☐ | ☐ | ☐ |
| 11 | Companion object — dengan interface | ☐ | ☐ | ☐ |
| 12 | Data object — singleton dengan toString/equals | ☐ | ☐ | ☐ |
| 13 | Menerapkan ketiga konsep dalam kode | ☐ | ☐ | ☐ |

---

**Disusun oleh,**
[Nama Dosen Pengampu]
Dosen Program Studi D4 Teknologi Rekayasa Informatika Industri
