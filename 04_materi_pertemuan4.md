# MATERI AJAR PERTEMUAN 4
## PEMROGRAMAN BERORIENTASI OBJEK (OOP) DENGAN KOTLIN
### “Polimorfisme — Satu Antarmuka, Banyak Bentuk”

---

# BAGIAN 1: KONSEP DASAR POLIMORFISME

## 1.1 Apa itu Polimorfisme?

**Polimorfisme (Polymorphism)** adalah salah satu dari **empat pilar utama** dalam Pemrograman Berorientasi Objek (OOP), bersama dengan Encapsulation (Enkapsulasi), Inheritance (Pewarisan), dan Abstraction (Abstraksi).

Secara etimologi, kata "polimorfisme" berasal dari bahasa Yunani: ***poly*** (banyak) dan ***morph*** (bentuk). Jadi, polimorfisme berarti **"banyak bentuk"** .

> **Definisi Sederhana:** Polimorfisme adalah kemampuan sebuah objek atau metode untuk **berperilaku berbeda** tergantung pada konteksnya. Satu antarmuka (interface) yang sama dapat memiliki banyak implementasi yang berbeda.

Dalam konteks pemrograman, polimorfisme memungkinkan:
- Objek dari kelas yang berbeda untuk **merespons pesan yang sama dengan cara yang berbeda**
- Sebuah variabel bertipe superclass untuk **menampung objek dari subclass**
- Sebuah metode untuk **berperilaku berbeda** berdasarkan parameter yang diberikan

---

## 1.2 Analogi Polimorfisme dalam Kehidupan Nyata

Untuk memahami polimorfisme, mari kita lihat beberapa analogi dari kehidupan sehari-hari:

### A. Tombol "Mulai" di Berbagai Perangkat

| **Perangkat** | **Tombol yang Sama** | **Efek yang Berbeda** |
|---|---|---|
| **Televisi** | Tombol "Mulai" | Menyalakan gambar dan suara |
| **AC (Air Conditioner)** | Tombol "Mulai" | Menyalakan pendingin ruangan |
| **Mobil** | Tombol "Start" | Menyalakan mesin |
| **Komputer** | Tombol "Power" | Menyalakan sistem operasi |

**Pesan:** Tombol yang sama (interface) memberikan perintah yang sama, tetapi setiap perangkat merespons dengan cara yang berbeda sesuai dengan fungsinya masing-masing.

### B. Perintah "Bunyikan Suara" untuk Hewan

| **Hewan** | **Perintah yang Sama** | **Suara yang Berbeda** |
|---|---|---|
| **Anjing** | "Bunyikan suara!" | Guk! Guk! |
| **Kucing** | "Bunyikan suara!" | Meong! Meong! |
| **Sapi** | "Bunyikan suara!" | Moo! Moo! |
| **Burung** | "Bunyikan suara!" | Cuit! Cuit! |

**Pesan:** Perintah yang sama menghasilkan perilaku yang berbeda tergantung pada objek yang menerima perintah.

### C. Metode Pembayaran

| **Metode Pembayaran** | **Perintah yang Sama** | **Proses yang Berbeda** |
|---|---|---|
| **Kartu Kredit** | `bayar(100000)` | Memotong limit kartu kredit |
| **QRIS** | `bayar(100000)` | Memotong saldo e-wallet |
| **Transfer Bank** | `bayar(100000)` | Memindahkan dana antar rekening |
| **Cash** | `bayar(100000)` | Mengurangi uang tunai |

**Pesan:** Metode `bayar()` yang sama diimplementasikan secara berbeda oleh setiap metode pembayaran.

---

## 1.3 Mengapa Polimorfisme Sangat Penting?

Polimorfisme memberikan banyak manfaat dalam pengembangan perangkat lunak:

| **Manfaat** | **Penjelasan** | **Contoh** |
|---|---|---|
| **Fleksibilitas Kode** | Kode dapat bekerja dengan objek dari berbagai tipe tanpa perlu mengetahui detail spesifiknya | Satu fungsi `processPayment()` bisa menangani semua metode pembayaran |
| **Extensibility** | Kita dapat menambahkan kelas baru tanpa mengubah kode yang sudah ada | Menambah metode `CryptoPayment` tanpa mengubah kode yang sudah ada |
| **Code Reusability** | Satu fungsi dapat menangani berbagai tipe objek | Satu fungsi `printArea()` untuk semua bentuk geometris |
| **Abstraksi** | Pengguna kode hanya perlu tahu interface-nya, bukan implementasinya | Pengguna hanya perlu tahu `Shape.area()`, bukan cara menghitungnya |
| **Mendukung Prinsip Open/Closed** | Kode terbuka untuk ekstensi (kelas baru) tetapi tertutup untuk modifikasi | Menambah `Triangle` tanpa mengubah kode yang memproses `Shape` |
| **Maintainability** | Kode lebih mudah dipelihara karena lebih modular | Perubahan di satu subclass tidak mempengaruhi yang lain |

---

## 1.4 Dua Jenis Polimorfisme di Kotlin

Polimorfisme di Kotlin (dan OOP secara umum) terbagi menjadi **dua jenis utama**:

| **Jenis** | **Nama Lain** | **Waktu Binding** | **Contoh** |
|---|---|---|---|
| **Runtime Polymorphism** | Dynamic Polymorphism | Saat runtime (dinamis) | Method Overriding |
| **Compile-time Polymorphism** | Static Polymorphism | Saat compile-time (statis) | Method Overloading |

### 1.4.1 Runtime Polymorphism (Method Overriding)

