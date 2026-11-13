# FASE 2: PENELUSURAN LITERATUR & EVIDENCE MATRIX
## Sumber: Scopus (melalui Scopus AI, 2021–2026) ditambah penelusuran jurnal nasional dan rujukan fondasional

---

## 1. Alur Kerja Penelusuran dan Pengelolaan Referensi

| Alat | Dipakai untuk | Tahap | Keluaran di proyek ini |
| :--- | :--- | :--- | :--- |
| Scopus AI | Menelusuri basis data Scopus dan memetakan konsep | Ideasi dan eksplorasi celah | 126 publikasi teridentifikasi; laporan PDF di folder ini |
| Evidence matrix (dokumen ini) | Menyaring dan mengekstraksi metode, data, temuan, dan keterbatasan tiap studi | Penyaringan dan ekstraksi | 15 studi primer (S01–S15) + 8 studi tambahan (D1–D3, E1–E5) |
| Mendeley | Mengelola referensi, sitasi, dan daftar pustaka | Sepanjang penulisan | Daftar Referensi proposal (gaya APA) |
| LLM | Membantu menyusun kerangka dan draf | Penyusunan Bab I–V | Draf proposal; seluruh klaim dan sitasi diperiksa ulang terhadap sumber |
| Turnitin | Memeriksa kemiripan | Pemeriksaan akhir | Belum dijalankan |

---

## 2. Kueri dan Protokol Pencarian

Penelusuran pada Scopus (judul, abstrak, kata kunci) menggabungkan tiga klaster kata kunci:

```text
(
  "Multi-Agent Systems" OR "Multi-Agent" OR "Agent Collaboration" OR
  "Agentic AI" OR "Role-Specialized Agents"
)
AND
(
  "Natural Language Processing" OR "NLP" OR "Unstructured Text" OR
  "Machine Learning" OR "Scientific Literature Dataset" OR "Metadata-Driven"
)
AND
(
  "Hybrid Architectures" OR "Symbolic Control" OR "Neuro-Symbolic" OR
  "Software Quality Assessment" OR "Multi-Level Evaluation" OR "AI Governance"
)
AND PUBYEAR > 2020 AND PUBYEAR < 2027
```

- **Rentang tahun:** 2021–2026.
- **Hasil seleksi Scopus:** 126 publikasi teridentifikasi → 84 dikeluarkan pada penyaringan → 42 dinilai kelayakannya → 27 dikeluarkan → **15 studi primer (S01–S15)**.
- **Penelusuran tambahan:** literatur Scopus di atas tidak memuat penelitian tentang format skripsi berbahasa Indonesia maupun analisis struktur dokumen. Karena itu dilakukan penelusuran tambahan pada jurnal nasional dan rujukan fondasional analisis dokumen, yang menghasilkan **8 studi tambahan** (D1–D3 dan E1–E5). Studi tambahan ini sebagian terbit sebelum 2021 karena bersifat fondasional.
- **Total studi yang disintesis:** 23.

---

## 3. Evidence Matrix — 15 Studi Primer Scopus (S01–S15)

Kolom “Kode proposal” menunjukkan baris studi tersebut pada Tabel 2.1 draf proposal. Kolom “Data/korpus” diisi “—” untuk studi berupa tinjauan atau kajian konseptual.

