# RENCANA PEMBELAJARAN SEMESTER (RPS)
## PERTEMUAN KE-7 — RENCANA PELAKSANAAN PEMBELAJARAN (RPP)
### PEMROGRAMAN BERORIENTASI OBJEK (OBJECT-ORIENTED PROGRAMMING)
### “Generic, Collection & Exception Handling — Memanipulasi Data dan Mengelola Error”

---

## A. IDENTITAS PERTEMUAN

| **Komponen** | **Keterangan** |
|---|---|
| **Pertemuan Ke-** | 7 |
| **Topik** | Generic, Collection & Exception Handling |
| **Durasi** | 8 Jam Praktik (480 menit) |
| **Hari/Tanggal** | [Disesuaikan] |
| **Ruang** | Laboratorium Komputer |
| **Dosen** | [Nama Dosen] |
| **Capaian Pembelajaran** | Mahasiswa memahami dan mampu mengimplementasikan konsep Generic (kelas, fungsi, interface generic), mampu menggunakan Collection (List, Set, Map) beserta operasi-operasinya (filter, map, dll), serta mampu melakukan Exception Handling dengan try-catch-finally dan runCatching |

---

## B. CAPAIAN PEMBELAJARAN PERTEMUAN (CPP)

Setelah mengikuti pertemuan ke-7 ini, mahasiswa mampu:

1. **CPP 7.1:** Menjelaskan konsep Generic dan manfaatnya dalam meningkatkan type safety dan reusability kode.
2. **CPP 7.2:** Mendefinisikan dan menggunakan Generic Class, Generic Interface, dan Generic Function di Kotlin.
3. **CPP 7.3:** Memahami dan menggunakan Generic Constraints (batasan tipe) dengan `where` clause.
4. **CPP 7.4:** Menjelaskan tiga jenis Collection di Kotlin: `List`, `Set`, dan `Map` serta perbedaan read-only vs mutable.
5. **CPP 7.5:** Menggunakan fungsi-fungsi Collection Operations seperti `filter()`, `map()`, `forEach()`, `sorted()`, dll.
6. **CPP 7.6:** Menjelaskan konsep Exception Handling dan perbedaan checked vs unchecked exception.
7. **CPP 7.7:** Mengimplementasikan `try-catch-finally` untuk menangani exception.
8. **CPP 7.8:** Menggunakan `runCatching` sebagai alternatif modern untuk exception handling.
9. **CPP 7.9:** Memahami dan menggunakan `throw` expression serta tipe `Nothing`.
10. **CPP 7.10:** Menerapkan Generic, Collection, dan Exception Handling dalam studi kasus terintegrasi.

---

## C. MATERI POKOK

### 1. Generic — Type Safety dan Reusability (Sesi 1)

#### 1.1 Apa itu Generic?

**Generic** adalah fitur yang memungkinkan Anda menulis kode yang **type-safe** dan **reusable** dengan menggunakan **type parameters** (parameter tipe).

> **Definisi Sederhana:** Generic adalah "cetakan kode" yang bisa bekerja dengan berbagai tipe data tanpa harus menulis ulang kode untuk setiap tipe.

#### 1.2 Mengapa Generic Penting?

| **Manfaat** | **Penjelasan** |
|---|---|
| **Type Safety** | Kompiler memeriksa tipe data, mencegah error runtime |
| **Reusability** | Satu kode bisa digunakan untuk berbagai tipe data |
| **Readability** | Kode lebih bersih dan mudah dipahami |
| **Eliminasi Casting** | Tidak perlu melakukan casting secara manual |

#### 1.3 Generic Class

```kotlin
// Definisi Generic Class
class Box<T>(private var content: T) {
    fun getContent(): T = content
    fun setContent(newContent: T) {
        content = newContent
    }
}

fun main() {
    // Penggunaan Generic Class
    val intBox = Box<Int>(42)
    val strBox = Box<String>("Hello")

    println(intBox.getContent())  // Output: 42
    println(strBox.getContent())  // Output: Hello
}
```

#### 1.4 Generic Interface

```kotlin
// Definisi Generic Interface
interface Comparator<T> {
    fun compare(a: T, b: T): Int
}

// Implementasi Generic Interface
class IntComparator : Comparator<Int> {
    override fun compare(a: Int, b: Int): Int = a - b
}

class StringComparator : Comparator<String> {
    override fun compare(a: String, b: String): Int = a.compareTo(b)
}

fun main() {
    val intComp = IntComparator()
    val strComp = StringComparator()

    println(intComp.compare(5, 3))     // Output: 2
    println(strComp.compare("apple", "banana"))  // Output: -1
}
```

