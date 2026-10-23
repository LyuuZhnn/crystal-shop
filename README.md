# Crystal Shop — Static E-commerce Demo

Crystal Shop adalah proyek toko online statis menggunakan HTML, CSS, dan JavaScript murni. Proyek ini dirancang untuk GitHub Pages; tidak memerlukan Node.js, PHP, Express, server tambahan, atau database backend.

## Struktur proyek

```text
crystal-shop/
├── index.html             # Toko publik
├── admin.html             # Halaman admin lokal terpisah, tidak ada di navigasi publik
├── css/
│   └── style.css
├── js/
│   ├── storage.js         # localStorage, format, validasi helper
│   ├── products.js        # katalog/CRUD produk lokal
│   ├── cart.js            # keranjang dan validasi stok
│   ├── orders.js          # checkout, riwayat, status, WhatsApp
│   ├── app.js             # navigasi dan tampilan toko publik
│   └── admin.js           # login demo, dashboard dan pengaturan lokal
├── assets/images/
│   └── crystal-mark.svg
├── .nojekyll
└── README.md
```

## Menjalankan lokal

Bisa dibuka langsung dengan `index.html` di browser, tetapi beberapa fitur hash kata sandi menggunakan Web Crypto yang umumnya memerlukan konteks aman. Untuk pengujian login akun/admin, gunakan alamat HTTPS setelah diterbitkan oleh GitHub Pages. Tidak ada proses build.

### Ekstrak melalui Termux (Android)

Letakkan ZIP yang diunduh di folder Download, lalu jalankan:

```bash
pkg install unzip git -y
termux-setup-storage
mkdir -p ~/crystal-shop
unzip -o ~/storage/downloads/Crystal_Shop_GitHub_Pages.zip -d ~/crystal-shop
cd ~/crystal-shop
ls -la
```

Arsip ini menyimpan `index.html` langsung di akar ZIP, bukan dalam folder bertingkat. Setelah ekstrak, `ls -la` harus menampilkan `index.html`, `admin.html`, `css/`, `js/`, dan `assets/`. Jika nama unduhan ditambahkan `(1)`, sesuaikan nama berkas pada perintah `unzip`.

## Publikasi GitHub Pages

1. Buat repository GitHub baru bernama `crystal-shop`, atau gunakan repository yang sudah ada. Nama repository menentukan bagian path pada URL, bukan nama toko.
2. Unggah **isi folder proyek ini** ke root repository. Pastikan `index.html`, `admin.html`, `.nojekyll`, folder `css`, `js`, dan `assets` berada di root yang sama—jangan mengunggah folder pembungkus tambahan.
3. Jika mengunggah dari Termux ke repository baru, jalankan `git init`, `git add .`, `git commit -m "Build Crystal Shop static website"`, `git branch -M main`, lalu tambahkan remote repository dan jalankan `git push -u origin main`.
4. Buka **Settings → Pages**.
5. Pada **Build and deployment**, pilih **Deploy from a branch**.
6. Pilih branch `main` dan folder `/(root)`, kemudian tekan **Save**.
7. Setelah deployment selesai, link biasanya `https://USERNAME.github.io/crystal-shop/`. Jika menggunakan repository lama bernama `sky-shop`, URL tetap `https://USERNAME.github.io/sky-shop/`.
8. Uji beranda, katalog, tampilan mobile, keranjang, checkout, pesanan, dan akses admin melalui HTTPS.

Semua referensi berkas bersifat relatif (`css/style.css`, `js/app.js`, `assets/images/...`) sehingga bekerja pada alamat repositori seperti `username.github.io/nama-repository/`.

## Membuka halaman admin

Halaman admin tidak ditautkan dari navigasi publik. Buka langsung:

`https://USERNAME.github.io/crystal-shop/admin.html`

Pada browser/origin yang baru, buat kata sandi admin lokal minimal 10 karakter. Kata sandi tidak disimpan sebagai teks biasa; hash SHA-256 disimpan di `localStorage`. Jangan gunakan kata sandi penting.

**Peringatan keamanan:** halaman admin ini hanyalah pagar demonstrasi di frontend. Siapa pun yang dapat memeriksa atau memodifikasi JavaScript, `localStorage`, dan status sesi dapat melewati pemeriksaan. Jangan gunakan untuk pengelolaan uang, data pribadi, atau sebagai perlindungan toko publik. Tidak ada password admin bawaan yang ditanam dalam kode.

## Fitur publik

- Beranda, katalog, pencarian langsung, kategori, filter, pengurutan harga/tanggal, dan detail produk.
- Tambah/ubah/hapus jumlah keranjang dan validasi jumlah terhadap stok lokal.
- Checkout tamu dengan validasi nama, nomor WhatsApp, alamat, catatan dan persetujuan penyimpanan lokal.
- Nomor pesanan unik, riwayat pesanan pada browser yang sama, perubahan status lokal melalui admin, dan komposisi pesan WhatsApp.
- Halaman Tentang Kami dan kontak yang dapat disesuaikan oleh pengaturan lokal.
- Akun pengguna demonstrasi opsional; kata sandi di-hash, bukan disimpan sebagai teks biasa.
- Dashboard admin lokal: CRUD produk, status pesanan lokal, statistik yang dihitung dari data lokal, pengaturan toko, serta ekspor JSON.

## Batasan yang disengaja

- `localStorage` berbeda untuk setiap browser/origin dan tidak tersinkronisasi antarperangkat. Pengunjung lain tidak akan otomatis melihat produk yang ditambahkan admin lokal. Pesanan pelanggan juga tidak terkirim ke admin secara otomatis.
- Ketika data toko diedit dari panel admin, perubahan hanya ada di browser itu. Untuk membuat perubahan katalog tampil bagi semua pengunjung di GitHub Pages, ubah file statis di repository dan publikasikan ulang, atau pindah ke layanan data terpusat (di luar cakupan statis ini).
- Pesanan yang dibuat disimpan secara lokal. Tombol WhatsApp hanya membuka pesan yang disiapkan untuk dikirim oleh pengguna; hal itu bukan bukti toko telah menerima pesanan atau pembayaran.
- Website tidak memproses pembayaran, menghitung tarif pengiriman, atau memverifikasi transaksi.
- Produk tidak diisi otomatis dengan data contoh. Pemilik toko perlu memasukkan katalog sendiri. Statistik awal bernilai nol.
- Foto produk/logo/banner sebaiknya memakai URL HTTPS yang dapat diakses publik atau aset dalam repository. Gambar yang hanya tersedia sebagai data lokal/browser tidak otomatis dapat dilihat pengguna lain.
- Font DM Sans dan Manrope mengambil Google Fonts secara opsional. Jika jaringan memblokirnya, browser memakai font sistem sebagai fallback.

## Penyimpanan lokal

Prefiks key `crystal.shop.v1.*` digunakan untuk memisahkan data produk, kategori, keranjang, pesanan, pengaturan toko, akun lokal, hash sandi, dan sesi admin. Data dapat dihapus pengguna melalui pengaturan browser. Gunakan tombol ekspor untuk mengunduh salinan JSON data toko lokal.

## Catatan nama

Nama antarmuka proyek ini **Crystal Shop**. Ini adalah website statis demonstrasi, bukan platform e-commerce dengan server produksi.
