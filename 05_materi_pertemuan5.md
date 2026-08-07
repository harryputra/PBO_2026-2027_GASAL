# MATERI AJAR PERTEMUAN 5
## PEMROGRAMAN BERORIENTASI OBJEK (OOP) DENGAN KOTLIN
### “Abstraksi dan Interface — Menyembunyikan Kompleksitas, Mendefinisikan Kontrak”

---

# BAGIAN 1: KONSEP DASAR ABSTRAKSI

## 1.1 Apa itu Abstraksi?

**Abstraksi (Abstraction)** adalah salah satu dari **empat pilar utama OOP** yang berarti **menyembunyikan detail implementasi** dan **hanya menampilkan fitur-fitur esensial** dari sebuah objek.

> **Definisi Sederhana:** Abstraksi adalah kemampuan untuk **menyembunyikan kompleksitas** dan **hanya menampilkan apa yang perlu diketahui** oleh pengguna. Pengguna tidak perlu tahu *bagaimana* sesuatu bekerja, hanya *apa* yang bisa dilakukan.

---

## 1.2 Analogi Abstraksi dalam Kehidupan Nyata

| **Analogi** | **Penjelasan** |
|---|---|
| **Mengemudi Mobil** | Anda tahu cara mengemudi (setir, gas, rem) tanpa perlu tahu bagaimana mesin, transmisi, atau sistem bahan bakar bekerja di dalamnya. |
| **Menggunakan ATM** | Anda tahu cara mengambil uang (masukkan kartu, PIN, pilih jumlah) tanpa perlu tahu bagaimana sistem perbankan memproses transaksi di belakang layar. |
| **Menggunakan Smartphone** | Anda tahu cara menggunakan aplikasi (geser, tap, swipe) tanpa perlu tahu kode sumber atau arsitektur sistem operasinya. |
| **Memesan Makanan di Restoran** | Anda tahu cara memesan dari menu tanpa perlu tahu bagaimana koki memasak di dapur. |

---

## 1.3 Mengapa Abstraksi Penting?

| **Manfaat** | **Penjelasan** |
|---|---|
| **Menyederhanakan Kompleksitas** | Pengguna hanya perlu memahami interface, bukan implementasi |
| **Meningkatkan Maintainability** | Perubahan implementasi tidak mempengaruhi kode yang bergantung pada abstraksi |
| **Meningkatkan Reusability** | Abstraksi memungkinkan kode digunakan kembali dalam konteks yang berbeda |
| **Mendukung Polymorphism** | Abstraksi adalah fondasi untuk polimorfisme |
| **Membuat Kode Lebih Modular** | Setiap komponen memiliki tanggung jawab yang jelas |

---

## 1.4 Dua Cara Menerapkan Abstraksi di Kotlin

Kotlin menyediakan **dua mekanisme** untuk menerapkan abstraksi:

| **Mekanisme** | **Keyword** | **Tujuan** |
|---|---|---|
| **Abstract Class** | `abstract class` | Menyediakan **kerangka dasar** dengan beberapa implementasi dan beberapa yang belum diimplementasikan — **mendefinisikan "bagaimana" (How)**  |
| **Interface** | `interface` | Mendefinisikan **kontrak perilaku** tanpa implementasi (atau dengan default implementation) — **mendefinisikan "apa" (What)**  |

---

# BAGIAN 2: ABSTRACT CLASS DI KOTLIN

## 2.1 Apa itu Abstract Class?

**Abstract class** adalah kelas yang **tidak bisa di-instansiasi** (tidak bisa dibuat objeknya secara langsung). Abstract class digunakan sebagai **kerangka dasar** untuk kelas-kelas turunannya dan dapat dipahami sebagai **"implementasi setengah jadi"** — kelas yang sudah memiliki beberapa implementasi, tetapi masih memiliki bagian-bagian yang harus dilengkapi oleh subclass.

---

## 2.2 Karakteristik Abstract Class

| **Karakteristik** | **Penjelasan** | **Contoh** |
|---|---|---|
| **Tidak bisa di-instansiasi** | Tidak bisa membuat objek langsung dari abstract class | `val animal = Animal()` → ❌ ERROR |
| **Dapat memiliki constructor** | Abstract class bisa memiliki primary/secondary constructor | `abstract class Animal(val name: String)` |
| **Dapat memiliki state** | Bisa memiliki properti dengan backing field (`var`/`val`) | `var age: Int = 0` |
| **Dapat memiliki metode konkret** | Bisa memiliki metode dengan implementasi lengkap | `fun eat() { println("Eating...") }` |
| **Dapat memiliki metode abstrak** | Metode tanpa implementasi yang harus di-override oleh subclass | `abstract fun makeSound()` |
| **Single inheritance** | Sebuah kelas hanya bisa mewarisi satu abstract class | `class Dog : Animal()` |

---

## 2.3 Sintaks Abstract Class

