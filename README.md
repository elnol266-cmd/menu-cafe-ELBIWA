# ELBIWA VIEW - Digital Order & Cashier Management System ☕📉

**ELBIWA VIEW** adalah sistem manajemen kafe terintegrasi yang terdiri dari dua komponen utama: **Dashboard Kasir Pro** (untuk pihak manajemen/kasir) dan **Digital Order System** (untuk pembeli/pelanggan). Sistem ini dirancang mandiri menggunakan teknologi web modern dan terhubung secara *real-time* menggunakan **Firebase Realtime Database**.

---

## 🚀 Fitur Utama

### 1. Dashboard Kasir (`kasir.html`)
* **Keamanan Akses:** Dilengkapi halaman *login* terproteksi untuk admin/kasir.
* **Live Order Panel:** Memantau pesanan yang masuk dari *smartphone* pembeli secara *real-time* disertai notifikasi suara dan desktop.
* **Kasir Manual (Walk-in):** Fitur POS untuk melayani pelanggan yang memesan langsung di kasir dengan pengecekan batas stok otomatis.
* **Manajemen Stok & Katalog:** Modul CRUD (Create, Read, Update, Delete) untuk menambah menu, memperbarui harga, dan mengelola stok produk.
* **Cetak Struk Otomatis:** Integrasi cetak nota/struk belanja belanja ramah *printer thermal* (Media `@media print`).
* **Manajemen Karyawan:** Pendataan posisi staf (Kasir, Barista, Waiter, Kitchen) beserta pembagian *shift* kerja.
* **Analisis Finansial & Ekspor:** Grafik omzet interaktif berbasis Chart.js dan fitur *export* riwayat transaksi langsung ke format `.xlsx` (Excel).

### 2. Sistem Pemesanan Pembeli (`pembeli.html`)
* **Responsif & Mobile-Friendly:** Didesain khusus agar nyaman digunakan langsung dari HP pelanggan melalui pemindaian kode QR di meja.
* **Self-Service Ordering:** Pelanggan dapat memilih menu, memantau sisa stok secara langsung, dan menentukan kuantitas pesanan.
* **Validasi Meja:** Sistem mencegah pengiriman pesanan jika nomor meja dan nama pelanggan belum terisi.

---

## 🛠️ Arsitektur Teknologi

Aplikasi ini dibangun tanpa memerlukan *backend* server terpisah (*serverless architecture*) dengan memanfaatkan teknologi berikut:

* **Frontend:** HTML5, CSS3 (Custom Glassmorphism & Stone UI Theme), JavaScript (ES6+)
* **Database:** Firebase Realtime Database (v8.10.1)
* **Library Pihak Ketiga:**
    * [FontAwesome v6.4.0](https://fontawesome.com/) - Ikon antarmuka.
    * [Chart.js](https://www.chartjs.org/) - Visualisasi grafik omzet pendapatan.
    * [SheetJS (XLSX)](https://sheetjs.com/) - Generator laporan Excel di sisi klien.
    * Google Fonts - Inter & Playfair Display.

---

## 🗄️ Struktur Basis Data (Firebase RTDB JSON)

Sistem ini menggunakan struktur data NoSQL terpusat sebagai berikut:

```json
{
  "produk": {
    "product_id_1": {
      "nama_produk": "Es Kopi Susu Elbiwa",
      "harga": 18000,
      "stok": 45,
      "gambar": "[https://url-gambar.com/kopi.jpg](https://url-gambar.com/kopi.jpg)"
    }
  },
  "pesanan_masuk": {
    "order_id_1": {
      "nama_pelanggan": "Andi",
      "nomor_meja": "3",
      "status": "Pending",
      "total_bayar": 36000,
      "items": [
        {
          "nama": "Es Kopi Susu Elbiwa",
          "jumlah": 2
        }
      ]
    }
  },
  "riwayat_pendapatan": {
    "history_id_1": {
      "Waktu": "30/06/2026, 11.00.00",
      "Tipe": "Online (Meja 3)",
      "Menu": "Es Kopi Susu Elbiwa (x2)",
      "Total": 36000
    }
  },
  "karyawan": {
    "emp_id_1": {
      "name": "Budi",
      "pos": "Barista",
      "shift": "Pagi"
    }
