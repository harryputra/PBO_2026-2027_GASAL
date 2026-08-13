# TUGAS PRAKTIKUM KELOMPOK - PEMROGRAMAN BERORIENTASI OBJEK

## Sistem Manajemen E-Commerce

---

## A. PENDAHULUAN

### 1.1 Deskripsi Tugas

Selamat! Anda telah mempelajari empat pilar utama Pemrograman Berorientasi Objek (OOP):
- **Pertemuan 1**: Konsep Dasar OOP (Kelas, Objek, Atribut, Metode)
- **Pertemuan 2**: Enkapsulasi (Access Modifier, Getter/Setter, Private Setter)
- **Pertemuan 3**: Pewarisan (Inheritance, `open`, `override`, `super`)
- **Pertemuan 4**: Polimorfisme (Polymorphic References, Smart Casting, Sealed Class)

Sekarang saatnya Anda mengimplementasikan **semua konsep tersebut** dalam satu proyek kelompok yang komprehensif!

### 1.2 Tujuan Tugas

- Menerapkan **Enkapsulasi** untuk melindungi data sensitif
- Menerapkan **Pewarisan** untuk membangun hierarki kelas
- Menerapkan **Polimorfisme** untuk menangani berbagai jenis objek
- Menerapkan **Sealed Class** untuk status yang terbatas
- Menerapkan **Smart Casting** untuk penanganan tipe yang aman
- Bekerja sama dalam tim untuk mengembangkan sistem yang terstruktur

---

## B. STUDI KASUS: SISTEM MANAJEMEN E-COMMERCE

### 2.1 Deskripsi Sistem

Anda diminta untuk membangun sistem manajemen **toko online (e-commerce)** sederhana. Sistem ini harus dapat mengelola:

1. **Produk** dengan berbagai kategori (Elektronik, Pakaian, Makanan)
2. **Keranjang Belanja** untuk menyimpan produk yang akan dibeli
3. **Pesanan** dengan status yang berbeda-beda
4. **Pengguna** yang melakukan pembelian
5. **Metode Pembayaran** yang berbeda-beda

### 2.2 Fitur yang Harus Diimplementasikan

| **Fitur** | **Deskripsi** |
|-----------|---------------|
| Manajemen Produk | Menambah, mencari, dan menampilkan produk |
| Kategori Produk | Produk memiliki kategori dengan perilaku berbeda |
| Keranjang Belanja | Menambah, menghapus, dan menghitung total belanja |
| Proses Checkout | Mengubah keranjang menjadi pesanan |
| Status Pesanan | Melacak status pesanan (Pending, Paid, Shipped, Delivered, Cancelled) |
| Metode Pembayaran | Berbagai metode pembayaran (Kartu Kredit, QRIS, Transfer Bank) |
| Diskon Produk | Produk tertentu memiliki diskon khusus |
| Laporan Penjualan | Menampilkan ringkasan penjualan |

---

## C. SPESIFIKASI KELAS

### 3.1 Kelas `Product` (Kelas Induk)

```kotlin
abstract class Product(
    val id: String,
    val name: String,
    private var price: Double,
    var stock: Int
) {
    // ============================================================
    // PROPERTI
    // ============================================================

    // Getter untuk price dengan format
    val formattedPrice: String
        get() = "Rp ${formatRupiah(price)}"

    // ============================================================
    // METODE ABSTRAK
    // ============================================================

    // Menghitung diskon — harus diimplementasikan oleh subclass
    abstract fun calculateDiscount(): Double

    // Mendapatkan kategori produk
    abstract fun getCategory(): String

    // ============================================================
    // METODE CONCRETE (Bisa digunakan semua subclass)
    // ============================================================

    // Harga setelah diskon
    open fun getDiscountedPrice(): Double {
        return price - calculateDiscount()
    }

    // Menampilkan info produk
    open fun displayInfo() {
        println("=" .repeat(50))
        println("📦 ${getCategory()} - $name")
        println("ID        : $id")
        println("Harga     : $formattedPrice")
        println("Diskon    : Rp ${formatRupiah(calculateDiscount())}")
        println("Harga Akhir: Rp ${formatRupiah(getDiscountedPrice())}")
        println("Stok      : $stock")
        println("=" .repeat(50))
    }

    // Mengurangi stok
    fun reduceStock(quantity: Int): Boolean {
        return if (stock >= quantity) {
            stock -= quantity
            true
        } else {
            false
        }
    }

    // ============================================================
    // HELPER METHOD (Protected)
    // ============================================================

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
```

