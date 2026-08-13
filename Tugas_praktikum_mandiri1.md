# TUGAS MANDIRI - PEMROGRAMAN BERORIENTASI OBJEK

## Sistem Manajemen Perpustakaan Digital

---

## A. PENDAHULUAN

### 1.1 Deskripsi Tugas

Tugas mandiri ini mengharuskan Anda untuk **menulis seluruh kode dari awal** berdasarkan spesifikasi yang diberikan. Anda **tidak diperkenankan** menyalin kode dari sumber mana pun. Tujuan tugas ini adalah menguji kemampuan Anda dalam:

1. Menerjemahkan spesifikasi kebutuhan ke dalam struktur kelas OOP
2. Mengimplementasikan **4 Pilar OOP** (Enkapsulasi, Pewarisan, Polimorfisme, Abstraksi)
3. Menulis kode yang **bersih, terstruktur, dan terdokumentasi**
4. Menggunakan fitur-fitur Kotlin seperti **Sealed Class**, **Smart Casting**, dan **Null Safety**

### 1.2 Kasus yang Diangkat

Anda diminta membangun **Sistem Manajemen Perpustakaan Digital** yang dapat mengelola:

- **Item** perpustakaan (Buku, Jurnal, DVD)
- **Anggota** perpustakaan
- **Transaksi** peminjaman dan pengembalian
- **Status** transaksi dengan berbagai keadaan
- **Denda** atas keterlambatan pengembalian

---

## B. KETENTUAN UMUM

### 2.1 Aturan Pengerjaan

| **No** | **Aturan** | **Keterangan** |
|--------|------------|----------------|
| 1 | **Kode Asli** | Semua kode harus ditulis sendiri. Copy-paste dari internet atau teman akan dikenakan sanksi. |
| 2 | **KDoc Wajib** | Setiap kelas, properti publik, dan metode harus memiliki dokumentasi KDoc. |
| 3 | **Naming Convention** | Gunakan `camelCase` untuk variabel/fungsi, `PascalCase` untuk kelas. |
| 4 | **Modular** | Setiap kelas harus berada di file terpisah dengan nama yang sesuai. |
| 5 | **No External Library** | Hanya gunakan Kotlin Standard Library. |

### 2.2 Struktur Folder Wajib

```
Tugas_Mandiri_OOP_NIM_Nama/
├── src/
│   ├── Main.kt
│   ├── Item.kt
│   ├── Book.kt
│   ├── Journal.kt
│   ├── DVD.kt
│   ├── TransactionStatus.kt
│   ├── Transaction.kt
│   ├── Member.kt
│   └── Library.kt
├── docs/
│   └── Laporan_Tugas_Mandiri.pdf
└── README.md
```

---

## C. SPESIFIKASI KELAS (Yang Harus Dibuat)

### 3.1 Kelas `Item` (Kelas Induk Abstrak)

#### Tujuan
Merepresentasikan item umum yang dapat dipinjam di perpustakaan. Kelas ini bersifat **abstrak**—tidak bisa diinstansiasi langsung.

#### Properti yang Harus Ada

| **Nama Properti** | **Tipe** | **Visibility** | **Keterangan** |
|-------------------|----------|----------------|----------------|
| `id` | `String` | `val` (public) | ID unik item |
| `title` | `String` | `val` (public) | Judul item |
| `year` | `Int` | `val` (public) | Tahun terbit/rilis |
| `isAvailable` | `Boolean` | `var` dengan **`private set`** | Status ketersediaan. Default: `true`. Hanya bisa diubah dari dalam kelas. |

#### Metode Abstrak (Wajib di-*override* oleh subclass)

| **Nama Metode** | **Return Type** | **Deskripsi** |
|-----------------|-----------------|---------------|
| `calculateFinePerDay()` | `Double` | Menghitung denda per hari keterlambatan. Besaran berbeda tiap jenis item. |
| `getItemType()` | `String` | Mengembalikan jenis item ("Buku", "Jurnal", atau "DVD"). |
| `getMaxBorrowDays()` | `Int` | Mengembalikan batas maksimal peminjaman dalam hari. |

