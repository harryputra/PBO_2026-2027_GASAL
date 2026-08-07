# MATERI AJAR PERTEMUAN 8
## PEMROGRAMAN BERORIENTASI OBJEK (OOP) DENGAN KOTLIN
### “UJIAN AKHIR SEMESTER — Proyek Akhir, Presentasi, dan Ujian Praktik”

---

## A. PENDAHULUAN

### 1.1 Gambaran Umum Ujian Akhir Semester

Pertemuan ke-8 merupakan **puncak** dari seluruh pembelajaran OOP selama satu semester. Pada pertemuan ini, mahasiswa akan menunjukkan kemampuan mereka dalam merancang dan mengimplementasikan sebuah sistem berbasis OOP yang mengintegrasikan **seluruh konsep** yang telah dipelajari.

> **Pesan Penting:** UAS ini bukan hanya tentang menulis kode, tetapi tentang **membuktikan** bahwa Anda memahami dan mampu menerapkan OOP secara utuh dalam sebuah proyek nyata.

### 1.2 Komponen Ujian Akhir Semester

| **Komponen** | **Bobot** | **Durasi** | **Deskripsi** |
|---|---|---|---|
| **Proyek Akhir (Kode)** | 50% | 4 jam | Implementasi sistem berbasis OOP sesuai spesifikasi |
| **Presentasi & Demonstrasi** | 30% | 15-20 menit per mahasiswa | Presentasi slide dan live demo aplikasi |
| **Ujian Praktik (Wawancara)** | 20% | 5-10 menit per mahasiswa | Tanya jawab teknis tentang kode dan konsep OOP |

---

## B. PROYEK AKHIR — SPESIFIKASI UMUM

### 2.1 Tujuan Proyek Akhir

Proyek akhir bertujuan untuk mengukur kemampuan mahasiswa dalam:

1. **Merancang** sistem berbasis OOP yang terstruktur
2. **Mengimplementasikan** seluruh pilar OOP (Enkapsulasi, Pewarisan, Polimorfisme, Abstraksi)
3. **Menggunakan** fitur-fitur Kotlin modern (Generic, Collection, Exception Handling)
4. **Mendokumentasikan** kode dengan baik
5. **Mempresentasikan** hasil karya secara profesional

### 2.2 Tema Proyek

Mahasiswa dapat memilih salah satu tema berikut atau mengusulkan tema sendiri (dengan persetujuan dosen):

| **No** | **Tema Proyek** | **Deskripsi Singkat** |
|---|---|---|
| 1 | **Sistem Manajemen Perpustakaan** | Mengelola buku, anggota, peminjaman, pengembalian, dan denda |
| 2 | **Sistem Pemesanan Restoran** | Mengelola menu, pesanan, kalkulasi tagihan, dan status pesanan |
| 3 | **Sistem Manajemen Hotel** | Mengelola kamar, reservasi, check-in/check-out, dan pembayaran |
| 4 | **Sistem Manajemen Karyawan** | Mengelola karyawan, absensi, penggajian, dan cuti |
| 5 | **Sistem E-Commerce Sederhana** | Mengelola produk, keranjang belanja, pesanan, dan pembayaran |
| 6 | **Sistem Manajemen Akademik** | Mengelola mahasiswa, dosen, mata kuliah, dan nilai |
| 7 | **Sistem Manajemen Inventaris** | Mengelola barang, stok, pemasukan, dan pengeluaran |
| 8 | **Sistem Manajemen Proyek** | Mengelola proyek, tugas, anggota tim, dan deadline |
| 9 | **Sistem Manajemen Kontak** | Mengelola kontak (individu/organisasi) dan pencarian |
| 10 | **Simulator Mesin Kopi** | Mensimulasikan mesin kopi dengan berbagai jenis kopi dan manajemen stok |

### 2.3 Ketentuan Wajib Proyek Akhir

Setiap proyek akhir **WAJIB** mengimplementasikan komponen-komponen berikut:

#### A. Enkapsulasi (15%)

| **Komponen** | **Spesifikasi** |
|---|---|
| **Access Modifier** | Gunakan `private`, `protected`, `internal`, `public` dengan tepat |
| **Private Setter** | Minimal 1 properti dengan `private set` |
| **Getter/Setter** | Implementasikan custom getter/setter dengan validasi |

**Contoh Penerapan:**
```kotlin
class BankAccount(private var balance: Double) {
    var transactionHistory: List<String> = emptyList()
        private set  // Private setter

    fun deposit(amount: Double) {
        require(amount > 0) { "Amount must be positive" }
        balance += amount
    }
}
```

#### B. Pewarisan (15%)

| **Komponen** | **Spesifikasi** |
|---|---|
| **Hierarki Kelas** | Minimal 1 hierarki dengan 3 tingkat (Grandparent → Parent → Child) |
| **`open` dan `override`** | Gunakan `open` pada kelas dan metode yang akan di-override |
| **`super`** | Gunakan `super` untuk mengakses member kelas induk |

**Contoh Penerapan:**
```kotlin
open class LibraryItem(open val title: String) {
    open fun getType(): String = "Item"
}

open class Book(title: String, val author: String) : LibraryItem(title) {
    override fun getType(): String = "Book"
}

class EBook(title: String, author: String, val fileSize: Int) : Book(title, author) {
    override fun getType(): String = "E-Book"
}
```

#### C. Polimorfisme (10%)

| **Komponen** | **Spesifikasi** |
|---|---|
| **Polymorphic References** | Gunakan variabel bertipe superclass untuk menampung objek subclass |
| **Smart Casting** | Gunakan `is` dan `when` untuk type checking |
| **`as?`** | Gunakan `as?` untuk safe casting |