**Method Overriding** terjadi ketika sebuah subclass menyediakan **implementasi spesifik** untuk metode yang sudah didefinisikan di superclass.

```kotlin
open class Animal {
    open fun makeSound() {
        println("Animal makes a sound")
    }
}

class Dog : Animal() {
    override fun makeSound() {
        println("Dog barks: Guk! Guk!")
    }
}

class Cat : Animal() {
    override fun makeSound() {
        println("Cat meows: Meong! Meong!")
    }
}
```

**Karakteristik Runtime Polymorphism:**
- Terjadi saat **runtime** (saat program berjalan)
- Memerlukan **inheritance** (pewarisan)
- Metode di superclass harus `open`, metode di subclass harus `override`
- Metode yang dipanggil ditentukan oleh **tipe objek sebenarnya**, bukan tipe variabel

### 1.4.2 Compile-time Polymorphism (Method Overloading)

**Method Overloading** terjadi ketika sebuah kelas memiliki **beberapa metode dengan nama yang sama** tetapi **parameter yang berbeda** (jumlah, tipe, atau urutan parameter berbeda).

```kotlin
class Calculator {
    // Overloading: 3 metode dengan nama yang sama tapi parameter berbeda
    fun add(a: Int, b: Int): Int {
        return a + b
    }

    fun add(a: Double, b: Double): Double {
        return a + b
    }

    fun add(a: Int, b: Int, c: Int): Int {
        return a + b + c
    }
}
```

**Karakteristik Compile-time Polymorphism:**
- Terjadi saat **compile-time** (saat kode dikompilasi)
- **Tidak** memerlukan inheritance
- Kompiler memilih metode yang tepat berdasarkan **argumen yang diberikan**
- Juga dikenal sebagai **static polymorphism** atau **ad-hoc polymorphism**

### 1.4.3 Perbandingan Overriding vs Overloading

| **Aspek** | **Overriding** | **Overloading** |
|---|---|---|
| **Hubungan** | Antar kelas (superclass → subclass) | Dalam satu kelas |
| **Keyword** | `override` | Tidak ada keyword khusus |
| **Parameter** | Harus **sama persis** dengan superclass | Harus **berbeda** (jumlah/tipe/urutan) |
| **Return Type** | Harus **sama** atau **subtype** (covariant) | Bisa berbeda |
| **Waktu Binding** | Runtime (dinamis) | Compile-time (statis) |
| **Kebutuhan Inheritance** | ✅ Ya | ❌ Tidak |
| **Metode di Superclass** | Harus `open` | Tidak relevan |

---

# BAGIAN 2: POLYMORPHIC REFERENCES (REFERENSI POLIMORFIK)

## 2.1 Konsep Polymorphic References

**Polymorphic references** adalah kemampuan untuk **menyimpan objek dari subclass ke dalam variabel bertipe superclass**. Ini adalah implementasi paling dasar dari polimorfisme.

```kotlin
// Superclass
open class Animal {
    open fun makeSound() {
        println("Animal makes a sound")
    }
}

// Subclasses
class Dog : Animal() {
    override fun makeSound() {
        println("Dog barks: Guk! Guk!")
    }
}

class Cat : Animal() {
    override fun makeSound() {
        println("Cat meows: Meong! Meong!")
    }
}

fun main() {
    // POLYMORPHIC REFERENCES
    // Variabel bertipe Animal bisa menampung objek Dog atau Cat
    val animal1: Animal = Dog()   // Dog disimpan dalam variabel Animal
    val animal2: Animal = Cat()   // Cat disimpan dalam variabel Animal

    // Meskipun variabel bertipe Animal, metode yang dipanggil adalah dari subclass
    animal1.makeSound()  // Output: Dog barks: Guk! Guk!
    animal2.makeSound()  // Output: Cat meows: Meong! Meong!
}
```

## 2.2 Mengapa Polymorphic References Penting?

Polymorphic references memungkinkan kita menulis kode yang **lebih umum dan fleksibel**:

```kotlin
// Tanpa polymorphic references — kode menjadi kaku
fun processDog(dog: Dog) {
    dog.makeSound()
}
fun processCat(cat: Cat) {
    cat.makeSound()
}

// Dengan polymorphic references — satu fungsi untuk semua Animal
fun processAnimal(animal: Animal) {
    animal.makeSound()  // Bisa menerima Animal, Dog, Cat, atau subclass lainnya
}

fun main() {
    val animals: List<Animal> = listOf(Dog(), Cat(), Dog())
    for (animal in animals) {
        processAnimal(animal)  // Satu fungsi menangani semua jenis Animal
    }
}
```

## 2.3 Contoh Lengkap: Polymorphic Array/List

```kotlin
open class Shape {
    open fun area(): Double = 0.0
    open fun name(): String = "Shape"
}

class Circle(val radius: Double) : Shape() {
    override fun area(): Double = Math.PI * radius * radius
    override fun name(): String = "Circle"
}

class Rectangle(val width: Double, val height: Double) : Shape() {
    override fun area(): Double = width * height
    override fun name(): String = "Rectangle"
}

class Triangle(val base: Double, val height: Double) : Shape() {
    override fun area(): Double = 0.5 * base * height
    override fun name(): String = "Triangle"
}

fun main() {
    // Polymorphic list — List berisi berbagai subclass Shape
    val shapes: List<Shape> = listOf(
        Circle(5.0),
        Rectangle(4.0, 6.0),
        Triangle(3.0, 4.0),
        Circle(3.0)
    )

    // Satu loop menangani semua jenis Shape
    for (shape in shapes) {
        println("${shape.name()} area: ${shape.area()}")
    }
    // Output:
    // Circle area: 78.53981633974483
    // Rectangle area: 24.0
    // Triangle area: 6.0
    // Circle area: 28.274333882308138
}
```

