# RENCANA PEMBELAJARAN SEMESTER (RPS)
## PERTEMUAN KE-3 — RENCANA PELAKSANAAN PEMBELAJARAN (RPP)
### PEMROGRAMAN BERORIENTASI OBJEK (OBJECT-ORIENTED PROGRAMMING)
### “Pewarisan (Inheritance) — Membangun Hierarki Kelas”

---

## A. IDENTITAS PERTEMUAN

| **Komponen** | **Keterangan** |
|---|---|
| **Pertemuan Ke-** | 3 |
| **Topik** | Pewarisan (Inheritance) — `open` Class, `override`, Constructor dalam Inheritance, `super` Keyword, dan Hierarki Kelas |
| **Durasi** | 8 Jam Praktik (480 menit) |
| **Hari/Tanggal** | [Disesuaikan] |
| **Ruang** | Laboratorium Komputer |
| **Dosen** | [Nama Dosen] |
| **Capaian Pembelajaran** | Mahasiswa memahami konsep pewarisan dalam OOP, mampu mengimplementasikan inheritance di Kotlin menggunakan keyword `open` dan `override`, memahami constructor dalam inheritance, serta mampu membangun hierarki kelas yang efisien dan reusable |

---

## B. CAPAIAN PEMBELAJARAN PERTEMUAN (CPP)

Setelah mengikuti pertemuan ke-3 ini, mahasiswa mampu:

1. **CPP 3.1:** Menjelaskan konsep pewarisan (inheritance) dan manfaatnya dalam pemrograman berorientasi objek.
2. **CPP 3.2:** Menjelaskan mengapa kelas di Kotlin bersifat `final` secara default dan kapan menggunakan keyword `open`.
3. **CPP 3.3:** Mengimplementasikan pewarisan kelas di Kotlin menggunakan sintaks `:` (colon).
4. **CPP 3.4:** Menggunakan keyword `override` untuk mengganti perilaku metode dan properti dari kelas induk.
5. **CPP 3.5:** Memahami dan mengimplementasikan constructor dalam hierarki pewarisan (primary dan secondary constructor).
6. **CPP 3.6:** Menggunakan keyword `super` untuk mengakses member kelas induk.
7. **CPP 3.7:** Memahami konsep single inheritance di Kotlin dan hierarki kelas `Any`.
8. **CPP 3.8:** Menerapkan pewarisan dalam studi kasus nyata (sistem kendaraan / sistem pegawai).

---

## C. MATERI POKOK

### 1. Pendahuluan: Apa itu Pewarisan (Inheritance)? (Sesi 1)

#### 1.1 Definisi Pewarisan

**Pewarisan (Inheritance)** adalah salah satu dari **empat pilar utama OOP** yang memungkinkan sebuah kelas (subclass/child class) untuk **mewarisi properti dan metode** dari kelas lain (superclass/parent class).

> **Definisi Sederhana:** Pewarisan adalah mekanisme di mana **“anak” mewarisi sifat dari “orang tua”** . Sebuah kelas turunan memiliki semua properti dan metode yang dimiliki oleh kelas induknya, dan dapat menambahkan atau mengubah perilaku sesuai kebutuhan.

#### 1.2 Analogi Pewarisan dalam Kehidupan Nyata

| **Analogi** | **Penjelasan** |
|---|---|
| **Hubungan Orang Tua-Anak** | Anak mewarisi sifat fisik (warna mata, tinggi) dan perilaku (cara bicara) dari orang tua, tetapi juga memiliki sifat dan perilaku uniknya sendiri. |
| **Kendaraan** | Semua kendaraan memiliki fitur dasar (roda, mesin, bisa bergerak). Mobil adalah kendaraan yang memiliki fitur tambahan (pintu, AC). Motor adalah kendaraan yang memiliki fitur berbeda (tanpa pintu, 2 roda). |
| **Hewan** | Semua hewan bernapas dan bergerak. Kucing adalah hewan yang bisa mengeong. Anjing adalah hewan yang bisa menggonggong. |
| **Perusahaan** | Semua pegawai memiliki nama, NIP, dan gaji. Pegawai Tetap adalah pegawai dengan tunjangan tetap. Pegawai Kontrak adalah pegawai dengan durasi kontrak. |

#### 1.3 Mengapa Pewarisan Penting?

| **Manfaat** | **Penjelasan** |
|---|---|
| **Reusability (Penggunaan Ulang)** | Kode yang sudah ditulis di kelas induk dapat digunakan kembali oleh semua kelas turunan, mengurangi duplikasi kode. |
| **Extensibility (Perluasan)** | Kelas turunan dapat menambahkan fungsionalitas baru tanpa mengubah kelas induk. |
| **Hierarki Konseptual** | Membuat struktur kelas yang mencerminkan hubungan "is-a" dalam dunia nyata (contoh: *Car is a Vehicle*). |
| **Polymorphism (Polimorfisme)** | Pewarisan adalah fondasi untuk polimorfisme—kemampuan objek berbeda untuk merespons pesan yang sama dengan cara berbeda. |
| **Maintainability** | Perubahan di kelas induk secara otomatis diwariskan ke semua kelas turunan. |

#### 1.4 Prinsip "IS-A" (Inheritance)

Pewarisan digunakan ketika ada hubungan **"IS-A"** (adalah) antara dua kelas:

- ✅ **Mobil IS-A Kendaraan** → Boleh menggunakan inheritance
- ✅ **Kucing IS-A Hewan** → Boleh menggunakan inheritance
- ✅ **Mahasiswa IS-A Manusia** → Boleh menggunakan inheritance
- ❌ **Mobil IS-A Mesin** → Tidak tepat (Mobil *memiliki* Mesin, bukan *adalah* Mesin) → gunakan komposisi

---

### 2. Kelas `Any` — Superclass Tertinggi di Kotlin (Sesi 1)

**Semua kelas di Kotlin secara implisit mewarisi dari kelas `Any`** [6†L11-L13].

