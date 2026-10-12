# STUDI KASUS LATIHAN PERTEMUAN 5
## MATA KULIAH: PEMROGRAMAN BERORIENTASI OBJEK (OOP)
### TOPIK: ABSTRAKSI DAN INTERFACE

---

## A. PENDAHULUAN

Latihan pertemuan 5 terdiri dari **dua bagian**:
1. **Studi Kasus Individu** – dikerjakan secara mandiri untuk memperkuat pemahaman konsep abstract class, interface, default method, multiple interface, dan sealed class.
2. **Studi Kasus Kelompok** – dikerjakan secara berkelompok (3–4 orang) untuk melatih kolaborasi dalam merancang dan mengimplementasikan sistem yang lebih kompleks.

Setiap studi kasus dilengkapi dengan **panduan langkah demi langkah**, **spesifikasi teknis**, **output yang diharapkan**, dan **kriteria penilaian** agar mahasiswa dapat mengerjakan dengan jelas dan terarah.

---

## B. STUDI KASUS INDIVIDU
### “SISTEM MANAJEMEN PEGAWAI SEDERHANA”

#### B.1. Latar Belakang
Sebuah perusahaan memiliki tiga jenis pegawai:
- **Pegawai Tetap** – mendapatkan gaji pokok + tunjangan + bonus tahunan.
- **Pegawai Kontrak** – hanya mendapatkan gaji pokok, tanpa bonus.
- **Pegawai Magang** – mendapatkan uang saku, tidak dikenakan pajak.

Perusahaan ingin menghitung:
- Gaji total per pegawai.
- Pajak yang harus dibayar (jika ada).
- Bonus yang diterima (jika ada).
- Menampilkan status pegawai (Aktif, Cuti, Berhenti).

#### B.2. Tujuan Pembelajaran
- Menerapkan **abstract class** dengan metode abstrak dan konkret.
- Menerapkan **interface** dengan default method.
- Menerapkan **multiple interface** pada kelas yang sesuai.
- Menggunakan **sealed class** untuk status pegawai.
- Menerapkan **enkapsulasi** dan **polimorfisme** dalam satu kesatuan.

#### B.3. Spesifikasi Teknis

##### 1. Abstract Class `Employee`
| Komponen | Keterangan |
|----------|------------|
| Properti | `id: String` (read-only), `name: String` (read-only), `baseSalary: Double` (read-only) |
| Metode abstrak | `calculateSalary(): Double` |
| Metode konkret | `displayInfo()` – menampilkan ID, Nama, Gaji Pokok, Gaji Total |
| Properti abstrak | `status: EmployeeStatus` (mutable) |

##### 2. Interface `Taxable`
| Komponen | Keterangan |
|----------|------------|
| Metode | `calculateTax(): Double` – **default**: 5% dari `calculateSalary()` |

##### 3. Interface `BonusEligible`
| Komponen | Keterangan |
|----------|------------|
| Properti | `bonusRate: Double` (read-only) |
| Metode | `calculateBonus(): Double` – **default**: `bonusRate * calculateSalary()` |

##### 4. Sealed Class `EmployeeStatus`
- `Active` – pegawai aktif.
- `OnLeave` – pegawai sedang cuti.
- `Terminated` – pegawai berhenti.
- Method `display(): String` untuk menampilkan status.

##### 5. Subclass
| Subclass | Properti Tambahan | Implementasi Interface | Override |
|----------|-------------------|------------------------|----------|
| `FullTimeEmployee` | `allowance: Double` (tunjangan), `annualBonus: Double` | `Taxable`, `BonusEligible` | `calculateSalary() = baseSalary + allowance` <br> `calculateBonus() = annualBonus` |
| `ContractEmployee` | `contractDuration: Int` (bulan) | `Taxable` | `calculateSalary() = baseSalary` |
| `Intern` | `stipend: Double` (uang saku) | – | `calculateSalary() = stipend` |

