Baik, saya pahami sekarang. Anda ingin **1 studi kasus** yang dipecah menjadi **5 soal** (sub-tugas) yang saling berkaitan. Setiap soal akan fokus pada implementasi bagian tertentu dari sistem, dan secara bertahap membangun keseluruhan aplikasi OOP dari dasar hingga lengkap.

Berikut saya sajikan **Tugas Mandiri OOP - Sistem Manajemen Transportasi Online (5 Soal Berurutan)**.

---

# TUGAS MANDIRI OOP (1 STUDI KASUS - 5 SOAL)

## Sistem Manajemen Transportasi Online

---

### Deskripsi Umum Studi Kasus

Anda diminta membangun **Sistem Manajemen Transportasi Online** (mirip seperti Gojek/Grab). Sistem ini mengelola:

- **Kendaraan** (mobil, motor, truk) dengan jenis dan tarif berbeda.
- **Pengemudi** (driver) yang memiliki kendaraan.
- **Pelanggan** (customer) yang memesan perjalanan.
- **Pesanan** (order) yang menghubungkan pelanggan, pengemudi, dan kendaraan.
- **Pembayaran** dengan berbagai metode (Kartu Kredit, QRIS, Tunai).
- **Status** pesanan yang berubah sepanjang proses (Menunggu, Berjalan, Selesai, Dibatalkan).

**Keterkaitan 5 Soal:**

| **Soal** | **Fokus** | **Kelas yang Dibuat** |
|----------|-----------|----------------------|
| Soal 1 | Konsep Dasar OOP (Kelas, Objek, Properti, Metode) | `Vehicle`, `Driver`, `Customer` |
| Soal 2 | Enkapsulasi (Private Setter, Getter, Validasi) | `Order`, `Payment` |
| Soal 3 | Pewarisan (Inheritance, `open`, `override`, `super`) | `Car`, `Motorcycle`, `Truck` (mewarisi `Vehicle`) |
| Soal 4 | Polimorfisme, Interface, Sealed Class | `PaymentMethod` (interface), `PaymentResult` (sealed), `OrderStatus` (sealed) |
| Soal 5 | Integrasi Sistem & Fungsi `main()` | `TransportSystem` (controller) + demo lengkap |

---

## Aturan Umum (Berlaku untuk Semua Soal)

| **No** | **Aturan** | **Keterangan** |
|--------|------------|----------------|
| 1 | **Kode Asli** | Semua kode harus ditulis sendiri. Dilarang copy-paste. |
| 2 | **KDoc Wajib** | Setiap kelas, properti publik, dan metode harus memiliki dokumentasi KDoc. |
| 3 | **Naming Convention** | `camelCase` untuk variabel/fungsi, `PascalCase` untuk kelas/interface. |
| 4 | **Modular** | Setiap kelas **harus** berada di file terpisah (`[NamaKelas].kt`). |
| 5 | **No External Library** | Hanya gunakan Kotlin Standard Library (`kotlin.*`, `java.time.*`, dll). |
| 6 | **Tipe Data** | Gunakan tipe data yang sesuai (`Double` untuk uang, `Int` untuk hitungan). |

---

# SOAL 1: KELAS DASAR (Basic Classes)

### Tujuan
Mengimplementasikan **kelas, objek, properti, dan metode dasar** tanpa fitur OOP lanjutan.

### Yang Harus Dibuat

#### 1. Kelas `Vehicle` (Kendaraan)

| **Komponen** | **Spesifikasi** |
|--------------|-----------------|
| **Properti** | `plateNumber: String` (val)<br>`brand: String` (val)<br>`model: String` (val)<br>`year: Int` (val)<br>`isAvailable: Boolean` (var, default `true`) |
| **Metode** | `displayInfo(): Unit` → cetak semua properti kendaraan<br>`calculateFare(distanceKm: Double): Double` → tarif dasar = `5000 + (distanceKm * 2000)` |

#### 2. Kelas `Driver` (Pengemudi)

| **Komponen** | **Spesifikasi** |
|--------------|-----------------|
| **Properti** | `id: String` (val)<br>`name: String` (val)<br>`phone: String` (val)<br>`vehicle: Vehicle` (val)<br>`isActive: Boolean` (var, default `true`) |
| **Metode** | `displayInfo(): Unit` → cetak semua data driver (termasuk info kendaraan)<br>`acceptOrder(): Boolean` → jika `isActive` true dan `vehicle.isAvailable` true, return true, jika tidak return false |

