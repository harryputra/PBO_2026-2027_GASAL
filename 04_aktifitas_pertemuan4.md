# RENCANA PEMBELAJARAN SEMESTER (RPS)
## PERTEMUAN KE-4 — RENCANA PELAKSANAAN PEMBELAJARAN (RPP)
### PEMROGRAMAN BERORIENTASI OBJEK (OBJECT-ORIENTED PROGRAMMING)
### “Polimorfisme — Satu Interface, Banyak Bentuk”

---

## A. IDENTITAS PERTEMUAN

| **Komponen** | **Keterangan** |
|---|---|
| **Pertemuan Ke-** | 4 |
| **Topik** | Polimorfisme (Polymorphism) — Polymorphic References, Method Overriding & Overloading, Upcasting & Downcasting, Smart Casting, dan Sealed Class |
| **Durasi** | 8 Jam Praktik (480 menit) |
| **Hari/Tanggal** | [Disesuaikan] |
| **Ruang** | Laboratorium Komputer |
| **Dosen** | [Nama Dosen] |
| **Capaian Pembelajaran** | Mahasiswa memahami konsep polimorfisme dalam OOP, mampu mengimplementasikan polymorphic references, memahami perbedaan overriding dan overloading, mampu melakukan upcasting dan downcasting dengan aman, memahami smart casting di Kotlin, serta mampu menerapkan polimorfisme dalam studi kasus nyata |

---

## B. CAPAIAN PEMBELAJARAN PERTEMUAN (CPP)

Setelah mengikuti pertemuan ke-4 ini, mahasiswa mampu:

1. **CPP 4.1:** Menjelaskan konsep polimorfisme dan manfaatnya dalam pemrograman berorientasi objek.
2. **CPP 4.2:** Membedakan antara method overriding (runtime polymorphism) dan method overloading (compile-time polymorphism).
3. **CPP 4.3:** Mengimplementasikan polymorphic references — referensi superclass ke objek subclass.
4. **CPP 4.4:** Memahami dan melakukan upcasting (casting ke superclass) dan downcasting (casting ke subclass).
5. **CPP 4.5:** Menggunakan operator `is` dan `!is` untuk type checking di Kotlin.
6. **CPP 4.6:** Memahami dan memanfaatkan smart casting di Kotlin.
7. **CPP 4.7:** Menggunakan operator `as` dan `as?` untuk explicit casting.
8. **CPP 4.8:** Memahami konsep sealed class untuk closed polymorphism.
9. **CPP 4.9:** Menerapkan polimorfisme dalam studi kasus nyata (sistem pembayaran/manajemen karyawan).

---

## C. MATERI POKOK

### 1. Pendahuluan: Apa itu Polimorfisme? (Sesi 1)

#### 1.1 Definisi Polimorfisme

**Polimorfisme (Polymorphism)** adalah salah satu dari **empat pilar utama OOP** yang berarti **"banyak bentuk"** (dari bahasa Yunani: *poly* = banyak, *morph* = bentuk). Dalam konteks pemrograman, polimorfisme memungkinkan objek-objek dari kelas yang berbeda untuk **merespons pesan yang sama dengan cara yang berbeda**.

> **Definisi Sederhana:** Polimorfisme adalah kemampuan sebuah metode atau operasi untuk **berperilaku berbeda** tergantung pada objek yang menjalankannya. Satu interface (antar muka) yang sama dapat memiliki banyak implementasi yang berbeda.

#### 1.2 Analogi Polimorfisme dalam Kehidupan Nyata

| **Analogi** | **Penjelasan** |
|---|---|
| **Tombol "Mulai" di berbagai perangkat** | Tombol yang sama (interface) tetapi efeknya berbeda: di TV → menyalakan gambar, di AC → menyalakan pendingin, di mobil → menyalakan mesin |
| **Perintah "bunyikan suara" untuk hewan** | Perintah yang sama, tetapi setiap hewan merespons dengan suara yang berbeda: anjing menggonggong, kucing mengeong, sapi melenguh |
| **Metode pembayaran** | Metode `bayar(jumlah)` yang sama, tetapi implementasinya berbeda: kartu kredit → potong limit, QRIS → kurangi saldo e-wallet, transfer bank → kurangi saldo rekening |
| **Kendaraan yang dikemudikan** | Perintah "belok kanan" yang sama, tetapi cara belok mobil, motor, dan kapal berbeda |

