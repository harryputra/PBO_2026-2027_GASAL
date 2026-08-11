Berikut adalah **Modul Praktikum Pertemuan 1** yang **Super Ultra Lengkap** sesuai dengan materi pokok yang telah diberikan. Modul ini mencakup **3 Praktikum Terbimbing** (step-by-step dengan dosen) dan **5 Praktikum Mandiri** (dikerjakan sendiri oleh mahasiswa), lengkap dengan teori pendukung, kode solusi, contoh output, dan rubrik penilaian.

---

# MODUL PRAKTIKUM PEMROGRAMAN BERORIENTASI OBJEK (PBO)
## Pertemuan 1: Pengenalan Kotlin & Konsep Dasar OOP

| **Kode Mata Kuliah** | TRI-XX-XXX |
| :--- | :--- |
| **Program Studi** | D4 Teknologi Rekayasa Informatika Industri |
| **Semester** | Ganjil |
| **Alokasi Waktu** | 4 x 50 Menit (Sesi 1-4) |

---

### A. Capaian Pembelajaran Praktikum (CPMK)
1. Mahasiswa mampu menginstal dan mengkonfigurasi lingkungan pengembangan Kotlin (JDK + IntelliJ IDEA).
2. Mahasiswa mampu membuat project Kotlin pertama dan menjalankan fungsi `main()`.
3. Mahasiswa mampu membedakan serta mengimplementasikan `var`, `val`, dan `const val` dalam kode sederhana.
4. Mahasiswa mampu mendeklarasikan **Class**, **Atribut/Properti**, dan **Method** sesuai kaidah OOP di Kotlin.
5. Mahasiswa mampu menginstansiasi objek dan mengakses properti/metodenya tanpa menggunakan keyword `new`.

### B. Alat dan Bahan
- **Perangkat Keras**: Laptop/PC dengan spesifikasi minimal (RAM 4GB, Processor Dual Core).
- **Perangkat Lunak**:
  - JDK 11 atau lebih tinggi (disarankan **Eclipse Adoptium** atau **Oracle OpenJDK**).
  - **IntelliJ IDEA Community Edition** 2023.3 atau lebih baru.
  - Sistem Operasi: Windows 10/11, Linux, atau MacOS.

---

## BAGIAN I: PRAKTIKUM TERBIMBING (3 Sesi)

*Instruksi: Ikuti langkah-langkah di bawah ini bersama asisten/dosen. Jangan lanjut ke tahap berikutnya sebelum kode berhasil dijalankan.*

---

### Praktikum Terbimbing 1: Hello World & Eksplorasi `var`, `val`, dan `const val`
**Tujuan**: Memahami struktur dasar project Kotlin, fungsi `main()`, serta perbedaan `var`, `val`, dan `const val`.

**Langkah-Langkah**:
1. Buka IntelliJ IDEA, pilih **New Project**.
2. Pada panel kiri, pilih **Kotlin**. Isi:
   - **Name**: `Praktikum1_HelloWorld`
   - **Build system**: `IntelliJ`
   - **JDK**: Pilih JDK yang sudah diinstal (minimal version 11).
   - Centang **Add sample code** agar otomatis membuat file `main.kt`.
   - Klik **Create**.
3. Tunggu hingga project selesai di-load. Buka file `src/main/kotlin/main.kt`.
4. Hapus kode template, lalu tulis kode berikut untuk menguji `var` dan `val`:

```kotlin
// 1. Mendeklarasikan konstanta compile-time (CONST VAL)
const val APP_VERSION = "1.0.0" // Harus di top-level

fun main() {
    // 2. Menggunakan var (Mutable)
    var namaDepan: String = "Budi"
    var namaBelakang = "Santoso" // Type inference (String)
    println("Halo, $namaDepan $namaBelakang!")

    // Mengubah nilai var (BOLEH)
    namaDepan = "Andi"
    println("Nama setelah diubah: $namaDepan $namaBelakang")

    // 3. Menggunakan val (Read-Only / Immutable reference)
    val nim: String = "1234567890"
    println("NIM: $nim")
    // nim = "0987654321" // ERROR! Baris ini akan error karena val tidak bisa di-reassign

    // 4. Membuktikan val pada objek mutable (isi bisa berubah, referensi tetap)
    val daftarNilai = mutableListOf(85, 90, 78)
    println("Daftar nilai awal: $daftarNilai")
    daftarNilai.add(95) // Menambah elemen (BOLEH, karena isi objek berubah)
    println("Daftar nilai setelah tambah: $daftarNilai")

    // 5. Mengakses konstanta compile-time
    println("Aplikasi versi: $APP_VERSION")

    // 6. Perbedaan dengan konstanta di Java (static final) - const val hanya untuk tipe primitif/String
    // const val PI = 3.14 // Boleh (Double)
    // const val USER_NAME = "admin" // Boleh (String)
}
```

