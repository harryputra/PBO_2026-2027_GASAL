# MATERI AJAR PERTEMUAN 2

## PEMROGRAMAN BERORIENTASI OBJEK (OOP) DENGAN KOTLIN

### “Enkapsulasi — Melindungi Data dari Dunia Luar”

---

# BAGIAN 1: KONSEP DASAR ENKAPSULASI

## 1.1 Apa itu Enkapsulasi?

**Enkapsulasi (Encapsulation)** adalah salah satu dari **empat pilar utama** dalam Pemrograman Berorientasi Objek (OOP), bersama dengan Inheritance (Pewarisan), Polymorphism (Polimorfisme), dan Abstraction (Abstraksi).

Secara definisi, enkapsulasi adalah mekanisme untuk **membungkus data (atribut) dan metode (perilaku)** yang beroperasi pada data tersebut ke dalam satu unit (kelas), serta **menyembunyikan detail implementasi internal** dari dunia luar.

> **Definisi Sederhana:** Enkapsulasi adalah **“mengunci” data di dalam kelas** sehingga tidak bisa diakses atau diubah secara sembarangan dari luar. Hanya metode-metode yang disediakan oleh kelas yang boleh mengakses dan mengubah data tersebut.

---

## 1.2 Analogi Enkapsulasi dalam Kehidupan Nyata

Untuk memahami enkapsulasi, mari kita lihat beberapa analogi dari kehidupan sehari-hari:

### A. Mesin ATM (Anjungan Tunai Mandiri)

| **Komponen ATM** | **Analogi dalam OOP** |
| --- | --- |
| **Mesin ATM** | Kelas (`class ATM`) |
| **Saldo dalam sistem** | Atribut private (`private var saldo`) |
| **Tombol "Cek Saldo"** | Metode public getter (`fun cekSaldo()`) |
| **Tombol "Tarik Tunai"** | Metode public dengan validasi (`fun tarikTunai(jumlah)`) |
| **Tombol "Setor Tunai"** | Metode public dengan validasi (`fun setorTunai(jumlah)`) |
| **Bagian dalam mesin** | Detail implementasi yang disembunyikan (private) |

**Pesan:** Anda bisa melihat saldo dan menarik uang, tapi Anda **tidak tahu** bagaimana mesin ATM bekerja di dalam. Anda **tidak bisa** langsung mengubah saldo dengan menekan tombol tertentu — semua transaksi harus melalui proses yang **tervalidasi** (PIN, saldo cukup, dll).

### B. Mobil

| **Komponen Mobil** | **Analogi dalam OOP** |
| --- | --- |
| **Mobil** | Kelas (`class Mobil`) |
| **Kecepatan mesin** | Atribut private (`private var kecepatan`) |
| **Pedal gas** | Metode public (`fun gas()`) |
| **Pedal rem** | Metode public (`fun rem()`) |
| **Speedometer** | Getter public (`fun getKecepatan()`) |
| **Cara kerja mesin** | Detail implementasi yang disembunyikan |

**Pesan:** Anda bisa mengemudi mobil (menggunakan setir, gas, rem), tapi Anda **tidak perlu tahu** bagaimana mesin bekerja di dalam. Anda **tidak bisa** langsung mengubah kecepatan mesin dengan cara sembarangan.

### C. Kotak Amal

| **Komponen Kotak Amal** | **Analogi dalam OOP** |
| --- | --- |
| **Kotak Amal** | Kelas (`class KotakAmal`) |
| **Uang di dalam kotak** | Atribut private (`private var uang`) |
| **Celah memasukkan uang** | Metode public (`fun masukkanUang(jumlah)`) |
| **Kunci untuk membuka** | Metode private/internal (`private fun bukaKotak()`) |

**Pesan:** Anda bisa **memasukkan** uang ke dalam kotak (metode `deposit`), tapi Anda **tidak bisa langsung mengambil** uang dari dalam tanpa kunci (metode `withdraw` yang terkontrol).

---

## 1.3 Mengapa Enkapsulasi Sangat Penting?

Enkapsulasi bukan sekadar "aturan main" dalam OOP — ia memiliki manfaat yang sangat konkret:

| **Manfaat** | **Penjelasan** | **Contoh Kasus** |
| --- | --- | --- |
| **Keamanan Data** | Mencegah data diubah secara tidak sah atau tidak sengaja | Saldo bank tidak bisa diubah langsung oleh pengguna |
| **Kontrol Akses** | Pengembang kelas bisa mengontrol bagaimana data diakses dan dimodifikasi | Hanya metode `deposit()` dan `withdraw()` yang bisa mengubah saldo |
| **Validasi Data** | Setiap perubahan data bisa divalidasi terlebih dahulu | IPK tidak boleh < 0 atau > 4; umur tidak boleh negatif |
| **Maintainability** | Perubahan internal tidak mempengaruhi kode di luar kelas | Mengganti cara penyimpanan data tidak merusak kode pemanggil |
| **Modularitas** | Setiap kelas menjadi unit yang mandiri | Kelas bisa dikembangkan secara terpisah |
| **Mencegah Penyalahgunaan** | API publik yang terbatas mencegah penggunaan yang salah | Pengguna tidak bisa menarik uang lebih dari saldo |

---

## 1.4 Prinsip Emas Enkapsulasi

> **“Jadikan atribut private, sediakan metode publik untuk mengakses dan mengubahnya.”**

Ini adalah prinsip yang harus selalu diingat:

1. **Atribut** → dibuat **private** (atau protected) — tidak bisa diakses langsung dari luar
2. **Getter** → metode publik untuk **membaca** nilai atribut
3. **Setter** → metode publik untuk **mengubah** nilai atribut (dengan validasi)

Dengan prinsip ini, kita bisa:

- **Membaca** data melalui getter
- **Mengubah** data melalui setter dengan **validasi**
- **Menyembunyikan** detail implementasi dari pengguna kelas

---

# BAGIAN 2: ACCESS MODIFIER (VISIBILITY MODIFIER) DI KOTLIN

## 2.1 Pengenalan Access Modifier

**Access modifier** (atau visibility modifier) adalah kata kunci yang digunakan untuk **mengontrol siapa yang bisa mengakses** kelas, properti, metode, dan konstruktor.

Kotlin menyediakan **empat access modifier**:

| **Modifier** | **Visibilitas** | **Analog** |
| --- | --- | --- |
| **`public`** (default) | Terlihat **di mana saja** | Pintu rumah terbuka untuk semua orang |
| **`private`** | Terlihat **hanya di dalam kelas** yang sama | Barang berharga di brankas pribadi |
| **`protected`** | Terlihat di dalam kelas **dan di subclass** | Warisan untuk keluarga (anak) |
| **`internal`** | Terlihat **di dalam modul yang sama** | Hanya untuk karyawan satu perusahaan |

> **Catatan Penting:** Di Kotlin, **default visibility adalah `public`** — berbeda dengan Java yang default-nya `package-private`.

---

## 2.2 Access Modifier `public` (Default)

**`public`** adalah visibility modifier default di Kotlin. Jika tidak dituliskan modifier apapun, maka secara otomatis bersifat `public`.

```kotlin
// Kedua deklarasi ini SAMA SAJA

// Cara 1: Tanpa modifier (default = public)
class Mahasiswa {
    var nama: String = ""
    fun tampilkan() {
        println(nama)
    }
}

// Cara 2: Dengan modifier public (eksplisit)
public class Mahasiswa {
    public var nama: String = ""
    public fun tampilkan() {
        println(nama)
    }
}
```