**Contoh Penerapan:**
```kotlin
val items: List<LibraryItem> = listOf(Book("OOP", "John"), EBook("Kotlin", "Jane", 1024))
for (item in items) {
    when (item) {
        is EBook -> println("E-Book: ${item.title}, Size: ${item.fileSize}MB")
        is Book -> println("Book: ${item.title} by ${item.author}")
    }
}
```

#### D. Abstraksi (10%)

| **Komponen** | **Spesifikasi** |
|---|---|
| **Abstract Class** | Minimal 1 abstract class dengan metode abstrak dan konkret |
| **Interface** | Minimal 1 interface dengan default method |
| **Multiple Interface** | Minimal 1 kelas mengimplementasikan 2 interface atau lebih |

**Contoh Penerapan:**
```kotlin
abstract class Vehicle(val brand: String) {
    abstract fun start()
    fun stop() = println("$brand stopped")
}

interface Electric {
    fun charge()
}

interface Autonomous {
    fun selfDrive()
}

class Tesla(brand: String) : Vehicle(brand), Electric, Autonomous {
    override fun start() = println("$brand started silently")
    override fun charge() = println("$brand charging")
    override fun selfDrive() = println("$brand driving autonomously")
}
```

#### E. Generic (10%)

| **Komponen** | **Spesifikasi** |
|---|---|
| **Generic Class** | Minimal 1 generic class (contoh: `Repository<T>`) |
| **Generic Function** | Minimal 1 generic function |

**Contoh Penerapan:**
```kotlin
class Repository<T : Any> {
    private val items = mutableListOf<T>()

    fun add(item: T) = items.add(item)
    fun getAll(): List<T> = items.toList()
    fun find(predicate: (T) -> Boolean): T? = items.find(predicate)
}

fun <T> printItems(items: List<T>) {
    items.forEach { println(it) }
}
```

#### F. Collection (10%)

| **Komponen** | **Spesifikasi** |
|---|---|
| **List** | Gunakan List untuk menyimpan data berurutan |
| **Set** | Gunakan Set untuk data unik |
| **Map** | Gunakan Map untuk data key-value |
| **Operations** | Gunakan minimal 3 operasi: `filter`, `map`, `sorted`, `forEach`, dll |

**Contoh Penerapan:**
```kotlin
val books = listOf(
    Book("OOP", "John", 2023),
    Book("Kotlin", "Jane", 2024),
    Book("Java", "John", 2020)
)

// Filter, map, sorted
val recentBooks = books
    .filter { it.year >= 2023 }
    .map { it.title }
    .sorted()
```

#### G. Exception Handling (10%)

| **Komponen** | **Spesifikasi** |
|---|---|
| **try-catch-finally** | Gunakan try-catch-finally untuk menangani exception |
| **runCatching** | Gunakan `runCatching` sebagai alternatif |
| **Custom Exception** | Minimal 2 custom exception |
| **throw** | Gunakan `throw` untuk melempar exception |

**Contoh Penerapan:**
```kotlin
class BookNotFoundException(message: String) : Exception(message)
class MemberNotFoundException(message: String) : Exception(message)

fun borrowBook(bookId: String, memberId: String) {
    runCatching {
        val book = findBook(bookId) ?: throw BookNotFoundException("Book not found")
        val member = findMember(memberId) ?: throw MemberNotFoundException("Member not found")
        // Proses peminjaman
    }.onFailure { exception ->
        println("Error: ${exception.message}")
    }
}
```

#### H. Struktur Kode (10%)

| **Komponen** | **Spesifikasi** |
|---|---|
| **Komentar** | Kode diberi komentar yang jelas (fungsi, kelas, logika penting) |
| **Naming Convention** | Mengikuti konvensi penamaan Kotlin (camelCase, PascalCase) |
| **Struktur** | Kode terstruktur dengan rapi (indentasi, spasi) |

#### I. Fungsionalitas (10%)

| **Komponen** | **Spesifikasi** |
|---|---|
| **Program Berjalan** | Program berjalan tanpa error |
| **Fitur Berfungsi** | Semua fitur yang direncanasi berfungsi dengan baik |
| **Input/Output** | Interaksi dengan pengguna berjalan dengan baik |

---

## C. RUBRIK PENILAIAN

### 3.1 Rubrik Penilaian Proyek Akhir (50%)

| **Kriteria** | **Bobot** | **Excellent (100%)** | **Good (75%)** | **Fair (50%)** | **Poor (25%)** |
|---|---|---|---|---|---|
| **Enkapsulasi** | 15% | Semua properti private, getter/setter dengan validasi, private setter digunakan tepat | Sebagian besar properti private, getter/setter ada | Beberapa properti private | Tidak ada enkapsulasi |
| **Pewarisan** | 15% | Hierarki 3 tingkat, `open`/`override` tepat, `super` digunakan | Hierarki 2 tingkat | Hierarki sederhana | Tidak ada pewarisan |
| **Polimorfisme** | 10% | Polymorphic references, smart casting, `as?` digunakan tepat | Polymorphic references dan smart casting | Salah satu digunakan | Tidak ada |
| **Abstraksi** | 10% | Abstract class, interface default method, multiple interface | Abstract class dan interface | Salah satu | Tidak ada |
| **Generic** | 10% | Generic class dan generic function | Generic class atau generic function | Generic sederhana | Tidak ada |
| **Collection** | 10% | List, Set, Map dengan 3+ operasi | List dan Map dengan 2 operasi | Satu collection | Tidak ada |
| **Exception Handling** | 10% | try-catch, runCatching, 2+ custom exception | try-catch dan 1 custom exception | try-catch saja | Tidak ada |
| **Struktur Kode** | 10% | Kode bersih, komentar lengkap, naming convention tepat | Kode bersih, komentar sebagian | Kode cukup bersih | Kode berantakan |
| **Fungsionalitas** | 10% | Semua fitur berfungsi, program berjalan tanpa error | Sebagian besar fitur berfungsi | Beberapa fitur berfungsi | Program tidak berjalan |