#### Metode Concrete (Sudah punya implementasi, boleh di-*override*)

| **Nama Metode** | **Parameter** | **Return** | **Deskripsi Perilaku** |
|-----------------|---------------|------------|------------------------|
| `borrow()` | - | `Boolean` | Jika `isAvailable == true`, ubah menjadi `false`, cetak pesan sukses, return `true`. Jika `false`, cetak pesan error, return `false`. |
| `returnItem()` | `daysLate: Int = 0` | `Double` | Jika `isAvailable == false`, ubah menjadi `true`. Hitung denda = `daysLate * calculateFinePerDay()`. Cetak pesan pengembalian dan total denda (jika > 0). Kembalikan total denda. Jika item tidak dipinjam, cetak peringatan dan return `0.0`. |
| `displayInfo()` | - | `Unit` | Cetak informasi item secara terstruktur (ID, judul, tahun, status, denda/hari, maks pinjam). **Bersifat `open`** agar subclass bisa menambahkan properti spesifik. |

---

### 3.2 Kelas `Book` (Mewarisi `Item`)

#### Tujuan
Merepresentasikan **Buku** dengan properti tambahan spesifik buku.

#### Properti Tambahan

| **Nama Properti** | **Tipe** | **Visibility** | **Keterangan** |
|-------------------|----------|----------------|----------------|
| `author` | `String` | `val` (public) | Penulis buku |
| `pages` | `Int` | `val` (public) | Jumlah halaman |
| `genre` | `String` | `val` (public) | Genre buku |

#### Implementasi Metode Abstrak

| **Metode** | **Nilai yang Harus Dikembalikan** |
|------------|-----------------------------------|
| `calculateFinePerDay()` | `2000.0` (Rp 2.000 per hari) |
| `getItemType()` | `"Buku"` |
| `getMaxBorrowDays()` | `14` (14 hari) |

#### Override `displayInfo()`
Panggil `super.displayInfo()`, kemudian tambahkan cetakan:
- Penulis
- Jumlah Halaman
- Genre

---

### 3.3 Kelas `Journal` (Mewarisi `Item`)

#### Tujuan
Merepresentasikan **Jurnal** dengan properti tambahan spesifik jurnal.

#### Properti Tambahan

| **Nama Properti** | **Tipe** | **Visibility** | **Keterangan** |
|-------------------|----------|----------------|----------------|
| `publisher` | `String` | `val` (public) | Penerbit jurnal |
| `volume` | `Int` | `val` (public) | Volume jurnal |
| `issueNumber` | `Int` | `val` (public) | Nomor edisi |

#### Implementasi Metode Abstrak

| **Metode** | **Nilai yang Harus Dikembalikan** |
|------------|-----------------------------------|
| `calculateFinePerDay()` | `3000.0` (Rp 3.000 per hari) |
| `getItemType()` | `"Jurnal"` |
| `getMaxBorrowDays()` | `7` (7 hari) |

#### Override `displayInfo()`
Panggil `super.displayInfo()`, kemudian tambahkan cetakan:
- Penerbit
- Volume
- Edisi

---

### 3.4 Kelas `DVD` (Mewarisi `Item`)

#### Tujuan
Merepresentasikan **DVD** dengan properti tambahan spesifik DVD.

#### Properti Tambahan

| **Nama Properti** | **Tipe** | **Visibility** | **Keterangan** |
|-------------------|----------|----------------|----------------|
| `director` | `String` | `val` (public) | Sutradara |
| `duration` | `Int` | `val` (public) | Durasi (menit) |
| `genre` | `String` | `val` (public) | Genre DVD |

#### Implementasi Metode Abstrak