### 3.2 Subclass `ElectronicProduct`

```kotlin
class ElectronicProduct(
    id: String,
    name: String,
    price: Double,
    stock: Int,
    val brand: String,
    val warrantyMonths: Int,  // Durasi garansi dalam bulan
    val isPremium: Boolean    // Premium mendapat diskon ekstra
) : Product(id, name, price, stock) {

    override fun calculateDiscount(): Double {
        var discount = 0.0

        // Diskon dasar: 5% untuk semua elektronik
        discount += price * 0.05

        // Diskon tambahan: 10% jika premium
        if (isPremium) {
            discount += price * 0.10
        }

        // Diskon tambahan: 5% jika garansi > 24 bulan
        if (warrantyMonths > 24) {
            discount += price * 0.05
        }

        return discount
    }

    override fun getCategory(): String = "Elektronik"

    override fun displayInfo() {
        super.displayInfo()
        println("Merek     : $brand")
        println("Garansi   : $warrantyMonths bulan")
        println("Premium   : ${if (isPremium) "✅ Ya" else "❌ Tidak"}")
        println("=" .repeat(50))
    }
}
```

### 3.3 Subclass `ClothingProduct`

```kotlin
class ClothingProduct(
    id: String,
    name: String,
    price: Double,
    stock: Int,
    val size: String,
    val material: String,
    val isSeasonal: Boolean  // Seasonal mendapat diskon khusus
) : Product(id, name, price, stock) {

    override fun calculateDiscount(): Double {
        var discount = 0.0

        // Diskon dasar: 10% untuk semua pakaian
        discount += price * 0.10

        // Diskon tambahan: 15% jika seasonal
        if (isSeasonal) {
            discount += price * 0.15
        }

        // Diskon tambahan: 5% untuk size XL atau lebih besar
        if (size.uppercase() in listOf("XL", "XXL", "XXXL")) {
            discount += price * 0.05
        }

        return discount
    }

    override fun getCategory(): String = "Pakaian"

    override fun displayInfo() {
        super.displayInfo()
        println("Ukuran    : $size")
        println("Bahan     : $material")
        println("Seasonal  : ${if (isSeasonal) "✅ Ya" else "❌ Tidak"}")
        println("=" .repeat(50))
    }
}
```

### 3.4 Subclass `FoodProduct`

```kotlin
class FoodProduct(
    id: String,
    name: String,
    price: Double,
    stock: Int,
    val expiryDate: String,
    val weight: Double,  // dalam gram
    val isOrganic: Boolean
) : Product(id, name, price, stock) {

    override fun calculateDiscount(): Double {
        var discount = 0.0

        // Diskon dasar: 5% untuk semua makanan
        discount += price * 0.05

        // Diskon tambahan: 20% jika organik
        if (isOrganic) {
            discount += price * 0.20
        }

        return discount
    }

    override fun getCategory(): String = "Makanan"

    override fun displayInfo() {
        super.displayInfo()
        println("Berat     : $weight gram")
        println("Kadaluarsa: $expiryDate")
        println("Organik   : ${if (isOrganic) "✅ Ya" else "❌ Tidak"}")
        println("=" .repeat(50))
    }
}
```

### 3.5 Kelas `ShoppingCart`