### 3.2 Rubrik Penilaian Presentasi (30%)

| **Kriteria** | **Bobot** | **Excellent (100%)** | **Good (75%)** | **Fair (50%)** | **Poor (25%)** |
|---|---|---|---|---|---|
| **Struktur Presentasi** | 25% | Lengkap (8 slide), alur logis, waktu tepat | Lengkap, alur cukup logis | Kurang lengkap | Tidak terstruktur |
| **Kualitas Slide** | 20% | Profesional, visual menarik, mudah dibaca | Rapi, mudah dibaca | Cukup rapi | Berantakan |
| **Demo Aplikasi** | 30% | Live demo semua fitur, berjalan lancar | Demo sebagian besar fitur | Demo terbatas | Tidak ada demo |
| **Komunikasi** | 25% | Jelas, percaya diri, menjawab pertanyaan dengan baik | Cukup jelas | Kurang jelas | Tidak jelas |

### 3.3 Rubrik Penilaian Ujian Praktik (20%)

| **Kriteria** | **Bobot** | **Excellent (100%)** | **Good (75%)** | **Fair (50%)** | **Poor (25%)** |
|---|---|---|---|---|---|
| **Pemahaman Kode** | 40% | Menjelaskan semua bagian kode dengan baik | Menjelaskan sebagian besar kode | Menjelaskan sebagian kode | Tidak bisa menjelaskan |
| **Konsep OOP** | 40% | Menjawab semua pertanyaan konsep dengan benar | Menjawab sebagian besar | Menjawab sebagian | Tidak bisa menjawab |
| **Problem Solving** | 20% | Memberikan solusi tepat untuk masalah yang diberikan | Memberikan solusi cukup tepat | Memberikan solusi terbatas | Tidak bisa memberikan solusi |

---

## D. STRUKTUR PRESENTASI

### 4.1 Template Slide Presentasi

#### Slide 1: Judul
```
┌─────────────────────────────────────────────────────────────┐
│                                                             │
│                   [NAMA PROYEK]                             │
│                                                             │
│            Sistem Manajemen [Tema]                          │
│                                                             │
│                    [Nama Mahasiswa]                         │
│                    [NIM]                                    │
│                    [Kelas]                                  │
│                                                             │
│            Pemrograman Berorientasi Objek                   │
│            Prodi D4 Teknologi Rekayasa Informatika Industri│
│                                                             │
└─────────────────────────────────────────────────────────────┘
```

#### Slide 2: Latar Belakang
```
┌─────────────────────────────────────────────────────────────┐
│                    LATAR BELAKANG                           │
├─────────────────────────────────────────────────────────────┤
│                                                             │
│  • Masalah yang dipecahkan:                                 │
│    [Deskripsi masalah]                                      │
│                                                             │
│  • Mengapa proyek ini penting?                             │
│    [Alasan/justifikasi]                                     │
│                                                             │
│  • Tujuan proyek:                                           │
│    [Tujuan yang ingin dicapai]                              │
│                                                             │
└─────────────────────────────────────────────────────────────┘
```

#### Slide 3: Analisis Kebutuhan
```
┌─────────────────────────────────────────────────────────────┐
│                  ANALISIS KEBUTUHAN                         │
├─────────────────────────────────────────────────────────────┤
│                                                             │
│  Kebutuhan Fungsional:                                      │
│  • [Fitur 1]                                                │
│  • [Fitur 2]                                                │
│  • [Fitur 3]                                                │
│  • ...                                                      │
│                                                             │
│  Kebutuhan Non-Fungsional:                                  │
│  • [Kebutuhan 1]                                            │
│  • [Kebutuhan 2]                                            │
│  • ...                                                      │
│                                                             │
└─────────────────────────────────────────────────────────────┘
```

#### Slide 4: Class Diagram
```
┌─────────────────────────────────────────────────────────────┐
│                    CLASS DIAGRAM                            │
├─────────────────────────────────────────────────────────────┤
│                                                             │
│  [Gambar Class Diagram]                                     │
│                                                             │
│  Keterangan:                                                │
│  • [Jelaskan hubungan antar kelas]                          │
│  • [Jelaskan inheritance, interface, association]           │
│                                                             │
└─────────────────────────────────────────────────────────────┘
```

#### Slide 5: Implementasi — Struktur Kode
```
┌─────────────────────────────────────────────────────────────┐
│                IMPLEMENTASI — STRUKTUR KODE                 │
├─────────────────────────────────────────────────────────────┤
│                                                             │
│  Struktur Package/File:                                     │
│  • [File 1] — [Deskripsi]                                   │
│  • [File 2] — [Deskripsi]                                   │
│  • [File 3] — [Deskripsi]                                   │
│  • ...                                                      │
│                                                             │
│  Konsep OOP yang digunakan:                                 │
│  • Enkapsulasi: [Contoh]                                    │
│  • Pewarisan: [Contoh]                         │
│  • Polimorfisme: [Contoh]                     │
│  • Abstraksi: [Contoh]                         │
│                                                             │
└─────────────────────────────────────────────────────────────┘
```

#### Slide 6: Implementasi — Fitur Utama
```
┌─────────────────────────────────────────────────────────────┐
│                IMPLEMENTASI — FITUR UTAMA                   │
├─────────────────────────────────────────────────────────────┤
│                                                             │
│  Fitur 1: [Nama Fitur]                                      │
│  • [Deskripsi]                                              │
│  • [Kode snippet / screenshot]                              │
│                                                             │
│  Fitur 2: [Nama Fitur]                                      │
│  • [Deskripsi]                                              │
│  • [Kode snippet / screenshot]                              │
│                                                             │
│  Fitur 3: [Nama Fitur]                                      │
│  • [Deskripsi]                                              │
│  • [Kode snippet / screenshot]                              │
│                                                             │
│  Tantangan & Solusi:                                        │
│  • [Tantangan] → [Solusi]                                   │
│                                                             │
└─────────────────────────────────────────────────────────────┘
```

