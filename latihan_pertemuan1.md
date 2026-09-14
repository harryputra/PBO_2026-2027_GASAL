# 🎓 LATIHAN TERBIMBING OOP KOTLIN

## Studi Kasus: Sistem Manajemen Pet Shop "MeowWoof"

> **Tujuan utama:** Setelah menyelesaikan latihan ini, Anda **dijamin** bisa mengerjakan Tugas Mandiri Perpustakaan Digital tanpa bingung, karena strukturnya **95% identik** — hanya beda nama kelas dan domain.

---

## 🧭 FILOSOFI BELAJAR

Kita akan naik **7 level** secara bertahap:

| Level | Konsep | Output |
| ------- | -------- | -------- |
| 0 | Setup Proyek | Project siap |
| 1 | Class & Object Dasar | Paham cara buat kelas |
| 2 | Encapsulation | Paham `private` & `private set` |
| 3 | Inheritance | Paham `open`, `override`, `super` |
| 4 | Abstraction | Paham `abstract class` & method |
| 5 | Polymorphism | Paham smart casting `is`, `as?` |
| 6 | Sealed Class | Paham state machine |
| 7 | Mini Project (Gabungan) | Sistem Pet Shop lengkap |
| 8 | Mapping ke Perpustakaan | Siap garap tugas akhir |

**Aturan main:**

- ❌ Jangan skip level. Setiap level adalah fondasi level berikutnya.
- ✅ Ketik ulang semua kode dengan tangan Anda (bukan copy-paste).
- ✅ Setiap selesai 1 level, langsung RUN dan pastikan output sesuai.
- ✅ Kalau error, baca dulu pesan errornya — 90% jawabannya ada di situ.

---

# 📦 BAB 0 — SETUP PROYEK (15 menit)

## Step 0.1: Install IntelliJ IDEA

1. Download **IntelliJ IDEA Community** (gratis): <https://www.jetbrains.com/idea/download/>
2. Install → buka → tunggu indexing selesai.
3. JDK 17+ biasanya sudah bundled. Kalau belum, install **OpenJDK 17** manual.

## Step 0.2: Buat Project

1. **File → New → Project**
2. Pilih **Kotlin** (bukan Java)
3. Build system: **IntelliJ** (bukan Gradle/Maven — lebih simpel)
4. JDK: **17** atau lebih baru
5. Project name: `Latihan_OOP_PetShop`
6. Klik **Create**

## Step 0.3: Buat Struktur Folder

Di dalam `src/`, klik kanan → **New → Package** → ketik `petshop`.

Semua file `.kt` akan dibuat di dalam package `petshop`.

## Step 0.4: Test "Hello World"

Buat file `Main.kt`:

```kotlin
fun main() {
    println("Hello, OOP!")
}
```

Klik ikon ▶️ di sebelah kiri `fun main()`. Kalau muncul output → **setup berhasil!**

---

# 🟢 LEVEL 1 — CLASS & OBJECT DASAR

## 🎯 Tujuan Pembelajaran

Setelah level ini, Anda bisa:

- Membuat class dengan **primary constructor**
- Membuat properti `val` vs `var`
- Membuat method
- Instansiasi object & memanggil method

## 📖 Teori Singkat (2 menit baca)

**Class** = blueprint / cetakan.
**Object** = hasil nyata dari cetakan itu.

Contoh analogi: `class Mobil` adalah desainnya. `val avanza = Mobil(...)` adalah mobil nyata yang bisa dikendarai.

**Kotlin primary constructor** — beda dengan Java:

```kotlin
// Kotlin
class Mahasiswa(val nama: String, var ipk: Double)
```

Ini sekaligus mendefinisikan properti `nama` dan `ipk` — tidak perlu bikin getter/setter manual.

- `val` = read-only (immutable)
- `var` = read-write (mutable)

## 🧩 Studi Kasus: Hewan Sederhana

Kita buat kelas `Hewan` dengan 3 properti dan 1 method.

## 💻 Kode Lengkap

**File: `Hewan.kt`**

```kotlin
package petshop

/**
 * Kelas dasar yang merepresentasikan seekor hewan di Pet Shop.
 *
 * @property nama Nama hewan (misal: "Milo").
 * @property umur Umur hewan dalam tahun.
 * @property jenis Jenis hewan (misal: "Kucing").
 */
class Hewan(
    val nama: String,
    val umur: Int,
    val jenis: String
) {
    /**
     * Menampilkan perkenalan singkat tentang hewan ini.
     */
    fun perkenalan() {
        println("Halo! Namaku $nama, umur $umur tahun, jenis $jenis.")
    }
}
```

**File: `Main.kt`**

```kotlin
package petshop

fun main() {
    // Instansiasi 3 object
    val kucing = Hewan("Milo", 2, "Kucing")
    val anjing = Hewan("Rex", 4, "Anjing")
    val burung = Hewan("Chirpy", 1, "Burung")

    // Panggil method
    kucing.perkenalan()
    anjing.perkenalan()
    burung.perkenalan()
}
```

## 🧪 Output yang Diharapkan

```
Halo! Namaku Milo, umur 2 tahun, jenis Kucing.
Halo! Namaku Rex, umur 4 tahun, jenis Anjing.
Halo! Namaku Chirpy, umur 1 tahun, jenis Burung.
```

## ✍️ Latihan Mandiri

1. **Mudah:** Tambahkan properti `warna: String` ke constructor. Sesuaikan `perkenalan()` supaya menampilkan warna.
2. **Sedang:** Tambahkan method `makan(makanan: String)` yang mencetak: `"Milo makan Whiskas dengan lahap!"`
3. **Tantang:** Tambahkan properti `beratKg: Double` dengan default `0.5`. Buat object tanpa mengisi berat, lalu buat object yang mengisi berat.

## ✅ Checklist Level 1

- [ ] Bisa buat class dengan primary constructor
- [ ] Paham beda `val` dan `var`
- [ ] Bisa instansiasi object
- [ ] Bisa panggil method
- [ ] Bisa kompilasi & run tanpa error

> **🚨 Kalau stuck di sini, JANGAN LANJUT.** Level 1 adalah fondasi segalanya.

---

# 🔒 LEVEL 2 — ENCAPSULATION (ENKAPSULASI)

## 🎯 Tujuan Pembelajaran

- Paham `private val` (read-only dari luar, tidak bisa diakses sama sekali)
- Paham `private set` (bisa dibaca, tidak bisa diubah dari luar)
- Bisa membuat getter publik
- Paham kenapa enkapsulasi itu penting

## 📖 Teori Singkat

**Enkapsulasi** = melindungi data dari akses/ubah sembarangan.

Bayangkan Anda punya **rekening bank**. Anda tidak mau orang bisa langsung `rekening.saldo = 1_000_000_000`. Anda mau lewat method `setor()` dan `tarik()` yang punya validasi. Itulah enkapsulasi.

**3 modifier utama di Kotlin:**

| Modifier | Efek |
| ---------- | ------ |
| `public` (default) | Bisa diakses dari mana saja |
| `private` | Hanya bisa diakses di dalam kelas itu |
| `protected` | Hanya bisa diakses di kelas itu & subclass-nya |

**Kombinasi spesial Kotlin:**

