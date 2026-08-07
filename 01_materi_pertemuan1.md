# MATERI AJAR PERTEMUAN 1

## PEMROGRAMAN BERORIENTASI OBJEK (OOP) DENGAN KOTLIN

### “Dari Nol Menjadi Programmer OOP — Fondasi untuk Mobile Programming”

---

# BAGIAN 1: PENDAHULUAN DAN KONSEP DASAR OOP

## 1.1 Selamat Datang di Dunia Pemrograman Berorientasi Objek

### Apa itu Pemrograman?

Sebelum kita bicara tentang OOP, mari kita pahami dulu apa itu **pemrograman**. Pemrograman adalah proses menulis instruksi (kode) yang告诉 komputer apa yang harus dilakukan. Komputer adalah mesin yang sangat pintar tetapi juga sangat **bodoh** — ia hanya melakukan apa yang kita perintahkan, tidak lebih, tidak kurang.

### Paradigma Pemrograman

Paradigma pemrograman adalah **gaya** atau **cara berpikir** dalam menulis kode. Ada beberapa paradigma utama:

| **Paradigma** | **Deskripsi** | **Contoh Bahasa** |
| --- | --- | --- |
| **Prosedural** | Program ditulis sebagai urutan instruksi/langkah demi langkah | C, Pascal, BASIC |
| **Fungsional** | Program dibangun dari fungsi-fungsi murni (tanpa efek samping) | Haskell, Lisp, Erlang |
| **Berorientasi Objek (OOP)** | Program dibangun dari **objek** yang memiliki **data** dan **perilaku** | Java, C++, Python, Kotlin, C# |

### Mengapa OOP?

OOP lahir karena kebutuhan untuk mengelola **kompleksitas perangkat lunak**. Bayangkan Anda membuat aplikasi e-commerce seperti Tokopedia atau Shopee — ada ribuan fitur, jutaan pengguna, dan milyaran transaksi. Bagaimana cara mengatur semua itu?

OOP menjawab pertanyaan ini dengan satu prinsip sederhana: **“Modelkan dunia nyata ke dalam kode.”**

Di dunia nyata, kita berinteraksi dengan **objek**: mobil, rumah, manusia, buku, dan sebagainya. Setiap objek memiliki:

- **Karakteristik** (data/properti) — misalnya mobil memiliki warna, merek, tahun produksi
- **Perilaku** (fungsi/metode) — misalnya mobil bisa berjalan, berhenti, membelok

OOP membawa konsep ini ke dalam pemrograman.

---

## 1.2 Definisi Pemrograman Berorientasi Objek (OOP)

**Pemrograman Berorientasi Objek (Object-Oriented Programming / OOP)** adalah paradigma pemrograman yang mengorganisir kode di sekitar **objek** (yang berisi data dan perilaku) daripada di sekitar **fungsi** dan **logika**.

> “OOP adalah cara berpikir: **bukan ‘apa yang harus saya lakukan?** ’ tetapi **‘objek apa yang ada, dan apa yang bisa mereka lakukan?’** ”

---

## 1.3 Konsep Dasar OOP

### A. Kelas (Class)

**Kelas** adalah **blueprint** atau **cetakan** untuk membuat objek. Kelas mendefinisikan:

- **Atribut/Properti** — data yang dimiliki oleh objek
- **Metode/Fungsi** — perilaku yang dapat dilakukan oleh objek

**Analogi:** Kelas seperti **cetakan kue**.

- Cetakan menentukan bentuk kue, bahan-bahan yang dibutuhkan, dan cara membuatnya.
- Cetakan itu sendiri **bukan** kue — ia adalah **rencana** untuk membuat kue.

```kotlin
// Ini adalah KELAS — blueprint untuk objek Mahasiswa
class Mahasiswa {
    var nama: String = ""
    var nim: String = ""
    var ipk: Double = 0.0

    fun tampilkanData() {
        println("Nama: $nama, NIM: $nim, IPK: $ipk")
    }
}
```

### B. Objek (Object)

**Objek** adalah **instansi** (realisasi) dari sebuah kelas. Objek adalah **wujud nyata** dari cetakan yang sudah dibuat.

**Analogi:** Objek adalah **kue yang sudah jadi** dari cetakan.

- Setiap kue memiliki bentuk yang sama (sesuai cetakan)
- Tapi setiap kue bisa memiliki topping, warna, atau ukuran yang berbeda

```kotlin
// Ini adalah OBJEK — realisasi dari kelas Mahasiswa
val mahasiswa1 = Mahasiswa()
mahasiswa1.nama = "Budi Santoso"
mahasiswa1.nim = "TI2024001"
mahasiswa1.ipk = 3.75
mahasiswa1.tampilkanData()  // Output: Nama: Budi Santoso, NIM: TI2024001, IPK: 3.75
```

### C. Atribut (Attribute / Property)

**Atribut** adalah **variabel** yang melekat pada sebuah objek. Atribut menyimpan **keadaan** (state) dari objek.

**Analogi:** Atribut adalah **bahan-bahan kue**.

- Tepung, gula, telur adalah bahan yang mendefinisikan kue

Dalam kode:

```kotlin
class Mobil {
    var merek: String = ""      // atribut
    var warna: String = ""      // atribut
    var tahun: Int = 0          // atribut
    var kecepatan: Int = 0      // atribut
}
```

### D. Metode (Method / Function)

**Metode** adalah **fungsi** yang melekat pada sebuah objek. Metode mendefinisikan **perilaku** (behavior) dari objek.

**Analogi:** Metode adalah **cara membuat kue**.

- Mencampur, mengocok, memanggang adalah perilaku/aksi

Dalam kode:

```kotlin
class Mobil {
    var kecepatan: Int = 0

    // METODE — perilaku objek
    fun gas() {
        kecepatan += 10
        println("Kecepatan: $kecepatan km/jam")
    }

    fun rem() {
        kecepatan -= 5
        if (kecepatan < 0) kecepatan = 0
        println("Kecepatan: $kecepatan km/jam")
    }
}
```

