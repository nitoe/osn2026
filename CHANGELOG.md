# CHANGELOG — Latihan OSN SD
> Platform latihan soal HOTS berbasis kisi-kisi resmi OSN 2025  
> Dikembangkan oleh **Arif Azwar Anas** — Wakil Kepala Sekolah Bidang Kurikulum, SD Muhammadiyah 01 Kukusan

---

## [3.0.1] — 2025-05-01 · Hotfix: Pengaturan Sesi & Tombol Mulai
> File yang diubah: `OSN-Matematika-SD-Latihan-Olimpiade.html` saja

### Penyebab Masalah
Ditemukan **3 bug berlapis** yang menyebabkan pengaturan jumlah soal dan tombol "Mulai Latihan" tidak berfungsi:

| # | Bug | Lokasi | Dampak |
|---|-----|--------|--------|
| 1 | **Syntax error JS** — dua koma hilang di batas antar-batch soal (antara id:100→101 dan id:200→201) | `questionBank` array | Seluruh JavaScript gagal di-parse browser → semua tombol mati |
| 2 | **Event listener menumpuk** — `initHome()` menggunakan `addEventListener` lalu dipanggil ulang oleh `restartQuiz()` setiap sesi selesai | `function initHome()` | Setelah restart, setiap klik tombol memicu handler berganda; state `nQuestions` bisa di-set berkali-kali tak tentu |
| 3 | **Visual tombol tidak sinkron** — tidak ada mekanisme untuk memperbarui tampilan tombol terpilih setelah restart | `function restartQuiz()` | Tombol yang tampak "terpilih" tidak mencerminkan nilai `state.nQuestions` yang sebenarnya |

### Diperbaiki
- **Koma hilang** di dua titik batas batch: setelah soal id:100 dan id:200 di array `questionBank` — inilah penyebab utama seluruh JS tidak berjalan
- **`initHome()`** direfaktor: logika wiring tombol n-btn dipindahkan ke fungsi terpisah, menggunakan properti `.onclick` (menggantikan, bukan menambah) sebagai ganti `addEventListener`
- **`syncHomeScreen()`** dibuat sebagai fungsi baru — hanya menyinkronkan tampilan visual tombol terpilih berdasarkan `state.nQuestions`, tanpa menyentuh event listener
- **`restartQuiz()`** kini memanggil `syncHomeScreen()` bukan `initHome()` — event listener hanya terpasang sekali seumur hidup halaman
- **Boot sequence** dipertegas: `initHome()` dipanggil **sekali** via `window.addEventListener('load')` saja
- **Console logging** ditambahkan di titik-titik kritis untuk memudahkan debugging di browser DevTools:
  - `[OSN] Boot — questionBank size: 300` saat halaman dimuat
  - `[OSN] nQuestions set to X` saat tombol pilihan soal diklik
  - `[OSN] startQuiz — nQuestions: X | pool size: 300` saat kuis dimulai
  - `[OSN] Session built — actual questions: X` setelah soal dipilih

---


### Ditambahkan
- **OSN Matematika SD** — kuis baru dengan arsitektur yang dirancang khusus untuk mata pelajaran matematika
- **KaTeX** (v0.16.9) via CDN untuk rendering persamaan matematika (`$...$` dan `$$...$$`) — menggantikan teks biasa yang tidak terbaca untuk pecahan, akar, pangkat, sigma, dll.
- **16 jenis ilustrasi SVG inline** yang dirender langsung oleh JavaScript tanpa dependensi eksternal:
  - Geometri: `rect`, `triangle`, `trapezoid`, `parallelogram`, `kite`, `lShape`, `cube`, `box3d`, `triangularPrism`
  - Bilangan: `numberLine`, `fractionBar`
  - Koordinat: `coordPlane`
  - Statistika: `barChart`, `pie`
  - Kombinatorik: `grid`, `dotPattern`
- **300 soal pool** terbagi rata 60 soal per bidang: Bilangan · Aritmatika · Geometri · Statistika & Pengukuran · Kombinatorik
- **Pilihan sesi 50 soal** (sebelumnya maks 40) untuk semua kuis
- Field `illustration` pada setiap objek soal — berisi string SVG atau `null`
- Tipe soal **Pilihan Ganda Kompleks** (`type: "multiple"`) untuk soal yang memiliki lebih dari satu jawaban benar
- Render KaTeX di tiga titik: teks soal, pilihan jawaban, dan panel pembahasan di layar review

### Diubah
- **index.html** — ditambahkan kartu OSN Matematika, statistik diperbarui (750 soal · 23 topik · 3 mata pelajaran)
- Proses boot kuis menggunakan `window.onload` (sebelumnya `DOMContentLoaded`) agar KaTeX CDN pasti selesai dimuat sebelum render
- Layar review menampilkan teks soal penuh (bukan versi stripped) sehingga KaTeX bisa dirender di sana juga

### Diperbaiki
- 15+ kesalahan kunci jawaban diaudit dan diperbaiki di batch 1–3
- Semua kalimat "Hmm" / "Tunggu" di teks penjelasan dihapus dan diganti penjelasan bersih
- Opsi duplikat (id:214) diperbaiki
- Soal id:34 direvisi agar jawaban benar tersedia di pilihan (kapasitas tangki)
- Soal id:36 direvisi dengan nilai yang logis untuk tinggi badan
- Soal id:91 direvisi agar pilihan jawaban mencakup jawaban yang benar (440)
- Soal id:58 opsi diperbaiki agar mencakup nilai eksak (263,76 cm²)
- Soal id:294 opsi diperbaiki agar mencakup jawaban eksak (102)

