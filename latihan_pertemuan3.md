# LATIHAN PRAKTIKUM PERTEMUAN 3

## PEWARISAN (INHERITANCE) DENGAN KOTLIN

### "Membangun Hierarki Kelas yang Kuat dan Reusable"

---

## PETUNJUK PRAKTIKUM

| **Komponen** | **Keterangan** |
| --- | --- |
| **Topik** | Pewarisan (Inheritance): `open`, `override`, `super`, Constructor Inheritance |
| **Durasi** | 8 Jam Praktik (480 menit) |
| **Tools** | IntelliJ IDEA / Kotlin Playground |
| **Aturan** | • Kerjakan latihan secara berurutan dari Latihan 1 hingga Latihan 6<br>• Setiap latihan memiliki tingkat kesulitan yang meningkat<br>• Kumpulkan semua file `.kt` ke dalam folder `Pertemuan3_NamaAnda`<br>• Berikan komentar pada kode Anda |

---

## LATIHAN 1: DASAR PEWARISAN & KEYWORD `open`

**Estimasi Waktu: 30 Menit | Tingkat: Dasar**

### Tujuan

Memahami cara membuat kelas yang bisa diwarisi dan mengimplementasikan pewarisan dasar.

### Instruksi

**1.1** Buatlah kelas induk `Kendaraan` dengan spesifikasi berikut:

```kotlin
// Lengkapi kode di bawah ini
open class Kendaraan(
    val merek: String,
    val model: String,
    val tahun: Int
) {
    // Buat metode open bernama "info()" yang menampilkan:
    // "Kendaraan: [merek] [model] ([tahun])"

    // Buat metode final bernama "start()" yang menampilkan:
    // "[merek] [model] dinyalakan"
}
```

**1.2** Buatlah dua kelas anak yang mewarisi `Kendaraan`:

| **Kelas** | **Properti Tambahan** | **Override** |
| --- | --- | --- |
| `Mobil` | `jumlahPintu: Int`, `jenisBahanBakar: String` | `info()` menampilkan info mobil lengkap |
| `Motor` | `kapasitasMesin: Int`, `jenis: String` | `info()` menampilkan info motor lengkap |

**1.3** Buat fungsi `main()` yang:

- Membuat 1 objek `Mobil` dan 1 objek `Motor`
- Memanggil `info()` dan `start()` pada masing-masing objek

### Output yang Diharapkan

```
=== KENDARAAN ===
Mobil: Toyota Avanza (2023) - 4 Pintu, Bensin
Toyota Avanza dinyalakan

Motor: Honda Beat (2022) - 125cc, Matic
Honda Beat dinyalakan
```

### Pertanyaan Refleksi

1. Apa yang terjadi jika kelas `Kendaraan` tidak ditandai `open`? Coba dan jelaskan!
2. Apa yang terjadi jika metode `info()` tidak ditandai `open`? Coba dan jelaskan!
3. Mengapa metode `start()` tidak bisa di-override?

---

## LATIHAN 2: OVERRIDING METODE & PROPERTI

**Estimasi Waktu: 45 Menit | Tingkat: Dasar-Menengah**

### Tujuan

Memahami overriding metode dan properti, serta penggunaan keyword `super`.

### Instruksi

**2.1** Buatlah hierarki kelas `Hewan` dengan spesifikasi:

```kotlin
open class Hewan(
    open val nama: String,
    open val umur: Int
) {
    open val jenis: String = "Hewan"

    open fun suara() {
        println("$nama bersuara...")
    }

    open fun info() {
        println("Nama: $nama")
        println("Umur: $umur tahun")
        println("Jenis: $jenis")
    }
}
```

**2.2** Buatlah 3 subclass dengan spesifikasi:

| **Subclass** | **Override Properti** | **Override Metode** |
| --- | --- | --- |
| `Kucing` | `jenis = "Kucing"` | `suara()` → "Meong! Meong!" |
| `Anjing` | `jenis = "Anjing"` | `suara()` → "Guk! Guk!" |
| `Sapi` | `jenis = "Sapi"` | `suara()` → "Mooo!" |

