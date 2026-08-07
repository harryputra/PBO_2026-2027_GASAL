# RENCANA PEMBELAJARAN SEMESTER (RPS)
## PERTEMUAN KE-1 — RENCANA PELAKSANAAN PEMBELAJARAN (RPP)
### PEMROGRAMAN BERORIENTASI OBJEK (OBJECT-ORIENTED PROGRAMMING)

---

## A. IDENTITAS PERTEMUAN

| **Komponen** | **Keterangan** |
|---|---|
| **Pertemuan Ke-** | 1 |
| **Topik** | Pengenalan OOP & Setup Environment |
| **Durasi** | 8 Jam Praktik (480 menit) |
| **Hari/Tanggal** | [Disesuaikan] |
| **Ruang** | Laboratorium Komputer |
| **Dosen** | [Nama Dosen] |
| **Capaian Pembelajaran** | Mahasiswa memahami RPS, kontrak kuliah, konsep dasar OOP (kelas & objek, atribut & metode), serta mampu menginstal dan mengkonfigurasi lingkungan pengembangan Kotlin/Java, dan membuat program sederhana pertama |

---

## B. CAPAIAN PEMBELAJARAN PERTEMUAN (CPP)

Setelah mengikuti pertemuan ke-1 ini, mahasiswa mampu:

1. **CPP 1.1:** Menjelaskan RPS, kontrak perkuliahan, sistem penilaian, dan aturan perkuliahan.
2. **CPP 1.2:** Menjelaskan paradigma pemrograman berorientasi objek dan perbedaannya dengan paradigma prosedural.
3. **CPP 1.3:** Menjelaskan alasan pemilihan Kotlin sebagai bahasa pengantar OOP dan kaitannya dengan Mobile Programming.
4. **CPP 1.4:** Menginstal dan mengkonfigurasi IntelliJ IDEA (atau Android Studio) serta JDK untuk pengembangan Kotlin.
5. **CPP 1.5:** Membuat project Kotlin pertama dan menjalankan program "Hello World".
6. **CPP 1.6:** Mendefinisikan kelas sederhana dengan atribut dan metode dalam Kotlin.
7. **CPP 1.7:** Membuat objek dari kelas dan mengakses atribut serta memanggil metode.

---

## C. MATERI POKOK

### 1. Pendahuluan dan Kontrak Perkuliahan (Sesi 1)
- RPS dan kontrak perkuliahan
- Sistem penilaian dan kehadiran
- Pentingnya OOP dalam kurikulum D4 Teknologi Rekayasa Informatika Industri

### 2. Pengenalan Pemrograman Berorientasi Objek (Sesi 1)
- Definisi OOP/PBO
- Perbedaan OOP vs Pemrograman Prosedural
- Konsep dasar: Kelas (Class), Objek (Object), Atribut (Attribute/Property), Metode (Method/Function)
- Analogi dunia nyata: kelas = blueprint/cetakan, objek = realisasi dari cetakan

### 3. Mengapa Kotlin? (Sesi 1)
- Sejarah dan latar belakang Kotlin (dikembangkan oleh JetBrains, dirilis 2016)
- Kotlin sebagai bahasa resmi Android (Kotlin-first sejak Google I/O 2019)
- Keunggulan Kotlin:
  - **Interoperabilitas dengan Java 100%** — dapat memanggil kode Java dari Kotlin dan sebaliknya
  - **Sintaks lebih ringkas** — kode lebih sedikit hingga 30% dibanding Java
  - **Null Safety** — tipe sistem mencegah NullPointerException (NPE)
  - **Produktivitas lebih tinggi** — aplikasi berbasis Kotlin 20% lebih kecil kemungkinannya untuk crash
  - **Mudah dipelajari** — terutama bagi yang sudah mengenal Java
- Kaitan dengan Mobile Programming: semester depan mahasiswa akan belajar Mobile Programming menggunakan Kotlin, sehingga penguasaan OOP dengan Kotlin menjadi fondasi yang kuat

