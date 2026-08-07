# MATERI AJAR PERTEMUAN 6
## PEMROGRAMAN BERORIENTASI OBJEK (OOP) DENGAN KOTLIN
### “Konsep Lanjutan: Data Class, Object Declaration, dan Companion Object”

---

# BAGIAN 1: DATA CLASS — KELAS PENYIMPAN DATA

## 1.1 Apa itu Data Class?

Dalam pemrograman, seringkali kita membuat kelas yang **tujuan utamanya hanya untuk menyimpan data**. Kelas seperti ini biasanya hanya berisi properti dan beberapa fungsi standar seperti `toString()`, `equals()`, dan `hashCode()`.

Di Kotlin, kelas seperti ini disebut **Data Class** dan ditandai dengan keyword `data`.

> **Definisi Sederhana:** Data Class adalah "kelas penyimpan data" yang membebaskan Anda dari menulis kode berulang (boilerplate) seperti `toString()`, `equals()`, `hashCode()`, dan `copy()`.

### 1.1.1 Mengapa Data Class?

Bayangkan Anda harus menulis kelas `User` secara manual:

```kotlin
// Tanpa Data Class — banyak kode berulang!
class User(val name: String, val age: Int) {
    override fun toString(): String {
        return "User(name='$name', age=$age)"
    }

    override fun equals(other: Any?): Boolean {
        if (this === other) return true
        if (other !is User) return false
        return name == other.name && age == other.age
    }

    override fun hashCode(): Int {
        var result = name.hashCode()
        result = 31 * result + age
        return result
    }

    fun copy(name: String = this.name, age: Int = this.age): User {
        return User(name, age)
    }
}

// Dengan Data Class — SATU BARIS!
data class User(val name: String, val age: Int)
```

---

## 1.2 Fungsi yang Dihasilkan Secara Otomatis

Untuk setiap data class, compiler Kotlin secara otomatis menghasilkan **lima fungsi penting**:

| **Fungsi** | **Kegunaan** | **Contoh Output** |
|---|---|---|
| `toString()` | Representasi string yang readable | `User(name=John, age=42)` |
| `equals()` | Membandingkan berdasarkan nilai properti | `user1 == user2` → true jika semua properti sama |
| `hashCode()` | Menghasilkan hash code berdasarkan properti | Digunakan untuk collection seperti HashMap |
| `copy()` | Membuat salinan dengan beberapa properti diubah | `user.copy(age = 30)` |
| `componentN()` | Mendukung destructuring declaration | `val (name, age) = user` |

### 1.2.1 Contoh Penggunaan

```kotlin
data class User(val name: String, val age: Int)

fun main() {
    val user1 = User("John", 42)
    val user2 = User("John", 42)

    // 1. toString() — output yang readable
    println(user1)
    // Output: User(name=John, age=42)

    // 2. equals() — membandingkan berdasarkan nilai
    println(user1 == user2)  // Output: true (nilai sama)
    println(user1 === user2) // Output: false (referensi berbeda)

    // 3. hashCode() — berdasarkan properti
    println(user1.hashCode()) // Output: (nilai hash berdasarkan name dan age)

    // 4. copy() — copy dengan modifikasi
    val user3 = user1.copy(age = 30)
    println(user3)  // Output: User(name=John, age=30)

    // 5. Destructuring declaration
    val (name, age) = user1
    println("Name: $name, Age: $age")  // Output: Name: John, Age: 42
}
```

---

## 1.3 Aturan Data Class

Data class di Kotlin harus memenuhi persyaratan berikut:

| **Aturan** | **Penjelasan** |
|---|---|
| **Primary constructor minimal 1 parameter** | Data class harus memiliki setidaknya satu properti di primary constructor |
| **Semua parameter primary constructor harus `val` atau `var`** | Properti harus dideklarasikan dengan `val` (immutable) atau `var` (mutable) |
| **Tidak bisa `abstract`, `open`, `sealed`, atau `inner`** | Data class memiliki batasan inheritance |
| **Properti di class body tidak diikutsertakan** | Hanya properti di primary constructor yang digunakan untuk `toString()`, `equals()`, `hashCode()`, dan `copy()` |

### 1.3.1 Properti di Class Body — Tidak Diikutsertakan

Properti yang dideklarasikan di **class body** (bukan di primary constructor) **tidak** diikutsertakan dalam fungsi yang dihasilkan secara otomatis.

```kotlin
data class Person(val name: String) {
    var age: Int = 0  // ❌ TIDAK diikutsertakan dalam toString/equals/hashCode
}

fun main() {
    val p1 = Person("Alice")
    p1.age = 25
    val p2 = Person("Alice")
    p2.age = 30

    // equals() hanya membandingkan properti di primary constructor (name)
    println(p1 == p2)  // Output: true (name sama, age diabaikan)
    println(p1)        // Output: Person(name=Alice) (age tidak ditampilkan)
}
```