#### 1.5 Generic Function

```kotlin
// Generic Function
fun <T> printList(items: List<T>) {
    for (item in items) {
        println(item)
    }
}

fun <T> findMax(a: T, b: T, comparator: Comparator<T>): T {
    return if (comparator.compare(a, b) > 0) a else b
}

fun main() {
    val numbers = listOf(1, 2, 3, 4, 5)
    printList(numbers)  // Output: 1 2 3 4 5

    val strings = listOf("apple", "banana", "cherry")
    printList(strings)  // Output: apple banana cherry

    val maxInt = findMax(10, 20, IntComparator())
    println(maxInt)  // Output: 20
}
```

#### 1.6 Generic Constraints (Batasan Tipe)

Kita bisa membatasi tipe parameter dengan **Generic Constraints** menggunakan `where` clause.

```kotlin
// Generic dengan constraint: T harus merupakan subclass dari Number
fun <T : Number> sumNumbers(a: T, b: T): Double {
    return a.toDouble() + b.toDouble()
}

// Generic dengan multiple constraints
fun <T> processItems(items: List<T>) where T : CharSequence, T : Comparable<T> {
    val sorted = items.sorted()
    println("Sorted: $sorted")
}

fun main() {
    println(sumNumbers(10, 20))    // Output: 30.0
    println(sumNumbers(3.14, 2.5)) // Output: 5.64

    val strings = listOf("banana", "apple", "cherry")
    processItems(strings)  // Output: Sorted: [apple, banana, cherry]
}
```

---

### 2. Collection — List, Set, Map (Sesi 2-3)

#### 2.1 Overview Collection di Kotlin

Kotlin Standard Library menyediakan **tiga jenis collection** utama:

| **Collection** | **Deskripsi** | **Karakteristik** |
|---|---|---|
| **List** | Ordered collection | Elemen dapat diakses dengan index, boleh ada duplikat |
| **Set** | Unique elements | Tidak ada duplikat, unordered |
| **Map** | Key-Value pairs | Key unik, value bisa duplikat |

#### 2.2 Read-only vs Mutable Collection

Setiap collection memiliki dua versi:

| **Read-only** | **Mutable** |
|---|---|
| `List<T>` | `MutableList<T>` |
| `Set<T>` | `MutableSet<T>` |
| `Map<K, V>` | `MutableMap<K, V>` |

```kotlin
// Read-only List
val readOnlyList: List<String> = listOf("apple", "banana", "cherry")

// Mutable List
val mutableList: MutableList<String> = mutableListOf("apple", "banana", "cherry")
mutableList.add("durian")  // ✅ Bisa ditambah
// readOnlyList.add("durian")  // ❌ ERROR: Unresolved reference

// Read-only view dari mutable list
val lockedView: List<String> = mutableList
// lockedView.add("x")  // ❌ ERROR: Tidak bisa diubah melalui read-only view
```

#### 2.3 List — Ordered Collection

```kotlin
// Membuat List
val fruits = listOf("Apple", "Banana", "Cherry", "Apple")  // Boleh duplikat

// Mengakses elemen
println(fruits[0])        // Output: Apple
println(fruits.first())   // Output: Apple
println(fruits.last())    // Output: Apple
println(fruits.size)      // Output: 4

// Mutable List
val mutableFruits = mutableListOf("Apple", "Banana")
mutableFruits.add("Cherry")
mutableFruits.add(1, "Durian")
mutableFruits.remove("Apple")
println(mutableFruits)  // Output: [Durian, Banana, Cherry]
```

#### 2.4 Set — Unique Elements

```kotlin
// Membuat Set
val uniqueNumbers = setOf(1, 2, 3, 4, 5, 5, 5)  // Duplikat diabaikan
println(uniqueNumbers)  // Output: [1, 2, 3, 4, 5]

// Mengecek keanggotaan
println(3 in uniqueNumbers)   // Output: true
println(10 in uniqueNumbers)  // Output: false

// Mutable Set
val mutableSet = mutableSetOf("Java", "Kotlin", "Python")
mutableSet.add("Kotlin")  // Tidak efek karena sudah ada
mutableSet.add("Go")
println(mutableSet)  // Output: [Java, Kotlin, Python, Go]
```

#### 2.5 Map — Key-Value Pairs