---

# BAGIAN 3: TYPE CHECKS DAN CASTING

## 3.1 Operator `is` dan `!is` untuk Type Checking

Gunakan operator **`is`** (dan **`!is`** untuk negasi) untuk memeriksa apakah sebuah objek memiliki tipe tertentu.

```kotlin
open class Animal
class Dog : Animal() {
    fun bark() = println("Guk! Guk!")
}
class Cat : Animal() {
    fun meow() = println("Meong! Meong!")
}

fun main() {
    val animal: Animal = Dog()

    // is — memeriksa apakah objek memiliki tipe tertentu
    println(animal is Dog)   // Output: true
    println(animal is Cat)   // Output: false
    println(animal is Animal) // Output: true

    // !is — memeriksa apakah objek TIDAK memiliki tipe tertentu
    println(animal !is Cat)  // Output: true
}
```

### Penggunaan `is` dengan `when`

```kotlin
fun handleAnimal(animal: Animal) {
    when {
        animal is Dog -> {
            println("Ini adalah Dog")
            animal.bark()  // Smart cast — otomatis ke Dog
        }
        animal is Cat -> {
            println("Ini adalah Cat")
            animal.meow()  // Smart cast — otomatis ke Cat
        }
        else -> {
            println("Animal tidak dikenal")
        }
    }
}

fun main() {
    handleAnimal(Dog())   // Output: Ini adalah Dog \n Guk! Guk!
    handleAnimal(Cat())   // Output: Ini adalah Cat \n Meong! Meong!
}
```

## 3.2 Smart Casting — Fitur Andalan Kotlin

**Smart casting** adalah fitur Kotlin di mana kompiler **secara otomatis melakukan casting** setelah pemeriksaan tipe dengan `is` atau `!is`.

```kotlin
fun demoSmartCasting(obj: Any) {
    // Sebelum pemeriksaan, obj bertipe Any
    // obj.length  // ❌ ERROR: Any tidak punya property length

    if (obj is String) {
        // Setelah pemeriksaan, obj secara otomatis di-cast ke String
        println(obj.length)  // ✅ OK — smart cast ke String
        println(obj.uppercase())
    }

    if (obj !is Int) {
        // Jika obj BUKAN Int, kita tidak bisa menggunakan operasi Int
        return
    }
    // Setelah return, kompiler tahu bahwa obj PASTI Int
    println(obj + 10)  // ✅ OK — smart cast ke Int
}
```

**Smart casting bekerja di berbagai struktur kontrol:**

```kotlin
// 1. if expression
fun process(value: Any) {
    if (value is String) {
        println(value.length)  // Smart cast ke String
    }
}

// 2. when expression
fun describe(value: Any): String {
    return when (value) {
        is String -> "String dengan panjang ${value.length}"  // Smart cast
        is Int -> "Integer: ${value + 10}"  // Smart cast
        is Boolean -> "Boolean: ${if (value) "true" else "false"}"  // Smart cast
        else -> "Tipe tidak dikenal"
    }
}

// 3. while loop — smart cast setelah kondisi terpenuhi
fun processWhile(value: Any) {
    while (value is String) {
        println(value.length)  // Smart cast ke String
        // ...
    }
}

// 4. Boolean variable — smart cast dengan boolean condition
fun processWithBoolean(value: Any) {
    val isString = value is String
    if (isString) {
        println(value.length)  // Smart cast ke String
    }
}
```

## 3.3 Upcasting — Casting ke Superclass

**Upcasting** adalah proses mengkonversi objek dari subclass ke superclass. Ini **selalu aman** karena setiap objek subclass adalah juga objek superclass.

```kotlin
open class Animal
class Dog : Animal()

fun main() {
    val dog = Dog()

    // Upcasting — otomatis dan aman
    val animal: Animal = dog  // Implicit upcasting

    // Explicit upcasting (tidak perlu, tapi bisa)
    val animal2 = dog as Animal
}
```

**Upcasting di Kotlin terjadi secara otomatis** — Anda tidak perlu melakukan casting secara eksplisit.

## 3.4 Downcasting — Casting ke Subclass

**Downcasting** adalah proses mengkonversi objek dari superclass ke subclass. Ini **tidak selalu aman** karena tidak semua objek superclass adalah subclass tertentu.

```kotlin
open class Animal
class Dog : Animal() {
    fun bark() = println("Guk! Guk!")
}
class Cat : Animal() {
    fun meow() = println("Meong! Meong!")
}

fun main() {
    val animal: Animal = Dog()  // Upcasting (otomatis)

    // ❌ Tanpa pengecekan — bisa crash!
    // val dog = animal as Dog  // Bisa berhasil, tapi berbahaya

    // ✅ Dengan pengecekan — aman
    if (animal is Dog) {
        val dog = animal  // Smart cast — otomatis ke Dog
        dog.bark()
    }
}
```

## 3.5 Operator Casting: `as` dan `as?`

Untuk casting eksplisit, Kotlin menyediakan dua operator:

| **Operator** | **Deskripsi** | **Perilaku jika gagal** |
|---|---|---|
| `as` | Unsafe cast | **Throw ClassCastException** (crash) |
| `as?` | Safe cast | **Return null** (tidak crash) |