#### Slide 7: Demo Aplikasi
```
┌─────────────────────────────────────────────────────────────┐
│                    DEMO APLIKASI                            │
├─────────────────────────────────────────────────────────────┤
│                                                             │
│  [Live Demo / Screenshot / Rekaman]                         │
│                                                             │
│  Skenario Demo:                                             │
│  1. [Skenario 1]                                            │
│  2. [Skenario 2]                                            │
│  3. [Skenario 3]                                            │
│                                                             │
│  Hasil yang Diharapkan:                                     │
│  • [Hasil 1]                                                │
│  • [Hasil 2]                                                │
│  • [Hasil 3]                                                │
│                                                             │
└─────────────────────────────────────────────────────────────┘
```

#### Slide 8: Kesimpulan
```
┌─────────────────────────────────────────────────────────────┐
│                     KESIMPULAN                              │
├─────────────────────────────────────────────────────────────┤
│                                                             │
│  Ringkasan Proyek:                                          │
│  • [Apa yang telah dibuat]                                  │
│  • [Bagaimana OOP diterapkan]                               │
│                                                             │
│  Pembelajaran yang Didapat:                                 │
│  • [Pembelajaran 1]                                         │
│  • [Pembelajaran 2]                                         │
│  • [Pembelajaran 3]                                         │
│                                                             │
│  Pengembangan ke Depan:                                     │
│  • [Ide pengembangan]                                       │
│                                                             │
│  Terima Kasih                                               │
│                                                             │
└─────────────────────────────────────────────────────────────┘
```

---

## E. CONTOH KODE REFERENSI — SISTEM MANAJEMEN PERPUSTAKAAN

Berikut adalah contoh implementasi lengkap sistem manajemen perpustakaan yang mengimplementasikan seluruh konsep OOP yang dipelajari.