**Karakteristik `public`:**

- Terlihat **di mana saja** — dari dalam kelas, dari subclass, dari kelas lain di package yang sama, dari package lain
- Bisa diakses oleh **siapa pun** yang bisa melihat kelasnya

```kotlin
// File: packageA/Contoh.kt
package packageA

public class Contoh {
    public val data: String = "Public"
}

// File: packageB/Lain.kt (package berbeda)
package packageB
import packageA.Contoh

fun test() {
    val obj = Contoh()
    println(obj.data)  // ✅ Bisa diakses — public di mana saja
}
```

---

## 2.3 Access Modifier `private`

**`private`** adalah modifier dengan tingkat visibilitas **paling ketat**.

**Karakteristik `private`:**

- Terlihat **hanya di dalam kelas yang sama** (termasuk semua member-nya)
- **Tidak** terlihat di subclass
- **Tidak** terlihat di kelas lain
- Untuk deklarasi top-level (di luar kelas), `private` berarti hanya terlihat di **file yang sama**

```kotlin
class RekeningBank {
    // PRIVATE — hanya bisa diakses di dalam kelas ini
    private var saldo: Long = 0

    // PRIVATE — hanya bisa diakses di dalam kelas ini
    private fun validasiSaldo() {
        if (saldo < 0) {
            println("⚠️ Saldo negatif!")
        }
    }

    fun deposit(jumlah: Long) {
        saldo += jumlah  // ✅ Bisa diakses dari dalam kelas
        validasiSaldo()  // ✅ Bisa diakses dari dalam kelas
    }
}

fun main() {
    val rekening = RekeningBank()
    // rekening.saldo = 100000  // ❌ ERROR: Cannot access 'saldo': it is private
    // rekening.validasiSaldo() // ❌ ERROR: Cannot access 'validasiSaldo': it is private
    rekening.deposit(50000)     // ✅ Bisa diakses — public
}
```

### Private untuk Top-Level Declaration

Jika `private` digunakan di luar kelas (top-level), maka hanya terlihat di file yang sama:

```kotlin
// File: utility.kt
private const val PI = 3.14159  // Hanya terlihat di file ini

private fun helperFunction() {   // Hanya terlihat di file ini
    println("Helper called")
}

class Calculator {
    fun hitungLuas(jariJari: Double): Double {
        return PI * jariJari * jariJari  // ✅ Bisa diakses — dalam file yang sama
    }
}

// File: main.kt (file berbeda)
// const val PI tidak bisa diakses dari sini
// helperFunction() tidak bisa dipanggil dari sini
```

---

## 2.4 Access Modifier `protected`

**`protected`** adalah modifier untuk member yang **bisa diwariskan** ke subclass.

**Karakteristik `protected`:**

- Memiliki visibilitas yang sama dengan `private` di dalam kelas
- **Tambahan:** terlihat juga di **subclass** (kelas turunan)
- **Tidak** bisa digunakan untuk deklarasi top-level (di luar kelas)

```kotlin
// Kelas induk (superclass)
open class Kendaraan {
    // PROTECTED — bisa diakses di kelas ini dan subclass
    protected var kecepatan: Int = 0

    // PROTECTED — bisa diakses di kelas ini dan subclass
    protected fun gas() {
        kecepatan += 10
    }

    // PUBLIC — bisa diakses di mana saja
    fun getKecepatan(): Int {
        return kecepatan  // ✅ Bisa akses protected dari dalam kelas
    }
}

// Kelas anak (subclass) — mewarisi Kendaraan
class Mobil : Kendaraan() {
    fun akselerasi() {
        gas()  // ✅ Bisa akses protected dari subclass
        kecepatan += 5  // ✅ Bisa akses protected dari subclass
    }
}

// Kelas tidak terkait
class Lain {
    fun test() {
        val k = Kendaraan()
        // k.kecepatan = 100  // ❌ ERROR: Cannot access 'kecepatan': it is protected
        // k.gas()            // ❌ ERROR: Cannot access 'gas': it is protected
    }
}
```

### Perbedaan `protected` di Kotlin vs Java

| **Aspek** | **Kotlin** | **Java** |
| --- | --- | --- |
| **Visibilitas di subclass** | ✅ Terlihat | ✅ Terlihat |
| **Visibilitas di package yang sama** | ❌ Tidak terlihat | ✅ Terlihat (package-private) |
| **Untuk top-level declaration** | ❌ Tidak bisa digunakan | N/A |

---

## 2.5 Access Modifier `internal`

**`internal`** adalah modifier untuk visibilitas **di tingkat modul**.

**Karakteristik `internal`:**

- Terlihat **di dalam modul yang sama** (kumpulan file yang dikompilasi bersama)
- **Tidak** terlihat di luar modul
- Cocok untuk API internal modul

**Apa itu "modul" di Kotlin?**
Modul adalah sekumpulan file Kotlin yang dikompilasi bersama, misalnya:

- Satu proyek IntelliJ IDEA
- Satu modul Maven
- Satu proyek Gradle
- Satu set file yang dikompilasi dengan satu panggilan kompiler

```kotlin
// File: moduleA/InternalApi.kt
package moduleA

internal class InternalClass {
    internal val data: String = "Internal"
}

internal fun internalFunction() {
    println("Internal function")
}

class PublicClass {
    internal fun internalMethod() {
        println("Internal method")
    }
}

// File: moduleA/Test.kt (modul yang sama)
package moduleA

fun test() {
    val obj = InternalClass()     // ✅ Bisa diakses — modul yang sama
    println(obj.data)             // ✅ Bisa diakses — modul yang sama
    internalFunction()            // ✅ Bisa diakses — modul yang sama
    val pub = PublicClass()
    pub.internalMethod()          // ✅ Bisa diakses — modul yang sama
}

// File: moduleB/Test.kt (modul berbeda)
package moduleB
import moduleA.InternalClass  // ❌ ERROR: Tidak bisa import — modul berbeda
```

---

## 2.6 Ringkasan Access Modifier

| **Modifier** | **Kelas yang sama** | **Subclass** | **Modul yang sama** | **Di mana saja** |
| --- | --- | --- | --- | --- |
| **`private`** | ✅ | ❌ | ❌ | ❌ |
| **`protected`** | ✅ | ✅ | ❌ | ❌ |
| **`internal`** | ✅ | ✅ | ✅ | ❌ |
| **`public`** | ✅ | ✅ | ✅ | ✅ |

---

## 2.7 Access Modifier untuk Getter dan Setter

Di Kotlin, **getter selalu memiliki visibilitas yang sama dengan propertinya**. Namun, **setter bisa memiliki visibilitas yang berbeda** (lebih terbatas).

```kotlin
class Contoh {
    // Properti public, setter-nya private
    var counter: Int = 0
        private set  // Hanya kelas ini yang bisa mengubah nilai

    // Properti public, setter-nya internal
    var data: String = ""
        internal set

    // Properti public, setter-nya protected
    var value: Int = 0
        protected set
}

fun main() {
    val obj = Contoh()
    println(obj.counter)  // ✅ Bisa dibaca (getter public)
    // obj.counter = 10   // ❌ ERROR: Cannot assign to 'counter': the setter is private
    // obj.data = "test"  // ❌ ERROR: Cannot access setter (internal di modul berbeda)
    // obj.value = 5      // ❌ ERROR: Cannot access setter (protected)
}
```