| **Metode** | **Nilai yang Harus Dikembalikan** |
|------------|-----------------------------------|
| `calculateFinePerDay()` | `5000.0` (Rp 5.000 per hari) |
| `getItemType()` | `"DVD"` |
| `getMaxBorrowDays()` | `3` (3 hari) |

#### Override `displayInfo()`
Panggil `super.displayInfo()`, kemudian tambahkan cetakan:
- Sutradara
- Durasi
- Genre

---

### 3.5 Sealed Class `TransactionStatus`

#### Tujuan
Mewakili **status transaksi** peminjaman. Karena status hanya ada beberapa kemungkinan, gunakan **sealed class** agar semua kemungkinan diketahui di compile-time.

#### Subclass/Objects yang Harus Ada

| **Nama** | **Tipe** | **Properti** | **Deskripsi** |
|----------|----------|--------------|---------------|
| `Borrowed` | `object` | - | Status: sedang dipinjam |
| `Returned` | `object` | - | Status: sudah dikembalikan |
| `Overdue` | `data class` | `daysLate: Int` | Status: terlambat dengan jumlah hari keterlambatan |
| `Cancelled` | `object` | - | Status: dibatalkan |

#### Metode yang Harus Ada

| **Nama Metode** | **Return Type** | **Deskripsi** |
|-----------------|-----------------|---------------|
| `display()` | `String` | **Abstrak**. Mengembalikan string representasi status (misal: "📖 Dipinjam", "⚠️ Terlambat (3 hari)"). |
| `isFinal()` | `Boolean` | **Concrete**. Mengembalikan `true` jika status adalah `Returned` atau `Cancelled` (status akhir yang tidak bisa diubah lagi). |

---

### 3.6 Kelas `Transaction`

#### Tujuan
Merepresentasikan **satu transaksi peminjaman** yang menghubungkan item, anggota, dan status.

#### Properti yang Harus Ada

| **Nama Properti** | **Tipe** | **Visibility** | **Keterangan** |
|-------------------|----------|----------------|----------------|
| `id` | `String` | `val` (public) | ID unik transaksi |
| `item` | `Item` | `val` (public) | Item yang dipinjam |
| `member` | `Member` | `val` (public) | Anggota yang meminjam |
| `borrowDate` | `String` | `val` (public) | Tanggal pinjam (gunakan `java.time.LocalDate.now().toString()`) |
| `status` | `TransactionStatus` | `var` (public) | Status transaksi, default: `TransactionStatus.Borrowed` |

#### Metode yang Harus Ada

| **Nama Metode** | **Parameter** | **Return** | **Deskripsi Perilaku** |
|-----------------|---------------|------------|------------------------|
| `returnItem()` | `daysLate: Int` | `Double` | Jika status sudah final (`isFinal()`), cetak error dan return `0.0`. Jika belum, panggil `item.returnItem(daysLate)` untuk mengembalikan item. Jika `daysLate > 0`, ubah status menjadi `TransactionStatus.Overdue(daysLate)`. Jika tidak, ubah menjadi `TransactionStatus.Returned`. Kembalikan total denda. |
| `cancel()` | - | `Unit` | Jika status sudah final, cetak error. Jika belum, ubah status menjadi `TransactionStatus.Cancelled`, dan panggil `item.returnItem(0)` untuk mengembalikan ketersediaan item. |
| `displayTransaction()` | - | `Unit` | Cetak seluruh informasi transaksi (ID, item, peminjam, tanggal, status, dan keterangan tambahan jika ada). |

---

### 3.7 Kelas `Member`

#### Tujuan
Merepresentasikan **anggota perpustakaan** yang dapat meminjam item.

#### Properti yang Harus Ada