---

## 1.4 Praktik Terbaik Data Class

> **Gunakan `val` (immutable) sebisa mungkin** untuk membuat data class yang aman dan mudah diprediksi.

```kotlin
// ✅ Direkomendasikan: immutable data class
data class Product(val id: Int, val name: String, val price: Double)

// ⚠️ Boleh tapi kurang direkomendasikan: mutable data class
data class MutableProduct(var id: Int, var name: String, var price: Double)
```

### 1.4.1 Mengapa `val` Lebih Baik?

1. **Thread-safe** — objek immutable aman untuk multi-thread
2. **Predictable** — nilai tidak berubah setelah dibuat
3. **Mudah di-debug** — tidak ada efek samping yang tidak terduga
4. **Cocok untuk functional programming** — lebih mudah dikomposisi

---

## 1.5 Data Class dengan Inheritance

Data class dapat **mewarisi** dari kelas lain (termasuk sealed class).

```kotlin
// Data class mewarisi dari sealed class
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

### 1.5.1 Data Class dengan Default Values

Untuk JVM, jika data class membutuhkan constructor tanpa parameter, gunakan default values:

```kotlin
data class User(val name: String = "", val age: Int = 0)
// Sekarang bisa dibuat tanpa parameter: User()
```

---

## 1.6 Destructuring Declaration

Data class secara otomatis mendukung **destructuring declaration** — membongkar objek menjadi variabel terpisah.

```kotlin
data class Student(val id: String, val name: String, val gpa: Double)

fun main() {
    val student = Student("S001", "Budi", 3.75)

    // Destructuring — membongkar menjadi 3 variabel
    val (id, name, gpa) = student
    println("ID: $id, Name: $name, GPA: $gpa")
    // Output: ID: S001, Name: Budi, GPA: 3.75

    // Bisa juga di loop
    val students = listOf(
        Student("S001", "Budi", 3.75),
        Student("S002", "Siti", 3.50)
    )
    for ((id, name, gpa) in students) {
        println("$id: $name ($gpa)")
    }
}
```

---

# BAGIAN 2: OBJECT DECLARATION — SINGLETON PATTERN

## 2.1 Apa itu Object Declaration?

**Object Declaration** adalah cara di Kotlin untuk **mendeklarasikan kelas dan membuat satu-satunya instance-nya dalam satu langkah**.

> **Definisi Sederhana:** Object Declaration adalah "cara termudah membuat Singleton di Kotlin" — sebuah kelas yang hanya memiliki satu instance dan bisa diakses secara global.

### 2.1.1 Apa itu Singleton?

**Singleton** adalah sebuah kelas yang **hanya memiliki satu instance** dan menyediakan titik akses global ke instance tersebut. Singleton sangat berguna untuk:
- **Shared resources** — database connection pool, configuration manager
- **Factory methods** — cara efisien untuk membuat instance
- **Global coordination** — logging, authentication

---

## 2.2 Karakteristik Object Declaration

| **Karakteristik** | **Penjelasan** |
|---|---|
| **Singleton** | Hanya ada satu instance dari object tersebut |
| **Lazy Initialization** | Object dibuat hanya ketika pertama kali diakses |
| **Thread-Safe** | Inisialisasi object aman untuk multi-thread |
| **Tidak bisa memiliki constructor** | Object tidak bisa memiliki constructor karena instance-nya sudah tunggal |
| **Bisa memiliki supertype** | Object bisa mewarisi class atau mengimplementasikan interface |
| **Bukan expression** | Object declaration tidak bisa digunakan di sisi kanan assignment |

---

## 2.3 Sintaks Object Declaration

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
    DatabaseManager.connect()    // Output: 🔗 Connecting to database...
    DatabaseManager.connect()    // Output: ✅ Already connected
    println(DatabaseManager.getStatus())  // Output: 🟢 Connected

    // ❌ Tidak bisa membuat instance baru
    // val db = DatabaseManager()  // ERROR!
}
```

---

## 2.4 Object Declaration dengan Interface dan Inheritance

Object declaration dapat **mengimplementasikan interface** dan **mewarisi class**.

### 2.4.1 Dengan Interface

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

### 2.4.2 Dengan Abstract Class

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

## 2.5 Object Declaration — Lazy Initialization

Object declaration diinisialisasi **secara lazy** — hanya ketika pertama kali diakses.

