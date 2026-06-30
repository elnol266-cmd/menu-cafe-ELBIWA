# 📖 Panduan Pengguna & Manual Operasional - ELBIWA VIEW

Dokumen ini berisi panduan lengkap mengenai cara menjalankan, mengonfigurasi, dan mengoperasikan Sistem Manajemen Kafe & Pemesanan Digital **ELBIWA VIEW** (`kasir.html` dan `pembeli.html`).

---

## 🛠️ Persiapan Awal & Akses Sistem

Aplikasi ini menggunakan arsitektur *serverless* berbasis cloud. Seluruh data disinkronkan secara *real-time* via Firebase.

### 1. Kredensial Login Kasir/Admin
Untuk masuk ke Dashboard Manajemen, buka file `kasir.html` pada browser Anda dan masukkan akun default berikut:
* **Username:** `admin`
* **Password:** `kopiElbiwa2026`

> 💡 *Tips:* Pada halaman login, Anda dapat menekan tombol **Enter** pada keyboard setelah mengisi username untuk berpindah ke kolom password secara cepat, dan tekan **Enter** sekali lagi untuk langsung masuk (login).

---

## 🖥️ Panduan Operasional Dashboard Kasir (`kasir.html`)

Setelah berhasil login, Anda akan masuk ke Dashboard Utama yang terdiri dari beberapa tab navigasi di panel kiri. Berikut adalah detail fungsi dan petunjuk penggunaannya:

### 1. Tab: Dashboard Utama (Ringkasan & Live Order)
Halaman ini adalah pusat pemantauan aktivitas kafe secara *real-time*.
* **Live Order Card:** Setiap kali pembeli mengirimkan pesanan dari meja lewat `pembeli.html`, pesanan tersebut akan langsung muncul di panel kasir secara otomatis disertai dengan **notifikasi suara (sound alert)**.
* **Mengubah Status Pesanan:** * Klik tombol **"Proses"** untuk mengubah status menjadi sedang disiapkan oleh dapur/barista.
    * Klik tombol **"Selesai & Cetak"** apabila pesanan sudah siap disajikan dan dibayar. Tindakan ini akan otomatis memicu jendela cetak (*print pop-up*) untuk nota fisik dan memindahkan data ke riwayat pendapatan.
    * Klik tombol **"Batalkan"** jika terjadi kesalahan pesanan atau pembatalan dari pelanggan.

### 2. Tab: Kasir Manual (Walk-in / POS)
Gunakan fitur ini apabila ada pelanggan yang datang langsung memesan di meja kasir (*dine-in langsung* atau *take-away*).
1.  Pilih menu yang diinginkan dari daftar katalog produk yang tersedia.
2.  Sistem akan otomatis memvalidasi sisa stok. Jika stok habis, menu tidak dapat ditambahkan ke keranjang belanja.
3.  Sesuaikan jumlah (*quantity*) pesanan.
4.  Klik tombol **"Proses Transaksi & Cetak Nota"** untuk memproses pembayaran dan mencetak struk belanja belanja.

### 3. Tab: Manajemen Stok (Katalog CRUD)
Modul untuk mengelola menu hidangan kafe Anda.
* **Tambah Menu Baru:** Isi formulir Nama Produk, Harga, Stok Awal, dan URL tautan gambar produk, lalu klik *Simpan*. Data akan langsung terupdate ke halaman pembeli secara instan.
* **Edit & Hapus:** Anda dapat memperbarui jumlah stok harian yang tersedia atau menghapus menu yang sudah tidak dijual kembali.

### 4. Tab: Manajemen Karyawan
Modul internal untuk mendata tim operasional yang sedang bertugas.
* Anda dapat mencatat Nama Karyawan, Posisi Kerja (seperti *Kasir, Barista, Waiter, Kitchen*), dan *Shift* Kerja (Pagi / Siang / Malam).

### 5. Tab: Analisis & Laporan Finansial
* **Grafik Omzet:** Dilengkapi visualisasi grafik garis (*Line Chart*) interaktif berbasis Chart.js yang melacak tren pendapatan kafe.
* **Ekspor Data ke Excel:** Terdapat tombol **"Download Excel"**. Ketika diklik, sistem menggunakan pustaka SheetJS untuk mengonversi seluruh riwayat transaksi di database menjadi file spreadsheets `.xlsx` secara otomatis dengan penamaan instan berdasarkan tanggal hari ini (`Laporan_Kasir_Elbiwa_YYYY-MM-DD.xlsx`).

---

## 📱 Panduan Pemesanan Mandiri Pembeli (`pembeli.html`)

Sistem ini didesain *mobile-first* agar mudah diakses oleh pelanggan melalui smartphone mereka (umumnya dipasang menggunakan QR Code di setiap meja kafe).

### Langkah-langkah Pemesanan oleh Pelanggan:
1.  **Identifikasi Diri:** Pelanggan wajib mengisi **Nomor Meja** dan **Nama Lengkap** pada kolom bagian atas sebelum dapat memesan.
2.  **Memilih Menu:** Pelanggan dapat melihat katalog makanan/minuman yang aktif beserta informasi harga dan sisa stok secara langsung (*real-time inventory check*).
3.  **Mengatur Keranjang:** Klik ikon tambah (`+`) atau kurang (`-`) pada menu untuk memasukkan pesanan ke dalam keranjang digital. Total harga belanjaan akan terkalkulasi otomatis di bagian bawah halaman.
4.  **Mengirim Pesanan:** Klik tombol **"Kirim Pesanan"**.
    * Sistem akan melakukan validasi otomatis. Jika nama atau nomor meja kosong, pesanan akan ditolak oleh sistem dan muncul peringatan.
    * Setelah sukses dikirim, tombol akan terkunci sementara (*disabled*) untuk mencegah pengiriman ganda, dan pelanggan akan menerima konfirmasi bahwa pesanan mereka berhasil diteruskan ke dapur dan meja kasir.

---

## 🖨️ Panduan Cetak Struk (Thermal Printer)

Sistem telah dioptimalkan khusus untuk pencetakan nota fisik menggunakan kertas kasir standard atau *thermal printer* (seperti ukuran 58mm atau 80mm). 

* Ketika kasir menekan tombol **Selesai & Cetak**, kode `@media print` pada CSS aplikasi akan menyembunyikan seluruh elemen navigasi, tombol-tombol dashboard, dan latar belakang warna gelap (menjadikannya putih bersih).
* Yang tersisa pada kertas print hanyalah teks nota belanja yang rapi dan minimalis (berisi Nama Kafe, Waktu Transaksi, Rincian Pesanan, dan Total Bayar) sehingga hemat tinta dan pas di ukuran kertas struk.

---

## ⚠️ Penanganan Masalah (Troubleshooting)

1.  **Notifikasi Pesanan Masuk Tidak Terdengar?**
    Pastikan browser kasir Anda telah memberikan izin pemutaran suara (*Allow Audio/Autoplay Permission*) pada pengaturan browser Anda, karena beberapa browser memblokir audio otomatis sebelum adanya interaksi pengguna.
2.  **Stok Tidak Berkurang?**
    Pastikan status pesanan di dashboard kasir diproses hingga selesai. Pengurangan stok di database utama tervalidasi saat transaksi diselesaikan oleh kasir guna menghindari pemesanan fiktif.
3.  **Data Tidak Sinkron?**
    Periksa koneksi internet Anda. Karena sistem ini berjalan secara langsung di atas Firebase Realtime Database, kestabilan jaringan internet sangat memengaruhi kecepatan sinkronisasi data antara `pembeli.html` dan `kasir.html`.