---

## 2.8 Access Modifier untuk Konstruktor

Kita juga bisa mengatur visibilitas **primary constructor**:

```kotlin
// Primary constructor private — kelas tidak bisa diinstansiasi dari luar
class Singleton private constructor() {
    companion object {
        private var instance: Singleton? = null

        fun getInstance(): Singleton {
            if (instance == null) {
                instance = Singleton()
            }
            return instance!!
        }
    }
}

// Primary constructor internal — hanya bisa diinstansiasi dalam modul yang sama
class InternalClass internal constructor(val data: String)

fun main() {
    // val s = Singleton()  // ❌ ERROR: Cannot access '<init>': it is private
    val s = Singleton.getInstance()  // ✅ Bisa melalui metode factory

    val ic = InternalClass("test")  // ✅ Bisa jika dalam modul yang sama
}
```

---

# BAGIAN 3: GETTER, SETTER, DAN BACKING FIELD

## 3.1 Apa itu Getter dan Setter?

Di Kotlin, setiap properti secara otomatis memiliki **getter** (untuk membaca nilai) dan **setter** (untuk mengubah nilai).

| **Istilah** | **Fungsi** | **Kapan Dipanggil** |
| --- | --- | --- |
| **Getter** (`get()`) | Membaca nilai properti | Saat properti diakses: `obj.properti` |
| **Setter** (`set(value)`) | Mengubah nilai properti | Saat properti diubah: `obj.properti = nilai` |

Getter dan setter ini disebut juga **property accessors**.

---

## 3.2 Default Getter dan Setter

Saat Anda mendeklarasikan properti dengan `var`, Kotlin secara otomatis menghasilkan getter dan setter default.

```kotlin
class Contact(val id: Int, var email: String) {
    var category: String = ""
}
```

Di balik layar, kode di atas **setara** dengan:

```kotlin
class Contact(val id: Int, var email: String) {
    var category: String = ""
        get() = field       // Getter default: mengembalikan nilai dari backing field
        set(value) {        // Setter default: menyimpan nilai ke backing field
            field = value
        }
}
```

**Untuk properti `val` (read-only):**

- Hanya memiliki **getter**
- **Tidak** memiliki setter

```kotlin
class Contoh {
    val id: Int = 1
        get() = field  // Hanya getter — tidak ada setter
}

fun main() {
    val obj = Contoh()
    println(obj.id)  // ✅ Bisa dibaca
    // obj.id = 2    // ❌ ERROR: Val cannot be reassigned
}
```

---

## 3.3 Custom Getter (Getter Kustom)

Custom getter digunakan ketika Anda perlu **logika tambahan** saat membaca properti.

### A. Properti Terhitung (Computed Property)

Properti yang nilainya **dihitung** dari properti lain, bukan disimpan sebagai field.

```kotlin
class PersegiPanjang(val lebar: Int, val tinggi: Int) {
    // Luas dihitung dari lebar dan tinggi — TIDAK disimpan sebagai field
    // Tidak ada backing field karena tidak menggunakan field
    val luas: Int
        get() = lebar * tinggi
}

fun main() {
    val pp = PersegiPanjang(5, 3)
    println(pp.luas)  // Output: 15
    // Setiap kali diakses, nilai dihitung ulang
}
```

### B. Custom Getter dengan Formatting

```kotlin
class Mahasiswa(val nama: String, val ipk: Double) {
    // Nama selalu ditampilkan dengan huruf kapital di awal
    val namaFormal: String
        get() = nama.replaceFirstChar {
            if (it.isLowerCase()) it.uppercase() else it.toString()
        }

    // IPK ditampilkan dengan 2 angka di belakang koma
    val ipkFormatted: String
        get() = "%.2f".format(ipk)
}

fun main() {
    val mhs = Mahasiswa("budi santoso", 3.756)
    println(mhs.namaFormal)     // Output: Budi santoso
    println(mhs.ipkFormatted)   // Output: 3.76
}
```

### C. Custom Getter dengan Validasi

```kotlin
class Lingkaran(val jariJari: Double) {
    // Luas selalu non-negatif (tidak mungkin negatif, tapi ini contoh)
    val luas: Double
        get() {
            val hasil = Math.PI * jariJari * jariJari
            return if (hasil < 0) 0.0 else hasil
        }
}
```

---

## 3.4 Custom Setter (Setter Kustom)

Custom setter digunakan ketika Anda perlu **logika tambahan** saat mengubah nilai properti.

### A. Setter dengan Validasi

```kotlin
class Mahasiswa {
    var ipk: Double = 0.0
        set(value) {
            if (value in 0.0..4.0) {
                field = value  // field = backing field
            } else {
                println("⚠️ IPK $value tidak valid! IPK harus antara 0.0 - 4.0")
            }
        }
}

fun main() {
    val mhs = Mahasiswa()
    mhs.ipk = 3.75   // ✅ OK
    println(mhs.ipk) // Output: 3.75
    mhs.ipk = 5.0    // ⚠️ IPK 5.0 tidak valid! IPK harus antara 0.0 - 4.0
    println(mhs.ipk) // Output: 3.75 (nilai tidak berubah)
}
```

### B. Setter dengan Konversi Nilai

```kotlin
class Person {
    var name: String = ""
        set(value) {
            // Memastikan huruf pertama kapital
            field = value.replaceFirstChar {
                if (it.isLowerCase()) it.uppercase() else it.toString()
            }
        }
}

fun main() {
    val person = Person()
    person.name = "kodee"  // Input huruf kecil semua
    println(person.name)   // Output: Kodee — otomatis dikapitalisasi
}
```

### C. Setter dengan Logging (Pencatatan)

```kotlin
class BankAccount {
    var balance: Int = 0
        set(value) {
            println("💰 Saldo berubah: $field → $value")  // Logging
            field = value
        }

    fun deposit(amount: Int) {
        require(amount > 0) { "Jumlah deposit harus positif" }
        balance += amount
    }
}

fun main() {
    val account = BankAccount()
    account.deposit(100)   // Output: 💰 Saldo berubah: 0 → 100
    account.deposit(50)    // Output: 💰 Saldo berubah: 100 → 150
}
```

### D. Setter dengan Notifikasi (Event)

```kotlin
class ObservableCounter {
    var value: Int = 0
        set(newValue) {
            val oldValue = field
            field = newValue
            onValueChanged(oldValue, newValue)  // Panggil callback
        }

    private fun onValueChanged(old: Int, new: Int) {
        println("🔔 Nilai berubah: $old → $new")
    }
}

fun main() {
    val counter = ObservableCounter()
    counter.value = 5   // Output: 🔔 Nilai berubah: 0 → 5
    counter.value = 10  // Output: 🔔 Nilai berubah: 5 → 10
}
```

---

## 3.5 Backing Field (`field`) — Konsep Kritis

### Apa itu Backing Field?

**Backing field** adalah **variabel tersembunyi** yang menyimpan nilai aktual dari sebuah properti.

| **Konsep** | **Penjelasan** |
| --- | --- |
| **Backing Field** | Tempat penyimpanan nilai properti yang sebenarnya |
| **Keyword `field`** | Digunakan di dalam getter/setter untuk mengakses backing field |
| **Kapan ada?** | Jika menggunakan getter/setter default ATAU menggunakan keyword `field` |

