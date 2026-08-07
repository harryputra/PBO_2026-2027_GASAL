# MATERI AJAR PERTEMUAN 3
## PEMROGRAMAN BERORIENTASI OBJEK (OOP) DENGAN KOTLIN
### “Pewarisan (Inheritance) — Membangun Hierarki Kelas yang Kuat dan Reusable”

---

# BAGIAN 1: KONSEP DASAR PEWARISAN

## 1.1 Apa itu Pewarisan (Inheritance)?

**Pewarisan (Inheritance)** adalah salah satu dari **empat pilar utama** dalam Pemrograman Berorientasi Objek (OOP), bersama dengan Encapsulation (Enkapsulasi), Polymorphism (Polimorfisme), dan Abstraction (Abstraksi).

Secara definisi, pewarisan adalah mekanisme yang memungkinkan sebuah kelas (disebut **subclass** atau **child class**) untuk **mewarisi properti dan metode** dari kelas lain (disebut **superclass** atau **parent class**).

> **Definisi Sederhana:** Pewarisan adalah mekanisme di mana **“anak” mewarisi sifat dari “orang tua”** . Sebuah kelas turunan memiliki semua properti dan metode yang dimiliki oleh kelas induknya, dan dapat menambahkan atau mengubah perilaku sesuai kebutuhan.

---

## 1.2 Analogi Pewarisan dalam Kehidupan Nyata

Untuk memahami pewarisan, mari kita lihat beberapa analogi dari kehidupan sehari-hari:

### A. Hubungan Orang Tua-Anak

| **Komponen** | **Analogi dalam OOP** |
|---|---|
| **Orang Tua** | Superclass (kelas induk) |
| **Anak** | Subclass (kelas anak) |
| **Sifat fisik (warna mata, tinggi)** | Properti yang diwarisi |
| **Cara bicara, perilaku dasar** | Metode yang diwarisi |
| **Bakat/talenta unik anak** | Properti/metode tambahan di subclass |
| **Cara bicara yang berbeda** | Overriding (mengubah perilaku yang diwarisi) |

### B. Kendaraan

| **Komponen** | **Analogi dalam OOP** |
|---|---|
| **Kendaraan** | Superclass |
| **Mobil, Motor, Bus** | Subclass |
| **Roda, mesin, bisa bergerak** | Properti/metode yang diwarisi |
| **Mobil memiliki pintu, AC** | Properti tambahan di subclass Mobil |
| **Motor memiliki 2 roda** | Properti tambahan di subclass Motor |

### C. Hewan

| **Komponen** | **Analogi dalam OOP** |
|---|---|
| **Hewan** | Superclass |
| **Kucing, Anjing, Burung** | Subclass |
| **Bernapas, bergerak** | Metode yang diwarisi |
| **Kucing mengeong** | Overriding metode `suara()` |
| **Anjing menggonggong** | Overriding metode `suara()` |

### D. Perusahaan

| **Komponen** | **Analogi dalam OOP** |
|---|---|
| **Pegawai** | Superclass |
| **Pegawai Tetap, Pegawai Kontrak** | Subclass |
| **Nama, NIP, gaji** | Properti yang diwarisi |
| **Pegawai Tetap memiliki tunjangan** | Properti tambahan |

---

## 1.3 Prinsip "IS-A" — Kapan Menggunakan Pewarisan?

Pewarisan digunakan ketika ada hubungan **"IS-A"** (adalah) antara dua kelas:

| **Hubungan** | **Apakah IS-A?** | **Keputusan** |
|---|---|---|
| Mobil **adalah** Kendaraan | ✅ Ya | Gunakan inheritance |
| Kucing **adalah** Hewan | ✅ Ya | Gunakan inheritance |
| Mahasiswa **adalah** Manusia | ✅ Ya | Gunakan inheritance |
| Mobil **adalah** Mesin | ❌ Tidak (Mobil *memiliki* Mesin) | Gunakan komposisi, BUKAN inheritance |
| Restoran **adalah** Bangunan | ✅ Ya | Gunakan inheritance |
| Restoran **adalah** Dapur | ❌ Tidak (Restoran *memiliki* Dapur) | Gunakan komposisi |

> **Penting:** Jika hubungannya adalah **"HAS-A"** (memiliki), gunakan **komposisi**, bukan pewarisan! Misalnya, Mobil *memiliki* Mesin → jangan gunakan inheritance.

---

## 1.4 Mengapa Pewarisan Sangat Penting?

Pewarisan memberikan banyak manfaat dalam pengembangan perangkat lunak:

| **Manfaat** | **Penjelasan** | **Contoh** |
|---|---|---|
| **Reusability (Penggunaan Ulang)** | Kode yang sudah ditulis di kelas induk dapat digunakan kembali oleh semua kelas turunan, mengurangi duplikasi kode | Semua subclass Pegawai menggunakan properti `nama`, `nip` dari kelas induk |
| **Extensibility (Perluasan)** | Kelas turunan dapat menambahkan fungsionalitas baru tanpa mengubah kelas induk | PegawaiTetap menambahkan properti `tunjangan` |
| **Hierarki Konseptual** | Membuat struktur kelas yang mencerminkan hubungan dunia nyata | Hierarki: Kendaraan → Mobil → Sedan |
| **Polymorphism (Polimorfisme)** | Pewarisan adalah fondasi untuk polimorfisme—kemampuan objek berbeda untuk merespons pesan yang sama dengan cara berbeda | Semua Pegawai bisa `hitungGaji()`, tapi cara menghitungnya berbeda |
| **Maintainability** | Perubahan di kelas induk secara otomatis diwariskan ke semua kelas turunan | Mengubah format `tampilkanInfo()` di Pegawai akan mempengaruhi semua subclass |

---

## 1.5 Single Inheritance di Kotlin

**Kotlin hanya mendukung single inheritance** — sebuah kelas hanya bisa mewarisi dari **satu** kelas induk.

```kotlin
// ✅ BENAR — single inheritance
open class A
class B : A()  // B mewarisi dari A

// ❌ SALAH — multiple inheritance (tidak didukung di Kotlin)
// class C : A(), B()  // ERROR! Tidak bisa mewarisi dari dua kelas
```

> **Catatan:** Meskipun single inheritance, Kotlin mendukung **multiple interface implementation** (akan dipelajari di pertemuan 5 tentang Abstraksi dan Interface).

---

# BAGIAN 2: KELAS `Any` — SUPERCLASS TERTINGGI DI KOTLIN

## 2.1 Apa itu Kelas `Any`?

**Semua kelas di Kotlin secara implisit mewarisi dari kelas `Any`** .

```kotlin
// Kedua deklarasi ini SAMA SAJA

// Cara 1: Tanpa deklarasi superclass (implisit mewarisi Any)
class Contoh

// Cara 2: Eksplisit mewarisi dari Any
class Contoh : Any()
```

## 2.2 Metode dari Kelas `Any`

Kelas `Any` menyediakan **tiga metode** yang diwarisi oleh semua kelas di Kotlin:

| **Metode** | **Fungsi** | **Contoh Penggunaan** |
|---|---|---|
| `toString()` | Mengembalikan representasi string dari objek | `println(obj.toString())` |
| `equals(other: Any?)` | Membandingkan dua objek untuk kesamaan | `if (obj1.equals(obj2))` |
| `hashCode()` | Mengembalikan nilai hash code dari objek | Untuk digunakan dalam collection seperti HashMap |

### Contoh Penggunaan `toString()` dari `Any`

```kotlin
class Mahasiswa(val nama: String, val nim: String)

fun main() {
    val mhs = Mahasiswa("Budi", "12345")
    println(mhs.toString())
    // Output: Mahasiswa@...(default — alamat memori)
    // Kita bisa meng-override toString() untuk output yang lebih bermakna
}
```

### Overriding Metode dari `Any`

Karena metode di `Any` bersifat `open`, kita bisa meng-override-nya:

```kotlin
class Mahasiswa(val nama: String, val nim: String) {
    // Override toString() dari Any
    override fun toString(): String {
        return "Mahasiswa(nama='$nama', nim='$nim')"
    }

    // Override equals() dari Any
    override fun equals(other: Any?): Boolean {
        if (this === other) return true
        if (other !is Mahasiswa) return false
        return nim == other.nim
    }

    // Override hashCode() dari Any
    override fun hashCode(): Int {
        return nim.hashCode()
    }
}

fun main() {
    val mhs1 = Mahasiswa("Budi", "12345")
    val mhs2 = Mahasiswa("Budi", "12345")

    println(mhs1.toString())  // Output: Mahasiswa(nama='Budi', nim='12345')
    println(mhs1 == mhs2)     // Output: true (karena equals di-override)
}
```

---

# BAGIAN 3: KEYWORD `OPEN` — MEMBUKA KELAS UNTUK PEWARISAN

## 3.1 Mengapa Kotlin Menggunakan `open`?

**Di Kotlin, semua kelas secara default adalah `final` — tidak bisa diwarisi.**

Ini adalah keputusan desain yang sangat penting dari Kotlin, dengan alasan:

| **Alasan** | **Penjelasan** |
|---|---|
| **Mencegah pewarisan yang tidak disengaja** | Programmer harus secara eksplisit mengizinkan pewarisan |
| **Membuat kode lebih mudah dipelihara** | Kelas yang tidak dirancang untuk diwarisi tidak akan diwarisi |
| **Mengikuti prinsip "composition over inheritance"** | Mendorong penggunaan komposisi daripada pewarisan yang berlebihan |
| **Keamanan** | Mencegah subclass merusak invariant kelas induk |

> **Filosofi Kotlin:** "Jangan biarkan kelas diwarisi kecuali programmer secara eksplisit mengizinkannya."

## 3.2 Sintaks `open` untuk Kelas

Untuk membuat kelas bisa diwarisi, gunakan keyword **`open`** sebelum `class`:

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

### Mencoba Mewarisi Kelas Tanpa `open`

```kotlin
// Kelas tanpa open — TIDAK BISA diwarisi
class Kendaraan {
    fun bergerak() {
        println("Kendaraan bergerak")
    }
}

// ❌ ERROR: This type is final, so it cannot be inherited from
class Mobil : Kendaraan() {
    // ...
}
```

## 3.3 `open` untuk Metode dan Properti

Tidak hanya kelas, **metode dan properti juga harus ditandai `open`** jika ingin di-override oleh subclass:

```kotlin
open class Kendaraan {
    // ✅ Metode ini BISA di-override oleh subclass
    open fun bergerak() {
        println("Kendaraan bergerak")
    }

    // ❌ Metode ini TIDAK BISA di-override (final by default)
    fun berhenti() {
        println("Kendaraan berhenti")
    }

    // ✅ Properti ini BISA di-override oleh subclass
    open val jenis: String = "Kendaraan Umum"

    // ❌ Properti ini TIDAK BISA di-override (final by default)
    val tahunProduksi: Int = 2024
}
```

## 3.4 Ringkasan Aturan `open`

| **Elemen** | **Default** | **Untuk Membuka** |
|---|---|---|
| **Kelas** | `final` (tidak bisa diwarisi) | Gunakan `open` |
| **Metode** | `final` (tidak bisa di-override) | Gunakan `open` |
| **Properti** | `final` (tidak bisa di-override) | Gunakan `open` |
| **Metode di `Any`** | `open` (bisa di-override) | - |

---

# BAGIAN 4: SINTAKS PEWARISAN DI KOTLIN

## 4.1 Cara Membuat Subclass

Untuk membuat kelas yang mewarisi dari kelas lain, gunakan **tanda `:` (colon)** setelah nama kelas, diikuti dengan **panggilan constructor kelas induk**:

```kotlin
// Kelas induk (parent class) — harus open
open class Kendaraan(val merek: String, val model: String)

// Kelas anak (child class) — mewarisi Kendaraan
class Mobil(merek: String, model: String, val jumlahPintu: Int) : Kendaraan(merek, model)

// Kelas anak lainnya
class Motor(merek: String, model: String, val jenis: String) : Kendaraan(merek, model)
```

### Penjelasan Sintaks

```kotlin
class NamaSubclass(parameterSubclass) : NamaSuperclass(parameterSuperclass)
```

| **Bagian** | **Penjelasan** |
|---|---|
| `class NamaSubclass` | Mendeklarasikan kelas anak |
| `(parameterSubclass)` | Parameter untuk constructor kelas anak |
| `:` | Tanda "mewarisi dari" |
| `NamaSuperclass(parameterSuperclass)` | Memanggil constructor kelas induk dengan parameter yang sesuai |

## 4.2 Contoh Lengkap

```kotlin
// Kelas induk — open agar bisa diwarisi
open class Kendaraan(val merek: String, val model: String) {
    open fun tampilkanInfo() {
        println("Kendaraan: $merek $model")
    }
}

// Kelas anak 1 — Mobil
class Mobil(merek: String, model: String, val jumlahPintu: Int) : Kendaraan(merek, model) {
    override fun tampilkanInfo() {
        println("Mobil: $merek $model, Pintu: $jumlahPintu")
    }
}

// Kelas anak 2 — Motor
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

## 4.3 Parameter di Subclass

Perhatikan bahwa parameter di subclass **tidak perlu** menggunakan `val`/`var` jika hanya diteruskan ke superclass:

```kotlin
open class Person(val nama: String, val umur: Int)

// ✅ BENAR — parameter diteruskan ke superclass, tidak perlu val/var
class Mahasiswa(nama: String, umur: Int, val nim: String) : Person(nama, umur)

