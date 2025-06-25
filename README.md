Fullstack Test Application
Aplikasi web untuk autentikasi, manajemen pengguna, dan manajemen buku menggunakan Laravel 12, Breeze, dan PostgreSQL.
Persyaratan

PHP 8.2+
Composer
Node.js & NPM
PostgreSQL

Instalasi

Clone repository:git clone https://github.com/your-repo/fullstack-test.git
cd fullstack-test


Install dependensi PHP:composer install


Install dependensi Node.js:npm install && npm run dev


Salin .env.example ke .env dan konfigurasi:cp .env.example .env

Edit DB_* dan MAIL_* di .env. Untuk Gmail SMTP, gunakan App Password.
Generate kunci aplikasi:php artisan key:generate


Jalankan migrasi database:php artisan migrate


Jalankan queue worker untuk email:php artisan queue:work


Link storage untuk thumbnail:php artisan storage:link


Jalankan server:php artisan serve


Akses aplikasi di http://127.0.0.1:8000.

Fitur

Landing Page:
Pengguna yang belum login dapat melihat daftar buku di /.
Filter buku berdasarkan penulis, uploader (nama pengguna), tanggal unggah (terbaru/terlama), dan rating (1-5).
Pagination dengan 10 buku per halaman.


Autentikasi:
Registrasi: Redirect ke login setelah registrasi, dengan email verifikasi via Gmail SMTP.
Login: Hanya pengguna dengan email diverifikasi yang bisa login, dengan alert jika belum diverifikasi.
Verifikasi Email: Link verifikasi diakses tanpa login.
Lupa Password: Email reset password untuk mengatur ulang.
Ganti Password: Di profil pengguna.
Middleware: Pengguna yang sudah login tidak dapat mengakses halaman login atau registrasi (diterapkan via RedirectIfAuthenticated, dikonfigurasi di bootstrap/app.php).


Home Page:
Menampilkan nama pengguna dan status verifikasi email di /dashboard menggunakan x-app-layout.


User List:
Menampilkan daftar pengguna di /users (nama, email, status verifikasi) dengan pagination (10 per halaman).
Filter berdasarkan status verifikasi (terverifikasi/belum).
Pencarian berdasarkan nama atau email.


Book Management:
Menambah, melihat, memperbarui, dan menghapus buku di /books.
Setiap buku memiliki judul, penulis, deskripsi, cover (thumbnail), dan rating (1-5).
Hanya pemilik buku yang bisa mengakses/mengedit/menghapus, diatur via BookPolicy.



Testing

Unit Test:
Menguji validasi input (misalnya, pembuatan buku dengan data tidak valid).
Menguji logika otorisasi di BookPolicy.


Integration Test:
Menguji alur autentikasi (registrasi, login, verifikasi email, reset password, akses halaman login/registrasi saat sudah login).
Menguji manajemen buku (tambah, lihat, perbarui, hapus).
Menguji Landing Page (filter penulis, uploader, tanggal, rating, pagination).
Menguji User List (filter status, pencarian, pagination).



Library Pihak Ketiga

Laravel Breeze: Autentikasi siap pakai.
Tailwind CSS: UI responsif dan modern.

Menjalankan Test
php artisan test

Catatan

Menggunakan <x-app-layout> untuk halaman autentikasi.
Pastikan resources/views/layouts/app.blade.php ada.
Policy untuk Book didaftarkan di AppServiceProvider karena Laravel 12 tidak menyertakan AuthServiceProvider.
Pastikan storage di-link untuk thumbnail buku (php artisan storage:link).
Middleware dikonfigurasi di bootstrap/app.php karena Laravel 12 tidak menggunakan Kernel.php.