```kotlin
/**
 * ============================================================
 * SISTEM MANAJEMEN PERPUSTAKAAN — CONTOH REFERENSI UAS
 * ============================================================
 * Demonstrasi implementasi seluruh konsep OOP:
 * 1. Enkapsulasi
 * 2. Pewarisan
 * 3. Polimorfisme
 * 4. Abstraksi
 * 5. Generic
 * 6. Collection
 * 7. Exception Handling
 * ============================================================
 */

// ============================================================
// 1. CUSTOM EXCEPTION (Exception Handling)
// ============================================================

class BookNotFoundException(message: String) : Exception(message)
class MemberNotFoundException(message: String) : Exception(message)
class BookAlreadyBorrowedException(message: String) : Exception(message)
class InvalidInputException(message: String) : Exception(message)
class InsufficientStockException(message: String) : Exception(message)

// ============================================================
// 2. GENERIC CLASS: Repository<T> (Generic)
// ============================================================

class Repository<T : Any> {
    private val items = mutableListOf<T>()

    fun add(item: T): Boolean {
        return try {
            items.add(item)
            true
        } catch (e: Exception) {
            false
        }
    }

    fun remove(item: T): Boolean = items.remove(item)

    fun find(predicate: (T) -> Boolean): T? = items.find(predicate)

    fun findAll(predicate: (T) -> Boolean): List<T> = items.filter(predicate)

    fun getAll(): List<T> = items.toList()

    fun size(): Int = items.size

    // Generic function
    fun <R> map(transform: (T) -> R): List<R> = items.map(transform)
}

// ============================================================
// 3. INTERFACE: Identifiable & Borrowable (Abstraksi)
// ============================================================

interface Identifiable {
    val id: String
}

interface Borrowable {
    fun borrow(memberId: String): Boolean
    fun returnItem(): Boolean
    fun isAvailable(): Boolean
    fun getBorrower(): String?
}

// ============================================================
// 4. DATA CLASSES (Data Class)
// ============================================================

data class Book(
    override val id: String,
    val title: String,
    val author: String,
    val year: Int,
    var isBorrowed: Boolean = false,
    var borrowerId: String? = null
) : Identifiable

data class Member(
    override val id: String,
    val name: String,
    val email: String,
    val phone: String
) : Identifiable

data class BorrowTransaction(
    val id: String,
    val bookId: String,
    val memberId: String,
    val borrowDate: String,
    var returnDate: String? = null
)

// ============================================================
// 5. ABSTRACT CLASS: LibraryItem (Abstraksi)
// ============================================================

abstract class LibraryItem(
    open val id: String,
    open val title: String
) {
    abstract fun getType(): String
    abstract fun getDetails(): String

    fun display() {
        println("[$getType] $title (ID: $id)")
        println("   Details: ${getDetails()}")
    }
}

// ============================================================
// 6. SUBCLASS: BookItem (Pewarisan)
// ============================================================

class BookItem(
    override val id: String,
    override val title: String,
    val author: String,
    val year: Int,
    val pages: Int
) : LibraryItem(id, title) {
    override fun getType(): String = "Book"

    override fun getDetails(): String = "by $author ($year), $pages pages"
}

// ============================================================
// 7. SUBCLASS: MagazineItem (Pewarisan)
// ============================================================

class MagazineItem(
    override val id: String,
    override val title: String,
    val issueNumber: Int,
    val publisher: String
) : LibraryItem(id, title) {
    override fun getType(): String = "Magazine"

    override fun getDetails(): String = "Issue #$issueNumber, published by $publisher"
}

// ============================================================
// 8. SUBCLASS: BorrowableBook (Pewarisan + Interface)
// ============================================================

class BorrowableBook(
    id: String,
    title: String,
    author: String,
    year: Int,
    pages: Int,
    private var _isBorrowed: Boolean = false,
    private var _borrowerId: String? = null
) : BookItem(id, title, author, year, pages), Borrowable {

    // Enkapsulasi — private setter untuk properti tertentu
    var isBorrowed: Boolean = _isBorrowed
        private set

    var borrowerId: String? = _borrowerId
        private set

    override fun borrow(memberId: String): Boolean {
        return if (isAvailable()) {
            borrowerId = memberId
            isBorrowed = true
            println("✅ Book '$title' borrowed by member $memberId")
            true
        } else {
            println("❌ Book '$title' is not available")
            false
        }
    }

    override fun returnItem(): Boolean {
        return if (!isAvailable()) {
            val member = borrowerId
            borrowerId = null
            isBorrowed = false
            println("✅ Book '$title' returned by $member")
            true
        } else {
            println("❌ Book '$title' is not borrowed")
            false
        }
    }

    override fun isAvailable(): Boolean = !isBorrowed

    override fun getBorrower(): String? = borrowerId
}

// ============================================================
// 9. OBJECT DECLARATION: LibraryManager (Singleton)
// ============================================================

object LibraryManager {
    // Collection — List, Map
    private val bookRepo = Repository<BorrowableBook>()
    private val memberRepo = Repository<Member>()
    private val transactionRepo = Repository<BorrowTransaction>()
    private val borrowHistory = mutableMapOf<String, MutableList<String>>() // memberId -> list of bookIds

    // ==================== BOOK OPERATIONS ====================

    fun addBook(book: BorrowableBook) {
        bookRepo.add(book)
        println("✅ Book added: ${book.title}")
    }

    fun findBook(id: String): BorrowableBook? {
        return bookRepo.find { it.id == id }
    }

    fun getAllBooks(): List<BorrowableBook> = bookRepo.getAll()

    fun getAvailableBooks(): List<BorrowableBook> {
        return bookRepo.findAll { it.isAvailable() }
    }

    fun getBorrowedBooks(): List<BorrowableBook> {
        return bookRepo.findAll { !it.isAvailable() }
    }

    // Collection operations — filter, map, sorted
    fun getBooksByAuthor(author: String): List<BorrowableBook> {
        return bookRepo.getAll()
            .filter { it.author.contains(author, ignoreCase = true) }
            .sortedBy { it.title }
    }

    fun getBookTitles(): List<String> {
        return bookRepo.getAll()
            .map { it.title }
            .sorted()
    }

    // ==================== MEMBER OPERATIONS ====================

    fun addMember(member: Member) {
        memberRepo.add(member)
        println("✅ Member added: ${member.name}")
    }

    fun findMember(id: String): Member? {
        return memberRepo.find { it.id == id }
    }

    fun getAllMembers(): List<Member> = memberRepo.getAll()

    fun searchMembersByName(name: String): List<Member> {
        return memberRepo.findAll {
            it.name.contains(name, ignoreCase = true)
        }
    }

    // ==================== BORROW OPERATIONS ====================

    fun borrowBook(bookId: String, memberId: String): Boolean {
        return runCatching {  // Exception Handling dengan runCatching
            val book = findBook(bookId) ?: throw BookNotFoundException("Book $bookId not found")
            val member = findMember(memberId) ?: throw MemberNotFoundException("Member $memberId not found")

            if (!book.isAvailable()) {
                throw BookAlreadyBorrowedException("Book '${book.title}' is already borrowed")
            }

            // Proses peminjaman
            book.borrow(memberId)
            borrowHistory.getOrPut(memberId) { mutableListOf() }.add(bookId)

            // Catat transaksi
            val transaction = BorrowTransaction(
                id = "TRX-${System.currentTimeMillis()}",
                bookId = bookId,
                memberId = memberId,
                borrowDate = java.time.LocalDate.now().toString()
            )
            transactionRepo.add(transaction)

            true
        }.onFailure { exception ->
            println("❌ Borrow failed: ${exception.message}")
        }.getOrDefault(false)
    }

    fun returnBook(bookId: String): Boolean {
        return runCatching {
            val book = findBook(bookId) ?: throw BookNotFoundException("Book $bookId not found")
            book.returnItem()
        }.onFailure { exception ->
            println("❌ Return failed: ${exception.message}")
        }.getOrDefault(false)
    }

    fun getMemberBorrowHistory(memberId: String): List<String> {
        return borrowHistory[memberId] ?: emptyList()
    }

    fun getMemberTransactions(memberId: String): List<BorrowTransaction> {
        return transactionRepo.findAll { it.memberId == memberId }
    }

    // ==================== STATISTICS ====================

    fun getTotalBooks(): Int = bookRepo.size()
    fun getTotalMembers(): Int = memberRepo.size()
    fun getTotalTransactions(): Int = transactionRepo.size()

    fun getMostBorrowedBooks(): List<Pair<String, Int>> {
        // Menghitung buku paling sering dipinjam
        val borrowCount = mutableMapOf<String, Int>()
        transactionRepo.getAll().forEach { transaction ->
            borrowCount[transaction.bookId] = borrowCount.getOrDefault(transaction.bookId, 0) + 1
        }
        return borrowCount.toList()
            .sortedByDescending { it.second }
            .take(5)
            .mapNotNull { (id, count) ->
                findBook(id)?.let { it.title to count }
            }
    }

    // ==================== DISPLAY ====================

    fun displayAllBooks() {
        println("=" .repeat(50))
        println("📚 ALL BOOKS (${getTotalBooks()} books)")
        println("=" .repeat(50))
        getAllBooks().forEach { book ->
            val status = if (book.isAvailable()) "✅ Available" else "🔴 Borrowed by ${book.borrowerId}"
            println("   ${book.id}: ${book.title} by ${book.author} ($status)")
        }
        println("=" .repeat(50))
    }

    fun displayAvailableBooks() {
        println("=" .repeat(50))
        println("📚 AVAILABLE BOOKS")
        println("=" .repeat(50))
        getAvailableBooks().forEach { book ->
            println("   ${book.id}: ${book.title} by ${book.author}")
        }
        println("=" .repeat(50))
    }

    fun displayMembers() {
        println("=" .repeat(50))
        println("👤 MEMBERS (${getTotalMembers()} members)")
        println("=" .repeat(50))
        getAllMembers().forEach { member ->
            val history = getMemberBorrowHistory(member.id)
            println("   ${member.id}: ${member.name} (${member.email})")
            println("      Borrowed: ${history.size} books")
        }
        println("=" .repeat(50))
    }

    fun displayStatistics() {
        println("=" .repeat(50))
        println("📊 STATISTICS")
        println("=" .repeat(50))
        println("Total Books      : ${getTotalBooks()}")
        println("Total Members    : ${getTotalMembers()}")
        println("Total Transactions: ${getTotalTransactions()}")
        println("\nMost Borrowed Books:")
        getMostBorrowedBooks().forEachIndexed { index, (title, count) ->
            println("   ${index + 1}. $title ($count times)")
        }
        println("=" .repeat(50))
    }
}

// ============================================================
// 10. DEMONSTRASI POLIMORFISME
// ============================================================

fun demonstratePolymorphism() {
    println("=" .repeat(50))
    println("🔄 POLYMORPHISM DEMONSTRATION")
    println("=" .repeat(50))

    // Polymorphic references — List of LibraryItem
    val items: List<LibraryItem> = listOf(
        BookItem("B010", "Pemrograman Kotlin", "Budi Santoso", 2023, 350),
        BookItem("B011", "Dasar-Dasar OOP", "Siti Rahayu", 2022, 280),
        MagazineItem("M001", "Tech Today", 42, "Tech Media")
    )

    // Smart casting dengan when
    items.forEach { item ->
        when (item) {
            is BookItem -> println("📖 ${item.title} — Book, ${item.pages} pages")
            is MagazineItem -> println("📰 ${item.title} — Magazine, Issue #${item.issueNumber}")
            else -> println("Unknown item: ${item.title}")
        }
    }
}

// ============================================================
// 11. DEMONSTRASI GENERIC FUNCTION
// ============================================================

fun <T> displayItems(items: List<T>, label: String) {
    println("--- $label (${items.size} items) ---")
    items.forEachIndexed { index, item ->
        println("   ${index + 1}. $item")
    }
}

// ============================================================
// 12. MAIN FUNCTION
// ============================================================

fun main() {
    println("=" .repeat(55))
    println("📚 SISTEM MANAJEMEN PERPUSTAKAAN — DEMO UAS")
    println("=" .repeat(55))
    println()

    // ==================== 1. ADD DATA ====================

    println("--- ADDING BOOKS ---")
    val book1 = BorrowableBook("B001", "Pemrograman Kotlin", "Budi Santoso", 2023, 350)
    val book2 = BorrowableBook("B002", "Dasar-Dasar OOP", "Siti Rahayu", 2022, 280)
    val book3 = BorrowableBook("B003", "Algoritma dan Struktur Data", "Ahmad Fauzi", 2023, 400)
    val book4 = BorrowableBook("B004", "Database Sistem", "Dewi Lestari", 2021, 320)
    val book5 = BorrowableBook("B005", "Jaringan Komputer", "Rizki Pratama", 2022, 360)

    LibraryManager.addBook(book1)
    LibraryManager.addBook(book2)
    LibraryManager.addBook(book3)
    LibraryManager.addBook(book4)
    LibraryManager.addBook(book5)
    println()

    println("--- ADDING MEMBERS ---")
    val member1 = Member("M001", "Budi Santoso", "budi@email.com", "08123456789")
    val member2 = Member("M002", "Siti Rahayu", "siti@email.com", "08129876543")
    val member3 = Member("M003", "Ahmad Fauzi", "ahmad@email.com", "08125556677")

    LibraryManager.addMember(member1)
    LibraryManager.addMember(member2)
    LibraryManager.addMember(member3)
    println()

    // ==================== 2. DISPLAY BOOKS ====================

    LibraryManager.displayAllBooks()
    println()

    // ==================== 3. COLLECTION OPERATIONS ====================

    println("--- COLLECTION OPERATIONS ---")
    // filter + map + sorted
    val recentBooks = LibraryManager.getAllBooks()
        .filter { it.year >= 2023 }
        .map { "${it.title} (${it.year})" }
        .sorted()
    println("Books from 2023 onwards: $recentBooks")

    // Generic function
    val bookTitles = LibraryManager.getAllBooks().map { it.title }
    displayItems(bookTitles, "Book Titles")
    println()

    // ==================== 4. BORROW BOOKS ====================

    println("--- BORROWING BOOKS ---")
    LibraryManager.borrowBook("B001", "M001")  // ✅ Berhasil
    LibraryManager.borrowBook("B002", "M001")  // ✅ Berhasil
    LibraryManager.borrowBook("B003", "M002")  // ✅ Berhasil
    LibraryManager.borrowBook("B001", "M002")  // ❌ Gagal (sudah dipinjam)
    LibraryManager.borrowBook("B999", "M001")  // ❌ Gagal (buku tidak ditemukan)
    println()

    LibraryManager.displayAllBooks()
    println()

    // ==================== 5. DEMONSTRASI POLIMORFISME ====================

    demonstratePolymorphism()
    println()

    // ==================== 6. RETURN BOOK ====================

    println("--- RETURNING BOOKS ---")
    LibraryManager.returnBook("B001")  // ✅ Berhasil
    LibraryManager.returnBook("B001")  // ❌ Gagal (sudah dikembalikan)
    println()

    LibraryManager.displayAllBooks()
    println()

    // ==================== 7. DISPLAY MEMBERS ====================

    LibraryManager.displayMembers()
    println()

    // ==================== 8. STATISTICS ====================

    LibraryManager.displayStatistics()
    println()

    // ==================== 9. EXCEPTION HANDLING DEMONSTRATION ====================

    println("--- EXCEPTION HANDLING ---")
    runCatching {
        LibraryManager.findBook("B999") ?: throw BookNotFoundException("Book B999 not found")
    }.onFailure { exception ->
        println("❌ Caught exception: ${exception.message}")
    }

    // try-catch-finally
    try {
        val invalidInput = "abc".toInt()
    } catch (e: NumberFormatException) {
        println("❌ Number format error: ${e.message}")
    } finally {
        println("✅ Finally block executed")
    }

    println()
    println("=" .repeat(55))
    println("🏁 PROGRAM SELESAI")
    println("=" .repeat(55))
}
```

