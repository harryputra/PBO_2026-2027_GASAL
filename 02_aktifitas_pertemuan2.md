# RENCANA PEMBELAJARAN SEMESTER (RPS)
## PERTEMUAN KE-2 — RENCANA PELAKSANAAN PEMBELAJARAN (RPP)
### PEMROGRAMAN BERORIENTASI OBJEK (OBJECT-ORIENTED PROGRAMMING)
### “Enkapsulasi — Melindungi Data dari Dunia Luar”

---

## A. IDENTITAS PERTEMUAN

| **Komponen** | **Keterangan** |
|---|---|
| **Pertemuan Ke-** | 2 |
| **Topik** | Enkapsulasi (Encapsulation) — Access Modifier, Getter, Setter, dan Backing Field |
| **Durasi** | 8 Jam Praktik (480 menit) |
| **Hari/Tanggal** | [Disesuaikan] |
| **Ruang** | Laboratorium Komputer |
| **Dosen** | [Nama Dosen] |
| **Capaian Pembelajaran** | Mahasiswa memahami konsep enkapsulasi, mampu menerapkan access modifier (private, protected, internal, public), memahami serta mengimplementasikan getter dan setter (termasuk custom getter/setter dan private setter), serta memahami konsep backing field dalam Kotlin |

---

## B. CAPAIAN PEMBELAJARAN PERTEMUAN (CPP)

Setelah mengikuti pertemuan ke-2 ini, mahasiswa mampu:

1. **CPP 2.1:** Menjelaskan konsep enkapsulasi dan manfaatnya dalam pemrograman berorientasi objek.
2. **CPP 2.2:** Membedakan dan menggunakan empat access modifier di Kotlin: `private`, `protected`, `internal`, dan `public`.
3. **CPP 2.3:** Menjelaskan konsep getter dan setter serta perannya dalam enkapsulasi.
4. **CPP 2.4:** Mengimplementasikan custom getter dan setter dengan logika tambahan (validasi, formatting, logging).
5. **CPP 2.5:** Mengimplementasikan private setter untuk membuat properti yang hanya bisa diubah dari dalam kelas.
6. **CPP 2.6:** Menjelaskan dan menggunakan backing field (`field`) dalam custom setter.
7. **CPP 2.7:** Menerapkan prinsip enkapsulasi dalam studi kasus nyata (sistem perbankan/manajemen data).

---

## C. MATERI POKOK

### 1. Pendahuluan: Apa itu Enkapsulasi? (Sesi 1)

#### 1.1 Definisi Enkapsulasi

**Enkapsulasi** adalah salah satu dari **empat pilar OOP** yang bertujuan untuk **membungkus data (atribut) dan metode (perilaku)** yang beroperasi pada data tersebut ke dalam satu unit (kelas), serta **menyembunyikan detail implementasi internal** dari dunia luar.

> **Definisi Sederhana:** Enkapsulasi adalah **“mengunci” data di dalam kelas** sehingga tidak bisa diakses atau diubah secara sembarangan dari luar.

#### 1.2 Analogi Enkapsulasi dalam Kehidupan Nyata

| **Analogi** | **Penjelasan** |
|---|---|
| **ATM Bank** | Anda bisa melihat saldo dan menarik uang, tapi Anda tidak tahu bagaimana mesin ATM bekerja di dalam. Anda tidak bisa langsung mengubah saldo dengan menekan tombol tertentu — semua transaksi harus melalui proses yang valid. |
| **Mobil** | Anda bisa mengemudi mobil (menggunakan setir, gas, rem), tapi Anda tidak perlu tahu bagaimana mesin bekerja di dalam. Anda tidak bisa langsung mengubah kecepatan mesin dengan cara sembarangan. |
| **Smartphone** | Anda bisa menggunakan aplikasi, tapi Anda tidak bisa langsung mengubah kode sistem operasi di dalamnya. |
| **Kotak Amal** | Anda bisa memasukkan uang ke dalam kotak (metode `deposit`), tapi Anda tidak bisa langsung mengambil uang dari dalam tanpa kunci (metode `withdraw` yang terkontrol). |

#### 1.3 Mengapa Enkapsulasi Penting?

| **Manfaat** | **Penjelasan** |
|---|---|
| **Keamanan Data** | Mencegah data diubah secara tidak sah atau tidak sengaja |
| **Kontrol Akses** | Pengembang kelas bisa mengontrol bagaimana data diakses dan dimodifikasi |
| **Validasi Data** | Setiap perubahan data bisa divalidasi terlebih dahulu (misal: IPK tidak boleh < 0 atau > 4) |
| **Maintainability** | Perubahan internal tidak mempengaruhi kode di luar kelas (kode di luar hanya bergantung pada interface publik) |
| **Modularitas** | Setiap kelas menjadi unit yang mandiri dan tidak saling bergantung secara berlebihan |

#### 1.4 Prinsip Dasar Enkapsulasi

> **“Jadikan atribut private, sediakan metode publik untuk mengakses dan mengubahnya.”**

Ini adalah prinsip emas enkapsulasi:
- **Atribut** → dibuat **private** (atau protected)
- **Getter** → metode publik untuk **membaca** nilai atribut
- **Setter** → metode publik untuk **mengubah** nilai atribut (dengan validasi)

---

### 2. Access Modifier di Kotlin (Sesi 1)