**2.3** Pada setiap subclass, override `info()` untuk memanggil `super.info()` terlebih dahulu, lalu tambahkan baris kosong.

**2.4** Buat fungsi `main()` yang membuat array/list berisi 3 hewan dan menampilkan info serta suara masing-masing.

### Output yang Diharapkan

```
=== INFO HEWAN ===
Nama: Milo
Umur: 3 tahun
Jenis: Kucing

Nama: Rex
Umur: 5 tahun
Jenis: Anjing

Nama: Sapi
Umur: 4 tahun
Jenis: Sapi

=== SUARA HEWAN ===
Meong! Meong!
Guk! Guk!
Mooo!
```

### Tantangan Tambahan

- Tambahkan subclass `KucingAnggora` yang mewarisi `Kucing`
- Override `suara()` di `KucingAnggora` dan panggil `super.suara()` terlebih dahulu
- Gunakan `final override` di `Kucing` untuk `suara()` dan buktikan bahwa `KucingAnggora` tidak bisa meng-override-nya (berikan komentar sebagai bukti)

---

## LATIHAN 3: CONSTRUCTOR DALAM INHERITANCE

**Estimasi Waktu: 45 Menit | Tingkat: Menengah**

### Tujuan

Memahami cara kerja primary dan secondary constructor dalam hierarki pewarisan.

### Instruksi

**3.1** Buatlah kelas `Pegawai` dengan primary constructor:

```kotlin
open class Pegawai(
    open val nama: String,
    open val nip: String,
    open val gajiPokok: Double
) {
    init {
        println("📋 Pegawai $nama terdaftar dengan NIP $nip")
    }

    open fun hitungGaji(): Double = gajiPokok

    open fun tampilkanInfo() {
        println("Nama      : $nama")
        println("NIP       : $nip")
        println("Gaji Pokok: Rp $gajiPokok")
        println("Total Gaji: Rp ${hitungGaji()}")
    }
}
```

**3.2** Buatlah subclass `PegawaiTetap` dengan constructor:

```kotlin
class PegawaiTetap(
    nama: String,
    nip: String,
    gajiPokok: Double,
    val tunjangan: Double
) : Pegawai(nama, nip, gajiPokok) {
    // Override hitungGaji() → gajiPokok + tunjangan
    // Override tampilkanInfo() → panggil super, lalu tampilkan tunjangan
}
```

**3.3** Buatlah subclass `PegawaiKontrak` dengan constructor:

```kotlin
class PegawaiKontrak(
    nama: String,
    nip: String,
    gajiPokok: Double,
    val durasiKontrak: Int  // dalam bulan
) : Pegawai(nama, nip, gajiPokok) {
    // Override tampilkanInfo() → panggil super, lalu tampilkan durasi kontrak
}
```

**3.4** Buatlah kelas `Manager` yang mewarisi `PegawaiTetap` dengan tambahan `tunjanganManajemen: Double`. Override `hitungGaji()` untuk menambahkan tunjangan manajemen.

**3.5** Demonstrasikan urutan inisialisasi dengan membuat objek dari setiap kelas dan amati output yang muncul.

### Output yang Diharapkan

```
📋 Pegawai Budi terdaftar dengan NIP P001
📋 Pegawai Siti terdaftar dengan NIP P002
📋 Pegawai Dewi terdaftar dengan NIP P003

=== INFO PEGAWAI TETAP ===
Nama      : Budi
NIP       : P001
Gaji Pokok: Rp 5000000.0
Total Gaji: Rp 6500000.0
Tunjangan : Rp 1500000.0

=== INFO PEGAWAI KONTRAK ===
Nama      : Siti
NIP       : P002
Gaji Pokok: Rp 4500000.0
Total Gaji: Rp 4500000.0
Durasi    : 12 bulan

=== INFO MANAGER ===
Nama      : Dewi
NIP       : P003
Gaji Pokok: Rp 8000000.0
Total Gaji: Rp 13000000.0
Tunjangan : Rp 2000000.0
Tunj. Manajemen: Rp 3000000.0
```

### Pertanyaan Refleksi