#### 3. Kelas `Customer` (Pelanggan)

| **Komponen** | **Spesifikasi** |
|--------------|-----------------|
| **Properti** | `id: String` (val)<br>`name: String` (val)<br>`phone: String` (val)<br>`email: String` (val)<br>`balance: Double` (var, default `0.0`) |
| **Metode** | `displayInfo(): Unit` → cetak semua data pelanggan<br>`topUp(amount: Double): Unit` → tambahkan ke `balance`<br>`canPay(amount: Double): Boolean` → return `balance >= amount` |

---

### Ketentuan Khusus Soal 1

1. **Buat semua kelas** di file terpisah (`Vehicle.kt`, `Driver.kt`, `Customer.kt`).
2. **Buat fungsi `main()`** di `Main.kt` yang:
   - Membuat 1 objek `Vehicle` (contoh: "B 1234 ABC", "Toyota", "Avanza", 2020).
   - Membuat 1 objek `Driver` dengan kendaraan tersebut.
   - Membuat 1 objek `Customer` dengan saldo awal Rp 50.000.
   - Tampilkan info semua objek.
   - Panggil `calculateFare(10.0)` dari kendaraan dan tampilkan hasilnya.
   - Top-up saldo customer sebesar Rp 100.000 dan tampilkan saldo baru.
   - Panggil `acceptOrder()` dari driver dan tampilkan hasilnya.

---

# SOAL 2: ENKAPSULASI (Encapsulation)

### Tujuan
Mengimplementasikan **enkapsulasi** dengan `private`, `private set`, getter, dan validasi.

### Yang Harus Dibuat

#### 1. Kelas `Order` (Pesanan) - *Memperkenalkan Enkapsulasi*

| **Komponen** | **Spesifikasi** |
|--------------|-----------------|
| **Properti** | `id: String` (val)<br>`customer: Customer` (val)<br>`driver: Driver` (val)<br>`pickupLocation: String` (val)<br>`destination: String` (val)<br>`distanceKm: Double` (val)<br>`_status: String` (var **private**, default `"Menunggu"`)<br>`_totalFare: Double` (var **private**, dihitung di `init`) |
| **Getter** | `getStatus(): String` → return `_status`<br>`getTotalFare(): Double` → return `_totalFare` |
| **Metode** | `startTrip(): Boolean` → jika `_status == "Menunggu"`, ubah ke `"Berjalan"`, return true<br>`completeTrip(): Boolean` → jika `_status == "Berjalan"`, ubah ke `"Selesai"`, return true<br>`cancelTrip(reason: String): Boolean` → jika `_status != "Selesai"`, ubah ke `"Dibatalkan"`, return true<br>`displayOrder(): Unit` → cetak semua data pesanan (ID, pelanggan, driver, lokasi, jarak, total, status) |

> **Catatan:** Gunakan `init` block untuk menghitung `_totalFare = driver.vehicle.calculateFare(distanceKm)`.

#### 2. Kelas `Payment` (Pembayaran) - *Enkapsulasi Penuh*

| **Komponen** | **Spesifikasi** |
|--------------|-----------------|
| **Properti** | `order: Order` (val)<br>`_amount: Double` (var **private**, diisi dari `order.getTotalFare()`)<br>`_method: String` (var **private**, default `"Tunai"`)<br>`_isPaid: Boolean` (var **private set**, default `false`) |
| **Getter** | `getAmount(): Double` → return `_amount`<br>`getMethod(): String` → return `_method`<br>`isPaid(): Boolean` → return `_isPaid` |
| **Metode** | `setMethod(method: String): Unit` → validasi method hanya "Tunai", "Kartu Kredit", atau "QRIS". Jika valid, set `_method`.<br>`processPayment(paidAmount: Double): Boolean` → jika `!_isPaid` dan `paidAmount >= _amount`, set `_isPaid = true`, return true. Jika kurang, return false.<br>`displayPayment(): Unit` → cetak detail pembayaran |

---

### Ketentuan Khusus Soal 2