| **Nama Properti** | **Tipe** | **Visibility** | **Keterangan** |
|-------------------|----------|----------------|----------------|
| `id` | `String` | `val` (public) | ID anggota |
| `name` | `String` | `val` (public) | Nama anggota |
| `email` | `String` | `private val` | Email (di-enkapsulasi) |
| `phone` | `String` | `private val` | Telepon (di-enkapsulasi) |
| `transactions` | `MutableList<Transaction>` | `private val` | Daftar transaksi anggota |

#### Properti Turunan (Computed Property)

| **Nama Properti** | **Tipe** | **Deskripsi** |
|-------------------|----------|---------------|
| `transactionCount` | `Int` | Jumlah total transaksi (`transactions.size`) |
| `totalFines` | `Double` | Total denda dari semua transaksi (jumlahkan `daysLate * item.calculateFinePerDay()` pada status `Overdue`) |
| `activeBorrows` | `Int` | Jumlah transaksi dengan status `Borrowed` |

#### Getter untuk Properti Private

| **Nama Metode** | **Return** | **Deskripsi** |
|-----------------|------------|---------------|
| `getEmail()` | `String` | Mengembalikan email |
| `getPhone()` | `String` | Mengembalikan telepon |

#### Metode yang Harus Ada

| **Nama Metode** | **Parameter** | **Return** | **Deskripsi Perilaku** |
|-----------------|---------------|------------|------------------------|
| `borrowItem()` | `item: Item` | `Transaction?` | Cek `item.isAvailable`. Jika tidak tersedia, cetak error, return `null`. Cek `activeBorrows`. Jika sudah >= 3, cetak error (maksimal 3 item), return `null`. Jika lolos, panggil `item.borrow()`. Buat objek `Transaction` baru (generate ID dengan `TRX-${System.currentTimeMillis()}`). Tambahkan ke `transactions`. Cetak sukses. Return transaksi. |
| `returnItem()` | `item: Item`, `daysLate: Int = 0` | `Double` | Cari transaksi aktif (`status is Borrowed`) dengan `item` yang sesuai. Jika tidak ditemukan, cetak error, return `0.0`. Jika ditemukan, panggil `transaction.returnItem(daysLate)` dan kembalikan nilai dendanya. |
| `getTransactions()` | - | `List<Transaction>` | Mengembalikan daftar transaksi (boleh pakai `toList()` untuk immutability). |
| `displayInfo()` | - | `Unit` | Cetak informasi anggota: ID, Nama, Email, Telepon, Total Pinjam, Pinjam Aktif, Total Denda. |
| `displayTransactions()` | - | `Unit` | Cetak riwayat transaksi anggota secara terstruktur. |

---

### 3.8 Kelas `Library`

#### Tujuan
Kelas utama yang mengelola seluruh operasi perpustakaan (menyimpan item, anggota, dan transaksi).

#### Properti yang Harus Ada

| **Nama Properti** | **Tipe** | **Visibility** | **Keterangan** |
|-------------------|----------|----------------|----------------|
| `name` | `String` | `val` (public) | Nama perpustakaan |
| `items` | `MutableList<Item>` | `private val` | Daftar semua item |
| `members` | `MutableList<Member>` | `private val` | Daftar semua anggota |
| `transactions` | `MutableList<Transaction>` | `private val` | Daftar semua transaksi |

#### Properti Turunan (Computed Property)

| **Nama Properti** | **Tipe** | **Deskripsi** |
|-------------------|----------|---------------|
| `totalItems` | `Int` | Jumlah semua item (`items.size`) |
| `availableItems` | `Int` | Jumlah item yang tersedia (`items.count { it.isAvailable }`) |
| `totalMembers` | `Int` | Jumlah anggota (`members.size`) |
| `totalTransactions` | `Int` | Jumlah transaksi (`transactions.size`) |

#### Metode Manajemen Item