```kotlin
object HeavyObject {
    init {
        println("🔥 HeavyObject initialized! (only once)")
    }

    fun doWork() {
        println("⚡ Doing work...")
    }
}

fun main() {
    println("Program started")
    // HeavyObject BELUM dibuat

    println("Calling HeavyObject...")
    HeavyObject.doWork()  // ← Di sini HeavyObject dibuat!
    // Output: 🔥 HeavyObject initialized! (only once)
    //         ⚡ Doing work...

    HeavyObject.doWork()  // ← Tidak dibuat lagi
    // Output: ⚡ Doing work...
}
```

---

# BAGIAN 3: OBJECT EXPRESSION — ANONYMOUS OBJECT

## 3.1 Apa itu Object Expression?

**Object Expression** digunakan untuk membuat **objek anonim (tanpa nama)** dari sebuah kelas atau interface secara langsung, tanpa harus mendeklarasikan subclass secara eksplisit.

> **Perbedaan Utama:** Object Declaration = **bernama** (singleton), Object Expression = **anonim** (sekali pakai).

---

## 3.2 Karakteristik Object Expression

| **Karakteristik** | **Penjelasan** |
|---|---|
| **Tanpa nama** | Object expression tidak memiliki nama |
| **Sekali pakai** | Digunakan untuk satu keperluan spesifik |
| **Dieksekusi segera** | Object expression diinisialisasi saat digunakan |
| **Bisa digunakan di sisi kanan assignment** | Object expression adalah expression |
| **Bisa memiliki properti dan method** | Object expression bisa memiliki member tambahan |

---

## 3.3 Contoh Object Expression

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

---

## 3.4 Perbandingan Object Declaration vs Object Expression

| **Aspek** | **Object Declaration** | **Object Expression** |
|---|---|---|
| **Nama** | Memiliki nama | Tanpa nama (anonim) |
| **Singleton** | Ya (satu instance global) | Tidak (instance baru setiap kali) |
| **Inisialisasi** | Lazy (saat pertama diakses) | Immediate (saat dibuat) |
| **Penggunaan** | Global, reusable | Sekali pakai, lokal |
| **Assignment** | Tidak bisa di sisi kanan | Bisa di sisi kanan |
| **Contoh** | `object DatabaseManager` | `object : ClickListener { ... }` |

---

# BAGIAN 4: COMPANION OBJECT — STATIC MEMBERS

## 4.1 Apa itu Companion Object?

**Companion Object** adalah object declaration yang dideklarasikan **di dalam sebuah kelas**. Fungsinya adalah untuk menyediakan **anggota kelas (method/property) yang dapat diakses tanpa harus membuat instance dari kelas tersebut**.

> **Definisi Sederhana:** Companion Object adalah "pengganti static member di Java" — memungkinkan Anda memanggil method seperti `MyClass.method()` tanpa membuat objek.

---

## 4.2 Karakteristik Companion Object

| **Karakteristik** | **Penjelasan** |
|---|---|
| **Class-level members** | Anggota companion object terikat ke kelas, bukan ke instance |
| **Akses tanpa instansiasi** | Bisa dipanggil langsung melalui nama kelas |
| **Hanya satu per kelas** | Setiap kelas hanya bisa memiliki satu companion object |
| **Bisa memiliki nama** | Bisa diberi nama (opsional) |
| **Bisa mengimplementasikan interface** | Companion object bisa mengimplementasikan interface |
| **Diinisialisasi saat kelas dimuat** | Companion object diinisialisasi ketika kelasnya direferensi pertama kali |

---

## 4.3 Sintaks Dasar Companion Object

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

### 4.3.1 Companion Object dengan Nama

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

### 4.3.2 Companion Object — Nama Default "Companion"

Jika tidak diberi nama, companion object secara default bernama `Companion`:

```kotlin
class MyClass {
    companion object {
        fun hello() = println("Hello!")
    }
}

fun main() {
    // Bisa diakses tanpa nama
    MyClass.hello()

    // Bisa juga diakses melalui nama default "Companion"
    MyClass.Companion.hello()
}
```

---

## 4.4 Companion Object sebagai Factory Method

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

---

## 4.5 Companion Object dengan Interface

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

---

## 4.6 Companion Object dengan State (Class-level State)

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

---

## 4.7 Companion Object Extension Functions

Kita bisa menambahkan **extension function** ke companion object:

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

## 4.8 Companion Object vs Object Declaration

| **Aspek** | **Object Declaration** | **Companion Object** |
|---|---|---|
| **Deklarasi** | Di luar kelas | Di dalam kelas |
| **Tujuan** | Singleton global | Static members untuk kelas |
| **Akses** | `NamaObject.method()` | `NamaKelas.method()` |
| **Instance** | Satu global | Satu per kelas |
| **Constructor** | Tidak bisa | Tidak bisa |
| **Nama default** | Harus diberi nama | `Companion` |

---

# BAGIAN 5: DATA OBJECT — SINGLETON DENGAN TOSTRING/EQUALS

## 5.1 Apa itu Data Object?