```kotlin
// Abstract class dengan constructor dan state
abstract class Animal(val name: String) {
    // ✅ Bisa menyimpan state (backing field)
    var age: Int = 0

    // ✅ Bisa memiliki init block
    init {
        println("🐾 Animal $name created")
    }

    // ✅ Bisa memiliki metode konkret (dengan implementasi)
    fun eat() {
        println("$name is eating...")
    }

    // ✅ Bisa memiliki metode konkret dengan parameter
    fun sleep(hours: Int) {
        println("$name is sleeping for $hours hours...")
    }

    // ✅ Bisa memiliki metode abstrak — HARUS di-override oleh subclass
    abstract fun makeSound()

    // ✅ Bisa memiliki metode abstrak dengan parameter
    abstract fun move(distance: Double)
}

// Subclass — harus mengimplementasikan SEMUA metode abstrak
class Dog(name: String) : Animal(name) {
    override fun makeSound() {
        println("$name barks: Guk! Guk!")
    }

    override fun move(distance: Double) {
        println("$name runs $distance meters")
    }
}

class Cat(name: String) : Animal(name) {
    override fun makeSound() {
        println("$name meows: Meong! Meong!")
    }

    override fun move(distance: Double) {
        println("$name walks $distance meters silently")
    }
}

fun main() {
    // ❌ ERROR: Cannot create an instance of an abstract class
    // val animal = Animal("Buddy")

    // ✅ Bisa membuat instance dari subclass
    val dog = Dog("Buddy")
    val cat = Cat("Kitty")

    dog.eat()        // Output: Buddy is eating...
    dog.makeSound()  // Output: Buddy barks: Guk! Guk!
    dog.move(10.0)   // Output: Buddy runs 10.0 meters

    cat.makeSound()  // Output: Kitty meows: Meong! Meong!
    cat.move(5.0)    // Output: Kitty walks 5.0 meters silently
}
```

---

## 2.4 Abstract Class dengan Constructor dan Properti

```kotlin
/**
 * Abstract class Vehicle dengan primary constructor
 * dan properti yang diwarisi oleh subclass
 */
abstract class Vehicle(
    val brand: String,
    val model: String,
    val year: Int
) {
    // State — bisa disimpan di abstract class
    var mileage: Double = 0.0
    protected var isEngineRunning: Boolean = false

    // Properti abstrak — HARUS di-override oleh subclass
    abstract val maxSpeed: Int

    // Metode konkret — bisa digunakan langsung oleh subclass
    fun displayInfo() {
        println("=" .repeat(40))
        println("🚗 VEHICLE INFO")
        println("=" .repeat(40))
        println("Brand : $brand")
        println("Model : $model")
        println("Year  : $year")
        println("Max Speed : $maxSpeed km/h")
        println("Mileage   : $mileage km")
        println("Engine    : ${if (isEngineRunning) "🟢 Running" else "🔴 Stopped"}")
        println("=" .repeat(40))
    }

    // Metode konkret dengan implementasi
    fun startEngine() {
        isEngineRunning = true
        println("✅ $brand $model engine started")
    }

    fun stopEngine() {
        isEngineRunning = false
        println("✅ $brand $model engine stopped")
    }

    // Metode abstrak — HARUS di-override
    abstract fun drive(distance: Double)
    abstract fun calculateFuelEfficiency(): Double
}

/**
 * Subclass Car — mewarisi Vehicle
 */
class Car(
    brand: String,
    model: String,
    year: Int,
    override val maxSpeed: Int,
    val numberOfDoors: Int,
    val fuelType: String
) : Vehicle(brand, model, year) {

    private var fuelConsumed: Double = 0.0

    override fun drive(distance: Double) {
        if (!isEngineRunning) {
            println("❌ Cannot drive: engine is not running")
            return
        }
        mileage += distance
        fuelConsumed += distance / 10.0  // Asumsi: 1 liter untuk 10 km
        println("🚗 $brand $model drove $distance km")
    }

    override fun calculateFuelEfficiency(): Double {
        return if (mileage > 0) mileage / fuelConsumed else 0.0
    }

    // Metode tambahan khusus Car
    fun honk() {
        println("📢 $brand $model: Beep! Beep!")
    }
}

/**
 * Subclass Motorcycle — mewarisi Vehicle
 */
class Motorcycle(
    brand: String,
    model: String,
    year: Int,
    override val maxSpeed: Int,
    val engineCapacity: Int  // dalam cc
) : Vehicle(brand, model, year) {

    private var fuelConsumed: Double = 0.0

    override fun drive(distance: Double) {
        if (!isEngineRunning) {
            println("❌ Cannot drive: engine is not running")
            return
        }
        mileage += distance
        fuelConsumed += distance / 25.0  // Motor lebih irit: 1 liter untuk 25 km
        println("🏍️ $brand $model rode $distance km")
    }

    override fun calculateFuelEfficiency(): Double {
        return if (mileage > 0) mileage / fuelConsumed else 0.0
    }

    // Metode tambahan khusus Motorcycle
    fun wheelie() {
        println("🏍️ $brand $model doing a wheelie! 🤸")
    }
}

fun main() {
    val car = Car("Toyota", "Avanza", 2023, 180, 4, "Bensin")
    val motor = Motorcycle("Honda", "Beat", 2024, 110, 110)

    car.startEngine()
    car.drive(50.0)
    car.drive(30.0)
    car.stopEngine()
    car.displayInfo()

    println()

    motor.startEngine()
    motor.drive(20.0)
    motor.drive(15.0)
    motor.wheelie()
    motor.displayInfo()
}
```

---

## 2.5 Kapan Menggunakan Abstract Class?

| **Skenario** | **Penjelasan** |
|---|---|
| **Memiliki state yang harus dibagi** | Abstract class bisa menyimpan state (`var`/`val`) yang diwarisi oleh subclass |
| **Memiliki constructor** | Abstract class bisa memiliki constructor untuk inisialisasi |
| **Memiliki metode konkret yang reusable** | Abstract class bisa menyediakan implementasi default untuk beberapa metode |
| **Membutuhkan protected members** | Abstract class bisa memiliki member `protected` yang hanya bisa diakses oleh subclass |
| **Hubungan "IS-A" yang kuat** | Ketika subclass benar-benar adalah tipe dari superclass |

---

# BAGIAN 3: INTERFACE DI KOTLIN

## 3.1 Apa itu Interface?