```kotlin
// Membuat Map
val studentGrades = mapOf(
    "Alice" to 85,
    "Bob" to 92,
    "Charlie" to 78
)

// Mengakses value
println(studentGrades["Alice"])      // Output: 85
println(studentGrades.get("Bob"))    // Output: 92
println(studentGrades.getOrDefault("David", 0))  // Output: 0

// Iterasi Map
for ((name, grade) in studentGrades) {
    println("$name: $grade")
}

// Mutable Map
val mutableGrades = mutableMapOf("Alice" to 85)
mutableGrades["Bob"] = 92
mutableGrades.put("Charlie", 78)
mutableGrades["Alice"] = 90  // Update value
println(mutableGrades)  // Output: {Alice=90, Bob=92, Charlie=78}
```

#### 2.6 Collection Operations — Filter, Map, dan Lainnya

Kotlin menyediakan berbagai fungsi untuk memanipulasi collection.

**Filtering (Filter):**

```kotlin
val numbers = listOf(1, 2, 3, 4, 5, 6, 7, 8, 9, 10)

// filter — memfilter berdasarkan kondisi
val evenNumbers = numbers.filter { it % 2 == 0 }
println(evenNumbers)  // Output: [2, 4, 6, 8, 10]

// filterNot — kebalikan dari filter
val oddNumbers = numbers.filterNot { it % 2 == 0 }
println(oddNumbers)  // Output: [1, 3, 5, 7, 9]

// filter dengan index
val filteredByIndex = numbers.filterIndexed { index, value ->
    index % 2 == 0 && value > 5
}
println(filteredByIndex)  // Output: [7, 9]
```

**Mapping (Map):**

```kotlin
val numbers = listOf(1, 2, 3, 4, 5)

// map — transformasi setiap elemen
val doubled = numbers.map { it * 2 }
println(doubled)  // Output: [2, 4, 6, 8, 10]

// map dengan index
val withIndex = numbers.mapIndexed { index, value ->
    "Index $index: $value"
}
println(withIndex)  // Output: [Index 0: 1, Index 1: 2, ...]

// mapNotNull — filter null hasil transformasi
val mixed = listOf(1, 2, 3, 4, 5)
val transformed = mixed.mapNotNull { if (it % 2 == 0) it * 2 else null }
println(transformed)  // Output: [4, 8]
```

**Lainnya:**

```kotlin
val numbers = listOf(5, 2, 8, 1, 9, 3)

// sorted — sorting ascending
println(numbers.sorted())  // Output: [1, 2, 3, 5, 8, 9]

// sortedDescending — sorting descending
println(numbers.sortedDescending())  // Output: [9, 8, 5, 3, 2, 1]

// forEach — iterasi setiap elemen
numbers.forEach { println("Number: $it") }

// reduce — agregasi
val sum = numbers.reduce { acc, value -> acc + value }
println(sum)  // Output: 28

// fold — agregasi dengan initial value
val sumWithInitial = numbers.fold(10) { acc, value -> acc + value }
println(sumWithInitial)  // Output: 38

// any — apakah ada elemen yang memenuhi kondisi
println(numbers.any { it > 5 })   // Output: true
println(numbers.all { it > 0 })   // Output: true
println(numbers.none { it > 10 }) // Output: true

// find — mencari elemen pertama yang memenuhi kondisi
println(numbers.find { it > 5 })  // Output: 8
```

#### 2.7 Filter dengan Map

```kotlin
val grades = mapOf(
    "Alice" to 85,
    "Bob" to 92,
    "Charlie" to 78,
    "David" to 65
)

// Filter Map berdasarkan key
val aNames = grades.filter { it.key.startsWith("A") }
println(aNames)  // Output: {Alice=85}

// Filter Map berdasarkan value
val highGrades = grades.filter { it.value >= 80 }
println(highGrades)  // Output: {Alice=85, Bob=92}

// Transformasi Map
val updatedGrades = grades.mapValues { it.value + 5 }
println(updatedGrades)  // Output: {Alice=90, Bob=97, Charlie=83, David=70}
```

---

### 3. Exception Handling (Sesi 3-4)

#### 3.1 Apa itu Exception?

**Exception** adalah event yang mengganggu aliran normal program. Di Kotlin, semua exception adalah subclass dari `Throwable`.

> **Definisi Sederhana:** Exception adalah "kesalahan" yang terjadi saat program berjalan, seperti pembagian dengan nol atau file tidak ditemukan.

#### 3.2 Checked vs Unchecked Exception

| **Java** | **Kotlin** |
|---|---|
| Ada Checked Exception (harus ditangani) | **Tidak ada** Checked Exception |
| Compiler memaksa penanganan | Compiler **tidak** memaksa penanganan |

> **Keuntungan:** Kotlin tidak memiliki checked exception sehingga kode lebih bersih dan tidak perlu try-catch untuk setiap operasi yang berpotensi error.