##### 6. Kelas `Company`
| Komponen | Keterangan |
|----------|------------|
| Properti | `name: String`, `employees: MutableList<Employee>` (private) |
| Metode | `addEmployee(employee: Employee)` <br> `getTotalSalary(): Double` <br> `getTotalTax(): Double` <br> `getTotalBonus(): Double` <br> `displayAllEmployees()` |

#### B.4. Panduan Pengerjaan (Langkah demi Langkah)

1. **Buat file `Employee.kt`**
   Definisikan `sealed class EmployeeStatus` terlebih dahulu.
   ```kotlin
   sealed class EmployeeStatus {
       object Active : EmployeeStatus()
       object OnLeave : EmployeeStatus()
       object Terminated : EmployeeStatus()
       fun display(): String = when(this) {
           Active -> "Aktif"
           OnLeave -> "Cuti"
           Terminated -> "Berhenti"
       }
   }
   ```

2. **Buat abstract class `Employee`**
   Tambahkan properti dan metode sesuai spesifikasi.
   ```kotlin
   abstract class Employee(
       val id: String,
       val name: String,
       val baseSalary: Double
   ) {
       abstract var status: EmployeeStatus
       abstract fun calculateSalary(): Double

       open fun displayInfo() {
           println("ID: $id, Nama: $name")
           println("Gaji Pokok: Rp ${baseSalary}")
           println("Gaji Total: Rp ${calculateSalary()}")
           println("Status: ${status.display()}")
       }
   }
   ```

3. **Buat interface `Taxable` dan `BonusEligible`**
   Sertakan default method.
   ```kotlin
   interface Taxable {
       fun calculateTax(): Double = 0.05 * (this as Employee).calculateSalary()
   }

   interface BonusEligible {
       val bonusRate: Double
       fun calculateBonus(): Double = bonusRate * (this as Employee).calculateSalary()
   }
   ```

4. **Buat subclass `FullTimeEmployee`, `ContractEmployee`, `Intern`**
   Implementasikan abstract class dan interface yang sesuai.
   ```kotlin
   class FullTimeEmployee(
       id: String, name: String, baseSalary: Double,
       val allowance: Double, val annualBonus: Double
   ) : Employee(id, name, baseSalary), Taxable, BonusEligible {
       override var status: EmployeeStatus = EmployeeStatus.Active
       override val bonusRate: Double = 0.0 // tidak digunakan karena override calculateBonus
       override fun calculateSalary(): Double = baseSalary + allowance
       override fun calculateBonus(): Double = annualBonus
   }

   class ContractEmployee(
       id: String, name: String, baseSalary: Double,
       val contractDuration: Int
   ) : Employee(id, name, baseSalary), Taxable {
       override var status: EmployeeStatus = EmployeeStatus.Active
       override fun calculateSalary(): Double = baseSalary
   }

   class Intern(
       id: String, name: String, val stipend: Double
   ) : Employee(id, name, 0.0) {
       override var status: EmployeeStatus = EmployeeStatus.Active
       override fun calculateSalary(): Double = stipend
   }
   ```

5. **Buat kelas `Company`**
   Kelola daftar pegawai dan hitung total.
   ```kotlin
   class Company(val name: String) {
       private val employees = mutableListOf<Employee>()
       fun addEmployee(employee: Employee) { employees.add(employee) }
       fun getTotalSalary(): Double = employees.sumOf { it.calculateSalary() }
       fun getTotalTax(): Double = employees.filterIsInstance<Taxable>().sumOf { it.calculateTax() }
       fun getTotalBonus(): Double = employees.filterIsInstance<BonusEligible>().sumOf { it.calculateBonus() }
       fun displayAllEmployees() {
           println("=== Daftar Pegawai $name ===")
           employees.forEach { it.displayInfo(); println("---") }
       }
   }
   ```