```kotlin
// Kedua deklarasi ini SAMA SAJA

// Cara 1: Tanpa deklarasi superclass
class Contoh

// Cara 2: Eksplisit mewarisi dari Any
class Contoh : Any()
```

**Kelas `Any` menyediakan tiga metode yang diwarisi oleh semua kelas:** [6†L13]

| **Metode** | **Fungsi** |
|---|---|
| `toString()` | Mengembalikan representasi string dari objek |
| `equals()` | Membandingkan dua objek untuk kesamaan |
| `hashCode()` | Mengembalikan nilai hash code dari objek |

```kotlin
class Mahasiswa(val nama: String, val nim: String)

fun main() {
    val mhs = Mahasiswa("Budi", "12345")
    println(mhs.toString())  // Output: Mahasiswa@...(default, bisa di-override)
}
```

---

### 3. Keyword `open` — Membuka Kelas untuk Pewarisan (Sesi 1)

#### 3.1 Mengapa Kotlin Menggunakan `open`?

**Di Kotlin, semua kelas secara default adalah `final` — tidak bisa diwarisi** [1†L12-L14][2†L19-L21]. Ini adalah keputusan desain untuk:
- **Mencegah pewarisan yang tidak disengaja**
- **Membuat kode lebih mudah dipelihara (maintainable)**
- **Mengikuti prinsip "composition over inheritance"** [7†L17-L18]

> **Filosofi Kotlin:** "Jangan biarkan kelas diwarisi kecuali programmer secara eksplisit mengizinkannya."

#### 3.2 Sintaks `open`

Untuk membuat kelas bisa diwarisi, gunakan keyword **`open`** sebelum `class` [1†L13-L14][6†L15-L16][8†L10-L11]:

```kotlin
// ❌ Kelas ini TIDAK BISA diwarisi (final by default)
class Kendaraan {
    fun bergerak() {
        println("Kendaraan bergerak")
    }
}

// ✅ Kelas ini BISA diwarisi (open)
open class Kendaraan {
    fun bergerak() {
        println("Kendaraan bergerak")
    }
}
```

#### 3.3 `open` untuk Metode dan Properti

Tidak hanya kelas, **metode dan properti juga harus ditandai `open`** jika ingin di-override oleh subclass [6†L26-L29][2†L22-L23]:

```kotlin
open class Kendaraan {
    // Metode ini BISA di-override oleh subclass
    open fun bergerak() {
        println("Kendaraan bergerak")
    }

    // Metode ini TIDAK BISA di-override (final by default)
    fun berhenti() {
        println("Kendaraan berhenti")
    }
}
```

---

### 4. Sintaks Pewarisan di Kotlin (Sesi 1-2)

#### 4.1 Cara Membuat Subclass

Untuk membuat kelas yang mewarisi dari kelas lain, gunakan **tanda `:` (colon)** setelah nama kelas, diikuti dengan **panggilan constructor kelas induk** [8†L12-L16][1†L19-L22]:

```kotlin
// Kelas induk (parent class)
open class Kendaraan(val merek: String, val model: String)

// Kelas anak (child class) — mewarisi Kendaraan
class Mobil(merek: String, model: String, val jumlahPintu: Int) : Kendaraan(merek, model)

// Kelas anak lainnya
class Motor(merek: String, model: String, val jenis: String) : Kendaraan(merek, model)
```

#### 4.2 Contoh Lengkap

```kotlin
open class Kendaraan(val merek: String, val model: String) {
    open fun tampilkanInfo() {
        println("Kendaraan: $merek $model")
    }
}

class Mobil(merek: String, model: String, val jumlahPintu: Int) : Kendaraan(merek, model) {
    override fun tampilkanInfo() {
        println("Mobil: $merek $model, Pintu: $jumlahPintu")
    }
}

class Motor(merek: String, model: String, val jenis: String) : Kendaraan(merek, model) {
    override fun tampilkanInfo() {
        println("Motor: $merek $model, Jenis: $jenis")
    }
}

fun main() {
    val mobil = Mobil("Toyota", "Avanza", 4)
    val motor = Motor("Honda", "Beat", "Matic")

    mobil.tampilkanInfo()  // Output: Mobil: Toyota Avanza, Pintu: 4
    motor.tampilkanInfo()  // Output: Motor: Honda Beat, Jenis: Matic
}
```

---

### 5. Overriding Metode dan Properti (Sesi 2)

#### 5.1 Overriding Metode

**Overriding** adalah proses mengganti implementasi metode dari kelas induk di kelas anak [8†L25-L28].

**Aturan Overriding di Kotlin:** [6†L45-L47][8†L29-L35]

| **Aturan** | **Penjelasan** |
|---|---|
| Metode di kelas induk harus `open` | Jika tidak `open`, tidak bisa di-override |
| Metode di kelas anak harus `override` | Wajib menggunakan keyword `override` |
| Metode `override` bersifat `open` secara default | Bisa di-override lagi oleh subclass di bawahnya |
| Gunakan `final` untuk menghentikan overriding | `final override fun ...()` |

```kotlin
open class Hewan {
    open fun suara() {
        println("Hewan bersuara")
    }
}

class Kucing : Hewan() {
    override fun suara() {
        println("Meong! Meong!")
    }
}

class Anjing : Hewan() {
    override fun suara() {
        println("Guk! Guk!")
    }
}

fun main() {
    val kucing = Kucing()
    val anjing = Anjing()

    kucing.suara()  // Output: Meong! Meong!
    anjing.suara()  // Output: Guk! Guk!
}
```

#### 5.2 Overriding Properti

Properti juga bisa di-override dengan aturan yang sama:

```kotlin
open class Hewan {
    open val nama: String = "Hewan"
    open val suara: String = "..."
}

class Kucing : Hewan() {
    override val nama: String = "Kucing"
    override val suara: String = "Meong"
}

class Anjing : Hewan() {
    override val nama: String = "Anjing"
    override val suara: String = "Guk"
}

fun main() {
    val kucing = Kucing()
    println("${kucing.nama} bersuara ${kucing.suara}")  // Output: Kucing bersuara Meong
}
```