1. Mengapa parameter `nama`, `nip`, dan `gajiPokok` di subclass tidak perlu menggunakan `val`/`var`?
2. Apa yang terjadi jika subclass tidak memanggil constructor superclass?
3. Jelaskan urutan inisialisasi yang terjadi saat objek `Manager` dibuat!

---

## LATIHAN 4: PEWARISAN BERTINGKAT (MULTI-LEVEL INHERITANCE)

**Estimasi Waktu: 60 Menit | Tingkat: Menengah**

### Tujuan

Membangun hierarki kelas bertingkat dan memahami rantai pewarisan.

### Instruksi

Buatlah hierarki kelas untuk bentuk geometris (Shapes) dengan 3 level:

```
Level 1: Shape (abstract concept)
    ↓
Level 2: TwoDimensionalShape, ThreeDimensionalShape
    ↓
Level 3: Circle, Rectangle, Triangle, Cube, Sphere
```

**4.1** Buat kelas induk `Shape`:

```kotlin
open class Shape(val name: String) {
    open fun luas(): Double = 0.0
    open fun keliling(): Double = 0.0
    open fun volume(): Double = 0.0

    open fun tampilkanInfo() {
        println("=== $name ===")
        println("Luas     : ${"%.2f".format(luas())}")
        println("Keliling : ${"%.2f".format(keliling())}")
        println("Volume   : ${"%.2f".format(volume())}")
    }
}
```

**4.2** Buat kelas `TwoDimensionalShape` (mewarisi `Shape`):

```kotlin
open class TwoDimensionalShape(name: String) : Shape(name) {
    // Override volume() → return 0.0 (bangun datar tidak punya volume)
}
```

**4.3** Buat kelas `ThreeDimensionalShape` (mewarisi `Shape`):

```kotlin
open class ThreeDimensionalShape(name: String) : Shape(name) {
    // Override keliling() → return 0.0 (bangun ruang tidak punya keliling)
}
```

**4.4** Buat subclass konkret:

| **Kelas** | **Mewarisi** | **Properti** | **Rumus** |
| --- | --- | --- | --- |
| `Circle` | `TwoDimensionalShape` | `jariJari: Double` | Luas = π × r², Keliling = 2 × π × r |
| `Rectangle` | `TwoDimensionalShape` | `panjang: Double`, `lebar: Double` | Luas = p × l, Keliling = 2 × (p + l) |
| `Triangle` | `TwoDimensionalShape` | `alas: Double`, `tinggi: Double`, `sisiA: Double`, `sisiB: Double`, `sisiC: Double` | Luas = 0.5 × a × t, Keliling = a + b + c |
| `Cube` | `ThreeDimensionalShape` | `sisi: Double` | Luas = 6 × s², Volume = s³ |
| `Sphere` | `ThreeDimensionalShape` | `jariJari: Double` | Luas = 4 × π × r², Volume = (4/3) × π × r³ |

**4.5** Buat fungsi `main()` yang:

- Membuat objek dari semua subclass
- Menampilkan info setiap bentuk
- Menghitung total luas semua bentuk 2D
- Menghitung total volume semua bentuk 3D

### Output yang Diharapkan

```
=== Circle ===
Luas     : 78.54
Keliling : 31.42
Volume   : 0.00

=== Rectangle ===
Luas     : 50.00
Keliling : 30.00
Volume   : 0.00

=== Cube ===
Luas     : 96.00
Keliling : 0.00
Volume   : 64.00

Total Luas Bangun 2D: 128.54
Total Volume Bangun 3D: 64.00
```

---

## LATIHAN 5: STUDI KASUS — SISTEM PERPUSTAKAAN

**Estimasi Waktu: 90 Menit | Tingkat: Menengah-Lanjut**

### Tujuan

Mengimplementasikan semua konsep pewarisan dalam studi kasus nyata.

### Instruksi

Bangunlah sistem manajemen perpustakaan dengan hierarki berikut:

```
                    ItemPerpustakaan
                    /              \
            Buku                  Majalah
           /    \                /      \
    BukuFiksi  BukuNonFiksi  MajalahHarian  MajalahMingguan
```