**Data Object** adalah object declaration yang ditandai dengan keyword `data`. Mirip dengan data class, data object secara otomatis memiliki fungsi `toString()` dan `equals()`.

> **Perbedaan dengan Data Class:** Data object **tidak** memiliki fungsi `copy()` karena object declaration hanya memiliki satu instance yang tidak bisa di-copy.

---

## 5.2 Karakteristik Data Object

| **Karakteristik** | **Penjelasan** |
|---|---|
| **Singleton** | Hanya satu instance |
| **`toString()` otomatis** | Menampilkan nama object |
| **`equals()` otomatis** | Semua instance dianggap sama |
| **Tidak ada `copy()`** | Karena hanya satu instance |

---

## 5.3 Contoh Data Object

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
    println(DefaultSettings)  // Output: DefaultSettings

    // equals() berdasarkan identitas (hanya satu instance)
    val config1 = AppConfig
    val config2 = AppConfig
    println(config1 == config2)  // Output: true (satu instance yang sama)

    // Mengakses properti
    println(AppConfig.appName)   // Output: My Application
    AppConfig.appName = "New App"
    println(AppConfig.appName)   // Output: New App

    println(DefaultSettings.theme)  // Output: Dark
}
```

---

## 5.4 Data Object vs Data Class

| **Aspek** | **Data Object** | **Data Class** |
|---|---|---|
| **Keyword** | `data object` | `data class` |
| **Instance** | Singleton (satu instance) | Banyak instance |
| **`toString()`** | ✅ Otomatis | ✅ Otomatis |
| **`equals()`/`hashCode()`** | ✅ Otomatis | ✅ Otomatis |
| **`copy()`** | ❌ Tidak ada | ✅ Otomatis |
| **Destructuring** | ❌ Tidak ada | ✅ Otomatis |
| **Kapan Gunakan** | Singleton dengan data | Data container |

---

# BAGIAN 6: STUDI KASUS — SISTEM MANAJEMEN TOKO

Mari kita bangun sistem manajemen toko yang mengintegrasikan semua konsep yang telah dipelajari.

## 6.1 Analisis Kebutuhan

| **Komponen** | **Konsep yang Digunakan** | **Tujuan** |
|---|---|---|
| **Product** | Data Class | Menyimpan data produk dengan `toString()`, `equals()`, `copy()` |
| **Order** | Data Class | Menyimpan data pesanan |
| **OrderStatus** | Sealed Class | Status pesanan yang terbatas |
| **OrderFactory** | Companion Object | Factory untuk membuat Order |
| **DatabaseManager** | Object Declaration | Singleton untuk mengelola data |
| **AppConfig** | Data Object | Konfigurasi aplikasi global |

## 6.2 Implementasi Lengkap

```kotlin
/**
 * ============================================================
 * SISTEM MANAJEMEN TOKO DENGAN DATA CLASS, OBJECT DECLARATION,
 * COMPANION OBJECT, DAN DATA OBJECT
 * ============================================================
 * Demonstrasi:
 * 1. Data Class untuk Product dan Order
 * 2. Object Declaration untuk DatabaseManager
 * 3. Companion Object untuk Order Factory
 * 4. Data Object untuk AppConfig
 * 5. Sealed Class untuk OrderStatus
 * ============================================================
 */

// ============================================================
// SEALED CLASS: OrderStatus
// ============================================================
sealed class OrderStatus {
    object Pending : OrderStatus()
    object Processing : OrderStatus()
    object Shipped : OrderStatus()
    object Delivered : OrderStatus()
    object Cancelled : OrderStatus()

    fun display(): String {
        return when (this) {
            Pending -> "⏳ Pending"
            Processing -> "🔄 Processing"
            Shipped -> "📦 Shipped"
            Delivered -> "✅ Delivered"
            Cancelled -> "❌ Cancelled"
        }
    }
}

// ============================================================
// DATA CLASS: Product
// ============================================================
data class Product(
    val id: String,
    val name: String,
    val price: Double,
    var stock: Int  // mutable karena stok bisa berubah
)

// ============================================================
// DATA CLASS: Order
// ============================================================
data class Order(
    val id: String,
    val customerName: String,
    val items: List<Product>,
    val total: Double,
    var status: OrderStatus
)

// ============================================================
// COMPANION OBJECT: Order Factory
// ============================================================
class Order private constructor(
    val id: String,
    val customerName: String,
    val items: List<Product>,
    val total: Double,
    var status: OrderStatus
) {
    companion object Factory {
        private var nextId = 1

        /**
         * Factory method untuk membuat Order baru
         * Menghitung total otomatis dari items
         */
        fun create(customerName: String, items: List<Product>): Order {
            val total = items.sumOf { it.price }
            val id = "ORD-${String.format("%04d", nextId)}"
            nextId++
            return Order(id, customerName, items, total, OrderStatus.Pending)
        }

        /**
         * Factory method dari Map
         */
        fun fromMap(map: Map<String, Any>): Order? {
            val customerName = map["customerName"] as? String ?: return null
            val items = map["items"] as? List<Product> ?: return null
            return create(customerName, items)
        }

        /**
         * Reset counter (untuk testing)
         */
        fun resetCounter() {
            nextId = 1
        }
    }
}