**Interface** adalah **kontrak** atau **perjanjian** yang mendefinisikan **apa yang harus dilakukan** oleh sebuah kelas, tanpa mendefinisikan **bagaimana** melakukannya. Interface berfungsi sebagai **"daftar janji"** — sebuah kelas yang mengimplementasikan interface berjanji untuk menyediakan implementasi untuk semua metode yang dideklarasikan di interface.

---

## 3.2 Karakteristik Interface

| **Karakteristik** | **Penjelasan** | **Contoh** |
|---|---|---|
| **Tidak bisa di-instansiasi** | Tidak bisa membuat objek langsung dari interface | `val device = InputDevice()` → ❌ ERROR |
| **Tidak memiliki constructor** | Interface tidak bisa memiliki constructor | `interface InputDevice { ... }` |
| **Tidak bisa menyimpan state** | Interface tidak bisa memiliki backing field | Tidak bisa `var x: Int = 0` di interface |
| **Dapat memiliki properti** | Tapi harus abstrak atau memiliki accessor | `val version: String` atau `val name: String get() = "..."` |
| **Dapat memiliki metode abstrak** | Metode tanpa implementasi | `fun input(event: Any)` |
| **Dapat memiliki default method** | Metode dengan implementasi (sejak Kotlin 1.2/1.4) | `fun foo() { println("default") }` |
| **Multiple inheritance** | Sebuah kelas bisa mengimplementasikan banyak interface | `class C : A, B` |

---

## 3.3 Sintaks Interface

```kotlin
// Mendefinisikan interface
interface InputDevice {
    // ✅ Properti abstrak — HARUS di-override oleh implementor
    val version: String

    // ✅ Properti dengan accessor — tidak memiliki backing field
    val name: String
        get() = "Input Device v$version"

    // ✅ Metode abstrak — tidak memiliki implementasi
    fun input(event: Any)

    // ✅ Default method — memiliki implementasi (sejak Kotlin 1.2)
    fun onLowPower() {
        println("⚠️ Warning: Device is running low on power")
    }

    // ✅ Default method dengan logika lebih kompleks
    fun getStatus(): String {
        return "Device: $name, Version: $version"
    }
}

// Mengimplementasikan interface
class Keyboard(override val version: String) : InputDevice {
    override fun input(event: Any) {
        println("⌨️ Keyboard input: $event")
    }

    // Optional: override default method
    override fun onLowPower() {
        println("⌨️ Keyboard battery is low! Please replace batteries.")
    }
}

class Mouse(override val version: String) : InputDevice {
    override fun input(event: Any) {
        println("🖱️ Mouse input: $event")
    }
    // onLowPower() menggunakan implementasi default dari interface
}

fun main() {
    val keyboard = Keyboard("1.0")
    val mouse = Mouse("2.0")

    keyboard.input("Hello")         // Output: ⌨️ Keyboard input: Hello
    keyboard.onLowPower()           // Output: ⌨️ Keyboard battery is low! Please replace batteries.
    println(keyboard.getStatus())   // Output: Device: Input Device v1.0, Version: 1.0

    mouse.input("Click")            // Output: 🖱️ Mouse input: Click
    mouse.onLowPower()              // Output: ⚠️ Warning: Device is running low on power
}
```

---

## 3.4 Properti di Interface

Properti di interface **tidak bisa memiliki backing field** — mereka harus abstrak atau memiliki accessor.

```kotlin
interface MyInterface {
    // ✅ Properti abstrak — HARUS di-override
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

    // ❌ ERROR: Backing field not allowed in interfaces
    // var count: Int = 0
}

class MyClass(override val id: String) : MyInterface {
    // counter harus di-override atau menggunakan implementasi default
    override var counter: Int = 0
}
```

### Contoh Properti dengan Default Accessor

```kotlin
interface Configurable {
    // Properti abstrak — HARUS di-override
    val configKey: String

    // Properti dengan default getter — tidak perlu di-override
    val configValue: String
        get() = System.getProperty(configKey) ?: "default"

    // Default method
    fun reload() {
        println("🔄 Reloading configuration for $configKey")
    }

    fun display() {
        println("📋 $configKey = $configValue")
    }
}

class AppConfig : Configurable {
    override val configKey: String = "app.mode"
    // configValue menggunakan default getter dari interface
}

class DatabaseConfig : Configurable {
    override val configKey: String = "db.url"

    // Override configValue dengan implementasi sendiri
    override val configValue: String
        get() = "jdbc:mysql://localhost:3306/mydb"
}

fun main() {
    val appConfig = AppConfig()
    appConfig.display()   // Output: 📋 app.mode = default
    appConfig.reload()    // Output: 🔄 Reloading configuration for app.mode

    val dbConfig = DatabaseConfig()
    dbConfig.display()    // Output: 📋 db.url = jdbc:mysql://localhost:3306/mydb
}
```

---

## 3.5 Kapan Menggunakan Interface?

| **Skenario** | **Penjelasan** |
|---|---|
| **Mendefinisikan perilaku** | Interface mendefinisikan "apa" yang bisa dilakukan, bukan "bagaimana" |
| **Multiple inheritance** | Ketika sebuah kelas perlu memiliki perilaku dari berbagai sumber |
| **Kontrak untuk API** | Interface mendefinisikan kontrak antara berbagai komponen |
| **Polimorfisme** | Interface memungkinkan polimorfisme tanpa inheritance |
| **Dependency Injection** | Interface memungkinkan decoupling antara komponen |

---

# BAGIAN 4: PERBANDINGAN ABSTRACT CLASS VS INTERFACE

## 4.1 Perbandingan Mendetail

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

---