**5.1** Kelas Induk `ItemPerpustakaan`:

| **Komponen** | **Spesifikasi** |
| --- | --- |
| **Properti** | `id: String` (read-only)<br>`judul: String` (read-only)<br>`tahunTerbit: Int` (read-only)<br>`isDipinjam: Boolean` (private setter, default false) |
| **Metode** | `dipinjam(): Boolean` — menandai item dipinjam<br>`dikembalikan(): Boolean` — menandai item dikembalikan<br>`hitungDenda(hariTerlambat: Int): Double` (open) — default: 1000 per hari<br>`tampilkanInfo()` (open) — menampilkan info item |

**5.2** Subclass `Buku` (mewarisi `ItemPerpustakaan`):

| **Komponen** | **Spesifikasi** |
| --- | --- |
| **Properti Tambahan** | `penulis: String`<br>`jumlahHalaman: Int` |
| **Override** | `hitungDenda()` → 2000 per hari<br>`tampilkanInfo()` → menampilkan info buku lengkap |

**5.3** Subclass `Majalah` (mewarisi `ItemPerpustakaan`):

| **Komponen** | **Spesifikasi** |
| --- | --- |
| **Properti Tambahan** | `edisi: Int`<br>`bulanTerbit: String` |
| **Override** | `hitungDenda()` → 500 per hari<br>`tampilkanInfo()` → menampilkan info majalah lengkap |

**5.4** Subclass `BukuFiksi` (mewarisi `Buku`):

| **Komponen** | **Spesifikasi** |
| --- | --- |
| **Properti Tambahan** | `genre: String` ("Fantasi", "Romance", "Misteri", dll.) |
| **Override** | `tampilkanInfo()` → menampilkan genre |

**5.5** Subclass `BukuNonFiksi` (mewarisi `Buku`):

| **Komponen** | **Spesifikasi** |
| --- | --- |
| **Properti Tambahan** | `bidang: String` ("Sains", "Sejarah", "Teknologi", dll.) |
| **Override** | `tampilkanInfo()` → menampilkan bidang |

**5.6** Subclass `MajalahHarian` dan `MajalahMingguan` (mewarisi `Majalah`):

| **Kelas** | **Properti Tambahan** | **Override** |
| --- | --- | --- |
| `MajalahHarian` | `hariTerbit: String` | `hitungDenda()` → 300 per hari |
| `MajalahMingguan` | `hariTerbit: String` | `hitungDenda()` → 700 per hari |

**5.7** Kelas `Perpustakaan`:

| **Komponen** | **Spesifikasi** |
| --- | --- |
| **Properti** | `nama: String` (read-only)<br>`koleksi: MutableList<ItemPerpustakaan>` (private) |
| **Metode** | `tambahItem(item: ItemPerpustakaan)`<br>`cariItem(keyword: String): List<ItemPerpustakaan>`<br>`tampilkanSemuaItem()`<br>`tampilkanItemDipinjam()`<br>`tampilkanItemTersedia()`<br>`hitungTotalDenda(hariTerlambat: Int): Double` |

**5.8** Fungsi `main()`:

- Buat objek `Perpustakaan` dengan nama "Perpustakaan Digital Nusantara"
- Tambahkan minimal **8 item** (2 BukuFiksi, 2 BukuNonFiksi, 2 MajalahHarian, 2 MajalahMingguan)
- Tampilkan semua item
- Lakukan peminjaman beberapa item
- Tampilkan item yang dipinjam dan tersedia
- Hitung total denda jika semua item yang dipinjam terlambat 5 hari

### Output yang Diharapkan (Contoh)