5. **Jalankan kode** dengan mengklik tombol segitiga hijau di samping fungsi `main()`.
6. **Output yang diharapkan**:
```text
Halo, Budi Santoso!
Nama setelah diubah: Andi Santoso
NIM: 1234567890
Daftar nilai awal: [85, 90, 78]
Daftar nilai setelah tambah: [85, 90, 78, 95]
Aplikasi versi: 1.0.0
```

**Diskusi Terbimbing**:
- Mengapa `APP_VERSION` menggunakan `const val` dan diletakkan di luar `main()`?
- Apa yang terjadi jika kita meng-uncomment baris `nim = ...`? Jelaskan pesan errornya.

---

### Praktikum Terbimbing 2: Membuat Class dan Objek Sederhana (Blueprint Kue)
**Tujuan**: Memahami analogi kelas sebagai cetakan (blueprint) dan objek sebagai realisasinya.

**Langkah-Langkah**:
1. Di project yang sama, buat file Kotlin baru dengan cara: Klik kanan pada folder `src/main/kotlin` → **New** → **Kotlin Class/File**. Beri nama `Kue.kt`.
2. Tulis kode berikut di `Kue.kt`:

```kotlin
// Ini adalah BLUEPRINT / CETAKAN (Class)
class Kue(
    val nama: String,          // Properti read-only (bahan dasar)
    var rasa: String,          // Properti mutable (bahan bisa diganti?)
    var beratGram: Int         // Properti mutable
) {
    // Method / Perilaku
    fun cetakResep() {
        println("--- Resep Kue $nama ---")
        println("Rasa: $rasa")
        println("Berat: $beratGram gram")
        println("Nikmati kue Anda!")
    }

    fun ubahRasa(rasaBaru: String) {
        println("Mengubah rasa dari $rasa menjadi $rasaBaru")
        rasa = rasaBaru
    }

    fun tambahBerat(gramTambah: Int) {
        beratGram += gramTambah
        println("Berat sekarang: $beratGram gram")
    }
}
```

3. Buka kembali `main.kt`, dan tambahkan kode berikut di dalam fungsi `main()` (boleh di bawah kode sebelumnya):

```kotlin
fun main() {
    // ... (kode sebelumnya tetap ada)

    println("\n--- DEMO CLASS KUE ---")
    // Membuat Objek (Instansiasi) - TANPA KEYWORD 'new'
    val kueUltah = Kue("Ultah", "Coklat", 500)
    val kueLebaran = Kue("Nastar", "Nanas", 250)

    // Memanggil method pada objek
    kueUltah.cetakResep()
    kueLebaran.cetakResep()

    // Mengubah properti objek
    kueUltah.ubahRasa("Stroberi")
    kueUltah.tambahBerat(100)

    // Mengakses properti langsung
    println("Nama kue ultah sekarang: ${kueUltah.nama}") // val tidak bisa diubah
    // kueUltah.nama = "Kue Ulang Tahun" // ERROR!
}
```

4. **Jalankan kode**. Output tambahan yang diharapkan:
```text
--- DEMO CLASS KUE ---
--- Resep Kue Ultah ---
Rasa: Coklat
Berat: 500 gram
Nikmati kue Anda!
--- Resep Kue Nastar ---
Rasa: Nanas
Berat: 250 gram
Nikmati kue Anda!
Mengubah rasa dari Coklat menjadi Stroberi
Berat sekarang: 600 gram
Nama kue ultah sekarang: Ultah
```

**Diskusi Terbimbing**:
- Apa perbedaan `val nama` dengan `var rasa` pada class `Kue`?
- Coba buat objek baru dengan nama `kueCoklat` dan isi data sendiri.