```kotlin
fun main() {
    val obj: Any = "Hello"

    // === UNSAFE CAST (as) ===
    val str1: String = obj as String  // ✅ Berhasil
    // val num1: Int = obj as Int     // ❌ ClassCastException!

    // === SAFE CAST (as?) ===
    val str2: String? = obj as? String  // ✅ Berhasil: "Hello"
    val num2: Int? = obj as? Int        // ✅ Aman: null (tidak crash)

    println(str2)  // Output: Hello
    println(num2)  // Output: null

    // === as? dengan Elvis Operator ===
    val num3: Int = obj as? Int ?: 0  // Jika gagal, gunakan default 0
    println(num3)  // Output: 0
}
```

**Best Practice:** Gunakan `as?` daripada `as` kecuali Anda **100% yakin** casting akan berhasil.

---

# BAGIAN 4: SEALED CLASS — CLOSED POLYMORPHISM

## 4.1 Apa itu Sealed Class?

**Sealed class** adalah kelas yang **membatasi hierarki subclass** — semua subclass dari sealed class harus dideklarasikan **dalam file yang sama** dengan sealed class tersebut.

> **Closed Polymorphism:** Semua subclass dari sealed class **diketahui pada saat compile time**.

## 4.2 Mengapa Sealed Class?

| **Keuntungan Sealed Class** | **Penjelasan** |
|---|---|
| **Ekshaustif `when`** | Compiler memastikan semua kemungkinan ditangani di `when` expression |
| **Type Safety** | Tidak ada subclass yang tidak terduga |
| **Mewakili State Terbatas** | Cocok untuk mewakili state yang terbatas (Success, Loading, Error) |
| **Closed APIs** | Membuat API publik yang robust untuk library |
| **Controlled Inheritance** | Inheritance yang terkontrol dan terbatas |

## 4.3 Sintaks Sealed Class

```kotlin
// Sealed class — semua subclass harus di file yang sama
sealed class Result {
    data class Success(val data: String) : Result()
    data class Error(val message: String) : Result()
    object Loading : Result()
}

// Subclass bisa di file yang sama (di luar sealed class)
class CustomResult : Result()  // Juga boleh

// ❌ ERROR: Subclass di file berbeda tidak diizinkan
// class AnotherResult : Result()  // Tidak bisa di file lain
```

### Sealed Interface (Kotlin 1.5+)

Kotlin 1.5+ mendukung **sealed interface**:

```kotlin
sealed interface PaymentStatus {
    object Success : PaymentStatus
    data class Failed(val reason: String) : PaymentStatus
    object Pending : PaymentStatus
}

// Sebuah class bisa mengimplementasikan multiple sealed interfaces
sealed interface Printable
sealed interface Drawable

class Document : Printable, Drawable  // Bisa mengimplementasikan keduanya
```

## 4.4 Sealed Class vs Enum Class

| **Aspek** | **Sealed Class** | **Enum Class** |
|---|---|---|
| **Subclass** | Bisa memiliki subclass yang berbeda | Semua instance adalah konstanta dari enum yang sama |
| **State** | Setiap subclass bisa memiliki state berbeda | Semua konstanta memiliki state yang sama |
| **Inheritance** | Subclass bisa mewarisi dari sealed class | Enum tidak bisa diwarisi |
| **Multiple Instances** | Setiap subclass bisa punya banyak instance | Setiap konstanta hanya satu instance |
| **Kapan Gunakan** | Representasi state yang kompleks | Representasi konstanta sederhana |

```kotlin
// Enum — untuk konstanta sederhana
enum class Status {
    SUCCESS, ERROR, LOADING
}

// Sealed Class — untuk state dengan data berbeda
sealed class NetworkState {
    data class Success(val data: String) : NetworkState()
    data class Error(val error: String) : NetworkState()
    object Loading : NetworkState()
}
```

## 4.5 Sealed Class dengan `when` Ekshaustif

Keunggulan utama sealed class adalah **`when` expression yang ekshaustif** — compiler memastikan semua kemungkinan ditangani.

```kotlin
sealed class Result {
    data class Success(val data: String) : Result()
    data class Error(val message: String) : Result()
    object Loading : Result()
}

fun handleResult(result: Result): String {
    // Compiler memastikan semua kemungkinan ditangani
    return when (result) {
        is Result.Success -> "✅ Success: ${result.data}"
        is Result.Error -> "❌ Error: ${result.message}"
        Result.Loading -> "⏳ Loading..."
        // Tidak perlu else — semua kemungkinan sudah tercakup!
    }
}

fun main() {
    println(handleResult(Result.Success("Data berhasil")))
    println(handleResult(Result.Error("Terjadi kesalahan")))
    println(handleResult(Result.Loading))
}
```

---

# BAGIAN 5: STUDI KASUS — SISTEM PEMBAYARAN DENGAN POLIMORFISME

## 5.1 Analisis Kebutuhan

Kita akan membangun sistem pembayaran yang mengimplementasikan semua konsep polimorfisme.

| **Metode Pembayaran** | **Atribut** | **Perilaku** |
|---|---|---|
| **Payment (Base)** | amount: Double | processPayment(): PaymentStatus, getFee(): Double |
| **CreditCard** | cardNumber, expiryDate, cvv | Fee = 2% dari amount |
| **QRIS** | qrCode, merchantId | Fee = 0.5% dari amount |
| **BankTransfer** | bankName, accountNumber | Fee = 1% dari amount (minimal Rp 5.000) |
| **E-Wallet** | walletId, phoneNumber | Fee = 1.5% dari amount |