6. **Buat fungsi `main()`**
   Demonstrasikan semua fitur.
   ```kotlin
   fun main() {
       val company = Company("PT Maju Jaya")
       company.addEmployee(FullTimeEmployee("P001", "Budi", 5_000_000.0, 1_500_000.0, 6_000_000.0))
       company.addEmployee(ContractEmployee("P002", "Siti", 4_500_000.0, 12))
       company.addEmployee(Intern("P003", "Ahmad", 2_000_000.0))

       company.displayAllEmployees()
       println("Total Gaji: Rp ${company.getTotalSalary()}")
       println("Total Pajak: Rp ${company.getTotalTax()}")
       println("Total Bonus: Rp ${company.getTotalBonus()}")
   }
   ```

#### B.5. Output yang Diharapkan (Contoh)
```
=== Daftar Pegawai PT Maju Jaya ===
ID: P001, Nama: Budi
Gaji Pokok: Rp 5000000.0
Gaji Total: Rp 6500000.0
Status: Aktif
---
ID: P002, Nama: Siti
Gaji Pokok: Rp 4500000.0
Gaji Total: Rp 4500000.0
Status: Aktif
---
ID: P003, Nama: Ahmad
Gaji Pokok: Rp 0.0
Gaji Total: Rp 2000000.0
Status: Aktif
---
Total Gaji: Rp 13000000.0
Total Pajak: Rp 550000.0
Total Bonus: Rp 6000000.0
```

#### B.6. Kriteria Penilaian Individu
| Kriteria | Bobot | Indikator |
|----------|-------|-----------|
| Abstract Class | 20% | `Employee` sebagai abstract class, metode abstrak & konkret benar |
| Interface & Default Method | 20% | `Taxable` dan `BonusEligible` dengan default method tepat |
| Multiple Interface | 15% | `FullTimeEmployee` mengimplementasikan 2 interface |
| Sealed Class | 15% | `EmployeeStatus` dengan `when` ekshaustif |
| Enkapsulasi & Polimorfisme | 15% | Properti private, polimorfisme pada `Company` |
| Kode & Output | 15% | Kode bersih, program berjalan, output sesuai |

---

## C. STUDI KASUS KELOMPOK
### “SISTEM MANAJEMEN PERPUSTAKAAN”

#### C.1. Latar Belakang
Perpustakaan kampus memiliki koleksi:
- **Buku** – bisa dipinjam, bisa dicari berdasarkan judul/penulis.
- **Majalah** – hanya bisa dicari, tidak dipinjam.
- **DVD** – bisa dipinjam, bisa dicari.

Setiap item memiliki ID, judul, tahun. Status item: Tersedia, Dipinjam (oleh siapa, tanggal), atau Hilang.

Sistem harus mampu:
- Menambah item ke koleksi.
- Mencari item berdasarkan kata kunci.
- Meminjam dan mengembalikan item yang borrowable.
- Menampilkan daftar item tersedia dan dipinjam.
- Menangani error (item tidak ditemukan, sudah dipinjam, dll).

#### C.2. Tujuan Pembelajaran
- Merancang **abstract class** dan **interface** secara kolaboratif.
- Menerapkan **multiple interface** pada kelas yang berbeda.
- Menggunakan **sealed class** untuk status item.
- Menerapkan **generic** (Repository) dan **collection**.
- Menerapkan **exception handling**.
- Melatih **kolaborasi** dan **integrasi kode**.

#### C.3. Pembagian Tugas Kelompok (3–4 Orang)
| Peran | Tugas |
|-------|-------|
| **Anggota 1 – Arsitek** | Mendesain abstract class `LibraryItem`, interface `Borrowable`, `Searchable`, sealed class `ItemStatus`. Membuat kerangka kelas. |
| **Anggota 2 – Implementator Buku & Majalah** | Implementasi `Book` dan `Magazine`. |
| **Anggota 3 – Implementator DVD & Manager** | Implementasi `DVD` dan `LibraryManager` (Repository, operasi pinjam/cari). |
| **Anggota 4 – Integrator & Exception** | Membuat custom exception, exception handling, dan `main()` program. |

> **Catatan:** Jika kelompok hanya 3 orang, Anggota 1 merangkap Anggota 4.

#### C.4. Spesifikasi Teknis

