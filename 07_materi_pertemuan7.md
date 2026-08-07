# MATERI AJAR PERTEMUAN 7
## PEMROGRAMAN BERORIENTASI OBJEK (OOP) DENGAN KOTLIN
### “Generic, Collection & Exception Handling — Memanipulasi Data dan Mengelola Error”

---

# BAGIAN 1: GENERIC — TYPE SAFETY DAN REUSABILITY

## 1.1 Apa itu Generic?

**Generic** adalah fitur yang memungkinkan Anda menulis kode yang **type-safe** dan **reusable** dengan menggunakan **type parameters** (parameter tipe). Generic memungkinkan kelas, interface, dan fungsi beroperasi pada tipe yang ditentukan saat penggunaan, bukan saat definisi.

> **Definisi Sederhana:** Generic adalah "cetakan kode" yang bisa bekerja dengan berbagai tipe data tanpa harus menulis ulang kode untuk setiap tipe.

## 1.2 Mengapa Generic Penting?

| **Manfaat** | **Penjelasan** |
|---|---|
| **Type Safety** | Kompiler memeriksa tipe data, mencegah error runtime |
| **Reusability** | Satu kode bisa digunakan untuk berbagai tipe data |
| **Readability** | Kode lebih bersih dan mudah dipahami |
| **Eliminasi Casting** | Tidak perlu melakukan casting secara manual |

---

## 1.3 Generic Class

Generic class didefinisikan dengan menempatkan **type parameter** di dalam tanda `<>` setelah nama kelas.

```kotlin
// Definisi Generic Class
class Box<T>(private var content: T) {
    fun getContent(): T = content
    fun setContent(newContent: T) {
        content = newContent
    }
}

fun main() {
    // Penggunaan Generic Class — dengan type arguments eksplisit
    val intBox: Box<Int> = Box<Int>(42)
    val strBox: Box<String> = Box<String>("Hello")

    // Type arguments dapat di-infer oleh compiler
    val inferredBox = Box(3.14)  // Compiler menginfer Box<Double>

    println(intBox.getContent())  // Output: 42
    println(strBox.getContent())  // Output: Hello
    println(inferredBox.getContent())  // Output: 3.14
}
```

### Generic Class dengan Multiple Type Parameters

```kotlin
// Generic class dengan dua type parameters
class Pair<K, V>(val key: K, val value: V) {
    override fun toString(): String = "($key, $value)"
}

fun main() {
    val pair1 = Pair("Name", "Budi")
    val pair2 = Pair(1, "Item")

    println(pair1)  // Output: (Name, Budi)
    println(pair2)  // Output: (1, Item)
}
```

---

## 1.4 Generic Interface

Generic interface didefinisikan dengan cara yang sama — type parameter ditempatkan setelah nama interface.

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
    println(strComp.compare("apple", "banana"))  // Output: -1 (apple < banana)
}
```

---

## 1.5 Generic Function

Generic function didefinisikan dengan menempatkan type parameter **sebelum nama fungsi**.

```kotlin
// Generic Function
fun <T> printList(items: List<T>) {
    for (item in items) {
        println(item)
    }
}

fun <T> singletonList(item: T): List<T> {
    return listOf(item)
}

// Generic Extension Function
fun <T> T.basicToString(): String {
    return "Item: $this"
}

fun main() {
    // Type arguments dapat di-infer dari context
    val numbers = listOf(1, 2, 3, 4, 5)
    printList(numbers)  // Output: 1 2 3 4 5

    val strings = listOf("apple", "banana", "cherry")
    printList(strings)  // Output: apple banana cherry

    val single = singletonList("Hello")
    println(single)  // Output: [Hello]

    println(42.basicToString())  // Output: Item: 42
    println("Kotlin".basicToString())  // Output: Item: Kotlin
}
```

---

## 1.6 Generic Constraints — Batasan Tipe

Generic constraints membatasi tipe yang dapat digunakan sebagai type arguments.

### Upper Bound (Batasan Atas)

Upper bound adalah batasan yang paling umum, setara dengan `extends` di Java.

```kotlin
// Generic dengan constraint: T harus merupakan subclass dari Number
fun <T : Number> sumNumbers(a: T, b: T): Double {
    return a.toDouble() + b.toDouble()
}

// Generic dengan constraint: T harus mengimplementasikan Comparable
fun <T : Comparable<T>> findMax(a: T, b: T): T {
    return if (a > b) a else b
}

fun main() {
    println(sumNumbers(10, 20))    // Output: 30.0
    println(sumNumbers(3.14, 2.5)) // Output: 5.64

    println(findMax(10, 20))       // Output: 20
    println(findMax("apple", "banana"))  // Output: banana (karena 'b' > 'a')
}
```

### Multiple Constraints dengan `where` Clause

Jika satu type parameter membutuhkan lebih dari satu upper bound, gunakan **`where` clause**.

```kotlin
// Multiple constraints dengan where clause
fun <T> processItems(items: List<T>) where T : CharSequence, T : Comparable<T> {
    val sorted = items.sorted()
    println("Sorted: $sorted")
    println("First: ${sorted.firstOrNull()}")
    println("Last: ${sorted.lastOrNull()}")
}