| **Nama Metode** | **Parameter** | **Return** | **Deskripsi Perilaku** |
|-----------------|---------------|------------|------------------------|
| `addItem()` | `item: Item` | `Unit` | Tambahkan item ke `items`, cetak pesan sukses. |
| `addItems()` | `vararg newItems: Item` | `Unit` | Tambahkan banyak item sekaligus (panggil `addItem` per item). |
| `findItem()` | `id: String` | `Item?` | Cari item berdasarkan ID, return `null` jika tidak ditemukan. |
| `searchItems()` | `keyword: String` | `List<Item>` | Cari item berdasarkan judul atau ID yang mengandung `keyword` (case-insensitive). |

#### Metode Manajemen Anggota

| **Nama Metode** | **Parameter** | **Return** | **Deskripsi Perilaku** |
|-----------------|---------------|------------|------------------------|
| `registerMember()` | `id: String`, `name: String`, `email: String`, `phone: String` | `Boolean` | Jika ID sudah digunakan, cetak error, return `false`. Jika belum, buat objek `Member`, tambahkan ke `members`, cetak sukses, return `true`. |
| `findMember()` | `id: String` | `Member?` | Cari anggota berdasarkan ID, return `null` jika tidak ditemukan. |

#### Metode Operasi Perpustakaan

| **Nama Metode** | **Parameter** | **Return** | **Deskripsi Perilaku** |
|-----------------|---------------|------------|------------------------|
| `borrowItem()` | `memberId: String`, `itemId: String` | `Transaction?` | Cari `member` dan `item`. Jika salah satu null, cetak error, return `null`. Jika ditemukan, panggil `member.borrowItem(item)`. Jika transaksi berhasil dibuat, tambahkan ke `transactions` dan return transaksi. |
| `returnItem()` | `memberId: String`, `itemId: String`, `daysLate: Int = 0` | `Double` | Cari `member` dan `item`. Jika salah satu null, cetak error, return `0.0`. Jika ditemukan, panggil `member.returnItem(item, daysLate)` dan kembalikan nilai dendanya. |

#### Metode Laporan dan Tampilan

| **Nama Metode** | **Deskripsi Perilaku** |
|-----------------|------------------------|
| `displayAllItems()` | Cetak semua item dengan memanggil `displayInfo()` setiap item. Sertakan total dan jumlah tersedia. |
| `displayAvailableItems()` | Cetak daftar item yang tersedia (`isAvailable == true`) dalam format ringkas. |
| `displayAllMembers()` | Cetak informasi semua anggota dengan memanggil `displayInfo()` setiap anggota. |
| `displayAllTransactions()` | Cetak semua transaksi dengan memanggil `displayTransaction()` setiap transaksi. |
| `displayReport()` | Cetak laporan ringkasan perpustakaan: nama, total item, tersedia, dipinjam, total anggota, total transaksi, total denda. |

---

## D. SPESIFIKASI FUNGSI `main()`

Anda harus membuat fungsi `main()` yang mendemonstrasikan **seluruh fitur** sistem dengan skenario **wajib** berikut. **Kode harus ditulis dari nol** berdasarkan spesifikasi ini.

### D.1 Data Wajib yang Digunakan

#### Item (Minimal 6 item, 2 dari setiap jenis)

| **Jenis** | **Data** |
|-----------|----------|
| **Buku 1** | ID: `B001`, Judul: `"Pemrograman Kotlin"`, Tahun: `2023`, Penulis: `"Budi Santoso"`, Halaman: `350`, Genre: `"Programming"` |
| **Buku 2** | ID: `B002`, Judul: `"Dasar-Dasar OOP"`, Tahun: `2022`, Penulis: `"Siti Rahayu"`, Halaman: `280`, Genre: `"Education"` |
| **Jurnal 1** | ID: `J001`, Judul: `"Jurnal Teknologi Informasi"`, Tahun: `2023`, Penerbit: `"ITB"`, Volume: `15`, Edisi: `2` |
| **Jurnal 2** | ID: `J002`, Judul: `"Jurnal Pendidikan"`, Tahun: `2022`, Penerbit: `"UGM"`, Volume: `10`, Edisi: `1` |
| **DVD 1** | ID: `D001`, Judul: `"Inception"`, Tahun: `2010`, Sutradara: `"Christopher Nolan"`, Durasi: `148`, Genre: `"Sci-Fi"` |
| **DVD 2** | ID: `D002`, Judul: `"The Matrix"`, Tahun: `1999`, Sutradara: `"Wachowski"`, Durasi: `136`, Genre: `"Action"` |