```kotlin
class ShoppingCart(private val owner: String) {
    // ============================================================
    // PROPERTI
    // ============================================================

    private val items = mutableMapOf<Product, Int>()  // Product → Quantity
    var totalItems: Int = 0
        private set

    // ============================================================
    // METODE
    // ============================================================

    fun addItem(product: Product, quantity: Int): Boolean {
        if (quantity <= 0) {
            println("❌ Jumlah harus lebih dari 0")
            return false
        }

        if (!product.reduceStock(quantity)) {
            println("❌ Stok tidak mencukupi (tersedia: ${product.stock})")
            return false
        }

        items[product] = items.getOrDefault(product, 0) + quantity
        totalItems += quantity
        println("✅ ${product.name} x$quantity ditambahkan ke keranjang")
        return true
    }

    fun removeItem(product: Product): Boolean {
        val quantity = items[product] ?: return false
        items.remove(product)
        totalItems -= quantity
        // Kembalikan stok
        product.reduceStock(-quantity)
        println("✅ ${product.name} dihapus dari keranjang")
        return true
    }

    fun getTotalPrice(): Double {
        return items.entries.sumOf { (product, quantity) ->
            product.getDiscountedPrice() * quantity
        }
    }

    fun getTotalDiscount(): Double {
        return items.entries.sumOf { (product, quantity) ->
            product.calculateDiscount() * quantity
        }
    }

    fun getItems(): Map<Product, Int> = items

    fun isEmpty(): Boolean = items.isEmpty()

    fun displayCart() {
        println("=" .repeat(50))
        println("🛒 KERANJANG BELANJA - $owner")
        println("=" .repeat(50))

        if (items.isEmpty()) {
            println("   Keranjang kosong")
        } else {
            items.forEach { (product, quantity) ->
                println("${product.name} x$quantity = Rp ${formatRupiah(product.getDiscountedPrice() * quantity)}")
                println("   (Diskon: Rp ${formatRupiah(product.calculateDiscount() * quantity)})")
            }
            println("-" .repeat(50))
            println("Total Diskon : Rp ${formatRupiah(getTotalDiscount())}")
            println("Total Belanja: Rp ${formatRupiah(getTotalPrice())}")
        }
        println("=" .repeat(50))
    }

    private fun formatRupiah(nominal: Double): String {
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
```

### 3.6 Sealed Class `OrderStatus`

```kotlin
sealed class OrderStatus {
    object Pending : OrderStatus() {
        override fun display() = "⏳ Menunggu Pembayaran"
    }
    object Paid : OrderStatus() {
        override fun display() = "✅ Dibayar"
    }
    object Shipped : OrderStatus() {
        override fun display() = "🚚 Dikirim"
    }
    object Delivered : OrderStatus() {
        override fun display() = "📦 Diterima"
    }
    data class Cancelled(val reason: String) : OrderStatus() {
        override fun display() = "❌ Dibatalkan: $reason"
    }

    abstract fun display(): String

    fun isFinal(): Boolean {
        return this is Delivered || this is Cancelled
    }
}
```

### 3.7 Kelas `Order`

```kotlin
class Order(
    val id: String,
    val customerName: String,
    val items: Map<Product, Int>,
    var status: OrderStatus = OrderStatus.Pending
) {
    // ============================================================
    // PROPERTI
    // ============================================================

    val totalPrice: Double
        get() = items.entries.sumOf { (product, quantity) ->
            product.getDiscountedPrice() * quantity
        }

    val totalDiscount: Double
        get() = items.entries.sumOf { (product, quantity) ->
            product.calculateDiscount() * quantity
        }

    val createdAt: String = java.time.LocalDateTime.now().toString()

    // ============================================================
    // METODE
    // ============================================================

    fun updateStatus(newStatus: OrderStatus): Boolean {
        if (status.isFinal()) {
            println("❌ Status sudah final, tidak bisa diubah")
            return false
        }
        status = newStatus
        println("✅ Status order $id diubah menjadi: ${status.display()}")
        return true
    }

    fun displayOrder() {
        println("=" .repeat(55))
        println("📋 DETAIL ORDER")
        println("=" .repeat(55))
        println("ID Order    : $id")
        println("Pelanggan   : $customerName")
        println("Tanggal     : $createdAt")
        println("Status      : ${status.display()}")
        println("-" .repeat(55))
        println("Items:")
        items.forEach { (product, quantity) ->
            println("   ${product.name} x$quantity = Rp ${formatRupiah(product.getDiscountedPrice() * quantity)}")
        }
        println("-" .repeat(55))
        println("Total Diskon: Rp ${formatRupiah(totalDiscount)}")
        println("Total Harga : Rp ${formatRupiah(totalPrice)}")
        println("=" .repeat(55))
    }

    private fun formatRupiah(nominal: Double): String {
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
```

### 3.8 Interface `PaymentMethod`

```kotlin
interface PaymentMethod {
    val name: String
    fun processPayment(amount: Double): PaymentResult
    fun getFee(amount: Double): Double
}

// Sealed class untuk hasil pembayaran
sealed class PaymentResult {
    data class Success(val transactionId: String) : PaymentResult()
    data class Failed(val reason: String, val errorCode: Int) : PaymentResult()
    object Pending : PaymentResult()
}
```

### 3.9 Implementasi PaymentMethod