// Contoh lain: multiple constraints
fun <T> copyWhenGreater(list: List<T>, threshold: T): List<String>
        where T : CharSequence, T : Comparable<T> {
    return list.filter { it > threshold }.map { it.toString() }
}

fun main() {
    val strings = listOf("banana", "apple", "cherry", "date")
    processItems(strings)
    // Output: Sorted: [apple, banana, cherry, date]
    //         First: apple
    //         Last: date

    val result = copyWhenGreater(strings, "cherry")
    println(result)  // Output: [date]
}
```

### Default Upper Bound

Jika tidak ada constraint yang ditentukan, default upper bound adalah `Any?`.

```kotlin
// Tanpa constraint — T bisa berupa tipe apa saja (termasuk null)
fun <T> printItem(item: T) {
    println(item)
}

// T dengan upper bound Any (tidak nullable)
fun <T : Any> printNonNullItem(item: T) {
    println(item)
}

fun main() {
    printItem("Hello")     // OK
    printItem(null)        // OK — T adalah Any?

    printNonNullItem("Hello")  // OK
    // printNonNullItem(null)  // ERROR — T tidak bisa nullable
}
```

---

## 1.7 Type Erasure

Kotlin melakukan **type erasure** pada generic — informasi tipe dihapus saat runtime.

```kotlin
// Type erasure — informasi tipe tidak tersedia saat runtime
fun main() {
    val list1: List<String> = listOf("a", "b", "c")
    val list2: List<Int> = listOf(1, 2, 3)

    // ❌ ERROR: Cannot check for instance of erased type
    // if (list1 is List<String>) { ... }

    // ✅ Bisa menggunakan star projection
    if (list1 is List<*>) {
        println("list1 is a List")
    }
}
```

---

# BAGIAN 2: COLLECTION — LIST, SET, MAP

## 2.1 Overview Collection di Kotlin

Kotlin Standard Library menyediakan **tiga jenis collection** utama untuk mengelompokkan data:

| **Collection** | **Deskripsi** | **Karakteristik** |
|---|---|---|
| **List** | Ordered collection | Elemen dapat diakses dengan index, boleh ada duplikat |
| **Set** | Unique elements | Tidak ada duplikat, unordered |
| **Map** | Key-Value pairs | Key unik, value bisa duplikat |

## 2.2 Read-only vs Mutable Collection

Setiap collection memiliki dua versi — **read-only** dan **mutable**:

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
// readOnlyList.add("durian")  // ❌ ERROR

// Read-only view dari mutable list
val lockedView: List<String> = mutableList
// lockedView.add("x")  // ❌ ERROR: Tidak bisa diubah melalui read-only view

// Mencegah unwanted modifications dengan read-only view
val shapes: MutableList<String> = mutableListOf("triangle", "square", "circle")
val shapesLocked: List<String> = shapes  // Read-only view
```

---

## 2.3 List — Ordered Collection

List menyimpan elemen dalam urutan sesuai penambahan dan mengizinkan duplikat.

### Membuat List

```kotlin
// Read-only List
val fruits = listOf("Apple", "Banana", "Cherry", "Apple")  // Boleh duplikat

// Mutable List
val mutableFruits = mutableListOf("Apple", "Banana")

// List dengan tipe eksplisit
val shapes: List<String> = listOf("triangle", "square", "circle")
```

### Mengakses Elemen List

```kotlin
val fruits = listOf("Apple", "Banana", "Cherry")

// Indexed access operator
println(fruits[0])        // Output: Apple
println(fruits[1])        // Output: Banana

// First and last items
println(fruits.first())   // Output: Apple
println(fruits.last())    // Output: Cherry

// Size
println(fruits.size)      // Output: 3
```

### Operasi Mutable List

```kotlin
val mutableFruits = mutableListOf("Apple", "Banana")

// Menambah elemen
mutableFruits.add("Cherry")
mutableFruits.add(1, "Durian")  // Tambah di index 1

// Menghapus elemen
mutableFruits.remove("Apple")
mutableFruits.removeAt(0)

// Mengupdate elemen
mutableFruits[0] = "Mango"

println(mutableFruits)  // Output: [Mango, Cherry]
```

---

## 2.4 Set — Unique Elements

Set menyimpan elemen unik (tidak ada duplikat) dan tidak memiliki urutan tertentu.

### Membuat Set

```kotlin
// Read-only Set
val uniqueNumbers = setOf(1, 2, 3, 4, 5, 5, 5)  // Duplikat diabaikan
println(uniqueNumbers)  // Output: [1, 2, 3, 4, 5]

// Mutable Set
val mutableSet = mutableSetOf("Java", "Kotlin", "Python")
```

### Operasi Set

```kotlin
val numbers = setOf(1, 2, 3, 4, 5)

// Mengecek keanggotaan
println(3 in numbers)   // Output: true
println(10 in numbers)  // Output: false

// Mutable Set operations
val mutableSet = mutableSetOf("Java", "Kotlin", "Python")
mutableSet.add("Kotlin")  // Tidak efek karena sudah ada
mutableSet.add("Go")
mutableSet.remove("Java")

println(mutableSet)  // Output: [Kotlin, Python, Go]
```