##### 1. Sealed Class `ItemStatus`
```kotlin
sealed class ItemStatus {
    object Available : ItemStatus()
    data class Borrowed(val by: String, val date: String) : ItemStatus()
    object Lost : ItemStatus()
    fun display(): String = when(this) {
        Available -> "Tersedia"
        is Borrowed -> "Dipinjam oleh $by pada $date"
        Lost -> "Hilang"
    }
}
```

##### 2. Abstract Class `LibraryItem`
```kotlin
abstract class LibraryItem(
    open val id: String,
    open val title: String,
    open val year: Int
) {
    abstract var status: ItemStatus
    abstract fun getDetails(): String
    open fun display() {
        println("[$id] $title ($year) - ${status.display()}")
        println("   Detail: ${getDetails()}")
    }
}
```

##### 3. Interface `Borrowable`
```kotlin
interface Borrowable {
    fun borrow(memberId: String, date: String): Boolean
    fun returnItem(): Boolean
    fun isAvailable(): Boolean
    fun getBorrower(): String?
}
```

##### 4. Interface `Searchable`
```kotlin
interface Searchable {
    fun matches(query: String): Boolean
}
```

##### 5. Subclass
| Subclass | Properti Tambahan | Interface |
|----------|-------------------|-----------|
| `Book` | `author: String`, `pages: Int` | `Borrowable`, `Searchable` |
| `Magazine` | `issueNumber: Int`, `publisher: String` | `Searchable` |
| `DVD` | `duration: Int`, `genre: String` | `Borrowable`, `Searchable` |

##### 6. Generic `Repository<T>`
```kotlin
class Repository<T : Any> {
    private val items = mutableListOf<T>()
    fun add(item: T) { items.add(item) }
    fun getAll(): List<T> = items.toList()
    fun find(predicate: (T) -> Boolean): T? = items.find(predicate)
    fun findAll(predicate: (T) -> Boolean): List<T> = items.filter(predicate)
}
```

##### 7. Custom Exception
- `ItemNotFoundException`
- `ItemAlreadyBorrowedException`
- `ItemNotBorrowedException`

##### 8. Kelas `LibraryManager` (Object Declaration)
| Komponen | Keterangan |
|----------|------------|
| Properti | `itemRepo: Repository<LibraryItem>` (private) |
| Metode | `addItem(item: LibraryItem)` <br> `findByTitle(query: String): List<LibraryItem>` <br> `borrowItem(itemId: String, memberId: String, date: String): Boolean` <br> `returnItem(itemId: String): Boolean` <br> `getAvailableItems(): List<LibraryItem>` <br> `getBorrowedItems(): List<LibraryItem>` <br> `displayAllItems()` |

#### C.5. Panduan Pengerjaan Kelompok

**Tahap 1 – Desain (30 menit)**
- Diskusikan bersama: buat class diagram sederhana di kertas/whiteboard.
- Tentukan pembagian tugas secara jelas.
- Pastikan semua anggota memahami antarmuka (method signature) yang akan digunakan.

**Tahap 2 – Implementasi Paralel (60 menit)**
- Setiap anggota mengerjakan bagiannya masing-masing.
- Gunakan repository Git sederhana (misal folder bersama) atau Google Drive untuk berbagi file.
- **Aturan:** Jangan mengubah method signature yang sudah disepakati tanpa persetujuan kelompok.

**Tahap 3 – Integrasi (30 menit)**
- Gabungkan semua file.
- Perbaiki error kompilasi.
- Uji fungsionalitas dasar.

**Tahap 4 – Penyempurnaan & Exception Handling (30 menit)**
- Tambahkan custom exception dan `runCatching` pada `LibraryManager`.
- Uji skenario error: pinjam item yang tidak ada, pinjam item yang sudah dipinjam, kembalikan item yang tidak dipinjam.

**Tahap 5 – Demo & Presentasi (30 menit)**
- Siapkan `main()` yang mendemonstrasikan semua fitur.
- Presentasikan hasil di depan kelas (10 menit per kelompok).