## 4.2 Kapan Menggunakan Abstract Class vs Interface?

| **Situasi** | **Pilihan** | **Alasan** |
|---|---|---|
| **Perlu menyimpan state** | Abstract Class | Interface tidak bisa menyimpan state |
| **Perlu constructor untuk inisialisasi** | Abstract Class | Interface tidak memiliki constructor |
| **Perlu multiple behavior dari berbagai sumber** | Interface | Sebuah kelas bisa mengimplementasikan banyak interface |
| **Hubungan "IS-A" yang kuat** | Abstract Class | Contoh: `Dog IS-A Animal` |
| **Hubungan "CAN-DO" (perilaku)** | Interface | Contoh: `Dog CAN-DO Swimmable` |
| **Membutuhkan protected members** | Abstract Class | Interface tidak mendukung `protected` |
| **Membutuhkan final members** | Abstract Class | Interface tidak mendukung `final` |

---

## 4.3 Contoh Perbandingan Langsung

```kotlin
// ============================================================
// ABSTRACT CLASS — mendefinisikan "bagaimana" (How)
// ============================================================
abstract class Animal(val name: String) {
    // ✅ Bisa menyimpan state
    var age: Int = 0

    // ✅ Bisa memiliki constructor
    init {
        println("🐾 Animal $name created")
    }

    // ✅ Bisa memiliki metode konkret
    fun eat() {
        println("🍽️ $name is eating...")
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
        println("🏊 Swimming at $swimSpeed km/h")
    }
}

interface Flyable {
    val flySpeed: Double

    fun fly() {
        println("✈️ Flying at $flySpeed km/h")
    }
}

// ============================================================
// CLASS — mengimplementasikan kedua interface dan mewarisi abstract class
// ============================================================
class Duck(name: String) : Animal(name), Swimmable, Flyable {
    override val swimSpeed: Double = 5.0
    override val flySpeed: Double = 40.0

    override fun makeSound() {
        println("🦆 $name says: Quack! Quack!")
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
    duck.fly()          // Dari interface (default — tidak di-override)
}
```

---

# BAGIAN 5: MULTIPLE INTERFACE IMPLEMENTATION

## 5.1 Konsep Multiple Interface

Kotlin mendukung **multiple interface implementation** — sebuah kelas bisa mengimplementasikan **lebih dari satu interface**.

```kotlin
interface Printable {
    fun print() {
        println("🖨️ Printing...")
    }
}

interface Scannable {
    fun scan() {
        println("📄 Scanning...")
    }
}

interface Faxable {
    fun fax() {
        println("📠 Faxing...")
    }
}

// Sebuah kelas bisa mengimplementasikan banyak interface
class MultiFunctionPrinter : Printable, Scannable, Faxable {
    // Semua metode menggunakan implementasi default dari interface
    // Tapi kita bisa meng-override jika perlu
    override fun print() {
        println("🖨️ Multi-function printer is printing in color...")
    }
}

fun main() {
    val mfp = MultiFunctionPrinter()
    mfp.print()   // Output: 🖨️ Multi-function printer is printing in color...
    mfp.scan()    // Output: 📄 Scanning...
    mfp.fax()     // Output: 📠 Faxing...
}
```

---

## 5.2 Contoh: Perangkat dengan Multiple Capabilities

```kotlin
// ============================================================
// INTERFACE — Mendefinisikan berbagai capabilities
// ============================================================

interface Chargeable {
    val batteryLevel: Int
    val batteryCapacity: Int

    val batteryPercentage: Double
        get() = (batteryLevel.toDouble() / batteryCapacity) * 100

    fun charge(amount: Int) {
        println("🔋 Charging $amount%...")
    }

    fun getBatteryStatus(): String {
        return "Battery: $batteryLevel / $batteryCapacity mAh (${"%.1f".format(batteryPercentage)}%)"
    }
}

interface Connectable {
    val connectionType: String

    fun connect() {
        println("🔗 Connecting via $connectionType...")
    }

    fun disconnect() {
        println("🔗 Disconnecting from $connectionType...")
    }

    fun isConnected(): Boolean = false
}

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
// CLASS — Mengimplementasikan multiple interfaces
// ============================================================

class Smartphone(
    val brand: String,
    val model: String,
    override val batteryCapacity: Int,
    override val connectionType: String = "5G",
    override val resolution: String = "1080x2400"
) : Chargeable, Connectable, Displayable {

    override var batteryLevel: Int = 0
        private set

    private var connected: Boolean = false

    override fun charge(amount: Int) {
        batteryLevel = minOf(batteryLevel + amount, batteryCapacity)
        println("🔋 Charging... Battery: $batteryLevel / $batteryCapacity mAh")
        if (batteryLevel >= batteryCapacity) {
            println("✅ Battery fully charged!")
        }
    }

    override fun connect() {
        connected = true
        println("📶 Connected to $connectionType network")
    }

    override fun disconnect() {
        connected = false
        println("📶 Disconnected from $connectionType network")
    }

    override fun isConnected(): Boolean = connected

    override fun display() {
        println("📱 Displaying on $resolution screen")
    }
}

class SmartWatch(
    val brand: String,
    val model: String,
    override val batteryCapacity: Int,
    override val connectionType: String = "Bluetooth"
) : Chargeable, Connectable {

    override var batteryLevel: Int = 0
        private set

    private var connected: Boolean = false

    override fun charge(amount: Int) {
        batteryLevel = minOf(batteryLevel + amount, batteryCapacity)
        println("⌚ Charging watch... Battery: $batteryLevel / $batteryCapacity mAh")
    }

    override fun connect() {
        connected = true
        println("⌚ Connected via $connectionType")
    }

    override fun disconnect() {
        connected = false
        println("⌚ Disconnected from $connectionType")
    }

    override fun isConnected(): Boolean = connected

    // Metode tambahan khusus SmartWatch
    fun trackHeartRate() {
        println("❤️ Heart rate: 72 BPM")
    }
}

fun main() {
    val phone = Smartphone("Samsung", "Galaxy S24", 5000)
    val watch = SmartWatch("Apple", "Watch Series 9", 300)

    // Smartphone — mengimplementasikan 3 interface
    phone.charge(30)
    phone.connect()
    phone.display()
    println(phone.getBatteryStatus())

    println()

    // SmartWatch — mengimplementasikan 2 interface
    watch.charge(50)
    watch.connect()
    watch.trackHeartRate()
    println(watch.getBatteryStatus())
}
```