### 4. Persiapan Lingkungan Pengembangan (Sesi 2)
- **JDK (Java Development Kit)** — Kotlin berjalan di atas JVM (Java Virtual Machine), sehingga JDK wajib diinstal
- **IntelliJ IDEA** — IDE utama untuk pengembangan Kotlin (Community Edition gratis)
  - Alternatif: Android Studio (untuk yang sudah familiar dengan pengembangan Android)
- **Kotlin Plugin** — sudah ter-bundle di IntelliJ IDEA dan aktif secara default
- Langkah-langkah instalasi:
  1. Download dan install JDK (Oracle OpenJDK atau Adoptium)
  2. Download dan install IntelliJ IDEA Community Edition
  3. Buka IntelliJ IDEA dan verifikasi Kotlin Plugin sudah aktif

### 5. Membuat Project Kotlin Pertama (Sesi 2)
- Langkah-langkah membuat project di IntelliJ IDEA:
  1. Pada Welcome Screen, klik **New Project**
  2. Pada panel kiri, pilih **Kotlin**
  3. Beri nama project (contoh: `PBO-Project1`)
  4. Pilih **IntelliJ** sebagai build system
  5. Pilih JDK yang sudah diinstal
  6. Centang **Add sample code** untuk membuat file dengan contoh Hello World
  7. Klik **Create**
- Struktur project Kotlin
- File `main.kt` dan fungsi `main()`

### 6. Hello World di Kotlin (Sesi 2)
- Sintaks dasar Kotlin:
  ```kotlin
  fun main() {
      println("Hello, World!")
  }
  ```
- Perbedaan dengan Java:
  - Tidak perlu class wrapper untuk fungsi main
  - Menggunakan keyword `fun` untuk mendeklarasikan fungsi
  - Titik koma (;) bersifat opsional

### 7. Konsep Dasar Kelas dan Objek di Kotlin (Sesi 3)
- **Deklarasi kelas** menggunakan keyword `class`
  ```kotlin
  class Mahasiswa
  ```
- **Atribut/Properti** — data atau variabel yang menggambarkan karakteristik objek
  ```kotlin
  class Mahasiswa(val nim: String, val nama: String, var umur: Int)
  ```
  - `val` = read-only (tidak bisa diubah setelah diinisialisasi)
  - `var` = mutable (bisa diubah)
- **Metode/Fungsi** — perilaku atau aksi yang dapat dilakukan oleh objek
  ```kotlin
  class Mahasiswa(val nim: String, val nama: String, var umur: Int) {
      fun tampilkan() {
          println("NIM: $nim, Nama: $nama, Umur: $umur")
      }

      fun bertambahUmur() {
          umur++
      }
  }
  ```
- **Membuat Objek** (Instansiasi) — di Kotlin tidak perlu keyword `new`
  ```kotlin
  val mhs = Mahasiswa("12345", "Budi Santoso", 20)
  mhs.tampilkan()
  mhs.bertambahUmur()
  println("Umur sekarang: ${mhs.umur}")
  ```

### 8. Analogi Dunia Nyata (Sesi 3)
- **Kelas** = cetakan kue (blueprint) — mendefinisikan bentuk, bahan, dan cara membuat
- **Objek** = kue yang sudah jadi — realisasi dari cetakan
- **Atribut** = bahan-bahan kue (tepung, gula, telur)
- **Metode** = cara membuat kue (mencampur, mengocok, memanggang)

### 9. Latihan Mandiri: Sistem Data Mahasiswa Sederhana (Sesi 4)

**Studi Kasus:** Buatlah program sederhana untuk mengelola data mahasiswa dengan ketentuan:
- Kelas `Mahasiswa` dengan atribut: NIM (String), Nama (String), Jurusan (String), dan IPK (Double)
- Metode:
  - `tampilkan()` → menampilkan semua data mahasiswa
  - `predikat()` → mengembalikan predikat kelulusan berdasarkan IPK:
    - IPK ≥ 3.5 → "Cumlaude"
    - IPK ≥ 3.0 → "Sangat Memuaskan"
    - IPK ≥ 2.5 → "Memuaskan"
    - IPK < 2.5 → "Perlu Perbaikan"