```
==================================================
📚 PERPUSTAKAAN DIGITAL NUSANTARA
==================================================

=== DAFTAR KOLEKSI ===

[Buku Fiksi] ID: B001
Judul    : Laskar Pelangi
Penulis  : Andrea Hirata
Tahun    : 2005
Halaman  : 529
Genre    : Drama
Status   : Tersedia

[Buku Non-Fiksi] ID: B002
Judul    : Sapiens
Penulis  : Yuval Noah Harari
Tahun    : 2011
Halaman  : 498
Bidang   : Sejarah
Status   : Tersedia

...

=== PEMINJAMAN ===
✅ Buku "Laskar Pelangi" berhasil dipinjam
✅ Majalah "National Geographic" berhasil dipinjam

=== ITEM DIPINJAM ===
- Laskar Pelangi (Buku Fiksi)
- National Geographic (Majalah Harian)

=== ITEM TERSEDIA ===
- Sapiens (Buku Non-Fiksi)
- ...

=== TOTAL DENDA (5 hari terlambat) ===
Total denda: Rp 11.500
```

---

## LATIHAN 6: TANTANGAN — SISTEM MANAJEMEN KENDARAAN

**Estimasi Waktu: 90 Menit | Tingkat: Lanjut**

### Tujuan

Mengimplementasikan semua konsep pewarisan dalam satu sistem terintegrasi.

### Instruksi

Buatlah program lengkap **Sistem Manajemen Kendaraan** dengan ketentuan berikut:

#### 1. Kelas `Vehicle` (Kendaraan) — Kelas Induk

| **Komponen** | **Spesifikasi** |
| --- | --- |
| **Properti** | `brand: String` (read-only)<br>`model: String` (read-only)<br>`year: Int` (read-only)<br>`price: Double` (read-only)<br>`isSold: Boolean` (private setter, default false) |
| **Metode** | `calculateTax(): Double` (open) → pajak = 10% dari harga<br>`sell(): Boolean` → menandai kendaraan sebagai sold<br>`isAvailable(): Boolean` → cek ketersediaan<br>`displayInfo(): String` (open) → menampilkan info kendaraan |

#### 2. Subclass `Car` — Mobil

| **Komponen** | **Spesifikasi** |
| --- | --- |
| **Properti Tambahan** | `numberOfDoors: Int`<br>`fuelType: String` ("Bensin", "Diesel", "Listrik") |
| **Override** | `calculateTax()` → pajak = 12% dari harga<br>`displayInfo()` → menampilkan info mobil |

#### 3. Subclass `Motorcycle` — Motor

| **Komponen** | **Spesifikasi** |
| --- | --- |
| **Properti Tambahan** | `engineCapacity: Int` (dalam cc)<br>`type: String` ("Sport", "Cruiser", "Matic") |
| **Override** | `calculateTax()` → pajak = 5% dari harga<br>`displayInfo()` → menampilkan info motor |

#### 4. Subclass `Truck` — Truk

| **Komponen** | **Spesifikasi** |
| --- | --- |
| **Properti Tambahan** | `loadCapacity: Double` (dalam ton)<br>`numberOfAxles: Int` |
| **Override** | `calculateTax()` → pajak = 15% dari harga<br>`displayInfo()` → menampilkan info truk |

#### 5. Kelas `Dealership` (Dealer)

| **Komponen** | **Spesifikasi** |
| --- | --- |
| **Properti** | `name: String` (read-only)<br>`vehicles: MutableList<Vehicle>` (private) |
| **Metode** | `addVehicle(vehicle: Vehicle)`<br>`findVehicle(brand: String, model: String): Vehicle?`<br>`sellVehicle(brand: String, model: String): Boolean`<br>`getAvailableVehicles(): List<Vehicle>`<br>`getSoldVehicles(): List<Vehicle>`<br>`displayAllVehicles()`<br>`displayAvailableVehicles()`<br>`getTotalRevenue(): Double` |

#### 6. Fungsi `main()`

- Buat objek `Dealership` dengan nama "Dealer Motor Jaya"
- Tambahkan **minimal 6 kendaraan** (2 mobil, 2 motor, 2 truk)
- Tampilkan semua kendaraan
- Tampilkan kendaraan yang tersedia
- Lakukan penjualan beberapa kendaraan
- Tampilkan kendaraan yang tersisa dan total pendapatan

### Output yang Diharapkan (Contoh)