---

## 2.5 Map — Key-Value Pairs

Map menyimpan pasangan key-value, di mana setiap key unik dan memetakan ke satu value.

### Membuat Map

```kotlin
// Read-only Map — menggunakan infix function `to`
val studentGrades = mapOf(
    "Alice" to 85,
    "Bob" to 92,
    "Charlie" to 78
)

// Mutable Map dengan apply
val mutableGrades = mutableMapOf<String, Int>().apply {
    this["Alice"] = 85
    this["Bob"] = 92
}

// Atau langsung
val mutableGrades2 = mutableMapOf("Alice" to 85, "Bob" to 92)
```

### Mengakses Value di Map

```kotlin
val grades = mapOf("Alice" to 85, "Bob" to 92, "Charlie" to 78)

// Mengakses value
println(grades["Alice"])      // Output: 85
println(grades.get("Bob"))    // Output: 92
println(grades.getOrDefault("David", 0))  // Output: 0

// Mengecek key
println("Alice" in grades)   // Output: true
println("David" in grades)   // Output: false
```

### Iterasi Map

```kotlin
val grades = mapOf("Alice" to 85, "Bob" to 92, "Charlie" to 78)

// Destructuring dalam loop
for ((name, grade) in grades) {
    println("$name: $grade")
}
// Output:
// Alice: 85
// Bob: 92
// Charlie: 78

// Iterasi keys
for (name in grades.keys) {
    println(name)
}

// Iterasi values
for (grade in grades.values) {
    println(grade)
}
```

### Operasi Mutable Map

```kotlin
val mutableGrades = mutableMapOf("Alice" to 85)

// Menambah / mengupdate
mutableGrades["Bob"] = 92
mutableGrades.put("Charlie", 78)
mutableGrades["Alice"] = 90  // Update value

// Menghapus
mutableGrades.remove("Charlie")

println(mutableGrades)  // Output: {Alice=90, Bob=92}
```

---

## 2.6 Collection Operations — Filter, Map, dan Lainnya

Kotlin menyediakan berbagai fungsi untuk memanipulasi collection.

### Filtering (Filter)

`filter()` mengembalikan elemen yang memenuhi predicate (kondisi).

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

// Filter untuk Map
val grades = mapOf("Alice" to 85, "Bob" to 92, "Charlie" to 78)
val highGrades = grades.filter { it.value >= 80 }
println(highGrades)  // Output: {Alice=85, Bob=92}
```

### Mapping (Map)

`map()` mentransformasi setiap elemen menjadi bentuk lain.

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
val transformed = mixed.mapNotNull {
    if (it % 2 == 0) it * 2 else null
}
println(transformed)  // Output: [4, 8]

// Transformasi Map
val updatedGrades = grades.mapValues { it.value + 5 }
println(updatedGrades)  // Output: {Alice=90, Bob=97, Charlie=83, David=70}
```

### Sorting

```kotlin
val numbers = listOf(5, 2, 8, 1, 9, 3)

// sorted — sorting ascending
println(numbers.sorted())  // Output: [1, 2, 3, 5, 8, 9]

// sortedDescending — sorting descending
println(numbers.sortedDescending())  // Output: [9, 8, 5, 3, 2, 1]
```

### Iterasi dan Agregasi

```kotlin
val numbers = listOf(1, 2, 3, 4, 5)

// forEach — iterasi setiap elemen
numbers.forEach { println("Number: $it") }

// reduce — agregasi tanpa initial value
val sum = numbers.reduce { acc, value -> acc + value }
println(sum)  // Output: 15

// fold — agregasi dengan initial value
val sumWithInitial = numbers.fold(10) { acc, value -> acc + value }
println(sumWithInitial)  // Output: 25
```

### Pengecekan dan Pencarian

```kotlin
val numbers = listOf(1, 2, 3, 4, 5, 6, 7, 8, 9, 10)

// any — apakah ada elemen yang memenuhi kondisi
println(numbers.any { it > 5 })   // Output: true
println(numbers.all { it > 0 })   // Output: true
println(numbers.none { it > 10 }) // Output: true

// find — mencari elemen pertama yang memenuhi kondisi
println(numbers.find { it > 5 })  // Output: 8

// first / last — dengan kondisi
println(numbers.first { it > 5 })  // Output: 6
println(numbers.last { it < 5 })   // Output: 4
```

---

# BAGIAN 3: EXCEPTION HANDLING

## 3.1 Apa itu Exception?

**Exception** adalah event yang mengganggu aliran normal program. Di Kotlin, semua exception adalah subclass dari `Exception`, yang merupakan subclass dari `Throwable`.

## 3.2 Checked vs Unchecked Exception

Kotlin **treats all exceptions as unchecked by default**.

| **Java** | **Kotlin** |
|---|---|
| Ada Checked Exception (harus ditangani) | **Tidak ada** Checked Exception |
| Compiler memaksa penanganan | Compiler **tidak** memaksa penanganan |