1. **Buat kelas `Order` dan `Payment`** di file terpisah.
2. **Gunakan ulang** kelas `Vehicle`, `Driver`, `Customer` dari Soal 1 (boleh di-copy ke folder baru).
3. **Buat fungsi `main()`** di `Main.kt` yang:
   - Buat 1 kendaraan, 1 driver, 1 customer (seperti Soal 1).
   - Buat 1 objek `Order` dengan jarak 15 km.
   - Tampilkan detail order.
   - Ubah status order: `startTrip()`, lalu `completeTrip()`.
   - Coba batalkan order (harus gagal karena sudah selesai).
   - Buat objek `Payment` untuk order tersebut.
   - Set method pembayaran ke "QRIS".
   - Proses pembayaran dengan nominal yang cukup (misal: cukup/salah).
   - Tampilkan detail pembayaran.
   - **Demonstrasi enkapsulasi**: coba akses langsung `order._status` dari luar (kompiler akan error karena private). Tuliskan komentar "// ERROR: Cannot access private property" sebagai bukti.

---

# SOAL 3: PEWARISAN (Inheritance)

### Tujuan
Mengimplementasikan **pewarisan** dengan `open class`, `override`, `super`, dan constructor inheritance.

### Yang Harus Dibuat

#### 1. Ubah Kelas `Vehicle` menjadi `open class`
- Jadikan `Vehicle` sebagai **`open class`**.
- Tambahkan metode `open fun getType(): String` yang mengembalikan `"Kendaraan Umum"`.
- Ubah metode `calculateFare` menjadi `open` agar bisa di-override.
- Ubah `displayInfo()` menjadi `open`.

#### 2. Subclass `Car` (Mobil) - Mewarisi `Vehicle`

| **Komponen** | **Spesifikasi** |
|--------------|-----------------|
| **Properti Tambahan** | `fuelType: String` ("Bensin", "Diesel", "Listrik")<br>`numberOfDoors: Int` |
| **Override** | `getType()` → return `"Mobil"`<br>`calculateFare(distanceKm: Double)` → `8000 + (distanceKm * 2500)` (lebih mahal dari dasar)<br>`displayInfo()` → panggil `super.displayInfo()`, tambahkan fuelType dan numberOfDoors |

#### 3. Subclass `Motorcycle` (Motor) - Mewarisi `Vehicle`

| **Komponen** | **Spesifikasi** |
|--------------|-----------------|
| **Properti Tambahan** | `engineCapacity: Int` (cc)<br>`hasHelmet: Boolean` |
| **Override** | `getType()` → return `"Motor"`<br>`calculateFare(distanceKm: Double)` → `3000 + (distanceKm * 1500)` (lebih murah)<br>`displayInfo()` → panggil `super.displayInfo()`, tambahkan engineCapacity dan hasHelmet |

#### 4. Subclass `Truck` (Truk) - Mewarisi `Vehicle`

| **Komponen** | **Spesifikasi** |
|--------------|-----------------|
| **Properti Tambahan** | `loadCapacity: Double` (ton)<br>`numberOfAxles: Int` |
| **Override** | `getType()` → return `"Truk"`<br>`calculateFare(distanceKm: Double)` → `10000 + (distanceKm * 3500)` (paling mahal)<br>`displayInfo()` → panggil `super.displayInfo()`, tambahkan loadCapacity dan numberOfAxles |

#### 5. Perbaiki Kelas `Driver`
- Properti `vehicle` tetap bertipe `Vehicle` (ini akan menjadi **polymorphic reference** di Soal 4, tetapi di sini cukup biarkan).

---

### Ketentuan Khusus Soal 3

1. **Buat 4 file**: `Vehicle.kt` (diubah menjadi open), `Car.kt`, `Motorcycle.kt`, `Truck.kt`.
2. **Buat fungsi `main()`** yang:
   - Buat objek `Car`, `Motorcycle`, dan `Truck`.
   - Tampilkan info masing-masing (panggil `displayInfo()`).
   - Hitung tarif untuk jarak 20 km untuk masing-masing kendaraan.
   - Buat 3 driver dengan 3 kendaraan berbeda.
   - Tampilkan info driver.
   - **Demonstrasi `super`**: Pada `displayInfo()` Car, panggil `super.displayInfo()` lalu tambahkan properti sendiri.
   - **Demonstrasi constructor inheritance**: Pastikan parameter `plateNumber`, `brand`, `model`, `year` diteruskan ke superclass.

---