```kotlin
var saldo: Double = 0.0
    private set   // Bisa DIBACA dari luar, tapi hanya bisa DIUBAH dari dalam kelas
```

## 🧩 Studi Kasus: Data Rahasia Hewan

Pet Shop punya data sensitif:

- `noVaksin` → hanya untuk internal, tidak boleh dibaca sembarangan (pakai `private val` + getter)
- `sudahDiVaksin` → bisa dilihat siapa saja, tapi hanya bisa diubah lewat method `vaksinasi()` (pakai `private set`)

## 💻 Kode Lengkap

**File: `Hewan.kt`** (timpa versi sebelumnya)

```kotlin
package petshop

/**
 * Kelas dasar hewan dengan penerapan enkapsulasi.
 *
 * @property nama Nama hewan.
 * @property umur Umur hewan dalam tahun.
 * @property jenis Jenis hewan.
 * @property noVaksin Nomor vaksin (rahasia — hanya bisa diakses via [getNoVaksin]).
 */
class Hewan(
    val nama: String,
    val umur: Int,
    val jenis: String,
    private val noVaksin: String
) {
    /**
     * Status vaksinasi hewan.
     * Hanya bisa diubah dari dalam kelas melalui [vaksinasi].
     */
    var sudahDiVaksin: Boolean = false
        private set

    /**
     * Melakukan vaksinasi. Jika sudah divaksin, tidak melakukan apa-apa.
     */
    fun vaksinasi() {
        if (sudahDiVaksin) {
            println("⚠️  $nama sudah pernah divaksin.")
        } else {
            sudahDiVaksin = true
            println("✅ $nama berhasil divaksin!")
        }
    }

    /**
     * Mengembalikan nomor vaksin (data rahasia).
     * @return Nomor vaksin.
     */
    fun getNoVaksin(): String = noVaksin

    /**
     * Menampilkan perkenalan singkat.
     */
    fun perkenalan() {
        val status = if (sudahDiVaksin) "sudah" else "belum"
        println("Halo! $nama ($jenis), $umur th, $status divaksin.")
    }
}
```

**File: `Main.kt`**

```kotlin
package petshop

fun main() {
    val milo = Hewan("Milo", 2, "Kucing", "VX-001")

    milo.perkenalan()               // "belum divaksin"
    milo.vaksinasi()                // sukses
    milo.perkenalan()               // "sudah divaksin"

    println("No vaksin Milo: ${milo.getNoVaksin()}")
    println("Status baca langsung: ${milo.sudahDiVaksin}")   // ✅ BOLEH (baca)

    // Coba baris di bawah ini satu per satu → akan ERROR:
    // milo.sudahDiVaksin = true         // ❌ Cannot access 'set': private
    // println(milo.noVaksin)            // ❌ Cannot access 'noVaksin': private
}
```

## 🧪 Output yang Diharapkan

```
Halo! Milo (Kucing), 2 th, belum divaksin.
✅ Milo berhasil divaksin!
Halo! Milo (Kucing), 2 th, sudah divaksin.
No vaksin Milo: VX-001
Status baca langsung: true
```

## 🔍 Eksperimen Wajib (Buktikan Enkapsulasi Bekerja!)

1. Hapus tanda `//` di `milo.sudahDiVaksin = true` → **compile akan error.**
2. Hapus tanda `//` di `println(milo.noVaksin)` → **compile akan error.**
3. **Catat pesan error-nya.** Itu bukti enkapsulasi bekerja.
4. Coba tambahkan tanda `//` kembali → compile sukses.

## ✍️ Latihan Mandiri

1. **Mudah:** Tambah `private val beratBadan: Double` dengan getter `getBeratBadan()`.
2. **Sedang:** Buat method `timbang(beratBaru: Double)` yang hanya meng-update kalau `beratBaru > 0`. Kalau ≤ 0, cetak error.
3. **Tantang:** Buat properti `var makananHarian: Int` dengan `private set`. Buat method `beriMakan()` yang menaikkan `makananHarian` sebanyak 1, tapi hanya boleh maksimal 3 kali sehari.
4. **Refleksi:** Diskusikan, kenapa `sudahDiVaksin` pakai `private set` tapi `nama` pakai `val` biasa?

## ✅ Checklist Level 2

- [ ] Paham `private val` → tidak bisa dibaca dari luar
- [ ] Paham `private set` → bisa dibaca, tidak bisa diubah dari luar
- [ ] Bisa buat getter publik
- [ ] Berhasil melihat error compile saat melanggar enkapsulasi
- [ ] Paham alasan di balik enkapsulasi

---

# 🧬 LEVEL 3 — INHERITANCE (PEWARISAN)

## 🎯 Tujuan Pembelajaran

- Paham `open class` (default class Kotlin = final!)
- Paham `override` untuk menimpa method
- Paham `super` untuk memanggil versi parent
- Paham constructor chaining

## 📖 Teori Singkat

**Pewarisan** = subclass mewarisi properti & method dari superclass.

**Analogi:** `Hewan` adalah blueprint umum. `Kucing` adalah blueprint yang lebih spesifik yang "adalah" Hewan + punya ciri tambahan.

**Aturan kunci Kotlin:**

1. Class default **final** — tidak bisa di-extend. Harus ditandai `open`.
2. Method default **final** — tidak bisa di-override. Harus ditandai `open`.
3. Subclass panggil constructor parent dengan `: Parent(...)`.

```kotlin
open class Parent(val x: Int)
class Child(x: Int, val y: Int) : Parent(x)
//                                   ^^^^^^^^^
//                                   Constructor chaining
```

## 🧩 Studi Kasus: 3 Jenis Hewan

Kita punya `Hewan` sebagai parent, lalu `Kucing`, `Anjing`, `Burung` sebagai subclass. Masing-masing punya properti unik dan suara sendiri.

## 💻 Kode Lengkap

**File: `Hewan.kt`**

```kotlin
package petshop

/**
 * Kelas dasar hewan.
 *
 * @property nama Nama hewan.
 * @property umur Umur dalam tahun.
 * @property noVaksin Nomor vaksin (rahasia).
 */
open class Hewan(
    val nama: String,
    val umur: Int,
    private val noVaksin: String
) {
    var sudahDiVaksin: Boolean = false
        private set

    fun vaksinasi() {
        sudahDiVaksin = true
        println("✅ $nama divaksin.")
    }

    fun getNoVaksin(): String = noVaksin

    /**
     * Menampilkan perkenalan umum. Bisa di-override oleh subclass.
     * Ditandai `open` agar subclass boleh menimpanya.
     */
    open fun perkenalan() {
        println("Halo, aku $nama, umur $umur tahun.")
    }

    /**
     * Suara hewan. Default: "...". Subclass wajib override.
     */
    open fun suara(): String = "..."
}
```

**File: `Kucing.kt`**

```kotlin
package petshop

/**
 * Subclass Kucing. Menambahkan properti [warnaBulu].
 */
class Kucing(
    nama: String,
    umur: Int,
    noVaksin: String,
    val warnaBulu: String
) : Hewan(nama, umur, noVaksin) {

    override fun suara(): String = "Meong!"

    override fun perkenalan() {
        super.perkenalan()
        println("Aku kucing dengan bulu warna $warnaBulu.")
    }
}
```

**File: `Anjing.kt`**