---

## 1.4 Empat Pilar OOP (The Four Pillars of OOP)

OOP dibangun di atas **empat pilar utama**:

| **Pilar** | **Deskripsi** | **Ilustrasi** |
| --- | --- | --- |
| **Abstraksi (Abstraction)** | Menyembunyikan detail kompleks dan hanya menampilkan esensi | Seperti mengemudi mobil — Anda tidak perlu tahu cara kerja mesin, cukup tahu cara menggunakan setir dan pedal |
| **Enkapsulasi (Encapsulation)** | Membungkus data dan metode dalam satu unit, menyembunyikan detail internal | Seperti ATM — Anda bisa mengambil uang tanpa tahu cara kerja mesin di dalamnya |
| **Pewarisan (Inheritance)** | Membuat kelas baru dari kelas yang sudah ada, mewarisi properti dan metode | Seperti anak mewarisi sifat dari orang tua |
| **Polimorfisme (Polymorphism)** | Kemampuan objek yang berbeda untuk merespons pesan yang sama dengan cara berbeda | Seperti perintah “bunyikan suara” — anjing menggonggong, kucing mengeong, sapi melenguh |

> **Catatan:** Keempat pilar ini akan kita pelajari secara mendalam di pertemuan-pertemuan berikutnya. Pertemuan 1 fokus pada pemahaman **kelas** dan **objek** sebagai fondasi.

---

## 1.5 OOP vs Pemrograman Prosedural

| **Aspek** | **Prosedural** | **OOP** |
| --- | --- | --- |
| **Unit utama** | Fungsi/prosedur | Objek |
| **Data** | Data terpisah dari fungsi | Data dan fungsi terbungkus dalam objek |
| **Keamanan data** | Rendah (data global mudah diakses) | Tinggi (enkapsulasi melindungi data) |
| **Reusability** | Sulit (copy-paste kode) | Mudah (inheritance dan komposisi) |
| **Maintenance** | Sulit untuk program besar | Lebih mudah (modular) |
| **Contoh** | Program kalkulator sederhana | Aplikasi e-commerce, game, sistem perbankan |

**Contoh Perbandingan Kode:**

**Pendekatan Prosedural (bayangkan dalam bahasa C):**

```c
// Data terpisah dari fungsi
struct Mahasiswa {
    char nama[50];
    float ipk;
};

void tampilkanMahasiswa(struct Mahasiswa m) {
    printf("Nama: %s, IPK: %.2f", m.nama, m.ipk);
}

int main() {
    struct Mahasiswa m = {"Budi", 3.75};
    tampilkanMahasiswa(m);
    return 0;
}
```

**Pendekatan OOP (Kotlin):**

```kotlin
// Data DAN perilaku terbungkus dalam satu kelas
class Mahasiswa(val nama: String, val ipk: Double) {
    fun tampilkan() {
        println("Nama: $nama, IPK: $ipk")
    }
}

fun main() {
    val m = Mahasiswa("Budi", 3.75)
    m.tampilkan()  // Objek bertanggung jawab atas datanya sendiri
}
```

---

# BAGIAN 2: MENGAPA KOTLIN?

## 2.1 Sejarah Singkat Kotlin

**Kotlin** adalah bahasa pemrograman modern yang dikembangkan oleh **JetBrains** (perusahaan di balik IntelliJ IDEA).

| **Tahun** | **Peristiwa Penting** |
| --- | --- |
| **2011** | JetBrains memulai pengembangan Kotlin |
| **2016** | Kotlin 1.0 resmi dirilis |
| **2017** | Google mengumumkan Kotlin sebagai bahasa resmi untuk Android (first-class support) |
| **2019** | Google mendeklarasikan **“Kotlin-first”** untuk Android development |
| **Sekarang** | Kotlin adalah bahasa pilihan untuk Android, backend, dan multiplatform |

### Mengapa Nama “Kotlin”?

Kotlin dinamai berdasarkan **Pulau Kotlin** di Rusia (dekat St. Petersburg), mirip seperti Java yang dinamai berdasarkan pulau Jawa di Indonesia. JetBrains ingin mengikuti tradisi penamaan bahasa pemrograman berdasarkan pulau.

---

## 2.2 Keunggulan Kotlin

### 1. **Interoperabilitas 100% dengan Java**

Kotlin dapat memanggil kode Java, dan Java dapat memanggil kode Kotlin. Ini berarti:

- Anda bisa menggunakan semua library Java yang sudah ada
- Anda bisa migrasi bertahap dari Java ke Kotlin
- Tim bisa menggunakan kedua bahasa secara bersamaan

### 2. **Sintaks yang Lebih Ringkas**

Kotlin mengurangi **boilerplate code** (kode berulang yang tidak perlu) hingga 20-30% dibanding Java.

**Java:**

```java
public class Person {
    private String name;
    private int age;

    public Person(String name, int age) {
        this.name = name;
        this.age = age;
    }

    public String getName() { return name; }
    public void setName(String name) { this.name = name; }
    public int getAge() { return age; }
    public void setAge(int age) { this.age = age; }
}
```

**Kotlin (hanya 1 baris!):**

```kotlin
class Person(var name: String, var age: Int)
```

### 3. **Null Safety — Mengakhiri NullPointerException**

NullPointerException (NPE) adalah **musuh nomor 1** programmer Java. Tony Hoare, ilmuwan yang menemukan konsep `null`, menyebutnya sebagai **“kesalahan bernilai satu miliar dolar”**.

Kotlin menyelesaikan masalah ini di **tingkat tipe data**:

- Secara default, variabel **tidak boleh bernilai null**
- Jika ingin mengizinkan null, harus **secara eksplisit** menyatakannya dengan `?`

```kotlin
var name: String = "Budi"
name = null  // ❌ ERROR: Null can not be a value of a non-null type String

var nullableName: String? = "Budi"
nullableName = null  // ✅ OK, karena kita sudah menyatakan bisa null
```