# SOAL 4: POLIMORFISME, INTERFACE, DAN SEALED CLASS

### Tujuan
Mengimplementasikan **polimorfisme** (polymorphic references, smart casting), **interface**, dan **sealed class**.

### Yang Harus Dibuat

#### 1. Interface `PaymentMethod`

| **Komponen** | **Spesifikasi** |
|--------------|-----------------|
| **Properti** | `name: String` (abstract) |
| **Metode** | `processPayment(amount: Double): PaymentResult`<br>`getFee(amount: Double): Double` (default = 0.0, bisa di-override) |

#### 2. Implementasi `PaymentMethod`

| **Kelas** | **Spesifikasi** |
|-----------|-----------------|
| `CreditCard` | `name = "Kartu Kredit"`, `getFee()` = `amount * 0.02`, validasi nomor kartu minimal 16 digit (via constructor) |
| `QRIS` | `name = "QRIS"`, `getFee()` = `amount * 0.005`, validasi kode QR minimal 10 karakter |
| `Cash` | `name = "Tunai"`, `getFee()` = `0.0` (tidak ada biaya) |

#### 3. Sealed Class `PaymentResult`

| **Komponen** | **Spesifikasi** |
|--------------|-----------------|
| **Subclass/Object** | `Success` (data class, properti: `transactionId: String`, `timestamp: String`)<br>`Failed` (data class, properti: `reason: String`, `errorCode: Int`)<br>`Pending` (object) |
| **Metode** | `display(): String` → abstrak, return representasi hasil |

#### 4. Sealed Class `OrderStatus` (Ganti dari `_status: String`)

| **Komponen** | **Spesifikasi** |
|--------------|-----------------|
| **Subclass/Object** | `Waiting` (object)<br>`OnGoing` (object)<br>`Completed` (object)<br>`Cancelled` (data class, properti: `reason: String`) |
| **Metode** | `display(): String` → abstrak<br>`isFinal(): Boolean` → concrete, return true jika `Completed` atau `Cancelled` |

#### 5. Ubah Kelas `Order`
- Ganti properti `_status: String` menjadi `status: OrderStatus` (var, default `OrderStatus.Waiting`).
- Hapus getter `getStatus()` karena status sekarang public (tapi tetap enkapsulasi via sealed class).
- Ubah metode `startTrip()`, `completeTrip()`, `cancelTrip()` menggunakan `OrderStatus`.

#### 6. Ubah Kelas `Payment`
- Ganti properti `_method: String` menjadi `method: PaymentMethod` (gunakan interface).
- Hapus `setMethod`, cukup set langsung di constructor atau setter.
- `processPayment()` sekarang memanggil `method.processPayment(amount)`.

---

### Ketentuan Khusus Soal 4

1. **Buat file**: `PaymentMethod.kt` (interface + implementasi), `PaymentResult.kt`, `OrderStatus.kt`.
2. **Perbarui** `Order.kt` dan `Payment.kt` sesuai perubahan.
3. **Buat fungsi `main()`** yang:
   - Buat list `List<Vehicle>` berisi `Car`, `Motorcycle`, `Truck` (polymorphic references).
   - Loop list, panggil `getType()` dan `calculateFare(10.0)`.
   - Gunakan `when` + `is` untuk mengecek jenis kendaraan (smart casting), lalu tampilkan properti spesifik (misal `fuelType` untuk Car).
   - Buat list `List<PaymentMethod>` berisi `CreditCard`, `QRIS`, `Cash`.
   - Proses pembayaran imajiner dengan nominal 100000, tampilkan hasil (gunakan `when` ekshaustif untuk `PaymentResult`).
   - Buat berbagai status `OrderStatus` (Waiting, Ongoing, Completed, Cancelled) dan gunakan `when` ekshaustif untuk mencetak `display()`.
   - **Demonstrasi `as?`**: coba casting Vehicle ke Car dengan aman, tampilkan hasil.

---

# SOAL 5: INTEGRASI SISTEM DAN FUNGSI MAIN LENGKAP

### Tujuan
Menggabungkan **semua kelas** yang sudah dibuat ke dalam satu sistem terintegrasi (`TransportSystem`) dan mendemonstrasikan seluruh fitur dalam skenario nyata.

### Yang Harus Dibuat

#### 1. Kelas `TransportSystem`