```kotlin
package petshop

/**
 * Subclass Anjing. Menambahkan properti [ras].
 */
class Anjing(
    nama: String,
    umur: Int,
    noVaksin: String,
    val ras: String
) : Hewan(nama, umur, noVaksin) {

    override fun suara(): String = "Guk guk!"

    override fun perkenalan() {
        super.perkenalan()
        println("Aku anjing ras $ras.")
    }
}
```

**File: `Burung.kt`**

```kotlin
package petshop

/**
 * Subclass Burung. Menambahkan properti [bisaTerbang].
 */
class Burung(
    nama: String,
    umur: Int,
    noVaksin: String,
    val bisaTerbang: Boolean
) : Hewan(nama, umur, noVaksin) {

    override fun suara(): String = "Cuit cuit!"

    override fun perkenalan() {
        super.perkenalan()
        val tb = if (bisaTerbang) "bisa" else "tidak bisa"
        println("Aku burung, $tb terbang.")
    }
}
```

**File: `Main.kt`**

```kotlin
package petshop

fun main() {
    val milo = Kucing("Milo", 2, "VX-01", "Oren")
    val rex = Anjing("Rex", 4, "VX-02", "German Shepherd")
    val chirpy = Burung("Chirpy", 1, "VX-03", true)

    milo.perkenalan();    println("  Suara: ${milo.suara()}\n")
    rex.perkenalan();     println("  Suara: ${rex.suara()}\n")
    chirpy.perkenalan();  println("  Suara: ${chirpy.suara()}\n")
}
```

## 🧪 Output yang Diharapkan

```
Halo, aku Milo, umur 2 tahun.
Aku kucing dengan bulu warna Oren.
  Suara: Meong!

Halo, aku Rex, umur 4 tahun.
Aku anjing ras German Shepherd.
  Suara: Guk guk!

Halo, aku Chirpy, umur 1 tahun.
Aku burung, bisa terbang.
  Suara: Cuit cuit!
```

## 🔍 Poin Penting yang Harus Dipahami

1. **Kenapa `nama`, `umur`, `noVaksin` di subclass tidak pakai `val`?**
   Karena sudah dideklarasikan di parent. Kalau pakai `val` lagi → error "conflicting declaration".

2. **Kenapa `Hewan` harus `open`?**
   Default Kotlin = `final` (tidak bisa di-extend). Untuk alasan keamanan.

3. **Kenapa `suara()` dan `perkenalan()` harus `open` di parent?**
   Supaya subclass diizinkan `override`. Kalau tidak `open`, subclass tidak bisa override.

4. **Apa fungsi `super.perkenalan()`?**
   Memanggil versi parent SEBELUM menambahkan info spesifik. Hasilnya tidak menimpa, tapi menambah.

## ✍️ Latihan Mandiri

1. **Mudah:** Buat subclass `Ikan` dengan properti `jenisAir: String` (nilai: "Tawar" atau "Asin"). Override `suara()` → "Blub blub!".
2. **Sedang:** Tambah `open fun makananFavorit(): String` di `Hewan` yang return `"Makanan umum"`, lalu override di tiap subclass.
3. **Tantang:** Buat subclass `Hamster` dengan properti `panjangEkorCm: Double`. Override semua method. Coba panggil `super.perkenalan()` di dalamnya.
4. **Refleksi:** Kenapa Kotlin membuat class `final` secara default? (Hint: prinsip "design for inheritance or prohibit it").

## ✅ Checklist Level 3

- [ ] Paham `open class` dan `open fun`
- [ ] Paham `override`
- [ ] Paham `super.method()`
- [ ] Paham constructor chaining `: Parent(...)`
- [ ] Bisa buat 3+ subclass

---

# 🎭 LEVEL 4 — ABSTRACTION (ABSTRAKSI)

## 🎯 Tujuan Pembelajaran

- Paham `abstract class` (tidak bisa diinstansiasi)
- Paham `abstract fun` (wajib di-override)
- Bisa mencampur abstract & concrete method
- Paham kapan pakai `abstract class` vs `open class`

## 📖 Teori Singkat

**Abstraksi** = membuat "kontrak" tanpa harus menyediakan implementasi.

**Analogi:** `Hewan` adalah konsep abstrak. Anda **tidak bisa** memelihara "Hewan" secara umum — Anda memelihara **Kucing**, **Anjing**, atau **Burung**. Jadi `Hewan` sebaiknya abstract.

**Perbedaan `open class` vs `abstract class`:**

| Aspek | `open class` | `abstract class` |
| ------- | ------------- | ------------------ |
| Bisa diinstansiasi? | ✅ Ya | ❌ Tidak |
| Bisa punya abstract method? | ❌ Tidak | ✅ Ya |
| Bisa punya concrete method? | ✅ Ya | ✅ Ya |

## 🧩 Studi Kasus: Biaya Perawatan Wajib Berbeda

Setiap hewan punya **biaya perawatan per hari** berbeda. Kita paksa setiap subclass mendefinisikan dengan `abstract fun`.

## 💻 Kode Lengkap

**File: `Hewan.kt`** (ubah jadi abstract)

```kotlin
package petshop

/**
 * Kelas abstrak dasar hewan. Tidak bisa diinstansiasi langsung.
 */
abstract class Hewan(
    val nama: String,
    val umur: Int,
    private val noVaksin: String
) {
    var sudahDiVaksin: Boolean = false
        private set

    // ====== ABSTRACT METHOD (wajib di-override) ======
    abstract fun biayaPerawatanPerHari(): Double
    abstract fun jenisHewan(): String
    abstract fun makananFavorit(): String

    // ====== CONCRETE METHOD (sudah ada implementasi) ======
    fun vaksinasi() {
        sudahDiVaksin = true
        println("✅ $nama divaksin.")
    }

    fun getNoVaksin(): String = noVaksin

    open fun perkenalan() {
        println("Halo, aku $nama (${jenisHewan()}), umur $umur tahun.")
    }
}
```

**File: `Kucing.kt`**

```kotlin
package petshop

class Kucing(
    nama: String,
    umur: Int,
    noVaksin: String,
    val warnaBulu: String
) : Hewan(nama, umur, noVaksin) {

    override fun biayaPerawatanPerHari(): Double = 50_000.0
    override fun jenisHewan(): String = "Kucing"
    override fun makananFavorit(): String = "Whiskas"

    override fun perkenalan() {
        super.perkenalan()
        println("Bulu: $warnaBulu")
    }
}
```

**File: `Anjing.kt`**

```kotlin
package petshop

class Anjing(
    nama: String,
    umur: Int,
    noVaksin: String,
    val ras: String
) : Hewan(nama, umur, noVaksin) {

    override fun biayaPerawatanPerHari(): Double = 80_000.0
    override fun jenisHewan(): String = "Anjing"
    override fun makananFavorit(): String = "Pedigree"

    override fun perkenalan() {
        super.perkenalan()
        println("Ras: $ras")
    }
}
```

**File: `Burung.kt`**

```kotlin
package petshop

class Burung(
    nama: String,
    umur: Int,
    noVaksin: String,
    val bisaTerbang: Boolean
) : Hewan(nama, umur, noVaksin) {

    override fun biayaPerawatanPerHari(): Double = 30_000.0
    override fun jenisHewan(): String = "Burung"
    override fun makananFavorit(): String = "Biji-bijian"

    override fun perkenalan() {
        super.perkenalan()
        println("Bisa terbang: $bisaTerbang")
    }
}
```