---

### Praktikum Terbimbing 3: Implementasi Sistem Data Mahasiswa dengan Logika Predikat
**Tujuan**: Menggabungkan seluruh konsep (properti, method, logika `when`) sesuai studi kasus di materi Sesi 4.

**Langkah-Langkah**:
1. Buat file baru bernama `Mahasiswa.kt`.
2. Tulis kode berikut:

```kotlin
class Mahasiswa(
    val nim: String,
    val nama: String,
    val jurusan: String,
    var ipk: Double
) {
    // Method untuk menampilkan data
    fun tampilkan() {
        println("=================================")
        println("          DATA MAHASISWA          ")
        println("=================================")
        println("NIM      : $nim")
        println("Nama     : $nama")
        println("Jurusan  : $jurusan")
        println("IPK      : %.2f".format(ipk))
        println("Predikat : ${predikat()}")
        println("=================================")
    }

    // Method untuk menentukan predikat (logika sesuai materi)
    fun predikat(): String {
        return when {
            ipk >= 3.5 -> "Cumlaude"
            ipk >= 3.0 -> "Sangat Memuaskan"
            ipk >= 2.5 -> "Memuaskan"
            else -> "Perlu Perbaikan"
        }
    }

    // Method tambahan: simulasi kenaikan IPK
    fun perbaikiNilai(kenaikan: Double) {
        if (kenaikan > 0) {
            ipk += kenaikan
            if (ipk > 4.0) ipk = 4.0 // Maksimal 4.0
            println("IPK $nama diperbaiki menjadi ${String.format("%.2f", ipk)}")
        } else {
            println("Kenaikan harus positif!")
        }
    }
}
```

3. Di `main.kt`, tambahkan kode berikut di bagian bawah fungsi `main()`:

```kotlin
fun main() {
    // ... (kode sebelumnya tetap ada)

    println("\n--- DATA MAHASISWA ---")
    // Membuat 3 objek Mahasiswa (sesuai instruksi materi)
    val mhs1 = Mahasiswa("TI001", "Anisa Rahma", "Teknik Informatika", 3.75)
    val mhs2 = Mahasiswa("TI002", "Budi Pratama", "Teknik Informatika", 2.80)
    val mhs3 = Mahasiswa("TI003", "Citra Dewi", "Sistem Informasi", 3.20)

    // Tampilkan data masing-masing
    mhs1.tampilkan()
    mhs2.tampilkan()
    mhs3.tampilkan()

    // Uji coba method perbaiki nilai
    println("\n--- SIMULASI PERBAIKAN NILAI ---")
    mhs2.perbaikiNilai(0.5) // IPK Budi naik 0.5 -> 3.30
    mhs2.tampilkan() // Predikat berubah jadi "Sangat Memuaskan"
}
```

4. **Jalankan kode**. Output yang diharapkan (perhatikan predikat):

```text
--- DATA MAHASISWA ---
=================================
          DATA MAHASISWA
=================================
NIM      : TI001
Nama     : Anisa Rahma
Jurusan  : Teknik Informatika
IPK      : 3.75
Predikat : Cumlaude
=================================
=================================
          DATA MAHASISWA
=================================
NIM      : TI002
Nama     : Budi Pratama
Jurusan  : Teknik Informatika
IPK      : 2.80
Predikat : Memuaskan
=================================
=================================
          DATA MAHASISWA
=================================
NIM      : TI003
Nama     : Citra Dewi
Jurusan  : Sistem Informasi
IPK      : 3.20
Predikat : Sangat Memuaskan
=================================

--- SIMULASI PERBAIKAN NILAI ---
IPK Budi Pratama diperbaiki menjadi 3.30
=================================
          DATA MAHASISWA
=================================
NIM      : TI002
Nama     : Budi Pratama
Jurusan  : Teknik Informatika
IPK      : 3.30
Predikat : Sangat Memuaskan
=================================
```

**Diskusi Terbimbing**:
- Apa fungsi `String.format("%.2f", ipk)` dan mengapa kita menggunakannya?
- Jika IPK diisi 4.5, bagaimana sistem menanganinya? (Petunjuk: lihat fungsi `perbaikiNilai` yang membatasi maksimal 4.0, tetapi konstruktor belum dilindungi. Diskusikan solusi menggunakan `init` block).

