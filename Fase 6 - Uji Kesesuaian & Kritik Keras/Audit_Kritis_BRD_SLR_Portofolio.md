# UJI KESESUAIAN BRD × SLR, KELAYAKAN, DAN NILAI PORTOFOLIO
## Asdoku — Audit Kritis dan Tindak Lanjutnya

Dokumen ini berisi tiga matriks (kesesuaian, kelayakan, nilai portofolio) dan kritik dari dua sudut pandang: dosen pembimbing/penguji yang skeptis dan *tech lead* yang pragmatis. Kritik pertama kali ditulis 21 Oktober 2026 terhadap dokumen Fase 1–5 versi awal. Versi ini menambahkan **tindak lanjut**: apa yang sudah diubah di draf proposal, dan apa yang masih terbuka.

Seluruh skor adalah penilaian peneliti sendiri dengan bantuan AI, belum dinilai dosen.

---

## 1. Matriks Kesesuaian BRD × SLR

Skor 1–5; skor di bawah 3 berarti dukungan literatur lemah dan klaim harus diubah.

| Sasaran (BRD) | Bukti pendukung (SLR) | Skor | Catatan kritis |
| :--- | :--- | :---: | :--- |
| BO-01 Deteksi struktur; multi-agen lebih baik daripada model saja | S01, S02, S03, S10, S11 (arsitektur hibrida, pembagian peran) | 4 | Studi tersebut membahas agen berbasis LLM, sedangkan Asdoku tidak memakai LLM. Dukungan sah sebatas **prinsip** (peran terpisah, kontrol simbolik); keunggulan multi-agen pada Asdoku harus dibuktikan sendiri lewat ablasi. |
| BO-02 Fitur gabungan lebih baik daripada teks saja | S05, S06, D1, D3 | 4 | D1 dan D3 bekerja pada PDF. Kesimpulan “teks + tampilan” dapat dipinjam, besarnya manfaat pada .docx belum diketahui. |
| BO-03 Berkas patuh 8 kriteria | E2–E5 (aturan format); pedoman UEU 2018 | 4 | Delapan kriteria adalah pilihan peneliti, jauh lebih sedikit daripada 44 aturan pada E5. Harus dinyatakan sebagai keterbatasan. |
| BO-04 Isi tidak berubah | Tidak ada studi yang mengukur keutuhan isi | 3 | Murni kebutuhan rekayasa; landasannya standar OOXML (ECMA-376), bukan SLR. |
| BO-05 Memperbaiki cacat, bukan hanya mendeteksi | E5 (evaluasi injeksi kesalahan) | 4 | Metode injeksi dipinjam dari E5; perbaikannya sendiri belum ada di literatur (inilah celahnya). |
| BO-06 Waktu proses | S05 (algoritma klasik ringan) | 3 | Batas 10 detik belum punya dasar selain perkiraan; menunggu konfirmasi pembimbing. |
| BO-07 Korpus berlabel | S07, S08, D2, D3; Ratner et al. (2017) | 5 | Dukungan kuat, baik untuk kelangkaan korpus maupun risiko label otomatis. |

Tidak ada skor di bawah 3. Dua klaim versi awal yang skornya di bawah 3 sudah dibuang (lihat bagian 4, temuan 1 dan 3).

---

## 2. Matriks Kelayakan

| Aspek | Pertanyaan kritis | Skor (1–5) | Risiko utama |
| :--- | :--- | :---: | :--- |
| Teknis | Apakah dapat dibangun dengan kemampuan dan alat yang ada? | 4 | Prototipe membuktikan format dapat diubah lewat OOXML tanpa menyentuh teks. Dua komponen belum ada: daftar cacat terstruktur dan perbaikan terarah. |
| Data | Apakah data dapat diperoleh dan cukup? | 3 | Enam naskah tugas akhir pengembangan sudah ada. Naskah uji baru minimal empat (target lima); empat calon baru tersedia dalam PDF. Label belum diverifikasi manusia; anotator kedua belum ditetapkan. |
| Waktu | Apakah selesai sesuai jadwal? | 3 | TA-2 hanya Desember 2026 – Maret 2027 untuk verifikasi 7.000-an paragraf, sembilan paket kerja, dan delapan eksperimen. Verifikasi label adalah pekerjaan paling lama. |
| Orisinalitas | Apakah berbeda dari penelitian yang ada? | 4 | Berbeda dari E1–E5 karena memperbaiki berkas dan memakai ML untuk naskah tanpa *style*. Bagian pemeriksaannya sendiri tidak baru. |
| Etika & legalitas | Apakah data dipakai secara sah? | 4 | Izin tertulis, anonimisasi, korpus tidak dipublikasikan. Formulir izin sudah ada; pastikan seluruh tujuh naskah yang sudah terkumpul memang memiliki izin tertulis. |
| **Total** | | **18 / 25** | |