#### 5.3 Menghentikan Overriding dengan `final`

Jika Anda tidak ingin metode yang sudah di-override di-override lagi oleh subclass di bawahnya, gunakan `final` [6†L36-L38]:

```kotlin
open class Hewan {
    open fun suara() {
        println("Hewan bersuara")
    }
}

open class Kucing : Hewan() {
    // Metode ini BISA di-override oleh subclass Kucing
    override fun suara() {
        println("Meong!")
    }
}

class Anggora : Kucing() {
    // ✅ Bisa override karena suara() di Kucing masih open
    override fun suara() {
        println("Meong! Meong! (Anggora)")
    }
}

open class Anjing : Hewan() {
    // Metode ini TIDAK BISA di-override lagi
    final override fun suara() {
        println("Guk! Guk!")
    }
}

class Bulldog : Anjing() {
    // ❌ ERROR: 'suara' in 'Anjing' is final and cannot be overridden
    // override fun suara() { ... }
}
```

---

### 6. Keyword `super` — Mengakses Member Kelas Induk (Sesi 2)

Keyword **`super`** digunakan untuk mengakses member (properti atau metode) dari kelas induk [3†L18-L20].

#### 6.1 Menggunakan `super` untuk Memanggil Metode Induk

```kotlin
open class Hewan {
    open fun suara() {
        println("Hewan bersuara")
    }
}

class Kucing : Hewan() {
    override fun suara() {
        super.suara()  // Memanggil metode suara() dari Hewan
        println("Meong! Meong!")  // Menambahkan perilaku baru
    }
}

fun main() {
    val kucing = Kucing()
    kucing.suara()
    // Output:
    // Hewan bersuara
    // Meong! Meong!
}
```

#### 6.2 Menggunakan `super` untuk Mengakses Properti Induk

```kotlin
open class Manusia {
    open val jenis: String = "Manusia"
}

class Mahasiswa : Manusia() {
    override val jenis: String = "Mahasiswa"

    fun tampilkanJenis() {
        println("Jenis saya: ${super.jenis}")  // Mengakses properti dari Manusia
        println("Jenis sebagai mahasiswa: $jenis")  // Mengakses properti sendiri
    }
}

fun main() {
    val mhs = Mahasiswa()
    mhs.tampilkanJenis()
    // Output:
    // Jenis saya: Manusia
    // Jenis sebagai mahasiswa: Mahasiswa
}
```

---

### 7. Constructor dalam Inheritance (Sesi 2-3)

#### 7.1 Primary Constructor — Inisialisasi Kelas Induk

Jika kelas anak memiliki **primary constructor**, kelas induk **harus** diinisialisasi di primary constructor tersebut [6†L18-L20]:

```kotlin
// Kelas induk dengan primary constructor
open class Person(val nama: String, val umur: Int)

// Kelas anak dengan primary constructor
// Harus memanggil constructor Person(nama, umur)
class Mahasiswa(nama: String, umur: Int, val nim: String) : Person(nama, umur)

class Dosen(nama: String, umur: Int, val nip: String) : Person(nama, umur)

fun main() {
    val mhs = Mahasiswa("Budi", 20, "12345")
    val dosen = Dosen("Dr. Siti", 45, "67890")

    println("${mhs.nama} (${mhs.umur}) - NIM: ${mhs.nim}")
    println("${dosen.nama} (${dosen.umur}) - NIP: ${dosen.nip}")
}
```

#### 7.2 Secondary Constructor — Inisialisasi Kelas Induk

Jika kelas anak **tidak memiliki primary constructor**, setiap secondary constructor **harus** menginisialisasi kelas induk menggunakan `super` [6†L20-L24]:

```kotlin
open class View {
    constructor(ctx: Context) {
        // Inisialisasi dengan Context
    }
    constructor(ctx: Context, attrs: AttributeSet) {
        // Inisialisasi dengan Context dan AttributeSet
    }
}

// Kelas anak TANPA primary constructor
class MyView : View {
    // Secondary constructor 1 — memanggil constructor View(ctx)
    constructor(ctx: Context) : super(ctx)

    // Secondary constructor 2 — memanggil constructor View(ctx, attrs)
    constructor(ctx: Context, attrs: AttributeSet) : super(ctx, attrs)

    // Secondary constructor 3 — memanggil constructor lain di kelas ini
    constructor(ctx: Context, attrs: AttributeSet, defStyle: Int) : this(ctx, attrs)
}
```

#### 7.3 Urutan Inisialisasi

Saat objek dari kelas anak dibuat, **urutan inisialisasi** adalah [6†L18-L20]:

1. **Kelas induk** diinisialisasi terlebih dahulu (constructor + init block)
2. **Kelas anak** diinisialisasi setelahnya (constructor + init block)

```kotlin
open class Induk(val nama: String) {
    init {
        println("1. Init block Induk: $nama")
    }

    constructor(nama: String, umur: Int) : this(nama) {
        println("2. Secondary constructor Induk: $nama, $umur")
    }
}

class Anak(nama: String, umur: Int, val nim: String) : Induk(nama, umur) {
    init {
        println("3. Init block Anak: $nama, $nim")
    }

    constructor(nama: String, nim: String) : this(nama, 0, nim) {
        println("4. Secondary constructor Anak: $nama, $nim")
    }
}

fun main() {
    val anak = Anak("Budi", "12345")
    // Output:
    // 1. Init block Induk: Budi
    // 2. Secondary constructor Induk: Budi, 0
    // 3. Init block Anak: Budi, 12345
    // 4. Secondary constructor Anak: Budi, 12345
}
```

---

### 8. Single Inheritance di Kotlin (Sesi 3)

**Kotlin hanya mendukung single inheritance** — sebuah kelas hanya bisa mewarisi dari **satu** kelas induk [7†L19-L20][5†L53-L54].