**File: `Main.kt`**

```kotlin
package petshop

fun main() {
    // val h = Hewan("X", 1, "VX") // ❌ ERROR: Cannot create instance of abstract class

    val list = listOf(
        Kucing("Milo", 2, "VX-01", "Oren"),
        Anjing("Rex", 4, "VX-02", "GS"),
        Burung("Chirpy", 1, "VX-03", true)
    )

    list.forEach {
        it.perkenalan()
        println("  Makanan favorit: ${it.makananFavorit()}")
        println("  Biaya/hari: Rp ${it.biayaPerawatanPerHari()}")
        println()
    }
}
```

## 🧪 Output yang Diharapkan

```
Halo, aku Milo (Kucing), umur 2 tahun.
Bulu: Oren
  Makanan favorit: Whiskas
  Biaya/hari: Rp 50000.0

Halo, aku Rex (Anjing), umur 4 tahun.
Ras: GS
  Makanan favorit: Pedigree
  Biaya/hari: Rp 80000.0

Halo, aku Chirpy (Burung), umur 1 tahun.
Bisa terbang: true
  Makanan favorit: Biji-bijian
  Biaya/hari: Rp 30000.0
```

## 🔍 Poin Penting

1. **Kenapa `Hewan` jadi `abstract`?** Karena tidak masuk akal punya "Hewan" tanpa spesifik Kucing/Anjing/dll.
2. **Kenapa `perkenalan()` tetap `open` bukan abstract?** Karena kita masih mau ada implementasi default.
3. **Kenapa `biayaPerawatanPerHari()` abstract?** Karena tidak ada nilai default yang masuk akal — tiap hewan beda.
4. **Keyword `abstract` di method** = otomatis `open`, tidak perlu tulis `open` lagi.

## ✍️ Latihan Mandiri

1. **Mudah:** Buat `abstract fun suara(): String`, override di semua subclass.
2. **Sedang:** Tambah method concrete `open fun infoLengkap()` yang print semua info (nama, jenis, biaya, makanan).
3. **Tantang:** Buat abstract class `Pegawai` dengan abstract `gajiBulanan(): Double`. Subclass: `DokterHewan`, `Perawat`, `Kasir`. Masing-masing punya gaji berbeda.
4. **Refleksi:** Kapan pakai `abstract class`, kapan pakai `interface`?

## ✅ Checklist Level 4

- [ ] Paham `abstract class` tidak bisa instansiasi
- [ ] Paham abstract method wajib di-override
- [ ] Bisa campur abstract + concrete
- [ ] Berhasil memicu error "Cannot create instance of abstract class"

---

# 🎨 LEVEL 5 — POLYMORPHISM (POLIMORFISME)

## 🎯 Tujuan Pembelajaran

- Paham **polymorphic reference**: `Hewan h = Kucing(...)`
- Paham **dynamic dispatch** (method dipilih saat runtime)
- Paham **smart casting** dengan `is`, `as?`, `as`
- Paham **pattern matching** dengan `when`

## 📖 Teori Singkat

**Polimorfisme** = "banyak bentuk". Satu variabel bertipe superclass bisa menampung objek subclass. Method yang dipanggil akan menyesuaikan objek aslinya (bukan tipe deklarasinya).

**Smart casting** = Kotlin cerdas — setelah cek `is Kucing`, otomatis compiler tahu objek itu Kucing, jadi kita bisa langsung akses `warnaBulu` tanpa cast manual.

**Tiga operator casting:**

| Operator | Aman? | Perilaku |
| ---------- | ------- | ---------- |
| `is T` | ✅ | Cek tipe, hasil `Boolean`. Memicu smart cast. |
| `as? T` | ✅ | Cast aman, kalau gagal → `null` |
| `as T` | ❌ | Cast paksa, kalau gagal → `ClassCastException` |

## 🧩 Studi Kasus: Daftar Campuran Hewan

Pet Shop punya daftar campuran. Kita ingin:

1. Loop semua hewan dan panggil method yang sama → hasil beda.
2. Cek jenis spesifik untuk print info detail.

## 💻 Kode Lengkap

**File: `Main.kt`**

```kotlin
package petshop

fun main() {
    // ===== POLYMORPHIC LIST =====
    val daftarHewan: List<Hewan> = listOf(
        Kucing("Milo", 2, "VX-01", "Oren"),
        Anjing("Rex", 4, "VX-02", "German Shepherd"),
        Burung("Chirpy", 1, "VX-03", true),
        Kucing("Luna", 3, "VX-04", "Hitam")
    )

    println("=== BIAYA PERAWATAN (POLYMORPHIC) ===")
    daftarHewan.forEach { h ->
        // Method sama, hasil beda-beda
        println("${h.nama} (${h.jenisHewan()}): Rp ${h.biayaPerawatanPerHari()}/hari")
    }

    // ===== SMART CAST DENGAN `is` =====
    println("\n=== SMART CAST DENGAN `is` ===")
    daftarHewan.forEach { h ->
        when (h) {
            is Kucing -> println("${h.nama} → Kucing warna bulu ${h.warnaBulu}")
            is Anjing -> println("${h.nama} → Anjing ras ${h.ras}")
            is Burung -> {
                val status = if (h.bisaTerbang) "bisa" else "tidak bisa"
                println("${h.nama} → Burung, $status terbang")
            }
            else -> println("${h.nama} → Jenis tidak dikenal")
        }
    }

    // ===== SAFE CAST `as?` =====
    println("\n=== SAFE CAST `as?` ===")
    val hewanPertama = daftarHewan[0]
    val sebagaiAnjing: Anjing? = hewanPertama as? Anjing
    println("Coba cast Milo ke Anjing: ${sebagaiAnjing ?: "GAGAL — hasil null"}")

    val sebagaiKucing: Kucing? = hewanPertama as? Kucing
    println("Coba cast Milo ke Kucing: ${sebagaiKucing?.warnaBulu ?: "GAGAL"}")

    // ===== UNSAFE CAST `as` (JANGAN dijalankan tanpa yakin!) =====
    // val paksa = hewanPertama as Anjing   // ❌ ClassCastException runtime!
}
```

## 🧪 Output yang Diharapkan

```
=== BIAYA PERAWATAN (POLYMORPHIC) ===
Milo (Kucing): Rp 50000.0/hari
Rex (Anjing): Rp 80000.0/hari
Chirpy (Burung): Rp 30000.0/hari
Luna (Kucing): Rp 50000.0/hari

=== SMART CAST DENGAN `is` ===
Milo → Kucing warna bulu Oren
Rex → Anjing ras German Shepherd
Chirpy → Burung, bisa terbang
Luna → Kucing warna bulu Hitam

=== SAFE CAST `as?` ===
Coba cast Milo ke Anjing: GAGAL — hasil null
Coba cast Milo ke Kucing: Oren
```

## 🔍 Poin Penting

