Judul : Sistem Portal Travel & Wisata Lokal.

Nama : Luh Ayu Ariantini
NIM : D0223004

Framework Web Based
2025

Proyek ini adalah sistem berbasis web menggunakan framework Laravel yang digunakan untuk memesan paket wisata lokal secara online. Sistem ini dibangun agar pengguna dapat melihat dan memesan paket perjalanan, serta melakukan pembayaran, sementara admin dan customer service dapat mengelola dan memverifikasi proses tersebut.

Penjelasan Role
1. Admin: Pengelola utama sistem: CRUD data master (paket, destinasi, pengguna), verifikasi pembayaran
2. Customer Service (CS):	Verifikasi pembayaran, bantu pelanggan, ubah status booking
3. User (Wisatawan): Melihat paket wisata, melakukan booking, upload bukti pembayaran, cek status

1. Fitur Utama (Akses untuk semua role):
* Autentikasi Pengguna
Sistem menyediakan halaman login dan registrasi agar pengguna dapat memiliki akun pribadi. Saat registrasi, pengguna akan otomatis mendapat role sebagai "User" biasa. Dengan autentikasi, data pengguna dapat disimpan dan dilindungi, serta tindakan seperti booking dan upload pembayaran hanya bisa dilakukan oleh pengguna yang sudah login.

* Landing Page Publik
Tampilan awal website menampilkan daftar semua paket wisata yang tersedia. Pengunjung (baik login atau belum) dapat melihat foto, harga, durasi, serta daftar destinasi dari setiap paket. Ini memberi gambaran umum sebelum pengguna memutuskan untuk mendaftar dan memesan.

* kontak & Informasi
Website menyediakan halaman kontak atau footer yang menampilkan informasi layanan pelanggan, alamat kantor travel, email, dan nomor telepon untuk komunikasi langsung.

2. Fitur untuk User (Wisatawan)
* Lihat & jelajahi paket wisata
Setelah login, user bisa menjelajahi semua paket wisata yang telah dibuat admin. Mereka dapat melihat detail seperti: Nama paket, Deskripsi, Harga per orang, Lama perjalanan, Daftar destinasi yang termasuk.
* pemesanan / Booking
User dapat memesan paket wisata yang diinginkan dengan mengisi jumlah peserta dan memilih tanggal keberangkatan. Data pemesanan akan tersimpan di database dan bisa dilihat kembali di profil user.
* upload bukti pembayaran 
Setelah memesan, user akan diberi instruksi untuk melakukan transfer pembayaran ke rekening perusahaan. Setelah transfer, mereka dapat mengunggah bukti pembayaran (file gambar atau PDF). Bukti ini akan diverifikasi oleh Customer Service.
* Lihat Riwayat & Status pemesanan.
User dapat melihat daftar semua pemesanan mereka, beserta statusnya: Menunggu Pembayaran, Menunggu Verifikasi, Diterima, Ditolak, Selesai.
Hal ini membuat pengalaman pengguna lebih transparan dan profesional.

3. Fitur untuk customer Service (CS)
* verifikasi pembayaran
CS memiliki akses untuk melihat semua bukti transfer yang diunggah oleh user. CS bertugas memverifikasi apakah bukti itu valid (misal: jumlah sesuai, rekening benar). Jika valid, status pembayaran diubah menjadi “Diterima”, dan jika tidak, menjadi “Ditolak”.
* update status pemesanan
Setelah pembayaran diverifikasi, CS juga bertugas memperbarui status pemesanan. Misalnya, setelah perjalanan selesai, pemesanan bisa diubah menjadi “Selesai” atau “Dibatalkan” jika user tidak melakukan pembayaran tepat waktu.
* melihat daftar booking
CS bisa melihat semua data pemesanan yang dilakukan user, agar bisa menyesuaikan verifikasi dan koordinasi.