| ID | Penulis (tahun) | Metode / fokus | Data / korpus | Temuan utama | Keterbatasan / celah | Dipakai di Asdoku untuk | Kode proposal |
| :---: | :--- | :--- | :--- | :--- | :--- | :--- | :---: |
| S01 | La Malfa et al. (2025) | Kajian kritis sistem multi-agen berbasis LLM | — | Banyak sistem “multi-agen” tidak memenuhi ciri multi-agen sejati karena desain statis dan disederhanakan | Tidak memberi rancangan untuk domain dokumen | Tiga kriteria operasional MAS (subbab 2.2.7); alasan uji ablasi arsitektur | A1 |
| S02 | Gabauer (2026) | Tinjauan sistematis sistem agen | — | Merekomendasikan arsitektur hibrida (model + kontrol simbolik) dan kerangka evaluasi terpadu | Berfokus pada agen berbasis LLM | Dasar arsitektur hibrida Agen 1 (statistik) + Agen 2 (aturan) | A2 |
| S03 | Petridis et al. (2025) | Menilai konsep agen modern dengan prinsip MAS klasik | — | Otonomi, pembagian peran, dan koordinasi tetap menjadi tolok ukur | Tidak ada evaluasi empiris pada domain dokumen | Pembagian peran deteksi – pengendali mutu – pelaksana | A3 |
| S04 | Kumara et al. (2026) | Metodologi perancangan MAS klasik hingga modern | — | Panduan merancang komunikasi dan aliran data antar-agen | Bersifat panduan umum | Kontrak data *blueprint* dan pesan antar-agen (Tabel 3.8–3.10) | A6 |
| S05 | Ali et al. (2024) | Studi komparatif algoritma ML untuk NLP | Beberapa tugas NLP | Algoritma klasik efektif sebagai *baseline* dan pada sumber daya terbatas | Bukan pada klasifikasi struktur dokumen | Perbandingan Random Forest, Logistic Regression, XGBoost (EX-1) | B2 |
| S06 | Roldan-Baluis et al. (2022) | Tinjauan sistematis NLP untuk teks tidak terstruktur | — | NLP efektif mengekstraksi struktur dari teks tidak terstruktur | Hanya fitur teks | Fitur TF-IDF, diperkaya metadata OOXML | B1 |
| S07 | Saier et al. (2023) | Pembangunan korpus unarXive | Publikasi arXiv (bahasa Inggris) | Korpus teks ilmiah terstruktur skala besar | Bahasa Inggris; sumber LaTeX, bukan .docx | Pembanding: korpus TA berbahasa Indonesia berlabel manual | B3 |
| S08 | Li et al. (2022) | Pembangunan korpus CSL | Literatur ilmiah berbahasa Mandarin | Korpus ilmiah non-Inggris untuk tugas NLP | Bukan bahasa Indonesia; bukan label struktur paragraf | Sama seperti S07 | B4 |
| S09 | Blagec et al. (2022) | Analisis metrik evaluasi NLP | — | Metrik harus dipilih sesuai karakteristik tugas dan data | — | Macro-F1 sebagai metrik utama karena kelas tidak seimbang | C1 |
| S10 | Muwa et al. (2026) | Tinjauan sistematis perencanaan neuro-simbolik | — | Paduan model berbasis data dan penalaran simbolik lebih andal dan dapat dijelaskan | Bukan pada domain dokumen | Random Forest dipadukan aturan pedoman UEU | A4 |
| S11 | Zhang et al. (2024) | Eksperimen mekanisme kolaborasi agen | Tugas penalaran untuk agen LLM | Spesialisasi peran dan refleksi antar-agen meningkatkan mutu hasil | Agen berbasis LLM | Pola pelaksana–peninjau yang diterapkan secara deterministik | A5 |
| S12 | Latha & Satyanarayan Reddy (2026) | Arsitektur *meta-learning* berbasis metadata | — | Metadata membantu adaptasi model pada tugas baru | “Metadata” di sini berarti metadata dataset/tugas, bukan atribut tata letak dokumen | **Tidak dipakai sebagai landasan.** Kaitannya dengan fitur OOXML dinilai dipaksakan (audit Fase 6); landasan fitur tampilan diganti D1–D3 | — |
| S13 | Chou (2026) | Eksperimen penilai berbasis AI untuk mutu perangkat lunak | Evaluasi kode multi-agen | Penilai berbasis LLM tidak konsisten dan peka terhadap kompleksitas | Domain evaluasi kode | Alasan pengendali mutu berbasis aturan yang deterministik | C2 |
| S14 | Liu, Huang, & Guo (2026) | Kerangka evaluasi MAS bertingkat (Mosaic) | — | Evaluasi MAS perlu bertingkat dan berorientasi proses | Kerangka umum | Dua gerbang pemeriksaan (Tier 1 dan Tier 2); evaluasi per agen dan per artefak | C3 |
| S15 | Agarwal & Nene (2025) | Kerangka tata kelola AI lima lapis | — | Regulasi, standar, dan sertifikasi perlu dipadukan | Tingkat kebijakan publik, bukan validasi dokumen | **Tidak dipakai sebagai landasan.** Padanan “5 lapis” dengan aturan Agen 2 dinilai dipaksakan (audit Fase 6) | — |

S12 dan S15 tetap dicatat karena lolos seleksi Scopus, tetapi tidak dikutip di proposal. Lihat catatan nomor 1 pada bagian 6.

---

## 4. Evidence Matrix — 8 Studi Tambahan (D1–D3, E1–E5)