---

# BAGIAN 6: RESOLVING OVERRIDING CONFLICTS

## 6.1 Masalah Konflik Overriding

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

---

## 6.2 Menyelesaikan Konflik dengan `super<Interface>`

Gunakan **`super<InterfaceName>`** untuk memanggil implementasi dari interface tertentu.

```kotlin
// ============================================================
// INTERFACE dengan konflik metode
// ============================================================

interface Printable {
    fun print() {
        println("🖨️ Printable: Printing document...")
    }
}

interface Loggable {
    fun print() {
        println("📝 Loggable: Logging activity...")
    }
}

// ============================================================
// SOLUSI 1: Override dengan implementasi sendiri
// ============================================================
class Document : Printable, Loggable {
    override fun print() {
        println("📄 Document: Printing document content...")
    }
}

// ============================================================
// SOLUSI 2: Memanggil salah satu implementasi interface
// ============================================================
class Report : Printable, Loggable {
    override fun print() {
        // Memanggil implementasi dari Printable saja
        super<Printable>.print()
    }
}

// ============================================================
// SOLUSI 3: Memanggil SEMUA implementasi
// ============================================================
class Invoice : Printable, Loggable {
    override fun print() {
        super<Printable>.print()
        super<Loggable>.print()
        println("🧾 Invoice: Printing invoice...")
    }
}

fun main() {
    Document().print()   // Output: 📄 Document: Printing document content...
    Report().print()     // Output: 🖨️ Printable: Printing document...
    Invoice().print()    // Output: 🖨️ Printable: Printing document... \n 📝 Loggable: Logging activity... \n 🧾 Invoice: Printing invoice...
}
```

---

## 6.3 Konflik dengan Properti

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
    // Harus meng-override properti name untuk menyelesaikan konflik
    override val name: String
        get() = "📚 Book: ${super<Named>.name} / ${super<Titled>.name}"
}

class Article : Named, Titled {
    // Alternatif: implementasi sendiri
    override val name: String
        get() = "📰 Article: Custom Title"
}

fun main() {
    val book = Book()
    println(book.name)  // Output: 📚 Book: Default Name / Default Title

    val article = Article()
    println(article.name)  // Output: 📰 Article: Custom Title
}
```

---

# BAGIAN 7: DEFAULT METHOD DI INTERFACE

## 7.1 Apa itu Default Method?

**Default method** adalah metode di interface yang **memiliki implementasi** (body). Sejak Kotlin 1.2/1.4, interface bisa memiliki default method.

```kotlin
interface Logger {
    // Default method — memiliki implementasi
    fun log(message: String) {
        println("[${this::class.simpleName}] $message")
    }

    // Default method dengan logika lebih kompleks
    fun logError(message: String) {
        log("❌ ERROR: $message")
    }

    fun logWarning(message: String) {
        log("⚠️ WARNING: $message")
    }

    fun logInfo(message: String) {
        log("ℹ️ INFO: $message")
    }
}

class ApplicationLogger : Logger {
    // Menggunakan semua default method dari Logger
    // Bisa meng-override jika perlu
    override fun log(message: String) {
        println("📝 ${System.currentTimeMillis()}: $message")
    }
}

class SimpleLogger : Logger {
    // Menggunakan implementasi default tanpa override
}

fun main() {
    val appLogger = ApplicationLogger()
    appLogger.log("Application started")        // Output: 📝 1234567890: Application started
    appLogger.logError("Connection failed")     // Output: 📝 1234567890: ❌ ERROR: Connection failed
    appLogger.logWarning("Low memory")          // Output: 📝 1234567890: ⚠️ WARNING: Low memory

    val simpleLogger = SimpleLogger()
    simpleLogger.logInfo("User logged in")      // Output: [SimpleLogger] ℹ️ INFO: User logged in
}
```

---

## 7.2 Manfaat Default Method

| **Manfaat** | **Penjelasan** |
|---|---|
| **Backward Compatibility** | Menambah metode baru ke interface tanpa merusak implementasi yang sudah ada |
| **Code Reusability** | Menyediakan implementasi default yang bisa digunakan oleh semua implementor |
| **Mengurangi Boilerplate** | Implementor tidak perlu meng-override semua metode |
| **Mendukung Evolution** | Interface bisa berevolusi seiring waktu |

---

## 7.3 Contoh: Interface dengan Default Method untuk Event Handling

```kotlin
interface EventListener {
    // Default method — semua method memiliki implementasi default
    fun onStart() {
        println("⏳ Event started")
    }

    fun onProgress(percentage: Int) {
        println("📊 Progress: $percentage%")
    }

    fun onComplete() {
        println("✅ Event completed")
    }

    fun onError(error: String) {
        println("❌ Error: $error")
    }
}

// Implementor hanya perlu meng-override method yang diperlukan
class DownloadListener : EventListener {
    override fun onStart() {
        println("📥 Download started...")
    }