// ============================================================
// DATA OBJECT: AppConfig
// ============================================================
data object AppConfig {
    var appName: String = "Toko Online"
    var version: String = "1.0.0"
    val taxRate: Double = 0.11  // PPN 11%
    var isDebugMode: Boolean = true

    fun display() {
        println("=" .repeat(40))
        println("📱 APP CONFIG")
        println("=" .repeat(40))
        println("App Name  : $appName")
        println("Version   : $version")
        println("Tax Rate  : ${taxRate * 100}%")
        println("Debug Mode: $isDebugMode")
        println("=" .repeat(40))
    }
}

// ============================================================
// OBJECT DECLARATION: DatabaseManager (Singleton)
// ============================================================
object DatabaseManager {
    // Data stores — private
    private val _products = mutableListOf<Product>()
    private val _orders = mutableListOf<Order>()
    private var _isConnected: Boolean = false

    // Public properties
    val isConnected: Boolean get() = _isConnected
    val totalProducts: Int get() = _products.size
    val totalOrders: Int get() = _orders.size

    // Connection management
    fun connect(): Boolean {
        if (_isConnected) {
            println("✅ Already connected to database")
            return true
        }
        println("🔗 Connecting to database...")
        _isConnected = true
        println("✅ Connected successfully!")
        return true
    }

    fun disconnect(): Boolean {
        if (!_isConnected) {
            println("⚠️ Already disconnected")
            return false
        }
        println("🔌 Disconnecting from database...")
        _isConnected = false
        println("✅ Disconnected successfully!")
        return true
    }

    // Product operations
    fun addProduct(product: Product) {
        if (!_isConnected) {
            println("❌ Cannot add product: database not connected")
            return
        }
        _products.add(product)
        println("✅ Product added: ${product.name} (${product.id})")
    }

    fun addProducts(vararg products: Product) {
        products.forEach { addProduct(it) }
    }

    fun findProduct(id: String): Product? {
        return _products.find { it.id == id }
    }

    fun getAllProducts(): List<Product> = _products.toList()

    fun getAvailableProducts(): List<Product> = _products.filter { it.stock > 0 }

    fun updateStock(productId: String, newStock: Int): Boolean {
        val product = findProduct(productId)
        return if (product != null) {
            product.stock = newStock
            println("✅ Stock updated for ${product.name}: $newStock")
            true
        } else {
            println("❌ Product not found: $productId")
            false
        }
    }

    // Order operations
    fun addOrder(order: Order) {
        if (!_isConnected) {
            println("❌ Cannot add order: database not connected")
            return
        }
        _orders.add(order)
        println("✅ Order added: ${order.id} (${order.customerName})")
    }

    fun findOrder(id: String): Order? {
        return _orders.find { it.id == id }
    }

    fun getAllOrders(): List<Order> = _orders.toList()

    fun getOrdersByCustomer(customer: String): List<Order> {
        return _orders.filter { it.customerName == customer }
    }

    fun getOrdersByStatus(status: OrderStatus): List<Order> {
        return _orders.filter { it.status == status }
    }

    fun updateOrderStatus(orderId: String, newStatus: OrderStatus): Boolean {
        val order = findOrder(orderId)
        return if (order != null) {
            order.status = newStatus
            println("✅ Order ${order.id} status updated to ${newStatus.display()}")
            true
        } else {
            println("❌ Order not found: $orderId")
            false
        }
    }

    // Reports
    fun getTotalRevenue(): Double {
        return _orders
            .filter { it.status == OrderStatus.Delivered }
            .sumOf { it.total }
    }

    fun getTotalRevenueWithTax(): Double {
        return getTotalRevenue() * (1 + AppConfig.taxRate)
    }

    fun displayAllProducts() {
        println("=" .repeat(50))
        println("📦 ALL PRODUCTS (${_products.size} items)")
        println("=" .repeat(50))
        if (_products.isEmpty()) {
            println("   No products available")
        } else {
            for (product in _products) {
                println("   ${product.id}: ${product.name}")
                println("      Price: Rp ${formatRupiah(product.price)}")
                println("      Stock: ${product.stock}")
            }
        }
        println("=" .repeat(50))
    }