- Di fungsi `main()`, buat minimal 3 objek mahasiswa dengan data berbeda, tampilkan data dan predikat masing-masing

---

## D. RINCIAN KEGIATAN PEMBELAJARAN (8 JAM)

### Sesi 1: Pengantar & Teori Konsep (2 Jam — 120 menit)

| **Waktu** | **Kegiatan** | **Detail** | **Metode** |
|---|---|---|---|
| **0-15'** | Pembukaan | • Dosen membuka perkuliahan dengan salam dan doa<br>• Perkenalan dosen dan mahasiswa<br>• Ice breaking singkat | Ceramah interaktif |
| **15-45'** | RPS & Kontrak Kuliah | • Penjelasan RPS secara menyeluruh<br>• Kontrak perkuliahan (kehadiran minimal 75%, tugas, UAS)<br>• Sistem penilaian (Tugas 35%, Proyek 35%, Presentasi 15%, Keaktifan 15%)<br>• Aturan praktikum dan tata tertib lab<br>• Q&A | Ceramah, Diskusi |
| **45-90'** | Pengenalan OOP | • Definisi Pemrograman Berorientasi Objek<br>• Sejarah dan evolusi paradigma pemrograman<br>• Perbandingan OOP vs Prosedural (contoh kasus)<br>• Konsep Class, Object, Attribute, Method dengan analogi<br>• Contoh sederhana dalam kehidupan sehari-hari | Ceramah, Tanya jawab, Analogi |
| **90-120'** | Mengapa Kotlin? | • Sejarah Kotlin (JetBrains, 2011-2016)<br>• Kotlin sebagai bahasa Android resmi<br>• Keunggulan Kotlin: interop dengan Java 100%, sintaks ringkas, null safety, produktivitas<br>• Kaitan dengan mata kuliah Mobile Programming semester depan<br>• Demonstrasi singkat perbandingan kode Java vs Kotlin | Ceramah, Demonstrasi, Diskusi |

---

### Sesi 2: Demonstrasi & Live Coding (2 Jam — 120 menit)

| **Waktu** | **Kegiatan** | **Detail** | **Metode** |
|---|---|---|---|
| **0-30'** | Instalasi Environment | • Dosen mendemonstrasikan instalasi JDK<br>• Demonstrasi instalasi IntelliJ IDEA Community Edition<br>• Verifikasi Kotlin Plugin<br>• Mahasiswa mengikuti langkah demi langkah | Demonstrasi, Praktik terbimbing |
| **30-60'** | Membuat Project Pertama | • Demonstrasi pembuatan project Kotlin di IntelliJ IDEA:<br>  - New Project → pilih Kotlin<br>  - Setting nama project dan lokasi<br>  - Pilih IntelliJ build system<br>  - Pilih JDK<br>  - Centang Add sample code<br>• Penjelasan struktur project Kotlin<br>• Mahasiswa membuat project masing-masing | Demonstrasi, Praktik terbimbing |
| **60-90'** | Hello World di Kotlin | • Demonstrasi penulisan kode Hello World:<br>  ```kotlin<br>  fun main() {<br>      println("Hello, World!")<br>  }<br>  ```<br>• Penjelasan sintaks: `fun`, `main()`, `println`<br>• Perbedaan dengan Java (tanpa class wrapper, tanpa semicolon wajib)<br>• Running program (klik tombol Run)<br>• Mahasiswa menulis dan menjalankan Hello World | Demonstrasi, Praktik mandiri |
| **90-120'** | Eksplorasi Dasar Kotlin | • Variabel dengan `val` dan `var`<br>  ```kotlin<br>  val nama = "Andi"  // tidak bisa diubah<br>  var umur = 20      // bisa diubah<br>  ```<br>• Type inference (tipe data otomatis)<br>• Tipe data dasar: String, Int, Double, Boolean<br>• Null safety: perbedaan `String` vs `String?`<br>• Mahasiswa bereksperimen dengan variabel dan tipe data | Demonstrasi, Eksplorasi, Praktik |