```kotlin
// ✅ BENAR — single inheritance
open class A
class B : A()  // B mewarisi dari A

// ❌ SALAH — multiple inheritance (tidak didukung di Kotlin)
// class C : A(), B()  // ERROR!
```

> **Catatan:** Meskipun single inheritance, Kotlin mendukung **multiple interface implementation** (akan dipelajari di pertemuan 5 tentang Abstraksi dan Interface).

---

### 9. Studi Kasus: Sistem Manajemen Pegawai (Sesi 3-4)

Mari kita bangun sistem manajemen pegawai yang mengimplementasikan semua konsep pewarisan.

#### 9.1 Analisis Kebutuhan

| **Jenis Pegawai** | **Atribut** | **Perilaku** |
|---|---|---|
| **Pegawai (Base)** | Nama, NIP, Gaji Pokok | Menghitung gaji, menampilkan info |
| **Pegawai Tetap** | Nama, NIP, Gaji Pokok, Tunjangan | Gaji = Gaji Pokok + Tunjangan |
| **Pegawai Kontrak** | Nama, NIP, Gaji Pokok, Durasi Kontrak | Gaji = Gaji Pokok (tidak ada tunjangan) |
| **Pegawai Harian** | Nama, NIP, Upah Harian, Jumlah Hari Kerja | Gaji = Upah Harian × Jumlah Hari Kerja |

#### 9.2 Implementasi Lengkap