    fun displayAllOrders() {
        println("=" .repeat(50))
        println("📋 ALL ORDERS (${_orders.size} orders)")
        println("=" .repeat(50))
        if (_orders.isEmpty()) {
            println("   No orders available")
        } else {
            for (order in _orders) {
                println("   ${order.id}: ${order.customerName}")
                println("      Items: ${order.items.size} item(s)")
                println("      Total: Rp ${formatRupiah(order.total)}")
                println("      Status: ${order.status.display()}")
            }
        }
        println("=" .repeat(50))
    }

    fun displayRevenueReport() {
        val revenue = getTotalRevenue()
        val revenueWithTax = getTotalRevenueWithTax()
        val tax = revenueWithTax - revenue

        println("=" .repeat(50))
        println("💰 REVENUE REPORT")
        println("=" .repeat(50))
        println("Total Orders      : ${_orders.size}")
        println("Delivered Orders  : ${getOrdersByStatus(OrderStatus.Delivered).size}")
        println("Revenue (excl. tax): Rp ${formatRupiah(revenue)}")
        println("Tax (${AppConfig.taxRate * 100}%)      : Rp ${formatRupiah(tax)}")
        println("Revenue (incl. tax): Rp ${formatRupiah(revenueWithTax)}")
        println("=" .repeat(50))
    }

    // Helper
    private fun formatRupiah(nominal: Double): String {
        val str = nominal.toLong().toString()
        val builder = StringBuilder()
        var count = 0
        for (i in str.length - 1 downTo 0) {
            builder.insert(0, str[i])
            count++
            if (count % 3 == 0 && i > 0) {
                builder.insert(0, ".")
            }
        }
        return builder.toString()
    }
}

// ============================================================
// FUNGSI UTAMA
// ============================================================
fun main() {
    println("=" .repeat(55))
    println("🏪 SISTEM MANAJEMEN TOKO")
    println("=" .repeat(55))
    println()

    // ============================================================
    // 1. DEMONSTRASI DATA OBJECT
    // ============================================================
    println("--- APP CONFIG (Data Object) ---")
    AppConfig.display()
    println()

    // ============================================================
    // 2. DEMONSTRASI DATABASE MANAGER (Object Declaration)
    // ============================================================
    println("--- DATABASE MANAGER (Object Declaration) ---")
    DatabaseManager.connect()
    println()

    // ============================================================
    // 3. DEMONSTRASI DATA CLASS: Product
    // ============================================================
    println("--- PRODUCTS (Data Class) ---")
    val product1 = Product("P001", "Laptop", 15_000_000.0, 10)
    val product2 = Product("P002", "Mouse", 250_000.0, 50)
    val product3 = Product("P003", "Keyboard", 500_000.0, 30)
    val product4 = Product("P004", "Monitor", 3_500_000.0, 15)

    DatabaseManager.addProducts(product1, product2, product3, product4)
    DatabaseManager.displayAllProducts()
    println()

    // Demonstrasi copy() dari Data Class
    val product1Discounted = product1.copy(price = 14_000_000.0)
    println("Original: $product1")
    println("Discounted: $product1Discounted")
    println()

    // Demonstrasi destructuring dari Data Class
    val (id, name, price, stock) = product1
    println("Destructuring: ID=$id, Name=$name, Price=$price, Stock=$stock")
    println()

    // ============================================================
    // 4. DEMONSTRASI COMPANION OBJECT: Order Factory
    // ============================================================
    println("--- ORDERS (Data Class dengan Companion Object Factory) ---")

    // Membuat order menggunakan factory method
    val order1 = Order.create("Budi Santoso", listOf(product1, product2))
    val order2 = Order.create("Siti Rahayu", listOf(product3, product4))
    val order3 = Order.create("Ahmad Fauzi", listOf(product2, product3, product4))

    DatabaseManager.addOrder(order1)
    DatabaseManager.addOrder(order2)
    DatabaseManager.addOrder(order3)

    DatabaseManager.displayAllOrders()
    println()

    // ============================================================
    // 5. DEMONSTRASI UPDATE ORDER STATUS
    // ============================================================
    println("--- UPDATING ORDER STATUS ---")
    DatabaseManager.updateOrderStatus(order1.id, OrderStatus.Processing)
    DatabaseManager.updateOrderStatus(order1.id, OrderStatus.Shipped)
    DatabaseManager.updateOrderStatus(order2.id, OrderStatus.Delivered)
    DatabaseManager.updateOrderStatus(order3.id, OrderStatus.Cancelled)
    println()

    DatabaseManager.displayAllOrders()
    println()

    // ============================================================
    // 6. DEMONSTRASI REVENUE REPORT
    // ============================================================
    DatabaseManager.displayRevenueReport()
    println()

    // ============================================================
    // 7. DEMONSTRASI PENGGUNAAN SEALED CLASS
    // ============================================================
    println("--- ORDER STATUS (Sealed Class) ---")
    val statuses = listOf(
        OrderStatus.Pending,
        OrderStatus.Processing,
        OrderStatus.Shipped,
        OrderStatus.Delivered,
        OrderStatus.Cancelled
    )
    for (status in statuses) {
        println("   ${status.display()}")
    }
    println()

    // ============================================================
    // 8. DEMONSTRASI FILTERING
    // ============================================================
    println("--- FILTERED ORDERS ---")
    val deliveredOrders = DatabaseManager.getOrdersByStatus(OrderStatus.Delivered)
    println("Delivered orders: ${deliveredOrders.size}")
    deliveredOrders.forEach { println("   ${it.id}: ${it.customerName} - Rp ${formatRupiah(it.total)}") }

    val cancelledOrders = DatabaseManager.getOrdersByStatus(OrderStatus.Cancelled)
    println("Cancelled orders: ${cancelledOrders.size}")
    cancelledOrders.forEach { println("   ${it.id}: ${it.customerName} - Rp ${formatRupiah(it.total)}") }
    println()

    // ============================================================
    // 9. DEMONSTRASI CLEANUP
    // ============================================================
    DatabaseManager.disconnect()

    println()
    println("=" .repeat(55))
    println("🏁 PROGRAM SELESAI")
    println("=" .repeat(55))
}