---

## 3. Matriks Nilai Portofolio

| Kriteria | Indikator “layak portofolio” | Skor (1–5) | Catatan |
| :--- | :--- | :---: | :--- |
| Kompleksitas teknis | Lebih dari sekadar melatih model | 4 | Dari ekstraksi fitur sampai manipulasi OOXML dan aplikasi web. |
| Dampak terukur | Ada angka hasil yang dapat dipertanggungjawabkan | 2 | Belum ada. Angka prototipe ditarik; hasil sahih baru ada setelah TA-2. |
| Demo & deploy | Dapat dicoba orang lain | 3 | Aplikasi berjalan lokal dan ada konfigurasi untuk demo daring; belum ada dokumen contoh yang bisa langsung dicoba. |
| Kualitas kode | Terstruktur, teruji, terdokumentasi | 3 | Ada uji otomatis dan README; nilai format masih tertanam di kode (PK-6). |
| Cerita interview | Ada keputusan rancangan yang bisa dijelaskan | 4 | Mengapa tanpa LLM; mengapa angka awal ditarik; mengapa pelatihan ulang otomatis dihentikan. |
| **Total** | | **16 / 25** | |

Ambang yang disarankan templat adalah ≥ 15/25. Kelayakan (18) dan nilai portofolio (16) sama-sama di atas ambang, sehingga penyusunan proposal dilanjutkan. Skor “dampak terukur” akan tetap rendah sampai evaluasi TA-2 selesai.

---

## 4. Audit Kesesuaian: Klaim yang Dipaksakan dan Tindak Lanjutnya

| No | Temuan pada versi awal | Tindak lanjut di draf proposal | Status |
| :---: | :--- | :--- | :--- |
| 1 | **S12 (Latha & Satyanarayan Reddy) dipakai sebagai dasar fitur OOXML.** “Metadata” di studi itu adalah metadata dataset, bukan atribut tata letak dokumen. | S12 tidak dikutip. Landasan fitur tampilan diganti penelitian analisis dokumen: Tkaczyk et al. (2015), Zhong et al. (2019), Li et al. (2020). Fitur OOXML dinyatakan sebagai rekayasa fitur peneliti sendiri (subbab 2.2.5). | Selesai |
| 2 | **Studi agen LLM dipakai membenarkan sistem tanpa LLM.** Penguji akan bertanya: ini multi-agen, atau tiga berkas Python yang dipanggil berurutan? | Subbab 2.2.7 menetapkan tiga kriteria operasional MAS dari La Malfa et al. dan Petridis et al.: peran dan kewenangan terpisah, umpan balik yang mengubah keputusan agen lain, kontribusi diukur dengan ablasi. Subbab 3.6.1 menunjukkan pemenuhannya. Putaran Tier 2 dirancang ulang agar sungguh mengubah keluaran (perbaikan terarah). | Selesai di rancangan; pembuktian di TA-2 (EX-3, EX-8) |
| 3 | **“5 Lapisan Guardrail” dipadankan dengan kerangka tata kelola lima lapis S15.** Padanan hanya pada angka lima. Istilah “Software Quality Assurance” untuk pemeriksaan margin juga tidak tepat. | S15 tidak dikutip. Aturan Agen 2 disebut apa adanya: lima kelompok aturan (Tabel 3.13). Istilah SQA diganti “audit *blueprint*” (Tier 1) dan “uji penerimaan berkas” (Tier 2), merujuk gerbang bertingkat pada Liu, Huang, & Guo (2026). | Selesai |
| 4 | **“Active learning” untuk pelatihan ulang dari keluaran aturan.** Melatih model dari keluaran aturan tanpa verifikasi manusia adalah supervisi lemah, bukan *active learning*. | Subbab 2.2.8 memakai istilah supervisi lemah (Ratner et al., 2017; Liu, Lu, & Mou, 2023). Pelatihan ulang otomatis setiap lima koreksi dihapus; diganti pembelajaran ulang terkendali: koreksi ditinjau peneliti, lalu uji non-regresi (subbab 3.6.10). | Selesai |
| 5 | **Manipulasi OOXML dikaitkan dengan literatur keamanan agen.** | Teori OOXML dipisah dari SLR dan diletakkan di landasan teori (subbab 2.2.2) dengan rujukan ECMA-376. | Selesai |
| 6 | **Sitasi yang tidak dapat diverifikasi** sempat muncul pada draf awal Fase 2. | Daftar referensi dibatasi pada rujukan yang ada sumbernya; rujukan pendukung yang belum diverifikasi dikeluarkan dari Fase 2 dan Fase 4. | Selesai; verifikasi Mendeley menyeluruh masih perlu dilakukan |