// ❌ SALAH — tidak perlu val/var untuk parameter yang hanya diteruskan
// TAPI ini juga BISA (hanya redundant)
class Mahasiswa(val nama: String, val umur: Int, val nim: String) : Person(nama, umur)
//                                              ^^^^^^      ^^^^^^
//                                              Ini redundant karena sudah di Person
```

---

# BAGIAN 5: OVERRIDING METODE DAN PROPERTI

## 5.1 Apa itu Overriding?

**Overriding** adalah proses mengganti implementasi metode atau properti dari kelas induk di kelas anak.

> **Overriding** memungkinkan subclass untuk memberikan **implementasi spesifik** untuk metode yang sudah didefinisikan di superclass.

## 5.2 Aturan Overriding di Kotlin

Kotlin memiliki aturan yang ketat untuk overriding:

| **Aturan** | **Penjelasan** |
|---|---|
| Metode di kelas induk harus `open` | Jika tidak `open`, tidak bisa di-override |
| Metode di kelas anak harus `override` | Wajib menggunakan keyword `override` |
| Metode `override` bersifat `open` secara default | Bisa di-override lagi oleh subclass di bawahnya |
| Gunakan `final` untuk menghentikan overriding | `final override fun ...()` |

## 5.3 Overriding Metode

```kotlin
open class Hewan {
    // Metode ini BISA di-override
    open fun suara() {
        println("Hewan bersuara")
    }

    // Metode ini TIDAK BISA di-override (final by default)
    fun makan() {
        println("Hewan makan")
    }
}

class Kucing : Hewan() {
    // Wajib menggunakan keyword override
    override fun suara() {
        println("Meong! Meong!")
    }

    // ❌ ERROR: 'makan' in 'Hewan' is final and cannot be overridden
    // override fun makan() { ... }
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

## 5.4 Overriding Properti

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
    println("${kucing.nama} bersuara ${kucing.suara}")
    // Output: Kucing bersuara Meong
}
```

### Overriding Properti dengan Custom Getter

```kotlin
open class Person {
    open val greeting: String
        get() = "Hello!"
}

class IndonesianPerson : Person() {
    override val greeting: String
        get() = "Halo!"  // Mengubah perilaku getter
}

class JapanesePerson : Person() {
    override val greeting: String
        get() = "Konnichiwa!"
}

fun main() {
    val person1 = IndonesianPerson()
    val person2 = JapanesePerson()

    println(person1.greeting)  // Output: Halo!
    println(person2.greeting)  // Output: Konnichiwa!
}
```

## 5.5 Menghentikan Overriding dengan `final`

Jika Anda tidak ingin metode yang sudah di-override di-override lagi oleh subclass di bawahnya, gunakan `final`:

```kotlin
open class Hewan {
    open fun suara() {
        println("Hewan bersuara")
    }
}

open class Kucing : Hewan() {
    // Metode ini BISA di-override oleh subclass Kucing (masih open)
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

## 5.6 Praktik Terbaik Overriding Properti

Menurut dokumentasi Kotlin, **tidak disarankan** untuk meng-override properti di kelas open.

**❌ Kurang Disarankan — Overriding Properti:**
```kotlin
open class Vehicle(val make: String, val model: String) {
    open val transmissionType: String = "Manual"
}

class Car(make: String, model: String, val numberOfDoors: Int) : Vehicle(make, model) {
    override val transmissionType: String = "Automatic"
}
```

**✅ Lebih Disarankan — Parameter di Constructor:**
```kotlin
open class Vehicle(
    val make: String,
    val model: String,
    val transmissionType: String = "Manual"
)

class Car(
    make: String,
    model: String,
    val numberOfDoors: Int
) : Vehicle(make, model, "Automatic")
```

> **Pesan:** Akses properti secara langsung, bukan dengan override, menghasilkan kode yang lebih sederhana dan mudah dibaca.

---

# BAGIAN 6: KEYWORD `SUPER` — MENGAKSES KELAS INDUK

## 6.1 Apa itu Keyword `super`?

Keyword **`super`** digunakan untuk mengakses member (properti atau metode) dari kelas induk.

## 6.2 Menggunakan `super` untuk Memanggil Metode Induk

```kotlin
open class Hewan {
    open fun suara() {
        println("Hewan bersuara")
    }
}

class Kucing : Hewan() {
    override fun suara() {
        super.suara()  // ✅ Memanggil metode suara() dari Hewan
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

## 6.3 Menggunakan `super` untuk Mengakses Properti Induk

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

## 6.4 Menggunakan `super` untuk Memanggil Constructor Induk

`super` juga digunakan di secondary constructor untuk memanggil constructor kelas induk:

```kotlin
open class View {
    constructor(ctx: Context) {
        // Inisialisasi dengan Context
    }
    constructor(ctx: Context, attrs: AttributeSet) {
        // Inisialisasi dengan Context dan AttributeSet
    }
}

class MyView : View {
    // Secondary constructor memanggil superclass constructor
    constructor(ctx: Context) : super(ctx)