1. **Kenapa `daftarHewan[0] as? Anjing` hasilnya `null`?** Karena Milo adalah `Kucing`, bukan `Anjing`. Safe cast mengembalikan `null` alih-alih melempar exception.
2. **Kenapa `h.warnaBulu` bisa diakses di dalam `is Kucing ->`?** Itu **smart cast** — Kotlin tahu `h` pasti `Kucing` di branch itu.
3. **Kapan pakai `as?` vs `as`?** Pakai `as?` kalau tidak yakin. Pakai `as` hanya kalau Anda 100% yakin dan mau error kalau salah.

## ✍️ Latihan Mandiri

1. **Mudah:** Filter `daftarHewan` jadi hanya Kucing, lalu print semuanya.
2. **Sedang:** Hitung total biaya perawatan seluruh hewan jika dirawat 7 hari.
3. **Tantang:** Kelompokkan hewan berdasarkan `jenisHewan()`, print tiap kelompok.
4. **Tantang+:** Buat fungsi `deskripsiHewan(h: Hewan): String` yang memanfaatkan `when` + smart cast untuk print info detail per jenis.

## ✅ Checklist Level 5

- [ ] Paham `List<Hewan>` bisa isi subclass
- [ ] Paham dynamic dispatch
- [ ] Bisa pakai `is` + smart cast
- [ ] Bisa pakai `as?` untuk safe cast
- [ ] Tahu perbedaan `as` dan `as?`

---

# 🚦 LEVEL 6 — SEALED CLASS

## 🎯 Tujuan Pembelajaran

- Paham `sealed class` = class dengan himpunan subclass terbatas
- Paham kapan pakai `object` vs `data class` di sealed
- Paham **ekshaustif `when`** (tanpa `else`)
- Paham konsep "status akhir" (`isFinal`)

## 📖 Teori Singkat

**Sealed class** = superclass yang semua subclass-nya harus berada dalam **file yang sama**. Compiler tahu semua kemungkinannya → cocok untuk **state/status**.

**Analogi:** Lampu lalu lintas hanya punya 3 state: Merah, Kuning, Hijau. Tidak mungkin ada state ke-4. Kalau pakai class biasa, orang bisa buat subclass baru seenaknya.

**Kapan pakai apa:**

| Butuh | Pakai |
| ------- | ------- |
| State tanpa data tambahan | `object` |
| State dengan data | `data class` |
| Himpunan terbatas, tidak butuh instance | `enum class` |
| Himpunan terbatas + perlu data berbeda tiap state | `sealed class` |

## 🧩 Studi Kasus: Status Adopsi

Proses adopsi punya 4 status:

- 🟢 `Tersedia` — tanpa data
- 🟡 `Diajukan` — perlu nama calon
- ✅ `SudahDiadopsi` — perlu tanggal
- ❌ `Dibatalkan` — tanpa data

## 💻 Kode Lengkap

**File: `StatusAdopsi.kt`**

```kotlin
package petshop

/**
 * Sealed class untuk merepresentasikan status adopsi hewan.
 * Semua subclass didefinisikan di file yang sama.
 */
sealed class StatusAdopsi {

    /**
     * Deskripsi singkat status untuk ditampilkan.
     */
    abstract fun deskripsi(): String

    /**
     * Apakah status ini final (tidak bisa diubah lagi)?
     * Default: false. Subclass final harus override jadi true.
     */
    open fun isFinal(): Boolean = false

    /** Hewan tersedia untuk diadopsi. */
    object Tersedia : StatusAdopsi() {
        override fun deskripsi() = "🟢 Tersedia untuk diadopsi"
    }

    /** Hewan sedang diajukan oleh calon tertentu. */
    data class Diajukan(val namaCalon: String) : StatusAdopsi() {
        override fun deskripsi() = "🟡 Sedang diajukan oleh $namaCalon"
    }

    /** Hewan sudah resmi diadopsi. Status final. */
    data class SudahDiadopsi(val tanggal: String) : StatusAdopsi() {
        override fun deskripsi() = "✅ Sudah diadopsi pada $tanggal"
        override fun isFinal(): Boolean = true
    }

    /** Adopsi dibatalkan. Status final. */
    object Dibatalkan : StatusAdopsi() {
        override fun deskripsi() = "❌ Adopsi dibatalkan"
        override fun isFinal(): Boolean = true
    }
}
```

**File: `Main.kt`**

```kotlin
package petshop

fun main() {
    val daftarStatus: List<StatusAdopsi> = listOf(
        StatusAdopsi.Tersedia,
        StatusAdopsi.Diajukan("Budi"),
        StatusAdopsi.SudahDiadopsi("2024-05-01"),
        StatusAdopsi.Dibatalkan
    )

    println("=== DEMO SEALED CLASS ===")
    daftarStatus.forEach { s ->
        // `when` EKSHAUSTIF — TANPA `else`!
        val info = when (s) {
            is StatusAdopsi.Tersedia -> "Belum ada calon"
            is StatusAdopsi.Diajukan -> "Calon: ${s.namaCalon}"
            is StatusAdopsi.SudahDiadopsi -> "Tanggal: ${s.tanggal}"
            is StatusAdopsi.Dibatalkan -> "Tidak ada adopsi"
        }
        println("${s.deskripsi()} | $info | final=${s.isFinal()}")
    }
}
```

## 🧪 Output yang Diharapkan

```
=== DEMO SEALED CLASS ===
🟢 Tersedia untuk diadopsi | Belum ada calon | final=false
🟡 Sedang diajukan oleh Budi | Calon: Budi | final=false
✅ Sudah diadopsi pada 2024-05-01 | Tanggal: 2024-05-01 | final=true
❌ Adopsi dibatalkan | Tidak ada adopsi | final=true
```

## 🔍 Poin Penting

1. **Kenapa `object` untuk `Tersedia` dan `Dibatalkan`?** Karena tidak ada data tambahan — cukup satu instance global.
2. **Kenapa `data class` untuk `Diajukan` dan `SudahDiadopsi`?** Karena perlu data (nama calon / tanggal).
3. **Kenapa `when` tidak butuh `else`?** Karena sealed class — compiler tahu semua kemungkinan subclass. Ini disebut **ekshaustif**.
4. **Eksperimen wajib:** Coba tambahkan subclass baru `Kadaluarsa` ke `StatusAdopsi.kt`. Compile → **error "when expression must be exhaustive"**. Itu bukti sealed class memaksa Anda menangani semua kasus.

## ✍️ Latihan Mandiri

1. **Mudah:** Tambah status `Kadaluarsa(val alasan: String)`. Update semua `when` yang ekshaustif.
2. **Sedang:** Buat method `bisaDibatalkan(): Boolean` yang return `!isFinal()`.
3. **Tantang:** Buat sealed class baru `StatusPembayaran` dengan state: `BelumBayar`, `DP(val jumlah: Double)`, `Lunas(val total: Double)`, `Refund(val alasan: String)`.
4. **Refleksi:** Kenapa `enum class` kurang cocok untuk kasus ini? (Hint: enum tidak bisa simpan data berbeda per case.)

## ✅ Checklist Level 6

- [ ] Paham `sealed class`
- [ ] Paham `object` vs `data class` di sealed
- [ ] Paham ekshaustif `when`
- [ ] Berhasil memicu error "when must be exhaustive"

---

# 🏆 LEVEL 7 — MINI PROJECT: GABUNGKAN SEMUA

## 🎯 Tujuan

Membangun sistem mini yang **strukturnya mirip perpustakaan**, tapi dengan domain Pet Shop.

## 📁 Struktur File