Kotlin menyediakan **empat access modifier** (visibility modifier) untuk mengontrol siapa yang bisa mengakses kelas, properti, metode, dan konstruktor:

| **Modifier** | **Visibilitas** | **Kapan Digunakan** |
|---|---|---|
| **`public`** (default) | Terlihat **di mana saja** | Untuk API publik kelas |
| **`private`** | Terlihat **hanya di dalam kelas** yang sama | Untuk menyembunyikan detail implementasi |
| **`protected`** | Terlihat di dalam kelas **dan di subclass** | Untuk member yang boleh diwariskan |
| **`internal`** | Terlihat **di dalam modul yang sama** | Untuk API internal modul |

> **Catatan Penting:** Di Kotlin, **default visibility adalah `public`** — berbeda dengan Java yang default-nya `package-private`.

#### 2.1 Access Modifier untuk Properti

```kotlin
class Contoh {
    // PUBLIC (default) — bisa diakses dari mana saja
    var publicProperty: String = "public"

    // PRIVATE — hanya bisa diakses di dalam kelas ini
    private var privateProperty: String = "private"

    // PROTECTED — bisa diakses di dalam kelas dan subclass
    protected var protectedProperty: String = "protected"

    // INTERNAL — bisa diakses di dalam modul yang sama
    internal var internalProperty: String = "internal"
}
```

#### 2.2 Access Modifier untuk Getter dan Setter

Getter selalu memiliki visibilitas yang sama dengan propertinya. Namun, **setter bisa memiliki visibilitas yang berbeda**:

```kotlin
class Contoh {
    // Properti public, tapi setter-nya private
    var counter: Int = 0
        private set  // Hanya kelas ini yang bisa mengubah nilai

    // Properti public, setter-nya internal
    var data: String = ""
        internal set
}
```

#### 2.3 Access Modifier untuk Konstruktor

```kotlin
// Primary constructor private — kelas tidak bisa diinstansiasi dari luar
class Singleton private constructor() {
    companion object {
        fun getInstance() = Singleton()
    }
}

// Primary constructor public (default)
class Mahasiswa(val nama: String)  // public secara default
```

---

### 3. Getter dan Setter di Kotlin (Sesi 2)

#### 3.1 Apa itu Getter dan Setter?

Di Kotlin, setiap properti secara otomatis memiliki **getter** (untuk membaca nilai) dan **setter** (untuk mengubah nilai).

| **Istilah** | **Fungsi** | **Sintaks** |
|---|---|---|
| **Getter** (`get()`) | Membaca nilai properti | Dipanggil saat properti diakses: `obj.properti` |
| **Setter** (`set(value)`) | Mengubah nilai properti | Dipanggil saat properti diubah: `obj.properti = nilai` |

#### 3.2 Default Getter dan Setter

Saat Anda mendeklarasikan properti, Kotlin secara otomatis menghasilkan getter dan setter default:

```kotlin
class Mahasiswa {
    var nama: String = ""
    // Secara otomatis menghasilkan:
    // get() = field
    // set(value) { field = value }
}
```

Di balik layar, kode di atas setara dengan:

```kotlin
class Mahasiswa {
    var nama: String = ""
        get() = field
        set(value) {
            field = value
        }
}
```

#### 3.3 Custom Getter (Getter Kustom)

Custom getter digunakan ketika Anda perlu **logika tambahan** saat membaca properti, seperti:
- Menghitung nilai dari properti lain
- Memformat data
- Validasi saat pembacaan

**Contoh 1: Properti Terhitung (Computed Property)**

```kotlin
class PersegiPanjang(val lebar: Int, val tinggi: Int) {
    // Luas dihitung dari lebar dan tinggi — tidak disimpan sebagai field
    val luas: Int
        get() = lebar * tinggi  // Dipanggil setiap kali diakses
}

fun main() {
    val pp = PersegiPanjang(5, 3)
    println(pp.luas)  // Output: 15
}
```

**Contoh 2: Custom Getter dengan Formatting**

```kotlin
class Mahasiswa(val nama: String, val ipk: Double) {
    // Nama selalu ditampilkan dengan huruf kapital di awal
    val namaFormal: String
        get() = nama.replaceFirstChar { if (it.isLowerCase()) it.titlecase(Locale.getDefault()) else it.toString() }

    // IPK ditampilkan dengan 2 angka di belakang koma
    val ipkFormatted: String
        get() = "%.2f".format(ipk)
}

fun main() {
    val mhs = Mahasiswa("budi santoso", 3.756)
    println(mhs.namaFormal)     // Output: Budi Santoso
    println(mhs.ipkFormatted)   // Output: 3.76
}
```

#### 3.4 Custom Setter (Setter Kustom)

Custom setter digunakan ketika Anda perlu **logika tambahan** saat mengubah nilai properti, seperti:
- **Validasi** nilai sebelum disimpan
- **Logging** (mencatat perubahan)
- **Notifikasi** (memberi tahu bagian lain tentang perubahan)
- **Konversi** nilai sebelum disimpan

**Contoh 1: Setter dengan Validasi**

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

**Contoh 2: Setter dengan Logging**