### Mengapa Perlu Backing Field?

**Masalah:** Jika di dalam setter Anda mengakses properti secara langsung (bukan `field`), akan terjadi **rekursi tak terbatas (infinite loop)** yang menyebabkan `StackOverflowError`.

```kotlin
// ❌ SALAH — infinite loop!
class Salah {
    var name: String = ""
        set(value) {
            name = value  // Memanggil setter lagi! → StackOverflowError
        }
}

// ✅ BENAR — menggunakan backing field
class Benar {
    var name: String = ""
        set(value) {
            field = value  // Mengakses backing field langsung
        }
}
```

### Ilustrasi Cara Kerja Backing Field

```
┌─────────────────────────────────────────────────┐
│               OBJEK Mahasiswa                   │
│                                                 │
│  ┌───────────────────────────────────────────┐  │
│  │          Backing Field (field)            │  │
│  │         nilai: "Budi Santoso"             │  │
│  └───────────────────────────────────────────┘  │
│                                                 │
│  var nama: String                              │
│      get() = field          ←─── membaca dari   │
│      set(value) {                              │
│          field = value      ←─── menulis ke    │
│      }                                         │
└─────────────────────────────────────────────────┘
```

### Kapan Backing Field Tidak Ada?

Backing field **tidak ada** jika properti **tidak** menggunakan default getter/setter dan **tidak** menggunakan keyword `field`.

```kotlin
class Contoh {
    // Tidak ada backing field — nilai dihitung setiap kali diakses
    val luas: Int
        get() = lebar * tinggi  // Tidak pakai field → tidak ada backing field

    // Tidak ada backing field — nilai diambil dari properti lain
    val namaLengkap: String
        get() = "$firstName $lastName"  // Tidak pakai field
}
```

### Contoh Lengkap Penggunaan Backing Field

```kotlin
class Product {
    // Properti dengan backing field
    var price: Double = 0.0
        set(value) {
            // Validasi: harga tidak boleh negatif
            if (value < 0) {
                println("⚠️ Harga tidak boleh negatif!")
                return
            }
            // Gunakan field untuk menyimpan nilai
            field = value
            // Logging setelah perubahan
            println("💰 Harga diperbarui: $field")
        }

    // Properti tanpa backing field (computed)
    val tax: Double
        get() = price * 0.11  // PPN 11%

    // Properti tanpa backing field (computed)
    val totalPrice: Double
        get() = price + tax
}

fun main() {
    val product = Product()
    product.price = 100000.0   // Output: 💰 Harga diperbarui: 100000.0
    println("Harga: ${product.price}")         // Output: Harga: 100000.0
    println("PPN: ${product.tax}")             // Output: PPN: 11000.0
    println("Total: ${product.totalPrice}")    // Output: Total: 111000.0
    product.price = -5000.0    // Output: ⚠️ Harga tidak boleh negatif!
}
```

---

# BAGIAN 4: PRIVATE SETTER — PUBLIC GETTER

## 4.1 Konsep Private Setter

**Private setter** adalah teknik enkapsulasi di mana properti memiliki **getter public** (bisa dibaca dari mana saja) tetapi **setter private** (hanya bisa diubah dari dalam kelas).

> **Manfaat:** Properti bersifat **read-only dari luar**, tetapi **writeable dari dalam** kelas.

### Sintaks Dasar

```kotlin
class MyClass {
    var myProperty: String = "default"
        private set  // Setter private, getter public (default)
}

fun main() {
    val obj = MyClass()
    println(obj.myProperty)  // ✅ Bisa dibaca (getter public)
    // obj.myProperty = "new" // ❌ ERROR: Cannot assign to 'myProperty': the setter is private
}
```

---

## 4.2 Private Setter dengan Custom Logic

Private setter juga bisa memiliki **custom logic** sendiri:

```kotlin
class LoggingBankAccount {
    var balance: Int = 0
        private set(value) {
            println("💰 Saldo berubah: $field → $value")  // Logging
            field = value
        }

    fun deposit(amount: Int) {
        require(amount > 0) { "Jumlah deposit harus positif" }
        balance += amount  // Memanggil private setter
    }

    fun withdraw(amount: Int) {
        require(amount > 0) { "Jumlah penarikan harus positif" }
        require(amount <= balance) { "Saldo tidak mencukupi" }
        balance -= amount  // Memanggil private setter
    }
}

fun main() {
    val account = LoggingBankAccount()
    account.deposit(100)   // Output: 💰 Saldo berubah: 0 → 100
    account.withdraw(50)   // Output: 💰 Saldo berubah: 100 → 50
    println(account.balance) // Output: 50
    // account.balance = 999  // ❌ ERROR: Cannot assign to 'balance': the setter is private
}
```

---

## 4.3 Studi Kasus: Sistem Rekening Bank

**Studi Kasus Lengkap — Rekening Bank dengan Enkapsulasi Penuh**

