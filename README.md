# 🎓 SIAKAD - Sistem Informasi Akademik Mahasiswa

Projek ini adalah Sistem Informasi Akademik berbasis Laravel sebagai tugas proyek 2 semester 4. Sistem ini mendukung pengelolaan data akademik, mahasiswa, dosen, serta fitur tambahan untuk prodi dan marketing kampus.

## 📌 Fitur Utama Berdasarkan Kelompok

---

### 1. Kelompok Akademik

#### 📅 Penjadwalan Kelas
- Menampilkan jadwal per hari atau minggu dalam format tabel.
- Menggunakan tabel `schedules` (kolom: `hari`, `jam_mulai`, `jam_selesai`, `course_id`).
- Ditampilkan menggunakan looping di view Blade.

#### 🏫 Manajemen Ruang Kuliah
- Input dan daftar ruang kuliah (`nama`, `kapasitas`).
- Menggunakan model `Room`.
- Relasi one-to-many dengan model `Schedule`.

#### 📢 Pengumuman Akademik
- CRUD pengumuman akademik seperti jadwal ujian atau kalender akademik.
- Menggunakan model `AcademicAnnouncement` dan resource controller.

---

### 2. Kelompok Mahasiswa

#### 🧾 Registrasi & Login
- Form pendaftaran mahasiswa baru.
- Autentikasi menggunakan Laravel Auth Scaffolding (Jetstream atau `make:auth` untuk Laravel lama).

#### 👤 Profil Mahasiswa & Akses Nilai
- Halaman profil readonly: NIM, nama, dan prodi tidak dapat diedit oleh mahasiswa.
- Menampilkan KHS semester berjalan & transkrip seluruh nilai.
- Admin dapat mengedit program studi mahasiswa.
- Tab “Nilai” tersedia di halaman profil.

#### 📝 KRS Online
- Mahasiswa dapat memilih mata kuliah semester berjalan.
- Menggunakan pivot table `course_student`.
- Form checkbox untuk pemilihan mata kuliah, disimpan dengan `attach()`.

#### 📍 Absensi Online
- Tombol “Absen” menyimpan timestamp dan lokasi (latitude & longitude).
- Menggunakan Geolocation API JavaScript dan controller `AttendanceController@store`.

---

### 3. Kelompok Dosen

#### 🧑‍🏫 Dashboard Dosen
- Menampilkan ringkasan kelas yang diajar dan jumlah mahasiswa per kelas.
- Query dengan `Course::where('dosen_id', auth()->id())->withCount('students')`.

#### 🧾 Input Nilai Mahasiswa
- Form input nilai UTS dan UAS.
- Menggunakan relasi Enrollment, nilai disimpan lewat form POST.

#### 🖨️ Cetak KHS (Kartu Hasil Studi)
- Generate PDF nilai mahasiswa.
- Menggunakan package `barryvdh/laravel-dompdf`.

---

### 4. Kelompok Marketing

#### 🌐 Halaman Landing Page
- Informasi singkat tentang SIAKAD (fitur, keuntungan).
- Dibuat dengan Blade + Bootstrap.
- Terdapat link ke form pendaftaran dan kontak.

#### 📢 Pengumuman Umum
- CRUD pengumuman yang tampil di halaman depan.
- Ditampilkan otomatis saat halaman diload.

#### 📬 Form Kontak
- Kirim pesan ke admin via email.
- Validasi email dan pengiriman menggunakan `Mail::send()`.

---

### 5. Kelompok Prodi dan Keuangan

#### 🎓 Data Program Studi & Mata Kuliah
- CRUD data prodi (`kode`, `nama`, `akreditasi`) dan mata kuliah (`kode`, `nama`, `sks`).
- Resource controller + model `Program`.
- Relasi ke mahasiswa dan mata kuliah.

#### 💵 Tagihan & Pembayaran
- Generate tagihan SPP berdasarkan mahasiswa.
- Tabel `invoices` menyimpan data tagihan.
- Fitur “Bayar” untuk menandai status lunas.

#### 📊 Laporan Keuangan Bulanan
- Export CSV berisi ringkasan pemasukan bulanan.
- Fitur download CSV via route khusus.

---

## 🛠️ Tools & Teknologi
- **Framework**: Laravel
- **Frontend**: Blade + Bootstrap
- **Database**: MySQL
- **PDF**: barryvdh/laravel-dompdf
- **Email**: Laravel Mail
- **CSV Export**: Laravel response with file download
- **Geolocation**: JavaScript API

---

## 💡 Cara Menjalankan Aplikasi
1. Clone repository:
   ```bash
   git clone https://github.com/nama-akun/project-siakad.git
   cd siakad

2. Masuk ke branch sesuai klompok:
    # Untuk Kelompok Akademik
    git checkout feature/akademik
    
    # Untuk Kelompok Mahasiswa
    git checkout feature/mahasiswa
    
    # Untuk Kelompok Dosen
    git checkout feature/dosen
    
    # Untuk Kelompok Marketing
    git checkout feature/marketing
    
    # Untuk Kelompok Prodi dan Keuangan
    git checkout feature/prodi-keuangan

3. Install dependency Laravel:
    composer install
    npm install && npm run dev
    cp .env.example .env
    php artisan key:generate