```kotlin
/**
 * ============================================================
 * SISTEM MANAJEMEN PEGAWAI DENGAN PEWARISAN
 * ============================================================
 * Studi kasus komprehensif untuk mendemonstrasikan:
 * 1. Inheritance dengan open class
 * 2. Overriding metode dan properti
 * 3. Constructor dalam inheritance
 * 4. Keyword super
 * 5. Hierarki kelas dengan single inheritance
 * ============================================================
 */

/**
 * KELAS INDUK: Pegawai
 *
 * Semua pegawai memiliki atribut dasar dan perilaku umum.
 * Kelas ini bersifat open agar bisa diwarisi.
 */
open class Pegawai(
    open val nama: String,
    open val nip: String,
    open val gajiPokok: Double
) {
    // Init block untuk logging saat objek dibuat
    init {
        println("📋 Pegawai $nama dengan NIP $nip terdaftar")
    }

    // Metode open — bisa di-override oleh subclass
    open fun hitungGaji(): Double {
        return gajiPokok
    }

    // Metode open — bisa di-override oleh subclass
    open fun tampilkanInfo() {
        println("=" .repeat(50))
        println("👤 INFO PEGAWAI")
        println("=" .repeat(50))
        println("Nama       : $nama")
        println("NIP        : $nip")
        println("Gaji Pokok : Rp ${formatRupiah(gajiPokok)}")
        println("Total Gaji : Rp ${formatRupiah(hitungGaji())}")
        println("=" .repeat(50))
    }

    // Helper method untuk format Rupiah
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
 * SUBCLASS 1: PegawaiTetap
 *
 * Pegawai tetap memiliki tunjangan di samping gaji pokok.
 */
class PegawaiTetap(
    nama: String,
    nip: String,
    gajiPokok: Double,
    val tunjangan: Double
) : Pegawai(nama, nip, gajiPokok) {

    // Override properti — menambahkan informasi tambahan
    override val nama: String
        get() = super.nama + " (Tetap)"

    // Override metode hitungGaji
    override fun hitungGaji(): Double {
        return super.hitungGaji() + tunjangan
    }

    // Override metode tampilkanInfo
    override fun tampilkanInfo() {
        super.tampilkanInfo()  // Memanggil method dari Pegawai
        println("Tunjangan  : Rp ${formatRupiah(tunjangan)}")
        println("Status     : Pegawai Tetap")
        println("=" .repeat(50))
    }
}

/**
 * SUBCLASS 2: PegawaiKontrak
 *
 * Pegawai kontrak memiliki durasi kontrak dan tidak mendapat tunjangan.
 */
class PegawaiKontrak(
    nama: String,
    nip: String,
    gajiPokok: Double,
    val durasiKontrak: Int  // dalam bulan
) : Pegawai(nama, nip, gajiPokok) {

    // Override properti
    override val nama: String
        get() = super.nama + " (Kontrak)"

    // Override metode tampilkanInfo
    override fun tampilkanInfo() {
        super.tampilkanInfo()
        println("Durasi     : $durasiKontrak bulan")
        println("Status     : Pegawai Kontrak")
        println("=" .repeat(50))
    }
}

/**
 * SUBCLASS 3: PegawaiHarian
 *
 * Pegawai harian dibayar berdasarkan jumlah hari kerja.
 * Gaji = upahHarian × jumlahHariKerja
 */
class PegawaiHarian(
    nama: String,
    nip: String,
    val upahHarian: Double,
    val jumlahHariKerja: Int
) : Pegawai(nama, nip, 0.0) {  // Gaji pokok 0 karena menggunakan upah harian

    // Override properti
    override val nama: String
        get() = super.nama + " (Harian)"

    // Override gajiPokok — dihitung dari upah harian
    override val gajiPokok: Double
        get() = upahHarian * jumlahHariKerja

    // Override metode hitungGaji
    override fun hitungGaji(): Double {
        return upahHarian * jumlahHariKerja
    }

    // Override metode tampilkanInfo
    override fun tampilkanInfo() {
        println("=" .repeat(50))
        println("👤 INFO PEGAWAI HARIAN")
        println("=" .repeat(50))
        println("Nama          : $nama")
        println("NIP           : $nip")
        println("Upah Harian   : Rp ${formatRupiah(upahHarian)}")
        println("Jumlah Hari   : $jumlahHariKerja hari")
        println("Total Gaji    : Rp ${formatRupiah(hitungGaji())}")
        println("Status        : Pegawai Harian")
        println("=" .repeat(50))
    }
}

/**
 * SUBCLASS 4: PegawaiManager (menunjukkan pewarisan bertingkat)
 *
 * Manager adalah pegawai tetap dengan tunjangan manajemen tambahan.
 */
class PegawaiManager(
    nama: String,
    nip: String,
    gajiPokok: Double,
    tunjangan: Double,
    val tunjanganManajemen: Double
) : PegawaiTetap(nama, nip, gajiPokok, tunjangan) {

    // Override properti
    override val nama: String
        get() = super.nama.replace(" (Tetap)", "") + " (Manager)"

    // Override metode hitungGaji
    override fun hitungGaji(): Double {
        return super.hitungGaji() + tunjanganManajemen
    }

    // Override metode tampilkanInfo
    override fun tampilkanInfo() {
        super.tampilkanInfo()
        println("Tunj. Manajemen: Rp ${formatRupiah(tunjanganManajemen)}")
        println("Jabatan       : Manager")
        println("=" .repeat(50))
    }
}

/**
 * KELAS UTAMA — DEMO SISTEM MANAJEMEN PEGAWAI
 */
fun main() {
    println("=" .repeat(55))
    println("🏢 SISTEM MANAJEMEN PEGAWAI")
    println("=" .repeat(55))
    println()

    // Membuat berbagai jenis pegawai
    val pegawai1 = PegawaiTetap("Budi Santoso", "P001", 5_000_000.0, 1_500_000.0)
    val pegawai2 = PegawaiKontrak("Siti Rahayu", "P002", 4_500_000.0, 12)
    val pegawai3 = PegawaiHarian("Ahmad Fauzi", "P003", 150_000.0, 20)
    val pegawai4 = PegawaiManager("Dr. Dewi Lestari", "P004", 8_000_000.0, 2_000_000.0, 3_000_000.0)

    println()
    println("--- DAFTAR PEGAWAI ---")
    println()

    // Tampilkan info semua pegawai
    pegawai1.tampilkanInfo()
    println()
    pegawai2.tampilkanInfo()
    println()
    pegawai3.tampilkanInfo()
    println()
    pegawai4.tampilkanInfo()

    // Demonstrasi polimorfisme (akan diperdalam di pertemuan 4)
    println()
    println("--- DEMONSTRASI POLIMORFISME ---")
    val daftarPegawai: List<Pegawai> = listOf(pegawai1, pegawai2, pegawai3, pegawai4)
    println("Total pegawai: ${daftarPegawai.size}")
    println("Total gaji semua pegawai: Rp ${formatRupiah(daftarPegawai.sumOf { it.hitungGaji() })}")

    // Demonstrasi bahwa pewarisan tidak bisa dilakukan tanpa open
    println()
    println("--- DEMONSTRASI ATURAN PEWARISAN ---")
    println("✅ Kelas Pegawai ditandai 'open' sehingga bisa diwarisi")
    println("✅ Metode di Pegawai ditandai 'open' sehingga bisa di-override")
    println("✅ Subclass menggunakan 'override' untuk mengganti perilaku")

    println()
    println("=" .repeat(55))
    println("🏁 PROGRAM SELESAI")
    println("=" .repeat(55))
}

// Helper function untuk format Rupiah (top-level)
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

### Sesi 1: Pengantar & Teori Pewarisan + `open` Keyword (2 Jam — 120 menit)

| **Waktu** | **Kegiatan** | **Detail** | **Metode** |
|---|---|---|---|
| **0-10'** | Pembukaan & Review | • Dosen membuka perkuliahan dengan salam dan doa<br>• Review singkat materi pertemuan 2 (enkapsulasi, access modifier, getter/setter)<br>• Menghubungkan enkapsulasi dengan pewarisan | Ceramah interaktif, Tanya jawab |
| **10-40'** | Konsep Pewarisan | • **Definisi pewarisan** — mekanisme mewarisi properti dan metode dari kelas induk<br>• **Analogi pewarisan** (orang tua-anak, kendaraan, hewan, pegawai)<br>• **Prinsip IS-A** — kapan menggunakan inheritance<br>• **Manfaat pewarisan** — reusability, extensibility, hierarki, polymorphism<br>• **Single inheritance** di Kotlin — hanya bisa mewarisi dari satu kelas<br>• **Kelas `Any`** — superclass tertinggi semua kelas di Kotlin | Ceramah, Analogi, Diskusi |
| **40-70'** | Keyword `open` | • **Mengapa kelas di Kotlin final by default?** — mencegah pewarisan tidak disengaja<br>• **Sintaks `open`** untuk kelas, metode, dan properti<br>• **Perbedaan** kelas `open` vs `final`<br>• Demo kode: mencoba mewarisi kelas tanpa `open` → error<br>• Demo kode: mewarisi kelas dengan `open` → berhasil | Ceramah, Demonstrasi, Live Coding |
| **70-90'** | Praktik `open` Keyword | • Mahasiswa membuat kelas `Hewan` dengan `open`<br>• Membuat subclass `Kucing` dan `Anjing` yang mewarisi `Hewan`<br>• Mengamati bahwa properti dan metode dari `Hewan` tersedia di subclass | Praktik terbimbing |
| **90-120'** | Diskusi & Review | • Diskusi kelompok: "Kapan sebaiknya sebuah kelas dibuat `open` dan kapan `final`?"<br>• Dosen memberikan contoh kasus nyata<br>• Q&A dan penyimpulan | Diskusi kelompok, Tanya jawab |

---

### Sesi 2: Sintaks Pewarisan, Overriding, dan `super` (2 Jam — 120 menit)

| **Waktu** | **Kegiatan** | **Detail** | **Metode** |
|---|---|---|---|
| **0-10'** | Review Singkat | • Mereview `open` keyword<br>• Menghubungkan dengan sintaks pewarisan | Ceramah |
| **10-40'** | Sintaks Pewarisan | • **Cara membuat subclass** — menggunakan `:` (colon)<br>• **Memanggil constructor kelas induk** — `: NamaInduk(param) `<br>• **Parameter di subclass** — harus meneruskan parameter ke induk<br>• Demo: Membuat kelas `Kendaraan` → `Mobil` → `Motor`<br>• Mahasiswa mengikuti live coding | Ceramah, Demonstrasi, Live Coding |
| **40-70'** | Overriding Metode & Properti | • **Konsep overriding** — mengganti perilaku dari kelas induk<br>• **Aturan overriding**: metode induk `open`, metode anak `override`<br>• **Overriding properti** — properti juga bisa di-override<br>• **`final override`** — menghentikan overriding lebih lanjut<br>• Demo: Overriding metode `suara()` di `Kucing` dan `Anjing`<br>• Demo: Overriding properti `nama` dan `suara` | Ceramah, Demonstrasi, Live Coding |
| **70-90'** | Keyword `super` | • **Konsep `super`** — mengakses member kelas induk<br>• **`super` untuk memanggil metode induk** — `super.namaMetode()`<br>• **`super` untuk mengakses properti induk** — `super.namaProperti`<br>• Demo: Memanggil `super.suara()` sebelum menambahkan perilaku baru<br>• Demo: Mengakses `super.nama` untuk mendapatkan nilai dari induk | Ceramah, Demonstrasi |
| **90-120'** | Praktik Overriding & `super` | • Mahasiswa membuat hierarki kelas `Hewan` → `Kucing` → `Anggora`<br>• Mengimplementasikan overriding di setiap level<br>• Menggunakan `super` untuk memanggil metode induk<br>• Dosen berkeliling memberikan asistensi | Praktik mandiri, Asistensi |

---

### Sesi 3: Constructor dalam Inheritance & Hierarki Lanjutan (2 Jam — 120 menit)

| **Waktu** | **Kegiatan** | **Detail** | **Metode** |
|---|---|---|---|
| **0-10'** | Review & Motivasi | • Review overriding dan `super`<br>• "Bagaimana constructor bekerja dalam pewarisan?" | Ceramah |
| **10-45'** | Constructor dalam Inheritance | • **Primary constructor** — kelas induk harus diinisialisasi di primary constructor<br>• **Secondary constructor** — setiap secondary constructor harus memanggil `super`<br>• **Urutan inisialisasi** — induk dulu, baru anak<br>• Demo: Primary constructor dengan pewarisan<br>• Demo: Secondary constructor dengan pewarisan<br>• Demo: Urutan inisialisasi dengan `init` block | Ceramah, Demonstrasi, Live Coding |
| **45-75'** | Hierarki Kelas Lanjutan | • **Pewarisan bertingkat** — Grandparent → Parent → Child<br>• **Single inheritance** — hanya satu induk<br>• **Kelas `Any`** — superclass tertinggi<br>• Demo: Membuat hierarki 3 tingkat<br>• Demo: Mengakses `toString()` dari `Any` | Ceramah, Demonstrasi |
| **75-90'** | Praktik Constructor & Hierarki | • Mahasiswa membuat hierarki `Manusia` → `Mahasiswa` → `MahasiswaS2`<br>• Mengimplementasikan constructor di setiap level<br>• Mengamati urutan inisialisasi | Praktik mandiri |
| **90-120'** | Diskusi Kasus | • Diskusi: "Apa perbedaan pewarisan di Kotlin vs Java?"<br>• Dosen menjelaskan perbedaan (final by default vs tidak)<br>• Q&A dan penyimpulan | Diskusi, Tanya jawab |

---

### Sesi 4: Studi Kasus & Tugas 3 (2 Jam — 120 menit)

| **Waktu** | **Kegiatan** | **Detail** | **Metode** |
|---|---|---|---|
| **0-15'** | Review Materi Pertemuan 3 | • Rangkuman seluruh materi:<br>  - Pewarisan dan konsep IS-A<br>  - `open` keyword untuk kelas dan member<br>  - Sintaks pewarisan dengan `:` (colon)<br>  - Overriding dengan `override`<br>  - `super` untuk mengakses induk<br>  - Constructor dalam inheritance<br>  - Single inheritance dan kelas `Any`<br>• Menjawab pertanyaan mahasiswa | Review, Tanya jawab |
| **15-45'** | Studi Kasus: Sistem Pegawai | • Dosen menjelaskan studi kasus sistem manajemen pegawai (lihat bagian C.9)<br>• Menganalisis kebutuhan dan hierarki kelas<br>• Dosen melakukan live coding bersama mahasiswa<br>• Menjelaskan setiap bagian kode | Demonstrasi, Live Coding, Diskusi |
| **45-90'** | Pengerjaan Tugas 3 | • Mahasiswa mengerjakan Tugas 3 secara mandiri (lihat bagian E)<br>• Dosen berkeliling memberikan bimbingan intensif<br>• Mahasiswa dapat bertanya jika mengalami kendala | Praktik mandiri, Asistensi intensif |
| **90-105'** | Pengumpulan & Presentasi | • Mahasiswa mengumpulkan Tugas 3<br>• 2-3 mahasiswa diminta mempresentasikan kodenya<br>• Dosen memberikan feedback konstruktif | Presentasi, Feedback |
| **105-120'** | Penutupan | • Dosen merangkum pencapaian pertemuan 3<br>• Preview materi pertemuan 4 (Polimorfisme)<br>• Memberikan tugas membaca modul pertemuan 4<br>• Menutup perkuliahan dengan doa dan salam | Ceramah |

---

## E. TUGAS 3 (Dikumpulkan)

### Sistem Manajemen Toko Online dengan Pewarisan

Buatlah program lengkap sistem manajemen toko online dengan ketentuan berikut:

#### 1. Kelas `Product` (Produk) — Kelas Induk

| **Komponen** | **Spesifikasi** |
|---|---|
| **Properti** | `id: String` (read-only)<br>`nama: String` (read-only)<br>`harga: Double` (read-only)<br>`stok: Int` (bisa diubah) |
| **Metode** | `hitungDiskon(): Double` → mengembalikan diskon (default: 0.0)<br>`hitungHargaJual(): Double` → harga setelah diskon (harga - diskon)<br>`tampilkanInfo(): String` → menampilkan info produk<br>`kurangiStok(jumlah: Int): Boolean` → mengurangi stok jika tersedia |

#### 2. Subclass `Elektronik` — Produk Elektronik

| **Komponen** | **Spesifikasi** |
|---|---|
| **Properti Tambahan** | `garansi: Int` (dalam bulan)<br>`daya: Int` (dalam Watt) |
| **Overriding** | `hitungDiskon()` → diskon 10% jika garansi > 12 bulan |

#### 3. Subclass `Makanan` — Produk Makanan

| **Komponen** | **Spesifikasi** |
|---|---|
| **Properti Tambahan** | `tanggalKadaluarsa: String`<br>`berat: Double` (dalam gram) |
| **Overriding** | `hitungDiskon()` → diskon 20% jika tanggal kadaluarsa kurang dari 7 hari |

#### 4. Subclass `Pakaian` — Produk Pakaian

| **Komponen** | **Spesifikasi** |
|---|---|
| **Properti Tambahan** | `ukuran: String` (S, M, L, XL)<br>`bahan: String` |
| **Overriding** | `hitungDiskon()` → diskon 15% jika ukuran XL |

#### 5. Kelas `Toko`

| **Komponen** | **Spesifikasi** |
|---|---|
| **Properti** | `nama: String` (read-only)<br>`daftarProduk: MutableList<Product>` (private) |
| **Metode** | `tambahProduk(product: Product)`<br>`cariProduk(keyword: String): List<Product>`<br>`tampilkanSemuaProduk()`<br>`tampilkanProdukByKategori(kategori: String)` — "Elektronik", "Makanan", "Pakaian" |

#### 6. Fungsi `main()`

- Buat objek `Toko` dengan nama "Toko Serba Ada"
- Tambahkan **minimal 6 produk** (2 dari setiap kategori)
- Tampilkan semua produk
- Tampilkan produk yang sedang diskon
- Lakukan pembelian (kurangi stok) beberapa produk
- Tampilkan status akhir semua produk

#### 7. Kriteria Penilaian Tugas 3

| **Kriteria** | **Bobot** | **Indikator** |
|---|---|---|
| **Hierarki Pewarisan** | 30% | • Kelas induk `Product` menggunakan `open`<br>• Subclass mewarisi dengan benar menggunakan `:`<br>• Constructor inheritance diimplementasikan dengan benar |
| **Overriding** | 25% | • Metode `hitungDiskon()` di-override di semua subclass<br>• Menggunakan `super` dengan tepat<br>• Overriding properti jika diperlukan |
| **Fungsi main()** | 20% | • Menampilkan semua skenario yang diminta<br>• Output jelas dan informatif |
| **Kode Berkualitas** | 15% | • Kode bersih, terstruktur, diberi komentar<br>• Menggunakan naming convention yang benar |
| **Program Berjalan** | 10% | • Program berjalan tanpa error<br>• Semua fungsi berfungsi sesuai spesifikasi |

---

## F. MEDIA DAN ALAT PEMBELAJARAN

| **Media** | **Keterangan** |
|---|---|
| **Laptop/PC** | Setiap mahasiswa menggunakan laptop/PC masing-masing |
| **IntelliJ IDEA** | IDE utama untuk pengembangan Kotlin |
| **JDK** | Java Development Kit (versi 11 atau 17) |
| **Proyektor/LCD** | Untuk presentasi dan demonstrasi dosen |
| **Whiteboard** | Untuk menjelaskan konsep dan hierarki kelas |
| **Modul Praktikum** | Modul cetak/digital pertemuan 3 |
| **Kotlin Playground** | Alternatif untuk mencoba kode tanpa instalasi |

---

## G. PENILAIAN PERTEMUAN 3

| **Komponen** | **Bobot** | **Indikator** | **Teknik** |
|---|---|---|---|
| **Keaktifan Sesi 1-3** | 15% dari total keaktifan | • Kehadiran tepat waktu<br>• Partisipasi dalam diskusi dan tanya jawab<br>• Keterlibatan dalam praktik kelompok | Observasi |
| **Tugas 3** | 100% dari nilai tugas 3 | • Lihat kriteria penilaian Tugas 3 di atas | Penilaian kode |
| **Kuis Singkat** | Bonus | • Pertanyaan tentang `open`, `override`, `super`, dan constructor inheritance | Tes tertulis/lisan |

---

## H. REFERENSI PERTEMUAN 3

### Referensi Utama:

1. **Kotlin Official Documentation – Inheritance** — [https://kotlinlang.org/docs/inheritance.html](https://kotlinlang.org/docs/inheritance.html)

2. **Kotlin Official Documentation – Open and Special Classes** — [https://kotlinlang.org/docs/kotlin-tour-intermediate-open-special-classes.html](https://kotlinlang.org/docs/kotlin-tour-intermediate-open-special-classes.html)

3. **Kotlin Official Documentation – Classes and Interfaces** — [https://kotlinlang.org/docs/kotlin-tour-intermediate-classes-interfaces.html](https://kotlinlang.org/docs/kotlin-tour-intermediate-classes-interfaces.html)

### Referensi Pendukung:

4. **Baeldung – Open Keyword in Kotlin** — [https://www.baeldung.com/kotlin/open-keyword](https://www.baeldung.com/kotlin/open-keyword)

5. **Kotlin `super` Keyword** — [https://kotlinlang.org/docs/inheritance.html#calling-the-superclass-implementation](https://kotlinlang.org/docs/inheritance.html#calling-the-superclass-implementation)

6. **Android Developers – Kotlin Inheritance** — [https://developer.android.com/kotlin/learn](https://developer.android.com/kotlin/learn)

---

## I. LAMPIRAN

### Lampiran 1: Perbandingan Inheritance di Kotlin vs Java

| **Aspek** | **Kotlin** | **Java** |
|---|---|---|
| **Default kelas** | `final` (tidak bisa diwarisi) | Bisa diwarisi (kecuali `final`) |
| **Keyword untuk inheritance** | `:` (colon) | `extends` |
| **Keyword untuk override** | `override` (wajib) | `@Override` (opsional, annotation) |
| **Member default** | `final` (tidak bisa di-override) | Bisa di-override (kecuali `final`) |
| **Keyword untuk membuka** | `open` | (tidak ada — default sudah terbuka) |
| **Superclass tertinggi** | `Any` | `Object` |
| **Single inheritance** | ✅ Ya | ✅ Ya |

### Lampiran 2: Checklist Pemahaman Mahasiswa

| **No** | **Konsep** | **Paham** | **Kurang Paham** | **Tidak Paham** |
|---|---|---|---|---|
| 1 | Definisi pewarisan (inheritance) | ☐ | ☐ | ☐ |
| 2 | Prinsip IS-A | ☐ | ☐ | ☐ |
| 3 | Manfaat pewarisan | ☐ | ☐ | ☐ |
| 4 | Kelas `Any` sebagai superclass tertinggi | ☐ | ☐ | ☐ |
| 5 | Keyword `open` untuk kelas | ☐ | ☐ | ☐ |
| 6 | Keyword `open` untuk metode/properti | ☐ | ☐ | ☐ |
| 7 | Sintaks pewarisan dengan `:` (colon) | ☐ | ☐ | ☐ |
| 8 | Memanggil constructor kelas induk | ☐ | ☐ | ☐ |
| 9 | Overriding metode dengan `override` | ☐ | ☐ | ☐ |
| 10 | Overriding properti | ☐ | ☐ | ☐ |
| 11 | Keyword `super` | ☐ | ☐ | ☐ |
| 12 | Constructor dalam inheritance | ☐ | ☐ | ☐ |
| 13 | Single inheritance di Kotlin | ☐ | ☐ | ☐ |
| 14 | Hierarki kelas bertingkat | ☐ | ☐ | ☐ |

### Lampiran 3: Kode Dasar — Hierarki Hewan (Solusi Referensi)

```kotlin
/**
 * ============================================================
 * HIERARKI HEWAN — DEMONSTRASI PEWARISAN
 * ============================================================
 */

