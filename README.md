# 🎓 SIAKAD - Sistem Informasi Akademik Mahasiswa

Projek ini adalah Sistem Informasi Akademik berbasis Laravel sebagai tugas proyek 2 semester 4. Sistem ini mendukung pengelolaan data akademik, mahasiswa, dosen, serta fitur tambahan untuk prodi dan marketing kampus.

## 🌟 Fitur Utama

### 👨‍🏫 Kelompok Akademik
- **📅 Penjadwalan Kelas**
  - Menampilkan jadwal per hari/minggu dalam format tabel
  - Tabel `schedules` dengan kolom: `hari`, `jam_mulai`, `jam_selesai`, `course_id`
  - Ditampilkan menggunakan looping di Blade

- **🏫 Manajemen Ruang Kuliah**
  - CRUD data ruang kuliah (`nama`, `kapasitas`)
  - Menggunakan model `Room`
  - Relasi one-to-many dengan `Schedule`

- **📢 Pengumuman Akademik**
  - CRUD pengumuman (jadwal ujian, kalender akademik)
  - Model `AcademicAnnouncement` dengan resource controller

### 👨‍🎓 Kelompok Mahasiswa
- **🔐 Registrasi & Login**
  - Form pendaftaran mahasiswa baru
  - Autentikasi Laravel (Jetstream/make:auth)

- **👤 Profil & Nilai**
  - Halaman profil read-only (NIM, nama, prodi)
  - Menampilkan KHS semester berjalan & transkrip nilai
  - Admin bisa edit program studi

- **📝 KRS Online**
  - Pemilihan mata kuliah semester berjalan
  - Pivot table `course_student`
  - Penyimpanan dengan `attach()`

- **📍 Absensi Online**
  - Tombol absen dengan timestamp & lokasi
  - Geolocation API JavaScript
  - Controller `AttendanceController@store`

### 👨‍🏫 Kelompok Dosen
- **📊 Dashboard Dosen**
  - Ringkasan kelas yang diajar
  - Query: `Course::where('dosen_id', auth()->id())->withCount('students')`

- **📝 Input Nilai**
  - Form input nilai UTS/UAS
  - Relasi Enrollment dengan form POST

- **🖨️ Cetak KHS**
  - Generate PDF nilai mahasiswa
  - Package `barryvdh/laravel-dompdf`

### 📢 Kelompok Marketing
- **🌐 Landing Page**
  - Informasi fitur SIAKAD
  - Blade + Bootstrap
  - Link pendaftaran & kontak

- **📢 Pengumuman Umum**
  - CRUD pengumuman halaman depan
  - Tampil otomatis saat load

- **📬 Form Kontak**
  - Kirim pesan ke admin via email
  - Validasi & `Mail::send()`

### 💰 Kelompok Prodi & Keuangan
- **📚 Data Prodi & Matkul**
  - CRUD prodi (`kode`, `nama`, `akreditasi`)
  - CRUD mata kuliah (`kode`, `nama`, `sks`)
  - Model `Program` dengan relasi

- **💳 Tagihan & Pembayaran**
  - Generate tagihan SPP per mahasiswa
  - Tabel `invoices` untuk data tagihan
  - Fitur status lunas

- **📈 Laporan Keuangan**
  - Export CSV pemasukan bulanan
  - Download via route khusus

## 🛠️ Teknologi
- **Backend**: Laravel
- **Frontend**: Blade + Bootstrap
- **Database**: MySQL
- **Libraries**:
  - `barryvdh/laravel-dompdf` (PDF)
  - Laravel Mail (Email)
  - Geolocation API (Absensi)

## 🚀 Panduan Instalasi
1. Clone repository:
   ```bash
   git clone https://github.com/nama-akun/Siakad.git
   cd siakad

2. Pilih branch sesuai kelompok:
   ```bash
   # Akademik
    git checkout feature/akademik

    # Mahasiswa
    git checkout feature/mahasiswa

    # Dosen
    git checkout feature/dosen

    # Marketing
    git checkout feature/marketing

    # Prodi & Keuangan
    git checkout feature/prodi-keuangan

3. Install dependencies:
   ```bash
   composer install
    npm install && npm run dev
    cp .env.example .env
    php artisan key:generate