---

## 5. Kritik Kelayakan dari Sudut Pandang Pembimbing dan Penguji

### 5.1 Realistis untuk satu semester?

**Kritik.** Bila dimulai dari nol, tidak realistis. Karena prototipe sudah ada, pertanyaannya bergeser: apakah peneliti memahami setiap bagian sistem dan dapat menjelaskannya tanpa bantuan?

**Tindak lanjut.** Penelitian dibagi dua: TA-1 hanya rancangan, TA-2 pembangunan dan evaluasi. Rancangan ditulis rinci sampai tingkat algoritma, struktur data, dan aturan, sehingga dapat dijelaskan dan diuji. Risiko yang tersisa adalah waktu (bagian 2).

### 5.2 Topik klise?

**Kritik.** Tidak klise. Masalahnya nyata dan hasilnya dapat diperagakan langsung.

**Tindak lanjut.** Fokus dipertahankan pada deteksi struktur dan perbaikan format; tidak melebar ke tata bahasa, sitasi, atau *chatbot*.

### 5.3 Data legal dan etis?

**Kritik.** Naskah mahasiswa lain memuat data pribadi; memakainya tanpa izin tertulis dapat dipersoalkan.

**Tindak lanjut.** Subbab 3.12 (etika penelitian): izin tertulis (Lampiran 4), anonimisasi, korpus tidak dipublikasikan, naskah asli dihapus setelah sidang. Laporan magang dikeluarkan dari cakupan, sehingga data perusahaan mitra tidak ikut terbawa.

### 5.4 Tiga skenario kegagalan

| No | Skenario | Akar masalah | Tindak lanjut | Status |
| :---: | :--- | :--- | :--- | :--- |
| 1 | **Tuduhan kebocoran data dan hasil yang terlalu bagus.** | Label dibuat aturan yang mirip aturan Agen 2 lalu dikoreksi AI; naskah uji ikut dipakai menyetel aturan. | Angka prototipe ditarik. Seluruh label diverifikasi manusia, ≥ 20% dianotasi ulang (κ ≥ 0,80). Data dibagi per naskah. Naskah U01 dan U02 diturunkan menjadi data validasi. Naskah uji baru dibuka setelah sistem dibekukan. | Dirancang; dikerjakan pada TA-2 |
| 2 | **Berkas hasil rusak atau tampil salah di Word.** | Manipulasi XML langsung; Word diam-diam mengabaikan elemen yang tidak sesuai skema. | Penyusunan di atas salinan template; paragraf disalin utuh; setiap hasil dibuka di Word; verifikasi manual 8 kriteria (EX-4); uji keutuhan isi (EX-5). | Dirancang; sebagian sudah diuji pada prototipe |
| 3 | **Model makin buruk karena belajar dari koreksi yang keliru.** | Pelatihan ulang otomatis dari keluaran aturan. | Pelatihan ulang otomatis dihapus. Koreksi masuk pool berstatus “belum ditinjau”; peneliti meninjau; kandidat hanya diterima bila macro-F1 tidak turun melebihi toleransi 0,005. Pada prototipe, uji non-regresi memang menolak kandidat yang dilatih dengan label lemah. | Tersedia pada prototipe |

---

## 6. Kritik dari Sudut Pandang Tech Lead

### 6.1 Pertanyaan yang akan muncul, dan jawaban saat ini

1. **“Mengapa ini disebut multi-agen? Apa bedanya dengan *pipeline* berurutan?”**
   Tiga agen memiliki masukan, cara bernalar, dan kewenangan berbeda; Agen 2 dapat mengganti keputusan Agen 1 dan menolak berkas Agen 3; ada dua putaran umpan balik. Agen berjalan dalam satu proses secara berurutan, tidak asinkron, dan itu dinyatakan terbuka di subbab 3.6.9. Bukti bahwa kolaborasi berguna baru ada setelah ablasi arsitektur (EX-3).

2. **“Bagaimana bila model diganti saat ada permintaan yang sedang diproses?”**
   Pelatihan ulang tidak lagi berjalan di server saat pengguna memproses naskah; dijalankan peneliti lewat skrip, dikunci agar tidak ada dua pelatihan bersamaan, dan Agen 1 memuat model baru pada permintaan berikutnya. Selama evaluasi akhir sistem dibekukan.

3. **“Mengapa Random Forest di atas TF-IDF? Jangan-jangan model hanya menebak dari huruf tebal dan ukuran huruf?”**
   Inilah yang diuji: XGBoost dan Logistic Regression sebagai pembanding (EX-1), dan ablasi fitur dengan empat konfigurasi pada naskah asli serta versi heading polos (EX-2). Jawabannya belum ada.

