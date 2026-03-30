# 🏅 Latihan OSN SD — Olimpiade Sains Nasional

Platform latihan soal **HOTS** berbasis kisi-kisi resmi OSN 2025 untuk siswa Sekolah Dasar. Tersedia sepenuhnya di browser tanpa perlu instalasi — cukup buka dan mulai berlatih.

🔗 **[Buka Platform → (GitHub Pages)](https://your-username.github.io/your-repo-name)**

---

## 📚 Mata Pelajaran

| Mata Pelajaran | Status | Jumlah Soal | Topik |
|---|---|---|---|
| **IPA** (Ilmu Pengetahuan Alam) | ✅ Tersedia | 150 soal | 13 topik |
| **IPS** (Ilmu Pengetahuan Sosial) | 🚧 Segera Hadir | — | — |

---

## ✨ Fitur

- **Soal HOTS level C4–C6** — Analisis, evaluasi, dan kreasi, bukan sekadar hafalan
- **Pilihan ganda biasa & kompleks** — Melatih ketelitian memilih lebih dari satu jawaban yang benar
- **Soal dan opsi diacak** setiap sesi sehingga latihan selalu terasa baru
- **Konfirmasi per soal** — Langsung lihat jawaban benar/salah setelah menjawab
- **Penjelasan mendalam** di setiap soal untuk pemahaman konsep yang kuat
- **Rekap hasil per topik** — Mudah mengidentifikasi materi mana yang perlu diperkuat
- **Tanpa instalasi** — Murni HTML/CSS/JS, berjalan langsung di browser

---

## 🔬 Topik OSN IPA SD

| # | Topik |
|---|---|
| 1 | Keterampilan & Metode Ilmiah |
| 2 | Keanekaragaman Hayati & Klasifikasi |
| 3 | Proses & Mekanisme Makhluk Hidup |
| 4 | Ekologi, Lingkungan & Pelestarian |
| 5 | Fisika — Gaya, Gerak & Energi |
| 6 | Fisika — Cahaya, Bunyi & Gelombang |
| 7 | Fisika — Listrik & Magnet |
| 8 | Kimia Dasar & Perubahan Materi |
| 9 | Bumi, Tata Surya & Antariksa |
| 10 | Teknologi & Penerapan Sains |
| 11 | Kesehatan & Gizi |
| 12 | Lingkungan & Perubahan Iklim |
| 13 | Soal Terpadu & Analisis Data |

---

## 🗂️ Struktur Repository

```
.
├── index.html                          # Halaman utama
├── OSN-IPA-SD-Latihan-Olimpiade.html   # Aplikasi latihan OSN IPA
├── OSN-IPS-SD-Latihan-Olimpiade.html   # Aplikasi latihan OSN IPS (segera)
└── README.md
```

---

## 🚀 Cara Menggunakan

### Secara Online (GitHub Pages)
Kunjungi langsung link GitHub Pages di bagian atas README ini.

### Secara Lokal
```bash
# Clone repository
git clone https://github.com/your-username/your-repo-name.git

# Masuk ke folder
cd your-repo-name

# Buka di browser (tidak perlu server)
open index.html
```

> Tidak diperlukan Node.js, Python, atau server apapun. Cukup buka file HTML di browser.

---

## ⚙️ Mengaktifkan GitHub Pages

1. Buka halaman repository di GitHub
2. Pergi ke **Settings → Pages**
3. Di bagian *Source*, pilih branch `main` dan folder `/ (root)`
4. Klik **Save**
5. Tunggu beberapa menit, lalu akses di `https://your-username.github.io/your-repo-name`

---

## 🛠️ Pengembangan

Platform ini dibangun sepenuhnya dengan **vanilla HTML, CSS, dan JavaScript** — tidak ada framework atau dependensi eksternal selain Google Fonts. Semua soal tersimpan langsung di dalam file HTML.

### Menambahkan Soal Baru
Soal disimpan dalam array `questionBank` di dalam file HTML. Setiap soal mengikuti struktur berikut:

```javascript
{
  id: 1,
  topicId: 1,
  topicName: "Nama Topik",
  type: "single",      // "single" atau "multiple"
  question: "Teks pertanyaan...",
  options: ["Opsi A", "Opsi B", "Opsi C", "Opsi D"],
  correct: [0],        // Index jawaban benar (0-based), bisa lebih dari satu
  explanation: "Penjelasan lengkap mengapa jawaban ini benar..."
}
```

---

## 📄 Lisensi

Proyek ini bersifat open-source dan bebas digunakan untuk keperluan pendidikan non-komersial.

---

*Semangat belajar! Persiapan yang baik adalah kunci sukses OSN.* 🌟