    override fun onProgress(percentage: Int) {
        println("📥 Downloading... $percentage%")
    }

    override fun onComplete() {
        println("📥 Download complete! ✅")
    }
    // onError menggunakan implementasi default
}

class UploadListener : EventListener {
    override fun onStart() {
        println("📤 Upload started...")
    }

    override fun onComplete() {
        println("📤 Upload complete! ✅")
    }
    // onProgress dan onError menggunakan implementasi default
}

fun simulateTask(listener: EventListener) {
    listener.onStart()
    listener.onProgress(25)
    listener.onProgress(50)
    listener.onProgress(75)
    listener.onComplete()
}

fun main() {
    println("=== Download Task ===")
    simulateTask(DownloadListener())

    println("\n=== Upload Task ===")
    simulateTask(UploadListener())
}
```

---

# BAGIAN 8: SEALED CLASS — CLOSED POLYMORPHISM

## 8.1 Apa itu Sealed Class?

**Sealed class** adalah kelas yang **membatasi hierarki subclass** — semua subclass dari sealed class harus dideklarasikan **dalam file yang sama** dengan sealed class tersebut.

> **Closed Polymorphism:** Semua subclass dari sealed class **diketahui pada saat compile time**. Sealed class secara implisit adalah abstract class dan tidak bisa di-instansiasi langsung.

---

## 8.2 Sealed Class vs Abstract Class

| **Aspek** | **Sealed Class** | **Abstract Class** |
|---|---|---|
| **Subclass** | Terbatas — hanya di file yang sama | Tidak terbatas — bisa di mana saja |
| **Polymorphism** | Closed (tertutup) | Open (terbuka) |
| **`when` Expression** | Ekshaustif — compiler memastikan semua kasus ditangani | Tidak ekshaustif — perlu `else` |
| **Instansiasi** | ❌ Tidak bisa | ❌ Tidak bisa |
| **State** | ✅ Bisa | ✅ Bisa |
| **Secara implisit** | Abstract | Abstract |

---

## 8.3 Sintaks Sealed Class

```kotlin
// Sealed class — semua subclass HARUS di file yang sama
sealed class OperationResult {
    // Subclass sebagai data class — bisa memiliki state berbeda
    data class Success(val data: String, val code: Int) : OperationResult()
    data class Error(val message: String, val errorCode: Int) : OperationResult()
    object Loading : OperationResult()
    object Idle : OperationResult()
}

// Subclass tambahan bisa dideklarasikan di file yang sama
class CustomResult(val customData: String) : OperationResult()

// ❌ ERROR: Subclass di file berbeda TIDAK diizinkan
// class AnotherResult : OperationResult()  // Tidak bisa di file lain

// ============================================================
// Fungsi dengan when expression yang EKSHAUSTIF
// ============================================================
fun handleResult(result: OperationResult): String {
    // Compiler memastikan SEMUA kemungkinan ditangani
    return when (result) {
        is OperationResult.Success -> "✅ Success: ${result.data} (Code: ${result.code})"
        is OperationResult.Error -> "❌ Error: ${result.message} (Code: ${result.errorCode})"
        OperationResult.Loading -> "⏳ Loading..."
        OperationResult.Idle -> "💤 Idle"
        is CustomResult -> "🔧 Custom: ${result.customData}"
        // Tidak perlu else — semua kemungkinan sudah tercakup!
    }
}

fun main() {
    val results = listOf(
        OperationResult.Success("Data loaded", 200),
        OperationResult.Error("Connection failed", 500),
        OperationResult.Loading,
        OperationResult.Idle,
        CustomResult("Custom data here")
    )

    for (result in results) {
        println(handleResult(result))
    }
}
```

---

## 8.4 Sealed Interface (Kotlin 1.5+)

Kotlin 1.5+ mendukung **sealed interface**.

```kotlin
// Sealed interface — semua implementasi harus di file yang sama
sealed interface PaymentStatus {
    // Implementasi sebagai object — singleton
    object Success : PaymentStatus
    object Pending : PaymentStatus

    // Implementasi sebagai data class — bisa memiliki state
    data class Failed(val reason: String, val errorCode: Int) : PaymentStatus
}

// Sebuah class bisa mengimplementasikan multiple sealed interfaces
sealed interface Printable
sealed interface Drawable

class Document : Printable, Drawable  // Bisa mengimplementasikan keduanya

// ============================================================
// Fungsi dengan when expression yang EKSHAUSTIF
// ============================================================
fun handlePayment(status: PaymentStatus): String {
    return when (status) {
        PaymentStatus.Success -> "✅ Payment successful"
        PaymentStatus.Pending -> "⏳ Payment pending..."
        is PaymentStatus.Failed -> "❌ Payment failed: ${status.reason} (Code: ${status.errorCode})"
    }
}

fun main() {
    println(handlePayment(PaymentStatus.Success))
    println(handlePayment(PaymentStatus.Pending))
    println(handlePayment(PaymentStatus.Failed("Insufficient balance", 402)))
}
```

---

## 8.5 Sealed Class vs Enum Class

| **Aspek** | **Sealed Class** | **Enum Class** |
|---|---|---|
| **Subclass** | Bisa memiliki subclass yang berbeda | Semua instance adalah konstanta dari enum yang sama |
| **State** | Setiap subclass bisa memiliki state berbeda | Semua konstanta memiliki state yang sama |
| **Inheritance** | Subclass bisa mewarisi dari sealed class | Enum tidak bisa diwarisi |
| **Multiple Instances** | Setiap subclass bisa punya banyak instance | Setiap konstanta hanya satu instance |
| **Kapan Gunakan** | Representasi state yang kompleks | Representasi konstanta sederhana |

```kotlin
// ============================================================
// ENUM — untuk konstanta sederhana
// ============================================================
enum class SimpleStatus {
    SUCCESS, ERROR, LOADING
}