---

## BAGIAN II: PRAKTIKUM MANDIRI (5 Sesi)

*Instruksi: Kerjakan soal-soal berikut secara individu di rumah atau di laboratorium. Kumpulkan dalam bentuk file `.kt` (bisa digabung dalam satu project atau per file terpisah). Pastikan kode bebas dari error dan berjalan dengan sempurna.*

---

### Soal Mandiri 1: Sistem Peminjaman Buku Sederhana
**Tema**: Class `Buku` dengan properti `judul` (val), `pengarang` (val), dan `tahunTerbit` (var). Buat method `infoBuku()` yang menampilkan semua data dengan format rapi. Di `main()`, buat **minimal 3 objek** buku dengan data berbeda (misal: buku fiksi, non-fiksi, dan komik). Tampilkan info semua buku.

**Kerangka Kode Minimal**:
```kotlin
class Buku(val judul: String, val pengarang: String, var tahunTerbit: Int) {
    fun infoBuku() {
        // TODO: Lengkapi
    }
}

fun main() {
    // TODO: Buat objek dan panggil method
}
```

**Kriteria Penilaian**:
- [ ] Deklarasi class tepat dengan properti yang sesuai (val/var).
- [ ] Method `infoBuku` berjalan dengan output yang rapi.
- [ ] Minimal 3 objek diinstansiasi tanpa `new`.
- [ ] Output menunjukkan semua data buku.

---

### Soal Mandiri 2: Perhitungan Lingkaran (Luas & Keliling)
**Tema**: Class `Lingkaran` memiliki properti `jariJari` (Double, bisa diubah via `var`). Buat method `hitungLuas()` dan `hitungKeliling()` yang mengembalikan nilai Double (gunakan `Math.PI`). Di `main()`, buat **2 objek** dengan jari-jari 7.0 dan 14.0. Tampilkan luas dan keliling masing-masing dengan 2 angka di belakang koma.

**Hint**: Gunakan `String.format("%.2f", hasil)`.

**Kerangka Kode**:
```kotlin
class Lingkaran(var jariJari: Double) {
    fun hitungLuas(): Double {
        // TODO: Rumus PI * r * r
    }
    fun hitungKeliling(): Double {
        // TODO: Rumus 2 * PI * r
    }
}
```

---

### Soal Mandiri 3: Manajemen Gaji Karyawan
**Tema**: Buat class `Karyawan` dengan properti `nama` (val) dan `gajiPokok` (var, Double). Tambahkan method:
- `tampilkanGaji()` → mencetak "Nama: X, Gaji: Rp Y".
- `naikGaji(persen: Double)` → menambah gaji pokok sebesar persen (%) yang diberikan (misal: naikGaji(10.0) berarti gaji += 10%).

Di `main()`, buat 1 objek karyawan dengan gaji 5.000.000. Tampilkan gaji awal, naikkan gaji sebesar 15%, lalu tampilkan gaji akhir.

**Catatan**: Format Rupiah bisa menggunakan `String.format("Rp %,d", gajiPokok.toInt())`.

---

### Soal Mandiri 4: Persegi Panjang (Interaksi Properti)
**Tema**: Class `PersegiPanjang` dengan properti `panjang` dan `lebar` (keduanya `var` Double). Buat method:
- `hitungLuas()` → mengembalikan luas.
- `ubahUkuran(panjangBaru: Double, lebarBaru: Double)` → mengubah panjang dan lebar objek.

Di `main()`:
1. Buat objek dengan panjang 10.0 dan lebar 5.0.
2. Tampilkan luas awal.
3. Panggil method `ubahUkuran(20.0, 10.0)`.
4. Tampilkan luas baru.

**Tambahan Eksplorasi**: Tambahkan method `isSquare()` yang mengembalikan Boolean (true jika panjang == lebar). Di `main()`, cek apakah persegi panjang tersebut berbentuk persegi.

---

### Soal Mandiri 5: Data Mahasiswa Interaktif (Input User)
**Tema**: Modifikasi class `Mahasiswa` dari materi (Sesi 4) agar dapat menerima input dari pengguna menggunakan fungsi `readln()`.