#### 3.3 Try-Catch-Finally

**try-catch-finally** adalah struktur dasar untuk menangani exception.

```kotlin
// Basic Try-Catch
fun basicTryCatch() {
    try {
        val num = "abc".toInt()  // Akan throw NumberFormatException
    } catch (e: NumberFormatException) {
        println("Cannot convert to number: ${e.message}")
    }
}
```

**Multiple Catch Blocks:**

```kotlin
fun multipleCatch() {
    try {
        val fileContent = File("data.txt").readText()
        val numbers = fileContent.split(",").map { it.toInt() }
        val result = numbers[0] / numbers[1]
        println("Result: $result")
    } catch (e: java.io.FileNotFoundException) {
        println("Error: File not found")
    } catch (e: ArithmeticException) {
        println("Error: Division by zero")
    } catch (e: Exception) {
        println("Error: Unexpected exception: ${e.message}")
    }
}
```

**Finally Block:**

`finally` block **selalu** dieksekusi, baik terjadi exception atau tidak.

```kotlin
fun withFinally() {
    val file = File("nonexistent.txt")
    try {
        val contents = file.readText()
        println(contents)
    } catch (e: Exception) {
        println("Error reading file: ${e.message}")
    } finally {
        println("Cleanup operations complete")  // Selalu dieksekusi
    }
}
```

#### 3.4 Try sebagai Expression

Di Kotlin, **try adalah expression** — bisa mengembalikan nilai.

```kotlin
fun parseNumber(str: String): Int? {
    return try {
        str.toInt()  // Jika berhasil, return nilai ini
    } catch (e: NumberFormatException) {
        null         // Jika gagal, return null
    }
}

fun main() {
    val num1 = parseNumber("123")
    val num2 = parseNumber("abc")

    println(num1)  // Output: 123
    println(num2)  // Output: null
}
```

#### 3.5 Throw Expression dan Nothing Type

`throw` adalah expression di Kotlin dan memiliki tipe **Nothing** — tipe yang tidak memiliki nilai.

```kotlin
// throw sebagai expression
fun validateAge(age: Int): Int {
    return if (age >= 0) age else throw IllegalArgumentException("Age cannot be negative")
}

// throw dengan Elvis operator
fun getUsername(user: User?): String {
    return user?.name ?: throw IllegalArgumentException("User is null")
}

// Fungsi yang mengembalikan Nothing
fun fail(message: String): Nothing {
    throw IllegalArgumentException(message)
}

fun main() {
    val name = "Budi" ?: fail("Name is null")
    // Compiler tahu bahwa setelah fail(), kode tidak akan dieksekusi
    println(name)
}
```

#### 3.6 runCatching — Pendekatan Modern

`runCatching` adalah fungsi bawaan Kotlin untuk exception handling yang lebih fungsional.

```kotlin
// runCatching — mengembalikan Result<T>
fun parseWithRunCatching(str: String): Result<Int> {
    return runCatching {
        str.toInt()
    }
}

fun main() {
    val result1 = parseWithRunCatching("123")
    val result2 = parseWithRunCatching("abc")

    // onSuccess — jika berhasil
    result1.onSuccess { value ->
        println("Success: $value")
    }

    // onFailure — jika gagal
    result2.onFailure { exception ->
        println("Failed: ${exception.message}")
    }

    // getOrElse — dapatkan nilai atau default
    val value1 = result1.getOrElse { 0 }
    val value2 = result2.getOrElse { 0 }
    println(value1)  // Output: 123
    println(value2)  // Output: 0

    // getOrNull — dapatkan nilai atau null
    val value3 = result1.getOrNull()
    val value4 = result2.getOrNull()
    println(value3)  // Output: 123
    println(value4)  // Output: null

    // fold — handle success dan failure
    val message = result1.fold(
        onSuccess = { "Success: $it" },
        onFailure = { "Error: ${it.message}" }
    )
    println(message)  // Output: Success: 123
}
```

#### 3.7 Custom Exception

```kotlin
// Membuat custom exception
class InvalidInputException(message: String) : Exception(message)

class InsufficientBalanceException(balance: Double, requested: Double) :
    Exception("Insufficient balance: balance=$balance, requested=$requested")

// Menggunakan custom exception
class BankAccount(private var balance: Double) {
    fun withdraw(amount: Double) {
        if (amount <= 0) {
            throw InvalidInputException("Amount must be positive")
        }
        if (amount > balance) {
            throw InsufficientBalanceException(balance, amount)
        }
        balance -= amount
        println("Withdrawal successful. New balance: $balance")
    }
}

fun main() {
    val account = BankAccount(1000.0)

    try {
        account.withdraw(500.0)   // ✅ Berhasil
        account.withdraw(600.0)   // ❌ InsufficientBalanceException
    } catch (e: InsufficientBalanceException) {
        println("Error: ${e.message}")
    } catch (e: InvalidInputException) {
        println("Error: ${e.message}")
    }
}
```