// Kelas induk — open agar bisa diwarisi
open class Hewan(
    open val nama: String,
    open val umur: Int
) {
    init {
        println("🐾 Hewan $nama (umur $umur tahun) dibuat")
    }

    open fun suara() {
        println("$nama bersuara")
    }

    open fun info() {
        println("Nama: $nama, Umur: $umur tahun")
    }
}

// Subclass 1: Mamalia
open class Mamalia(
    nama: String,
    umur: Int,
    open val jenisMamalia: String
) : Hewan(nama, umur) {

    override fun suara() {
        println("$nama (Mamalia $jenisMamalia) bersuara")
    }

    override fun info() {
        super.info()
        println("Jenis Mamalia: $jenisMamalia")
    }
}

// Subclass 2: Kucing (mewarisi Mamalia)
class Kucing(
    nama: String,
    umur: Int,
    jenisMamalia: String,
    val warna: String
) : Mamalia(nama, umur, jenisMamalia) {

    override val nama: String
        get() = super.nama + " (Kucing)"

    override fun suara() {
        super.suara()
        println("   Meong! Meong!")
    }

    override fun info() {
        super.info()
        println("Warna: $warna")
    }
}

// Subclass 3: Anjing (mewarisi Mamalia)
class Anjing(
    nama: String,
    umur: Int,
    jenisMamalia: String,
    val ras: String
) : Mamalia(nama, umur, jenisMamalia) {

    override val nama: String
        get() = super.nama + " (Anjing)"

    override fun suara() {
        super.suara()
        println("   Guk! Guk!")
    }

    override fun info() {
        super.info()
        println("Ras: $ras")
    }
}