---

### Sesi 3: Praktik Mandiri/Berkelompok (2 Jam — 120 menit)

| **Waktu** | **Kegiatan** | **Detail** | **Metode** |
|---|---|---|---|
| **0-30'** | Teori Kelas & Objek | • Penjelasan konsep kelas dan objek di Kotlin<br>• Cara mendeklarasikan kelas dengan properti<br>• Perbedaan `val` dan `var` dalam properti kelas<br>• Cara membuat objek (tanpa `new`)<br>• Contoh kode:<br>  ```kotlin<br>  class Mahasiswa(val nim: String, val nama: String)<br>  val mhs = Mahasiswa("123", "Budi")<br>  println(mhs.nama)<br>  ``` | Ceramah, Demonstrasi |
| **30-60'** | Praktik Membuat Kelas | • Mahasiswa membuat kelas `Mahasiswa` dengan atribut NIM, Nama, Jurusan<br>• Menambahkan metode `tampilkan()` untuk menampilkan data<br>• Menambahkan metode `ubahJurusan(jurusanBaru: String)`<br>• Dosen berkeliling memberikan asistensi | Praktik mandiri, Asistensi |
| **60-90'** | Praktik Membuat Objek | • Mahasiswa membuat minimal 3 objek dari kelas `Mahasiswa`<br>• Memanggil metode `tampilkan()` untuk setiap objek<br>• Mengubah jurusan salah satu objek dan menampilkan ulang<br>• Eksperimen dengan properti `val` vs `var` | Praktik mandiri, Eksplorasi |
| **90-120'** | Diskusi & Troubleshooting | • Diskusi kelompok kecil (3-4 orang) tentang kendala yang dihadapi<br>• Dosen membantu troubleshooting error yang umum terjadi<br>• Review beberapa kode mahasiswa yang berhasil<br>• Tips dan trik penggunaan IntelliJ IDEA | Diskusi kelompok, Asistensi |

---

### Sesi 4: Review & Penyelesaian Tugas (2 Jam — 120 menit)

| **Waktu** | **Kegiatan** | **Detail** | **Metode** |
|---|---|---|---|
| **0-30'** | Review Materi | • Dosen mereview seluruh materi pertemuan 1<br>• Menjawab pertanyaan mahasiswa<br>• Merangkum poin-poin penting:<br>  - Konsep OOP: Class, Object, Attribute, Method<br>  - Setup environment: JDK + IntelliJ IDEA<br>  - Sintaks dasar Kotlin: `fun`, `main`, `val`, `var`<br>  - Deklarasi kelas dan pembuatan objek | Review, Tanya jawab |
| **30-90'** | Pengerjaan Tugas 1 | • Mahasiswa mengerjakan Tugas 1 secara mandiri<br>• **Tugas 1:** Sistem Data Mahasiswa Sederhana (lihat detail di bagian C.9)<br>• Dosen berkeliling memberikan bimbingan intensif<br>• Mahasiswa dapat bertanya jika mengalami kendala | Praktik mandiri, Asistensi intensif |
| **90-110'** | Pengumpulan & Presentasi Singkat | • Mahasiswa mengumpulkan Tugas 1 (file .kt)<br>• 2-3 mahasiswa diminta mempresentasikan kodenya secara singkat<br>• Dosen memberikan feedback konstruktif | Presentasi, Feedback |
| **110-120'** | Penutupan | • Dosen merangkum pencapaian pertemuan 1<br>• Preview materi pertemuan 2 (Enkapsulasi)<br>• Memberikan tugas membaca modul pertemuan 2<br>• Menutup perkuliahan dengan doa dan salam | Ceramah |

---