```kotlin
class BankAccount {
    var balance: Int = 0
        private set(value) {  // Private setter dengan logging
            println("💰 Saldo berubah: $field → $value")
            field = value
        }

    fun deposit(amount: Int) {
        require(amount > 0) { "Jumlah deposit harus positif" }
        balance += amount
    }

    fun withdraw(amount: Int) {
        require(amount > 0) { "Jumlah penarikan harus positif" }
        require(amount <= balance) { "Saldo tidak mencukupi" }
        balance -= amount
    }
}

fun main() {
    val account = BankAccount()
    account.deposit(100)   // Output: 💰 Saldo berubah: 0 → 100
    account.withdraw(50)   // Output: 💰 Saldo berubah: 100 → 50
    // account.balance = 999  // ❌ ERROR: Cannot assign to 'balance': the setter is private
}
```

---

### 4. Backing Field (`field`) (Sesi 2)

#### 4.1 Apa itu Backing Field?

**Backing field** adalah **variabel tersembunyi** yang menyimpan nilai aktual dari sebuah properti.

| **Konsep** | **Penjelasan** |
|---|---|
| **Backing Field** | Tempat penyimpanan nilai properti yang sebenarnya |
| **Keyword `field`** | Digunakan di dalam getter/setter untuk mengakses backing field |
| **Kapan ada?** | Jika menggunakan getter/setter default ATAU menggunakan keyword `field` |

#### 4.2 Mengapa Perlu Backing Field?

**Masalah:** Jika di dalam setter Anda mengakses properti secara langsung (bukan `field`), akan terjadi **rekursi tak terbatas (infinite loop)** yang menyebabkan `StackOverflowError`.

```kotlin
// ❌ SALAH — infinite loop!
class Salah {
    var nilai: Int = 0
        set(value) {
            nilai = value  // Memanggil setter lagi! → StackOverflowError
        }
}

// ✅ BENAR — menggunakan backing field
class Benar {
    var nilai: Int = 0
        set(value) {
            field = value  // Mengakses backing field langsung
        }
}
```

#### 4.3 Cara Kerja Backing Field

```kotlin
class Contoh {
    var data: String = "default"
        get() = field                    // Mengembalikan nilai dari backing field
        set(value) {
            field = value                // Menyimpan nilai ke backing field
        }
}
```

**Ilustrasi:**

```
┌─────────────────────────────────────┐
│           OBJEK Contoh              │
│                                     │
│  ┌───────────────────────────────┐  │
│  │      Backing Field (field)    │  │
│  │     nilai: "default"          │  │
│  └───────────────────────────────┘  │
│                                     │
│  get() = field  ←─── membaca dari   │
│  set(value) { field = value }       │
│                 ←─── menulis ke     │
└─────────────────────────────────────┘
```

#### 4.4 Kapan Backing Field Tidak Ada?

Backing field **tidak ada** jika properti tidak menggunakan default getter/setter dan tidak menggunakan keyword `field`.

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

---

### 5. Private Setter — Public Getter (Sesi 3)

#### 5.1 Konsep Private Setter

**Private setter** adalah teknik enkapsulasi di mana properti memiliki **getter public** (bisa dibaca dari mana saja) tetapi **setter private** (hanya bisa diubah dari dalam kelas).

> **Manfaat:** Properti bersifat **read-only dari luar**, tetapi **writeable dari dalam** kelas.

#### 5.2 Sintaks Private Setter

```kotlin
class Contoh {
    var counter: Int = 0
        private set  // Setter private, getter public (default)

    fun increment() {
        counter++  // ✅ Bisa diubah dari dalam kelas
    }
}

fun main() {
    val obj = Contoh()
    println(obj.counter)  // ✅ Bisa dibaca: 0
    obj.increment()
    println(obj.counter)  // ✅ Bisa dibaca: 1
    // obj.counter = 10   // ❌ ERROR: Cannot assign to 'counter': the setter is private
}
```

#### 5.3 Private Setter dengan Custom Logic

```kotlin
class BankAccount {
    var balance: Int = 0
        private set(value) {  // Private setter dengan validasi
            require(value >= 0) { "Saldo tidak boleh negatif" }
            field = value
        }

    fun deposit(amount: Int) {
        require(amount > 0) { "Deposit harus positif" }
        balance += amount
    }

    fun withdraw(amount: Int) {
        require(amount > 0) { "Penarikan harus positif" }
        require(amount <= balance) { "Saldo tidak mencukupi" }
        balance -= amount
    }
}
```

#### 5.4 Contoh Kasus: Sistem Bank

**Studi Kasus Lengkap — Rekening Bank:**