4. fitur untuk admin
* manajemen paket wisata
Admin bisa membuat, mengedit, dan menghapus paket wisata melalui halaman dashboard. Saat membuat paket, admin harus menentukan: Nama paket, Harga per orang, Deskripsi. Durasi, Relasi ke destinasi wisata (bisa lebih dari satu).
Admin juga bisa menambahkan jadwal khusus untuk tanggal keberangkatan tertentu jika sistem ingin dibuat lebih fleksibel.
* manajemen destinasi
Sebelum membuat paket, admin harus terlebih dahulu membuat daftar destinasi (misalnya: Pantai Kuta, Candi Borobudur, Danau Toba). Setiap paket wisata kemudian bisa mengaitkan beberapa destinasi. Admin bisa menambah/edit/hapus destinasi sesuai kebutuhan promosi.
* manajemen pengguna & role
Admin bisa melihat semua pengguna yang telah terdaftar, termasuk role mereka (user, CS, atau admin). Admin juga bisa mengubah role jika misalnya ingin menambahkan CS baru dari user biasa.
* laporan dan monitoring
Admin dapat mengakses rekap data pemesanan dan pembayaran, misalnya: Jumlah booking per bulan, Jumlah pembayaran berhasil dan gagal, Total pemasukan per bulan
Fitur ini membantu pengambilan keputusan bisnis.

Tabel Database, Field, dan Relasi
1. tabel user

| Field       | Tipe Data                                  | Deskripsi                               |
| ----------- | ------------------------------------------ | --------------------------------------- |
| id          | BIGINT AUTO\_INCREMENT                     | ID unik untuk setiap pengguna           |
| name        | VARCHAR(255)                               | Nama pengguna                           |
| email       | VARCHAR(255) UNIQUE                        | Alamat email pengguna                   |
| password    | VARCHAR(255)                               | Password pengguna (disarankan di-hash)  |
| role        | ENUM('admin', 'customer\_service', 'user') | Peran pengguna                          |
| created\_at | TIMESTAMP                                  | Waktu saat pengguna dibuat              |
| updated\_at | TIMESTAMP                                  | Waktu saat pengguna terakhir diperbarui |

2. Tabel Destinasi

| Field       | Tipe Data    | Deskripsi                        |
| ----------- | ------------ | -------------------------------- |
| id          | BIGINT       | ID unik destinasi                |
| name        | VARCHAR(255) | Nama destinasi                   |
| description | TEXT         | Deskripsi tempat                 |
| image       | VARCHAR(255) | URL atau path gambar destinasi   |
| created\_at | TIMESTAMP    | Tanggal data dibuat              |
| updated\_at | TIMESTAMP    | Tanggal data terakhir diperbarui |

3. Tabel Paket Wisata

| Field          | Tipe Data     | Deskripsi                        |
| -------------- | ------------- | -------------------------------- |
| id             | BIGINT        | ID unik paket                    |
| title          | VARCHAR(255)  | Judul atau nama paket wisata     |
| description    | TEXT          | Deskripsi paket                  |
| price          | DECIMAL(10,2) | Harga per orang                  |
| duration\_days | INTEGER       | Durasi wisata dalam hari         |
| image          | VARCHAR(255)  | Gambar ilustrasi paket           |
| created\_at    | TIMESTAMP     | Tanggal data dibuat              |
| updated\_at    | TIMESTAMP     | Tanggal data terakhir diperbarui |

4. Tabel Package_Destination (Pivot Paket ↔ Destinasi)

| Field           | Tipe Data | Deskripsi                |
| --------------- | --------- | ------------------------ |
| id              | BIGINT    | ID unik                  |
| package\_id     | BIGINT    | FK ke tabel packages     |
| destination\_id | BIGINT    | FK ke tabel destinations |

5. Tabel Bookings (Pemesanan)

| Field          | Tipe Data                                 | Deskripsi                    |
| -------------- | ----------------------------------------- | ---------------------------- |
| id             | BIGINT                                    | ID unik pemesanan            |
| user\_id       | BIGINT                                    | FK ke tabel users            |
| package\_id    | BIGINT                                    | FK ke tabel packages         |
| travel\_date   | DATE                                      | Tanggal keberangkatan        |
| total\_persons | INTEGER                                   | Jumlah orang yang ikut       |
| status         | ENUM('pending','paid','cancelled','done') | Status pemesanan             |
| created\_at    | TIMESTAMP                                 | Tanggal pemesanan dibuat     |
| updated\_at    | TIMESTAMP                                 | Tanggal pemesanan diperbarui |