#### Anggota (Minimal 3 anggota)

| **ID** | **Nama** | **Email** | **Telepon** |
|--------|----------|-----------|-------------|
| `M001` | `"Ahmad Fauzi"` | `"ahmad@email.com"` | `"08123456789"` |
| `M002` | `"Dewi Lestari"` | `"dewi@email.com"` | `"08129876543"` |
| `M003` | `"Rizky Pratama"` | `"rizky@email.com"` | `"08125678901"` |

### D.2 Skenario yang Harus Didemonstrasikan (Urutan Wajib)

1. **Inisialisasi**: Buat objek `Library` dengan nama `"Perpustakaan Kampus"`.

2. **Tambah Item**: Tambahkan 6 item di atas menggunakan `addItems()` atau `addItem()`.

3. **Registrasi Anggota**: Daftarkan 3 anggota di atas.

4. **Tampilkan Semua Item**: Panggil `displayAllItems()`.

5. **Peminjaman (Skenario A)**:
   - Ahmad (`M001`) meminjam **"Pemrograman Kotlin"** (`B001`).
   - Ahmad (`M001`) meminjam **"Inception"** (`D001`).
   - Dewi (`M002`) meminjam **"Jurnal Teknologi Informasi"** (`J001`).
   - Rizky (`M003`) meminjam **"Dasar-Dasar OOP"** (`B002`).

6. **Tampilkan Item Tersedia**: Panggil `displayAvailableItems()` untuk melihat item yang tersisa.

7. **Tampilkan Transaksi Anggota**:
   - Tampilkan transaksi Ahmad.
   - Tampilkan transaksi Dewi.

8. **Pengembalian (Skenario B)**:
   - Ahmad mengembalikan **"Pemrograman Kotlin"** tepat waktu (`daysLate = 0`).
   - Dewi mengembalikan **"Jurnal Teknologi Informasi"** terlambat **3 hari** (`daysLate = 3`).

9. **Tampilkan Transaksi Setelah Pengembalian**: Tampilkan transaksi Ahmad dan Dewi lagi untuk melihat perubahan status.

10. **Demonstrasi Polimorfisme**:
    - Buat `List<Item>` yang berisi 1 Buku, 1 Jurnal, dan 1 DVD.
    - Loop list tersebut, panggil `getItemType()` dan `calculateFinePerDay()` untuk setiap item.
    - Cetak hasilnya (contoh: "Buku - Denda/hari: Rp 2.000").

11. **Demonstrasi Sealed Class**:
    - Buat variabel dengan tipe `TransactionStatus` yang berisi:
      - `TransactionStatus.Borrowed`
      - `TransactionStatus.Returned`
      - `TransactionStatus.Overdue(5)`
      - `TransactionStatus.Cancelled`
    - Gunakan `when` expression untuk mencetak hasil `display()` dari masing-masing status.

12. **Demonstrasi Smart Casting**:
    - Ambil salah satu item (misal `B001`).
    - Gunakan operator `is` untuk mengecek apakah item tersebut adalah `Book`, `Journal`, atau `DVD`.
    - Cetak pesan sesuai jenisnya (misal: "Item B001 adalah Buku").
    - Gunakan `as?` untuk mencoba casting item ke `DVD`. Tampilkan hasilnya (bisa null atau berhasil).