#### 1.3 Mengapa Polimorfisme Penting?

| **Manfaat** | **Penjelasan** |
|---|---|
| **Fleksibilitas Kode** | Kode dapat bekerja dengan objek dari berbagai tipe tanpa perlu mengetahui detail spesifiknya |
| **Extensibility** | Kita dapat menambahkan kelas baru tanpa mengubah kode yang sudah ada |
| **Code Reusability** | Satu fungsi dapat menangani berbagai tipe objek |
| **Abstraksi** | Pengguna kode hanya perlu tahu interface-nya, bukan implementasinya |
| **Mendukung Prinsip Open/Closed** | Kode terbuka untuk ekstensi (kelas baru) tetapi tertutup untuk modifikasi |

---

### 2. Dua Jenis Polimorfisme di Kotlin (Sesi 1)

Polimorfisme di Kotlin (dan OOP secara umum) terbagi menjadi **dua jenis utama**:

| **Jenis** | **Nama Lain** | **Waktu Binding** | **Contoh** |
|---|---|---|---|
| **Method Overriding** | Runtime Polymorphism / Dynamic Polymorphism | Saat runtime (dinamis) | Subclass meng-override metode dari superclass |
| **Method Overloading** | Compile-time Polymorphism / Static Polymorphism | Saat compile-time (statis) | Beberapa metode dengan nama yang sama tapi parameter berbeda |

#### 2.1 Runtime Polymorphism (Method Overriding)

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
- Metode yang di-override bersifat `open` secara default, bisa ditambah `final` untuk menghentikan overriding lebih lanjut

#### 2.2 Compile-time Polymorphism (Method Overloading)

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

#### 2.3 Perbandingan Overriding vs Overloading

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

### 3. Polymorphic References (Referensi Polimorfik) (Sesi 1-2)

#### 3.1 Konsep Polymorphic References

**Polymorphic references** adalah kemampuan untuk **menyimpan objek dari subclass ke dalam variabel bertipe superclass**.

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

#### 3.2 Mengapa Polymorphic References Penting?

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

#### 3.3 Contoh Lengkap: Polymorphic Array/List

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

### 4. Upcasting dan Downcasting (Sesi 2)

#### 4.1 Apa itu Casting?

**Casting** adalah proses **mengkonversi** sebuah objek dari satu tipe ke tipe lainnya.

| **Jenis Casting** | **Arah** | **Deskripsi** |
|---|---|---|
| **Upcasting** | Subclass → Superclass | **Selalu aman** — otomatis dilakukan oleh Kotlin |
| **Downcasting** | Superclass → Subclass | **Perlu pengecekan** — bisa gagal jika objek bukan tipe yang dimaksud |

#### 4.2 Upcasting (Casting ke Superclass)

**Upcasting** adalah proses mengkonversi objek dari subclass ke superclass. Ini **selalu aman** karena setiap objek subclass adalah juga objek superclass.

```kotlin
open class Animal
class Dog : Animal()

fun main() {
    val dog = Dog()

    // Upcasting — otomatis dan aman
    val animal: Animal = dog  // Implicit upcasting
    val animal2 = dog as Animal  // Explicit upcasting (tidak perlu)
}
```

**Upcasting di Kotlin terjadi secara otomatis** — Anda tidak perlu melakukan casting secara eksplisit.

#### 4.3 Downcasting (Casting ke Subclass)

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
        val dog = animal as Dog  // Aman karena sudah dicek
        dog.bark()
    }
}
```

#### 4.4 Operator `is` dan `!is` untuk Type Checking

Gunakan operator **`is`** (dan **`!is`** untuk negasi) untuk memeriksa apakah sebuah objek memiliki tipe tertentu.

```kotlin
open class Animal
class Dog : Animal() {
    fun bark() = println("Guk! Guk!")
}
class Cat : Animal() {
    fun meow() = println("Meong! Meong!")
}