```
petshop/
├── Main.kt
├── Hewan.kt
├── Kucing.kt
├── Anjing.kt
├── Burung.kt
├── StatusAdopsi.kt
├── Adopsi.kt
├── CalonPemilik.kt
└── PetShop.kt
```

## 🧩 Aturan Bisnis

- **Hewan:** punya `id`, `nama`, `umur`, `tersedia` (private set).
- **Biaya perawatan:** Kucing Rp 50.000/hari, Anjing Rp 80.000/hari, Burung Rp 30.000/hari.
- **Calon pemilik:** Maksimal **2 adopsi aktif** sekaligus.
- **Adopsi:** punya `id` (auto-generate), `hewan`, `pemilik`, `tanggal`, `status`.
- **Pet Shop:** kelola semua.

## 💻 Kode Lengkap

### 1. `Hewan.kt`

```kotlin
package petshop

/**
 * Kelas abstrak dasar untuk semua hewan.
 */
abstract class Hewan(
    val id: String,
    val nama: String,
    val umur: Int
) {
    var tersedia: Boolean = true
        private set

    abstract fun biayaPerawatanHarian(): Double
    abstract fun jenisHewan(): String

    /**
     * Ajukan adopsi. Mengubah [tersedia] jadi false jika berhasil.
     */
    fun ajukanAdopsi(): Boolean {
        return if (tersedia) {
            tersedia = false
            println("✅ ${nama} berhasil diajukan untuk diadopsi.")
            true
        } else {
            println("❌ ${nama} tidak tersedia.")
            false
        }
    }

    /**
     * Kembalikan status tersedia (misal: adopsi dibatalkan).
     */
    fun batalkanAdopsi() {
        if (!tersedia) {
            tersedia = true
            println("↩️  Adopsi ${nama} dibatalkan, hewan kembali tersedia.")
        }
    }

    open fun displayInfo() {
        val status = if (tersedia) "Tersedia" else "Tidak tersedia"
        println("[$id] $nama | ${jenisHewan()} | ${umur} th | $status")
        println("     Biaya/hari: Rp ${biayaPerawatanHarian()}")
    }
}
```

### 2. `Kucing.kt`

```kotlin
package petshop

class Kucing(
    id: String, nama: String, umur: Int,
    val warnaBulu: String
) : Hewan(id, nama, umur) {
    override fun biayaPerawatanHarian() = 50_000.0
    override fun jenisHewan() = "Kucing"

    override fun displayInfo() {
        super.displayInfo()
        println("     Warna bulu: $warnaBulu")
    }
}
```

### 3. `Anjing.kt`

```kotlin
package petshop

class Anjing(
    id: String, nama: String, umur: Int,
    val ras: String
) : Hewan(id, nama, umur) {
    override fun biayaPerawatanHarian() = 80_000.0
    override fun jenisHewan() = "Anjing"

    override fun displayInfo() {
        super.displayInfo()
        println("     Ras: $ras")
    }
}
```

### 4. `Burung.kt`

```kotlin
package petshop

class Burung(
    id: String, nama: String, umur: Int,
    val bisaTerbang: Boolean
) : Hewan(id, nama, umur) {
    override fun biayaPerawatanHarian() = 30_000.0
    override fun jenisHewan() = "Burung"

    override fun displayInfo() {
        super.displayInfo()
        val tb = if (bisaTerbang) "bisa" else "tidak bisa"
        println("     $tb terbang")
    }
}
```

### 5. `StatusAdopsi.kt`

```kotlin
package petshop

sealed class StatusAdopsi {
    abstract fun deskripsi(): String
    open fun isFinal(): Boolean = false

    object Tersedia : StatusAdopsi() {
        override fun deskripsi() = "🟢 Tersedia"
    }
    data class Diajukan(val namaCalon: String) : StatusAdopsi() {
        override fun deskripsi() = "🟡 Diajukan oleh $namaCalon"
    }
    data class SudahDiadopsi(val tanggal: String) : StatusAdopsi() {
        override fun deskripsi() = "✅ Diadopsi pada $tanggal"
        override fun isFinal() = true
    }
    object Dibatalkan : StatusAdopsi() {
        override fun deskripsi() = "❌ Dibatalkan"
        override fun isFinal() = true
    }
}
```

### 6. `Adopsi.kt`

```kotlin
package petshop

import java.time.LocalDate

/**
 * Merepresentasikan satu proses adopsi.
 */
class Adopsi(
    val id: String,
    val hewan: Hewan,
    val pemilik: CalonPemilik,
    val tanggal: String = LocalDate.now().toString()
) {
    var status: StatusAdopsi = StatusAdopsi.Tersedia

    /**
     * Finalisasi adopsi. Return true jika berhasil.
     */
    fun finalisasi(): Boolean {
        if (status.isFinal()) {
            println("❌ Adopsi #$id sudah final, tidak bisa difinalisasi lagi.")
            return false
        }
        status = StatusAdopsi.SudahDiadopsi(tanggal)
        println("🎉 ${hewan.nama} resmi diadopsi oleh ${pemilik.nama}!")
        return true
    }

    /**
     * Batalkan adopsi. Mengembalikan hewan ke status tersedia.
     */
    fun batalkan() {
        if (status.isFinal()) {
            println("❌ Adopsi #$id sudah final, tidak bisa dibatalkan.")
            return
        }
        status = StatusAdopsi.Dibatalkan
        hewan.batalkanAdopsi()
    }

    fun display() {
        println("Adopsi #$id | Hewan: ${hewan.nama} | Pemilik: ${pemilik.nama}")
        println("  Tanggal: $tanggal")
        println("  Status: ${status.deskripsi()}")
    }
}
```

### 7. `CalonPemilik.kt`

```kotlin
package petshop

/**
 * Calon pemilik hewan (analog dengan "Member" di perpustakaan).
 */
class CalonPemilik(
    val id: String,
    val nama: String,
    private val email: String,
    private val telepon: String
) {
    private val riwayatAdopsi: MutableList<Adopsi> = mutableListOf()

    val jumlahAdopsi: Int get() = riwayatAdopsi.size
    val adopsiAktif: Int get() = riwayatAdopsi.count { !it.status.isFinal() }

    fun getEmail(): String = email
    fun getTelepon(): String = telepon

    /**
     * Ajukan adopsi hewan. Return [Adopsi] jika berhasil, null jika gagal.
     */
    fun ajukanAdopsi(hewan: Hewan): Adopsi? {
        if (!hewan.tersedia) {
            println("❌ ${hewan.nama} sedang tidak tersedia.")
            return null
        }
        if (adopsiAktif >= 2) {
            println("❌ $nama sudah punya 2 adopsi aktif. Selesaikan dulu.")
            return null
        }
        if (!hewan.ajukanAdopsi()) return null

        val adopsi = Adopsi("ADP-${System.currentTimeMillis()}", hewan, this)
        riwayatAdopsi.add(adopsi)
        println("✅ $nama berhasil mengajukan adopsi ${hewan.nama}.")
        return adopsi
    }

    fun displayInfo() {
        println("[$id] $nama | $email | $telepon")
        println("   Total adopsi: $jumlahAdopsi | Aktif: $adopsiAktif")
    }

    fun displayTransaksi() {
        println("\n--- Riwayat Adopsi: $nama ---")
        if (riwayatAdopsi.isEmpty()) {
            println("  (belum ada)")
        } else {
            riwayatAdopsi.forEach { it.display() }
        }
    }
}
```