13. **Demonstrasi Enkapsulasi**:
    - Coba akses langsung properti `isAvailable` dari item dan ubah nilainya. Kompiler akan error karena `private set`.
    - Coba akses langsung properti `email` dari anggota. Kompiler akan error karena `private val`.
    - Tampilkan pesan di layar bahwa enkapsulasi melindungi data tersebut (cukup dengan `println` yang menjelaskan).

14. **Tampilkan Laporan Akhir**: Panggil `displayReport()` untuk menampilkan ringkasan akhir perpustakaan.

---

## E. ANALISIS OOP (WAJIB DIJAWAB DI LAPORAN)

Jawablah pertanyaan-pertanyaan berikut dengan **lengkap, jelas, dan sertakan contoh dari kode yang Anda tulis**.

### E.1 Enkapsulasi

1. Sebutkan **minimal 3** contoh penerapan enkapsulasi dalam kode Anda (sebutkan nama properti, visibility modifier-nya, dan mengapa dibuat demikian).
2. Mengapa properti `isAvailable` di kelas `Item` menggunakan `private set`? Apa yang terjadi jika properti tersebut dibuat `public var`?
3. Mengapa properti `email` dan `phone` di kelas `Member` dibuat `private val`? Bagaimana cara mengaksesnya jika dibutuhkan?

### E.2 Pewarisan (Inheritance)

1. Gambarkan **diagram hierarki pewarisan** dari sistem Anda (mulai dari `Item` hingga subclass-nya).
2. Sebutkan contoh penggunaan keyword `open`, `override`, dan `super` dalam kode Anda. Jelaskan fungsi masing-masing.
3. Mengapa kelas `Item` dibuat sebagai `abstract class`, bukan `open class` biasa? Apa keuntungannya?

### E.3 Polimorfisme

1. Di mana letak penerapan **polymorphic references** dalam kode Anda? Berikan contoh baris kode yang menunjukkan variabel bertipe superclass menampung objek subclass.
2. Jelaskan bagaimana metode `calculateFinePerDay()` bekerja secara polimorfik. Mengapa pemanggilan metode yang sama bisa menghasilkan output berbeda?
3. Berikan contoh penggunaan **`is`** dan **`as?`** (smart casting) dalam kode Anda. Jelaskan perbedaan keduanya.

### E.4 Sealed Class

1. Mengapa `TransactionStatus` dibuat sebagai `sealed class` dan bukan `enum class` atau `interface`?
2. Sebutkan keuntungan menggunakan **sealed class** untuk representasi status transaksi, terutama dalam kaitannya dengan `when` expression.
3. Apa yang dimaksud dengan **ekshaustif `when`** pada sealed class? Berikan contoh dari kode Anda.

---

## F. FORMAT PENGUMPULAN

### F.1 Struktur File

```
Tugas_Mandiri_OOP_NIM_Nama/
├── src/
│   ├── Main.kt
│   ├── Item.kt
│   ├── Book.kt
│   ├── Journal.kt
│   ├── DVD.kt
│   ├── TransactionStatus.kt
│   ├── Transaction.kt
│   ├── Member.kt
│   └── Library.kt
├── docs/
│   └── Laporan_Tugas_Mandiri.pdf
└── README.md
```

### F.2 Laporan (PDF)

Laporan harus berisi:

1. **Cover** (Judul, Nama, NIM, Dosen)
2. **Pendahuluan** (Latar belakang, tujuan)
3. **Desain Sistem** (Diagram kelas)
4. **Implementasi** (Penjelasan setiap kelas dan metode penting)
5. **Demonstrasi** (Screenshot output program, minimal 10 screenshot)
6. **Analisis OOP** (Jawaban pertanyaan di bagian E)
7. **Kesimpulan dan Saran**
8. **Lampiran** (Kode lengkap - boleh copy-paste)

### F.3 README.md

Buat `README.md` yang berisi:
- Identitas mahasiswa
- Deskripsi singkat program
- Cara menjalankan program
- Struktur kelas

---