fun handleAnimal(animal: Animal) {
    // Type checking dengan is
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

#### 4.5 Smart Casting di Kotlin

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

// 3. while loop
fun processWhile(value: Any) {
    while (value is String) {
        println(value.length)  // Smart cast ke String
        // ...
    }
}
```

#### 4.6 Operator Casting: `as` dan `as?`

Untuk casting eksplisit, Kotlin menyediakan dua operator:

| **Operator** | **Deskripsi** | **Perilaku jika gagal** |
|---|---|---|
| `as` | Unsafe cast | **Throw ClassCastException** (crash) |
| `as?` | Safe cast | **Return null** (tidak crash) |

```kotlin
fun main() {
    val obj: Any = "Hello"

    // Unsafe cast — bisa crash jika gagal
    val str1: String = obj as String  // ✅ Berhasil
    // val num1: Int = obj as Int     // ❌ ClassCastException!

    // Safe cast — return null jika gagal
    val str2: String? = obj as? String  // ✅ Berhasil: "Hello"
    val num2: Int? = obj as? Int        // ✅ Aman: null (tidak crash)

    println(str2)  // Output: Hello
    println(num2)  // Output: null
}
```

**Best Practice:** Gunakan `as?` daripada `as` kecuali Anda **100% yakin** casting akan berhasil.

---

### 5. Sealed Class — Closed Polymorphism (Sesi 3)

#### 5.1 Apa itu Sealed Class?

**Sealed class** adalah kelas yang **membatasi hierarki subclass** — semua subclass dari sealed class harus dideklarasikan **dalam file yang sama** dengan sealed class tersebut.

> **Closed Polymorphism:** Semua subclass dari sealed class **diketahui pada saat compile time**.

#### 5.2 Mengapa Sealed Class?

| **Keuntungan Sealed Class** | **Penjelasan** |
|---|---|
| **Ekshaustif `when`** | Compiler memastikan semua kemungkinan ditangani di `when` expression |
| **Type Safety** | Tidak ada subclass yang tidak terduga |
| **Mewakili State Terbatas** | Cocok untuk mewakili state yang terbatas (Success, Loading, Error) |
| **Closed Polymorphism** | Semua subclass diketahui di compile time |

#### 5.3 Sintaks Sealed Class

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

#### 5.4 Sealed Interface (Kotlin 1.5+)

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

#### 5.5 Sealed Class vs Enum Class

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

#### 5.6 Sealed Class dengan `when` Ekshaustif

Keunggulan utama sealed class adalah **`when` expression yang ekshaustif**:

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

### 6. Studi Kasus: Sistem Pembayaran dengan Polimorfisme (Sesi 3-4)

Mari kita bangun sistem pembayaran yang mengimplementasikan semua konsep polimorfisme.

#### 6.1 Analisis Kebutuhan

| **Metode Pembayaran** | **Atribut** | **Perilaku** |
|---|---|---|
| **Payment (Base)** | amount: Double | processPayment(): Boolean, getFee(): Double |
| **CreditCard** | cardNumber, expiryDate, cvv | Fee = 2% dari amount |
| **QRIS** | qrCode, merchantId | Fee = 0.5% dari amount |
| **BankTransfer** | bankName, accountNumber | Fee = 1% dari amount (minimal Rp 5.000) |
| **E-Wallet** | walletId, phoneNumber | Fee = 1.5% dari amount |

#### 6.2 Implementasi Lengkap

```kotlin
/**
 * ============================================================
 * SISTEM PEMBAYARAN DENGAN POLIMORFISME
 * ============================================================
 * Demonstrasi:
 * 1. Polymorphic references
 * 2. Method overriding (runtime polymorphism)
 * 3. Upcasting dan downcasting
 * 4. Smart casting dengan is
 * 5. Sealed class untuk status pembayaran
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
    // Init block untuk logging
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

    // Helper untuk format Rupiah
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
        // Simulasi validasi kartu kredit
        if (cardNumber.length < 16) {
            return PaymentStatus.Failed("Nomor kartu tidak valid", 401)
        }
        if (cvv.length != 3) {
            return PaymentStatus.Failed("CVV tidak valid", 402)
        }

        // Simulasi pemrosesan
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
        // Simulasi validasi QRIS
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
        // Simulasi validasi transfer
        if (accountNumber.length < 8) {
            return PaymentStatus.Failed("Nomor rekening tidak valid", 404)
        }

        println("🏦 Memproses transfer bank...")
        println("   Bank: $bankName")
        println("   Rekening: $accountNumber")
        println("   Total: Rp ${formatRupiah(getTotalAmount())} (termasuk biaya Rp ${formatRupiah(getFee())})")

        // Simulasi — transfer bank butuh waktu
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
        // Simulasi validasi e-wallet
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

    // Menambahkan pembayaran — polymorphic parameter
    fun addPayment(payment: Payment) {
        payments.add(payment)
        println("✅ Pembayaran ditambahkan ke antrian")
    }

    // Memproses semua pembayaran — polymorphic loop
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

    // Menampilkan riwayat pembayaran
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

    // Demonstrasi Smart Casting
    println()
    println("--- DEMONSTRASI SMART CASTING ---")
    val payments: List<Payment> = listOf(payment1, payment2, payment3, payment4)

    for (payment in payments) {
        // Type checking dengan is
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
            else -> {
                println("🔍 Metode pembayaran tidak dikenal")
            }
        }
    }

    // Demonstrasi Downcasting dengan as?
    println()
    println("--- DEMONSTRASI DOWNCASTING ---")
    val somePayment: Payment = payment1  // Upcasting (otomatis)

    // Safe downcasting dengan as?
    val creditCard = somePayment as? CreditCardPayment
    if (creditCard != null) {
        println("✅ Berhasil downcast ke CreditCardPayment")
        println("   Nomor Kartu: ${creditCard.cardNumber}")
    } else {
        println("❌ Gagal downcast — objek bukan CreditCardPayment")
    }

    // Unsafe downcasting — bisa crash!
    try {
        val invalidCast = somePayment as? BankTransferPayment
        if (invalidCast != null) {
            println("Berhasil cast ke BankTransferPayment")
        } else {
            println("⚠️ Safe cast gagal — return null (tidak crash)")
        }
    } catch (e: Exception) {
        println("❌ Crash: ${e.message}")
    }

    // Demonstrasi bahwa getTotalAmount() adalah final
    println()
    println("--- DEMONSTRASI FINAL METHOD ---")
    println("Total yang harus dibayar untuk payment1: Rp ${formatRupiah(payment1.getTotalAmount())}")
    // payment1 tidak bisa meng-override getTotalAmount() karena final

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

## D. RINCIAN KEGIATAN PEMBELAJARAN (8 JAM)

### Sesi 1: Pengantar Polimorfisme & Perbandingan Overriding vs Overloading (2 Jam — 120 menit)

| **Waktu** | **Kegiatan** | **Detail** | **Metode** |
|---|---|---|---|
| **0-10'** | Pembukaan & Review | • Dosen membuka perkuliahan dengan salam dan doa<br>• Review singkat materi pertemuan 3 (inheritance, open, override, super)<br>• Menghubungkan inheritance dengan polimorfisme | Ceramah interaktif, Tanya jawab |
| **10-40'** | Konsep Polimorfisme | • **Definisi polimorfisme** — "banyak bentuk"<br>• **Analogi polimorfisme** (tombol, perintah suara, pembayaran)<br>• **Manfaat polimorfisme** — fleksibilitas, extensibility, reusability<br>• **Dua jenis polimorfisme**: runtime (overriding) dan compile-time (overloading)<br>• **Runtime Polymorphism** — method overriding dengan `open` dan `override`<br>• **Compile-time Polymorphism** — method overloading | Ceramah, Analogi, Diskusi |
| **40-70'** | Perbandingan Overriding vs Overloading | • **Method Overriding** — subclass memberikan implementasi spesifik<br>  - Memerlukan inheritance<br>  - Metode superclass harus `open`<br>  - Metode subclass harus `override`<br>  - Terjadi saat runtime<br>• **Method Overloading** — beberapa metode dengan nama sama, parameter berbeda<br>  - Tidak memerlukan inheritance<br>  - Terjadi saat compile-time<br>• **Perbandingan** dalam tabel<br>• Demo kode: Overriding dan Overloading | Ceramah, Demonstrasi, Live Coding |
| **70-90'** | Praktik Overriding & Overloading | • Mahasiswa membuat kelas `Shape` dengan metode `area()`<br>• Membuat subclass `Circle`, `Rectangle`, `Triangle` dengan override<br>• Membuat kelas `Calculator` dengan method overloading `add()`<br>• Mengamati perbedaan perilaku | Praktik terbimbing |
| **90-120'** | Diskusi & Review | • Diskusi kelompok: "Kapan menggunakan overriding vs overloading?"<br>• Dosen memberikan contoh kasus nyata<br>• Q&A dan penyimpulan | Diskusi kelompok, Tanya jawab |

---

### Sesi 2: Polymorphic References, Upcasting, Downcasting, dan Smart Casting (2 Jam — 120 menit)

| **Waktu** | **Kegiatan** | **Detail** | **Metode** |
|---|---|---|---|
| **0-10'** | Review Singkat | • Mereview overriding dan overloading<br>• Menghubungkan dengan polymorphic references | Ceramah |
| **10-40'** | Polymorphic References | • **Konsep** — variabel superclass menampung objek subclass<br>• **Mengapa penting** — kode lebih umum dan fleksibel<br>• **Polymorphic array/list** — satu koleksi menampung berbagai subclass<br>• Demo: `List<Animal>` berisi `Dog`, `Cat`, dll<br>• Demo: Satu fungsi `processAnimal(animal: Animal)` menangani semua subclass | Ceramah, Demonstrasi, Live Coding |
| **40-70'** | Upcasting dan Downcasting | • **Upcasting** — subclass → superclass (selalu aman, otomatis)<br>• **Downcasting** — superclass → subclass (perlu pengecekan)<br>• **Operator `is` dan `!is`** — type checking<br>• **Smart casting** — casting otomatis setelah type check<br>  - Bekerja di `if`, `when`, `while`<br>• **Operator `as` dan `as?`** — explicit casting<br>  - `as` = unsafe (crash jika gagal)<br>  - `as?` = safe (return null jika gagal)<br>• Demo: Semua konsep casting | Ceramah, Demonstrasi, Live Coding |
| **70-90'** | Praktik Casting & Smart Casting | • Mahasiswa membuat hierarki `Animal` → `Dog`, `Cat`, `Bird`<br>• Membuat fungsi dengan parameter `Animal`<br>• Menggunakan `is` untuk type checking<br>• Mengamati smart casting di `when` expression<br>• Mencoba `as` dan `as?` | Praktik mandiri, Asistensi |
| **90-120'** | Praktik Lanjutan | • Mahasiswa membuat polymorphic list<br>• Mengiterasi list dan melakukan type-specific operations<br>• Dosen berkeliling memberikan asistensi | Praktik mandiri, Asistensi |

---

### Sesi 3: Sealed Class & Studi Kasus Sistem Pembayaran (2 Jam — 120 menit)

| **Waktu** | **Kegiatan** | **Detail** | **Metode** |
|---|---|---|---|
| **0-10'** | Review & Motivasi | • Review casting dan smart casting<br>• "Bagaimana membuat hierarki yang lebih aman dengan closed polymorphism?" | Ceramah |
| **10-45'** | Sealed Class | • **Konsep sealed class** — semua subclass diketahui di compile time<br>• **Closed polymorphism** vs open polymorphism<br>• **Sintaks sealed class** — semua subclass di file yang sama<br>• **Sealed interface** (Kotlin 1.5+)<br>• **Sealed Class vs Enum Class** — kapan menggunakan masing-masing<br>• **Ekshaustif `when`** — compiler memastikan semua kemungkinan ditangani<br>• Demo: `Result` dengan `Success`, `Error`, `Loading` | Ceramah, Demonstrasi, Live Coding |
| **45-75'** | Studi Kasus: Sistem Pembayaran | • **Analisis kebutuhan** — berbagai metode pembayaran<br>• **Hierarki kelas** — `Payment` (induk) → `CreditCardPayment`, `QRISPayment`, dll<br>• **Sealed class `PaymentStatus`** — `Success`, `Failed`, `Pending`<br>• **Polymorphic processing** — satu processor menangani semua payment<br>• **Live coding** bersama dosen | Demonstrasi, Live Coding, Diskusi |
| **75-90'** | Praktik Sistem Pembayaran | • Mahasiswa mengimplementasikan sistem pembayaran sendiri<br>• Menambahkan metode pembayaran baru<br>• Dosen memberikan asistensi | Praktik mandiri, Asistensi |
| **90-120'** | Review & Diskusi Kasus | • Beberapa mahasiswa mempresentasikan kode mereka<br>• Diskusi: "Mengapa sealed class lebih aman untuk status?"<br>• Q&A dan penyimpulan | Presentasi, Diskusi |

---

### Sesi 4: Tugas 4 & Penutupan (2 Jam — 120 menit)

| **Waktu** | **Kegiatan** | **Detail** | **Metode** |
|---|---|---|---|
| **0-15'** | Review Materi Pertemuan 4 | • Rangkuman seluruh materi:<br>  - Polimorfisme dan manfaatnya<br>  - Overriding vs Overloading<br>  - Polymorphic references<br>  - Upcasting dan downcasting<br>  - Smart casting dengan `is`<br>  - Operator `as` dan `as?`<br>  - Sealed class untuk closed polymorphism<br>• Menjawab pertanyaan mahasiswa | Review, Tanya jawab |
| **15-45'** | Studi Kasus: Sistem Karyawan | • Dosen menjelaskan studi kasus sistem manajemen karyawan (lihat bagian E)<br>• Menganalisis kebutuhan dan hierarki kelas<br>• Menjelaskan bagaimana polimorfisme diterapkan | Demonstrasi, Diskusi |
| **45-90'** | Pengerjaan Tugas 4 | • Mahasiswa mengerjakan Tugas 4 secara mandiri (lihat bagian E)<br>• Dosen berkeliling memberikan bimbingan intensif<br>• Mahasiswa dapat bertanya jika mengalami kendala | Praktik mandiri, Asistensi intensif |
| **90-105'** | Pengumpulan & Presentasi | • Mahasiswa mengumpulkan Tugas 4<br>• 2-3 mahasiswa diminta mempresentasikan kodenya<br>• Dosen memberikan feedback konstruktif | Presentasi, Feedback |
| **105-120'** | Penutupan | • Dosen merangkum pencapaian pertemuan 4<br>• Preview materi pertemuan 5 (Abstraksi & Interface)<br>• Memberikan tugas membaca modul pertemuan 5<br>• Menutup perkuliahan dengan doa dan salam | Ceramah |

---

## E. TUGAS 4 (Dikumpulkan)

### Sistem Manajemen Karyawan dengan Polimorfisme

Buatlah program lengkap sistem manajemen karyawan yang mengimplementasikan polimorfisme dengan ketentuan berikut:

#### 1. Kelas `Employee` (Karyawan) — Kelas Induk

| **Komponen** | **Spesifikasi** |
|---|---|
| **Properti** | `id: String` (read-only)<br>`name: String` (read-only)<br>`baseSalary: Double` (read-only) |
| **Metode** | `calculateSalary(): Double` (open — default return baseSalary)<br>`calculateBonus(): Double` (open — default return 0.0)<br>`getRole(): String` (open — default return "Employee")<br>`displayInfo(): String` — menampilkan info karyawan |

#### 2. Subclass `FullTimeEmployee` — Karyawan Tetap

| **Komponen** | **Spesifikasi** |
|---|---|
| **Properti Tambahan** | `allowance: Double` (tunjangan)<br>`annualBonus: Double` (bonus tahunan) |
| **Overriding** | `calculateSalary()` → baseSalary + allowance<br>`calculateBonus()` → annualBonus / 12 (per bulan)<br>`getRole()` → "Full-Time Employee" |

#### 3. Subclass `PartTimeEmployee` — Karyawan Paruh Waktu

| **Komponen** | **Spesifikasi** |
|---|---|
| **Properti Tambahan** | `hourlyRate: Double`<br>`hoursWorked: Int` |
| **Overriding** | `calculateSalary()` → hourlyRate * hoursWorked<br>`calculateBonus()` → 0.0 (tidak ada bonus)<br>`getRole()` → "Part-Time Employee" |

#### 4. Subclass `ContractEmployee` — Karyawan Kontrak

| **Komponen** | **Spesifikasi** |
|---|---|
| **Properti Tambahan** | `contractDuration: Int` (dalam bulan)<br>`projectBonus: Double` (bonus proyek) |
| **Overriding** | `calculateSalary()` → baseSalary<br>`calculateBonus()` → projectBonus / contractDuration<br>`getRole()` → "Contract Employee" |

#### 5. Kelas `Company`

| **Komponen** | **Spesifikasi** |
|---|---|
| **Properti** | `name: String` (read-only)<br>`employees: MutableList<Employee>` (private) |
| **Metode** | `addEmployee(employee: Employee)`<br>`findEmployee(id: String): Employee?`<br>`getTotalSalary(): Double` — total gaji semua karyawan<br>`getTotalBonus(): Double` — total bonus semua karyawan<br>`getEmployeesByRole(role: String): List<Employee>`<br>`displayAllEmployees()`<br>`displaySalaryReport()` — menampilkan laporan gaji per karyawan |

#### 6. Sealed Class `EmployeeStatus` (Closed Polymorphism)

Buat sealed class untuk status karyawan:
- `Active` — karyawan aktif
- `OnLeave` — karyawan cuti
- `Terminated` — karyawan berhenti

Implementasikan metode `display()` untuk menampilkan status.

#### 7. Fungsi `main()`

- Buat objek `Company` dengan nama "PT Teknologi Maju"
- Tambahkan **minimal 6 karyawan** (2 dari setiap jenis)
- Tampilkan semua karyawan
- Tampilkan laporan gaji
- Tampilkan total gaji dan bonus
- Gunakan **polymorphic references** untuk menyimpan semua karyawan dalam satu list
- Gunakan **smart casting** dengan `is` untuk menangani tipe karyawan yang berbeda
- Gunakan **sealed class** untuk status karyawan

#### 8. Kriteria Penilaian Tugas 4

| **Kriteria** | **Bobot** | **Indikator** |
|---|---|---|
| **Hierarki Pewarisan & Overriding** | 25% | • Kelas induk `Employee` menggunakan `open`<br>• Metode di-override dengan benar di semua subclass<br>• `super` digunakan dengan tepat |
| **Polymorphic References** | 20% | • `List<Employee>` menampung berbagai subclass<br>• Satu fungsi menangani semua tipe Employee |
| **Smart Casting** | 15% | • Menggunakan `is` untuk type checking<br>• Memanfaatkan smart casting di `when` expression |
| **Sealed Class** | 15% | • `EmployeeStatus` sebagai sealed class<br>• `when` expression ekshaustif |
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
| **Modul Praktikum** | Modul cetak/digital pertemuan 4 |
| **Kotlin Playground** | Alternatif untuk mencoba kode tanpa instalasi |

---

## G. PENILAIAN PERTEMUAN 4

| **Komponen** | **Bobot** | **Indikator** | **Teknik** |
|---|---|---|---|
| **Keaktifan Sesi 1-3** | 15% dari total keaktifan | • Kehadiran tepat waktu<br>• Partisipasi dalam diskusi dan tanya jawab<br>• Keterlibatan dalam praktik kelompok | Observasi |
| **Tugas 4** | 100% dari nilai tugas 4 | • Lihat kriteria penilaian Tugas 4 di atas | Penilaian kode |
| **Kuis Singkat** | Bonus | • Pertanyaan tentang overriding, overloading, casting, sealed class | Tes tertulis/lisan |

---

## H. REFERENSI PERTEMUAN 4

### Referensi Utama:

1. **Kotlin Official Documentation – Inheritance** — [https://kotlinlang.org/docs/inheritance.html](https://kotlinlang.org/docs/inheritance.html)

2. **Kotlin Official Documentation – Open and Special Classes** — [https://kotlinlang.org/docs/kotlin-tour-intermediate-open-special-classes.html](https://kotlinlang.org/docs/kotlin-tour-intermediate-open-special-classes.html)

3. **Kotlin Official Documentation – Type Checks and Casts** — [https://kotlinlang.org/docs/typecasts.html](https://kotlinlang.org/docs/typecasts.html)

4. **Kotlin Official Documentation – Serialize Polymorphic Classes** — [https://kotlinlang.org/docs/serialization-polymorphism.html](https://kotlinlang.org/docs/serialization-polymorphism.html)

### Referensi Pendukung:

5. **Kotlin Sealed Classes** — [https://kotlinlang.org/docs/sealed-classes.html](https://kotlinlang.org/docs/sealed-classes.html)

6. **Kotlin Sealed Interfaces (What's New in 1.5)** — [https://kotlinlang.org/docs/whatsnew15.html#sealed-interfaces](https://kotlinlang.org/docs/whatsnew15.html#sealed-interfaces)

7. **Android Developers – Kotlin Polymorphism** — [https://developer.android.com/kotlin/learn](https://developer.android.com/kotlin/learn)

---

## I. LAMPIRAN

### Lampiran 1: Perbandingan Overriding vs Overloading — Contoh Lengkap

```kotlin
/**
 * DEMONSTRASI PERBANDINGAN OVERRIDING VS OVERLOADING
 */

// ============================================================
// 1. OVERRIDING — Runtime Polymorphism
// ============================================================

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

// ============================================================
// 2. OVERLOADING — Compile-time Polymorphism
// ============================================================

class MathOperations {
    // Overloading: nama sama, parameter berbeda
    fun add(a: Int, b: Int): Int = a + b
    fun add(a: Double, b: Double): Double = a + b
    fun add(a: Int, b: Int, c: Int): Int = a + b + c
    fun add(a: String, b: String): String = a + b
}

fun main() {
    println("=== OVERRIDING (Runtime) ===")
    val animals: List<Animal> = listOf(Dog(), Cat(), Dog())
    for (animal in animals) {
        animal.makeSound()  // Output berbeda tergantung tipe sebenarnya
    }

    println("\n=== OVERLOADING (Compile-time) ===")
    val math = MathOperations()
    println(math.add(5, 3))           // Output: 8 (Int)
    println(math.add(5.5, 3.2))       // Output: 8.7 (Double)
    println(math.add(5, 3, 2))        // Output: 10 (Int)
    println(math.add("Hello", "World")) // Output: HelloWorld (String)
}
```

### Lampiran 2: Perbandingan Sealed Class vs Enum Class

```kotlin
/**
 * PERBANDINGAN SEALED CLASS VS ENUM CLASS
 */

// ============================================================
// ENUM CLASS — untuk konstanta sederhana
// ============================================================

enum class SimpleStatus {
    SUCCESS,
    ERROR,
    LOADING
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

### Lampiran 3: Checklist Pemahaman Mahasiswa

| **No** | **Konsep** | **Paham** | **Kurang Paham** | **Tidak Paham** |
|---|---|---|---|---|
| 1 | Definisi polimorfisme | ☐ | ☐ | ☐ |
| 2 | Manfaat polimorfisme | ☐ | ☐ | ☐ |
| 3 | Method Overriding (runtime polymorphism) | ☐ | ☐ | ☐ |
| 4 | Method Overloading (compile-time polymorphism) | ☐ | ☐ | ☐ |
| 5 | Perbedaan overriding vs overloading | ☐ | ☐ | ☐ |
| 6 | Polymorphic references | ☐ | ☐ | ☐ |
| 7 | Upcasting | ☐ | ☐ | ☐ |
| 8 | Downcasting | ☐ | ☐ | ☐ |
| 9 | Operator `is` dan `!is` | ☐ | ☐ | ☐ |
| 10 | Smart casting | ☐ | ☐ | ☐ |
| 11 | Operator `as` dan `as?` | ☐ | ☐ | ☐ |
| 12 | Sealed class | ☐ | ☐ | ☐ |
| 13 | Sealed interface | ☐ | ☐ | ☐ |
| 14 | Closed polymorphism | ☐ | ☐ | ☐ |
| 15 | Menerapkan polimorfisme dalam kode | ☐ | ☐ | ☐ |

---

**Disusun oleh,**
M Harry K Saputra
Dosen Program Studi D4 Teknologi Rekayasa Informatika Industri