**Spesifikasi**:
1. Minta user mengisi data `NIM`, `Nama`, `Jurusan`, dan `IPK` melalui console.
2. Buat objek `Mahasiswa` dari data yang diinput.
3. Tampilkan data mahasiswa beserta predikatnya (gunakan method `tampilkan()`).
4. **Bonus (Nilai Tambah)**: Buat perulangan `while` agar user bisa memasukkan data untuk beberapa mahasiswa (misal: 3 kali), lalu tampilkan semua data di akhir program.

**Contoh Interaksi (Minimal)**:
```text
Masukkan NIM: TI999
Masukkan Nama: Siti Aisyah
Masukkan Jurusan: Teknik Komputer
Masukkan IPK: 3.45
--- Output ---
=================================
          DATA MAHASISWA
=================================
NIM      : TI999
Nama     : Siti Aisyah
Jurusan  : Teknik Komputer
IPK      : 3.45
Predikat : Sangat Memuaskan
=================================
```

**Peringatan**: Fungsi `readln()` tersedia di Kotlin 1.6+. Jika menggunakan versi lebih rendah, gunakan `readLine()!!`.

---

## BAGIAN III: RUBRIK PENILAIAN PRAKTIKUM MANDIRI

| **Kriteria** | **Bobot** | **Excellent (100%)** | **Good (75%)** | **Fair (50%)** | **Poor (25%)** |
| :--- | :--- | :--- | :--- | :--- | :--- |
| **Kebenaran Sintaks & Logika** | 40% | Tidak ada error, semua method berfungsi sesuai spesifikasi. | Ada 1-2 error kecil (minor) tapi program tetap jalan. | Ada error logika pada 1 method. | Banyak error, program tidak berjalan. |
| **Penggunaan Konsep OOP (Class, Properti, Method)** | 30% | Class, properti (var/val), dan method dideklarasi dengan tepat dan efisien. | Ada kesalahan kecil dalam pemilihan var/val. | Method tidak lengkap atau akses properti salah. | Tidak menggunakan class atau OOP sama sekali. |
| **Kreativitas & Eksplorasi (Bonus)** | 15% | Menambahkan fitur tambahan (seperti input loop, validasi, atau method ekstra). | Menambahkan fitur sederhana. | Hanya mengerjakan minimal requirement. | Tidak ada tambahan sama sekali. |
| **Kerapian Kode & Output** | 15% | Kode di-indent rapi, output terformat dengan jelas. | Kode rapi, output kurang terformat. | Kode berantakan, output sulit dibaca. | Kode tidak terbaca. |

---

## BAGIAN IV: PANDUAN SUBMISI (Pengumpulan Tugas)

1. **Format Pengumpulan**:
   - Gabungkan seluruh jawaban (Praktikum Mandiri 1-5) ke dalam **SATU Project IntelliJ**.
   - Beri nama project: `Praktikum_PBO_Pertemuan1_NIM_NAMA`.
   - Pastikan setiap soal mandiri dibuat dalam file terpisah, misal:
     - `Mandiri1_Buku.kt`
     - `Mandiri2_Lingkaran.kt`
     - `Mandiri3_Karyawan.kt`
     - `Mandiri4_PersegiPanjang.kt`
     - `Mandiri5_MahasiswaInteraktif.kt`
   - Jika menggunakan `main()` di setiap file, Anda bisa menjalankan satu per satu. Atau, untuk kemudahan, panggil semua fungsi `main` yang ada (tapi di Kotlin, setiap file boleh punya `main` sendiri, IntelliJ akan mendeteksinya).

2. **Cara Mengumpulkan**:
   - **Zip** folder project tersebut (bukan hanya file `.kt`-nya, tapi seluruh folder project).
   - Upload : https://forms.gle/ZNtULh8zE2VpA93a7.

3. **Hal yang Perlu Diperhatikan**:
   - Pastikan tidak ada error (garis merah) di IntelliJ sebelum di-zip.
   - Sertakan screenshot output di dalam dokumen terpisah (doc/docx).

---

**Selamat Mengerjakan! Praktikkan setiap hari, karena *"Ilmu tanpa praktik bagaikan pohon tanpa buah."*** 🚀