// ============================================================
// SEALED CLASS — untuk state dengan data berbeda
// ============================================================
sealed class DetailedStatus {
    data class Success(val data: String, val code: Int) : DetailedStatus()
    data class Error(val message: String, val errorCode: Int) : DetailedStatus()
    object Loading : DetailedStatus()
}

fun handleSimple(status: SimpleStatus): String {
    return when (status) {
        SimpleStatus.SUCCESS -> "✅ Berhasil"
        SimpleStatus.ERROR -> "❌ Gagal"
        SimpleStatus.LOADING -> "⏳ Loading"
    }
}

fun handleDetailed(status: DetailedStatus): String {
    return when (status) {
        is DetailedStatus.Success -> "✅ Berhasil: ${status.data} (Kode: ${status.code})"
        is DetailedStatus.Error -> "❌ Gagal: ${status.message} (Kode: ${status.errorCode})"
        DetailedStatus.Loading -> "⏳ Loading..."
    }
}

fun main() {
    println("=== ENUM CLASS ===")
    println(handleSimple(SimpleStatus.SUCCESS))
    println(handleSimple(SimpleStatus.ERROR))

    println("\n=== SEALED CLASS ===")
    println(handleDetailed(DetailedStatus.Success("Data berhasil", 200)))
    println(handleDetailed(DetailedStatus.Error("Terjadi kesalahan", 500)))
    println(handleDetailed(DetailedStatus.Loading))
}
```

---

# BAGIAN 9: STUDI KASUS — SISTEM PERANGKAT ELEKTRONIK

## 9.1 Analisis Kebutuhan

Mari kita bangun sistem perangkat elektronik yang mengimplementasikan semua konsep abstraksi.

| **Perangkat** | **Interface** | **Abstract Class** |
|---|---|---|
| **ElectronicDevice** | - | Abstract class dengan properti dasar |
| **Chargeable** | Interface untuk perangkat yang bisa di-charge | - |
| **Connectable** | Interface untuk perangkat yang bisa terhubung | - |
| **Displayable** | Interface untuk perangkat yang bisa menampilkan | - |
| **Smartphone** | Mewarisi ElectronicDevice, mengimplementasikan Chargeable, Connectable, Displayable | - |
| **Laptop** | Mewarisi ElectronicDevice, mengimplementasikan Chargeable, Connectable, Displayable | - |
| **SmartTV** | Mewarisi ElectronicDevice, mengimplementasikan Connectable, Displayable | - |

---

## 9.2 Implementasi Lengkap

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

    // Metode abstrak — HARUS di-override
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
// INTERFACE: Displayable
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

    override fun isConnected(): Boolean = connected

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

    override fun isConnected(): Boolean = connected

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

    override fun isConnected(): Boolean = connected

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

# BAGIAN 10: RINGKASAN MATERI PERTEMUAN 5

## 10.1 Poin-Poin Penting

| **Konsep** | **Penjelasan** | **Keyword/Sintaks** |
|---|---|---|
| **Abstraksi** | Menyembunyikan kompleksitas, menampilkan esensi | - |
| **Abstract Class** | "Setengah jadi" — bisa memiliki state, constructor, metode konkret & abstrak | `abstract class` |
| **Interface** | Kontrak perilaku — tidak bisa menyimpan state, bisa memiliki default method | `interface` |
| **Default Method** | Metode dengan implementasi di interface | `fun method() { ... }` |
| **Multiple Interface** | Sebuah kelas bisa mengimplementasikan banyak interface | `class C : A, B` |
| **Konflik Overriding** | Dua interface dengan metode signature yang sama | `super<Interface>.method()` |
| **Sealed Class** | Hierarki tertutup — semua subclass diketahui di compile time | `sealed class` |
| **Sealed Interface** | Sealed interface (Kotlin 1.5+) | `sealed interface` |

---

## 10.2 Kapan Menggunakan Apa?

| **Skenario** | **Solusi** | **Contoh** |
|---|---|---|
| Perlu menyimpan state dan constructor | Abstract Class | `abstract class Animal(val name: String)` |
| Mendefinisikan perilaku tanpa state | Interface | `interface Swimmable` |
| Perlu multiple behavior dari berbagai sumber | Multiple Interface | `class Duck : Swimmable, Flyable` |
| Dua interface dengan metode yang sama | `super<Interface>` | `super<A>.foo()` |
| Hierarki dengan subclass terbatas | Sealed Class | `sealed class Result` |
| `when` expression yang ekshaustif | Sealed Class + `when` | `when (result) { ... }` |

---

# BAGIAN 11: LATIHAN DAN TUGAS

## 11.1 Latihan Mandiri

### Latihan 1: Abstract Class `Shape`

Buatlah abstract class `Shape` dengan:
- Properti: `name: String`
- Metode abstrak: `area(): Double`
- Metode konkret: `display()` yang menampilkan nama dan luas

Buat subclass: `Circle`, `Rectangle`, `Triangle` yang mengimplementasikan `area()`

### Latihan 2: Interface `Drawable` dan `Resizable`

Buatlah dua interface:
- `Drawable` dengan metode `draw()` (default: print "Drawing...")
- `Resizable` dengan metode `resize(factor: Double)` (default: print "Resizing...")

Buat kelas `Shape` yang mengimplementasikan kedua interface.

### Latihan 3: Sealed Class `NetworkState`

Buatlah sealed class `NetworkState` dengan:
- `Success(data: String)`
- `Error(message: String)`
- `Loading`

Buat fungsi `handleState(state: NetworkState): String` dengan `when` expression ekshaustif.

---

## 11.2 Tugas 5 (Dikumpulkan)

### Sistem Manajemen Transportasi dengan Abstraksi

Buatlah program lengkap sistem manajemen transportasi yang mengimplementasikan abstraksi dengan ketentuan berikut:

#### 1. Abstract Class `Transportation`

| **Komponen** | **Spesifikasi** |
|---|---|
| **Properti** | `id: String` (read-only)<br>`name: String` (read-only)<br>`capacity: Int` (read-only)<br>`isOperational: Boolean` (bisa diubah) |
| **Metode** | `calculateFuelEfficiency(): Double` (abstract)<br>`calculateMaintenanceCost(): Double` (abstract)<br>`startOperation(): Boolean`<br>`stopOperation(): Boolean`<br>`displayInfo(): String` |

#### 2. Interface `ElectricPowered`

| **Komponen** | **Spesifikasi** |
|---|---|
| **Properti** | `batteryCapacity: Int` (kWh)<br>`currentCharge: Int` (%) |
| **Metode** | `charge(amount: Int): Boolean`<br>`getRange(): Double` |

#### 3. Interface `FuelPowered`

| **Komponen** | **Spesifikasi** |
|---|---|
| **Properti** | `fuelType: String`<br>`fuelCapacity: Int` (liter)<br>`currentFuel: Int` (liter) |
| **Metode** | `refuel(amount: Int): Boolean`<br>`getRange(): Double` |

#### 4. Subclass `ElectricCar`, `GasolineCar`, `ElectricBus`

Implementasikan sesuai dengan interface yang sesuai.

#### 5. Sealed Class `TripStatus`

- `Scheduled` — perjalanan terjadwal
- `InProgress` — perjalanan sedang berlangsung
- `Completed` — perjalanan selesai
- `Cancelled` — perjalanan dibatalkan

#### 6. Kelas `TransportationCompany`

| **Komponen** | **Spesifikasi** |
|---|---|
| **Properti** | `name: String`<br>`vehicles: MutableList<Transportation>` (private) |
| **Metode** | `addVehicle(vehicle: Transportation)`<br>`findVehicle(id: String): Transportation?`<br>`getTotalMaintenanceCost(): Double`<br>`displayAllVehicles()`<br>`displayOperationalVehicles()` |

#### 7. Kriteria Penilaian Tugas 5

| **Kriteria** | **Bobot** | **Indikator** |
|---|---|---|
| **Abstract Class** | 25% | `Transportation` sebagai abstract class dengan metode abstrak & konkret |
| **Interface** | 20% | `ElectricPowered` dan `FuelPowered` dengan default method |
| **Multiple Interface** | 15% | Subclass mengimplementasikan interface yang sesuai |
| **Sealed Class** | 15% | `TripStatus` dengan `when` ekshaustif |
| **Fungsi main()** | 15% | Menampilkan semua skenario |
| **Kode Berkualitas** | 10% | Kode bersih, terstruktur, diberi komentar |

---

# BAGIAN 12: REFERENSI

## 12.1 Referensi Utama

1. **Kotlin Official Documentation – Interfaces** — [https://kotlinlang.org/docs/interfaces.html](https://kotlinlang.org/docs/interfaces.html)

2. **Kotlin Official Documentation – Sealed Classes and Interfaces** — [https://kotlinlang.org/docs/sealed-classes.html](https://kotlinlang.org/docs/sealed-classes.html)

3. **Kotlin Official Documentation – Inheritance** — [https://kotlinlang.org/docs/inheritance.html](https://kotlinlang.org/docs/inheritance.html)

## 12.2 Referensi Pendukung

4. **Kotlin的接口与抽象类有何区别** — [https://m.yisu.com/zixun/994021.html](https://m.yisu.com/zixun/994021.html)

5. **Kotlin Sealed 关键字** — [https://zetcode.cn/kotlin/sealed/](https://zetcode.cn/kotlin/sealed/)

6. **Kotlin10 - 面向对象之抽象类与接口** — [https://developer.aliyun.com/article/1628049](https://developer.aliyun.com/article/1628049)

---

# BAGIAN 13: PENUTUP

## 13.1 Pesan untuk Mahasiswa

> **“Abstraksi adalah seni menyembunyikan kompleksitas. Interface adalah janji, Abstract Class adalah cetakan, dan Sealed Class adalah batas yang aman.”**

Pertemuan 5 ini adalah **puncak** dari pemahaman OOP setelah mempelajari enkapsulasi (pertemuan 2), pewarisan (pertemuan 3), dan polimorfisme (pertemuan 4). Dengan memahami abstraksi, Anda bisa:

- **Menyembunyikan kompleksitas** — pengguna hanya melihat apa yang perlu
- **Mendefinisikan kontrak yang jelas** — interface sebagai janji perilaku
- **Membangun hierarki yang terkontrol** — sealed class untuk keamanan
- **Menulis kode yang lebih modular** — setiap komponen memiliki tanggung jawab jelas

**Ingatlah:**
1. **Abstract Class** = "bagaimana" (How) — dengan state dan constructor
2. **Interface** = "apa" (What) — tanpa state, dengan default method
3. **Sealed Class** = hierarki tertutup — semua subclass diketahui
4. **Default method** = evolusi interface tanpa merusak implementasi
5. **`super<Interface>`** = menyelesaikan konflik overriding

---

**Disusun oleh,**
[Nama Dosen Pengampu]
Dosen Program Studi D4 Teknologi Rekayasa Informatika Industri
