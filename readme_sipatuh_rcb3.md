# SIPATUH RCB3 🏫
**Sistem Informasi Penegakan Tata Tertib dan Kehadiran SD Negeri Rancabentang 3**

SIPATUH RCB3 adalah sebuah aplikasi berbasis web ringan (Web App) yang dirancang khusus untuk membantu pendidik dan staf di SD Negeri Rancabentang 3 dalam mencatat, melacak, dan mengelola kedisiplinan serta kehadiran siswa. Aplikasi ini dikembangkan untuk berjalan di atas ekosistem **Google Apps Script (GAS)** dan **Google Sheets** sebagai basis datanya.

---

## ✨ Fitur Utama

1. **Dashboard Interaktif**: Menampilkan ringkasan statistik secara *real-time* (total keterlambatan bulan ini, pelanggaran tercatat, dan guru piket hari ini).
2. **Keterlambatan Siswa**: Modul untuk mencatat data siswa yang datang terlambat beserta alasannya.
3. **Pelanggaran Siswa**: Modul untuk mencatat pelanggaran tata tertib (atribut, rambut, membolos, dll) lengkap dengan sistem poin dan tindak lanjut.
4. **Kehadiran Siswa**: Modul untuk mencatat ketidakhadiran siswa dengan status Sakit, Izin, atau Alpha.
5. **Jadwal Piket Guru**: Modul untuk mengelola jadwal tugas guru piket harian.
6. **Ekspor Excel**: Setiap data tabel dapat diunduh langsung ke dalam format `.xlsx` (Excel) untuk keperluan laporan fisik/cetak menggunakan pustaka SheetJS.
7. **Responsif (Mobile-Friendly)**: Antarmuka dibangun menggunakan Tailwind CSS sehingga nyaman diakses melalui komputer (PC/Laptop) maupun perangkat seluler (HP).

---

## 🛠️ Teknologi yang Digunakan

* **Frontend**: HTML5, JavaScript (Vanilla)
* **Styling**: [Tailwind CSS](https://tailwindcss.com/) (via CDN)
* **Ikon**: [FontAwesome 6](https://fontawesome.com/) (via CDN)
* **Ekspor Data**: [SheetJS (xlsx)](https://sheetjs.com/)
* **Backend & Database** *(Target Deployment)*: Google Apps Script & Google Sheets

---

## 🚀 Panduan Instalasi & Deployment (Google Apps Script)

Kode HTML saat ini menggunakan data simulasi agar antarmuka dapat diuji langsung. Untuk menghubungkannya secara nyata dengan Google Sheets, ikuti langkah-langkah berikut:

### Langkah 1: Siapkan Google Sheets
1. Buka [Google Sheets](https://sheets.google.com) dan buat *spreadsheet* baru.
2. Beri nama *spreadsheet* tersebut (misal: `Database_SIPATUH`).
3. (Opsional) Buat beberapa *sheet* di bawahnya sesuai kebutuhan: `Keterlambatan`, `Pelanggaran`, `Kehadiran`, `Piket`.

### Langkah 2: Buka Editor Google Apps Script
1. Dari Google Sheets Anda, klik menu **Ekstensi** > **Apps Script**.
2. Anda akan dibawa ke tab baru berisi editor kode.

### Langkah 3: Tambahkan Kode Backend (`Code.gs`)
Pada file `Code.gs`, masukkan kode dasar berikut untuk merender file HTML Anda:

```javascript
function doGet() {
  // Merender file Index.html saat URL aplikasi diakses
  return HtmlService.createHtmlOutputFromFile('Index')
    .setTitle('SIPATUH RCB3 - SD Negeri Rancabentang 3')
    .addMetaTag('viewport', 'width=device-width, initial-scale=1');
}

// Catatan: Di sinilah Anda nantinya menambahkan fungsi-fungsi 
// untuk membaca/menulis ke Google Sheets.
// Contoh: function simpanPelanggaran(data) { ... }
```

### Langkah 4: Tambahkan Kode Frontend (`Index.html`)
1. Di panel kiri Apps Script, klik tombol **+** (Tambahkan File) > **HTML**.
2. Beri nama file tersebut **Index** (tanpa ekstensi .html, sistem akan menambahkannya otomatis).
3. Hapus kode bawaan, lalu **Paste/Tempel** seluruh kode HTML SIPATUH RCB3 yang telah Anda miliki ke dalam file `Index.html` ini.

### Langkah 5: Publikasikan sebagai Web App
1. Di kanan atas editor Apps Script, klik tombol biru **Terapkan (Deploy)** > **Deployment Baru**.
2. Pilih jenis deployment: **Aplikasi Web** (ikon roda gigi ⚙️).
3. Isi deskripsi (misal: "Versi 1.0").
4. Pada opsi **Jalankan sebagai**, pilih **Saya (email Anda)**.
5. Pada opsi **Siapa yang memiliki akses**, pilih sesuai kebutuhan (misal: **Siapa saja** jika ingin diakses guru lain, atau **Hanya saya**).
6. Klik **Terapkan**.
7. *Beri otorisasi jika diminta.*
8. Salin **URL Aplikasi Web** yang diberikan. Ini adalah link yang bisa Anda bagikan ke guru-guru untuk diakses via HP/Komputer.

---

## 💡 Pengembangan Lanjutan

Untuk membuat aplikasi ini benar-benar menyimpan data ke Google Sheets (bukan hanya di *browser*), Anda perlu menghubungkan fungsi JavaScript di frontend (`form.addEventListener`) dengan backend menggunakan `google.script.run`.

**Contoh sederhana:**
Ubah bagian *submit* form pelanggaran di `Index.html` menjadi:
```javascript
google.script.run
  .withSuccessHandler(function() {
      alert("Data berhasil disimpan ke Google Sheets!");
      // Panggil fungsi render tabel...
  })
  .simpanDataPelanggaran(newData); // 'simpanDataPelanggaran' adalah fungsi di Code.gs
```

---
*Dikembangkan untuk SD Negeri Rancabentang 3 | Hak Cipta &copy; 2026*