| **Komponen** | **Spesifikasi** |
|--------------|-----------------|
| **Properti** | `name: String` (val)<br>`vehicles: MutableList<Vehicle>` (private)<br>`drivers: MutableList<Driver>` (private)<br>`customers: MutableList<Customer>` (private)<br>`orders: MutableList<Order>` (private)<br>`payments: MutableList<Payment>` (private) |
| **Metode Manajemen** | `addVehicle(vehicle: Vehicle)`<br>`addDriver(driver: Driver)`<br>`addCustomer(customer: Customer)`<br>`findVehicle(plateNumber: String): Vehicle?`<br>`findDriver(id: String): Driver?`<br>`findCustomer(id: String): Customer?` |
| **Metode Operasi** | `createOrder(customerId: String, driverId: String, pickup: String, dest: String, distance: Double): Order?` → cari customer & driver, jika ada buat Order, tambahkan ke list, return order<br>`processPayment(orderId: String, method: PaymentMethod, paidAmount: Double): PaymentResult` → cari order, buat Payment, proses, simpan, return hasil<br>`completeOrder(orderId: String): Boolean`<br>`cancelOrder(orderId: String, reason: String): Boolean` |
| **Metode Laporan** | `displayAllVehicles()`<br>`displayAllDrivers()`<br>`displayAllCustomers()`<br>`displayAllOrders()`<br>`displayRevenueReport(): Unit` → total pendapatan dari semua order yang sudah selesai (status Completed) |

---

### Data Wajib untuk `main()` di Soal 5

**Kendaraan:**
1. Mobil: "B 1234 XYZ", "Toyota", "Innova", 2021, "Bensin", 4
2. Motor: "D 5678 ABC", "Honda", "Beat", 2022, 125, true
3. Truk: "E 9012 DEF", "Hino", "Dutro", 2020, 5.0, 2

**Driver:**
1. ID: D001, Nama: "Andi", Phone: "08123456789", Vehicle: Mobil
2. ID: D002, Nama: "Budi", Phone: "08129876543", Vehicle: Motor
3. ID: D003, Nama: "Citra", Phone: "08125678901", Vehicle: Truk

**Customer:**
1. ID: C001, Nama: "Dewi", Phone: "08134567890", Email: "dewi@email.com", Saldo: 100000
2. ID: C002, Nama: "Eko", Phone: "08135678901", Email: "eko@email.com", Saldo: 50000
3. ID: C003, Nama: "Fani", Phone: "08136789012", Email: "fani@email.com", Saldo: 200000

---

### Skenario Wajib di `main()` Soal 5

1. **Inisialisasi**: Buat `TransportSystem` dengan nama "Go-Transport 2024".
2. **Tambah Data**: Tambahkan semua kendaraan, driver, dan customer di atas.
3. **Tampilkan Data Awal**: Panggil `displayAllVehicles()`, `displayAllDrivers()`, `displayAllCustomers()`.
4. **Buat Pesanan 1**: Customer C001 (Dewi) memesan Driver D001 (Andi) dengan jarak 12 km dari "Kampus A" ke "Mall B".
5. **Buat Pesanan 2**: Customer C002 (Eko) memesan Driver D002 (Budi) dengan jarak 8 km dari "Stasiun" ke "Kantor".
6. **Buat Pesanan 3**: Customer C003 (Fani) memesan Driver D003 (Citra) dengan jarak 25 km dari "Gudang" ke "Pelabuhan".
7. **Tampilkan Semua Order**: Panggil `displayAllOrders()`.
8. **Proses Pembayaran Order 1**: Dewi membayar dengan metode **QRIS** dengan nominal sesuai tagihan.
9. **Proses Pembayaran Order 2**: Eko membayar dengan metode **Tunai** dengan nominal kurang (Rp 10.000 dari tagihan) → harus gagal. Kemudian top-up saldo Eko dan bayar lagi dengan **Kartu Kredit** (gunakan validasi kartu).
10. **Selesaikan Order 1**: Panggil `completeOrder(order1.id)`.
11. **Batalkan Order 3**: Fani membatalkan order dengan alasan "Hujan deras".
12. **Tampilkan Status Akhir**: Panggil `displayAllOrders()` lagi untuk melihat perubahan status.
13. **Tampilkan Laporan Pendapatan**: Panggil `displayRevenueReport()`.
14. **Demonstrasi Polimorfisme**: Loop `System.vehicles`, panggil `calculateFare(15.0)` untuk semua.
15. **Demonstrasi Smart Casting**: Cek apakah driver D001 punya kendaraan `Car`, jika ya tampilkan `fuelType`.
16. **Demonstrasi Sealed Class**: Buat variabel `OrderStatus` dan gunakan `when` untuk mencetak semua status yang mungkin.