## 5.2 Implementasi Lengkap

```kotlin
/**
 * ============================================================
 * SISTEM PEMBAYARAN DENGAN POLIMORFISME
 * ============================================================
 * Demonstrasi:
 * 1. Polymorphic references
 * 2. Method overriding (runtime polymorphism)
 * 3. Smart casting dengan is
 * 4. Sealed class untuk status pembayaran
 * 5. as? untuk safe casting
 * ============================================================
 */

/**
 * SEALED CLASS: PaymentStatus
 * Mewakili status pembayaran dengan closed polymorphism
 */
sealed class PaymentStatus {
    data class Success(val transactionId: String, val timestamp: String) : PaymentStatus()
    data class Failed(val reason: String, val errorCode: Int) : PaymentStatus()
    object Pending : PaymentStatus()

    // Helper untuk menampilkan status
    fun display(): String {
        return when (this) {
            is Success -> "✅ Berhasil (ID: $transactionId, Waktu: $timestamp)"
            is Failed -> "❌ Gagal: $reason (Kode: $errorCode)"
            Pending -> "⏳ Menunggu pemrosesan..."
        }
    }
}

/**
 * KELAS INDUK: Payment
 * Semua metode pembayaran mewarisi dari kelas ini
 */
open class Payment(
    open val amount: Double,
    open val customerName: String
) {
    init {
        println("💳 Pembayaran sebesar Rp ${formatRupiah(amount)} atas nama $customerName")
    }

    // Metode open — bisa di-override oleh subclass
    open fun getFee(): Double {
        return 0.0  // Default: tidak ada biaya
    }

    // Metode open — bisa di-override oleh subclass
    open fun processPayment(): PaymentStatus {
        println("⚠️ Metode pembayaran tidak didukung")
        return PaymentStatus.Failed("Metode tidak didukung", 400)
    }

    // Metode final — tidak bisa di-override
    final fun getTotalAmount(): Double {
        return amount + getFee()
    }

    protected fun formatRupiah(nominal: Double): String {
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

/**
 * SUBCLASS 1: CreditCardPayment
 * Pembayaran dengan kartu kredit
 */
class CreditCardPayment(
    amount: Double,
    customerName: String,
    val cardNumber: String,
    val expiryDate: String,
    val cvv: String
) : Payment(amount, customerName) {

    override fun getFee(): Double {
        return amount * 0.02  // Biaya 2%
    }

    override fun processPayment(): PaymentStatus {
        if (cardNumber.length < 16) {
            return PaymentStatus.Failed("Nomor kartu tidak valid", 401)
        }
        if (cvv.length != 3) {
            return PaymentStatus.Failed("CVV tidak valid", 402)
        }

        println("💳 Memproses pembayaran kartu kredit...")
        println("   Nomor: ${maskCardNumber(cardNumber)}")
        println("   Total: Rp ${formatRupiah(getTotalAmount())} (termasuk biaya Rp ${formatRupiah(getFee())})")

        return PaymentStatus.Success(
            transactionId = "CC-${System.currentTimeMillis()}",
            timestamp = java.time.LocalDateTime.now().toString()
        )
    }

    private fun maskCardNumber(number: String): String {
        return "****-****-****-${number.takeLast(4)}"
    }
}

/**
 * SUBCLASS 2: QRISPayment
 * Pembayaran dengan QRIS
 */
class QRISPayment(
    amount: Double,
    customerName: String,
    val qrCode: String,
    val merchantId: String
) : Payment(amount, customerName) {

    override fun getFee(): Double {
        return amount * 0.005  // Biaya 0.5%
    }

    override fun processPayment(): PaymentStatus {
        if (qrCode.length < 10) {
            return PaymentStatus.Failed("Kode QR tidak valid", 403)
        }

        println("📱 Memproses pembayaran QRIS...")
        println("   Merchant: $merchantId")
        println("   Total: Rp ${formatRupiah(getTotalAmount())} (termasuk biaya Rp ${formatRupiah(getFee())})")

        return PaymentStatus.Success(
            transactionId = "QR-${System.currentTimeMillis()}",
            timestamp = java.time.LocalDateTime.now().toString()
        )
    }
}

/**
 * SUBCLASS 3: BankTransferPayment
 * Pembayaran transfer bank
 */
class BankTransferPayment(
    amount: Double,
    customerName: String,
    val bankName: String,
    val accountNumber: String
) : Payment(amount, customerName) {

    override fun getFee(): Double {
        val fee = amount * 0.01  // 1%
        return maxOf(fee, 5000.0)  // Minimal Rp 5.000
    }

    override fun processPayment(): PaymentStatus {
        if (accountNumber.length < 8) {
            return PaymentStatus.Failed("Nomor rekening tidak valid", 404)
        }

        println("🏦 Memproses transfer bank...")
        println("   Bank: $bankName")
        println("   Rekening: $accountNumber")
        println("   Total: Rp ${formatRupiah(getTotalAmount())} (termasuk biaya Rp ${formatRupiah(getFee())})")

        return PaymentStatus.Pending
    }
}

/**
 * SUBCLASS 4: EWalletPayment
 * Pembayaran dengan e-wallet
 */
class EWalletPayment(
    amount: Double,
    customerName: String,
    val walletId: String,
    val phoneNumber: String,
    val provider: String  // "GoPay", "OVO", "DANA"
) : Payment(amount, customerName) {

    override fun getFee(): Double {
        return amount * 0.015  // Biaya 1.5%
    }

    override fun processPayment(): PaymentStatus {
        if (walletId.length < 5) {
            return PaymentStatus.Failed("ID wallet tidak valid", 405)
        }

        println("📱 Memproses pembayaran $provider...")
        println("   Wallet: $walletId")
        println("   Phone: $phoneNumber")
        println("   Total: Rp ${formatRupiah(getTotalAmount())} (termasuk biaya Rp ${formatRupiah(getFee())})")

        return PaymentStatus.Success(
            transactionId = "EW-${System.currentTimeMillis()}",
            timestamp = java.time.LocalDateTime.now().toString()
        )
    }
}

/**
 * KELAS: PaymentProcessor
 * Memproses berbagai jenis pembayaran secara polimorfik
 */
class PaymentProcessor {
    private val payments = mutableListOf<Payment>()
    private val history = mutableListOf<PaymentStatus>()

    fun addPayment(payment: Payment) {
        payments.add(payment)
        println("✅ Pembayaran ditambahkan ke antrian")
    }

    fun processAllPayments() {
        println("=" .repeat(55))
        println("🔄 MEMPROSES SEMUA PEMBAYARAN")
        println("=" .repeat(55))

        for (payment in payments) {
            println()
            println("--- ${payment::class.simpleName} ---")
            val status = payment.processPayment()
            history.add(status)
            println("Status: ${status.display()}")
        }
    }

    fun showHistory() {
        println("=" .repeat(55))
        println("📋 RIWAYAT PEMBAYARAN")
        println("=" .repeat(55))

        if (history.isEmpty()) {
            println("Belum ada transaksi")
        } else {
            for ((index, status) in history.withIndex()) {
                println("${index + 1}. ${status.display()}")
            }
        }
        println("=" .repeat(55))
    }
}

/**
 * FUNGSI UTAMA — DEMO SISTEM PEMBAYARAN
 */
fun main() {
    println("=" .repeat(55))
    println("💳 DEMO SISTEM PEMBAYARAN DENGAN POLIMORFISME")
    println("=" .repeat(55))
    println()

    // Membuat berbagai metode pembayaran
    val payment1 = CreditCardPayment(
        1_000_000.0,
        "Budi Santoso",
        "1234567890123456",
        "12/26",
        "123"
    )

    val payment2 = QRISPayment(
        500_000.0,
        "Siti Rahayu",
        "QR1234567890",
        "MERCHANT001"
    )

    val payment3 = BankTransferPayment(
        2_000_000.0,
        "Ahmad Fauzi",
        "BCA",
        "1234567890"
    )

    val payment4 = EWalletPayment(
        750_000.0,
        "Dewi Lestari",
        "WALLET123",
        "08123456789",
        "GoPay"
    )

    // Processor — menangani semua jenis payment secara polimorfik
    val processor = PaymentProcessor()

    println("📥 Menambahkan pembayaran ke antrian...")
    println()
    processor.addPayment(payment1)
    processor.addPayment(payment2)
    processor.addPayment(payment3)
    processor.addPayment(payment4)

    println()
    processor.processAllPayments()
    println()
    processor.showHistory()

    // ============================================================
    // DEMONSTRASI SMART CASTING
    // ============================================================
    println()
    println("--- DEMONSTRASI SMART CASTING ---")
    val payments: List<Payment> = listOf(payment1, payment2, payment3, payment4)

    for (payment in payments) {
        when (payment) {
            is CreditCardPayment -> {
                println("🔍 Kartu Kredit: ${payment.cardNumber} (CVV: ${payment.cvv})")
                // Smart cast — payment otomatis menjadi CreditCardPayment
            }
            is QRISPayment -> {
                println("🔍 QRIS: ${payment.merchantId} - ${payment.qrCode}")
            }
            is BankTransferPayment -> {
                println("🔍 Transfer Bank: ${payment.bankName} - ${payment.accountNumber}")
            }
            is EWalletPayment -> {
                println("🔍 E-Wallet: ${payment.provider} - ${payment.walletId}")
            }
        }
    }

    // ============================================================
    // DEMONSTRASI DOWNCASTING DENGAN as?
    // ============================================================
    println()
    println("--- DEMONSTRASI DOWNCASTING DENGAN as? ---")
    val somePayment: Payment = payment1  // Upcasting (otomatis)

    // Safe downcasting dengan as?
    val creditCard = somePayment as? CreditCardPayment
    if (creditCard != null) {
        println("✅ Berhasil downcast ke CreditCardPayment")
        println("   Nomor Kartu: ${creditCard.cardNumber}")
    } else {
        println("❌ Gagal downcast — objek bukan CreditCardPayment")
    }

    // Mencoba downcast ke tipe yang salah — aman dengan as?
    val invalidCast = somePayment as? BankTransferPayment
    if (invalidCast != null) {
        println("Berhasil cast ke BankTransferPayment")
    } else {
        println("⚠️ Safe cast gagal — return null (tidak crash)")
    }

    // ============================================================
    // DEMONSTRASI FINAL METHOD
    // ============================================================
    println()
    println("--- DEMONSTRASI FINAL METHOD ---")
    println("Total yang harus dibayar: Rp ${formatRupiah(payment1.getTotalAmount())}")
    // payment1 tidak bisa meng-override getTotalAmount() karena final

    println()
    println("=" .repeat(55))
    println("🏁 PROGRAM SELESAI")
    println("=" .repeat(55))
}

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

# BAGIAN 6: LATIHAN DAN TUGAS

## 6.1 Latihan Mandiri

### Latihan 1: Hierarki Bentuk dengan Polimorfisme

Buatlah program dengan hierarki kelas bentuk dan implementasikan polimorfisme:

```kotlin
// 1. Kelas induk: Shape
//    - Metode: area(): Double (open)
//    - Metode: perimeter(): Double (open)
//    - Metode: name(): String (open)