### 4. **Fitur Modern Lainnya**

| **Fitur** | **Deskripsi** |
| --- | --- |
| **Type Inference** | Kompiler bisa menebak tipe data, tidak perlu selalu menulis tipe secara eksplisit |
| **Data Class** | Kelas khusus untuk menyimpan data — otomatis menghasilkan `toString()`, `equals()`, `hashCode()` |
| **Extension Functions** | Menambah fungsi baru ke kelas yang sudah ada tanpa mengubah kode asli |
| **Coroutines** | Pemrograman asinkron yang sederhana dan efisien |
| **Lambda & Functional Programming** | Mendukung gaya pemrograman fungsional |

---

## 2.3 Kotlin dan Mobile Programming

**Mengapa kami mengajarkan OOP dengan Kotlin?**

Karena **semester depan**, Anda akan belajar **Mobile Programming** menggunakan **Kotlin** untuk pengembangan aplikasi Android.

Dengan menguasai OOP di Kotlin sekarang, Anda akan:

1. **Langsung siap** untuk mata kuliah Mobile Programming — tidak perlu belajar bahasa baru dari nol
2. **Memahami fondasi OOP** yang sama persis dengan yang akan Anda gunakan di Android
3. **Menghemat waktu** karena sintaks Kotlin sudah familiar

> **Pesan penting:** OOP adalah **konsep universal**. Prinsip yang Anda pelajari di Kotlin berlaku juga di Java, C++, Python, C#, dan bahasa OOP lainnya. Fokus pada **konsep**, bukan hanya sintaks!

---

# BAGIAN 3: PERSIAPAN LINGKUNGAN PENGEMBANGAN

## 3.1 Apa yang Dibutuhkan?

Untuk memulai pemrograman Kotlin, Anda membutuhkan:

| **Komponen** | **Deskripsi** | **Link Download** |
| --- | --- | --- |
| **JDK (Java Development Kit)** | Kotlin berjalan di atas JVM (Java Virtual Machine) — JDK adalah fondasinya | [Adoptium](https://adoptium.net/) atau [Oracle JDK](https://www.oracle.com/java/technologies/downloads/) |
| **IntelliJ IDEA** | IDE (Integrated Development Environment) untuk menulis kode Kotlin | [JetBrains IntelliJ IDEA](https://www.jetbrains.com/idea/download/) (Community Edition — gratis) |

> **Catatan:** Kotlin sudah **ter-bundle** di IntelliJ IDEA dan Android Studio. Tidak perlu instal plugin tambahan!

---

## 3.2 Panduan Instalasi JDK

### Langkah 1: Download JDK

1. Buka browser dan kunjungi [https://adoptium.net/](https://adoptium.net/)
2. Pilih versi **JDK 17** atau **JDK 21** (LTS — Long Term Support)
3. Pilih sistem operasi Anda (Windows, macOS, atau Linux)
4. Download installer (.msi untuk Windows, .dmg untuk macOS, .tar.gz untuk Linux)

### Langkah 2: Install JDK

**Windows:**

1. Jalankan file .msi yang sudah didownload
2. Ikuti petunjuk installer (klik Next > Next > Finish)
3. Secara default terinstal di `C:\Program Files\Java\jdk-17.x.x`

**macOS:**

1. Buka file .dmg yang sudah didownload
2. Ikuti petunjuk installer

**Linux (Ubuntu/Debian):**

```bash
sudo apt update
sudo apt install openjdk-17-jdk
```

### Langkah 3: Verifikasi Instalasi

Buka **Command Prompt** (Windows) atau **Terminal** (macOS/Linux) dan ketik:

```bash
java -version
```

Jika berhasil, Anda akan melihat output seperti:

```
openjdk version "17.0.9" 2023-10-17
OpenJDK Runtime Environment (build 17.0.9+9)
OpenJDK 64-Bit Server VM (build 17.0.9+9, mixed mode)
```

---

## 3.3 Panduan Instalasi IntelliJ IDEA

### Langkah 1: Download IntelliJ IDEA

1. Buka [https://www.jetbrains.com/idea/download/](https://www.jetbrains.com/idea/download/)
2. Pilih **Community Edition** (gratis) — **bukan** Ultimate Edition
3. Download installer sesuai sistem operasi Anda

### Langkah 2: Install IntelliJ IDEA

**Windows:**

1. Jalankan file .exe yang sudah didownload
2. Ikuti petunjuk installer
3. Centang opsi **“Add launchers dir to the PATH”** (memudahkan menjalankan dari terminal)
4. Centang **“.kt”** sebagai file extension yang terasosiasi

**macOS:**

1. Buka file .dmg
2. Drag IntelliJ IDEA ke folder Applications

**Linux:**

1. Ekstrak file .tar.gz
2. Jalankan `bin/idea.sh`

### Langkah 3: Verifikasi Kotlin Plugin

1. Buka IntelliJ IDEA
2. Buka **File → Settings** (Windows/Linux) atau **IntelliJ IDEA → Preferences** (macOS)
3. Pilih **Plugins**
4. Cari “Kotlin” — pastikan statusnya **“Installed”** dan **“Enabled”**

> **Catatan:** Kotlin Plugin sudah ter-bundle dan aktif secara default di IntelliJ IDEA versi terbaru.

---

## 3.4 Membuat Project Kotlin Pertama

### Langkah 1: Buat Project Baru

1. Buka IntelliJ IDEA
2. Pada **Welcome Screen**, klik **“New Project”**
3. Atau dari menu: **File → New → Project**

### Langkah 2: Konfigurasi Project

| **Opsi** | **Pilihan** | **Keterangan** |
| --- | --- | --- |
| **Language** | Kotlin | Pilih Kotlin sebagai bahasa utama |
| **Build System** | IntelliJ | Build system bawaan, tidak perlu download tambahan |
| **JDK** | Pilih JDK yang sudah diinstal | Jika tidak muncul, klik “Add JDK” dan arahkan ke folder JDK |
| **Project Name** | `PBO-Project1` | Bebas, tapi usahakan deskriptif |
| **Location** | Tentukan folder penyimpanan | Misal: `D:\Kuliah\PBO\Project1` |
| **Add Sample Code** | ✅ Centang | Akan membuat file dengan contoh Hello World |

### Langkah 3: Klik **“Create”**

### Langkah 4: Kenali Struktur Project

```
PBO-Project1/
├── .idea/              # Folder konfigurasi IntelliJ IDEA
├── src/
│   └── Main.kt         # File kode utama (berisi contoh Hello World)
└── PBO-Project1.iml    # File konfigurasi project
```

### Langkah 5: Buka File Main.kt

File `Main.kt` akan berisi kode seperti ini:

```kotlin
fun main() {
    println("Hello, World!")
}
```

---

# BAGIAN 4: HELLO WORLD DAN SINTAKS DASAR KOTLIN

## 4.1 Program Hello World

### Kode Hello World di Kotlin

```kotlin
fun main() {
    println("Hello, World!")
}
```

### Menjalankan Program

1. Klik **ikon segitiga hijau** (▶) di samping fungsi `main`
2. Atau klik kanan pada file → **Run ‘MainKt’**
3. Atau tekan **Ctrl + Shift + F10** (Windows/Linux) atau **Control + Shift + R** (macOS)

### Output yang Diharapkan

```
Hello, World!
```

---

## 4.2 Anatomi Program Kotlin

Mari kita bedah kode Hello World baris per baris:

```kotlin
fun main() {
    println("Hello, World!")
}
```

| **Bagian** | **Penjelasan** |
| --- | --- |
| `fun` | **Keyword** untuk mendeklarasikan fungsi (function) |
| `main` | **Nama fungsi** — fungsi khusus yang dieksekusi pertama kali saat program dijalankan |
| `()` | **Parameter** — fungsi `main` bisa menerima parameter (kita akan bahas nanti) |
| `{ ... }` | **Body fungsi** — berisi kode yang akan dijalankan |
| `println(...)` | **Fungsi** untuk mencetak teks ke layar dan **pindah baris** (new line) |
| `"Hello, World!"` | **String** (teks) — data yang akan dicetak |

### Perbedaan `print()` dan `println()`

```kotlin
fun main() {
    print("Hello ")   // Tidak pindah baris
    print("World!")   // Output: Hello World!
    println()         // Pindah baris (baris kosong)
    println("Selamat datang di OOP!")  // Output: Selamat datang di OOP! (dengan new line)
}
```

**Output:**

```
Hello World!
Selamat datang di OOP!
```

---

## 4.3 Variabel: `val` dan `var`

Variabel adalah **tempat menyimpan data** di dalam program.

### `val` — Immutable (Read-Only / Tidak Bisa Diubah)

`val` digunakan untuk variabel yang **nilainya tidak berubah** setelah diinisialisasi.

```kotlin
val nama = "Budi Santoso"
println(nama)  // Output: Budi Santoso

nama = "Siti Rahayu"  // ❌ ERROR: Val cannot be reassigned
```

### `var` — Mutable (Bisa Diubah)

`var` digunakan untuk variabel yang **nilainya bisa berubah**.

```kotlin
var umur = 20
println(umur)  // Output: 20

umur = 21      // ✅ OK, bisa diubah
println(umur)  // Output: 21
```

### Aturan Sederhana

> **“Gunakan `val` secara default. Gunakan `var` hanya jika benar-benar perlu diubah.”** — Ini adalah praktik terbaik (best practice) dalam Kotlin.

---

## 4.4 Type Inference (Penebakan Tipe Data)

Kotlin secara otomatis **menebak** tipe data variabel berdasarkan nilai yang diberikan.

```kotlin
val nama = "Budi"      // Kotlin menebak: String
var umur = 20          // Kotlin menebak: Int
val ipk = 3.75         // Kotlin menebak: Double
var isLulus = true     // Kotlin menebak: Boolean
```

### Menulis Tipe Data Secara Eksplisit

Anda juga bisa menulis tipe data secara **eksplisit** (jelas):

```kotlin
val nama: String = "Budi"
var umur: Int = 20
val ipk: Double = 3.75
var isLulus: Boolean = true
```

### Tipe Data Dasar di Kotlin

| **Tipe Data** | **Deskripsi** | **Contoh** |
| --- | --- | --- |
| `String` | Teks/kata-kata | `"Halo"`, `"Budi"` |
| `Int` | Bilangan bulat | `10`, `-5`, `0` |
| `Double` | Bilangan desimal | `3.14`, `-2.5`, `0.0` |
| `Boolean` | Nilai benar/salah | `true`, `false` |
| `Char` | Satu karakter | `'A'`, `'5'`, `'$'` |

---

## 4.5 Null Safety — Keamanan dari Null

### Masalah Null di Java

Di Java, **semua** variabel bisa bernilai `null`:

```java
String nama = null;   // OK di Java
int panjang = nama.length();  // ❌ ERROR: NullPointerException (runtime crash!)
```

Program akan **crash** di saat runtime (saat program berjalan) — ini sangat berbahaya!

### Solusi Kotlin: Null Safety

Di Kotlin, secara default variabel **tidak boleh null**.

```kotlin
var nama: String = "Budi"
nama = null  // ❌ ERROR: Null can not be a value of a non-null type String
```

### Variabel Nullable (Boleh Null)

Jika Anda **benar-benar** membutuhkan variabel yang bisa bernilai `null`, Anda harus menyatakannya dengan **`?`**.

```kotlin
var nama: String? = "Budi"
nama = null  // ✅ OK, karena sudah dinyatakan nullable
```

### Cara Aman Mengakses Variabel Nullable

**1. Safe Call (`?.`)** — Memanggil metode hanya jika variabel tidak null.

```kotlin
val nama: String? = "Budi"
val panjang = nama?.length  // Jika nama null, panjang = null (tidak crash!)
println(panjang)  // Output: 4
```

**2. Elvis Operator (`?:`)** — Memberikan nilai default jika variabel null.

```kotlin
val nama: String? = null
val panjang = nama?.length ?: 0  // Jika nama null, panjang = 0
println(panjang)  // Output: 0
```

**3. Not-Null Assertion (`!!`)** — Memaksa Kotlin untuk menganggap variabel tidak null (HATI-HATI!).

```kotlin
val nama: String? = "Budi"
val panjang = nama!!.length  // Yakin 100% tidak null
println(panjang)  // Output: 4
```

> **⚠️ PERINGATAN:** Gunakan `!!` hanya jika Anda **100% yakin** variabel tidak null. Jika ternyata null, program akan crash!

---

## 4.6 Fungsi (Function) di Kotlin

### Mendeklarasikan Fungsi

Gunakan keyword **`fun`** untuk mendeklarasikan fungsi.

```kotlin
fun sapa(nama: String) {
    println("Halo, $nama!")
}

fun main() {
    sapa("Budi")  // Output: Halo, Budi!
}
```

### Fungsi dengan Nilai Balik (Return Value)

```kotlin
fun tambah(a: Int, b: Int): Int {
    return a + b
}

fun main() {
    val hasil = tambah(5, 3)
    println(hasil)  // Output: 8
}
```

### Single-Expression Function (Fungsi Satu Baris)

Jika fungsi hanya terdiri dari satu ekspresi, bisa ditulis lebih ringkas:

```kotlin
// Cara panjang
fun tambah(a: Int, b: Int): Int {
    return a + b
}

// Cara ringkas (single-expression)
fun tambah(a: Int, b: Int) = a + b
```

### Fungsi dengan Parameter Default

Kotlin mendukung **nilai default** untuk parameter:

```kotlin
fun sapa(nama: String, sapaan: String = "Halo") {
    println("$sapaan, $nama!")
}

fun main() {
    sapa("Budi")           // Output: Halo, Budi!
    sapa("Siti", "Assalamu'alaikum")  // Output: Assalamu'alaikum, Siti!
}
```

---

## 4.7 String Template (Interpolasi String)

Di Kotlin, Anda bisa menyisipkan nilai variabel ke dalam string menggunakan **`$`**.

```kotlin
val nama = "Budi"
val umur = 20

// Tanpa string template
println("Nama saya " + nama + ", umur saya " + umur + " tahun.")

// Dengan string template (lebih bersih!)
println("Nama saya $nama, umur saya $umur tahun.")
```

### Ekspresi dalam String Template

Untuk ekspresi yang lebih kompleks, gunakan **`${...}`**:

```kotlin
val a = 5
val b = 3
println("Hasil $a + $b = ${a + b}")  // Output: Hasil 5 + 3 = 8
```

---

## 4.8 Input dari Pengguna (User Input)

Untuk membaca input dari pengguna, gunakan fungsi **`readln()`**.

```kotlin
fun main() {
    println("Siapa nama Anda?")
    val nama = readln()  // Membaca input dari pengguna
    println("Halo, $nama! Selamat belajar OOP!")
}
```

### Membaca Input dengan Tipe Data Tertentu

```kotlin
fun main() {
    println("Masukkan angka pertama:")
    val a = readln().toInt()  // Mengubah String menjadi Int

    println("Masukkan angka kedua:")
    val b = readln().toInt()

    println("Hasil penjumlahan: ${a + b}")
}
```

> **⚠️ PERINGATAN:** Fungsi `toInt()` akan error (crash) jika pengguna memasukkan teks yang bukan angka. Di pertemuan mendatang kita akan belajar cara menangani error ini (exception handling).

---

# BAGIAN 5: KELAS DAN OBJEK DI KOTLIN

## 5.1 Mendeklarasikan Kelas

Di Kotlin, kelas dideklarasikan dengan keyword **`class`**.

```kotlin
// Kelas kosong (minimal)
class Mahasiswa

// Kelas dengan properti
class Mahasiswa {
    var nim: String = ""
    var nama: String = ""
    var jurusan: String = ""
    var ipk: Double = 0.0
}
```

---

## 5.2 Properti di Kelas

Properti adalah **variabel** yang menjadi bagian dari kelas.

```kotlin
class Mobil {
    var merek: String = ""
    var model: String = ""
    var tahun: Int = 0
    var warna: String = ""
    var kecepatan: Int = 0
}
```

### Properti dengan Nilai Default

```kotlin
class Mobil {
    var merek: String = "Toyota"
    var model: String = "Avanza"
    var tahun: Int = 2024
    var warna: String = "Putih"
    var kecepatan: Int = 0
}
```

---

## 5.3 Metode di Kelas

Metode adalah **fungsi** yang menjadi bagian dari kelas.

```kotlin
class Mobil {
    var merek: String = "Toyota"
    var model: String = "Avanza"
    var kecepatan: Int = 0

    // METODE — perilaku objek
    fun gas() {
        kecepatan += 10
        println("Mobil melaju dengan kecepatan $kecepatan km/jam")
    }

    fun rem() {
        kecepatan -= 5
        if (kecepatan < 0) kecepatan = 0
        println("Mobil melambat, kecepatan $kecepatan km/jam")
    }

    fun tampilkanInfo() {
        println("Merek: $merek")
        println("Model: $model")
        println("Kecepatan: $kecepatan km/jam")
    }
}
```

---

## 5.4 Membuat Objek (Instansiasi)

Di Kotlin, objek dibuat **tanpa keyword `new`** (berbeda dengan Java).

```kotlin
fun main() {
    // Membuat objek dari kelas Mobil
    val mobilSaya = Mobil()

    // Mengakses properti
    mobilSaya.merek = "Honda"
    mobilSaya.model = "Civic"
    mobilSaya.kecepatan = 0

    // Memanggil metode
    mobilSaya.tampilkanInfo()
    mobilSaya.gas()
    mobilSaya.gas()
    mobilSaya.rem()
    mobilSaya.tampilkanInfo()
}
```

**Output:**

```
Merek: Honda
Model: Civic
Kecepatan: 0 km/jam
Mobil melaju dengan kecepatan 10 km/jam
Mobil melaju dengan kecepatan 20 km/jam
Mobil melambat, kecepatan 15 km/jam
Merek: Honda
Model: Civic
Kecepatan: 15 km/jam
```

---

## 5.5 Konstruktor (Constructor)

Konstruktor adalah fungsi khusus yang **dipanggil saat objek dibuat** untuk menginisialisasi properti.

### Primary Constructor

Di Kotlin, primary constructor ditulis **langsung di header kelas**.

```kotlin
class Mahasiswa(val nim: String, val nama: String, var ipk: Double) {
    fun tampilkan() {
        println("NIM: $nim, Nama: $nama, IPK: $ipk")
    }
}

fun main() {
    // Membuat objek dengan constructor
    val mhs = Mahasiswa("TI2024001", "Budi Santoso", 3.75)
    mhs.tampilkan()  // Output: NIM: TI2024001, Nama: Budi Santoso, IPK: 3.75
}
```

### Properti `val` vs `var` di Constructor

| **Keyword** | **Keterangan** |
| --- | --- |
| `val` di constructor | Properti **read-only** — tidak bisa diubah setelah objek dibuat |
| `var` di constructor | Properti **mutable** — bisa diubah setelah objek dibuat |

```kotlin
class Mahasiswa(val nim: String, val nama: String, var ipk: Double)

fun main() {
    val mhs = Mahasiswa("TI2024001", "Budi", 3.75)

    // ✅ Bisa mengubah ipk (var)
    mhs.ipk = 3.80

    // ❌ Tidak bisa mengubah nim (val)
    // mhs.nim = "TI2024002"  // ERROR!
}
```

### Init Block (Blok Inisialisasi)

`init` block dieksekusi **saat objek dibuat**, sebelum properti lainnya diakses.

```kotlin
class Mahasiswa(val nim: String, val nama: String, var ipk: Double) {
    init {
        println("Objek Mahasiswa dibuat!")
        println("NIM: $nim, Nama: $nama")
        if (ipk < 0.0 || ipk > 4.0) {
            println("⚠️ PERINGATAN: IPK tidak valid!")
        }
    }

    fun tampilkan() {
        println("NIM: $nim, Nama: $nama, IPK: $ipk")
    }
}
```

---

## 5.6 Contoh Lengkap: Sistem Manajemen Mahasiswa

Mari kita buat program lengkap yang menggabungkan semua konsep yang sudah dipelajari.

### File: Mahasiswa.kt

```kotlin
/**
 * Kelas Mahasiswa merepresentasikan data mahasiswa
 *
 * @property nim Nomor Induk Mahasiswa (tidak bisa diubah setelah dibuat)
 * @property nama Nama lengkap mahasiswa (tidak bisa diubah setelah dibuat)
 * @property jurusan Jurusan mahasiswa (bisa diubah)
 * @property ipk Indeks Prestasi Kumulatif (bisa diubah)
 */
class Mahasiswa(
    val nim: String,
    val nama: String,
    var jurusan: String,
    var ipk: Double
) {
    // Blok inisialisasi - dijalankan saat objek dibuat
    init {
        println("✅ Mahasiswa $nama dengan NIM $nim berhasil didaftarkan!")

        // Validasi IPK
        if (ipk < 0.0 || ipk > 4.0) {
            println("⚠️ PERINGATAN: IPK $ipk tidak valid! IPK harus antara 0.0 - 4.0")
        }
    }

    /**
     * Menampilkan seluruh data mahasiswa
     */
    fun tampilkan() {
        println("=" .repeat(50))
        println("📋 DATA MAHASISWA")
        println("=" .repeat(50))
        println("NIM     : $nim")
        println("Nama    : $nama")
        println("Jurusan : $jurusan")
        println("IPK     : $ipk")
        println("Predikat: ${hitungPredikat()}")
        println("=" .repeat(50))
    }

    /**
     * Menghitung predikat kelulusan berdasarkan IPK
     *
     * @return String predikat kelulusan
     */
    fun hitungPredikat(): String {
        return when {
            ipk >= 3.5 -> "🏆 Cumlaude (Dengan Pujian)"
            ipk >= 3.0 -> "⭐ Sangat Memuaskan"
            ipk >= 2.5 -> "✅ Memuaskan"
            ipk >= 2.0 -> "📖 Cukup"
            else -> "📚 Perlu Perbaikan"
        }
    }

    /**
     * Memperbarui IPK mahasiswa
     *
     * @param ipkBaru Nilai IPK baru (harus antara 0.0 - 4.0)
     * @return true jika berhasil, false jika gagal
     */
    fun updateIpk(ipkBaru: Double): Boolean {
        return if (ipkBaru in 0.0..4.0) {
            ipk = ipkBaru
            println("✅ IPK $nama berhasil diperbarui menjadi $ipkBaru")
            true
        } else {
            println("❌ Gagal: IPK $ipkBaru tidak valid (harus 0.0 - 4.0)")
            false
        }
    }

    /**
     * Mengecek apakah mahasiswa lulus (IPK >= 2.0)
     */
    fun isLulus(): Boolean {
        return ipk >= 2.0
    }
}

/**
 * Fungsi utama program
 */
fun main() {
    println("=" .repeat(50))
    println("🎓 SISTEM MANAJEMEN MAHASISWA")
    println("=" .repeat(50))
    println()

    // Membuat beberapa objek mahasiswa
    val mhs1 = Mahasiswa("TI2024001", "Budi Santoso", "Teknik Informatika", 3.75)
    val mhs2 = Mahasiswa("TI2024002", "Siti Rahayu", "Sistem Informasi", 3.20)
    val mhs3 = Mahasiswa("TI2024003", "Ahmad Fauzi", "Teknik Komputer", 1.80)

    println()

    // Menampilkan data semua mahasiswa
    mhs1.tampilkan()
    println()
    mhs2.tampilkan()
    println()
    mhs3.tampilkan()
    println()

    // Demonstrasi update data
    println("=" .repeat(50))
    println("🔄 DEMONSTRASI UPDATE DATA")
    println("=" .repeat(50))

    // Update IPK mhs3 (yang sebelumnya 1.80)
    println("Status kelulusan ${mhs3.nama}: ${if (mhs3.isLulus()) "✅ LULUS" else "❌ TIDAK LULUS"}")
    mhs3.updateIpk(2.50)
    println("Status kelulusan ${mhs3.nama} (baru): ${if (mhs3.isLulus()) "✅ LULUS" else "❌ TIDAK LULUS"}")
    mhs3.tampilkan()

    println()
    println("=" .repeat(50))
    println("🏁 PROGRAM SELESAI")
    println("=" .repeat(50))
}
```

### Output yang Diharapkan

```
==================================================
🎓 SISTEM MANAJEMEN MAHASISWA
==================================================

✅ Mahasiswa Budi Santoso dengan NIM TI2024001 berhasil didaftarkan!
✅ Mahasiswa Siti Rahayu dengan NIM TI2024002 berhasil didaftarkan!
✅ Mahasiswa Ahmad Fauzi dengan NIM TI2024003 berhasil didaftarkan!

==================================================
📋 DATA MAHASISWA
==================================================
NIM     : TI2024001
Nama    : Budi Santoso
Jurusan : Teknik Informatika
IPK     : 3.75
Predikat: 🏆 Cumlaude (Dengan Pujian)
==================================================

==================================================
📋 DATA MAHASISWA
==================================================
NIM     : TI2024002
Nama    : Siti Rahayu
Jurusan : Sistem Informasi
IPK     : 3.2
Predikat: ⭐ Sangat Memuaskan
==================================================

==================================================
📋 DATA MAHASISWA
==================================================
NIM     : TI2024003
Nama    : Ahmad Fauzi
Jurusan : Teknik Komputer
IPK     : 1.8
Predikat: 📚 Perlu Perbaikan
==================================================

==================================================
🔄 DEMONSTRASI UPDATE DATA
==================================================
Status kelulusan Ahmad Fauzi: ❌ TIDAK LULUS
✅ IPK Ahmad Fauzi berhasil diperbarui menjadi 2.5
Status kelulusan Ahmad Fauzi (baru): ✅ LULUS
==================================================
📋 DATA MAHASISWA
==================================================
NIM     : TI2024003
Nama    : Ahmad Fauzi
Jurusan : Teknik Komputer
IPK     : 2.5
Predikat: ✅ Memuaskan
==================================================

==================================================
🏁 PROGRAM SELESAI
==================================================
```

---

# BAGIAN 6: LATIHAN DAN TUGAS

## 6.1 Latihan Mandiri

### Latihan 1: Kelas Buku

Buatlah kelas **`Buku`** dengan:

- **Properti:**
  - `judul` (String, read-only)
  - `penulis` (String, read-only)
  - `tahunTerbit` (Int, read-only)
  - `isDipinjam` (Boolean, bisa diubah)
  - `peminjam` (String?, bisa diubah, nullable)
- **Metode:**
  - `pinjam(namaPeminjam: String)` → mengubah `isDipinjam` menjadi `true` dan mengisi `peminjam`
  - `kembalikan()` → mengubah `isDipinjam` menjadi `false` dan mengosongkan `peminjam`
  - `tampilkanInfo()` → menampilkan semua informasi buku
- **Constructor:** Primary constructor dengan semua properti (kecuali `isDipinjam` dan `peminjam` yang punya nilai default)

---

### Latihan 2: Kelas Lingkaran

Buatlah kelas **`Lingkaran`** dengan:

- **Properti:**
  - `jariJari` (Double, bisa diubah)
- **Metode:**
  - `luas()` → mengembalikan luas lingkaran (π × r²)
  - `keliling()` → mengembalikan keliling lingkaran (2 × π × r)
  - `tampilkan()` → menampilkan jari-jari, luas, dan keliling
- **Catatan:** Gunakan `Math.PI` untuk nilai π

---

### Latihan 3: Kelas Kalkulator

Buatlah kelas **`Kalkulator`** dengan:

- **Properti:** Tidak ada (kelas tanpa properti)
- **Metode:**
  - `tambah(a: Double, b: Double): Double`
  - `kurang(a: Double, b: Double): Double`
  - `kali(a: Double, b: Double): Double`
  - `bagi(a: Double, b: Double): Double` (handle pembagian dengan 0 — jika b = 0, return 0.0 dan cetak peringatan)
  - `tampilkanOperasi(a: Double, b: Double, operator: Char)` → menampilkan hasil operasi

---

## 6.2 Tugas 1 (Dikumpulkan)

### Sistem Manajemen Data Mahasiswa Sederhana

Buatlah program lengkap dengan ketentuan berikut:

**1. Kelas `Mahasiswa` dengan:**

- Properti (semua menggunakan primary constructor):
  - `nim: String` (read-only)
  - `nama: String` (read-only)
  - `jurusan: String` (bisa diubah)
  - `ipk: Double` (bisa diubah)
  - `angkatan: Int` (read-only) — diisi otomatis dari 2 digit terakhir NIM

- Metode:
  - `tampilkan()` → menampilkan semua data mahasiswa dengan format rapi
  - `predikat()` → mengembalikan predikat berdasarkan IPK (sama seperti contoh)
  - `isLulus()` → mengembalikan `true` jika IPK ≥ 2.0
  - `updateIpk(ipkBaru: Double)` → mengupdate IPK dengan validasi (0.0 - 4.0)

**2. Fungsi `main()`:**

- Buat **minimal 5 objek** mahasiswa dengan data berbeda
- Tampilkan data semua mahasiswa
- Tampilkan daftar mahasiswa yang **lulus** (IPK ≥ 2.0)
- Tampilkan daftar mahasiswa dengan predikat **Cumlaude** (IPK ≥ 3.5)
- Demonstrasikan update IPK untuk salah satu mahasiswa

**3. Kriteria Penilaian:**

| **Kriteria** | **Bobot** |
| --- | --- |
| Kelas Mahasiswa didefinisikan dengan benar | 25% |
| Semua metode berfungsi dengan benar | 25% |
| Fungsi main() lengkap sesuai ketentuan | 20% |
| Kode bersih, terstruktur, dan diberi komentar | 15% |
| Program berjalan tanpa error | 15% |

---

# BAGIAN 7: RINGKASAN MATERI PERTEMUAN 1

## 7.1 Poin-Poin Penting

| **Konsep** | **Penjelasan Singkat** | **Keyword/Sintaks** |
| --- | --- | --- |
| **OOP** | Paradigma pemrograman berbasis objek | - |
| **Kelas** | Blueprint/cetakan untuk membuat objek | `class` |
| **Objek** | Instansi/realisasi dari kelas | `val obj = NamaKelas()` |
| **Atribut** | Data/properti yang dimiliki objek | `var nama: String` |
| **Metode** | Perilaku/fungsi yang dimiliki objek | `fun namaMetode()` |
| **Enkapsulasi** | Menyembunyikan detail internal | (akan dipelajari nanti) |
| **Inheritance** | Mewarisi properti dari kelas lain | (akan dipelajari nanti) |
| **Polimorfisme** | Banyak bentuk untuk satu interface | (akan dipelajari nanti) |
| **Abstraksi** | Menyembunyikan kompleksitas | (akan dipelajari nanti) |
| **`val`** | Variabel tidak bisa diubah | `val nama = "Budi"` |
| **`var`** | Variabel bisa diubah | `var umur = 20` |
| **Null Safety** | Mencegah NullPointerException | `String?` untuk nullable |
| **`fun`** | Mendeklarasikan fungsi | `fun main()` |
| **`println()`** | Mencetak ke layar (dengan new line) | `println("Hello")` |

---

## 7.2 Persiapan untuk Pertemuan 2

**Materi berikutnya: ENKAPSULASI (Encapsulation)**

Apa yang akan dipelajari:

1. Access modifier (`private`, `protected`, `internal`, `public`)
2. Getter dan Setter
3. Properti dengan custom getter/setter
4. Backing field (`field`)
5. Praktik enkapsulasi dalam sistem nyata

**Tugas persiapan:**

- Baca modul tentang Enkapsulasi
- Review kembali materi kelas dan objek
- Pastikan semua latihan pertemuan 1 sudah selesai

---

# BAGIAN 8: REFERENSI DAN SUMBER BELAJAR

## 8.1 Referensi Utama

1. **Kotlin Official Documentation** — [https://kotlinlang.org/docs/](https://kotlinlang.org/docs/)
2. **Kotlin Tour** — Belajar Kotlin langsung di browser [https://kotlinlang.org/docs/kotlin-tour-welcome.html](https://kotlinlang.org/docs/kotlin-tour-welcome.html)
3. **IntelliJ IDEA Documentation** — [https://www.jetbrains.com/help/idea/get-started-with-kotlin.html](https://www.jetbrains.com/help/idea/get-started-with-kotlin.html)
4. **Kotlin Playground** — Coba Kotlin tanpa instalasi [https://play.kotlinlang.org/](https://play.kotlinlang.org/)

## 8.2 Referensi Pendukung

1. **Android Developers — Kotlin Learn** — [https://developer.android.com/kotlin/learn](https://developer.android.com/kotlin/learn)
2. **Kotlin 中文文档** — [https://book.kotlincn.net/](https://book.kotlincn.net/)

## 8.3 Istilah Penting

| **Istilah** | **Terjemahan** | **Deskripsi** |
| --- | --- | --- |
| Object-Oriented Programming | Pemrograman Berorientasi Objek | Paradigma pemrograman berbasis objek |
| Class | Kelas | Blueprint untuk membuat objek |
| Object | Objek | Instansi dari kelas |
| Attribute / Property | Atribut / Properti | Data yang dimiliki objek |
| Method / Function | Metode / Fungsi | Perilaku yang dimiliki objek |
| Encapsulation | Enkapsulasi | Menyembunyikan detail internal |
| Inheritance | Pewarisan | Mewarisi properti dari kelas lain |
| Polymorphism | Polimorfisme | Banyak bentuk untuk satu interface |
| Abstraction | Abstraksi | Menyembunyikan kompleksitas |
| Constructor | Konstruktor | Fungsi khusus saat objek dibuat |
| Instance | Instansi | Objek yang dibuat dari kelas |
| Null Safety | Keamanan Null | Mencegah NullPointerException |

---

# BAGIAN 9: PENUTUP

## 9.1 Motivasi untuk Mahasiswa

> **“Belajar OOP itu seperti belajar naik sepeda. Awalnya mungkin terasa sulit dan tidak seimbang. Tapi begitu Anda menguasainya, Anda akan bisa pergi ke mana saja.”**

Pertemuan 1 ini adalah **fondasi** dari seluruh mata kuliah OOP. Jika Anda memahami konsep **kelas** dan **objek** dengan baik, materi-materi berikutnya akan terasa lebih mudah.

**Ingatlah:**

1. OOP adalah **cara berpikir**, bukan sekadar sintaks
2. Latihan adalah **kunci** — semakin banyak Anda menulis kode, semakin paham Anda
3. Jangan takut **error** — error adalah guru terbaik
4. **Bertanyalah** jika ada yang tidak dimengerti

## 9.2 Doa Penutup

Semoga pertemuan pertama ini memberikan pemahaman yang kuat tentang dasar-dasar Pemrograman Berorientasi Objek. Teruslah belajar, teruslah berlatih, dan jadilah programmer yang handal!

**Sampai jumpa di pertemuan 2!** 🚀

---

**Disusun oleh,**
[Nama Dosen Pengampu]
Dosen Program Studi D4 Teknologi Rekayasa Informatika Industri