4. **“Berapa lama untuk naskah besar, dan bagaimana bila banyak pengguna sekaligus?”**
   Waktu proses diukur per naskah, lima kali, beserta jumlah paragraf dan ukuran berkas (EX-6). Pemakaian serentak oleh banyak pengguna **tidak** diuji; sistem dibatasi pada instalasi lokal (batasan masalah nomor 10).

### 6.2 Kelemahan yang masih ada

1. **Belum ada hasil yang sahih.** Semua klaim kinerja menunggu TA-2.
2. **Hanya delapan kriteria format.** Jauh lebih sedikit daripada pemeriksa berbasis aturan yang ada.
3. **Aturan Agen 2 disusun dari sedikit naskah.** Enam naskah dari satu fakultas; daya generalisasi belum diketahui.
4. **Penyimpanan berupa berkas CSV.** Cukup untuk pemakaian lokal satu pengguna; tidak untuk pemakaian serentak.
5. **Nilai format masih tertanam di kode** pada prototipe (PK-6).

### 6.3 Pembeda dari proyek ML umumnya

1. Tidak berhenti di model: menerima .docx dan mengembalikan .docx yang sudah diperbaiki.
2. Model statistik dikendalikan aturan yang deterministik, dengan alasan tertulis untuk setiap koreksi.
3. Evaluasi dirancang jujur: label diverifikasi manusia, naskah uji baru, sistem dibekukan, dan angka awal yang meragukan ditarik.

### 6.4 Skor daya jual di interview: 7 / 10

Nilai tambah: cakupan dari data sampai berkas hasil, keputusan rancangan yang dapat dijelaskan, dan sikap terhadap validitas hasil. Pengurang: belum ada angka hasil yang dapat dikutip, belum ada dokumen contoh untuk demo satu klik, dan belum diuji untuk pemakaian serentak. Skor versi awal (8,2) bertumpu pada angka prototipe yang kini ditarik.

---

## 7. Rencana Perbaikan

### 7.1 Kekuatan akademik

| Rekomendasi audit | Wujud di draf proposal | Status |
| :--- | :--- | :--- |
| Ablasi fitur: teks saja, metadata saja, gabungan | EX-2, empat konfigurasi, naskah asli dan versi heading polos (Tabel 4.4) | Dirancang; skrip belum ada (PK-9) |
| Bandingkan model saja dengan multi-agen | EX-3: Agen 1 saja, aturan saja, multi-agen lengkap, dengan uji McNemar (Tabel 4.5) | Dirancang; skrip ablasi arsitektur sudah ada, McNemar belum |
| Luruskan istilah | “agen hibrida” tanpa LLM; supervisi lemah; uji penerimaan berkas | Selesai |
| Pisahkan data per naskah; uji buta | Pembagian per naskah; naskah uji baru setelah pembekuan | Dirancang |
| Tambah model pembanding | XGBoost | Selesai di rancangan |
| Bukti masalah di lingkungan sendiri | Kuesioner studi pendahuluan, 35 responden (November 2026); hasil di Latar Belakang proposal dan BRD bagian 1.2 | Selesai |

### 7.2 Nilai portofolio (setelah TA-2)

1. Tabel hasil ablasi fitur dan arsitektur pada README.
2. Dokumen contoh yang dapat langsung dicoba di halaman Alat.
3. Perbandingan tampilan sebelum–sesudah di Word (*Navigation Pane*, Daftar Isi, nomor halaman, tabel).
4. Bagian “Mengapa tanpa LLM” pada README.
5. Kemasan Docker agar dapat dijalankan dengan satu perintah.

---

## 8. Yang Masih Terbuka

| Hal | Diperlukan untuk |
| :--- | :--- |
| Batas waktu proses (KNF-03), sementara ≤ 10 detik | Konfirmasi dosen pembimbing |
| Orang yang menjadi anotator kedua (kriterianya sudah ditetapkan) | Reliabilitas anotasi |
| Naskah uji dalam format .docx | Syarat minimal empat naskah uji |
| Nama jurnal sasaran (sementara: jurnal nasional terakreditasi SINTA) | Rencana luaran |
| Keputusan fakultas tentang spasi paragraf (0 pt atau 6 pt) | Konfigurasi aturan format |
| Pilihan judul (kandidat 1 atau 2, [Fase 5](../Fase%205%20-%20Analisis%20Gap%20&%20Penetapan%20Judul/Gap_Analysis_dan_Penetapan_Judul.md)) | Keputusan dosen pembimbing |
