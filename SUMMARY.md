# SIDATI - Ringkasan Aplikasi
## Sistem Informasi Database & Penomoran Otomatis SPT & SPPD

---

## 📋 Informasi Aplikasi

**Nama Aplikasi:** SIDATI  
**Versi:** 1.0  
**Bahasa:** Bahasa Indonesia  
**Institusi:** Sekretariat DPRD Kabupaten Padang Pariaman  
**Lokasi:** Jl. Mohd. Syafei No. 8 Kampung Perak Pariaman  
**Jenis Aplikasi:** Web-based Single Page Application (SPA)  
**Teknologi:** HTML5, CSS3 (Bootstrap 5.3.0), JavaScript Vanilla  
**Backend:** Google Apps Script (Makro)  

---

## 🎯 Fungsi Utama

Aplikasi SIDATI dirancang untuk mengelola penomoran otomatis dokumen dinas pegawai, khususnya:

1. **SPT (Surat Perintah Tugas)** - Dokumen perintah perjalanan dinas pegawai
2. **SPPD (Surat Pesan Perjalanan Dinas)** - Bukti dokumentasi perjalanan dinas

---

## 👤 Fitur Keamanan

### Autentikasi Login
- **Verifikasi NIP (18 digit)** - Nomor Induk Pegawai
- **Verifikasi Password** - Autentikasi credential
- **Backend Validation** - Validasi dilakukan melalui Google Apps Script
- **Session Management** - Menyimpan data user aktif di memory

**Endpoint:** `https://script.google.com/macros/s/AKfycbwihCEqF4EKl_ghOmtHAm7g-66TWvK7wTZn8E7mn4GqyBTLX1J979zfMrx5aNGPUaKK/exec`

---

## 🖥️ Antarmuka Pengguna

### 1. **Halaman Login**
- Form input NIP dan Password
- Alert notification untuk error login
- Validasi input real-time
- Tombol "Masuk Aplikasi"

### 2. **Dashboard Utama**
- Greeting personalisasi (Nama & NIP user)
- Tombol navigasi 3 fitur utama:
  - 📄 **Penomoran SPT Sekretariat**
  - 🚘 **Penomoran SPPD Sekretariat**
  - 📂 **Arsip & Laporan Registrasi**
- Tombol Logout

### 3. **Form Penomoran SPT**
- **Input Petugas/Pelaksana:** (Read-only - Auto-filled dari login)
- **Tanggal Berangkat:** Date picker dengan default hari ini
- **Tanggal Kembali:** Date picker dengan default hari ini
- **Maksud Perjalanan Dinas:** Text area untuk deskripsi agenda
- **Tujuan Perjalanan:** Input text (contoh: DPRD Prov. Sumbar)
- **Tombol:** Generate Nomor SPT

**Output:** Nomor registrasi unik otomatis

### 4. **Form Penomoran SPPD**
- **Input Petugas/Pelaksana:** (Read-only - Auto-filled dari login)
- **Nomor SPT Referensi:** Input nomor SPT yang dirujuk
- **Tempat Berangkat:** Default "Pariaman" (editable)
- **Tempat Tujuan:** Input destinasi perjalanan
- **Alat Transportasi:** Default "Kendaraan Dinas Operasional" (editable)
- **Tombol:** Generate Nomor SPPD

**Output:** Nomor SPPD unik otomatis

### 5. **Halaman Arsip & Laporan**
- **Tab SPT:**
  - Tabel data SPT dengan kolom: No. Registrasi, Petugas, Tgl Berangkat, Tgl Kembali, Maksud, Tujuan, Waktu Input
  - Loading state dan error handling
  
- **Tab SPPD Sekretariat:**
  - Tabel data SPPD dengan kolom: No. SPPD, Petugas, No. SPT Ref, Berangkat, Tujuan, Transportasi, Waktu Input
  - Loading state dan error handling

**Data Source:** Diambil dari Google Sheets melalui Google Apps Script

---

## 🖨️ Fitur Cetak Bukti

### Template Bukti Penomoran
Setiap penomoran menghasilkan bukti cetak yang berisi:

**Header Resmi:**
- Logo/Kop Surat Pemerintah Kabupaten Padang Pariaman
- Nama Sekretariat DPRD
- Alamat