#### C.6. Output yang Diharapkan (Contoh)
```
=== SISTEM MANAJEMEN PERPUSTAKAAN ===
[P001] Pemrograman Kotlin (2023) - Tersedia
   Detail: Buku oleh Budi Santoso, 350 halaman
[P002] Dasar-Dasar OOP (2022) - Tersedia
   Detail: Buku oleh Siti Rahayu, 280 halaman
[M001] Tech Today (2024) - Tersedia
   Detail: Majalah edisi #42, diterbitkan oleh Tech Media
[D001] Film Dokumenter (2021) - Tersedia
   Detail: DVD, 120 menit, genre: Dokumenter

--- Meminjam Buku P001 oleh M001 ---
✅ Buku 'Pemrograman Kotlin' dipinjam oleh M001 pada 2025-01-15

--- Mencari 'Kotlin' ---
[P001] Pemrograman Kotlin (2023) - Dipinjam oleh M001 pada 2025-01-15

--- Mengembalikan Buku P001 ---
✅ Buku 'Pemrograman Kotlin' dikembalikan

--- Item Tersedia ---
[P001] Pemrograman Kotlin (2023) - Tersedia
[P002] Dasar-Dasar OOP (2022) - Tersedia
[M001] Tech Today (2024) - Tersedia
[D001] Film Dokumenter (2021) - Tersedia
```

#### C.7. Kriteria Penilaian Kelompok
| Kriteria | Bobot | Indikator |
|----------|-------|-----------|
| Abstract Class & Interface | 25% | `LibraryItem`, `Borrowable`, `Searchable` tepat |
| Multiple Interface | 15% | `Book` dan `DVD` mengimplementasikan 2 interface |
| Sealed Class | 10% | `ItemStatus` dengan `when` ekshaustif |
| Generic & Collection | 15% | `Repository<T>` digunakan, operasi filter/map |
| Exception Handling | 15% | Custom exception, `runCatching`, validasi |
| Kolaborasi & Integrasi | 10% | Pembagian tugas jelas, kode terintegrasi |
| Presentasi & Demo | 10% | Demo berjalan, presentasi jelas |

---

## D. PANDUAN UMUM PENGERJAAN

### D.1. Struktur File yang Disarankan
```
src/
├── Main.kt
├── model/
│   ├── Employee.kt (individu)
│   ├── LibraryItem.kt (kelompok)
│   ├── interfaces/
│   │   ├── Taxable.kt
│   │   ├── BonusEligible.kt
│   │   ├── Borrowable.kt
│   │   └── Searchable.kt
│   ├── status/
│   │   ├── EmployeeStatus.kt
│   │   └── ItemStatus.kt
│   ├── subclasses/
│   │   ├── FullTimeEmployee.kt
│   │   ├── ContractEmployee.kt
│   │   ├── Intern.kt
│   │   ├── Book.kt
│   │   ├── Magazine.kt
│   │   └── DVD.kt
│   └── manager/
│       ├── Company.kt
│       └── LibraryManager.kt
└── exception/
    └── CustomExceptions.kt
```

### D.2. Tips Pengerjaan
1. **Mulai dari kontrak (interface/abstract class)** sebelum implementasi.
2. **Gunakan `val` sebisa mungkin** untuk properti immutable.
3. **Manfaatkan `when` ekshaustif** pada sealed class.
4. **Test setiap kelas** secara terpisah sebelum integrasi.
5. **Gunakan `runCatching`** untuk operasi yang berpotensi error.
6. **Beri komentar** pada bagian kode yang kompleks.
7. **Untuk kelompok:** komunikasi rutin, gunakan version control sederhana, dan integrasi bertahap.

### D.3. Pertanyaan Refleksi (Setelah Selesai)
- Kapan sebaiknya menggunakan abstract class dibanding interface?
- Apa keuntungan default method pada interface?
- Bagaimana sealed class membantu menangani status?
- Apa tantangan terbesar saat mengerjakan secara kelompok?

---

**Disusun oleh,**
M Harry K S
Dosen Program Studi D4 Teknologi Rekayasa Informatika Industri