## E. MEDIA DAN ALAT PEMBELAJARAN

| **Media** | **Keterangan** |
|---|---|
| **Laptop/PC** | Setiap mahasiswa menggunakan laptop/PC masing-masing atau PC laboratorium |
| **IntelliJ IDEA** | IDE utama untuk pengembangan Kotlin (Community Edition) |
| **JDK** | Java Development Kit (versi 11 atau 17) |
| **Proyektor/LCD** | Untuk presentasi dan demonstrasi dosen |
| **Whiteboard** | Untuk menjelaskan konsep dan analogi |
| **Modul Praktikum** | Modul cetak/digital yang berisi panduan langkah demi langkah |
| **E-Learning** | Platform untuk pengumpulan tugas dan materi tambahan |

---

## F. PENILAIAN PERTEMUAN 1

| **Komponen** | **Bobot** | **Indikator** | **Teknik** |
|---|---|---|---|
| **Keaktifan Sesi 1** | 15% dari total keaktifan | • Kehadiran tepat waktu<br>• Partisipasi dalam diskusi dan tanya jawab<br>• Keterlibatan dalam kegiatan praktik | Observasi |
| **Tugas 1** | 100% dari nilai tugas 1 | • Kelas `Mahasiswa` didefinisikan dengan benar<br>• Atribut menggunakan tipe data yang tepat<br>• Metode `tampilkan()` dan `predikat()` berfungsi dengan benar<br>• Minimal 3 objek dibuat dan ditampilkan<br>• Kode bersih, terstruktur, dan bebas error | Penilaian kode |
| **Kemampuan Setup** | Checklist | • JDK terinstal dengan benar<br>• IntelliJ IDEA terinstal<br>• Project Kotlin berhasil dibuat<br>• Program Hello World berjalan | Observasi |

---

## G. REFERENSI PERTEMUAN 1

