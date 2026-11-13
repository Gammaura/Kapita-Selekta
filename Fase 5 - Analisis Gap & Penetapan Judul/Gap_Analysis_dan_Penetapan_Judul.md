# ANALISIS CELAH PENELITIAN & PENETAPAN JUDUL TUGAS AKHIR
## Matriks Silang BRD × SLR — Asdoku

Dokumen ini menyilangkan 17 kebutuhan fungsional pada [BRD](../Fase%203%20-%20Dokumen%20BRD/BRD_Business_Requirements_Document.md) dengan 23 studi pada [SLR](../Fase%204%20-%20Dokumen%20SLR/SLR_Systematic_Literature_Review.md). Hasilnya dipakai untuk menetapkan celah penelitian dan judul. Isinya selaras dengan subbab 2.1.4 draf proposal.

Dokumen ini tidak memuat angka kinerja sistem. Yang disebut “fakta” di bawah adalah isi BRD dan temuan literatur; nilai skor adalah penilaian peneliti sendiri.

---

## Tahap 1 — Matriks Silang FR (BRD) × Solusi Eksisting (SLR)

Status: **Terpenuhi** = cara mengerjakannya sudah mapan di literatur; **Sebagian** = ada pendekatan serupa tetapi belum untuk kebutuhan ini; **Belum Ada** = tidak ditemukan pada 23 studi.

| FR | Kebutuhan (BRD) | Solusi eksisting (SLR) | Status | Catatan celah |
| :---: | :--- | :--- | :---: | :--- |
| FR-01 | Unggah .docx lewat aplikasi web; tolak berkas lain | E3 (Kolinu et al., 2025) membangun aplikasi web pemeriksa naskah .docx | Terpenuhi | Bukan kebaruan. |
| FR-02 | Ekstraksi 437 fitur: TF-IDF + tipografi OOXML + gaya Word + pola teks | S06 (fitur teks); D1 dan D3 (paduan teks dan tampilan pada PDF); E4 (TF-IDF untuk judul bab); E5 (*resolver* format OOXML) | Sebagian | Paduan teks dan tampilan sudah dikenal, tetapi belum diterapkan pada paragraf .docx untuk naskah tanpa *style*. |
| FR-03 | Klasifikasi paragraf ke 9 kelas struktur dengan ML | S05 (algoritma klasik untuk NLP); D1 (klasifikasi zona); E1 (ML untuk kesesuaian format) | Sebagian | E1 mendeteksi kesesuaian format, bukan peran struktural tiap paragraf. |
| FR-04 | Menandai paragraf ambigu (keyakinan < 0,70) | Tidak dibahas khusus pada 23 studi | Belum Ada | Dipakai sebagai penanda paragraf yang perlu dicek penulis. |
| FR-05 | Audit aturan: aturan pasti, zona dokumen, urutan bab, alasan koreksi | S02, S10 (kontrol simbolik atas model); E2–E5 (aturan format) | Sebagian | Aturan pada E2–E5 memeriksa format; belum ada aturan konteks dokumen yang mengoreksi hasil model. |
| FR-06 | Putaran koreksi Agen 2 → Agen 1 sampai konvergen | S11 (peran pelaksana–peninjau); S01, S03 (syarat sistem multi-agen) | Sebagian | Pola pelaksana–peninjau dikenal pada agen LLM; belum dalam bentuk deterministik untuk dokumen. |
| FR-07 | Penyusunan di atas template: kertas, margin, huruf, spasi | E2–E5 memeriksa aspek ini dan melaporkan kesalahan | Belum Ada | Tidak ada yang menerapkan perbaikannya. |
| FR-08 | *Heading Styles* bernomor otomatis | E5 membaca pewarisan *style*; tidak memasang | Belum Ada | — |
| FR-09 | Nomor halaman Romawi/Arab lewat *section*; header | E5 memeriksa sebagian aturan halaman | Belum Ada | — |
| FR-10 | *Caption* bernomor per bab, tabel APA 7, daftar pustaka | E2, E3, E5 memeriksa sebagian | Belum Ada | — |
| FR-11 | Daftar Isi, Daftar Tabel, Daftar Gambar sebagai *field* | Tidak ditemukan | Belum Ada | — |
| FR-12 | Uji 8 kriteria; daftar cacat terstruktur dan skor | E5 (44 aturan, evaluasi injeksi kesalahan); S14 (evaluasi bertingkat) | Terpenuhi | Pemeriksaan format berbasis aturan sudah mapan; E5 lebih luas cakupan aturannya. |
| FR-13 | Perbaikan terarah per kriteria tanpa mengubah isi, lalu uji ulang | E4 memberi rekomendasi perbaikan; tidak ada yang memperbaiki berkas | Belum Ada | Celah terkuat: sistem yang ada berhenti pada pelaporan. |
| FR-14 | Menampilkan skor, sisa cacat, log koreksi beserta alasan | E2, E3, E5 menampilkan laporan kesalahan | Terpenuhi | Bukan kebaruan. |
| FR-15 | Unduh hasil; unggahan dihapus | E3 | Terpenuhi | Bukan kebaruan. |
| FR-16 | Koreksi Agen 2 dicatat ke pool berstatus “belum ditinjau” | Supervisi lemah (Ratner et al., 2017; Liu, Lu, & Mou, 2023; D3) | Sebagian | Literatur memakai label lemah untuk melatih; di sini label lemah ditahan sampai ditinjau. |
| FR-17 | Tinjauan peneliti, pelatihan ulang dengan uji non-regresi, pembekuan sistem | D2, D3 membangun korpus dengan label otomatis tanpa verifikasi | Sebagian | Kendali mutu label sebelum pelatihan ulang belum dibahas. |