```kotlin
/**
 * Kelas RekeningBank merepresentasikan rekening bank dengan enkapsulasi penuh
 *
 * Prinsip: Saldo hanya bisa diubah melalui metode deposit() dan withdraw()
 * Tidak ada akses langsung dari luar untuk mengubah saldo
 */
class RekeningBank(
    private val nomorRekening: String,
    private val namaPemilik: String
) {
    // Saldo: public getter, private setter
    var saldo: Long = 0
        private set  // Hanya kelas ini yang bisa mengubah saldo

    // Riwayat transaksi: private — tidak terlihat dari luar
    private val riwayatTransaksi = mutableListOf<String>()

    /**
     * Menyetor uang ke rekening
     * @param jumlah Jumlah uang yang disetor (harus > 0)
     * @return true jika berhasil
     */
    fun deposit(jumlah: Long): Boolean {
        return if (jumlah > 0) {
            saldo += jumlah
            riwayatTransaksi.add("💰 DEPOSIT: +Rp $jumlah")
            println("✅ Deposit Rp $jumlah berhasil. Saldo: Rp $saldo")
            true
        } else {
            println("❌ Jumlah deposit harus lebih dari 0")
            false
        }
    }

    /**
     * Menarik uang dari rekening
     * @param jumlah Jumlah uang yang ditarik (harus > 0 dan <= saldo)
     * @return true jika berhasil
     */
    fun withdraw(jumlah: Long): Boolean {
        return when {
            jumlah <= 0 -> {
                println("❌ Jumlah penarikan harus lebih dari 0")
                false
            }
            jumlah > saldo -> {
                println("❌ Saldo tidak mencukupi. Saldo: Rp $saldo")
                false
            }
            else -> {
                saldo -= jumlah
                riwayatTransaksi.add("🏧 WITHDRAW: -Rp $jumlah")
                println("✅ Penarikan Rp $jumlah berhasil. Saldo: Rp $saldo")
                true
            }
        }
    }

    /**
     * Menampilkan informasi rekening
     */
    fun tampilkanInfo() {
        println("=" .repeat(50))
        println("🏦 INFORMASI REKENING")
        println("=" .repeat(50))
        println("Nomor Rekening: $nomorRekening")
        println("Nama Pemilik  : $namaPemilik")
        println("Saldo         : Rp $saldo")
        println("=" .repeat(50))
    }

    /**
     * Menampilkan riwayat transaksi (hanya 5 transaksi terakhir)
     */
    fun tampilkanRiwayat() {
        println("=" .repeat(50))
        println("📋 RIWAYAT TRANSAKSI (5 Terakhir)")
        println("=" .repeat(50))
        val start = if (riwayatTransaksi.size > 5) riwayatTransaksi.size - 5 else 0
        for (i in start until riwayatTransaksi.size) {
            println("  ${i + 1}. ${riwayatTransaksi[i]}")
        }
        println("=" .repeat(50))
    }
}

fun main() {
    val rekening = RekeningBank("1234567890", "Budi Santoso")

    rekening.tampilkanInfo()
    println()

    // Melakukan transaksi
    rekening.deposit(500000)
    rekening.deposit(250000)
    rekening.withdraw(100000)
    rekening.withdraw(700000)  // Gagal — saldo tidak cukup
    rekening.deposit(1000000)
    rekening.withdraw(1500000)

    println()
    rekening.tampilkanInfo()
    println()
    rekening.tampilkanRiwayat()

    // ❌ Tidak bisa mengubah saldo langsung dari luar!
    // rekening.saldo = 9999999  // ERROR: Cannot assign to 'saldo': the setter is private
}
```

---

### 6. Best Practices Enkapsulasi di Kotlin (Sesi 3)

| **Praktik Terbaik** | **Penjelasan** | **Contoh** |
|---|---|---|
| **Gunakan `private` secara default** | Properti dan metode yang tidak perlu diakses dari luar harus `private` | `private var counter: Int = 0` |
| **Gunakan `val` daripada `var`** | Jika properti tidak perlu diubah, gunakan `val` (read-only) | `val nim: String` |
| **Private setter untuk properti mutable** | Jika properti perlu diubah dari dalam kelas, gunakan `private set` | `var saldo: Long = 0 private set` |
| **Validasi di setter** | Selalu validasi nilai sebelum menyimpan ke backing field | `set(value) { if (value >= 0) field = value }` |
| **Jangan expose backing field** | Backing field (`field`) hanya boleh diakses di dalam getter/setter | - |
| **Gunakan metode daripada setter publik** | Untuk operasi kompleks, sediakan metode而非setter publik | `fun deposit(amount: Int)` bukan `balance = ...` |
| **Jaga agar API publik minimal** | Semakin sedikit yang diekspos, semakin mudah maintenance | - |

---

## D. RINCIAN KEGIATAN PEMBELAJARAN (8 JAM)

### Sesi 1: Pengantar & Teori Enkapsulasi + Access Modifier (2 Jam — 120 menit)

| **Waktu** | **Kegiatan** | **Detail** | **Metode** |
|---|---|---|---|
| **0-10'** | Pembukaan & Review | • Dosen membuka perkuliahan dengan salam dan doa<br>• Review singkat materi pertemuan 1 (kelas, objek, properti, metode)<br>• Menghubungkan materi sebelumnya dengan enkapsulasi | Ceramah interaktif, Tanya jawab |
| **10-40'** | Konsep Enkapsulasi | • **Definisi enkapsulasi** — membungkus data dan metode dalam satu unit<br>• **Analogi enkapsulasi** (ATM, mobil, smartphone, kotak amal)<br>• **Mengapa enkapsulasi penting?** — keamanan, kontrol, validasi, maintainability<br>• **Prinsip emas:** atribut private, metode publik untuk akses<br>• Diskusi: "Apa yang terjadi jika data bisa diubah sembarangan dari luar?" | Ceramah, Analogi, Diskusi |
| **40-70'** | Access Modifier di Kotlin | • **Empat access modifier:** `private`, `protected`, `internal`, `public`<br>• Perbedaan visibilitas masing-masing modifier<br>• **Default visibility** di Kotlin adalah `public`<br>• Access modifier untuk properti, metode, dan konstruktor<br>• **Getter vs Setter visibility** — getter selalu sama dengan properti, setter bisa berbeda<br>• Demo kode: Membandingkan keempat modifier | Ceramah, Demonstrasi, Tanya jawab |
| **70-90'** | Praktik Access Modifier | • Mahasiswa membuat kelas dengan keempat access modifier<br>• Mencoba mengakses dari dalam kelas, dari subclass, dari kelas lain<br>• Mengamati error yang muncul saat akses ditolak | Praktik terbimbing |
| **90-120'** | Diskusi & Review | • Diskusi kelompok: "Kapan menggunakan private, protected, internal, dan public?"<br>• Dosen memberikan contoh kasus nyata<br>• Q&A dan penyimpulan | Diskusi kelompok, Tanya jawab |