// Helper function
fun formatRupiah(nominal: Double): String {
    val str = nominal.toLong().toString()
    val builder = StringBuilder()
    var count = 0
    for (i in str.length - 1 downTo 0) {
        builder.insert(0, str[i])
        count++
        if (count % 3 == 0 && i > 0) {
            builder.insert(0, ".")
        }
    }
    return builder.toString()
}
```

---

# BAGIAN 7: RINGKASAN MATERI PERTEMUAN 6

## 7.1 Poin-Poin Penting

| **Konsep** | **Penjelasan** | **Keyword/Sintaks** |
|---|---|---|
| **Data Class** | Kelas untuk menyimpan data — otomatis `toString()`, `equals()`, `hashCode()`, `copy()`, `componentN()` | `data class` |
| **Object Declaration** | Singleton — satu instance global, lazy initialization, thread-safe | `object` |
| **Object Expression** | Anonymous object — sekali pakai, dieksekusi segera | `object : Interface` |
| **Companion Object** | Static members setara Java — akses tanpa instansiasi | `companion object` |
| **Data Object** | Singleton dengan `toString()` dan `equals()` otomatis | `data object` |

---

## 7.2 Kapan Menggunakan Apa?

| **Skenario** | **Solusi** | **Contoh** |
|---|---|---|
| Kelas hanya untuk menyimpan data | Data Class | `data class User` |
| Butuh singleton global | Object Declaration | `object DatabaseManager` |
| Butuh object anonim sekali pakai | Object Expression | `object : ClickListener` |
| Butuh static members seperti di Java | Companion Object | `companion object { ... }` |
| Singleton dengan toString/equals otomatis | Data Object | `data object AppConfig` |

---

# BAGIAN 8: LATIHAN DAN TUGAS

## 8.1 Latihan Mandiri

### Latihan 1: Data Class `Book`

Buatlah data class `Book` dengan properti: `id`, `title`, `author`, `year`, `price`. Demonstrasikan:
- `toString()` — cetak objek
- `equals()` — bandingkan dua buku
- `copy()` — buat salinan dengan tahun berbeda
- Destructuring — bongkar menjadi variabel

### Latihan 2: Object Declaration `MathUtils`

Buatlah object declaration `MathUtils` dengan method:
- `factorial(n: Int): Long` — menghitung faktorial
- `isPrime(n: Int): Boolean` — mengecek bilangan prima
- `fibonacci(n: Int): List<Int>` — menghasilkan deret Fibonacci

### Latihan 3: Companion Object `Logger`

Buatlah kelas `Logger` dengan companion object yang memiliki:
- `logLevel: String` — level logging (INFO, WARNING, ERROR)
- `log(message: String)` — mencetak log dengan timestamp
- `setLevel(level: String)` — mengubah level logging

---

## 8.2 Tugas 6 (Dikumpulkan)

### Sistem Manajemen Perpustakaan dengan Data Class, Object Declaration, dan Companion Object

Buatlah program lengkap sistem manajemen perpustakaan dengan ketentuan berikut:

#### 1. Data Class `Book`

| **Komponen** | **Spesifikasi** |
|---|---|
| **Properti** | `id: String` (read-only)<br>`title: String` (read-only)<br>`author: String` (read-only)<br>`year: Int` (read-only)<br>`isBorrowed: Boolean` (mutable) |

#### 2. Data Class `Member`

| **Komponen** | **Spesifikasi** |
|---|---|
| **Properti** | `id: String` (read-only)<br>`name: String` (read-only)<br>`email: String` (read-only)<br>`borrowedBooks: List<Book>` (read-only) |

#### 3. Sealed Class `BorrowStatus`

- `Available` — buku tersedia
- `Borrowed(by: String, date: String)` — buku dipinjam oleh member pada tanggal tertentu
- `Reserved(by: String)` — buku di-reservasi oleh member

#### 4. Companion Object untuk `Book` (Factory)

| **Komponen** | **Spesifikasi** |
|---|---|
| **Method** | `create(title: String, author: String, year: Int): Book` — membuat buku dengan ID unik<br>`fromMap(map: Map<String, Any>): Book?` — membuat buku dari Map |

#### 5. Object Declaration `LibraryManager`

| **Komponen** | **Spesifikasi** |
|---|---|
| **Properti** | `books: MutableList<Book>` (private)<br>`members: MutableList<Member>` (private) |
| **Metode** | `addBook(book: Book)`<br>`addMember(member: Member)`<br>`findBook(id: String): Book?`<br>`findMember(id: String): Member?`<br>`borrowBook(bookId: String, memberId: String): Boolean`<br>`returnBook(bookId: String): Boolean`<br>`getAvailableBooks(): List<Book>`<br>`getBorrowedBooks(): List<Book>`<br>`displayAllBooks()`<br>`displayAllMembers()` |

#### 6. Data Object `LibraryConfig`

| **Komponen** | **Spesifikasi** |
|---|---|
| **Properti** | `libraryName: String = "Perpustakaan Kampus"`<br>`maxBorrowDays: Int = 14`<br>`maxBooksPerMember: Int = 5` |

#### 7. Fungsi `main()`

- Tampilkan `LibraryConfig`
- Tambahkan minimal 5 buku dan 3 member
- Tampilkan semua buku
- Lakukan peminjaman dan pengembalian
- Tampilkan buku yang tersedia dan dipinjam
- Gunakan **data class** untuk `Book` dan `Member`
- Gunakan **object declaration** untuk `LibraryManager`
- Gunakan **companion object** untuk `Book` factory
- Gunakan **data object** untuk `LibraryConfig`

#### 8. Kriteria Penilaian Tugas 6

| **Kriteria** | **Bobot** | **Indikator** |
|---|---|---|
| **Data Class** | 25% | `Book` dan `Member` sebagai data class dengan `copy()` dan destructuring |
| **Object Declaration** | 20% | `LibraryManager` sebagai singleton dengan method lengkap |
| **Companion Object** | 25% | `Book` memiliki companion object dengan factory method |
| **Data Object** | 10% | `LibraryConfig` sebagai data object |
| **Fungsi main()** | 10% | Menampilkan semua skenario |
| **Kode Berkualitas** | 10% | Kode bersih, terstruktur, diberi komentar |

---

# BAGIAN 9: REFERENSI

## 9.1 Referensi Utama

1. **Kotlin Official Documentation – Data classes** — [https://kotlinlang.org/docs/data-classes.html](https://kotlinlang.org/docs/data-classes.html)

2. **Kotlin Official Documentation – Object declarations and expressions** — [https://kotlinlang.org/docs/object-declarations.html](https://kotlinlang.org/docs/object-declarations.html)

3. **Kotlin Official Documentation – Intermediate: Objects** — [https://kotlinlang.org/docs/kotlin-tour-intermediate-objects.html](https://kotlinlang.org/docs/kotlin-tour-intermediate-objects.html)

---

# BAGIAN 10: PENUTUP

## 10.1 Pesan untuk Mahasiswa

> **"Data Class menghemat waktu Anda menulis boilerplate. Object Declaration memberi Anda Singleton yang aman. Companion Object menggantikan static member Java. Kuasai ketiganya, dan kode Kotlin Anda akan lebih bersih, aman, dan profesional!"**

Pertemuan 6 ini memperkenalkan tiga konsep Kotlin yang sangat powerful:

1. **Data Class** — menghemat Anda dari menulis `toString()`, `equals()`, `hashCode()`, dan `copy()` secara manual
2. **Object Declaration** — implementasi Singleton yang aman dan lazy
3. **Companion Object** — pengganti static member Java yang elegan

**Ingatlah:**
1. **Data Class** = untuk menyimpan data — gunakan `val` sebisa mungkin
2. **Object Declaration** = untuk Singleton global — lazy dan thread-safe
3. **Object Expression** = untuk object anonim sekali pakai
4. **Companion Object** = untuk static members — akses tanpa instansiasi
5. **Data Object** = Singleton dengan `toString()` dan `equals()` otomatis

---

**Disusun oleh,**  
[Nama Dosen Pengampu]
Dosen Program Studi D4 Teknologi Rekayasa Informatika Industri