### 8. `PetShop.kt`

```kotlin
package petshop

/**
 * Kelas utama pengelola Pet Shop.
 */
class PetShop(val nama: String) {
    private val hewanList: MutableList<Hewan> = mutableListOf()
    private val pemilikList: MutableList<CalonPemilik> = mutableListOf()
    private val adopsiList: MutableList<Adopsi> = mutableListOf()

    val totalHewan: Int get() = hewanList.size
    val hewanTersedia: Int get() = hewanList.count { it.tersedia }
    val totalPemilik: Int get() = pemilikList.size
    val totalAdopsi: Int get() = adopsiList.size

    fun tambahHewan(h: Hewan) {
        hewanList.add(h)
        println("✅ ${h.nama} ditambahkan ke ${nama}.")
    }

    fun tambahHewan(vararg list: Hewan) {
        list.forEach { tambahHewan(it) }
    }

    fun daftarPemilik(id: String, nama: String, email: String, telp: String): Boolean {
        if (pemilikList.any { it.id == id }) {
            println("❌ ID $id sudah terdaftar.")
            return false
        }
        pemilikList.add(CalonPemilik(id, nama, email, telp))
        println("✅ Pemilik $nama berhasil didaftarkan.")
        return true
    }

    fun cariHewan(id: String): Hewan? = hewanList.find { it.id == id }
    fun cariPemilik(id: String): CalonPemilik? = pemilikList.find { it.id == id }

    fun ajukanAdopsi(pemilikId: String, hewanId: String): Adopsi? {
        val p = cariPemilik(pemilikId)
        if (p == null) { println("❌ Pemilik $pemilikId tidak ditemukan."); return null }
        val h = cariHewan(hewanId)
        if (h == null) { println("❌ Hewan $hewanId tidak ditemukan."); return null }

        val adopsi = p.ajukanAdopsi(h) ?: return null
        adopsiList.add(adopsi)
        return adopsi
    }

    fun displaySemuaHewan() {
        println("\n=== DAFTAR HEWAN ===")
        hewanList.forEach { it.displayInfo(); println() }
        println("Total: $totalHewan | Tersedia: $hewanTersedia")
    }

    fun displayHewanTersedia() {
        println("\n=== HEWAN TERSEDIA ===")
        val tersedia = hewanList.filter { it.tersedia }
        if (tersedia.isEmpty()) println("(tidak ada)")
        else tersedia.forEach { println("[$it.id] ${it.nama} (${it.jenisHewan()})") }
    }

    fun displaySemuaPemilik() {
        println("\n=== DAFTAR PEMILIK ===")
        pemilikList.forEach { it.displayInfo(); println() }
    }

    fun displaySemuaAdopsi() {
        println("\n=== SEMUA ADOPSI ===")
        if (adopsiList.isEmpty()) println("(belum ada)")
        else adopsiList.forEach { it.display(); println() }
    }

    fun displayLaporan() {
        println("\n=== LAPORAN PET SHOP ===")
        println("Nama          : $nama")
        println("Total hewan   : $totalHewan")
        println("Hewan tersedia: $hewanTersedia")
        println("Hewan diadopsi: ${totalHewan - hewanTersedia}")
        println("Total pemilik : $totalPemilik")
        println("Total adopsi  : $totalAdopsi")
    }
}
```

### 9. `Main.kt`

```kotlin
package petshop

fun main() {
    val shop = PetShop("MeowWoof Pet Shop")

    // ===== 1. Tambah hewan =====
    println("\n=== 1. TAMBAH HEWAN ===")
    shop.tambahHewan(
        Kucing("H001", "Milo", 2, "Oren"),
        Kucing("H002", "Luna", 3, "Hitam"),
        Anjing("H003", "Rex", 4, "German Shepherd"),
        Anjing("H004", "Bella", 2, "Poodle"),
        Burung("H005", "Chirpy", 1, true),
        Burung("H006", "Kiwi", 1, false)
    )

    // ===== 2. Daftarkan pemilik =====
    println("\n=== 2. DAFTAR PEMILIK ===")
    shop.daftarPemilik("P001", "Ahmad", "ahmad@mail.com", "081111")
    shop.daftarPemilik("P002", "Dewi", "dewi@mail.com", "082222")
    shop.daftarPemilik("P003", "Rizky", "rizky@mail.com", "083333")

    // ===== 3. Tampilkan semua hewan =====
    shop.displaySemuaHewan()

    // ===== 4. Adopsi =====
    println("\n=== 4. ADOPSI ===")
    shop.ajukanAdopsi("P001", "H001")   // Ahmad adopsi Milo
    shop.ajukanAdopsi("P001", "H003")   // Ahmad adopsi Rex
    shop.ajukanAdopsi("P002", "H005")   // Dewi adopsi Chirpy
    shop.ajukanAdopsi("P003", "H002")   // Rizky adopsi Luna

    // ===== 5. Hewan tersedia =====
    shop.displayHewanTersedia()

    // ===== 6. Laporan =====
    shop.displayLaporan()
}
```

## 🧪 Output yang Diharapkan (potongan)

```
=== 1. TAMBAH HEWAN ===
✅ Milo ditambahkan ke MeowWoof Pet Shop.
...

=== DAFTAR HEWAN ===
[H001] Milo | Kucing | 2 th | Tersedia
     Biaya/hari: Rp 50000.0
     Warna bulu: Oren
...

=== HEWAN TERSEDIA ===
[H004] Bella (Anjing)
[H006] Kiwi (Burung)

=== LAPORAN PET SHOP ===
Nama          : MeowWoof Pet Shop
Total hewan   : 6
Hewan tersedia: 2
Hewan diadopsi: 4
Total pemilik : 3
Total adopsi  : 4
```

## ✍️ Latihan Mini Project

1. **Mudah:** Tambah method `displayPemilikTransaksi(id: String)` yang print riwayat adopsi seorang pemilik.
2. **Sedang:** Tambah method `cariHewanByNama(keyword: String): List<Hewan>` (case-insensitive).
3. **Sedang:** Tambah fitur `finalisasiAdopsi(adopsiId)` — pindah status dari `Diajukan` → `SudahDiadopsi`.
4. **Tantang:** Tambah **biaya adopsi** (`biayaAdopsi()`) di tiap hewan (Kucing 500rb, Anjing 1jt, Burung 250rb). Tambah properti `totalBiayaAdopsi` di `CalonPemilik`.
5. **Tantang+:** Buat method `displayLaporanPerJenis()` yang mengelompokkan hewan per jenis dan hitung jumlahnya.

## ✅ Checklist Level 7

- [ ] 9 file `.kt` dibuat terpisah
- [ ] KDoc di semua kelas & method publik
- [ ] Semua konsep OOP diterapkan
- [ ] Program berjalan tanpa error
- [ ] Output sesuai harapan

---

# 🔄 BAB 8 — MAPPING KE PROYEK PERPUSTAKAAN

## Tabel Konversi Lengkap