---

## [2.0.0] — 2025-03-15
### Ditambahkan
- **OSN IPS SD** — kuis mata pelajaran Ilmu Pengetahuan Sosial
- 60 soal pool IPS mencakup 5 bidang: Kenampakan Alam & Budaya · Keragaman Sosial · Kegiatan Ekonomi · Perkembangan Sejarah Indonesia · Metode Ilmiah IPS

### Diubah
- **index.html** — ditambahkan kartu OSN IPS, statistik diperbarui (450 soal · 18 topik · 2 mata pelajaran)
- Desain kartu mata pelajaran di halaman utama diperbarui dengan status badge "● Tersedia"

---

## [1.0.0] — 2025-02-01
### Rilis Awal
- **index.html** — halaman utama platform dengan hero section, stats row, kartu mata pelajaran, panduan cara pakai, dan footer
- **OSN IPA SD** — kuis mata pelajaran Ilmu Pengetahuan Alam
- 390 soal pool IPA mencakup 13 topik sesuai silabus OSN 2025:
  1. Keterampilan & Metode Ilmiah
  2. Keanekaragaman Hayati & Klasifikasi
  3. Proses & Mekanisme pada Makhluk Hidup
  4. Ekologi, Lingkungan & Pelestarian
  5. Isu Kesehatan, Lingkungan & Teknologi
  6. Mekanika
  7. Wujud Benda
  8. Listrik & Magnet
  9. Gelombang & Optik
  10. Suhu & Kalor
  11. Bentuk Energi & Perubahannya
  12. Bumi, Tata Surya & Antariksa
  13. Kimia Dasar

### Fitur Inti (berlaku di semua kuis)
- **Pool soal acak** — soal dan pilihan jawaban diacak setiap sesi baru
- **Pembagian topik merata** — soal dipilih proporsional dari setiap bidang
- **Konfirmasi per soal** — jawaban dikunci saat tombol "Konfirmasi" ditekan, tidak bisa diubah
- **Navigasi bebas** — bisa mundur ke soal sebelumnya setelah dikonfirmasi (read-only)
- **Layar hasil** — skor cincin animasi, statistik (benar/salah/dilewati), dan capaian per topik dengan progress bar
- **Layar review** — semua soal dapat dibuka accordion, menampilkan status jawaban, jawaban benar, dan penjelasan mendalam
- **Responsive design** — dioptimalkan untuk ponsel (mayoritas siswa SD menggunakan HP orang tua)
- **Single HTML file** — tidak perlu server, backend, atau koneksi internet setelah dimuat (kecuali font Google Fonts)
- **Pengaturan sesi** — pilih 20, 30, atau 40 soal per sesi

---

## Roadmap

| Prioritas | Fitur | Status |
|-----------|-------|--------|
| Tinggi | Tambah soal pool hingga 500/mata pelajaran | 🔄 Dalam rencana |
| Tinggi | Mode "Latihan Topik Tertentu" — fokus satu bidang saja | 🔄 Dalam rencana |
| Sedang | Timer/countdown per soal untuk simulasi kondisi olimpiade | 🔄 Dalam rencana |
| Sedang | Simpan progres ke localStorage agar bisa dilanjutkan | 🔄 Dalam rencana |
| Sedang | Halaman statistik kumulatif antar sesi | 🔄 Dalam rencana |
| Rendah | Mode cetak soal (print-friendly layout) | 🔄 Dalam rencana |
| Rendah | OSN mata pelajaran lain (jika ada perubahan silabus) | 🔄 Dalam rencana |

---

## Catatan Teknis

### Arsitektur File
```
osn2026/
├── index.html                           # Halaman utama (portal)
├── OSN-IPA-SD-Latihan-Olimpiade.html    # Kuis IPA (390 soal)
├── OSN-IPS-SD-Latihan-Olimpiade.html    # Kuis IPS (60 soal)
├── OSN-Matematika-SD-Latihan-Olimpiade.html  # Kuis Matematika (300 soal)
├── CHANGELOG.md                         # File ini
└── README.md                            # Deskripsi proyek
```

### Stack Teknologi
| Komponen | Teknologi | Keterangan |
|----------|-----------|------------|
| Struktur | HTML5 single file | Tidak butuh build tool |
| Styling | CSS custom properties | Tanpa framework CSS |
| Logika | Vanilla JavaScript | Tanpa framework JS |
| Font | Google Fonts (Plus Jakarta Sans, Nunito) | CDN |
| Persamaan | KaTeX v0.16.9 | CDN, hanya Matematika |
| Ilustrasi | SVG inline (string JS) | Tanpa file gambar eksternal |

### Konvensi Struktur Soal (Matematika)
```javascript
{
    id: 101,                     // ID unik, integer
    topicId: 1,                  // 1–5 (sesuai TOPICS array)
    topicName: "Bilangan",       // Nama bidang
    type: "single"|"multiple",   // Jenis soal
    question: "Teks $\\LaTeX$",  // Mendukung KaTeX inline
    illustration: SVG.rect(10,5) // String SVG, atau null
    options: ["A","B","C","D"],  // 2–4 opsi, mendukung KaTeX
    correct: [0],                // Index jawaban benar (0-based)
    explanation: "Penjelasan $\\LaTeX$"  // Mendukung KaTeX
}
```

### Cara Menambah Soal Baru
Sisipkan objek soal baru sebelum komentar `]; // END questionBank` di file HTML yang bersangkutan. ID harus unik dan lanjut dari ID terakhir. Tidak ada proses build — langsung bisa digunakan setelah disimpan.