// 2. Subclass: Circle
//    - Properti: radius: Double
//    - Implementasi area(): π * r²
//    - Implementasi perimeter(): 2 * π * r

// 3. Subclass: Rectangle
//    - Properti: width: Double, height: Double
//    - Implementasi area(): width * height
//    - Implementasi perimeter(): 2 * (width + height)

// 4. Subclass: Square (mewarisi Rectangle)
//    - Properti: side: Double
//    - Implementasi yang sesuai

// 5. Di main():
//    - Buat List<Shape> berisi berbagai shape
//    - Loop dan tampilkan area dan perimeter setiap shape
//    - Gunakan when dengan is untuk menampilkan tipe spesifik
```

### Latihan 2: Sealed Class untuk Status Order

Buatlah sealed class untuk status pesanan:

```kotlin
// 1. Sealed class: OrderStatus
//    - Success(data: String, orderId: String)
//    - Failed(reason: String, errorCode: Int)
//    - Processing(progress: Int)
//    - Pending

// 2. Fungsi: handleOrderStatus(status: OrderStatus): String
//    - Gunakan when expression yang ekshaustif
//    - Kembalikan pesan yang sesuai untuk setiap status

// 3. Di main():
//    - Buat beberapa objek OrderStatus
//    - Panggil handleOrderStatus untuk masing-masing
```

## 6.2 Tugas 4 (Dikumpulkan)

### Sistem Manajemen Karyawan dengan Polimorfisme

Buatlah program lengkap sistem manajemen karyawan yang mengimplementasikan polimorfisme dengan ketentuan berikut:

#### 1. Kelas `Employee` (Karyawan) — Kelas Induk

| **Komponen** | **Spesifikasi** |
|---|---|
| **Properti** | `id: String` (read-only)<br>`name: String` (read-only)<br>`baseSalary: Double` (read-only) |
| **Metode** | `calculateSalary(): Double` (open — default return baseSalary)<br>`calculateBonus(): Double` (open — default return 0.0)<br>`getRole(): String` (open — default return "Employee")<br>`displayInfo(): String` |

#### 2. Subclass `FullTimeEmployee` — Karyawan Tetap

| **Komponen** | **Spesifikasi** |
|---|---|
| **Properti Tambahan** | `allowance: Double` (tunjangan)<br>`annualBonus: Double` (bonus tahunan) |
| **Overriding** | `calculateSalary()` → baseSalary + allowance<br>`calculateBonus()` → annualBonus / 12<br>`getRole()` → "Full-Time Employee" |

#### 3. Subclass `PartTimeEmployee` — Karyawan Paruh Waktu

| **Komponen** | **Spesifikasi** |
|---|---|
| **Properti Tambahan** | `hourlyRate: Double`<br>`hoursWorked: Int` |
| **Overriding** | `calculateSalary()` → hourlyRate * hoursWorked<br>`calculateBonus()` → 0.0<br>`getRole()` → "Part-Time Employee" |

#### 4. Subclass `ContractEmployee` — Karyawan Kontrak

| **Komponen** | **Spesifikasi** |
|---|---|
| **Properti Tambahan** | `contractDuration: Int` (bulan)<br>`projectBonus: Double` |
| **Overriding** | `calculateSalary()` → baseSalary<br>`calculateBonus()` → projectBonus / contractDuration<br>`getRole()` → "Contract Employee" |

#### 5. Kelas `Company`

| **Komponen** | **Spesifikasi** |
|---|---|
| **Properti** | `name: String`<br>`employees: MutableList<Employee>` (private) |
| **Metode** | `addEmployee(employee: Employee)`<br>`findEmployee(id: String): Employee?`<br>`getTotalSalary(): Double`<br>`getTotalBonus(): Double`<br>`getEmployeesByRole(role: String): List<Employee>`<br>`displayAllEmployees()`<br>`displaySalaryReport()` |

#### 6. Sealed Class `EmployeeStatus`

Buat sealed class untuk status karyawan:
- `Active` — karyawan aktif
- `OnLeave` — karyawan cuti
- `Terminated` — karyawan berhenti

Implementasikan metode `display()`.

#### 7. Fungsi `main()`

- Buat objek `Company` dengan nama "PT Teknologi Maju"
- Tambahkan **minimal 6 karyawan** (2 dari setiap jenis)
- Tampilkan semua karyawan
- Tampilkan laporan gaji
- Gunakan **polymorphic references** untuk menyimpan semua karyawan
- Gunakan **smart casting** dengan `is` untuk menangani tipe berbeda
- Gunakan **sealed class** untuk status karyawan

#### 8. Kriteria Penilaian Tugas 4

| **Kriteria** | **Bobot** | **Indikator** |
|---|---|---|
| **Hierarki & Overriding** | 25% | Kelas `open`, metode `override`, penggunaan `super` |
| **Polymorphic References** | 20% | `List<Employee>` menampung berbagai subclass |
| **Smart Casting** | 15% | Menggunakan `is` dan `when` untuk type checking |
| **Sealed Class** | 15% | `EmployeeStatus` dengan `when` ekshaustif |
| **Fungsi main()** | 15% | Menampilkan semua skenario |
| **Kode Berkualitas** | 10% | Kode bersih, terstruktur, diberi komentar |

---

# BAGIAN 7: RINGKASAN MATERI PERTEMUAN 4

## 7.1 Poin-Poin Penting

| **Konsep** | **Penjelasan** | **Keyword/Sintaks** |
|---|---|---|
| **Polimorfisme** | "Banyak bentuk" — satu antarmuka, banyak implementasi | - |
| **Runtime Polymorphism** | Terjadi saat runtime via method overriding | `open` + `override` |
| **Compile-time Polymorphism** | Terjadi saat compile-time via method overloading | Method overloading |
| **Polymorphic References** | Variabel superclass menampung objek subclass | `val animal: Animal = Dog()` |
| **`is` Operator** | Type checking — apakah objek memiliki tipe tertentu | `if (obj is String)` |
| **Smart Casting** | Casting otomatis setelah type check | Otomatis setelah `is` |
| **`as` Operator** | Unsafe cast — crash jika gagal | `obj as String` |
| **`as?` Operator** | Safe cast — return null jika gagal | `obj as? String` |
| **Sealed Class** | Hierarki tertutup — semua subclass diketahui | `sealed class Result` |
| **Ekshaustif `when`** | Compiler memastikan semua kemungkinan ditangani | `when (result) { ... }` |

## 7.2 Kapan Menggunakan Apa?

| **Skenario** | **Solusi** | **Contoh** |
|---|---|---|
| Ingin metode berperilaku berbeda di subclass | Method Overriding | `override fun calculateSalary()` |
| Ingin beberapa metode dengan nama sama tapi parameter berbeda | Method Overloading | `fun add(a: Int, b: Int)` vs `fun add(a: Double, b: Double)` |
| Ingin satu fungsi menangani berbagai tipe | Polymorphic References | `fun process(animal: Animal)` |
| Ingin memeriksa tipe objek | Operator `is` | `if (obj is String)` |
| Ingin casting otomatis setelah type check | Smart Casting | Otomatis setelah `is` |
| Ingin casting yang aman (tidak crash) | Operator `as?` | `obj as? String` |
| Ingin hierarki dengan subclass terbatas | Sealed Class | `sealed class Result` |
| Ingin `when` expression yang ekshaustif | Sealed Class + `when` | `when (result) { is Success -> ... }` |

---

# BAGIAN 8: REFERENSI

## 8.1 Referensi Utama

1. **Kotlin Official Documentation – Type Checks and Casts** — [https://kotlinlang.org/docs/typecasts.html](https://kotlinlang.org/docs/typecasts.html)

2. **Kotlin Official Documentation – Sealed Classes and Interfaces** — [https://kotlinlang.org/docs/sealed-classes.html](https://kotlinlang.org/docs/sealed-classes.html)

3. **Kotlin Official Documentation – Null Safety (as and as?)** — [https://kotlinlang.org/docs/kotlin-tour-intermediate-null-safety.html](https://kotlinlang.org/docs/kotlin-tour-intermediate-null-safety.html)

4. **Kotlin Official Documentation – Serialize Polymorphic Classes** — [https://kotlinlang.org/docs/serialization-polymorphism.html](https://kotlinlang.org/docs/serialization-polymorphism.html)

## 8.2 Referensi Pendukung

5. **Kotlin Polymorphism: Dynamic and Static Examples** — codesignal.com

6. **Introduction to Polymorphism in Kotlin** — codesignal.com

7. **Kotlin Sealed Class Tutorial** — guvi.in

---

# BAGIAN 9: PENUTUP

## 9.1 Pesan untuk Mahasiswa

> **“Polimorfisme adalah kekuatan untuk menulis kode yang fleksibel dan dapat diperluas. Satu antarmuka, banyak implementasi — itulah esensi dari polimorfisme.”**

Pertemuan 4 ini adalah **puncak** dari pemahaman OOP setelah mempelajari enkapsulasi (pertemuan 2) dan pewarisan (pertemuan 3). Dengan memahami polimorfisme, Anda bisa:

- **Menulis kode yang lebih fleksibel** — satu fungsi menangani berbagai tipe
- **Membuat sistem yang dapat diperluas** — tambah kelas baru tanpa mengubah kode lama
- **Memanfaatkan smart casting** — kode lebih bersih dan aman
- **Menggunakan sealed class** — hierarki yang aman dan terkontrol

**Ingatlah:**
1. Polimorfisme adalah tentang **"banyak bentuk"** — satu antarmuka, banyak implementasi
2. **Overriding** = runtime polymorphism, **Overloading** = compile-time polymorphism
3. **Smart casting** adalah fitur andalan Kotlin — manfaatkan semaksimal mungkin
4. **`as?` lebih aman daripada `as`** — gunakan `as?` kecuali 100% yakin
5. **Sealed class** untuk hierarki yang tertutup dan aman

## 9.2 Persiapan untuk Pertemuan 5

**Materi berikutnya: ABSTRAKSI DAN INTERFACE**

Apa yang akan dipelajari:
1. Konsep abstraksi — menyembunyikan kompleksitas
2. Abstract class di Kotlin
3. Interface di Kotlin
4. Perbedaan abstract class vs interface
5. Multiple interface implementation
6. Default methods di interface
7. Studi kasus: sistem dengan abstract class dan interface

**Tugas persiapan:**
- Baca modul tentang Abstraksi dan Interface
- Review kembali konsep polimorfisme dari pertemuan 4
- Pastikan semua latihan pertemuan 4 sudah selesai

---

**Disusun oleh,**
[Nama Dosen Pengampu]
Dosen Program Studi D4 Teknologi Rekayasa Informatika Industri