    constructor(ctx: Context, attrs: AttributeSet) : super(ctx, attrs)
}
```

---

# BAGIAN 7: CONSTRUCTOR DALAM INHERITANCE

## 7.1 Primary Constructor — Inisialisasi Kelas Induk

Jika kelas anak memiliki **primary constructor**, kelas induk **harus** diinisialisasi di primary constructor tersebut:

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

## 7.2 Secondary Constructor — Inisialisasi Kelas Induk

Jika kelas anak **tidak memiliki primary constructor**, setiap secondary constructor **harus** menginisialisasi kelas induk menggunakan `super`:

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

## 7.3 Urutan Inisialisasi

Saat objek dari kelas anak dibuat, **urutan inisialisasi** adalah:

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

### Visualisasi Urutan Inisialisasi

```
┌─────────────────────────────────────────────────────────────┐
│                    MEMBUAT OBJEK ANAK                      │
├─────────────────────────────────────────────────────────────┤
│  1. Memory dialokasikan untuk objek                        │
│  2. Properti kelas induk diinisialisasi                    │
│  3. Init block kelas induk dijalankan                      │
│  4. Constructor kelas induk dijalankan                     │
│  5. Properti kelas anak diinisialisasi                     │
│  6. Init block kelas anak dijalankan                       │
│  7. Constructor kelas anak dijalankan                      │
└─────────────────────────────────────────────────────────────┘
```

---

# BAGIAN 8: PEWARISAN BERTINGKAT (MULTI-LEVEL INHERITANCE)

## 8.1 Konsep Pewarisan Bertingkat

Kotlin mendukung **pewarisan bertingkat** — sebuah kelas bisa mewarisi dari kelas yang juga mewarisi dari kelas lain, membentuk hierarki.

```
Any (superclass tertinggi)
  ↑
Animal
  ↑
Mammal
  ↑
Cat
  ↑
PersianCat
```

## 8.2 Contoh Pewarisan Bertingkat

```kotlin
// Level 1: Hewan
open class Hewan(val nama: String) {
    open fun suara() {
        println("$nama bersuara")
    }
}

// Level 2: Mamalia (mewarisi Hewan)
open class Mamalia(nama: String, val jenisMamalia: String) : Hewan(nama) {
    override fun suara() {
        println("$nama (Mamalia $jenisMamalia) bersuara")
    }
}

// Level 3: Kucing (mewarisi Mamalia)
open class Kucing(nama: String, jenisMamalia: String, val warna: String)
    : Mamalia(nama, jenisMamalia) {
    override fun suara() {
        super.suara()  // Memanggil suara() dari Mamalia
        println("   Meong! Meong!")
    }
}

// Level 4: Anggora (mewarisi Kucing)
class Anggora(nama: String, jenisMamalia: String, warna: String, val asal: String)
    : Kucing(nama, jenisMamalia, warna) {
    override fun suara() {
        super.suara()  // Memanggil suara() dari Kucing
        println("   (Anggora dari $asal)")
    }
}

fun main() {
    val anggora = Anggora("Milo", "Karnivora", "Putih", "Turki")
    anggora.suara()
    // Output:
    // Milo (Mamalia Karnivora) bersuara
    //    Meong! Meong!
    //    (Anggora dari Turki)
}
```

## 8.3 Hierarki Kelas di Kotlin

```
                    ┌─────────────────┐
                    │       Any       │
                    │ (superclass     │
                    │  tertinggi)     │
                    └────────┬────────┘
                             │
                    ┌────────┴────────┐
                    │                 │
              ┌─────┴─────┐    ┌──────┴──────┐
              │  Vehicle  │    │   Animal    │
              └─────┬─────┘    └──────┬──────┘
                    │                 │
         ┌──────────┼──────────┐      │
    ┌────┴────┐┌────┴────┐┌────┴────┐ │
    │  Car    ││  Motor  ││  Bus    │ │
    └─────────┘└─────────┘└─────────┘ │
                               ┌──────┴──────┐
                               │   Mammal    │
                               └──────┬──────┘
                                      │
                               ┌──────┴──────┐
                               │    Cat      │
                               └──────┬──────┘
                                      │
                               ┌──────┴──────┐
                               │  Anggora    │
                               └─────────────┘
```

---

# BAGIAN 9: STUDI KASUS — SISTEM MANAJEMEN PEGAWAI

## 9.1 Analisis Kebutuhan

Kita akan membangun sistem manajemen pegawai dengan hierarki pewarisan.

| **Jenis Pegawai** | **Atribut** | **Perilaku** |
|---|---|---|
| **Pegawai (Base)** | Nama, NIP, Gaji Pokok | Menghitung gaji, menampilkan info |
| **Pegawai Tetap** | + Tunjangan | Gaji = Gaji Pokok + Tunjangan |
| **Pegawai Kontrak** | + Durasi Kontrak | Gaji = Gaji Pokok |
| **Pegawai Harian** | + Upah Harian, Jumlah Hari | Gaji = Upah Harian × Jumlah Hari |
| **Pegawai Manager** | + Tunjangan Manajemen | Gaji = Gaji Pokok + Tunjangan + Tunjangan Manajemen |

## 9.2 Implementasi Lengkap

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
 * 6. Pewarisan bertingkat
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

    // Helper method untuk format Rupiah (protected — bisa diakses subclass)
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

# BAGIAN 10: PERBANDINGAN KOTLIN VS JAVA

## 10.1 Perbedaan Inheritance di Kotlin dan Java

| **Aspek** | **Kotlin** | **Java** |
|---|---|---|
| **Default kelas** | `final` (tidak bisa diwarisi)  | Bisa diwarisi (kecuali `final`) |
| **Keyword untuk inheritance** | `:` (colon)  | `extends` |
| **Keyword untuk override** | `override` (wajib)  | `@Override` (opsional, annotation) |
| **Member default** | `final` (tidak bisa di-override)  | Bisa di-override (kecuali `final`) |
| **Keyword untuk membuka** | `open`  | (tidak ada — default sudah terbuka) |
| **Superclass tertinggi** | `Any`  | `Object` |
| **Single inheritance** | ✅ Ya  | ✅ Ya |

## 10.2 Contoh Perbandingan Kode

**Java:**
```java
// Di Java, kelas bisa diwarisi secara default
public class Vehicle {
    public void move() {
        System.out.println("Vehicle is moving");
    }
}

// Tidak perlu keyword khusus untuk inheritance
public class Car extends Vehicle {
    @Override  // Optional annotation
    public void move() {
        System.out.println("Car is moving");
    }
}
```

**Kotlin:**
```kotlin
// Di Kotlin, kelas harus ditandai open
open class Vehicle {
    open fun move() {
        println("Vehicle is moving")
    }
}

// Harus menggunakan : dan override
class Car : Vehicle() {
    override fun move() {  // override wajib
        println("Car is moving")
    }
}
```

---

# BAGIAN 11: LATIHAN DAN TUGAS

## 11.1 Latihan Mandiri

### Latihan 1: Hierarki Bentuk (Shapes)

Buatlah hierarki kelas untuk bentuk geometris:

```kotlin
// 1. Kelas induk: Shape
//    - Properti: name: String
//    - Metode: luas(): Double (open, default return 0.0)
//    - Metode: tampilkanInfo()

// 2. Subclass: Rectangle
//    - Properti tambahan: panjang: Double, lebar: Double
//    - Override luas(): panjang * lebar

// 3. Subclass: Circle
//    - Properti tambahan: jariJari: Double
//    - Override luas(): π * r²

// 4. Subclass: Triangle
//    - Properti tambahan: alas: Double, tinggi: Double
//    - Override luas(): 0.5 * alas * tinggi

// 5. Di main(), buat objek dari semua subclass dan tampilkan luasnya
```

### Latihan 2: Hierarki Produk

Buatlah hierarki kelas untuk produk di toko:

```kotlin
// 1. Kelas induk: Product
//    - Properti: id: String, name: String, price: Double
//    - Metode: getDiscountedPrice(): Double (open, default return price)

// 2. Subclass: ElectronicProduct
//    - Properti tambahan: warrantyMonths: Int
//    - Override getDiscountedPrice(): diskon 10% jika warranty > 12 bulan

// 3. Subclass: FoodProduct
//    - Properti tambahan: expiryDate: String
//    - Override getDiscountedPrice(): diskon 20% jika mendekati kadaluarsa

// 4. Subclass: ClothingProduct
//    - Properti tambahan: size: String, material: String
//    - Override getDiscountedPrice(): diskon 15% jika size = "XL"
```

## 11.2 Tugas 3 (Dikumpulkan)

### Sistem Manajemen Kendaraan dengan Pewarisan

Buatlah program lengkap sistem manajemen kendaraan dengan ketentuan berikut:

#### 1. Kelas `Vehicle` (Kendaraan) — Kelas Induk

| **Komponen** | **Spesifikasi** |
|---|---|
| **Properti** | `brand: String` (read-only)<br>`model: String` (read-only)<br>`year: Int` (read-only)<br>`price: Double` (read-only)<br>`isSold: Boolean` (private setter — default false) |
| **Metode** | `calculateTax(): Double` (open — pajak = 10% dari harga)<br>`sell(): Boolean` — menandai kendaraan sebagai sold<br>`displayInfo(): String` — menampilkan info kendaraan<br>`isAvailable(): Boolean` — cek ketersediaan |

#### 2. Subclass `Car` — Mobil

| **Komponen** | **Spesifikasi** |
|---|---|
| **Properti Tambahan** | `numberOfDoors: Int`<br>`fuelType: String` ("Bensin", "Diesel", "Listrik") |
| **Overriding** | `calculateTax()` — pajak = 12% dari harga (lebih tinggi) |

#### 3. Subclass `Motorcycle` — Motor

| **Komponen** | **Spesifikasi** |
|---|---|
| **Properti Tambahan** | `engineCapacity: Int` (dalam cc)<br>`type: String` ("Sport", "Cruiser", "Matic") |
| **Overriding** | `calculateTax()` — pajak = 5% dari harga (lebih rendah) |

#### 4. Subclass `Truck` — Truk (menunjukkan pewarisan bertingkat)

| **Komponen** | **Spesifikasi** |
|---|---|
| **Properti Tambahan** | `loadCapacity: Double` (dalam ton)<br>`numberOfAxles: Int` |
| **Overriding** | `calculateTax()` — pajak = 15% dari harga (tertinggi) |

#### 5. Kelas `Dealership` (Dealer)

| **Komponen** | **Spesifikasi** |
|---|---|
| **Properti** | `name: String` (read-only)<br>`vehicles: MutableList<Vehicle>` (private) |
| **Metode** | `addVehicle(vehicle: Vehicle)`<br>`findVehicle(brand: String, model: String): Vehicle?`<br>`sellVehicle(brand: String, model: String): Boolean`<br>`getAvailableVehicles(): List<Vehicle>`<br>`getSoldVehicles(): List<Vehicle>`<br>`displayAllVehicles()`<br>`displayAvailableVehicles()`<br>`getTotalRevenue(): Double` (total harga kendaraan yang terjual) |

#### 6. Fungsi `main()`

- Buat objek `Dealership` dengan nama "Dealer Motor Jaya"
- Tambahkan **minimal 6 kendaraan** (2 mobil, 2 motor, 2 truk)
- Tampilkan semua kendaraan
- Tampilkan kendaraan yang tersedia
- Lakukan penjualan beberapa kendaraan
- Tampilkan kendaraan yang tersisa dan total pendapatan

#### 7. Kriteria Penilaian Tugas 3

| **Kriteria** | **Bobot** | **Indikator** |
|---|---|---|
| **Hierarki Pewarisan** | 30% | • Kelas induk `Vehicle` menggunakan `open`<br>• Subclass mewarisi dengan benar menggunakan `:`<br>• Constructor inheritance diimplementasikan dengan benar |
| **Overriding** | 25% | • Metode `calculateTax()` di-override di semua subclass<br>• Menggunakan `super` dengan tepat<br>• Overriding properti jika diperlukan |
| **Fungsi main()** | 20% | • Menampilkan semua skenario yang diminta<br>• Output jelas dan informatif |
| **Kode Berkualitas** | 15% | • Kode bersih, terstruktur, diberi komentar<br>• Menggunakan naming convention yang benar |
| **Program Berjalan** | 10% | • Program berjalan tanpa error<br>• Semua fungsi berfungsi sesuai spesifikasi |

---

# BAGIAN 12: RINGKASAN MATERI PERTEMUAN 3

## 12.1 Poin-Poin Penting

| **Konsep** | **Penjelasan** | **Keyword/Sintaks** |
|---|---|---|
| **Pewarisan (Inheritance)** | Mekanisme mewarisi properti dan metode dari kelas induk  | - |
| **Prinsip IS-A** | Gunakan inheritance jika ada hubungan "adalah" | - |
| **Single Inheritance** | Hanya bisa mewarisi dari satu kelas  | - |
| **Kelas `Any`** | Superclass tertinggi semua kelas di Kotlin  | `class Contoh : Any()` |
| **`open`** | Membuka kelas/member untuk diwarisi/di-override  | `open class Base` |
| **Sintaks Pewarisan** | Menggunakan `:` (colon)  | `class Child : Parent()` |
| **`override`** | Mengganti implementasi dari kelas induk  | `override fun method()` |
| **`super`** | Mengakses member dari kelas induk  | `super.method()` |
| **`final`** | Menghentikan overriding lebih lanjut  | `final override fun method()` |
| **Constructor** | Inisialisasi kelas induk di constructor anak  | `class Child : Parent(params)` |

## 12.2 Kapan Menggunakan Apa?

| **Skenario** | **Solusi** | **Contoh** |
|---|---|---|
| Ingin membuat kelas yang bisa diwarisi | Gunakan `open` pada kelas | `open class Vehicle` |
| Ingin membuat metode yang bisa di-override | Gunakan `open` pada metode | `open fun calculateTax()` |
| Ingin mengganti perilaku metode induk | Gunakan `override` | `override fun calculateTax()` |
| Ingin mengakses metode/properti induk | Gunakan `super` | `super.calculateTax()` |
| Ingin mencegah override lebih lanjut | Gunakan `final` | `final override fun method()` |
| Ingin membuat hierarki kelas | Gunakan inheritance dengan `:` | `class Car : Vehicle()` |
| Hubungan "memiliki" (HAS-A) | Gunakan komposisi, BUKAN inheritance | `class Car { val engine = Engine() }` |

---

# BAGIAN 13: REFERENSI

## 13.1 Referensi Utama

1. **Kotlin Official Documentation – Inheritance** — [https://kotlinlang.org/docs/inheritance.html](https://kotlinlang.org/docs/inheritance.html)

2. **Kotlin Official Documentation – Open and Special Classes** — [https://kotlinlang.org/docs/kotlin-tour-intermediate-open-special-classes.html](https://kotlinlang.org/docs/kotlin-tour-intermediate-open-special-classes.html)

3. **Kotlin Official Documentation – Classes and Interfaces** — [https://kotlinlang.org/docs/kotlin-tour-intermediate-classes-interfaces.html](https://kotlinlang.org/docs/kotlin-tour-intermediate-classes-interfaces.html)

## 13.2 Referensi Pendukung

4. **Baeldung – Open Keyword in Kotlin** — [https://www.baeldung.com/kotlin/open-keyword](https://www.baeldung.com/kotlin/open-keyword)

5. **Kotlin `super` Keyword** — [https://kotlinlang.org/docs/inheritance.html#calling-the-superclass-implementation](https://kotlinlang.org/docs/inheritance.html#calling-the-superclass-implementation)

6. **Android Developers – Kotlin Inheritance** — [https://developer.android.com/kotlin/learn](https://developer.android.com/kotlin/learn)

---

# BAGIAN 14: PENUTUP

## 14.1 Pesan untuk Mahasiswa

> **“Pewarisan adalah cara untuk membangun hubungan 'IS-A' dalam kode Anda. Gunakan dengan bijak—jangan memaksakan pewarisan jika hubungannya sebenarnya 'HAS-A'.”**

Pertemuan 3 ini adalah **fondasi** untuk memahami hierarki kelas dan reusability kode. Dengan memahami pewarisan, Anda bisa:

- **Mengurangi duplikasi kode** — tulis sekali, gunakan di banyak tempat
- **Membangun hierarki yang alami** — mencerminkan hubungan dunia nyata
- **Mempersiapkan polimorfisme** — yang akan dipelajari di pertemuan 4
- **Menulis kode yang lebih terstruktur** — mudah dipahami dan dipelihara

**Ingatlah:**
1. Pewarisan adalah tentang hubungan **"IS-A"** , bukan "HAS-A"
2. **`open`** adalah kunci — tanpa `open`, tidak ada pewarisan
3. **`override`** wajib — tidak seperti Java, Kotlin memaksa Anda untuk eksplisit
4. **Single inheritance** — hanya satu induk, gunakan interface untuk multiple
5. **Komposisi > Inheritance** — jika ragu, gunakan komposisi

## 14.2 Persiapan untuk Pertemuan 4

**Materi berikutnya: POLIMORFISME (Polymorphism)**

Apa yang akan dipelajari:
1. Konsep polimorfisme — banyak bentuk untuk satu interface
2. Polymorphic references — referensi superclass ke objek subclass
3. Method overloading dan overriding
4. Upcasting dan downcasting
5. Smart casting di Kotlin
6. Studi kasus: sistem pembayaran dengan berbagai metode

**Tugas persiapan:**
- Baca modul tentang Polimorfisme
- Review kembali konsep inheritance dari pertemuan 3
- Pastikan semua latihan pertemuan 3 sudah selesai

---

**Disusun oleh,**
[Nama Dosen Pengampu]
Dosen Program Studi D4 Teknologi Rekayasa Informatika Industri