---

## F. JADWAL PELAKSANAAN UAS (8 JAM)

### Sesi 1: Briefing & Persiapan (2 Jam — 120 menit)

| **Waktu** | **Kegiatan** | **Detail** | **Metode** |
|---|---|---|---|
| **0-15'** | Pembukaan & Doa | • Dosen membuka perkuliahan dengan salam dan doa<br>• Menjelaskan bahwa ini adalah pertemuan terakhir (UAS) | Ceramah |
| **15-45'** | Briefing UAS | • **Penjelasan komponen UAS**: Proyek Akhir (50%), Presentasi (30%), Ujian Praktik (20%)<br>• **Penjelasan spesifikasi proyek akhir**<br>• **Kriteria penilaian** — lihat bagian C<br>• **Struktur presentasi** — lihat bagian D<br>• **Jadwal pelaksanaan**: 4 jam coding, 2 jam presentasi, 2 jam ujian praktik<br>• **Aturan**: tidak boleh menggunakan internet (kecuali IDE/documentation offline), tidak boleh copy-paste dari sumber luar | Ceramah, Diskusi |
| **45-75'** | Pemilihan Topik & Konsultasi | • Mahasiswa memilih topik proyek dari daftar yang disediakan<br>• Dosen memberikan konsultasi singkat untuk setiap topik<br>• Mahasiswa membuat **rancangan awal**: class diagram sederhana, fitur-fitur yang akan diimplementasikan | Diskusi, Konsultasi |
| **75-105'** | Perancangan Awal | • Mahasiswa membuat **Class Diagram** awal di kertas/whiteboard<br>• Mengidentifikasi kelas-kelas yang dibutuhkan<br>• Mengidentifikasi hubungan antar kelas (inheritance, interface, association) | Praktik, Asistensi |
| **105-120'** | Finalisasi Rencana | • Mahasiswa memfinalisasi rencana proyek<br>• Dosen menyetujui rancangan atau memberikan revisi | Konsultasi |