```kotlin
class CreditCardPayment(
    private val cardNumber: String,
    private val expiryDate: String,
    private val cvv: String
) : PaymentMethod {
    override val name = "Kartu Kredit"

    override fun getFee(amount: Double): Double {
        return amount * 0.02  // 2% fee
    }

    override fun processPayment(amount: Double): PaymentResult {
        if (cardNumber.length < 16) {
            return PaymentResult.Failed("Nomor kartu tidak valid", 401)
        }
        if (cvv.length != 3) {
            return PaymentResult.Failed("CVV tidak valid", 402)
        }
        return PaymentResult.Success("CC-${System.currentTimeMillis()}")
    }
}

class QRISPayment(
    private val qrCode: String,
    private val merchantId: String
) : PaymentMethod {
    override val name = "QRIS"

    override fun getFee(amount: Double): Double {
        return amount * 0.005  // 0.5% fee
    }

    override fun processPayment(amount: Double): PaymentResult {
        if (qrCode.length < 10) {
            return PaymentResult.Failed("Kode QR tidak valid", 403)
        }
        return PaymentResult.Success("QR-${System.currentTimeMillis()}")
    }
}

class BankTransferPayment(
    private val bankName: String,
    private val accountNumber: String
) : PaymentMethod {
    override val name = "Transfer Bank"

    override fun getFee(amount: Double): Double {
        val fee = amount * 0.01  // 1%
        return maxOf(fee, 5000.0)  // Minimal Rp 5.000
    }

    override fun processPayment(amount: Double): PaymentResult {
        if (accountNumber.length < 8) {
            return PaymentResult.Failed("Nomor rekening tidak valid", 404)
        }
        return PaymentResult.Success("BT-${System.currentTimeMillis()}")
    }
}
```

### 3.10 Kelas `User`

```kotlin
class User(
    val username: String,
    val email: String,
    private val password: String  // Encapsulated!
) {
    // ============================================================
    // PROPERTI
    // ============================================================

    private val orders = mutableListOf<Order>()
    private val cart = ShoppingCart(username)

    val orderCount: Int
        get() = orders.size

    val totalSpent: Double
        get() = orders.sumOf { it.totalPrice }

    // ============================================================
    // METODE
    // ============================================================

    fun authenticate(inputPassword: String): Boolean {
        return password == inputPassword
    }

    fun getCart(): ShoppingCart = cart

    fun checkout(paymentMethod: PaymentMethod): Order? {
        if (cart.isEmpty()) {
            println("❌ Keranjang kosong")
            return null
        }

        val amount = cart.getTotalPrice()
        println("💳 Memproses pembayaran dengan ${paymentMethod.name}...")

        val result = paymentMethod.processPayment(amount)
        when (result) {
            is PaymentResult.Success -> {
                println("✅ Pembayaran berhasil! ID: ${result.transactionId}")
                val order = createOrder()
                orders.add(order)
                println("✅ Order ${order.id} berhasil dibuat")
                return order
            }
            is PaymentResult.Failed -> {
                println("❌ Pembayaran gagal: ${result.reason}")
                return null
            }
            PaymentResult.Pending -> {
                println("⏳ Pembayaran pending...")
                // Kembalikan stok
                // ...
                return null
            }
        }
    }

    private fun createOrder(): Order {
        val orderId = "ORD-${System.currentTimeMillis()}"
        val items = cart.getItems()
        val order = Order(orderId, username, items)
        // Kosongkan keranjang
        // cart.clear()
        return order
    }

    fun displayOrders() {
        println("=" .repeat(50))
        println("📋 RIWAYAT ORDER - $username")
        println("=" .repeat(50))

        if (orders.isEmpty()) {
            println("   Belum ada order")
        } else {
            orders.forEachIndexed { index, order ->
                println("${index + 1}. Order ${order.id} - ${order.status.display()}")
                println("   Total: Rp ${formatRupiah(order.totalPrice)}")
            }
        }
        println("Total Belanja: Rp ${formatRupiah(totalSpent)}")
        println("=" .repeat(50))
    }

    private fun formatRupiah(nominal: Double): String {
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
```

### 3.11 Kelas `ECommerceSystem` (Main Controller)