```kotlin
/**
 * ============================================================
 * SISTEM REKENING BANK DENGAN ENKAPSULASI PENUH
 * ============================================================
 * Demonstrasi:
 * 1. Private setter untuk melindungi saldo
 * 2. Validasi di setiap metode
 * 3. Enkapsulasi data dan perilaku
 * ============================================================
 */

class BankAccount(
    private val accountNumber: String,
    private val ownerName: String
) {
    // ============================================================
    // PROPERTI
    // ============================================================

    /**
     * Saldo rekening — public getter, private setter
     *
     * private set berarti:
     * - Siapa pun bisa MEMBACA saldo (getter public)
     * - HANYA kelas ini yang bisa MENGUBAH saldo (setter private)
     */
    var balance: Long = 0
        private set

    /**
     * Riwayat transaksi — private total
     * Tidak ada akses dari luar sama sekali
     */
    private val transactionHistory = mutableListOf<String>()

    /**
     * Jumlah transaksi — computed property
     * Tidak ada backing field — dihitung dari riwayat
     */
    val transactionCount: Int
        get() = transactionHistory.size

    /**
     * Status rekening berdasarkan saldo — computed property
     */
    val status: String
        get() = when {
            balance > 100_000_000 -> "💎 Premium"
            balance > 10_000_000 -> "⭐ Gold"
            balance > 1_000_000 -> "🥈 Silver"
            balance > 0 -> "🥉 Bronze"
            else -> "⚫ Tidak Aktif"
        }

    // ============================================================
    // METODE
    // ============================================================

    /**
     * Menyetor uang ke rekening
     *
     * @param amount Jumlah uang yang disetor (harus > 0)
     * @return true jika berhasil, false jika gagal
     */
    fun deposit(amount: Long): Boolean {
        // Validasi: jumlah harus positif
        if (amount <= 0) {
            println("❌ ERROR: Jumlah deposit harus lebih dari 0")
            return false
        }

        // Update saldo (memanggil private setter)
        balance += amount

        // Catat riwayat
        transactionHistory.add("💰 DEPOSIT: +Rp ${formatRupiah(amount)}")
        println("✅ Deposit Rp ${formatRupiah(amount)} berhasil")
        return true
    }

    /**
     * Menarik uang dari rekening
     *
     * @param amount Jumlah uang yang ditarik (harus > 0 dan <= saldo)
     * @return true jika berhasil, false jika gagal
     */
    fun withdraw(amount: Long): Boolean {
        // Validasi: jumlah harus positif
        if (amount <= 0) {
            println("❌ ERROR: Jumlah penarikan harus lebih dari 0")
            return false
        }

        // Validasi: saldo harus mencukupi
        if (amount > balance) {
            println("❌ ERROR: Saldo tidak mencukupi")
            println("   Saldo: Rp ${formatRupiah(balance)}")
            println("   Dibutuhkan: Rp ${formatRupiah(amount)}")
            return false
        }

        // Update saldo
        balance -= amount

        // Catat riwayat
        transactionHistory.add("🏧 WITHDRAW: -Rp ${formatRupiah(amount)}")
        println("✅ Penarikan Rp ${formatRupiah(amount)} berhasil")
        return true
    }

    /**
     * Transfer uang ke rekening lain
     *
     * @param target Rekening tujuan
     * @param amount Jumlah uang yang ditransfer
     * @return true jika berhasil, false jika gagal
     */
    fun transfer(target: BankAccount, amount: Long): Boolean {
        // Validasi: tidak bisa transfer ke diri sendiri
        if (this === target) {
            println("❌ ERROR: Tidak bisa transfer ke rekening sendiri")
            return false
        }

        // Tarik dari rekening ini
        if (!withdraw(amount)) {
            return false
        }

        // Setor ke rekening tujuan
        target.deposit(amount)

        // Catat riwayat tambahan
        transactionHistory.add("🔄 TRANSFER KELUAR: -Rp ${formatRupiah(amount)} ke ${target.ownerName}")
        println("✅ Transfer Rp ${formatRupiah(amount)} ke ${target.ownerName} berhasil")
        return true
    }

    /**
     * Menampilkan informasi rekening
     */
    fun displayInfo() {
        println("=" .repeat(55))
        println("🏦 INFORMASI REKENING")
        println("=" .repeat(55))
        println("Nomor Rekening : $accountNumber")
        println("Nama Pemilik   : $ownerName")
        println("Saldo          : Rp ${formatRupiah(balance)}")
        println("Status         : $status")
        println("Total Transaksi: $transactionCount")
        println("=" .repeat(55))
    }

    /**
     * Menampilkan riwayat transaksi
     *
     * @param limit Jumlah transaksi yang ditampilkan (default: semua)
     */
    fun displayHistory(limit: Int = transactionHistory.size) {
        println("=" .repeat(55))
        println("📋 RIWAYAT TRANSAKSI (${minOf(limit, transactionHistory.size)} terakhir)")
        println("=" .repeat(55))

        if (transactionHistory.isEmpty()) {
            println("   Belum ada transaksi")
        } else {
            val start = maxOf(0, transactionHistory.size - limit)
            for (i in start until transactionHistory.size) {
                println("   ${i + 1}. ${transactionHistory[i]}")
            }
        }
        println("=" .repeat(55))
    }

    /**
     * Format Rupiah (helper method — private)
     */
    private fun formatRupiah(nominal: Long): String {
        val str = nominal.toString()
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
 * Fungsi utama — demo sistem perbankan
 */
fun main() {
    println("=" .repeat(55))
    println("🏦 DEMO SISTEM PERBANKAN DENGAN ENKAPSULASI")
    println("=" .repeat(55))
    println()

    // Buat beberapa rekening
    val accountBudi = BankAccount("1234567890", "Budi Santoso")
    val accountSiti = BankAccount("0987654321", "Siti Rahayu")

    // Tampilkan info awal
    println("--- INFO REKENING AWAL ---")
    accountBudi.displayInfo()
    println()
    accountSiti.displayInfo()
    println()

    // Lakukan transaksi
    println("--- MELAKUKAN TRANSAKSI ---")
    accountBudi.deposit(500000)
    accountBudi.deposit(250000)
    accountSiti.deposit(1000000)
    accountBudi.withdraw(100000)
    accountBudi.transfer(accountSiti, 200000)
    accountBudi.withdraw(700000)  // Gagal — saldo tidak cukup
    println()

    // Tampilkan info akhir
    println("--- INFO REKENING AKHIR ---")
    accountBudi.displayInfo()
    println()
    accountSiti.displayInfo()
    println()

    // Tampilkan riwayat
    accountBudi.displayHistory(5)
    println()
    accountSiti.displayHistory()

    // Demonstrasi bahwa saldo tidak bisa diubah langsung dari luar
    println()
    println("--- DEMONSTRASI ENKAPSULASI ---")
    println("Mencoba mengubah saldo langsung dari luar...")
    // accountBudi.balance = 9999999  // ❌ ERROR: Cannot assign to 'balance': the setter is private
    println("✅ Saldo TIDAK BISA diubah langsung dari luar — enkapsulasi berhasil!")

    println()
    println("=" .repeat(55))
    println("🏁 PROGRAM SELESAI")
    println("=" .repeat(55))
}
```

---

# BAGIAN 5: BEST PRACTICES ENKAPSULASI

## 5.1 Panduan Praktik Terbaik

| **Praktik Terbaik** | **Penjelasan** | **Contoh** |
| --- | --- | --- |
| **Gunakan `private` secara default** | Properti dan metode yang tidak perlu diakses dari luar harus `private` | `private var counter: Int = 0` |
| **Gunakan `val` daripada `var`** | Jika properti tidak perlu diubah, gunakan `val` (read-only) | `val nim: String` |
| **Private setter untuk properti mutable** | Jika properti perlu diubah dari dalam kelas, gunakan `private set` | `var saldo: Long = 0 private set` |
| **Validasi di setter** | Selalu validasi nilai sebelum menyimpan ke backing field | `set(value) { if (value >= 0) field = value }` |
| **Jangan expose backing field** | Backing field (`field`) hanya boleh diakses di dalam getter/setter | - |
| **Gunakan metode daripada setter publik** | Untuk operasi kompleks, sediakan metode而非setter publik | `fun deposit(amount: Int)` bukan `balance = ...` |
| **Jaga agar API publik minimal** | Semakin sedikit yang diekspos, semakin mudah maintenance | - |
| **Hindari efek samping di getter/setter** | Jangan melakukan operasi berat atau network call di getter/setter | - |

---

## 5.2 Contoh Penerapan Best Practices

```kotlin
/**
 * Contoh kelas dengan penerapan best practices enkapsulasi
 */
class Student(
    // 1. Gunakan val untuk data yang tidak pernah berubah
    val id: String,
    val name: String
) {
    // 2. Properti private secara default
    private var _gpa: Double = 0.0

    // 3. Public getter dengan validasi
    val gpa: Double
        get() {
            // 6. Hindari efek samping di getter
            return _gpa
        }

    // 4. Private setter dengan validasi
    var grade: String = ""
        private set(value) {
            // 5. Validasi di setter
            val validGrades = listOf("A", "B", "C", "D", "E")
            if (value in validGrades) {
                field = value
                // Update GPA berdasarkan grade
                _gpa = when (value) {
                    "A" -> 4.0
                    "B" -> 3.0
                    "C" -> 2.0
                    "D" -> 1.0
                    else -> 0.0
                }
            } else {
                println("⚠️ Grade tidak valid: $value")
            }
        }

    // 7. Gunakan metode untuk operasi kompleks
    fun setGrade(grade: String) {
        this.grade = grade  // Memanggil private setter
    }

    fun displayInfo() {
        println("ID: $id, Nama: $name, GPA: $gpa, Grade: $grade")
    }
}

fun main() {
    val student = Student("S001", "Budi")
    student.setGrade("A")
    student.displayInfo()  // Output: ID: S001, Nama: Budi, GPA: 4.0, Grade: A

    // student.grade = "B"  // ❌ ERROR: Cannot access setter
    // student._gpa = 3.5   // ❌ ERROR: Cannot access private property
}
```