---

## FORMAT PENGUMPULAN

### Struktur Folder

```
Tugas_Mandiri_OOP_NIM_Nama/
├── src/
│   ├── Main.kt                 (untuk semua soal, atau Main_Soal1.kt s/d Main_Soal5.kt)
│   ├── Vehicle.kt
│   ├── Car.kt
│   ├── Motorcycle.kt
│   ├── Truck.kt
│   ├── Driver.kt
│   ├── Customer.kt
│   ├── Order.kt
│   ├── OrderStatus.kt
│   ├── Payment.kt
│   ├── PaymentMethod.kt
│   ├── PaymentResult.kt
│   └── TransportSystem.kt
├── docs/
│   └── Laporan_Tugas_Mandiri.pdf
└── README.md
```

### Laporan (PDF)

Setiap **Soal (1-5)** harus memiliki bagian dalam laporan:
1. **Tujuan Soal** (konsep OOP yang dilatih).
2. **Penjelasan Kelas** (deskripsi singkat).
3. **Screenshot Output** (minimal 2 per soal).
4. **Analisis** (jawaban pertanyaan spesifik per soal).

---

## PERTANYAAN ANALISIS PER SOAL (WAJIB DIJAWAB DI LAPORAN)

| **Soal** | **Pertanyaan Analisis** |
|----------|--------------------------|
| **Soal 1** | 1. Apa perbedaan `val` dan `var`? Berikan contoh dari kode Anda.<br>2. Mengapa `calculateFare()` dibuat sebagai metode biasa (bukan `open` atau `abstract`) di Soal 1? |
| **Soal 2** | 1. Sebutkan 3 contoh enkapsulasi dalam kode Anda.<br>2. Apa manfaat `private set` dibandingkan `private val`?<br>3. Mengapa validasi penting di `setMethod()`? |
| **Soal 3** | 1. Mengapa `Vehicle` harus diubah menjadi `open class`?<br>2. Apa fungsi `super` dalam `displayInfo()` di `Car`?<br>3. Mengapa `calculateFare()` di-override di subclass? |
| **Soal 4** | 1. Apa perbedaan `interface` dan `abstract class`? Kapan menggunakan `interface`?<br>2. Mengapa `PaymentResult` dibuat `sealed class`?<br>3. Apa fungsi `as?` dalam smart casting? |
| **Soal 5** | 1. Bagaimana `TransportSystem` mengelola enkapsulasi data?<br>2. Di mana letak polimorfisme di `displayAllVehicles()`?<br>3. Mengapa `OrderStatus` menggunakan sealed class bukan enum? |

---

## KRITERIA PENILAIAN (5 Soal)

| **Kriteria** | **Bobot** | **Indikator** |
|--------------|-----------|---------------|
| **Kebenaran Kode per Soal** | 35% | Program berjalan tanpa error, semua fitur sesuai spesifikasi di setiap soal |
| **Implementasi 4 Pilar OOP** | 25% | Enkapsulasi, Pewarisan, Polimorfisme, Abstraksi diterapkan tepat di soal terkait |
| **Fungsi `main()`** | 15% | Mendemonstrasikan semua skenario wajib dengan output jelas dan terstruktur |
| **Dokumentasi KDoc** | 10% | KDoc lengkap di semua kelas, properti, dan metode publik |
| **Analisis OOP** | 10% | Jawaban pertanyaan analisis lengkap, akurat, dan mendalam |
| **Struktur & Laporan** | 5% | Struktur folder rapi, laporan lengkap dengan screenshot |

---

## PENUTUP

> **"Satu studi kasus yang dikerjakan secara bertahap akan membangun pemahaman OOP yang kokoh, dari dasar hingga sistem terintegrasi."**

Kerjakan **5 soal secara berurutan**. Jangan loncat ke Soal 5 sebelum menyelesaikan Soal 1-4, karena setiap soal membangun fondasi untuk soal berikutnya. Selamat mengerjakan!