// Subclass 4: Burung (langsung mewarisi Hewan)
class Burung(
    nama: String,
    umur: Int,
    val bisaTerbang: Boolean
) : Hewan(nama, umur) {

    override val nama: String
        get() = super.nama + " (Burung)"

    override fun suara() {
        println("$nama berkicau: Cuit! Cuit!")
    }

    override fun info() {
        super.info()
        println("Bisa Terbang: ${if (bisaTerbang) "Ya" else "Tidak"}")
    }
}

fun main() {
    println("=" .repeat(50))
    println("🐾 DEMO HIERARKI HEWAN")
    println("=" .repeat(50))
    println()

    val kucing = Kucing("Milo", 3, "Karnivora", "Orange")
    val anjing = Anjing("Rex", 5, "Karnivora", "German Shepherd")
    val burung = Burung("Tweety", 2, true)

    println()
    println("--- INFO HEWAN ---")
    println()
    kucing.info()
    println()
    anjing.info()
    println()
    burung.info()

    println()
    println("--- SUARA HEWAN ---")
    println()
    kucing.suara()
    println()
    anjing.suara()
    println()
    burung.suara()

    // Demonstrasi bahwa tidak bisa meng-override metode final
    println()
    println("--- DEMONSTRASI ATURAN ---")
    println("✅ Kelas Hewan dan Mamalia bersifat 'open' sehingga bisa diwarisi")
    println("✅ Metode suara() dan info() bersifat 'open' sehingga bisa di-override")
    println("✅ Subclass menggunakan 'override' untuk mengganti perilaku")

    println()
    println("=" .repeat(50))
    println("🏁 PROGRAM SELESAI")
    println("=" .repeat(50))
}
```

---

**Disusun oleh,**
[Nama Dosen Pengampu]
Dosen Program Studi D4 Teknologi Rekayasa Informatika Industri