---

# BAGIAN 6: STUDI KASUS LENGKAP — SISTEM PERPUSTAKAAN

## 6.1 Analisis Kebutuhan

Kita akan membangun sistem manajemen perpustakaan dengan enkapsulasi penuh.

**Kebutuhan:**

1. Setiap buku memiliki judul, penulis, ISBN, tahun terbit, status pinjam, dan peminjam
2. Buku bisa dipinjam dan dikembalikan
3. Perpustakaan menyimpan daftar buku
4. Bisa mencari buku, melihat buku tersedia, melihat buku dipinjam

## 6.2 Implementasi Lengkap

```kotlin
/**
 * ============================================================
 * SISTEM MANAJEMEN PERPUSTAKAAN DENGAN ENKAPSULASI PENUH
 * ============================================================
 * Studi kasus komprehensif untuk mendemonstrasikan:
 * 1. Enkapsulasi data buku
 * 2. Private setter untuk status pinjam
 * 3. Validasi di setiap operasi
 * 4. Class interaction yang aman
 * ============================================================
 */

/**
 * Kelas Buku — merepresentasikan satu buku di perpustakaan
 *
 * Prinsip Enkapsulasi:
 * - Semua properti immutable (val) kecuali status peminjaman
 * - Status peminjaman hanya bisa diubah melalui metode pinjam() dan kembalikan()
 * - Peminjam hanya bisa diatur melalui metode pinjam()
 */
class Book(
    val title: String,
    val author: String,
    val isbn: String,
    val year: Int
) {
    // ============================================================
    // PROPERTI
    // ============================================================

    /**
     * Status peminjaman — private setter
     * - Bisa dibaca dari luar (getter public)
     * - Hanya bisa diubah dari dalam kelas (setter private)
     */
    var isBorrowed: Boolean = false
        private set

    /**
     * Nama peminjam — private setter, nullable
     * - Bisa dibaca dari luar
     * - Hanya bisa diubah dari dalam kelas
     */
    var borrower: String? = null
        private set

    /**
     * Ketersediaan buku — computed property
     * Tidak ada backing field — dihitung dari isBorrowed
     */
    val isAvailable: Boolean
        get() = !isBorrowed

    // ============================================================
    // METODE
    // ============================================================

    /**
     * Meminjam buku
     *
     * @param name Nama peminjam
     * @return true jika berhasil, false jika gagal
     */
    fun borrow(name: String): Boolean {
        // Validasi: buku harus tersedia
        if (isBorrowed) {
            println("❌ Buku '$title' sedang dipinjam oleh $borrower")
            return false
        }

        // Validasi: nama peminjam tidak boleh kosong
        if (name.isBlank()) {
            println("❌ Nama peminjam tidak boleh kosong")
            return false
        }

        // Update status
        isBorrowed = true
        borrower = name
        println("✅ Buku '$title' berhasil dipinjam oleh $name")
        return true
    }

    /**
     * Mengembalikan buku
     *
     * @return true jika berhasil, false jika gagal
     */
    fun returnBook(): Boolean {
        // Validasi: buku harus sedang dipinjam
        if (!isBorrowed) {
            println("❌ Buku '$title' tidak sedang dipinjam")
            return false
        }

        val previousBorrower = borrower
        // Update status
        isBorrowed = false
        borrower = null
        println("✅ Buku '$title' berhasil dikembalikan oleh $previousBorrower")
        return true
    }

    /**
     * Menampilkan informasi buku
     */
    fun displayInfo() {
        println("=" .repeat(45))
        println("📚 INFORMASI BUKU")
        println("=" .repeat(45))
        println("Judul    : $title")
        println("Penulis  : $author")
        println("ISBN     : $isbn")
        println("Tahun    : $year")
        println("Status   : ${if (isBorrowed) "🔴 Dipinjam" else "🟢 Tersedia"}")
        if (isBorrowed) {
            println("Peminjam : $borrower")
        }
        println("=" .repeat(45))
    }
}

/**
 * Kelas Perpustakaan — mengelola koleksi buku
 *
 * Prinsip Enkapsulasi:
 * - Daftar buku private — tidak bisa diakses langsung dari luar
 * - Semua operasi melalui metode publik
 */
class Library(val name: String) {
    // ============================================================
    // PROPERTI
    // ============================================================

    /**
     * Daftar buku — private total
     * Tidak ada akses dari luar sama sekali
     */
    private val books = mutableListOf<Book>()

    /**
     * Jumlah buku — computed property
     */
    val totalBooks: Int
        get() = books.size

    /**
     * Jumlah buku tersedia — computed property
     */
    val availableBooks: Int
        get() = books.count { it.isAvailable }

    /**
     * Jumlah buku dipinjam — computed property
     */
    val borrowedBooks: Int
        get() = books.count { it.isBorrowed }

    // ============================================================
    // METODE
    // ============================================================

    /**
     * Menambah buku ke koleksi
     */
    fun addBook(book: Book) {
        books.add(book)
        println("✅ Buku '${book.title}' ditambahkan ke perpustakaan")
    }

    /**
     * Menambah multiple buku sekaligus
     */
    fun addBooks(vararg newBooks: Book) {
        for (book in newBooks) {
            addBook(book)
        }
    }

    /**
     * Mencari buku berdasarkan kata kunci (judul atau penulis)
     *
     * @param keyword Kata kunci pencarian (case-insensitive)
     * @return List buku yang cocok
     */
    fun searchBooks(keyword: String): List<Book> {
        val lowerKeyword = keyword.lowercase()
        return books.filter { book ->
            book.title.lowercase().contains(lowerKeyword) ||
            book.author.lowercase().contains(lowerKeyword)
        }
    }

    /**
     * Mencari buku berdasarkan ISBN (pencarian tepat)
     *
     * @param isbn ISBN buku
     * @return Buku yang ditemukan, atau null jika tidak ada
     */
    fun findBookByIsbn(isbn: String): Book? {
        return books.find { it.isbn == isbn }
    }

    /**
     * Meminjam buku berdasarkan ISBN
     *
     * @param isbn ISBN buku
     * @param borrower Nama peminjam
     * @return true jika berhasil, false jika gagal
     */
    fun borrowBook(isbn: String, borrower: String): Boolean {
        val book = findBookByIsbn(isbn)
        if (book == null) {
            println("❌ Buku dengan ISBN $isbn tidak ditemukan")
            return false
        }
        return book.borrow(borrower)
    }

    /**
     * Mengembalikan buku berdasarkan ISBN
     *
     * @param isbn ISBN buku
     * @return true jika berhasil, false jika gagal
     */
    fun returnBook(isbn: String): Boolean {
        val book = findBookByIsbn(isbn)
        if (book == null) {
            println("❌ Buku dengan ISBN $isbn tidak ditemukan")
            return false
        }
        return book.returnBook()
    }

    /**
     * Menampilkan semua buku
     */
    fun displayAllBooks() {
        println("=" .repeat(45))
        println("📚 DAFTAR SEMUA BUKU — $name")
        println("=" .repeat(45))
        println("Total: $totalBooks buku")
        println("Tersedia: $availableBooks buku")
        println("Dipinjam: $borrowedBooks buku")
        println("-" .repeat(45))

        if (books.isEmpty()) {
            println("   Belum ada buku")
        } else {
            for ((index, book) in books.withIndex()) {
                println("${index + 1}. ${book.title} — ${book.author}")
                println("   ISBN: ${book.isbn} | Status: ${if (book.isBorrowed) "🔴 Dipinjam" else "🟢 Tersedia"}")
                if (book.isBorrowed) {
                    println("   Peminjam: ${book.borrower}")
                }
            }
        }
        println("=" .repeat(45))
    }

    /**
     * Menampilkan buku yang tersedia
     */
    fun displayAvailableBooks() {
        val available = books.filter { it.isAvailable }
        println("=" .repeat(45))
        println("🟢 BUKU TERSEDIA — $name")
        println("=" .repeat(45))
        println("Jumlah: ${available.size} buku")
        println("-" .repeat(45))

        if (available.isEmpty()) {
            println("   Tidak ada buku tersedia")
        } else {
            for ((index, book) in available.withIndex()) {
                println("${index + 1}. ${book.title} — ${book.author} (ISBN: ${book.isbn})")
            }
        }
        println("=" .repeat(45))
    }

    /**
     * Menampilkan buku yang sedang dipinjam
     */
    fun displayBorrowedBooks() {
        val borrowed = books.filter { it.isBorrowed }
        println("=" .repeat(45))
        println("🔴 BUKU DIPINJAM — $name")
        println("=" .repeat(45))
        println("Jumlah: ${borrowed.size} buku")
        println("-" .repeat(45))

        if (borrowed.isEmpty()) {
            println("   Tidak ada buku yang dipinjam")
        } else {
            for ((index, book) in borrowed.withIndex()) {
                println("${index + 1}. ${book.title} — ${book.author}")
                println("   Peminjam: ${book.borrower} | ISBN: ${book.isbn}")
            }
        }
        println("=" .repeat(45))
    }
}

/**
 * Fungsi utama — demo sistem perpustakaan
 */
fun main() {
    println("=" .repeat(55))
    println("📚 DEMO SISTEM PERPUSTAKAAN DENGAN ENKAPSULASI")
    println("=" .repeat(55))
    println()

    // Buat perpustakaan
    val library = Library("Perpustakaan Kampus")

    // Buat beberapa buku
    val book1 = Book("Pemrograman Kotlin", "Budi Santoso", "978-602-1234-001", 2023)
    val book2 = Book("Dasar-Dasar OOP", "Siti Rahayu", "978-602-1234-002", 2022)
    val book3 = Book("Algoritma dan Struktur Data", "Ahmad Fauzi", "978-602-1234-003", 2023)
    val book4 = Book("Database Sistem", "Dewi Lestari", "978-602-1234-004", 2021)
    val book5 = Book("Jaringan Komputer", "Rizki Pratama", "978-602-1234-005", 2022)

    // Tambahkan buku ke perpustakaan
    library.addBooks(book1, book2, book3, book4, book5)
    println()

    // Tampilkan semua buku
    library.displayAllBooks()
    println()

    // Lakukan peminjaman
    println("--- PROSES PEMINJAMAN ---")
    library.borrowBook("978-602-1234-001", "Mahasiswa A")
    library.borrowBook("978-602-1234-003", "Mahasiswa B")
    library.borrowBook("978-602-1234-005", "Mahasiswa C")
    println()

    // Tampilkan buku tersedia dan dipinjam
    library.displayAvailableBooks()
    println()
    library.displayBorrowedBooks()
    println()

    // Kembalikan buku
    println("--- PROSES PENGEMBALIAN ---")
    library.returnBook("978-602-1234-001")
    library.returnBook("978-602-1234-003")
    println()

    // Tampilkan status akhir
    library.displayAllBooks()
    println()

    // Cari buku
    println("--- PENCARIAN BUKU ---")
    val searchResults = library.searchBooks("Kotlin")
    println("Hasil pencarian 'Kotlin': ${searchResults.size} buku ditemukan")
    for (book in searchResults) {
        println("   - ${book.title} oleh ${book.author}")
    }
    println()

    // Demonstrasi bahwa status buku tidak bisa diubah langsung dari luar
    println("--- DEMONSTRASI ENKAPSULASI ---")
    println("Mencoba mengubah status buku langsung dari luar...")
    // book1.isBorrowed = true  // ❌ ERROR: Cannot assign to 'isBorrowed': the setter is private
    // book1.borrower = "X"     // ❌ ERROR: Cannot assign to 'borrower': the setter is private
    println("✅ Status buku TIDAK BISA diubah langsung dari luar — enkapsulasi berhasil!")

    println()
    println("=" .repeat(55))
    println("🏁 PROGRAM SELESAI")
    println("=" .repeat(55))
}
```