---

### Sesi 2: Getter, Setter, dan Backing Field (2 Jam — 120 menit)

| **Waktu** | **Kegiatan** | **Detail** | **Metode** |
|---|---|---|---|
| **0-10'** | Review Singkat | • Mereview access modifier<br>• Menghubungkan dengan getter/setter | Ceramah |
| **10-40'** | Getter dan Setter Dasar | • **Apa itu getter dan setter?** — accessor untuk properti<br>• **Default getter dan setter** — otomatis dihasilkan oleh Kotlin<br>• **Sintaks** getter dan setter di Kotlin<br>• Perbedaan `val` (hanya getter) dan `var` (getter + setter)<br>• Demo: Melihat bytecode/decompiled Java untuk melihat getter/setter | Ceramah, Demonstrasi |
| **40-70'** | Custom Getter dan Setter | • **Custom getter** — logika tambahan saat membaca<br>  - Properti terhitung (computed property)<br>  - Formatting data<br>• **Custom setter** — logika tambahan saat mengubah<br>  - Validasi nilai<br>  - Logging<br>  - Notifikasi<br>• Demo: Implementasi custom getter dan setter | Ceramah, Demonstrasi, Live Coding |
| **70-90'** | Backing Field (`field`) | • **Apa itu backing field?** — tempat penyimpanan nilai aktual<br>• **Keyword `field`** — mengakses backing field di getter/setter<br>• **Kapan backing field ada?**<br>• **Bahaya infinite loop** jika mengakses properti langsung di setter<br>• Demo: Perbedaan `field` vs akses properti langsung | Ceramah, Demonstrasi |
| **90-120'** | Praktik Getter/Setter/Backing Field | • Mahasiswa membuat kelas dengan custom getter dan setter<br>• Implementasi validasi di setter<br>• Praktik menggunakan backing field<br>• Dosen berkeliling memberikan asistensi | Praktik mandiri, Asistensi |

---

### Sesi 3: Private Setter & Studi Kasus (2 Jam — 120 menit)

| **Waktu** | **Kegiatan** | **Detail** | **Metode** |
|---|---|---|---|
| **0-10'** | Review & Motivasi | • Review custom getter/setter<br>• "Bagaimana membuat properti yang hanya bisa dibaca dari luar tapi bisa diubah dari dalam?" | Ceramah |
| **10-40'** | Private Setter — Public Getter | • **Konsep private setter** — read-only dari luar, writeable dari dalam<br>• **Sintaks** private setter<br>• **Manfaat:** menjaga konsistensi data, mencegah modifikasi tidak sah<br>• **Private setter dengan custom logic**<br>• Demo: Implementasi private setter | Ceramah, Demonstrasi |
| **40-70'** | Studi Kasus: Sistem Perbankan | • **Analisis kebutuhan sistem perbankan**<br>  - Saldo tidak boleh diubah langsung dari luar<br>  - Deposit dan withdraw harus melalui metode dengan validasi<br>  - Riwayat transaksi harus dicatat<br>• **Perancangan kelas** `RekeningBank` dengan enkapsulasi penuh<br>• **Live coding** bersama dosen<br>• Menjelaskan setiap bagian kode | Demonstrasi, Live Coding, Diskusi |
| **70-90'** | Praktik Sistem Perbankan | • Mahasiswa mengimplementasikan sistem perbankan sendiri<br>• Menambahkan fitur: transfer antar rekening, cek saldo, riwayat<br>• Dosen memberikan asistensi | Praktik mandiri, Asistensi |
| **90-120'** | Review & Diskusi Kasus | • Beberapa mahasiswa mempresentasikan kode mereka<br>• Diskusi: "Apa yang terjadi jika kita tidak menggunakan enkapsulasi?"<br>• Best practices enkapsulasi di Kotlin | Presentasi, Diskusi |

---

### Sesi 4: Tugas 2 & Penutupan (2 Jam — 120 menit)

| **Waktu** | **Kegiatan** | **Detail** | **Metode** |
|---|---|---|---|
| **0-15'** | Review Materi Pertemuan 2 | • Rangkuman seluruh materi:<br>  - Enkapsulasi dan manfaatnya<br>  - 4 access modifier di Kotlin<br>  - Getter, setter, custom accessor<br>  - Backing field (`field`)<br>  - Private setter<br>• Menjawab pertanyaan mahasiswa | Review, Tanya jawab |
| **15-90'** | Pengerjaan Tugas 2 | • Mahasiswa mengerjakan Tugas 2 secara mandiri (lihat bagian E)<br>• Dosen berkeliling memberikan bimbingan intensif<br>• Mahasiswa dapat bertanya jika mengalami kendala | Praktik mandiri, Asistensi intensif |
| **90-105'** | Pengumpulan & Presentasi | • Mahasiswa mengumpulkan Tugas 2<br>• 2-3 mahasiswa diminta mempresentasikan kodenya<br>• Dosen memberikan feedback konstruktif | Presentasi, Feedback |
| **105-120'** | Penutupan | • Dosen merangkum pencapaian pertemuan 2<br>• Preview materi pertemuan 3 (Pewarisan/Inheritance)<br>• Memberikan tugas membaca modul pertemuan 3<br>• Menutup perkuliahan dengan doa dan salam | Ceramah |