### Sesi 2: Pengerjaan Proyek — Bagian 1 (2 Jam — 120 menit)

| **Waktu** | **Kegiatan** | **Detail** | **Metode** |
|---|---|---|---|
| **0-10'** | Review Rencana | • Dosen mereview rencana proyek mahasiswa | Ceramah |
| **10-70'** | Pengerjaan — Tahap 1 | • Implementasi **kelas-kelas dasar** (data class)<br>• Implementasi **enkapsulasi** (private properties, getter/setter, private setter)<br>• Implementasi **pewarisan** (hierarki dengan `open` dan `override`) | Praktik mandiri, Asistensi |
| **70-100'** | Pengerjaan — Tahap 2 | • Implementasi **abstraksi** (abstract class dan/atau interface)<br>• Implementasi **polimorfisme** (polymorphic references, smart casting)<br>• Implementasi **generic** (generic class atau generic function) | Praktik mandiri, Asistensi |
| **100-120'** | Checkpoint 1 | • Dosen melakukan pengecekan progres<br>• Memberikan feedback dan saran perbaikan | Konsultasi, Feedback |

### Sesi 3: Pengerjaan Proyek — Bagian 2 (2 Jam — 120 menit)

| **Waktu** | **Kegiatan** | **Detail** | **Metode** |
|---|---|---|---|
| **0-10'** | Review Checkpoint 1 | • Dosen mereview hasil checkpoint 1 | Ceramah |
| **10-70'** | Pengerjaan — Tahap 3 | • Implementasi **collection** (List, Set, Map dengan operasi filter, map, dll)<br>• Implementasi **exception handling** (try-catch-finally, runCatching, custom exception) | Praktik mandiri, Asistensi |
| **70-100'** | Pengerjaan — Tahap 4 | • **Testing** dan **debugging**<br>• Memastikan semua fitur berfungsi<br>• Membersihkan kode (refactoring, komentar, format) | Praktik mandiri, Asistensi |
| **100-120'** | Checkpoint 2 | • Dosen melakukan pengecekan akhir<br>• Mahasiswa mempersiapkan **slide presentasi** | Konsultasi, Feedback |

### Sesi 4: Presentasi & Ujian Praktik (2 Jam — 120 menit)