---

## D. RINCIAN KEGIATAN PEMBELAJARAN (8 JAM)

### Sesi 1: Generic — Type Safety dan Reusability (2 Jam — 120 menit)

| **Waktu** | **Kegiatan** | **Detail** | **Metode** |
|---|---|---|---|
| **0-10'** | Pembukaan & Review | • Dosen membuka perkuliahan dengan salam dan doa<br>• Review singkat materi pertemuan 6 (Data Class, Object Declaration, Companion Object)<br>• Menghubungkan dengan topik pertemuan 7: "Bagaimana membuat kode yang reusable dan type-safe?" | Ceramah interaktif, Tanya jawab |
| **10-35'** | Konsep Generic | • **Definisi Generic** — type parameter untuk reusability dan type safety<br>• **Manfaat Generic**: type safety, reusability, readability, eliminasi casting<br>• **Perbedaan** dengan tanpa Generic (casting manual)<br>• **Generic Class** — `class Box<T>`<br>• **Generic Interface** — `interface Comparator<T>`<br>• **Generic Function** — `fun <T> printList(list: List<T>)` | Ceramah, Demonstrasi, Diskusi |
| **35-60'** | Generic Constraints | • **Generic Constraints** — membatasi tipe parameter<br>• **Single constraint** — `T : Number`<br>• **Multiple constraints** — `where T : CharSequence, T : Comparable<T>`<br>• **Demo**: Generic class `Box<T>` dengan berbagai tipe<br>• **Demo**: Generic function `sumNumbers` dengan constraint Number<br>• **Demo**: Multiple constraints dengan `where` clause | Ceramah, Demonstrasi, Live Coding |
| **60-85'** | Praktik Generic | • Mahasiswa membuat Generic Class `Storage<T>` dengan method `add()`, `get()`, `remove()`<br>• Membuat Generic Interface `Transformer<T>` dengan method `transform(input: T): T`<br>• Membuat Generic Function `swap(a: T, b: T): Pair<T, T>`<br>• Menggunakan Generic Constraints untuk membuat fungsi `maxOf` | Praktik mandiri, Asistensi |
| **85-120'** | Diskusi & Review | • Diskusi: "Kapan sebaiknya menggunakan Generic?"<br>• Studi kasus: implementasi Generic untuk data cache<br>• Q&A | Diskusi, Tanya jawab |

---

### Sesi 2: Collection — List, Set, Map (2 Jam — 120 menit)

| **Waktu** | **Kegiatan** | **Detail** | **Metode** |
|---|---|---|---|
| **0-10'** | Review & Motivasi | • Review Generic<br>• "Bagaimana mengelola kumpulan data secara efisien?" | Ceramah |
| **10-35'** | Overview Collection | • **Tiga jenis collection**: List, Set, Map<br>• **Read-only vs Mutable**: `List<T>` vs `MutableList<T>`<br>• **List** — ordered, boleh duplikat<br>• **Set** — unique, unordered<br>• **Map** — key-value pairs, key unik<br>• Fungsi pembuatan: `listOf()`, `mutableListOf()`, `setOf()`, `mapOf()` | Ceramah, Demonstrasi |
| **35-65'** | Praktik List & Set | • Mahasiswa membuat List dan MutableList<br>• Menambahkan, menghapus, mengakses elemen<br>• Membuat Set dan MutableSet<br>• Mengecek keanggotaan dengan `in` operator<br>• Memahami perbedaan List vs Set | Praktik mandiri, Asistensi |
| **65-90'** | Praktik Map | • Mahasiswa membuat Map dan MutableMap<br>• Menambahkan, mengupdate, menghapus key-value<br>• Mengakses value dengan `get()` dan `getOrDefault()`<br>• Iterasi Map dengan destructuring `for ((key, value) in map)`<br>• Memahami perbedaan Map vs List | Praktik mandiri, Asistensi |
| **90-120'** | Diskusi & Review | • Diskusi: "Kapan menggunakan List, Set, atau Map?"<br>• Studi kasus: implementasi sistem manajemen data dengan collection<br>• Q&A | Diskusi, Tanya jawab |

---

### Sesi 3: Collection Operations & Exception Handling Dasar (2 Jam — 120 menit)