**Ringkasan:** Terpenuhi 4 (FR-01, 12, 14, 15); Sebagian 6 (FR-02, 03, 05, 06, 16, 17); Belum Ada 7 (FR-04, 07, 08, 09, 10, 11, 13).

Pola yang terlihat: literatur sudah kuat pada **memeriksa** format (FR-12) dan pada gagasan arsitektur hibrida. Yang belum ada adalah **memperbaiki berkas** (FR-07 s.d. FR-11, FR-13) dan mengenali struktur pada naskah yang tidak memakai *style* (FR-02, FR-03).

---

## Tahap 2 — Skoring Kandidat Gap

| Kandidat gap | Jenis gap | Novelty (1–10) | Kelayakan (1–10) | Dampak (1–10) | Total |
| :--- | :--- | :---: | :---: | :---: | :---: |
| **Gap 1.** Belum ada arsitektur multi-agen hibrida yang sekaligus mendeteksi struktur dan merekonstruksi berkas .docx tanpa menghilangkan isi (FR-05 s.d. FR-11, FR-13) | Metodologis dan konteks | 8 | 7 | 9 | **24** |
| **Gap 2.** Belum tersedia korpus naskah tugas akhir berbahasa Indonesia dengan label struktur yang diverifikasi manusia (FR-02, FR-03, FR-16, FR-17) | Dataset | 7 | 6 | 7 | 20 |
| **Gap 3.** Evaluasi sistem sejenis berhenti pada metrik klasifikasi atau deteksi pelanggaran; belum memeriksa kepatuhan dan keutuhan berkas akhir di Microsoft Word (FR-12, FR-13) | Performa | 7 | 8 | 7 | 22 |

**Gap terpilih: Gap 1.** Alasannya:

- **Fakta.** Lima penelitian format skripsi di Indonesia (E1–E5) melaporkan kesalahan dan menyerahkan perbaikan kepada penulis. Literatur multi-agen (S01–S04, S10, S11) merekomendasikan arsitektur hibrida dengan pembagian peran, tetapi tidak ada yang menerapkannya pada dokumen .docx.
- **Tafsiran.** Gap 2 dan Gap 3 tidak berdiri sendiri: korpus berlabel (Gap 2) adalah syarat untuk mengukur Gap 1 secara sahih, dan evaluasi berkas di Word (Gap 3) adalah cara membuktikan Gap 1. Mengambil Gap 2 atau Gap 3 saja tidak menjawab masalah mahasiswa.
- **Kebaruan yang diusulkan.** Tiga agen dengan peran dan kewenangan terpisah, dua putaran umpan balik yang benar-benar mengubah keluaran, dan perbaikan langsung pada berkas. Gap 2 dan Gap 3 tetap dikerjakan sebagai kontribusi pendukung, sehingga proposal menyebut ketiganya sebagai celah penelitian.

Nilai kelayakan Gap 1 tidak diberi angka tertinggi karena dua komponen masih harus dibangun pada TA-2 (daftar cacat terstruktur dan perbaikan terarah) dan label korpus belum diverifikasi manusia.

---

## Tahap 3 — Lima Kandidat Judul

Aturan templat: paling banyak 20 kata; spesifik; tanpa singkatan tak baku; menghindari frasa klise “Rancang Bangun”, “Implementasi”, “Studi Kasus”; berpola `[Metode] untuk [Outcome] pada [Objek]`; memuat metrik bila memungkinkan.