```kotlin
class ECommerceSystem(val name: String = "Toko Online") {
    // ============================================================
    // PROPERTI
    // ============================================================

    private val products = mutableListOf<Product>()
    private val users = mutableListOf<User>()
    private val orders = mutableListOf<Order>()

    // ============================================================
    // MANAJEMEN PRODUK
    // ============================================================

    fun addProduct(product: Product) {
        products.add(product)
        println("✅ Produk ${product.name} ditambahkan")
    }

    fun searchProduct(keyword: String): List<Product> {
        return products.filter {
            it.name.lowercase().contains(keyword.lowercase()) ||
            it.id.lowercase().contains(keyword.lowercase())
        }
    }

    fun findProductById(id: String): Product? {
        return products.find { it.id == id }
    }

    fun displayAllProducts() {
        println("=" .repeat(55))
        println("📦 SEMUA PRODUK")
        println("=" .repeat(55))
        println("Total: ${products.size} produk")
        println("-" .repeat(55))

        products.forEach { product ->
            product.displayInfo()
        }
    }

    // ============================================================
    // MANAJEMEN USER
    // ============================================================

    fun registerUser(username: String, email: String, password: String): Boolean {
        if (users.any { it.username == username }) {
            println("❌ Username $username sudah digunakan")
            return false
        }
        val user = User(username, email, password)
        users.add(user)
        println("✅ User $username berhasil didaftarkan")
        return true
    }

    fun findUser(username: String): User? {
        return users.find { it.username == username }
    }

    // ============================================================
    // MANAJEMEN ORDER
    // ============================================================

    fun addOrder(order: Order) {
        orders.add(order)
    }

    fun getTotalRevenue(): Double {
        return orders.sumOf { it.totalPrice }
    }

    fun getOrderCount(): Int = orders.size

    fun displaySalesReport() {
        println("=" .repeat(55))
        println("📊 LAPORAN PENJUALAN")
        println("=" .repeat(55))
        println("Total Order   : $orderCount")
        println("Total Revenue : Rp ${formatRupiah(getTotalRevenue())}")
        println("-" .repeat(55))

        if (orders.isEmpty()) {
            println("   Belum ada penjualan")
        } else {
            orders.forEachIndexed { index, order ->
                println("${index + 1}. ${order.id} - ${order.customerName}")
                println("   Status: ${order.status.display()}")
                println("   Total: Rp ${formatRupiah(order.totalPrice)}")
            }
        }
        println("=" .repeat(55))
    }

    private fun formatRupiah(nominal: Double): String {
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
```

---

## D. KETENTUAN TUGAS

### 4.1 Yang Harus Dikerjakan

| **No** | **Komponen** | **Status** |
|--------|--------------|------------|
| 1 | Kelas `Product` (abstract) | ✅ Disiapkan |
| 2 | Kelas `ElectronicProduct` | ✅ Disiapkan |
| 3 | Kelas `ClothingProduct` | ✅ Disiapkan |
| 4 | Kelas `FoodProduct` | ✅ Disiapkan |
| 5 | Kelas `ShoppingCart` | ✅ Disiapkan |
| 6 | Sealed Class `OrderStatus` | ✅ Disiapkan |
| 7 | Kelas `Order` | ✅ Disiapkan |
| 8 | Interface `PaymentMethod` | ✅ Disiapkan |
| 9 | Implementasi `PaymentMethod` | ✅ Disiapkan |
| 10 | Kelas `User` | ✅ Disiapkan |
| 11 | Kelas `ECommerceSystem` | ✅ Disiapkan |
| 12 | **Fungsi `main()` Demo** | **✏️ HARUS DIBUAT** |
| 13 | **Dokumentasi Kode** | **✏️ HARUS DIBUAT** |
| 14 | **Laporan Tugas** | **✏️ HARUS DIBUAT** |

### 4.2 Yang Harus Dibuat Kelompok

#### A. Fungsi `main()` Demo

Buat fungsi `main()` yang mendemonstrasikan **seluruh fitur** sistem:

```kotlin
fun main() {
    // 1. Inisialisasi sistem
    val system = ECommerceSystem("Toko Online Kampus")

    // 2. Tambahkan produk (minimal 6 produk, 2 dari setiap kategori)
    //    - 2 Elektronik (1 premium, 1 non-premium)
    //    - 2 Pakaian (1 seasonal, 1 non-seasonal)
    //    - 2 Makanan (1 organik, 1 non-organik)

    // 3. Register user (minimal 2 user)

    // 4. Tampilkan semua produk

    // 5. User 1: Menambahkan produk ke keranjang
    //    - Tambah beberapa produk dengan quantity berbeda

    // 6. User 1: Tampilkan keranjang

    // 7. User 1: Checkout dengan metode pembayaran
    //    - Pilih metode pembayaran (Credit Card / QRIS / Transfer Bank)
    //    - Tampilkan hasil pembayaran

    // 8. Tampilkan order user 1

    // 9. User 2: Lakukan hal yang sama

    // 10. Tampilkan laporan penjualan sistem

    // 11. Demonstrasi polimorfisme:
    //     - Buat List<Product> berisi berbagai produk
    //     - Loop dan panggil calculateDiscount() (polymorphic behavior)
    //     - Gunakan when + is untuk menampilkan kategori spesifik

    // 12. Demonstrasi sealed class:
    //     - Buat beberapa OrderStatus
    //     - Gunakan when expression ekshaustif

    // 13. Demonstrasi encapsulation:
    //     - Tunjukkan bahwa properti private tidak bisa diakses langsung

    // 14. Demonstrasi smart casting:
    //     - Casting dengan as? yang aman
}
```