| **Waktu** | **Kegiatan** | **Detail** | **Metode** |
|---|---|---|---|
| **0-10'** | Review & Motivasi | • Review List, Set, Map<br>• "Bagaimana memanipulasi data dalam collection secara efisien?" | Ceramah |
| **10-40'** | Collection Operations | • **Filtering**: `filter()`, `filterNot()`, `filterIndexed()`<br>• **Mapping**: `map()`, `mapIndexed()`, `mapNotNull()`<br>• **Sorting**: `sorted()`, `sortedDescending()`<br>• **Agregasi**: `reduce()`, `fold()`<br>• **Pengecekan**: `any()`, `all()`, `none()`<br>• **Pencarian**: `find()`, `first()`, `last()`<br>• **Demo**: Semua operasi dengan contoh | Ceramah, Demonstrasi, Live Coding |
| **40-70'** | Praktik Collection Operations | • Mahasiswa membuat list angka dan melakukan filter, map, sorting<br>• Membuat list objek dan melakukan operasi kompleks<br>• Menggunakan `forEach` untuk iterasi<br>• Menggunakan `reduce` dan `fold` untuk agregasi<br>• Filter dan transformasi Map | Praktik mandiri, Asistensi |
| **70-100'** | Exception Handling Dasar | • **Apa itu Exception** — event yang mengganggu aliran program<br>• **Checked vs Unchecked** — Kotlin tidak memiliki checked exception<br>• **try-catch-finally** — struktur dasar<br>• **Multiple catch blocks** — menangani berbagai jenis exception<br>• **finally block** — selalu dieksekusi<br>• **try sebagai expression** — mengembalikan nilai<br>• **throw expression** dan tipe `Nothing`<br>• **Demo**: Semua konsep exception handling | Ceramah, Demonstrasi, Live Coding |
| **100-120'** | Praktik Exception Handling | • Mahasiswa membuat program dengan try-catch untuk menangani NumberFormatException<br>• Menggunakan multiple catch blocks<br>• Menggunakan finally untuk cleanup<br>• Menggunakan try sebagai expression untuk parsing data<br>• Menggunakan throw dengan custom message | Praktik mandiri, Asistensi |

---

### Sesi 4: runCatching, Custom Exception & Studi Kasus Terintegrasi (2 Jam — 120 menit)

| **Waktu** | **Kegiatan** | **Detail** | **Metode** |
|---|---|---|---|
| **0-10'** | Review & Motivasi | • Review exception handling<br>• "Bagaimana pendekatan modern untuk exception handling?" | Ceramah |
| **10-35'** | runCatching & Custom Exception | • **runCatching** — pendekatan fungsional untuk exception handling<br>  - `onSuccess` dan `onFailure` callback<br>  - `getOrElse` dan `getOrNull`<br>  - `fold` untuk handle success dan failure<br>• **Custom Exception** — membuat exception sendiri<br>• **Perbandingan**: try-catch vs runCatching<br>• **Demo**: runCatching untuk parsing data<br>• **Demo**: Custom Exception `InvalidInputException` dan `InsufficientBalanceException` | Ceramah, Demonstrasi, Live Coding |
| **35-65'** | Praktik runCatching & Custom Exception | • Mahasiswa membuat program dengan runCatching<br>• Menggunakan onSuccess dan onFailure<br>• Menggunakan getOrElse dan getOrNull<br>• Membuat custom exception dan menggunakannya | Praktik mandiri, Asistensi |
| **65-90'** | Studi Kasus Terintegrasi | • Dosen menjelaskan studi kasus sistem manajemen data mahasiswa (lihat bagian E)<br>• Menggunakan Generic untuk `Repository<T>`<br>• Menggunakan Collection untuk menyimpan data<br>• Menggunakan Exception Handling untuk validasi<br>• **Live coding** bersama dosen | Demonstrasi, Live Coding, Diskusi |
| **90-105'** | Pengumpulan & Presentasi | • Mahasiswa mengumpulkan Tugas 7<br>• 2-3 mahasiswa diminta mempresentasikan kodenya<br>• Dosen memberikan feedback konstruktif | Presentasi, Feedback |
| **105-120'** | Penutupan | • Dosen merangkum pencapaian pertemuan 7<br>• Preview materi pertemuan 8 (UAS — Proyek Akhir & Review)<br>• Memberikan tugas membaca modul pertemuan 8<br>• Menutup perkuliahan dengan doa dan salam | Ceramah |

---

## E. TUGAS 7 (Dikumpulkan)

### Sistem Manajemen Data Mahasiswa dengan Generic, Collection, dan Exception Handling