---

## E. TUGAS 2 (Dikumpulkan)

### Sistem Manajemen Perpustakaan dengan Enkapsulasi Penuh

Buatlah program lengkap sistem manajemen perpustakaan dengan ketentuan berikut:

#### 1. Kelas `Buku`

| **Komponen** | **Spesifikasi** |
|---|---|
| **Properti** | `judul: String` (read-only, dari constructor)<br>`penulis: String` (read-only, dari constructor)<br>`isbn: String` (read-only, dari constructor)<br>`tahunTerbit: Int` (read-only, dari constructor)<br>`isDipinjam: Boolean` (private setter — hanya bisa diubah dari dalam kelas)<br>`peminjam: String?` (private setter — nullable) |
| **Metode** | `pinjam(namaPeminjam: String): Boolean` → meminjam buku jika tersedia<br>`kembalikan(): Boolean` → mengembalikan buku<br>`tampilkanInfo(): String` → menampilkan informasi buku<br>`isTersedia(): Boolean` → mengecek ketersediaan |

#### 2. Kelas `Perpustakaan`

| **Komponen** | **Spesifikasi** |
|---|---|
| **Properti** | `nama: String` (read-only, dari constructor)<br>`daftarBuku: MutableList<Buku>` (private — hanya bisa diakses dari dalam kelas) |
| **Metode** | `tambahBuku(buku: Buku)` → menambah buku ke daftar<br>`cariBuku(keyword: String): List<Buku>` → mencari buku berdasarkan judul/penulis<br>`pinjamBuku(isbn: String, peminjam: String): Boolean` → meminjam buku berdasarkan ISBN<br>`kembalikanBuku(isbn: String): Boolean` → mengembalikan buku berdasarkan ISBN<br>`tampilkanSemuaBuku()` → menampilkan semua buku<br>`tampilkanBukuTersedia()` → menampilkan buku yang tersedia<br>`tampilkanBukuDipinjam()` → menampilkan buku yang sedang dipinjam |

#### 3. Fungsi `main()`

- Buat objek `Perpustakaan` dengan nama "Perpustakaan Kampus"
- Tambahkan **minimal 5 buku** dengan data berbeda
- Tampilkan semua buku
- Lakukan peminjaman buku oleh beberapa mahasiswa
- Tampilkan buku yang tersedia dan yang dipinjam
- Kembalikan salah satu buku
- Tampilkan status akhir semua buku

#### 4. Kriteria Penilaian Tugas 2

| **Kriteria** | **Bobot** | **Indikator** |
|---|---|---|
| **Enkapsulasi Kelas Buku** | 30% | • Properti `isDipinjam` dan `peminjam` memiliki private setter<br>• Metode `pinjam()` dan `kembalikan()` memvalidasi status<br>• Tidak ada akses langsung ke properti internal dari luar |
| **Enkapsulasi Kelas Perpustakaan** | 25% | • `daftarBuku` bersifat private<br>• Metode publik menyediakan akses terkontrol ke data |
| **Fungsi main()** | 20% | • Menampilkan semua skenario yang diminta<br>• Output jelas dan informatif |
| **Kode Berkualitas** | 15% | • Kode bersih, terstruktur, diberi komentar<br>• Menggunakan naming convention yang benar<br>• Tidak ada kode yang tidak digunakan |
| **Program Berjalan** | 10% | • Program berjalan tanpa error<br>• Semua fungsi berfungsi sesuai spesifikasi |

---

## F. MEDIA DAN ALAT PEMBELAJARAN

| **Media** | **Keterangan** |
|---|---|
| **Laptop/PC** | Setiap mahasiswa menggunakan laptop/PC masing-masing |
| **IntelliJ IDEA** | IDE utama untuk pengembangan Kotlin |
| **JDK** | Java Development Kit (versi 11 atau 17) |
| **Proyektor/LCD** | Untuk presentasi dan demonstrasi dosen |
| **Whiteboard** | Untuk menjelaskan konsep dan access modifier |
| **Modul Praktikum** | Modul cetak/digital pertemuan 2 |
| **Kotlin Playground** | Alternatif untuk mencoba kode tanpa instalasi |

---

## G. PENILAIAN PERTEMUAN 2

| **Komponen** | **Bobot** | **Indikator** | **Teknik** |
|---|---|---|---|
| **Keaktifan Sesi 1-3** | 15% dari total keaktifan | • Kehadiran tepat waktu<br>• Partisipasi dalam diskusi dan tanya jawab<br>• Keterlibatan dalam praktik kelompok | Observasi |
| **Tugas 2** | 100% dari nilai tugas 2 | • Lihat kriteria penilaian Tugas 2 di atas | Penilaian kode |
| **Kuis Singkat** | Bonus | • Pertanyaan tentang access modifier dan getter/setter | Tes tertulis/lisan |