| **Waktu** | **Kegiatan** | **Detail** | **Metode** |
|---|---|---|---|
| **0-10'** | Pengaturan | • Dosen mengatur urutan presentasi<br>• Menjelaskan aturan presentasi dan ujian praktik | Ceramah |
| **10-85'** | Presentasi & Demo | • Setiap mahasiswa presentasi (10-12 menit):<br>  - Latar Belakang & Analisis (2 menit)<br>  - Class Diagram & Implementasi (3 menit)<br>  - Fitur Utama (2 menit)<br>  - Demo Aplikasi (5 menit)<br>  - Kesimpulan (1 menit) | Presentasi, Demonstrasi |
| **85-105'** | Ujian Praktik | • Dosen mengajukan pertanyaan teknis:<br>  - "Mengapa Anda menggunakan inheritance di sini?"<br>  - "Bagaimana enkapsulasi pada kelas ini?"<br>  - "Apa fungsi generic yang Anda gunakan?"<br>  - "Bagaimana Anda menangani exception?" | Tanya jawab, Wawancara |
| **105-120'** | Penutupan | • Dosen memberikan kesimpulan dan apresiasi<br>• Doa dan salam penutup | Ceramah |

---

## G. CHECKLIST PERSIAPAN UAS

| **No** | **Item Persiapan** | **Status** |
|---|---|---|
| 1 | Topik proyek sudah disetujui dosen | ☐ |
| 2 | Class Diagram sudah dibuat | ☐ |
| 3 | IDE (IntelliJ IDEA) sudah terinstal dan siap | ☐ |
| 4 | JDK sudah terinstal dan terkonfigurasi | ☐ |
| 5 | Template presentasi sudah disiapkan | ☐ |
| 6 | File project sudah dibuat | ☐ |
| 7 | Rencana fitur sudah ditentukan | ☐ |
| 8 | Konsep OOP yang akan digunakan sudah diidentifikasi | ☐ |

---

## H. PERTANYAAN UMUM UJIAN PRAKTIK

Berikut adalah contoh pertanyaan yang mungkin diajukan dosen saat ujian praktik:

### Pertanyaan Konsep OOP

1. **Enkapsulasi:** "Jelaskan bagaimana Anda menerapkan enkapsulasi pada kelas [nama kelas]. Mengapa Anda memilih untuk membuat properti tersebut private?"

2. **Pewarisan:** "Mengapa Anda memilih untuk membuat kelas [nama kelas] sebagai superclass? Apa alasan Anda menggunakan `open` dan `override` pada metode tersebut?"

3. **Polimorfisme:** "Tunjukkan bagian kode yang menerapkan polimorfisme. Bagaimana cara kerja polymorphic references pada kode Anda?"

4. **Abstraksi:** "Apa perbedaan antara abstract class dan interface pada proyek Anda? Mengapa Anda memilih salah satu dari keduanya?"

5. **Generic:** "Apa manfaat menggunakan generic pada kelas Repository<T>? Bagaimana jika Anda tidak menggunakan generic?"

6. **Collection:** "Mengapa Anda memilih List daripada Set untuk menyimpan data [nama data]? Tunjukkan penggunaan operasi collection pada kode Anda."

7. **Exception Handling:** "Bagaimana Anda menangani exception pada fitur [nama fitur]? Mengapa Anda memilih menggunakan try-catch atau runCatching?"

### Pertanyaan Kode Spesifik

1. "Tunjukkan bagian kode yang paling kompleks dan jelaskan cara kerjanya."

2. "Jika ada bug pada fitur ini, bagaimana Anda akan melakukan debugging?"

3. "Bagaimana Anda bisa menambahkan fitur baru [nama fitur] tanpa mengubah struktur kode yang sudah ada?"

4. "Apa yang akan terjadi jika pengguna memasukkan input yang tidak valid pada fitur ini?"

---

## I. REFERENSI

### Referensi Utama:

1. **Kotlin Official Documentation** — [https://kotlinlang.org/docs/](https://kotlinlang.org/docs/)

2. **Kotlin Tour: Classes and Interfaces** — [https://kotlinlang.org/docs/kotlin-tour-intermediate-classes-interfaces.html](https://kotlinlang.org/docs/kotlin-tour-intermediate-classes-interfaces.html)

3. **Kotlin Tour: Collections** — [https://kotlinlang.org/docs/kotlin-tour-collections.html](https://kotlinlang.org/docs/kotlin-tour-collections.html)

### Referensi Pendukung:

4. **Utilizing OOP Principles in Kotlin** — CodeSignal

5. **JetBrains Academy Projects** — Contacts, Coffee Machine

6. **OOP Grading Criteria** — Various university sources

---

## J. PENUTUP

### 10.1 Pesan untuk Mahasiswa

> **"Ujian Akhir Semester adalah kesempatan Anda untuk menunjukkan bahwa Anda telah menguasai OOP secara utuh. Bukan hanya menulis kode, tetapi merancang, mengimplementasikan, dan mengkomunikasikan solusi dengan baik."**

Pertemuan 8 adalah **puncak** dari perjalanan belajar OOP selama satu semester. Pada pertemuan ini, Anda akan:

1. **Membuktikan** pemahaman Anda tentang seluruh konsep OOP
2. **Menunjukkan** kemampuan Anda dalam merancang dan mengimplementasikan sistem
3. **Mengkomunikasikan** hasil karya secara profesional
4. **Menjawab** pertanyaan teknis dengan percaya diri

**Ingatlah:**
1. **Rencanakan** dengan baik — class diagram yang jelas memudahkan implementasi
2. **Fokus** pada kualitas, bukan kuantitas — implementasi yang tepat lebih baik daripada fitur yang banyak tapi tidak berfungsi
3. **Dokumentasikan** kode Anda — komentar yang jelas membantu menjelaskan logika
4. **Latih presentasi** — pastikan Anda bisa mendemonstrasikan semua fitur dengan lancar
5. **Pahami kode Anda** — Anda harus bisa menjelaskan setiap bagian dari kode yang Anda tulis

**Selamat mengerjakan UAS!** 🎓

---

**Disusun oleh,**
[Nama Dosen Pengampu]
Dosen Program Studi D4 Teknologi Rekayasa Informatika Industri