#### B. Dokumentasi Kode

Setiap kelas, properti, dan metode harus memiliki **dokumentasi** menggunakan **KDoc** (Kotlin Documentation):

```kotlin
/**
 * Kelas untuk merepresentasikan produk di sistem e-commerce
 *
 * @property id ID unik produk
 * @property name Nama produk
 * @property price Harga produk (private)
 * @property stock Jumlah stok produk
 */
abstract class Product(
    // ...
) {
    /**
     * Menghitung diskon yang berlaku untuk produk
     *
     * Implementasi diskon berbeda-beda tergantung kategori produk
     *
     * @return Jumlah diskon dalam Rupiah
     */
    abstract fun calculateDiscount(): Double

    // ...
}
```

#### C. Laporan Tugas

Buat laporan dengan struktur:

1. **Cover** — Judul, Nama Kelompok, NIM, Dosen Pengampu
2. **Pendahuluan** — Latar belakang, tujuan, ruang lingkup
3. **Desain Sistem** — Diagram kelas, deskripsi kelas
4. **Implementasi** — Penjelasan kode per modul
5. **Demonstrasi** — Screenshot/output program
6. **Analisis OOP** — Analisis penerapan 4 pilar OOP
7. **Kesimpulan** — Kesimpulan dan saran
8. **Lampiran** — Kode lengkap

### 4.3 Analisis OOP

Kelompok harus menjelaskan **penerapan 4 pilar OOP**:

| **Pilar** | **Contoh Penerapan** |
|-----------|----------------------|
| **Enkapsulasi** | Properti `private` di `Product.price`, `User.password`, setter private |
| **Pewarisan** | `ElectronicProduct`, `ClothingProduct`, `FoodProduct` mewarisi `Product` |
| **Polimorfisme** | `Product` references menampung berbagai subclass, `calculateDiscount()` |
| **Abstraksi** | `abstract class Product`, `interface PaymentMethod` |

---

## E. KETENTUAN PENGUMPULAN

### 5.1 Format Pengumpulan

| **Item** | **Format** | **Keterangan** |
|----------|------------|----------------|
| Kode Program | File `.kt` | Satu file atau multiple file |
| Laporan | PDF | Maksimal 20 halaman |
| Screenshot Output | Embed di laporan | Minimal 10 screenshot |
| README | `.md` atau `.txt` | Cara menjalankan program |

### 5.2 Struktur Folder

```
Tugas_OOP_Group_X/
├── src/
│   ├── Main.kt
│   ├── product/
│   │   ├── Product.kt
│   │   ├── ElectronicProduct.kt
│   │   ├── ClothingProduct.kt
│   │   └── FoodProduct.kt
│   ├── cart/
│   │   └── ShoppingCart.kt
│   ├── order/
│   │   ├── Order.kt
│   │   └── OrderStatus.kt
│   ├── payment/
│   │   ├── PaymentMethod.kt
│   │   ├── CreditCardPayment.kt
│   │   ├── QRISPayment.kt
│   │   └── BankTransferPayment.kt
│   ├── user/
│   │   └── User.kt
│   └── system/
│       └── ECommerceSystem.kt
├── docs/
│   └── Laporan_Tugas_OOP.pdf
├── README.md
└── .gitignore
```

---

## F. KRITERIA PENILAIAN

### 6.1 Rubrik Penilaian

| **Kriteria** | **Bobot** | **Skor Maks** | **Indikator** |
|--------------|-----------|---------------|---------------|
| **Kode Program** | 40% | 40 | Kode berjalan tanpa error, semua fitur terimplementasi |
| **OOP Implementation** | 30% | 30 | 4 pilar OOP diimplementasikan dengan benar |
| **Dokumentasi** | 15% | 15 | KDoc lengkap, kode terbaca, naming convention |
| **Laporan** | 10% | 10 | Struktur lengkap, analisis mendalam |
| **Kerapian & Struktur** | 5% | 5 | Struktur folder rapi, file terorganisir |