| No | Kandidat judul | Jumlah kata | Daya tarik (1–10) | Novelty (1–10) | Kelayakan (1–10) | Total |
| :---: | :--- | :---: | :---: | :---: | :---: | :---: |
| 1 | Rancang Bangun Multi-Agent System Berbasis Natural Language Processing untuk Otomatisasi Deteksi Struktur dan Formatting Dokumen Tugas Akhir (Studi Kasus: Fakultas Ilmu Komputer Universitas Esa Unggul) | 17 + 8 | 7 | 8 | 9 | **24** |
| 2 | Multi-Agent System Hibrida Berbasis Natural Language Processing untuk Deteksi Struktur dan Formatting Otomatis pada Dokumen Tugas Akhir | 17 | 8 | 8 | 8 | **24** |
| 3 | Kolaborasi Agen Machine Learning dan Agen Berbasis Aturan untuk Deteksi Struktur dan Perbaikan Format pada Naskah Tugas Akhir Berformat DOCX | 20 | 7 | 8 | 8 | 23 |
| 4 | Multi-Agent System Berbasis Natural Language Processing untuk Peningkatan Macro-F1 Deteksi Struktur dan Kepatuhan Format pada Dokumen Tugas Akhir | 18 | 7 | 7 | 7 | 21 |
| 5 | Klasifikasi Struktur Paragraf dengan Fitur TF-IDF dan Metadata OOXML untuk Formatting Otomatis pada Dokumen Tugas Akhir | 16 | 6 | 6 | 9 | 21 |

Pola `[Metode] untuk [Outcome] pada [Objek]`:

1. `[Multi-Agent System Berbasis NLP]` untuk `[Otomatisasi Deteksi Struktur dan Formatting]` pada `[Dokumen Tugas Akhir FASILKOM UEU]`.
2. `[Multi-Agent System Hibrida Berbasis NLP]` untuk `[Deteksi Struktur dan Formatting Otomatis]` pada `[Dokumen Tugas Akhir]`.
3. `[Kolaborasi Agen ML dan Agen Berbasis Aturan]` untuk `[Deteksi Struktur dan Perbaikan Format]` pada `[Naskah Tugas Akhir DOCX]`.
4. `[Multi-Agent System Berbasis NLP]` untuk `[Peningkatan Macro-F1 Deteksi Struktur dan Kepatuhan Format]` pada `[Dokumen Tugas Akhir]`.
5. `[Klasifikasi Struktur Paragraf dengan TF-IDF dan Metadata OOXML]` untuk `[Formatting Otomatis]` pada `[Dokumen Tugas Akhir]`.

---

## Tahap 4 — Penetapan Judul

### Judul yang dipakai

> **Rancang Bangun Multi-Agent System Berbasis Natural Language Processing untuk Otomatisasi Deteksi Struktur dan Formatting Dokumen Tugas Akhir (Studi Kasus: Fakultas Ilmu Komputer Universitas Esa Unggul)**

Ini adalah judul pada sampul draf proposal (kandidat 1).

**Mengapa kandidat 1.** Judul ini memuat ketiga unsur yang dijawab rumusan masalah: metode (multi-agen, NLP), keluaran (deteksi struktur dan *formatting* otomatis), dan objek (dokumen tugas akhir FASILKOM UEU). Frasa “Rancang Bangun” menyatakan jenis penelitiannya, dan anak judul membatasi klaim pada satu fakultas dan satu pedoman, sesuai batasan masalah.

**Dua hal yang menyimpang dari aturan templat:**

1. Judul memakai “Rancang Bangun” dan “Studi Kasus”, dua frasa yang disarankan dihindari.
2. Judul utama 17 kata, tetapi dengan anak judul menjadi 25 kata, melewati batas 20 kata.

Kandidat 2 memenuhi seluruh aturan templat dengan skor total yang sama. Pilihan di antara keduanya adalah keputusan dosen pembimbing; selama belum ada arahan lain, kandidat 1 dipertahankan agar sama dengan draf proposal.

### Perubahan dari judul versi Oktober 2026

| Versi lama | Versi sekarang | Alasan |
| :--- | :--- | :--- |
| “… Dokumen Akademik …” | “… Dokumen Tugas Akhir …” | Laporan magang/MBKM dikeluarkan dari cakupan; korpus hanya naskah tugas akhir lengkap. |
| Tanpa anak judul | “(Studi Kasus: Fakultas Ilmu Komputer Universitas Esa Unggul)” | Acuan format dan korpus hanya dari satu fakultas. |
| “… Berbasis NLP” di akhir | “… Berbasis NLP” setelah “Multi-Agent System” | Menegaskan bahwa NLP adalah dasar agen pendeteksi. |

### Versi untuk artikel jurnal

> *A Hybrid Multi-Agent System Combining Machine Learning and Rule-Based Control for Structure Detection and Formatting of Indonesian Undergraduate Theses*

Target jurnal belum ditetapkan; rencananya jurnal nasional terakreditasi SINTA.

### Paragraf pembuka latar belakang

Paragraf pembuka versi Oktober 2026 memuat klaim yang sudah tidak berlaku (lama perapian manual “2–4 jam” yang belum diukur, cakupan laporan kerja praktik, dan 420 fitur) sehingga dihapus. Latar belakang yang berlaku ada di [Draft_TA/sumber/bab1.md](../../Draft_TA/sumber/bab1.md).