| ID | Penulis (tahun) | Metode / fokus | Data / korpus | Temuan utama | Keterbatasan / celah | Beda dengan Asdoku |
| :---: | :--- | :--- | :--- | :--- | :--- | :--- |
| D1 | Tkaczyk et al. (2015) | CERMINE: klasifikasi zona artikel ilmiah | Artikel PDF | Fitur geometris dan tekstual bersama-sama mengenali metadata, isi, dan referensi | Ciri tampilan diestimasi dari PDF | Ciri tampilan dibaca langsung dari OOXML |
| D2 | Zhong et al. (2019) | PubLayNet: korpus tata letak | Halaman artikel dengan label otomatis dari XML | Label otomatis memungkinkan korpus besar | Label tidak diverifikasi manusia | Pra-label diverifikasi manual sebelum evaluasi |
| D3 | Li et al. (2020) | DocBank: anotasi tingkat token dengan supervisi lemah | Dokumen dari sumber LaTeX | Informasi teks dan tampilan perlu dipadukan | Tingkat token; bukan .docx | Paduan teks dan tipografi pada tingkat paragraf |
| E1 | Putro (2019) | ML untuk kesesuaian format laporan skripsi | Laporan skripsi | ML dapat mendeteksi kesesuaian format terhadap panduan | Hanya mendeteksi | Klasifikasi struktur per paragraf dan perbaikan otomatis |
| E2 | Castrena et al. (2021) | Pencocokan tag XML terhadap aturan template | Dokumen jurnal skripsi | Kesalahan huruf, ukuran, dan margin dilaporkan dalam PDF | Perbaikan manual; belum menangani struktur bab | Perbaikan otomatis; struktur bab, sub-bab, *caption* |
| E3 | Kolinu et al. (2025) | Prototipe Flask, python-docx, regex (CekNulis) | Naskah skripsi .docx | Mendeteksi kesalahan struktur, format, dan ejaan | Pencocokan string eksak | Struktur dikenali model ML |
| E4 | Aulia & Haviana (2026) | Sistem berbasis aturan; TF-IDF dan *cosine similarity* judul bab | Naskah tugas akhir | Akurasi 92,86%; memberi rekomendasi perbaikan | Tidak memperbaiki berkas | TF-IDF sebagai fitur klasifikasi per paragraf; perbaikan langsung |
| E5 | Putra et al. (2026) | 44 aturan dalam 9 kategori; *resolver* pewarisan format OOXML | 17 skripsi; uji injeksi kesalahan | F1 0,985 pada injeksi kesalahan; pelanggaran tersisa pada 15,9% pasangan dokumen–aturan | Memeriksa, tidak memperbaiki | Memperbaiki; deteksi ML untuk naskah tanpa *style* |

---

## 5. Rujukan Pendukung

Tiga publikasi lain dari hasil penelusuran Scopus dikutip di proposal hanya sebagai rujukan pendukung, bukan bagian dari sintesis:

1. Kamalov & Sulieman (2026) — pergeseran dari sistem berbasis aturan ke sistem berorientasi tujuan, dengan aturan tetap sebagai pengaman.
2. Liu, Lu, & Mou (2023) — supervisi lemah dengan pendekatan neuro-simbolik; dasar memperlakukan koreksi Agen 2 sebagai label lemah yang harus ditinjau.
3. Wang et al. (2026) — tinjauan paradigma sistem multi-agen dari klasik hingga berbasis model besar.

Rujukan pendukung lain yang tercantum pada versi 20 Oktober 2026 dokumen ini (nomor referensi 37, 38, 82, 84, 117, 118, 123, 124 pada laporan Scopus AI) **dikeluarkan**, karena tidak dipakai di proposal dan belum diverifikasi di Mendeley.

Rujukan fondasional (Breiman, 2001; Salton & Buckley, 1988; Cohen, 1960; McNemar, 1947; Hevner et al., 2004; dan lainnya) tidak termasuk evidence matrix; daftar lengkapnya ada di Daftar Referensi proposal.

---

## 6. Simpulan dan Catatan

**Simpulan bukti.** Literatur menunjukkan empat hal: (1) pergeseran dari model monolitik ke arsitektur hibrida dengan pembagian peran (S01–S04, S10, S11); (2) algoritma klasik dan fitur tampilan tetap relevan (S05, S06, D1, D3); (3) evaluasi perlu deterministik dan bertingkat (S09, S13, S14); dan (4) korpus berlabel berbahasa Indonesia belum tersedia, sedangkan label otomatis membawa derau (S07, S08, D2, D3). Penelitian format skripsi di Indonesia (E1–E5) berhenti pada pelaporan kesalahan; perbaikannya masih manual.

**Catatan yang perlu ditindaklanjuti.**

1. **Jumlah studi di Tabel 2.1 proposal.** Sudah diselesaikan: subbab 2.1.1 proposal kini menyebut 23 studi dikaji dan 21 studi dimuat di Tabel 2.1, beserta alasan dua studi primer tidak dipakai.
2. **Verifikasi Mendeley.** Seluruh rujukan di Daftar Referensi proposal perlu dipastikan sudah ada di Mendeley sebelum naskah dikumpulkan.
3. **Angka capaian.** Versi sebelumnya dokumen ini menyebut akurasi dan skor kepatuhan prototipe. Angka tersebut ditarik; lihat [README](../README.md).