```
==================================================
🏢 DEALER MOTOR JAYA
==================================================

=== SEMUA KENDARAAN ===

[Car] Toyota Avanza (2023)
Harga     : Rp 250.000.000
Pajak     : Rp 30.000.000
Pintu     : 4
Bahan Bakar: Bensin
Status    : Tersedia

[Motorcycle] Honda Beat (2022)
Harga     : Rp 18.000.000
Pajak     : Rp 900.000
Mesin     : 125cc
Tipe      : Matic
Status    : Tersedia

[Truck] Hino Dutro (2021)
Harga     : Rp 350.000.000
Pajak     : Rp 52.500.000
Kapasitas : 5.0 ton
Sumbu     : 4
Status    : Tersedia

...

=== PENJUALAN ===
✅ Toyota Avanza berhasil dijual!
✅ Honda Beat berhasil dijual!

=== KENDARAAN TERSEDIA ===
- Hino Dutro (Truck)
- ...

=== TOTAL PENDAPATAN ===
Rp 268.000.000
```

### Kriteria Penilaian Latihan 6

| **Kriteria** | **Bobot** | **Indikator** |
| --- | --- | --- |
| **Hierarki Pewarisan** | 30% | • Kelas induk `Vehicle` menggunakan `open`<br>• Subclass mewarisi dengan benar menggunakan `:`<br>• Constructor inheritance diimplementasikan dengan benar |
| **Overriding** | 25% | • Metode `calculateTax()` di-override di semua subclass<br>• Menggunakan `super` dengan tepat<br>• Overriding properti jika diperlukan |
| **Fungsi main()** | 20% | • Menampilkan semua skenario yang diminta<br>• Output jelas dan informatif |
| **Kode Berkualitas** | 15% | • Kode bersih, terstruktur, diberi komentar<br>• Menggunakan naming convention yang benar |
| **Program Berjalan** | 10% | • Program berjalan tanpa error<br>• Semua fungsi berfungsi sesuai spesifikasi |

---

## RUBRIK PENILAIAN PRAKTIKUM PERTEMUAN 3

| **Latihan** | **Bobot** | **Kriteria** |
| --- | --- | --- |
| **Latihan 1** | 10% | Program berjalan, output sesuai, refleksi dijawab |
| **Latihan 2** | 15% | Overriding benar, `super` digunakan, tantangan tambahan dikerjakan |
| **Latihan 3** | 15% | Constructor inheritance benar, urutan inisialisasi dipahami |
| **Latihan 4** | 20% | Hierarki 3 level benar, rumus perhitungan tepat |
| **Latihan 5** | 20% | Studi kasus lengkap, semua fitur berfungsi |
| **Latihan 6** | 20% | Tantangan diselesaikan dengan baik, kode berkualitas |
| **Total** | **100%** | |

---

## CHECKLIST PENGUMPULAN

- [ ] File `Latihan1_Kendaraan.kt`
- [ ] File `Latihan2_Hewan.kt`
- [ ] File `Latihan3_Pegawai.kt`
- [ ] File `Latihan4_Shapes.kt`
- [ ] File `Latihan5_Perpustakaan.kt`
- [ ] File `Latihan6_Dealership.kt`
- [ ] Screenshot output setiap latihan
- [ ] Jawaban pertanyaan refleksi (dalam file `.md` atau `.txt`)

---

## TIPS PRAKTIKUM

1. **Ketik ulang kode**, jangan copy-paste — ini membantu pemahaman
2. **Baca error dengan teliti** — compiler Kotlin memberikan pesan yang jelas
3. **Eksperimen** — coba hapus `open`, `override`, atau `super` dan lihat apa yang terjadi
4. **Gunakan `println()`** untuk debugging dan memahami alur program
5. **Diskusikan** dengan teman jika mengalami kesulitan, tapi tetap tulis kode sendiri
6. **Manfaatkan dokumentasi** — [https://kotlinlang.org/docs/inheritance.html](https://kotlinlang.org/docs/inheritance.html)
7. **Link Pengumpulan** - <https://forms.gle/L7b8sKAfC1ZCfvcK9>

---

**Selamat Mengerjakan! 🚀**

*"Pewarisan adalah fondasi hierarki kelas — kuasai dengan baik, maka polimorfisme akan mudah dipahami."*