### Referensi Utama:
1. **Kotlin Official Documentation** – *Getting Started with Kotlin* (https://kotlinlang.org/docs/home.html)
2. **IntelliJ IDEA Documentation** – *Get started with Kotlin* (https://www.jetbrains.com/help/idea/get-started-with-kotlin.html)
3. **Android Developers** – *Learn the Kotlin programming language* (https://developer.android.google.cn/kotlin/learn)

### Referensi Pendukung:
4. **Kotlin for Android** – *Kotlin官方文档* (https://kotlinlang.org/docs/android-overview.html)
5. **Modul Praktikum Pemrograman Berorientasi Objek** – Modul internal prodi
6. **Video Tutorial** – *Kotlin Tutorial for Beginners* (YouTube)

---

## H. LAMPIRAN

### Lampiran 1: Kode Solusi Tugas 1 (Contoh)

```kotlin
// File: Mahasiswa.kt

/**
 * Kelas Mahasiswa merepresentasikan data mahasiswa
 * @param nim Nomor Induk Mahasiswa (String)
 * @param nama Nama lengkap mahasiswa (String)
 * @param jurusan Jurusan mahasiswa (String)
 * @param ipk Indeks Prestasi Kumulatif (Double)
 */
class Mahasiswa(
    val nim: String,
    val nama: String,
    var jurusan: String,
    var ipk: Double
) {
    /**
     * Menampilkan seluruh data mahasiswa
     */
    fun tampilkan() {
        println("=" .repeat(40))
        println("DATA MAHASISWA")
        println("=" .repeat(40))
        println("NIM     : $nim")
        println("Nama    : $nama")
        println("Jurusan : $jurusan")
        println("IPK     : $ipk")
        println("Predikat: ${predikat()}")
        println("=" .repeat(40))
    }

    /**
     * Menentukan predikat kelulusan berdasarkan IPK
     * @return String predikat kelulusan
     */
    fun predikat(): String {
        return when {
            ipk >= 3.5 -> "Cumlaude"
            ipk >= 3.0 -> "Sangat Memuaskan"
            ipk >= 2.5 -> "Memuaskan"
            else -> "Perlu Perbaikan"
        }
    }
}

/**
 * Fungsi utama program
 */
fun main() {
    // Membuat 3 objek mahasiswa
    val mhs1 = Mahasiswa("TI2024001", "Budi Santoso", "Teknik Informatika", 3.75)
    val mhs2 = Mahasiswa("TI2024002", "Siti Rahayu", "Sistem Informasi", 3.20)
    val mhs3 = Mahasiswa("TI2024003", "Ahmad Fauzi", "Teknik Komputer", 2.80)

    // Menampilkan data semua mahasiswa
    mhs1.tampilkan()
    mhs2.tampilkan()
    mhs3.tampilkan()

    // Demonstrasi perubahan data
    println("\n--- DEMONSTRASI PERUBAHAN DATA ---")
    println("Sebelum: ${mhs1.nama} - Jurusan: ${mhs1.jurusan}")
    mhs1.jurusan = "Teknik Informatika (Mobile)"
    println("Sesudah: ${mhs1.nama} - Jurusan: ${mhs1.jurusan}")

    // Demonstrasi perubahan IPK
    println("\n--- DEMONSTRASI PERUBAHAN IPK ---")
    println("IPK ${mhs2.nama}: ${mhs2.ipk} -> Predikat: ${mhs2.predikat()}")
    mhs2.ipk = 3.55
    println("IPK ${mhs2.nama} (baru): ${mhs2.ipk} -> Predikat: ${mhs2.predikat()}")
}
```

### Lampiran 2: Checklist Persiapan Praktikum

| **No** | **Item** | **Status** | **Keterangan** |
|---|---|---|---|
| 1 | JDK terinstal | ☐ | Versi 11 atau 17 |
| 2 | JAVA_HOME terkonfigurasi | ☐ | |
| 3 | IntelliJ IDEA terinstal | ☐ | Community Edition |
| 4 | Kotlin Plugin aktif | ☐ | Cek di Settings → Plugins |
| 5 | Project Kotlin berhasil dibuat | ☐ | |
| 6 | Hello World berjalan | ☐ | |

### Lampiran 3: Panduan Troubleshooting Umum

| **Masalah** | **Solusi** |
|---|---|
| **Kotlin Plugin tidak aktif** | Buka File → Settings → Plugins, cari "Kotlin", aktifkan |
| **JDK tidak terdeteksi** | File → Project Structure → SDK → pilih atau tambahkan JDK |
| **Error "Unresolved reference"** | Pastikan tidak ada typo pada nama fungsi/variabel, coba Invalidate Caches |
| **Program tidak mau run** | Pastikan ada fungsi `main()` yang valid, cek Run Configuration |
| **Kotlin tidak dikenali** | Pastikan project dibuat sebagai Kotlin project, bukan Java project |

---

## I. CATATAN DOSEN

1. **Persiapan sebelum perkuliahan:**
   - Pastikan semua komputer laboratorium telah terinstal JDK dan IntelliJ IDEA
   - Siapkan modul praktikum cetak atau digital
   - Siapkan contoh kode solusi untuk referensi

2. **Tips pelaksanaan:**
   - Berikan waktu yang cukup untuk proses instalasi (bisa memakan waktu lama tergantung koneksi internet)
   - Sediakan panduan instalasi langkah demi langkah yang jelas
   - Untuk mahasiswa yang kesulitan, sediakan pairing dengan mahasiswa yang sudah berhasil
   - Tekankan pentingnya OOP sebagai fondasi untuk mata kuliah Mobile Programming

3. **Tindak lanjut:**
   - Kumpulkan semua Tugas 1 melalui platform e-learning
   - Berikan feedback tertulis untuk setiap tugas
   - Identifikasi mahasiswa yang masih kesulitan untuk diberikan pendampingan tambahan

---

**Disusun oleh,**
[Nama Dosen Pengampu]
Dosen Program Studi D4 Teknologi Rekayasa Informatika Industri