## G. KRITERIA PENILAIAN

| **Kriteria** | **Bobot** | **Indikator Penilaian** |
|--------------|-----------|--------------------------|
| **Kebenaran Kode** | 30% | Program berjalan tanpa error, semua fitur sesuai spesifikasi. |
| **Implementasi OOP** | 25% | Enkapsulasi, Pewarisan, Polimorfisme, dan Abstraksi diterapkan dengan tepat. |
| **Fungsi `main()`** | 15% | Mendemonstrasikan semua skenario wajib dengan output yang jelas dan terstruktur. |
| **Dokumentasi** | 10% | KDoc lengkap di semua kelas, properti, dan metode publik. Naming convention benar. |
| **Analisis OOP** | 10% | Jawaban pertanyaan analisis lengkap, akurat, dan mendalam. |
| **Laporan** | 10% | Struktur laporan lengkap, screenshot output, penjelasan yang baik. |

---

## H. PANDUAN PENGERJAAN (Tips)

1. **Kerjakan dari yang paling dasar**:
   - Mulai dari kelas `Item` (abstrak) dan subclass-nya (`Book`, `Journal`, `DVD`).
   - Test setiap kelas dengan membuat objek sederhana di `main()` sebelum melanjutkan.

2. **Gunakan IDE**:
   - Manfaatkan IntelliJ IDEA untuk autocomplete, error checking, dan debugging.

3. **Baca Error dengan Teliti**:
   - Jika kompiler error, baca pesan error-nya. Biasanya sudah jelas apa yang salah.

4. **Jangan Tulis Semua di Satu File**:
   - Pisahkan setiap kelas di file terpisah untuk memudahkan pengelolaan.

5. **Gunakan KDoc Secara Bertahap**:
   - Tulis dokumentasi setiap kali selesai membuat kelas/metode, jangan menunda.

6. **Testing Bertahap**:
   - Setelah membuat 1 kelas, langsung test. Jangan menunggu semua kelas selesai.

---

## I. PERTANYAAN YANG SERING DIAJUKAN (FAQ)

**Q: Apakah saya boleh menggunakan `data class` untuk kelas tertentu?**
A: Boleh, tetapi pastikan sesuai kebutuhan. Untuk kelas seperti `TransactionStatus.Overdue`, `data class` sangat cocok.

**Q: Bagaimana cara generate ID transaksi?**
A: Gunakan `"TRX-${System.currentTimeMillis()}"` untuk mendapatkan ID unik berdasarkan waktu.

**Q: Apakah saya harus membuat semua metode persis seperti spesifikasi?**
A: Nama metode dan parameter harus sesuai spesifikasi. Untuk logika internal, Anda bebas mengimplementasikannya selama perilaku output-nya sesuai.

**Q: Bagaimana jika saya lupa membuat dokumentasi KDoc?**
A: Nilai dokumentasi akan berkurang. Pastikan setiap kelas dan metode publik memiliki KDoc.

**Q: Apakah boleh menambahkan fitur di luar spesifikasi?**
A: Boleh, selama semua fitur wajib terpenuhi. Fitur tambahan dapat menjadi nilai plus.

---

## J. PENUTUP

> **"Kode yang baik adalah kode yang tidak hanya berfungsi, tetapi juga dapat dipahami oleh manusia lain (dan diri Anda sendiri 6 bulan kemudian)."**

Selamat mengerjakan! Gunakan tugas ini sebagai kesempatan untuk benar-benar menguasai konsep OOP. Jangan ragu untuk bereksperimen dan mencoba pendekatan yang berbeda. Kesalahan adalah bagian dari proses belajar.

**Pastikan Anda mengerjakan dengan jujur dan mandiri.** Kejujuran akademik adalah nilai yang tidak ternilai.

---

**Disusun oleh,**

M Harry K Saputra
Dosen Program Studi D4 Teknologi Rekayasa Informatika Industri