| Pet Shop | Perpustakaan Digital | Catatan |
| ---------- | --------------------- | --------- |
| `Hewan` | `Item` | Abstract class |
| `Kucing`, `Anjing`, `Burung` | `Book`, `Journal`, `DVD` | Subclass |
| `biayaPerawatanHarian()` | `calculateFinePerDay()` | Denda per hari |
| `jenisHewan()` | `getItemType()` | Jenis item |
| `tersedia` | `isAvailable` | Private set |
| `ajukanAdopsi()` | `borrow()` | Ubah jadi tidak tersedia |
| `batalkanAdopsi()` | `returnItem()` | **Beda!** Di perpus, `returnItem` punya parameter `daysLate` |
| `StatusAdopsi` | `TransactionStatus` | Sealed class |
| `Adopsi` | `Transaction` | Kelas transaksi |
| `CalonPemilik` | `Member` | Pengguna |
| `PetShop` | `Library` | Kelas utama |
| `jumlahAdopsi` | `transactionCount` | Computed |
| `adopsiAktif` | `activeBorrows` | Computed |
| — | `totalFines` | **BARU!** Di perpus ada denda |
| — | `getMaxBorrowDays()` | **BARU!** Batas hari pinjam |

## Perbedaan Penting yang Harus Disesuaikan

1. **`returnItem()` di `Item` perpustakaan** punya parameter `daysLate: Int = 0`, dan mengembalikan `Double` (denda).
2. **`TransactionStatus.Overdue(daysLate)`** adalah state baru yang tidak ada di Pet Shop.
3. **`getMaxBorrowDays()`** abstract method baru — di Pet Shop tidak ada.
4. **`Member.totalFines`** — jumlahkan `daysLate * item.calculateFinePerDay()` untuk semua transaksi `Overdue`.
5. **`Member.borrowItem()`** — batas 3 item aktif (Pet Shop: 2).
6. **ID transaksi** — pakai `"TRX-${System.currentTimeMillis()}"`.
7. **Tanggal** — pakai `java.time.LocalDate.now().toString()`.

## 🎯 Langkah Migrasi (Rekomendasi)

1. **Copy folder Pet Shop** → rename jadi `perpustakaan`.
2. **Rename semua kelas** sesuai tabel mapping di atas.
3. **Tambah `getMaxBorrowDays()`** abstract di `Item`, override di 3 subclass (14, 7, 3).
4. **Tambah parameter `daysLate`** di `returnItem()` dan ubah jadi return `Double`.
5. **Tambah `Overdue`** di `TransactionStatus`.
6. **Sesuaikan logika `Transaction.returnItem()`**:

   ```kotlin
   fun returnItem(daysLate: Int): Double {
       if (status.isFinal()) {
           println("❌ Transaksi sudah final.")
           return 0.0
       }
       val denda = item.returnItem(daysLate)
       status = if (daysLate > 0) TransactionStatus.Overdue(daysLate)
                else TransactionStatus.Returned
       return denda
   }
   ```

7. **Tambah `totalFines`** di `Member`:

   ```kotlin
   val totalFines: Double
       get() = transactions
           .filter { it.status is TransactionStatus.Overdue }
           .sumOf {
               (it.status as TransactionStatus.Overdue).daysLate *
               it.item.calculateFinePerDay()
           }
   ```

8. **Update `main()`** sesuai skenario D.2 di spesifikasi tugas.

---

# 🏋️ BAB 9 — LATIHAN MANDIRI TAMBAHAN

Setelah paham Pet Shop, coba kerjakan **satu** dari studi kasus berikut dari nol:

### 1. Sistem Rental Mobil 🚗

- `Kendaraan` (abstract) → `Mobil`, `Motor`, `Truk`
- `StatusRental` (sealed): `Tersedia`, `Disewa`, `Terlambat(hari)`, `Dikembalikan`
- `Penyewa` (member)
- `Rental` (transaksi)
- `RentalMobil` (library)

### 2. Sistem Kafe ☕

- `Menu` (abstract) → `Minuman`, `Makanan`, `Snack`
- `StatusPesanan` (sealed): `Dipesan`, `Dibuat`, `Disajikan`, `Dibatalkan`
- `Pelanggan` (member)
- `Pesanan` (transaksi)
- `Kafe` (library)

### 3. Sistem Bengkel 🔧

- `Servis` (abstract) → `ServisRingan`, `ServisBerat`, `GantiOli`
- `StatusServis` (sealed): `Antrian`, `Dikerjakan`, `Selesai`, `Batal`
- `Pelanggan` (member)
- `Order` (transaksi)
- `Bengkel` (library)

**Target:** Selesaikan dalam 1 hari. Kalau berhasil → Anda **SUDAH SIAP** untuk tugas perpustakaan.

---

# 📅 RENCANA BELAJAR 7 HARI

| Hari | Target | Durasi |
| ------ | -------- | -------- |
| 1 | Setup + Level 1–2 | 2 jam |
| 2 | Level 3–4 | 2 jam |
| 3 | Level 5–6 | 2 jam |
| 4 | Level 7 (Pet Shop part 1) | 3 jam |
| 5 | Level 7 (Pet Shop part 2) + testing | 3 jam |
| 6 | Mapping ke Perpustakaan + coding | 4 jam |
| 7 | Testing + Screenshot + Laporan | 4 jam |
| **Total** | | **~20 jam** |

---

# 💡 TIPS BELAJAR EMAS

1. **Ketik ulang, jangan copy-paste.** Otot jari harus hafal sintaks Kotlin.
2. **Ubah-ubah kode.** Ganti nama variabel, tambah properti, rusak sengaja, lalu perbaiki.
3. **Baca error dengan tenang.** Pesan error Kotlin sangat jelas — biasanya langsung menunjukkan baris & solusi.
4. **Gunakan `println` untuk debug.** Jangan malas. Print nilai di tengah kode untuk cek.
5. **Commit ke Git setiap level selesai.** Kalau nanti rusak, bisa rollback.
6. **Kalau stuck > 30 menit**, istirahat 10 menit, lanjut lagi.
7. **Jangan takut error.** Error = guru terbaik. Setiap error yang berhasil di-fix = 1 level naik.

---

# ✅ CHECKLIST AKHIR SEBELUM GARAP TUGAS PERPUSTAKAAN

- [ ] Semua 7 level sudah selesai
- [ ] Mini Project Pet Shop berjalan tanpa error
- [ ] Paham 4 pilar OOP (Enkapsulasi, Pewarisan, Polimorfisme, Abstraksi)
- [ ] Paham `sealed class` + ekshaustif `when`
- [ ] Paham smart casting (`is`, `as?`)
- [ ] Sudah coba minimal 1 latihan mandiri (Rental / Kafe / Bengkel)
- [ ] Bisa menjelaskan tiap baris kode ke orang lain

Kalau semua ✅ → **Anda SIAP mengerjakan Tugas Mandiri Perpustakaan Digital!** 🚀

---

## 🎓 PENUTUP

> **"Kode yang baik bukan yang paling pintar, tapi yang paling mudah dipahami oleh orang lain — dan oleh diri Anda sendiri 6 bulan kemudian."**

Setelah menyelesaikan latihan ini, tugas perpustakaan akan terasa seperti **versi upgrade dari Pet Shop** — hanya ganti nama kelas & tambah logika denda.

Semangat! Kalau stuck di level tertentu, tinggal tanya bagian mana yang bingung. 💪
