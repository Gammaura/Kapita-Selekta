# FASE 1: IDEASI, KERANGKA PICOS, DAN PERTANYAAN PENELITIAN
## Mata Kuliah: Kapita Selekta — Fakultas Ilmu Komputer, Universitas Esa Unggul

---

### Judul Penelitian

**Rancang Bangun Multi-Agent System Berbasis Natural Language Processing untuk Otomatisasi Deteksi Struktur dan Formatting Dokumen Tugas Akhir (Studi Kasus: Fakultas Ilmu Komputer Universitas Esa Unggul)**

Sistem yang dirancang diberi nama **Asdoku** (Asisten Dokumenku).

---

## 1. Kerangka PICOS

Kerangka PICOS dipakai untuk merumuskan masalah dan menurunkan pertanyaan tinjauan literatur (subbab 2.1.1 draf proposal).

| Komponen | Rumusan |
| :--- | :--- |
| **P** — *Platform / Target User* | Aplikasi web (FastAPI) yang dijalankan secara lokal dan memproses naskah akademik berformat .docx melalui struktur Office Open XML (OOXML). Pengguna sasaran: mahasiswa Fakultas Ilmu Komputer Universitas Esa Unggul yang menyusun tugas akhir; penerima manfaat tidak langsung: dosen pembimbing dan fakultas. |
| **I** — *Intervention* | Sistem multi-agen hibrida berbasis NLP yang terdiri atas tiga agen dengan peran terpisah: **Agen 1 — Inspector** (klasifikasi struktur dengan *machine learning* atas 437 fitur: 400 TF-IDF + 37 metadata), **Agen 2 — Quality Critic** (audit berbasis aturan pedoman dan konteks dokumen; dua gerbang: Tier 1 dan Tier 2), dan **Agen 3 — Formatting Actuator** (penyusunan ulang .docx di atas template resmi tanpa mengubah isi, serta perbaikan terarah per kriteria). |
| **C** — *Comparison* | (1) Model klasifikasi tunggal: Agen 1 saja, dibandingkan dengan aturan Agen 2 saja dan sistem multi-agen lengkap (uji ablasi arsitektur). (2) Antarmodel: Random Forest, Logistic Regression, dan XGBoost. (3) Antarkelompok fitur: TF-IDF saja, metadata saja, dan gabungan (uji ablasi fitur). (4) Pemeriksaan dan perapian format secara manual sebagai proses berjalan. |
| **O** — *Outcome* | (1) Ketepatan deteksi struktur: macro-F1 terhadap label yang diverifikasi manusia, pada naskah yang tidak dipakai selama pengembangan. (2) Kepatuhan format: 8 kriteria pedoman, diperiksa otomatis dan diverifikasi manual di Microsoft Word. (3) Keutuhan isi: selisih jumlah kata, tabel, gambar, sitasi, dan catatan kaki sebelum–sesudah (target 0). (4) Waktu proses per naskah. |
| **S** — *Subject* (objek kasus dan spesifikasi data) | Naskah tugas akhir lengkap mahasiswa Fakultas Ilmu Komputer UEU, berformat .docx, berbahasa Indonesia, diperoleh dengan izin tertulis penulis. Unit analisis adalah paragraf (elemen `w:p`), diberi satu dari 9 label kelas struktur. Korpus: 6 naskah pengembangan dengan 6.673 paragraf (4 latih, 2 validasi) dan minimal 4 naskah uji baru yang dikumpulkan pada TA-2. Proposal tugas akhir, laporan magang/MBKM, PDF, .doc, dan hasil pindaian **tidak** termasuk. |

Pada Bab II draf proposal, huruf **S** dibaca sebagai *Study design* mengikuti kebiasaan PRISMA, yaitu penelitian rancang bangun dengan evaluasi eksperimental dalam dua fase (perancangan pada TA-1, pembangunan dan evaluasi pada TA-2). Kedua pembacaan tidak bertentangan: tabel di atas mengikuti templat Kapita Selekta, sedangkan Bab II mengikuti PRISMA.

**Catatan tentang angka.** Dokumen Fase 1 versi sebelumnya mencantumkan angka capaian prototipe (akurasi, skor kepatuhan, dan waktu proses). Angka tersebut **ditarik** dan tidak dipakai lagi, karena label data latih prototipe belum diverifikasi manusia dan sebagian naskah ujinya ikut dipakai menyetel aturan (subbab 3.1 draf proposal). Bagian *Outcome* di atas karenanya berisi **ukuran yang akan dipakai**, bukan hasil. Hasil baru tersedia setelah evaluasi TA-2.

---

## 2. Tiga Pertanyaan Penelitian (RQ)

Tiga RQ berikut diturunkan dari PICOS dan menjadi dasar empat rumusan masalah (RM) pada Bab I draf proposal.

### RQ 1.1 — Representasi fitur untuk deteksi struktur

> *Bagaimana merancang representasi fitur berbasis Natural Language Processing yang dipadukan dengan metadata OOXML untuk mengklasifikasikan elemen struktur dokumen tugas akhir?*

- **Kaitan dengan judul:** “Berbasis Natural Language Processing” dan “Deteksi Struktur”.
- **Padanan di proposal:** RM 1 dan Tujuan 1.
- **Cara menjawab:** rancangan 437 fitur (Tabel 3.11), perbandingan model (EX-1), dan ablasi fitur (EX-2).

### RQ 1.2 — Rancang bangun arsitektur multi-agen dan otomatisasi format

> *Bagaimana merancang bangun arsitektur Multi-Agent System yang terdiri atas agen deteksi, agen pengendali mutu, dan agen formatting untuk mengotomatisasi deteksi struktur dan formatting dokumen tugas akhir sesuai Pedoman Penulisan Tugas Akhir UEU 2018?*

- **Kaitan dengan judul:** “Rancang Bangun Multi-Agent System” dan “Otomatisasi … Formatting”.
- **Padanan di proposal:** RM 2 dan Tujuan 2.
- **Cara menjawab:** cetak biru sistem pada Bab III (subbab 3.5–3.7), lalu uji fungsional (EX-7), waktu proses (EX-6), dan uji injeksi cacat (EX-8).

### RQ 1.3 — Kinerja deteksi dan mutu berkas hasil

> *Bagaimana kinerja deteksi struktur sistem (macro-F1 terhadap label manual pada naskah yang tidak digunakan dalam pengembangan), apakah kolaborasi agen meningkatkan kinerja dibandingkan model machine learning saja, dan bagaimana tingkat kepatuhan format serta keutuhan isi dokumen hasil ketika diperiksa di Microsoft Word?*

- **Kaitan dengan judul:** pembuktian empiris seluruh sistem.
- **Padanan di proposal:** RM 3 dan RM 4; Tujuan 3 dan 4.
- **Cara menjawab:** ablasi arsitektur dan uji McNemar (EX-3), kepatuhan 8 kriteria (EX-4), keutuhan isi (EX-5), dan injeksi cacat (EX-8).

---

## 3. Pemetaan RQ ke Rumusan Masalah Proposal

| RQ Fase 1 | Rumusan masalah di proposal | Eksperimen (Tabel 3.25) |
| :--- | :--- | :--- |
| RQ 1.1 | RM 1 — representasi fitur NLP + metadata OOXML | EX-1, EX-2 |
| RQ 1.2 | RM 2 — arsitektur tiga agen | EX-6, EX-7, EX-8 |
| RQ 1.3 | RM 3 — kinerja deteksi dan kontribusi kolaborasi agen | EX-1, EX-3 |
| RQ 1.3 | RM 4 — kepatuhan format dan keutuhan isi | EX-4, EX-5, EX-8 |