6. Tabel Payments (Pembayaran)

| Field         | Tipe Data                             | Deskripsi                     |
| ------------- | ------------------------------------- | ----------------------------- |
| id            | BIGINT                                | ID unik pembayaran            |
| booking\_id   | BIGINT                                | FK ke tabel bookings          |
| payment\_date | DATETIME                              | Tanggal pembayaran            |
| amount        | DECIMAL(10,2)                         | Jumlah yang dibayar           |
| proof\_image  | VARCHAR(255)                          | Path gambar bukti pembayaran  |
| status        | ENUM('pending','verified','rejected') | Status verifikasi oleh CS     |
| verified\_by  | BIGINT                                | FK ke users (khusus role CS)  |
| created\_at   | TIMESTAMP                             | Tanggal pembayaran dibuat     |
| updated\_at   | TIMESTAMP                             | Tanggal pembayaran diperbarui |

Jenis Relasi Dan tabel yang berelasi
1.  Relasi: One-to-Many (1:N)
a. User ↔ Booking
* Satu user bisa membuat banyak booking.
* Tapi satu booking hanya dimiliki oleh satu user.
b. Paket wisata ↔ Booking
* Satu paket wisata bisa dipesan dalam banyak booking.
* Tapi satu booking hanya terkait dengan satu paket wisata.
c. User ↔ Payments
* Satu user bisa melakukan banyak pembayaran.
* Satu pembayaran dilakukan oleh satu user.
d. Booking ↔ Payments
* Satu booking bisa memiliki satu atau lebih pembayaran, tapi biasanya satu pembayaran mewakili satu booking.

2. Relasi: Many-to-Many (N:N)
a. Packages ↔ Destinations
* Satu paket bisa mencakup banyak destinasi.
* Satu destinasi bisa masuk ke banyak paket wisata.
* Dihubungkan oleh tabel pivot: package_destination.

Ringkasan Tabel dan Relasinya
| Tabel          | Relasi Dengan                    | Jenis Relasi |
| -------------- | -------------------------------- | ------------ |
| `users`        | `bookings`, `payments`           | One-to-Many  |
| `packages`     | `bookings`                       | One-to-Many  |
| `packages`     | `destinations` via pivot         | Many-to-Many |
| `destinations` | `packages` via pivot             | Many-to-Many |
| `bookings`     | `payments`                       | One-to-Many  |
| `users`        | `bookings.handled_by` (opsional) | One-to-Many  |


### Premium Partners
- **[Vehikl](https://vehikl.com/)**
- **[Tighten Co.](https://tighten.co)**
- **[WebReinvent](https://webreinvent.com/)**
- **[Kirschbaum Development Group](https://kirschbaumdevelopment.com)**
- **[64 Robots](https://64robots.com)**
- **[Curotec](https://www.curotec.com/services/technologies/laravel/)**
- **[Cyber-Duck](https://cyber-duck.co.uk)**
- **[DevSquad](https://devsquad.com/hire-laravel-developers)**
- **[Jump24](https://jump24.co.uk)**
- **[Redberry](https://redberry.international/laravel/)**
- **[Active Logic](https://activelogic.com)**
- **[byte5](https://byte5.de)**
- **[OP.GG](https://op.gg)**

## Contributing
Thank you for considering contributing to the Laravel framework! The contribution guide can be found in the [Laravel documentation](https://laravel.com/docs/contributions).

## Code of Conduct
In order to ensure that the Laravel community is welcoming to all, please review and abide by the [Code of Conduct](https://laravel.com/docs/contributions#code-of-conduct).

## Security Vulnerabilities
If you discover a security vulnerability within Laravel, please send an e-mail to Taylor Otwell via [taylor@laravel.com](mailto:taylor@laravel.com). All security vulnerabilities will be promptly addressed.

## License

The Laravel framework is open-sourced software licensed under the [MIT license](https://opensource.org/licenses/MIT).