---

# BAGIAN 7: RINGKASAN MATERI PERTEMUAN 2

## 7.1 Poin-Poin Penting

| **Konsep** | **Penjelasan** | **Keyword/Sintaks** |
| --- | --- | --- |
| **Enkapsulasi** | Membungkus data dan metode, menyembunyikan detail internal | - |
| **Access Modifier** | Mengontrol siapa yang bisa mengakses member kelas | `private`, `protected`, `internal`, `public` |
| **`private`** | Hanya terlihat di dalam kelas yang sama | `private var data: String` |
| **`protected`** | Terlihat di kelas dan subclass | `protected var data: String` |
| **`internal`** | Terlihat di dalam modul yang sama | `internal var data: String` |
| **`public`** (default) | Terlihat di mana saja | `public var data: String` |
| **Getter** | Membaca nilai properti | `get() = field` |
| **Setter** | Mengubah nilai properti | `set(value) { field = value }` |
| **Backing Field (`field`)** | Menyimpan nilai aktual properti | Digunakan di getter/setter |
| **Private Setter** | Getter public, setter private | `var data: String = "" private set` |

---

## 7.2 Kapan Menggunakan Apa?

| **Skenario** | **Solusi** | **Contoh** |
| --- | --- | --- |
| Data tidak pernah berubah setelah dibuat | Gunakan `val` | `val id: String` |
| Data bisa berubah, tapi hanya dari dalam kelas | `var` + `private set` | `var balance: Long = 0 private set` |
| Data bisa berubah dengan validasi | Custom setter | `set(value) { if (value >= 0) field = value }` |
| Nilai dihitung dari properti lain | Custom getter (computed property) | `val luas get() = panjang * lebar` |
| Member hanya untuk penggunaan internal | `private` | `private fun helper()` |
| Member boleh diwariskan ke subclass | `protected` | `protected open fun process()` |
| API internal modul | `internal` | `internal class InternalApi` |

---

# BAGIAN 8: LATIHAN DAN TUGAS

## 8.1 Latihan Mandiri

### Latihan 1: Kelas `Temperature`

Buatlah kelas **`Temperature`** dengan:

- **Properti:**
  - `celsius: Double` (private setter — hanya bisa diubah dari dalam kelas)
  - `fahrenheit: Double` (computed property — dihitung dari celsius)
  - `kelvin: Double` (computed property — dihitung dari celsius)