### 6.2 Detail Penilaian

#### A. Kode Program (40%)

| **Aspek** | **Bobot** |
|-----------|-----------|
| Semua kelas diimplementasikan sesuai spesifikasi | 20% |
| Fungsi `main()` mendemonstrasikan semua fitur | 10% |
| Program berjalan tanpa error | 5% |
| Output jelas dan informatif | 5% |

#### B. OOP Implementation (30%)

| **Aspek** | **Bobot** |
|-----------|-----------|
| Enkapsulasi (private, private set, getter/setter) | 10% |
| Pewarisan (open class, override, super) | 10% |
| Polimorfisme (polymorphic references, smart casting) | 5% |
| Abstraksi (abstract class, interface) | 5% |

#### C. Dokumentasi (15%)

| **Aspek** | **Bobot** |
|-----------|-----------|
| KDoc untuk setiap kelas, properti, metode | 10% |
| Naming convention yang benar | 5% |

#### D. Laporan (10%)

| **Aspek** | **Bobot** |
|-----------|-----------|
| Struktur lengkap dan rapi | 5% |
| Analisis OOP mendalam | 5% |

---

## G. TIMELINE

| **Minggu** | **Aktivitas** | **Deadline** |
|------------|---------------|--------------|
| Minggu 1 | Pembagian tugas, desain sistem, setup project | - |
| Minggu 2 | Implementasi kelas dasar (Product, subclass) | - |
| Minggu 3 | Implementasi keranjang, order, sealed class | - |
| Minggu 4 | Implementasi payment, user, sistem | - |
| Minggu 5 | Pembuatan fungsi main(), testing | - |
| Minggu 6 | Dokumentasi, laporan, finalisasi | **Pengumpulan** |

---

## H. PANDUAN KERJA KELOMPOK

### 7.1 Pembagian Tugas (Rekomendasi)

| **Role** | **Tugas** |
|----------|-----------|
| **Project Lead** | Koordinasi, integrasi kode, fungsi main() |
| **Backend Developer 1** | Product, ElectronicProduct, ClothingProduct, FoodProduct |
| **Backend Developer 2** | ShoppingCart, Order, OrderStatus |
| **Payment Developer** | PaymentMethod, implementasi payment |
| **System Developer** | User, ECommerceSystem |
| **Documentation Lead** | KDoc, Laporan, README |

### 7.2 Alur Kerja yang Disarankan

1. **Fork** repository yang diberikan
2. **Clone** ke komputer masing-masing
3. Buat **branch** masing-masing
4. Push kode ke branch masing-masing
5. Lakukan **Pull Request** ke branch utama
6. Lakukan **Code Review** oleh anggota lain

### 7.3 Komunikasi Tim

- Gunakan **WhatsApp/Telegram Group** untuk komunikasi harian
- Gunakan **GitHub Issues** untuk tracking tugas
- Lakukan **daily standup** (15 menit) setiap hari

---

## I. CONTOH OUTPUT YANG DIHARAPKAN

### 8.1 Output Fungsi `main()`

```
=======================================================
🛍️ SELAMAT DATANG DI TOKO ONLINE KAMPUS
=======================================================

--- MENAMBAHKAN PRODUK ---
✅ Produk Laptop Gaming ditambahkan
✅ Produk Smartphone Premium ditambahkan
✅ Produk Jaket Musim Dingin ditambahkan
✅ Produk Kaos Polos ditambahkan
✅ Produk Beras Organik ditambahkan
✅ Produk Mie Instan ditambahkan

--- REGISTRASI USER ---
✅ User budi berhasil didaftarkan
✅ User siti berhasil didaftarkan

--- SEMUA PRODUK ---
=======================================================
📦 SEMUA PRODUK
=======================================================
Total: 6 produk
-------------------------------------------------------
==================================================
📦 Elektronik - Laptop Gaming
ID        : E001
Harga     : Rp 15.000.000
Diskon    : Rp 2.250.000
Harga Akhir: Rp 12.750.000
Stok      : 10
Merek     : ASUS
Garansi   : 36 bulan
Premium   : ✅ Ya
==================================================
... (dan seterusnya)

--- BUDI BELANJA ---
✅ Laptop Gaming x1 ditambahkan ke keranjang
✅ Jaket Musim Dingin x2 ditambahkan ke keranjang

--- KERANJANG BUDI ---
==================================================
🛒 KERANJANG BELANJA - budi
==================================================
Laptop Gaming x1 = Rp 12.750.000
   (Diskon: Rp 2.250.000)
Jaket Musim Dingin x2 = Rp 680.000
   (Diskon: Rp 120.000)
--------------------------------------------------
Total Diskon : Rp 2.370.000
Total Belanja: Rp 13.430.000
==================================================

--- CHECKOUT BUDI ---
💳 Memproses pembayaran dengan Kartu Kredit...
✅ Pembayaran berhasil! ID: CC-1700000000000
✅ Order ORD-1700000000001 berhasil dibuat

... (dan seterusnya)
```