Buatlah program lengkap sistem manajemen data mahasiswa dengan ketentuan berikut:

#### 1. Generic Class `Repository<T>`

| **Komponen** | **Spesifikasi** |
|---|---|
| **Properti** | `items: MutableList<T>` (private) |
| **Metode** | `add(item: T): Boolean` — menambah item<br>`remove(item: T): Boolean` — menghapus item<br>`find(predicate: (T) -> Boolean): T?` — mencari item<br>`findAll(predicate: (T) -> Boolean): List<T>` — mencari semua<br>`getAll(): List<T>` — mendapatkan semua item<br>`update(id: String, newItem: T): Boolean` — mengupdate item berdasarkan ID (gunakan reflection atau asumsi item memiliki property `id`) |

#### 2. Data Class `Student`

| **Komponen** | **Spesifikasi** |
|---|---|
| **Properti** | `id: String` (read-only)<br>`name: String` (read-only)<br>`major: String` (read-only)<br>`gpa: Double` (mutable) |

#### 3. Data Class `Course`

| **Komponen** | **Spesifikasi** |
|---|---|
| **Properti** | `id: String` (read-only)<br>`name: String` (read-only)<br>`credits: Int` (read-only)<br>`instructor: String` (read-only) |

#### 4. Data Class `Enrollment`

| **Komponen** | **Spesifikasi** |
|---|---|
| **Properti** | `studentId: String` (read-only)<br>`courseId: String` (read-only)<br>`grade: Double?` (mutable, nullable) |

#### 5. Custom Exception

Buatlah custom exception berikut:
- `DuplicateIdException` — ketika ID sudah ada
- `NotFoundException` — ketika data tidak ditemukan
- `InvalidGpaException` — ketika GPA tidak valid (0.0 - 4.0)
- `EnrollmentException` — ketika terjadi error dalam enrollment

#### 6. Object Declaration `DataManager`

| **Komponen** | **Spesifikasi** |
|---|---|
| **Properti** | `studentRepo: Repository<Student>`<br>`courseRepo: Repository<Course>`<br>`enrollmentRepo: Repository<Enrollment>` |
| **Metode** | `initData()` — inisialisasi data awal<br>`enrollStudent(studentId: String, courseId: String): Boolean` — enroll student ke course<br>`getStudentCourses(studentId: String): List<Course>` — mendapatkan course yang diambil student<br>`getCourseStudents(courseId: String): List<Student>` — mendapatkan student yang mengambil course<br>`calculateGPA(studentId: String): Double` — menghitung GPA student dari nilai course<br>`displayAllData()` — menampilkan semua data |

#### 7. Fungsi `main()`

- Inisialisasi data dengan `DataManager.initData()`
- Tampilkan semua student, course, dan enrollment
- Lakukan enroll student ke course
- Tampilkan course yang diambil oleh student tertentu
- Tampilkan student yang mengambil course tertentu
- Hitung dan tampilkan GPA student
- Gunakan **Generic** untuk `Repository<T>`
- Gunakan **Collection** (List, Set, Map) untuk menyimpan data
- Gunakan **Exception Handling** (try-catch, runCatching) untuk validasi

#### 8. Kriteria Penilaian Tugas 7

| **Kriteria** | **Bobot** | **Indikator** |
|---|---|---|
| **Generic** | 25% | • `Repository<T>` sebagai Generic Class<br>• Generic method digunakan dengan benar<br>• Type safety terjaga |
| **Collection** | 20% | • Menggunakan List, Set, Map dengan tepat<br>• Collection operations (filter, map, dll) digunakan |
| **Exception Handling** | 25% | • try-catch-finally digunakan dengan benar<br>• Custom exception dibuat dan digunakan<br>• runCatching digunakan sebagai alternatif |
| **Fungsi main()** | 15% | • Menampilkan semua skenario yang diminta<br>• Output jelas dan informatif |
| **Kode Berkualitas** | 15% | • Kode bersih, terstruktur, diberi komentar<br>• Menggunakan naming convention yang benar |

---

## F. MEDIA DAN ALAT PEMBELAJARAN

| **Media** | **Keterangan** |
|---|---|
| **Laptop/PC** | Setiap mahasiswa menggunakan laptop/PC masing-masing |
| **IntelliJ IDEA** | IDE utama untuk pengembangan Kotlin |
| **JDK** | Java Development Kit (versi 11 atau 17) |
| **Proyektor/LCD** | Untuk presentasi dan demonstrasi dosen |
| **Whiteboard** | Untuk menjelaskan konsep dan perbandingan |
| **Modul Praktikum** | Modul cetak/digital pertemuan 7 |
| **Kotlin Playground** | Alternatif untuk mencoba kode tanpa instalasi |