- **Metode:**
  - `setCelsius(value: Double)` → mengatur suhu dalam Celsius (dengan validasi: tidak boleh kurang dari -273.15)
  - `setFahrenheit(value: Double)` → mengatur suhu dalam Fahrenheit (konversi ke Celsius, dengan validasi)
  - `setKelvin(value: Double)` → mengatur suhu dalam Kelvin (konversi ke Celsius, dengan validasi)
  - `display()` → menampilkan suhu dalam ketiga satuan

---

### Latihan 2: Kelas `Counter`

Buatlah kelas **`Counter`** dengan:

- **Properti:**
  - `value: Int` (private setter — hanya bisa diubah dari dalam kelas)
  - `maxValue: Int` (read-only, dari constructor)
  - `minValue: Int` (read-only, dari constructor, default = 0)
- **Metode:**
  - `increment()` → menambah nilai 1 (tidak boleh melebihi maxValue)
  - `decrement()` → mengurangi nilai 1 (tidak boleh kurang dari minValue)
  - `reset()` → mengatur value ke minValue
  - `isAtMax()` → mengembalikan true jika value == maxValue
  - `isAtMin()` → mengembalikan true jika value == minValue
  - `display()` → menampilkan nilai counter

---

## 8.2 Tugas 2 (Dikumpulkan)

### Sistem Manajemen Hotel Sederhana

Buatlah program lengkap sistem manajemen hotel dengan ketentuan berikut:

#### 1. Kelas `Room` (Kamar)

| **Komponen** | **Spesifikasi** |
| --- | --- |
| **Properti** | `roomNumber: String` (read-only)<br>`type: String` (read-only) — "Standard", "Deluxe", "Suite"<br>`pricePerNight: Double` (read-only)<br>`isOccupied: Boolean` (private setter)<br>`guestName: String?` (private setter, nullable)<br>`checkInDate: String?` (private setter, nullable)<br>`checkOutDate: String?` (private setter, nullable) |
| **Metode** | `checkIn(guest: String, checkIn: String, checkOut: String): Boolean`<br>`checkOut(): Boolean`<br>`isAvailable(): Boolean`<br>`displayInfo(): String` |

#### 2. Kelas `Hotel`

| **Komponen** | **Spesifikasi** |
| --- | --- |
| **Properti** | `name: String` (read-only)<br>`rooms: MutableList<Room>` (private) |
| **Metode** | `addRoom(room: Room)`<br>`findRoom(roomNumber: String): Room?`<br>`checkIn(roomNumber: String, guest: String, checkIn: String, checkOut: String): Boolean`<br>`checkOut(roomNumber: String): Boolean`<br>`getAvailableRooms(): List<Room>`<br>`getOccupiedRooms(): List<Room>`<br>`displayAllRooms()`<br>`displayAvailableRooms()`<br>`displayOccupiedRooms()`<br>`getTotalRevenue(): Double` (hitung dari kamar yang sudah check-out) |

#### 3. Fungsi `main()`

- Buat objek `Hotel` dengan nama "Hotel Kampus"
- Tambahkan **minimal 6 kamar** dengan tipe berbeda
- Tampilkan semua kamar
- Lakukan check-in beberapa kamar
- Tampilkan kamar tersedia dan terisi
- Lakukan check-out beberapa kamar
- Tampilkan status akhir dan total pendapatan

#### 4. Kriteria Penilaian Tugas 2

| **Kriteria** | **Bobot** | **Indikator** |
| --- | --- | --- |
| **Enkapsulasi Kelas Room** | 30% | • Properti status menggunakan private setter<br>• Metode checkIn/checkOut memvalidasi status<br>• Tidak ada akses langsung ke properti internal |
| **Enkapsulasi Kelas Hotel** | 25% | • `rooms` bersifat private<br>• Metode publik menyediakan akses terkontrol |
| **Fungsi main()** | 20% | • Menampilkan semua skenario yang diminta<br>• Output jelas dan informatif |
| **Kode Berkualitas** | 15% | • Kode bersih, terstruktur, diberi komentar<br>• Menggunakan naming convention yang benar |
| **Program Berjalan** | 10% | • Program berjalan tanpa error<br>• Semua fungsi berfungsi sesuai spesifikasi |

---

# BAGIAN 9: REFERENSI

## 9.1 Referensi Utama

1. **Kotlin Official Documentation – Visibility Modifiers** — [https://kotlinlang.org/docs/visibility-modifiers.html](https://kotlinlang.org/docs/visibility-modifiers.html)

2. **Kotlin Official Documentation – Properties** — [https://kotlinlang.org/docs/properties.html](https://kotlinlang.org/docs/properties.html)

3. **Kotlin Tour – Intermediate: Properties** — [https://kotlinlang.org/docs/kotlin-tour-intermediate-properties.html](https://kotlinlang.org/docs/kotlin-tour-intermediate-properties.html)

## 9.2 Referensi Pendukung

1. **Baeldung – Variable with Public Getter and Private Setter in Kotlin** — [https://www.baeldung.com/kotlin/public-getter-private-setter](https://www.baeldung.com/kotlin/public-getter-private-setter)

2. **Baeldung – Kotlin Backing Fields** — [https://www.baeldung.com/kotlin/backing-fields](https://www.baeldung.com/kotlin/backing-fields)

3. **Android Developers – Classes and Objects in Kotlin** — [https://developer.android.com/kotlin/learn](https://developer.android.com/kotlin/learn)

---

# BAGIAN 10: PENUTUP

## 10.1 Pesan untuk Mahasiswa

> **“Enkapsulasi adalah senjata utama Anda untuk menulis kode yang aman dan mudah dipelihara.”**

Pertemuan 2 ini adalah **pondasi** dari praktik pemrograman yang profesional. Dengan memahami enkapsulasi, Anda tidak hanya bisa menulis kode yang **berfungsi**, tetapi juga kode yang:

- **Aman** — data tidak bisa diubah sembarangan
- **Terstruktur** — setiap kelas memiliki tanggung jawab yang jelas
- **Mudah dipelihara** — perubahan internal tidak merusak kode lain
- **Profesional** — mengikuti standar industri

**Ingatlah:**

1. Enkapsulasi adalah **cara berpikir**, bukan sekadar sintaks
2. Selalu tanyakan: **“Apakah data ini perlu diakses dari luar?”**
3. Jika ragu, buatlah **private** — Anda bisa mengubahnya menjadi public nanti, tapi tidak sebaliknya
4. **Latihan adalah kunci** — semakin banyak Anda menulis kode dengan enkapsulasi, semakin natural rasanya

## 10.2 Persiapan untuk Pertemuan 3

**Materi berikutnya: PEWARISAN (Inheritance)**

Apa yang akan dipelajari:

1. Konsep pewarisan (inheritance) di Kotlin
2. Keyword `open` dan `override`
3. Superclass dan subclass
4. Constructor dalam inheritance
5. Method overriding
6. Studi kasus: sistem kendaraan

**Tugas persiapan:**

- Baca modul tentang Inheritance
- Review kembali konsep kelas dan objek
- Pastikan semua latihan pertemuan 2 sudah selesai

---

**Disusun oleh,**
[Nama Dosen Pengampu]
Dosen Program Studi D4 Teknologi Rekayasa Informatika Industri