---

## J. PERTANYAAN YANG SERING DIAJUKAN (FAQ)

### Q1: Apakah boleh menambahkan fitur tambahan di luar spesifikasi?

**A:** Boleh, selama semua fitur wajib terpenuhi. Fitur tambahan akan menjadi nilai plus.

### Q2: Apakah boleh menggunakan library eksternal?

**A:** Sebaiknya tidak. Gunakan Kotlin standard library saja untuk fokus pada OOP concepts.

### Q3: Berapa maksimal anggota kelompok?

**A:** Maksimal 4-5 orang per kelompok.

### Q4: Apakah kode harus dalam satu file atau multiple file?

**A:** Multiple file (terstruktur) lebih baik dan akan mendapat nilai tambah.

### Q5: Apakah laporan harus dalam bahasa Indonesia atau Inggris?

**A:** Bahasa Indonesia, dengan istilah teknis boleh dalam bahasa Inggris.

---

## K. PENUTUP

Selamat mengerjakan tugas praktikum kelompok! Semoga tugas ini membantu Anda memahami dan mengimplementasikan konsep OOP secara komprehensif. Jangan ragu untuk bertanya kepada dosen atau asisten praktikum jika ada kesulitan.

> **"Kode yang baik bukanlah kode yang berfungsi, tetapi kode yang dapat dipahami dan dikelola oleh orang lain."**

---

**Disusun oleh,**

[Nama Dosen Pengampu]
Dosen Program Studi D4 Teknologi Rekayasa Informatika Industri

---

## L. LAMPIRAN: TEMPLATE LAPORAN

# LAPORAN TUGAS PRAKTIKUM OOP

## Sistem Manajemen E-Commerce

---

### Kelompok X

| **No** | **Nama** | **NIM** | **Role** |
|--------|----------|---------|----------|
| 1 | [Nama] | [NIM] | [Role] |
| 2 | [Nama] | [NIM] | [Role] |
| 3 | [Nama] | [NIM] | [Role] |
| 4 | [Nama] | [NIM] | [Role] |
| 5 | [Nama] | [NIM] | [Role] |

---

### Dosen Pengampu
[Nama Dosen Pengampu]

### Mata Kuliah
Pemrograman Berorientasi Objek (OOP)

### Tanggal Pengumpulan
[Tanggal]

---

## BAB I: PENDAHULUAN

### 1.1 Latar Belakang
...

### 1.2 Tujuan
...

### 1.3 Ruang Lingkup
...

---

## BAB II: DESAIN SISTEM

### 2.1 Diagram Kelas
...

### 2.2 Deskripsi Kelas
...

---

## BAB III: IMPLEMENTASI

### 3.1 Kelas Product
...

### 3.2 Kelas ElectronicProduct
...

### 3.3 ... (dst)
...

---

## BAB IV: DEMONSTRASI

### 4.1 Output Program
...

### 4.2 Analisis Skenario
...

---

## BAB V: ANALISIS OOP

### 5.1 Enkapsulasi
...

### 5.2 Pewarisan
...

### 5.3 Polimorfisme
...

### 5.4 Abstraksi
...

---

## BAB VI: KESIMPULAN

### 6.1 Kesimpulan
...

### 6.2 Saran
...

---

## LAMPIRAN: KODE LENGKAP

... (Kode lengkap)

---

**Penutup**

Demikian laporan tugas praktikum OOP ini kami buat. Semoga dapat memberikan manfaat dan menjadi referensi bagi pembaca. Kami menyadari bahwa laporan ini masih memiliki kekurangan, oleh karena itu kritik dan saran yang membangun sangat kami harapkan.

---

**Hormat kami,**

[Nama Ketua Kelompok]