---

## H. REFERENSI PERTEMUAN 2

### Referensi Utama:

1. **Kotlin Official Documentation – Visibility Modifiers** — [https://kotlinlang.org/docs/visibility-modifiers.html](https://kotlinlang.org/docs/visibility-modifiers.html)
2. **Kotlin Official Documentation – Properties** — [https://kotlinlang.org/docs/properties.html](https://kotlinlang.org/docs/properties.html)
3. **Kotlin Tour – Intermediate Properties** — [https://kotlinlang.org/docs/kotlin-tour-intermediate-properties.html](https://kotlinlang.org/docs/kotlin-tour-intermediate-properties.html)

### Referensi Pendukung:

4. **Baeldung – Public Getter and Private Setter in Kotlin** — [https://www.baeldung-cn.com/kotlin/public-getter-private-setter](https://www.baeldung-cn.com/kotlin/public-getter-private-setter)
5. **Android Developers – Classes and Objects in Kotlin** — [https://developer.android.com/kotlin/learn](https://developer.android.com/kotlin/learn)

---

## I. LAMPIRAN

### Lampiran 1: Kode Lengkap Sistem Perbankan (Solusi Referensi)

```kotlin
/**
 * ============================================================
 * SISTEM PERBANKAN SEDERHANA DENGAN ENKAPSULASI PENUH
 * ============================================================
 * Demonstrasi penggunaan:
 * 1. Access modifier (private, public)
 * 2. Private setter
 * 3. Custom getter
 * 4. Backing field (field)
 * 5. Enkapsulasi data
 * ============================================================
 */

/**
 * Kelas RekeningBank — merepresentasikan rekening bank
 *
 * Prinsip Enkapsulasi:
 * - Saldo (balance) hanya bisa diubah melalui metode deposit() dan withdraw()
 * - Riwayat transaksi (transactionHistory) hanya bisa diakses dari dalam kelas
 * - Nomor rekening dan nama pemilik tidak bisa diubah setelah dibuat
 */
class RekeningBank(
    private val nomorRekening: String,
    private val namaPemilik: String
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
    var saldo: Long = 0
        private set

    /**
     * Riwayat transaksi — private, hanya bisa diakses dari dalam kelas
     * Tidak ada getter/setter — benar-benar tersembunyi dari luar
     */
    private val riwayatTransaksi = mutableListOf<String>()

    /**
     * Jumlah transaksi — custom getter (dihitung dari riwayat)
     * Ini adalah computed property — tidak ada backing field
     */
    val jumlahTransaksi: Int
        get() = riwayatTransaksi.size

    /**
     * Status rekening — custom getter dengan logika
     */
    val status: String
        get() = when {
            saldo > 100000000 -> "💎 Premium"
            saldo > 10000000 -> "⭐ Gold"
            saldo > 1000000 -> "🥈 Silver"
            saldo > 0 -> "🥉 Bronze"
            else -> "⚫ Tidak Aktif"
        }

    // ============================================================
    // METODE
    // ============================================================

    /**
     * Menyetor uang ke rekening
     *
     * @param jumlah Jumlah uang yang disetor (harus > 0)
     * @return true jika berhasil, false jika gagal
     */
    fun deposit(jumlah: Long): Boolean {
        // Validasi: jumlah harus positif
        if (jumlah <= 0) {
            println("❌ ERROR: Jumlah deposit harus lebih dari 0")
            return false
        }

        // Update saldo (menggunakan operator += yang memanggil setter)
        saldo += jumlah

        // Catat riwayat
        riwayatTransaksi.add("💰 DEPOSIT: +Rp ${formatRupiah(jumlah)}")
        println("✅ Deposit Rp ${formatRupiah(jumlah)} berhasil")
        return true
    }

    /**
     * Menarik uang dari rekening
     *
     * @param jumlah Jumlah uang yang ditarik (harus > 0 dan <= saldo)
     * @return true jika berhasil, false jika gagal
     */
    fun withdraw(jumlah: Long): Boolean {
        // Validasi: jumlah harus positif
        if (jumlah <= 0) {
            println("❌ ERROR: Jumlah penarikan harus lebih dari 0")
            return false
        }

        // Validasi: saldo harus mencukupi
        if (jumlah > saldo) {
            println("❌ ERROR: Saldo tidak mencukupi")
            println("   Saldo: Rp ${formatRupiah(saldo)}")
            println("   Dibutuhkan: Rp ${formatRupiah(jumlah)}")
            return false
        }

        // Update saldo
        saldo -= jumlah

        // Catat riwayat
        riwayatTransaksi.add("🏧 WITHDRAW: -Rp ${formatRupiah(jumlah)}")
        println("✅ Penarikan Rp ${formatRupiah(jumlah)} berhasil")
        return true
    }

    /**
     * Transfer uang ke rekening lain
     *
     * @param tujuan Rekening tujuan
     * @param jumlah Jumlah uang yang ditransfer
     * @return true jika berhasil, false jika gagal
     */
    fun transfer(tujuan: RekeningBank, jumlah: Long): Boolean {
        // Validasi: tidak bisa transfer ke diri sendiri
        if (this === tujuan) {
            println("❌ ERROR: Tidak bisa transfer ke rekening sendiri")
            return false
        }

        // Tarik dari rekening ini
        if (!withdraw(jumlah)) {
            return false
        }

        // Setor ke rekening tujuan
        tujuan.deposit(jumlah)

        // Catat riwayat tambahan
        riwayatTransaksi.add("🔄 TRANSFER KELUAR: -Rp ${formatRupiah(jumlah)} ke ${tujuan.namaPemilik}")
        println("✅ Transfer Rp ${formatRupiah(jumlah)} ke ${tujuan.namaPemilik} berhasil")
        return true
    }

    /**
     * Menampilkan informasi rekening
     */
    fun tampilkanInfo() {
        println("=" .repeat(55))
        println("🏦 INFORMASI REKENING")
        println("=" .repeat(55))
        println("Nomor Rekening : $nomorRekening")
        println("Nama Pemilik   : $namaPemilik")
        println("Saldo          : Rp ${formatRupiah(saldo)}")
        println("Status         : $status")
        println("Total Transaksi: $jumlahTransaksi")
        println("=" .repeat(55))
    }

    /**
     * Menampilkan riwayat transaksi
     *
     * @param limit Jumlah transaksi yang ditampilkan (default: semua)
     */
    fun tampilkanRiwayat(limit: Int = riwayatTransaksi.size) {
        println("=" .repeat(55))
        println("📋 RIWAYAT TRANSAKSI (${minOf(limit, riwayatTransaksi.size)} terakhir)")
        println("=" .repeat(55))

        if (riwayatTransaksi.isEmpty()) {
            println("   Belum ada transaksi")
        } else {
            val start = maxOf(0, riwayatTransaksi.size - limit)
            for (i in start until riwayatTransaksi.size) {
                println("   ${i + 1}. ${riwayatTransaksi[i]}")
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
    val rekeningBudi = RekeningBank("1234567890", "Budi Santoso")
    val rekeningSiti = RekeningBank("0987654321", "Siti Rahayu")

    // Tampilkan info awal
    println("--- INFO REKENING AWAL ---")
    rekeningBudi.tampilkanInfo()
    println()
    rekeningSiti.tampilkanInfo()
    println()

    // Lakukan transaksi
    println("--- MELAKUKAN TRANSAKSI ---")
    rekeningBudi.deposit(500000)
    rekeningBudi.deposit(250000)
    rekeningSiti.deposit(1000000)
    rekeningBudi.withdraw(100000)
    rekeningBudi.transfer(rekeningSiti, 200000)
    rekeningBudi.withdraw(700000)  // Gagal — saldo tidak cukup
    println()

    // Tampilkan info akhir
    println("--- INFO REKENING AKHIR ---")
    rekeningBudi.tampilkanInfo()
    println()
    rekeningSiti.tampilkanInfo()
    println()

    // Tampilkan riwayat
    rekeningBudi.tampilkanRiwayat(5)
    println()
    rekeningSiti.tampilkanRiwayat()

    // Demonstrasi bahwa saldo tidak bisa diubah langsung dari luar
    println()
    println("--- DEMONSTRASI ENKAPSULASI ---")
    println("Mencoba mengubah saldo langsung dari luar...")
    // rekeningBudi.saldo = 9999999  // ❌ ERROR: Cannot assign to 'saldo': the setter is private
    println("✅ Saldo TIDAK BISA diubah langsung dari luar — enkapsulasi berhasil!")

    println()
    println("=" .repeat(55))
    println("🏁 PROGRAM SELESAI")
    println("=" .repeat(55))
}
```

### Lampiran 2: Perbandingan Access Modifier di Java vs Kotlin

| **Java** | **Kotlin** | **Perbedaan** |
|---|---|---|
| `public` | `public` | Sama — visible everywhere |
| `private` | `private` | Sama — visible only in class |
| `protected` | `protected` | Kotlin: visible in class + subclasses |
| `default` (package-private) | `internal` | Kotlin `internal` = visible in same module |
| Tidak ada | `internal` | Fitur baru di Kotlin |

### Lampiran 3: Checklist Pemahaman Mahasiswa

| **No** | **Konsep** | **Paham** | **Kurang Paham** | **Tidak Paham** |
|---|---|---|---|---|
| 1 | Definisi enkapsulasi | ☐ | ☐ | ☐ |
| 2 | Manfaat enkapsulasi | ☐ | ☐ | ☐ |
| 3 | Access modifier `private` | ☐ | ☐ | ☐ |
| 4 | Access modifier `protected` | ☐ | ☐ | ☐ |
| 5 | Access modifier `internal` | ☐ | ☐ | ☐ |
| 6 | Access modifier `public` | ☐ | ☐ | ☐ |
| 7 | Default visibility di Kotlin | ☐ | ☐ | ☐ |
| 8 | Konsep getter dan setter | ☐ | ☐ | ☐ |
| 9 | Custom getter | ☐ | ☐ | ☐ |
| 10 | Custom setter dengan validasi | ☐ | ☐ | ☐ |
| 11 | Backing field (`field`) | ☐ | ☐ | ☐ |
| 12 | Private setter | ☐ | ☐ | ☐ |
| 13 | Menerapkan enkapsulasi dalam kode | ☐ | ☐ | ☐ |

---

**Disusun oleh,**
[Nama Dosen Pengampu]
Dosen Program Studi D4 Teknologi Rekayasa Informatika Industri