**Isi Dokumen:**
- Jenis Dokumen (SPT atau SPPD)
- Nomor Registrasi Resmi (highlighted)
- Waktu Registrasi Sistem
- Nama/NIP Petugas
- Data spesifik sesuai jenis dokumen:
  - **Untuk SPT:** Maksud Perjalanan, Tanggal Pelaksanaan, Lama Perjalanan (dalam hari dan terbilang)
  - **Untuk SPPD:** Dasar SPT Referensi, Alat Transportasi
- Database Penyimpanan (Google Sheets tab)

**Footer Resmi:**
- Catatan Pengesahan & Verifikasi
- Lokasi dan Tanggal Cetak (Pariaman + tanggal otomatis)
- Signature Block untuk Petugas/Operator
- QR Code (mengarah ke: https://sekretariatdewanpdgprm-ops.github.io/sadati/)

### Fitur Print
- Responsive design untuk A4 paper
- Font: Times New Roman (serif) untuk dokumen resmi
- Margin: 10mm dari atas, 15mm dari samping
- Bisa diprint langsung atau save as PDF
- Mobile-friendly dengan media query terpisah

---

## 🎨 Styling & Design

### Color Scheme
- **Primary Color:** #0b3c5d (Navy Blue) - Untuk header dan tombol utama
- **Secondary Color:** #072a42 (Darker Navy) - Hover state
- **Background:** #f4f6f9 (Light Gray) - Untuk background halaman
- **Card Background:** #ffffff (White) - Untuk card containers
- **Highlight:** #eef4fc (Light Blue) - Untuk nomor registrasi

### Layout
- **Max Width Card:** 650px (normal), 1100px (large)
- **Framework:** Bootstrap 5.3.0
- **Responsive:** Mobile-first approach dengan media queries
- **Typography:** Segoe UI, Tahoma, Geneva, Verdana (sans-serif)

---

## 🔄 Alur Operasional

### Alur User Normal
```
1. Login (NIP + Password)
   ↓
2. Dashboard
   ├─ Pilih SPT / SPPD / Arsip
   ├─ SPT Flow:
   │  ├─ Isi Form SPT
   │  ├─ Generate Nomor
   │  └─ Cetak Bukti
   │
   ├─ SPPD Flow:
   │  ├─ Isi Form SPPD
   │  ├─ Generate Nomor
   │  └─ Cetak Bukti
   │
   └─ Arsip Flow:
      ├─ Lihat Tab SPT/SPPD
      ├─ Data dimuat dari Google Sheets
      └─ Kembali ke Dashboard
   
3. Logout
```

---

## 📊 Data Integration

### Koneksi Google Apps Script
- **Method:** POST via Fetch API
- **Format:** JSON
- **Actions yang didukung:**
  - `login` - Verifikasi NIP & Password
  - `generateSPT` - Generate nomor SPT otomatis
  - `generateSPPD` - Generate nomor SPPD otomatis
  - `getArsip` - Ambil data SPT dan SPPD dari Google Sheets

### Data Storage
- **Database:** Google Sheets
- **Sheet SPT:** `Data_SPT`
- **Sheet SPPD:** `SPPD_sekretariat`
- **Struktur Kolom:** Timestamp, No. Registrasi, Nama Petugas, Tanggal Berangkat, Tanggal Kembali, Maksud, Tujuan, (SPPD: Berangkat, Tujuan, Transportasi, No. SPT Ref)

---

## 🛠️ Utility Functions

### JavaScript Helper Functions

1. **`formatTanggalIndo(val)`**
   - Format tanggal dari YYYY-MM-DD menjadi DD/MM/YYYY
   - Contoh: "2026-07-24" → "24/07/2026"

2. **`renderTabelSpt(data)`**
   - Render tabel data SPT dari array Google Sheets
   - Parse kolom sesuai index

3. **`renderTabelSppd(data)`**
   - Render tabel data SPPD dari array Google Sheets
   - Parse kolom sesuai index

4. **`terbilang(angka)`**
   - Konversi angka ke kata-kata Bahasa Indonesia
   - Contoh: 5 → "Lima", 15 → "Lima Belas", 100 → "Seratus"
   - Max support hingga ratusan

5. **`cetakBukti(jenis)`**
   - Generate bukti cetak dinamis
   - Populate template sesuai tipe dokumen (SPT/SPPD)
   - Generate QR Code otomatis
   - Trigger window.print()

6. **`bukaForm(jenis)`** & **`bukaArsip()`**
   - Navigasi antar halaman
   - Hide/show container sesuai kondisi

7. **`kembaliKeDashboard()`** & **`logout()`**
   - Reset state aplikasi
   - Clear session user

---

## 🐛 Error Handling

### Validasi
- **Form Validation:** HTML5 required attributes
- **Input Validation:** Trim whitespace untuk NIP & Password
- **Date Validation:** Min/Max date picker
- **Empty State:** Loading indicator di tabel sebelum data dimuat
- **Error Messages:** Alert notification untuk gagal login atau fetch data

### Network Error
- Catch untuk failed fetch requests
- Display pesan error user-friendly
- Fallback ke "Gagal memuat data" untuk tabel kosong

---

## 🔒 Keamanan & Best Practice

✅ **Implemented:**
- NIP & Password validation via backend
- Session management di client
- HTTPS recommended (GitHub Pages automatic)
- QR Code untuk verifikasi dokumen
- Read-only field untuk auto-populated data

⚠️ **Catatan:**
- Password disimpan di Google Sheets (pastikan keamanan GCP)
- Tidak ada encryption di client-side (handled by backend)
- Session hanya di memory client (hilang saat refresh)

---

## 📱 Responsivitas & Mobile Support

### Fix Mobile Issue (Latest Update)
- **Masalah:** Halaman jadi PDF/kosong di mobile
- **Penyebab:** CSS media query `visibility: hidden` tidak kompatibel iOS Safari
- **Solusi:** 
  - Ubah dari `visibility` ke `display: none/block`
  - Pisahkan `@media screen` dan `@media print`
  - Sembunyikan `.container` saat print mode

### Browser Compatibility
- ✅ Chrome 90+
- ✅ Firefox 88+
- ✅ Safari 14+ (setelah fix mobile)
- ✅ Edge 90+
- ✅ Mobile browsers (iOS Safari, Chrome Mobile, Samsung Internet)

---

## 📦 File Structure

```
sadati/
├── index.html          # Single HTML file (SPA)
├── README.md          # Project documentation
└── (Static files hosted di GitHub Pages)
```

**GitHub Pages URL:** https://sekretariatdewanpdgprm-ops.github.io/sadati/

---

## 🚀 Fitur & Pembangunan Masa Depan

**Selesai:**
- ✅ Login & Autentikasi
- ✅ Generate SPT & SPPD
- ✅ Cetak Bukti dengan QR Code
- ✅ Arsip & Laporan Data
- ✅ Mobile Responsive (fix update terbaru)

**Potential Enhancement:**
- 🔄 Edit/Delete Nomor (belum ada)
- 📈 Statistics Dashboard
- 📧 Email notifikasi
- 📱 Native Mobile App
- 🔐 Two-factor authentication
- 📄 Export to PDF/Excel
- 🔍 Advanced search & filter
- 👥 User roles & permissions

---

## 📞 Support & Kontak

**Institusi:** Sekretariat DPRD Kabupaten Padang Pariaman  
**Email:** sekretariatdewanpdgprm@gmail.com  
**Alamat:** Jl. Mohd. Syafei No. 8 Kampung Perak Pariaman  
**Repository:** https://github.com/sekretariatdewanpdgprm-ops/sadati

---

## 📋 Changelog

### v1.0.1 (Latest - 24 Juli 2026)
- **Fix:** Perbaiki tampilan halaman di mobile/handphone
- **Change:** Ubah CSS print media query dari `visibility: hidden` ke `display: none`
- **Reason:** iOS Safari tidak support media query visibility dengan baik
- **Result:** Halaman normal di mobile, cetak tetap sempurna

### v1.0 (Initial Release)
- Login sistem
- Generate SPT & SPPD otomatis
- Cetak bukti dengan QR Code
- Arsip & laporan data
- Responsive design Bootstrap 5

---

## ✨ Catatan Teknis

- Aplikasi berjalan 100% client-side (no backend processing di local)
- Semua data processing via Google Apps Script
- Session data tidak persistent (refresh = logout)
- No database local (all via Google Sheets)
- Optimal untuk 1-2 pengguna concurrent
- QR Code generated via external API (qrserver.com)

---

**Dokumentasi Dibuat:** 24 Juli 2026  
**Versi Dokumentasi:** 1.0  
**Last Updated:** 24 Juli 2026