---

## G. PENILAIAN PERTEMUAN 7

| **Komponen** | **Bobot** | **Indikator** | **Teknik** |
|---|---|---|---|
| **Keaktifan Sesi 1-3** | 15% dari total keaktifan | • Kehadiran tepat waktu<br>• Partisipasi dalam diskusi dan tanya jawab<br>• Keterlibatan dalam praktik | Observasi |
| **Tugas 7** | 100% dari nilai tugas 7 | • Lihat kriteria penilaian Tugas 7 di atas | Penilaian kode |
| **Kuis Singkat** | Bonus | • Pertanyaan tentang Generic, Collection, Exception Handling | Tes tertulis/lisan |

---

## H. REFERENSI PERTEMUAN 7

### Referensi Utama:

1. **Kotlin Official Documentation – Collections Overview** — [https://kotlinlang.org/docs/collections-overview.html](https://kotlinlang.org/docs/collections-overview.html)

2. **Kotlin Official Documentation – Collections Tour** — [https://kotlinlang.org/docs/kotlin-tour-collections.html](https://kotlinlang.org/docs/kotlin-tour-collections.html)

3. **Kotlin Official Documentation – Exceptions** — [https://kotlinlang.org/docs/exceptions.html](https://kotlinlang.org/docs/exceptions.html)

### Referensi Pendukung:

4. **Kotlin Try/Catch/Finally Tutorial** — [https://zetcode.cn/kotlin/try-catch-finally-keywords/](https://zetcode.cn/kotlin/try-catch-finally-keywords/)

5. **Kotlin Generics Tutorial** — [http://m.yisu.com/ask/73303582.html](http://m.yisu.com/ask/73303582.html)

6. **runCatching vs try-catch** — Baeldung on Kotlin

---

## I. LAMPIRAN

### Lampiran 1: Perbandingan Collection Types

| **Aspek** | **List** | **Set** | **Map** |
|---|---|---|---|
| **Order** | Ordered (by index) | Unordered | Unordered (by key) |
| **Duplikat** | Boleh | Tidak boleh | Key tidak boleh, value boleh |
| **Akses** | By index (`list[0]`) | By value (`set.contains()`) | By key (`map["key"]`) |
| **Read-only** | `List<T>` | `Set<T>` | `Map<K, V>` |
| **Mutable** | `MutableList<T>` | `MutableSet<T>` | `MutableMap<K, V>` |
| **Contoh** | Daftar nama siswa | Nomor unik | Nilai siswa |

### Lampiran 2: Perbandingan Exception Handling Approaches

| **Aspek** | **try-catch-finally** | **runCatching** |
|---|---|---|
| **Pendekatan** | Imperatif | Fungsional |
| **Return type** | Tergantung blok try/catch | `Result<T>` |
| **Success handling** | Di blok try | `onSuccess { }` |
| **Failure handling** | Di blok catch | `onFailure { }` |
| **Default value** | Manual | `getOrElse { }` |
| **Cleanup** | `finally { }` | `finally` atau `onFailure` |

### Lampiran 3: Checklist Pemahaman Mahasiswa

| **No** | **Konsep** | **Paham** | **Kurang Paham** | **Tidak Paham** |
|---|---|---|---|---|
| 1 | Generic Class — `class Box<T>` | ☐ | ☐ | ☐ |
| 2 | Generic Interface — `interface Comparator<T>` | ☐ | ☐ | ☐ |
| 3 | Generic Function — `fun <T> printList()` | ☐ | ☐ | ☐ |
| 4 | Generic Constraints — `T : Number` | ☐ | ☐ | ☐ |
| 5 | List — ordered, boleh duplikat | ☐ | ☐ | ☐ |
| 6 | Set — unique, unordered | ☐ | ☐ | ☐ |
| 7 | Map — key-value pairs | ☐ | ☐ | ☐ |
| 8 | Read-only vs Mutable collection | ☐ | ☐ | ☐ |
| 9 | Collection Operations — filter, map | ☐ | ☐ | ☐ |
| 10 | try-catch-finally | ☐ | ☐ | ☐ |
| 11 | try sebagai expression | ☐ | ☐ | ☐ |
| 12 | throw dan Nothing type | ☐ | ☐ | ☐ |
| 13 | runCatching dan Result | ☐ | ☐ | ☐ |
| 14 | Custom Exception | ☐ | ☐ | ☐ |

---

**Disusun oleh,**
[Nama Dosen Pengampu]
Dosen Program Studi D4 Teknologi Rekayasa Informatika Industri