> **Keuntungan:** Kotlin tidak memiliki checked exception sehingga kode lebih bersih dan tidak perlu try-catch untuk setiap operasi yang berpotensi error.

## 3.3 Try-Catch-Finally

**try-catch-finally** adalah struktur dasar untuk menangani exception.

### Basic Try-Catch

```kotlin
fun basicTryCatch() {
    try {
        val num = "abc".toInt()  // Akan throw NumberFormatException
    } catch (e: NumberFormatException) {
        println("Cannot convert to number: ${e.message}")
    }
}
```

### Multiple Catch Blocks

```kotlin
fun multipleCatch() {
    try {
        val fileContent = java.io.File("data.txt").readText()
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

### Finally Block

`finally` block **selalu** dieksekusi, baik terjadi exception atau tidak.

```kotlin
fun withFinally() {
    val file = java.io.File("nonexistent.txt")
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

---

## 3.4 Try sebagai Expression

Di Kotlin, **try adalah expression** — bisa mengembalikan nilai.

```kotlin
fun parseNumber(str: String): Int? {
    return try {
        str.toInt()  // Jika berhasil, return nilai ini
    } catch (e: NumberFormatException) {
        null         // Jika gagal, return null
    }
}

fun parseNumberWithDefault(str: String, defaultValue: Int): Int {
    return try {
        str.toInt()
    } catch (e: NumberFormatException) {
        defaultValue
    }
}

fun main() {
    val num1 = parseNumber("123")
    val num2 = parseNumber("abc")

    println(num1)  // Output: 123
    println(num2)  // Output: null

    val num3 = parseNumberWithDefault("xyz", 0)
    println(num3)  // Output: 0
}
```

---

## 3.5 Throw Expression dan Nothing Type

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

---

## 3.6 runCatching — Pendekatan Modern

`runCatching` adalah fungsi bawaan Kotlin untuk exception handling yang lebih fungsional.

### Dasar runCatching

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

### runCatching dengan Custom Logic

```kotlin
fun processData(input: String): String {
    return runCatching {
        // Kode yang mungkin throw exception
        val number = input.toInt()
        val result = 100 / number
        "Result: $result"
    }.onSuccess {
        println("✅ Processing successful")
    }.onFailure { exception ->
        println("❌ Processing failed: ${exception.message}")
    }.getOrElse {
        "Fallback value"
    }
}

fun main() {
    println(processData("10"))   // Output: ✅ Processing successful \n Result: 10
    println(processData("0"))    // Output: ❌ Processing failed: / by zero \n Fallback value
    println(processData("abc"))  // Output: ❌ Processing failed: For input string: "abc" \n Fallback value
}
```

### runCatching vs try-catch-finally

Perbedaan penting: `runCatching` menangkap dan mengonsumsi exception, sedangkan `try-finally` melempar exception.

```kotlin
// try-finally — exception tetap di-propagasi
fun tryFinallyExample() {
    try {
        throw RuntimeException("Error!")
    } finally {
        println("Cleanup in finally")
    }
    // Exception tetap dilempar ke caller
}

// runCatching — exception ditangkap dan tidak di-propagasi
fun runCatchingExample() {
    runCatching {
        throw RuntimeException("Error!")
    }.onFailure {
        println("Caught: ${it.message}")
    }
    // Exception TIDAK di-propagasi ke caller
    println("Program continues normally")
}
```

---

## 3.7 Custom Exception

Karena `Exception` adalah `open class`, Anda dapat membuat custom exception.

### Custom Exception Sederhana

```kotlin
// Custom exception sederhana
class InvalidEmailException(message: String) : Exception(message)

// Custom exception dengan multiple parameters
class InsufficientBalanceException(balance: Double, requested: Double) :
    Exception("Insufficient balance: balance=$balance, requested=$requested")
```

### Penggunaan Custom Exception

```kotlin
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

class InvalidInputException(message: String) : Exception(message)

class InsufficientBalanceException(balance: Double, requested: Double) :
    Exception("Insufficient balance: balance=$balance, requested=$requested")

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

### Custom Exception dengan Cause

```kotlin
class DataProcessingException(message: String, cause: Throwable? = null) :
    Exception(message, cause)

fun processData(data: String) {
    try {
        val number = data.toInt()
        if (number < 0) {
            throw IllegalArgumentException("Number cannot be negative")
        }
    } catch (e: NumberFormatException) {
        throw DataProcessingException("Failed to parse data: $data", e)
    } catch (e: IllegalArgumentException) {
        throw DataProcessingException("Invalid data: ${e.message}", e)
    }
}

fun main() {
    try {
        processData("abc")
    } catch (e: DataProcessingException) {
        println("Error: ${e.message}")
        println("Cause: ${e.cause}")
    }
}
```

---

# BAGIAN 4: STUDI KASUS — SISTEM MANAJEMEN DATA MAHASISWA

## 4.1 Analisis Kebutuhan

| **Komponen** | **Konsep yang Digunakan** | **Tujuan** |
|---|---|---|
| **Repository<T>** | Generic Class | Menyimpan dan mengelola data berbagai tipe |
| **Student** | Data Class | Menyimpan data mahasiswa |
| **Course** | Data Class | Menyimpan data mata kuliah |
| **Enrollment** | Data Class | Menyimpan data pendaftaran |
| **DataManager** | Object Declaration | Singleton untuk mengelola semua data |
| **Custom Exception** | Exception Handling | Menangani error spesifik |

## 4.2 Implementasi Lengkap

```kotlin
/**
 * ============================================================
 * SISTEM MANAJEMEN DATA MAHASISWA
 * DENGAN GENERIC, COLLECTION, DAN EXCEPTION HANDLING
 * ============================================================
 * Demonstrasi:
 * 1. Generic Class Repository<T>
 * 2. Collection (List, Map) untuk menyimpan data
 * 3. Custom Exception untuk error handling
 * 4. runCatching untuk exception handling modern
 * ============================================================
 */

// ============================================================
// CUSTOM EXCEPTIONS
// ============================================================

class DuplicateIdException(id: String) :
    Exception("Duplicate ID: $id already exists")

class NotFoundException(id: String) :
    Exception("Item with ID $id not found")

class InvalidGpaException(gpa: Double) :
    Exception("Invalid GPA: $gpa (must be between 0.0 and 4.0)")

class EnrollmentException(message: String) : Exception(message)

// ============================================================
// GENERIC CLASS: Repository<T>
// ============================================================

class Repository<T : Any> {
    private val items = mutableListOf<T>()

    fun add(item: T): Boolean {
        return try {
            items.add(item)
            true
        } catch (e: Exception) {
            println("❌ Failed to add item: ${e.message}")
            false
        }
    }

    fun remove(item: T): Boolean {
        return items.remove(item)
    }

    fun find(predicate: (T) -> Boolean): T? {
        return items.find(predicate)
    }

    fun findAll(predicate: (T) -> Boolean): List<T> {
        return items.filter(predicate)
    }

    fun getAll(): List<T> {
        return items.toList()
    }

    fun update(id: String, newItem: T): Boolean where T : Identifiable {
        val index = items.indexOfFirst { it.id == id }
        return if (index >= 0) {
            items[index] = newItem
            true
        } else {
            false
        }
    }

    fun findById(id: String): T? where T : Identifiable {
        return items.find { it.id == id }
    }

    fun size(): Int = items.size

    fun clear() = items.clear()
}

// ============================================================
// INTERFACE: Identifiable
// ============================================================

interface Identifiable {
    val id: String
}

// ============================================================
// DATA CLASSES
// ============================================================

data class Student(
    override val id: String,
    val name: String,
    val major: String,
    var gpa: Double
) : Identifiable {
    init {
        if (gpa < 0.0 || gpa > 4.0) {
            throw InvalidGpaException(gpa)
        }
    }
}

data class Course(
    override val id: String,
    val name: String,
    val credits: Int,
    val instructor: String
) : Identifiable

data class Enrollment(
    val studentId: String,
    val courseId: String,
    var grade: Double? = null
)

// ============================================================
// OBJECT DECLARATION: DataManager
// ============================================================

object DataManager {
    private val studentRepo = Repository<Student>()
    private val courseRepo = Repository<Course>()
    private val enrollmentRepo = Repository<Enrollment>()

    // Inisialisasi data awal
    fun initData() {
        println("📊 Initializing data...")

        // Tambah students
        val students = listOf(
            Student("S001", "Budi Santoso", "Teknik Informatika", 3.75),
            Student("S002", "Siti Rahayu", "Sistem Informasi", 3.50),
            Student("S003", "Ahmad Fauzi", "Teknik Komputer", 3.20),
            Student("S004", "Dewi Lestari", "Teknik Informatika", 2.80)
        )
        students.forEach { studentRepo.add(it) }

        // Tambah courses
        val courses = listOf(
            Course("C001", "Pemrograman Kotlin", 3, "Dr. Andi"),
            Course("C002", "Database Sistem", 3, "Dr. Budi"),
            Course("C003", "Jaringan Komputer", 4, "Dr. Cici"),
            Course("C004", "Kecerdasan Buatan", 3, "Dr. Dedi")
        )
        courses.forEach { courseRepo.add(it) }

        // Tambah enrollments
        val enrollments = listOf(
            Enrollment("S001", "C001"),
            Enrollment("S001", "C002"),
            Enrollment("S002", "C001"),
            Enrollment("S002", "C003"),
            Enrollment("S003", "C002"),
            Enrollment("S003", "C004"),
            Enrollment("S004", "C001")
        )
        enrollments.forEach { enrollmentRepo.add(it) }

        println("✅ Data initialized successfully!")
        println("   Students: ${studentRepo.size()}")
        println("   Courses: ${courseRepo.size()}")
        println("   Enrollments: ${enrollmentRepo.size()}")
    }

    // Student operations
    fun addStudent(student: Student) {
        runCatching {
            if (studentRepo.findById(student.id) != null) {
                throw DuplicateIdException(student.id)
            }
            studentRepo.add(student)
            println("✅ Student added: ${student.name}")
        }.onFailure { exception ->
            println("❌ Failed to add student: ${exception.message}")
        }
    }

    fun getStudent(id: String): Student? {
        return runCatching {
            studentRepo.findById(id) ?: throw NotFoundException(id)
        }.onFailure {
            println("❌ ${it.message}")
        }.getOrNull()
    }

    fun getAllStudents(): List<Student> {
        return studentRepo.getAll()
    }

    fun updateStudentGpa(studentId: String, newGpa: Double): Boolean {
        return runCatching {
            if (newGpa < 0.0 || newGpa > 4.0) {
                throw InvalidGpaException(newGpa)
            }
            val student = studentRepo.findById(studentId) ?: throw NotFoundException(studentId)
            val updatedStudent = student.copy(gpa = newGpa)
            studentRepo.update(studentId, updatedStudent)
        }.onSuccess {
            println("✅ GPA updated for student $studentId")
        }.onFailure { exception ->
            println("❌ Failed to update GPA: ${exception.message}")
        }.getOrDefault(false)
    }

    // Course operations
    fun addCourse(course: Course) {
        runCatching {
            if (courseRepo.findById(course.id) != null) {
                throw DuplicateIdException(course.id)
            }
            courseRepo.add(course)
            println("✅ Course added: ${course.name}")
        }.onFailure { exception ->
            println("❌ Failed to add course: ${exception.message}")
        }
    }

    fun getCourse(id: String): Course? {
        return courseRepo.findById(id)
    }

    fun getAllCourses(): List<Course> {
        return courseRepo.getAll()
    }

    // Enrollment operations
    fun enrollStudent(studentId: String, courseId: String): Boolean {
        return runCatching {
            // Cek apakah student dan course exist
            val student = studentRepo.findById(studentId) ?: throw NotFoundException("Student $studentId")
            val course = courseRepo.findById(courseId) ?: throw NotFoundException("Course $courseId")

            // Cek apakah sudah terdaftar
            val existing = enrollmentRepo.find { it.studentId == studentId && it.courseId == courseId }
            if (existing != null) {
                throw EnrollmentException("Student ${student.name} already enrolled in ${course.name}")
            }

            val enrollment = Enrollment(studentId, courseId)
            enrollmentRepo.add(enrollment)
            println("✅ ${student.name} enrolled in ${course.name}")
            true
        }.onFailure { exception ->
            println("❌ Enrollment failed: ${exception.message}")
        }.getOrDefault(false)
    }

    fun getStudentCourses(studentId: String): List<Course> {
        val enrollments = enrollmentRepo.findAll { it.studentId == studentId }
        val courseIds = enrollments.map { it.courseId }.toSet()
        return courseRepo.getAll().filter { it.id in courseIds }
    }

    fun getCourseStudents(courseId: String): List<Student> {
        val enrollments = enrollmentRepo.findAll { it.courseId == courseId }
        val studentIds = enrollments.map { it.studentId }.toSet()
        return studentRepo.getAll().filter { it.id in studentIds }
    }

    fun calculateGPA(studentId: String): Double {
        val grades = enrollmentRepo
            .findAll { it.studentId == studentId }
            .mapNotNull { it.grade }

        return if (grades.isEmpty()) {
            0.0
        } else {
            grades.average()
        }
    }

    fun setGrade(studentId: String, courseId: String, grade: Double): Boolean {
        return runCatching {
            if (grade < 0.0 || grade > 4.0) {
                throw InvalidGpaException(grade)
            }
            val enrollment = enrollmentRepo.find {
                it.studentId == studentId && it.courseId == courseId
            } ?: throw NotFoundException("Enrollment not found")

            val updatedEnrollment = enrollment.copy(grade = grade)
            enrollmentRepo.update("$studentId-$courseId", updatedEnrollment)
            println("✅ Grade set for student $studentId in course $courseId: $grade")
            true
        }.onFailure { exception ->
            println("❌ Failed to set grade: ${exception.message}")
        }.getOrDefault(false)
    }

    fun displayAllData() {
        println("=" .repeat(55))
        println("📊 ALL DATA")
        println("=" .repeat(55))

        println("\n--- STUDENTS ---")
        getAllStudents().forEach { student ->
            println("   ${student.id}: ${student.name} (${student.major}) - GPA: ${student.gpa}")
        }

        println("\n--- COURSES ---")
        getAllCourses().forEach { course ->
            println("   ${course.id}: ${course.name} (${course.credits} credits) - ${course.instructor}")
        }

        println("\n--- ENROLLMENTS ---")
        enrollmentRepo.getAll().forEach { enrollment ->
            val student = getStudent(enrollment.studentId)
            val course = getCourse(enrollment.courseId)
            val grade = enrollment.grade?.toString() ?: "Not graded"
            println("   ${student?.name ?: "Unknown"} → ${course?.name ?: "Unknown"} (Grade: $grade)")
        }

        println("\n" + "=" .repeat(55))
    }
}

// ============================================================
// FUNGSI UTAMA
// ============================================================

fun main() {
    println("=" .repeat(55))
    println("🎓 SISTEM MANAJEMEN DATA MAHASISWA")
    println("=" .repeat(55))
    println()

    // 1. Inisialisasi data
    DataManager.initData()
    println()

    // 2. Tampilkan semua data
    DataManager.displayAllData()
    println()

    // 3. Demonstrasi enroll student ke course
    println("--- ENROLLMENT DEMONSTRATION ---")
    DataManager.enrollStudent("S001", "C003")  // Sudah ada
    DataManager.enrollStudent("S002", "C004")  // Baru
    DataManager.enrollStudent("S001", "C005")  // Course tidak ada
    println()

    // 4. Tampilkan courses untuk student tertentu
    println("--- STUDENT COURSES ---")
    val studentCourses = DataManager.getStudentCourses("S001")
    println("Courses for Budi Santoso:")
    studentCourses.forEach { println("   ${it.name} (${it.instructor})") }
    println()

    // 5. Tampilkan students untuk course tertentu
    println("--- COURSE STUDENTS ---")
    val courseStudents = DataManager.getCourseStudents("C001")
    println("Students in Pemrograman Kotlin:")
    courseStudents.forEach { println("   ${it.name} (${it.major})") }
    println()

    // 6. Set grade
    println("--- SET GRADE ---")
    DataManager.setGrade("S001", "C001", 3.5)
    DataManager.setGrade("S001", "C002", 3.8)
    DataManager.setGrade("S002", "C001", 3.2)
    println()

    // 7. Hitung GPA
    println("--- GPA CALCULATION ---")
    val gpaBudi = DataManager.calculateGPA("S001")
    println("Budi's GPA: $gpaBudi")
    val gpaSiti = DataManager.calculateGPA("S002")
    println("Siti's GPA: $gpaSiti")
    println()

    // 8. Update GPA
    println("--- UPDATE GPA ---")
    DataManager.updateStudentGpa("S001", 3.85)
    DataManager.updateStudentGpa("S001", 5.0)  // Invalid GPA
    println()

    // 9. Tampilkan data akhir
    DataManager.displayAllData()

    println()
    println("=" .repeat(55))
    println("🏁 PROGRAM SELESAI")
    println("=" .repeat(55))
}
```

---

# BAGIAN 5: RINGKASAN MATERI PERTEMUAN 7

## 5.1 Poin-Poin Penting

| **Konsep** | **Penjelasan** | **Keyword/Sintaks** |
|---|---|---|
| **Generic Class** | Kelas dengan type parameter | `class Box<T>` |
| **Generic Function** | Fungsi dengan type parameter | `fun <T> printList()` |
| **Generic Interface** | Interface dengan type parameter | `interface Comparator<T>` |
| **Upper Bound** | Batasan atas untuk type parameter | `T : Number` |
| **Multiple Constraints** | Multiple batasan dengan `where` | `where T : A, T : B` |
| **List** | Ordered, boleh duplikat | `listOf()`, `mutableListOf()` |
| **Set** | Unique, unordered | `setOf()`, `mutableSetOf()` |
| **Map** | Key-Value pairs | `mapOf()`, `mutableMapOf()` |
| **Read-only vs Mutable** | Dua versi collection | `List` vs `MutableList` |
| **Filter** | Memfilter elemen | `filter { }` |
| **Map** | Transformasi elemen | `map { }` |
| **try-catch-finally** | Exception handling dasar | `try { } catch { } finally { }` |
| **runCatching** | Exception handling fungsional | `runCatching { }` |
| **Custom Exception** | Exception buatan sendiri | `class MyException : Exception` |

---

## 5.2 Kapan Menggunakan Apa?

| **Skenario** | **Solusi** | **Contoh** |
|---|---|---|
| Kode reusable untuk berbagai tipe | Generic Class/Function | `class Repository<T>` |
| Batasi tipe yang bisa digunakan | Generic Constraints | `T : Number` |
| Multiple batasan untuk satu tipe | `where` clause | `where T : A, T : B` |
| Data dengan urutan dan boleh duplikat | List | `listOf("a", "b", "a")` |
| Data unik tanpa duplikat | Set | `setOf(1, 2, 3)` |
| Data dengan key-value | Map | `mapOf("key" to value)` |
| Memfilter data berdasarkan kondisi | `filter()` | `list.filter { it > 5 }` |
| Mentransformasi data | `map()` | `list.map { it * 2 }` |
| Menangani error yang mungkin terjadi | try-catch | `try { ... } catch { ... }` |
| Error handling dengan pendekatan fungsional | runCatching | `runCatching { ... }` |
| Error spesifik untuk aplikasi | Custom Exception | `class MyException : Exception` |

---

# BAGIAN 6: LATIHAN DAN TUGAS

## 6.1 Latihan Mandiri

### Latihan 1: Generic Class `Storage<T>`

Buatlah generic class `Storage<T>` dengan:
- Properti: `items: MutableList<T>`
- Metode: `add(item: T)`, `remove(item: T)`, `get(index: Int): T?`, `getAll(): List<T>`, `size(): Int`

### Latihan 2: Collection Operations

Diberikan list angka: `val numbers = listOf(1, 2, 3, 4, 5, 6, 7, 8, 9, 10)`
- Filter angka genap
- Kalikan setiap angka dengan 2
- Jumlahkan semua angka
- Cari angka pertama yang lebih besar dari 5
- Tampilkan semua angka dalam format "Number: X"

### Latihan 3: Exception Handling dengan runCatching

Buat fungsi `safeDivide(a: String, b: String): Int?` yang:
- Menggunakan `runCatching` untuk menangani error
- Mengonversi string ke Int
- Melakukan pembagian
- Mengembalikan null jika terjadi error

---

## 6.2 Tugas 7 (Dikumpulkan)

### Sistem Manajemen Data Mahasiswa dengan Generic, Collection, dan Exception Handling

Buatlah program lengkap sistem manajemen data mahasiswa dengan ketentuan berikut:

#### 1. Generic Class `Repository<T>`

| **Komponen** | **Spesifikasi** |
|---|---|
| **Properti** | `items: MutableList<T>` (private) |
| **Metode** | `add(item: T): Boolean`<br>`remove(item: T): Boolean`<br>`find(predicate: (T) -> Boolean): T?`<br>`findAll(predicate: (T) -> Boolean): List<T>`<br>`getAll(): List<T>`<br>`update(id: String, newItem: T): Boolean` (dengan constraint Identifiable) |

#### 2. Interface `Identifiable`

| **Komponen** | **Spesifikasi** |
|---|---|
| **Properti** | `val id: String` |

#### 3. Data Class `Student`, `Course`, `Enrollment`

Seperti pada studi kasus di atas.

#### 4. Custom Exception

- `DuplicateIdException`
- `NotFoundException`
- `InvalidGpaException`
- `EnrollmentException`

#### 5. Object Declaration `DataManager`

Seperti pada studi kasus di atas.

#### 6. Fungsi `main()`

- Inisialisasi data dengan `DataManager.initData()`
- Tampilkan semua student, course, dan enrollment
- Lakukan enroll student ke course
- Tampilkan course yang diambil oleh student tertentu
- Tampilkan student yang mengambil course tertentu
- Hitung dan tampilkan GPA student
- Update GPA student dengan validasi

#### 7. Kriteria Penilaian Tugas 7

| **Kriteria** | **Bobot** | **Indikator** |
|---|---|---|
| **Generic** | 25% | `Repository<T>` dengan method generic |
| **Collection** | 20% | Menggunakan List, Map dengan operasi filter/map |
| **Exception Handling** | 25% | try-catch, runCatching, custom exception |
| **Fungsi main()** | 15% | Menampilkan semua skenario |
| **Kode Berkualitas** | 15% | Kode bersih, terstruktur, diberi komentar |

---

# BAGIAN 7: REFERENSI

## 7.1 Referensi Utama

1. **Kotlin Official Documentation – Generics** — [https://kotlinlang.org/docs/generics.html](https://kotlinlang.org/docs/generics.html)

2. **Kotlin Official Documentation – Collections Overview** — [https://kotlinlang.org/docs/collections-overview.html](https://kotlinlang.org/docs/collections-overview.html)

3. **Kotlin Official Documentation – Exceptions** — [https://kotlinlang.org/docs/exceptions.html](https://kotlinlang.org/docs/exceptions.html)

## 7.2 Referensi Pendukung

4. **Constructing collections** — [https://kotlinlang.org/docs/constructing-collections.html](https://kotlinlang.org/docs/constructing-collections.html)

5. **Kotlin Tour: Collections** — [https://kotlinlang.org/docs/kotlin-tour-collections.html](https://kotlinlang.org/docs/kotlin-tour-collections.html)

6. **Collection transformation operations** — [https://kotlinlang.org/docs/collection-transformations.html](https://kotlinlang.org/docs/collection-transformations.html)

---

# BAGIAN 8: PENUTUP

## 8.1 Pesan untuk Mahasiswa

> **"Generic membuat kode Anda reusable dan type-safe. Collection membantu mengelola data dengan elegan. Exception Handling membuat program Anda robust dan siap menghadapi error. Kuasai ketiganya, dan kode Anda akan menjadi lebih profesional!"**

Pertemuan 7 ini memperkenalkan tiga konsep yang sangat penting dalam pengembangan software:

1. **Generic** — membuat kode reusable dan type-safe untuk berbagai tipe data
2. **Collection** — mengelola kumpulan data dengan operasi yang powerful (filter, map, dll)
3. **Exception Handling** — membuat program yang robust dan siap menghadapi error

**Ingatlah:**
1. **Generic** = type safety + reusability — gunakan untuk kode yang bekerja dengan berbagai tipe
2. **List** = ordered, boleh duplikat — untuk data berurutan
3. **Set** = unique, unordered — untuk data unik
4. **Map** = key-value pairs — untuk data dengan identitas unik
5. **try-catch** = exception handling dasar — untuk menangani error
6. **runCatching** = exception handling fungsional — pendekatan modern
7. **Custom Exception** = error spesifik aplikasi — untuk komunikasi error yang jelas

---

**Disusun oleh,**
[Nama Dosen Pengampu]
Dosen Program Studi D4 Teknologi Rekayasa Informatika Industri
