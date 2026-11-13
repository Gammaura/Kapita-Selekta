# FASE 7: SPESIFIKASI SISTEM & DIAGRAM ALIR
## Asdoku — Multi-Agent System Berbasis NLP untuk Otomatisasi Deteksi Struktur dan Formatting Dokumen Tugas Akhir

Dokumen ini memuat diagram alir sistem dalam bentuk kode Mermaid dan penjelasan tiap bloknya. Isinya mengikuti rancangan pada Bab III draf proposal (subbab 3.6). Diagram resmi yang dipakai di naskah proposal ada di [Draft_TA/diagram/](../../Draft_TA/diagram/) (22 diagram draw.io); diagram di folder ini adalah ringkasannya.

| Berkas | Isi |
| :--- | :--- |
| `flowchart_vertikal_detail.mmd` | Kode Mermaid alur lengkap (bagian 1 dokumen ini) |
| `flowchart_horizontal_slide.mmd` | Kode Mermaid alur ringkas untuk slide 16:9 (bagian 4) |
| `flowchart_vertikal_detail.drawio` | Salinan Gambar 3.6 draf proposal (Flowchart Cara Kerja Sistem) |
| `flowchart_horizontal_slide.drawio` | Salinan Gambar 3.4 draf proposal (Arsitektur Multi-Agent System) |

Kedua berkas `.drawio` versi lama (420 fitur, pelatihan ulang otomatis) diganti dengan salinan diagram draf proposal agar tidak ada dua versi yang berbeda. Bila diagram di Draft_TA diubah, salin ulang ke folder ini.

---

## 1. Diagram Alir Lengkap (Mermaid)

Diagram memuat empat bagian: masukan dan prapemrosesan, proses utama, keluaran dan evaluasi, serta tampilan pengguna. Warna mengikuti diagram proposal: Agen 1 biru, Agen 2 jingga, Agen 3 hijau, masukan/keluaran ungu, keputusan kuning.

```mermaid
flowchart TD
    classDef inputStyle fill:#EDE7F6,stroke:#5E35B1,stroke-width:2px,color:#311B92
    classDef agent1Style fill:#E3F2FD,stroke:#1565C0,stroke-width:2px,color:#0D47A1
    classDef agent2Style fill:#FFF3E0,stroke:#EF6C00,stroke-width:2px,color:#E65100
    classDef agent3Style fill:#E8F5E9,stroke:#2E7D32,stroke-width:2px,color:#1B5E20
    classDef decisionStyle fill:#FFFDE7,stroke:#F9A825,stroke-width:2px,color:#5D4037
    classDef evalStyle fill:#F5F5F5,stroke:#616161,stroke-width:2px,color:#212121

    subgraph S1 ["1. INPUT DATA & PREPROCESSING"]
        direction TB
        IN1(["Pengguna mengunggah naskah .docx<br/>di halaman Alat"])
        IN2{"Berekstensi .docx?"}
        IN3["Tolak dengan pesan galat"]
        PRE1["Simpan salinan sementara;<br/>baca seluruh paragraf secara hanya-baca"]
        PRE2["Ekstraksi fitur mentah per paragraf:<br/>teks, style, huruf, perataan, penomoran,<br/>spasi, indentasi, posisi"]
        PRE3["Transformasi menjadi 437 fitur:<br/>400 TF-IDF + 37 metadata<br/>(20 tipografi/tata letak, 7 gaya Word, 10 pola teks)"]
        IN1 --> IN2
        IN2 -- "Tidak" --> IN3
        IN2 -- "Ya" --> PRE1 --> PRE2 --> PRE3
    end

    subgraph S2 ["2. PROSES UTAMA (TIGA AGEN)"]
        direction TB

        subgraph A1 ["Agen 1 - Inspector (machine learning, tanpa aturan)"]
            A1_1["Random Forest: probabilitas 9 kelas;<br/>label = kelas tertinggi, nilainya = skor keyakinan"]
            A1_2["Tandai ambigu bila keyakinan di bawah 0,70"]
            A1_3["Terbitkan Draft Blueprint"]
            A1_1 --> A1_2 --> A1_3
        end

        subgraph A2T1 ["Agen 2 - Quality Critic, Tier 1 (audit blueprint)"]
            T1_1["Aturan pasti per paragraf;<br/>pembaruan zona dokumen;<br/>validasi urutan bab; rantai aturan; pemeriksaan akhir"]
            T1_2{"Ada koreksi baru<br/>dan iterasi belum 3?"}
            T1_3["Kirim arahan koreksi beserta alasan;<br/>Agen 1 menerapkan ke blueprint"]
            T1_4["Approved Blueprint + log koreksi<br/>+ daftar paragraf yang perlu dicek"]
            T1_1 --> T1_2
            T1_2 -- "Ya" --> T1_3
            T1_2 -- "Tidak (konvergen)" --> T1_4
        end

        subgraph A3 ["Agen 3 - Formatting Actuator"]
            A3_1["Penyusunan di atas salinan template resmi UEU:<br/>renderer per label; paragraf disalin utuh,<br/>hanya properti format yang diubah"]
            A3_2["Heading bernomor, section Romawi/Arab, header,<br/>caption bernomor, tabel APA 7,<br/>Daftar Isi/Tabel/Gambar sebagai field"]
            A3_3["Perbaikan terarah per kriteria;<br/>sidik isi dibandingkan sebelum-sesudah,<br/>perbaikan dibatalkan bila isi berubah"]
            A3_1 --> A3_2
        end

        subgraph A2T2 ["Agen 2 - Quality Critic, Tier 2 (uji penerimaan berkas)"]
            T2_1["Uji 8 kriteria K1-K8;<br/>nilai target dari konfigurasi aturan format"]
            T2_2{"Semua lolos?"}
            T2_3{"Daftar cacat berubah<br/>dan iterasi belum 3?"}
            T2_4["Daftar cacat terstruktur:<br/>kriteria, lokasi, nilai aktual, nilai target"]
            T2_1 --> T2_2
            T2_2 -- "Tidak" --> T2_3
            T2_3 -- "Ya" --> T2_4
        end

        PRE3 --> A1_1
        A1_3 --> T1_1
        T1_3 -->|"putaran Tier 1"| T1_1
        T1_4 --> A3_1
        A3_2 --> T2_1
        T2_4 --> A3_3
        A3_3 -->|"putaran Tier 2"| T2_1
    end

    subgraph S3 ["3. KELUARAN SISTEM & EVALUASI"]
        direction TB
        OUT1["Skor kepatuhan = kriteria lolos / 8;<br/>status PASS atau FAIL; sisa cacat"]
        POOL["Koreksi Agen 2 dicatat ke pool koreksi<br/>(status: belum ditinjau)"]
        RL["Di luar alur pengguna:<br/>peneliti meninjau pool, melatih kandidat,<br/>uji non-regresi (toleransi 0,005)"]
        EV["Evaluasi TA-2 pada naskah uji baru, sistem dibekukan:<br/>EX-1 s.d. EX-8 (macro-F1, ablasi, McNemar,<br/>kepatuhan, keutuhan isi, waktu, injeksi cacat)"]
        T2_2 -- "Ya" --> OUT1
        T2_3 -- "Tidak" --> OUT1
        T1_3 -.-> POOL
        POOL -.-> RL
        RL -.->|"versi model baru"| A1_1
        OUT1 -.-> EV
    end

    subgraph S4 ["4. TAMPILAN & ANTARMUKA PENGGUNA"]
        direction TB
        UI1["Halaman Alat: status tiga agen dan log proses"]
        UI2["Skor, hasil 8 kriteria, sisa cacat,<br/>log koreksi beserta alasan,<br/>paragraf yang perlu dicek penulis"]
        UI3(["Unduh: (Asdoku) - nama berkas.docx;<br/>salinan unggahan dihapus"])
        OUT1 --> UI1 --> UI2 --> UI3
    end

    class IN1,IN3,PRE1,PRE2,PRE3,UI1,UI2,UI3,POOL inputStyle
    class A1_1,A1_2,A1_3 agent1Style
    class T1_1,T1_3,T1_4,T2_1,T2_4,OUT1 agent2Style
    class A3_1,A3_2,A3_3 agent3Style
    class IN2,T1_2,T2_2,T2_3 decisionStyle
    class RL,EV evalStyle
```

---

## 2. Cara Memakai di Draw.io

1. Buka [app.diagrams.net](https://app.diagrams.net/) atau Draw.io Desktop.
2. Pilih **Arrange → Insert → Advanced → Mermaid**.
3. Tempel isi berkas `.mmd` (tanpa pagar ```` ```mermaid ````), lalu **Insert**.
4. Ekspor lewat **File → Export as → PNG** (300 dpi) atau **SVG**.

Kode Mermaid di dokumen ini belum dicoba dirender; periksa hasilnya di [mermaid.live](https://mermaid.live) sebelum dipakai di slide.

---

## 3. Penjelasan Tiap Blok

### Blok 1 — Masukan dan prapemrosesan

Pengguna mengunggah naskah di halaman Alat; berkas selain .docx ditolak (FR-01). Agen 1 membaca seluruh paragraf secara hanya-baca dan mengekstraksi fitur mentah, lalu mengubahnya menjadi **437 fitur**: 400 TF-IDF (unigram dan bigram) dan 37 metadata, yaitu 20 tipografi dan tata letak OOXML, 7 gaya Word, dan 10 pola teks (FR-02; Tabel 3.11).

### Blok 2 — Proses utama

- **Agen 1 — Inspector.** Random Forest menghasilkan probabilitas sembilan kelas. Paragraf dengan keyakinan di bawah 0,70 ditandai ambigu. Keluarannya *Draft Blueprint* (FR-03, FR-04). Agen ini murni *machine learning*, tanpa aturan buatan, agar kinerjanya dapat diukur terpisah.
- **Agen 2 — Tier 1.** Audit satu kali dari paragraf pertama sampai terakhir dengan mesin status zona dokumen: aturan pasti per paragraf, validasi urutan bab, rantai aturan berprioritas, dan pemeriksaan akhir (Tabel 3.13). Koreksi dikirim ke Agen 1, diterapkan ke *blueprint*, lalu diaudit ulang sampai tidak ada koreksi baru atau tiga iterasi. Keluarannya *Approved Blueprint*, log koreksi beserta alasan, dan daftar paragraf yang perlu dicek penulis (FR-05, FR-06).
- **Agen 3 — penyusunan.** Isi naskah disalin ke salinan template resmi UEU sesuai label, dengan *renderer* per label (Tabel 3.15). Paragraf disalin utuh; hanya properti format yang diubah (FR-07 s.d. FR-11).
- **Agen 2 — Tier 2.** Berkas diuji terhadap 8 kriteria (Tabel 3.14) dengan nilai target dari konfigurasi aturan format. Setiap pelanggaran menjadi satu objek cacat berisi kriteria, lokasi, nilai aktual, dan nilai target (FR-12).
- **Agen 3 — perbaikan terarah.** Untuk setiap cacat dijalankan tindakan perbaikan yang sesuai (Tabel 3.16). Sidik isi dihitung sebelum dan sesudah; bila berbeda, perbaikan dibatalkan. Putaran berhenti bila semua lolos, bila daftar cacat tidak berubah, atau setelah tiga iterasi (FR-13).

### Blok 3 — Keluaran dan evaluasi

- **Keluaran per naskah:** skor kepatuhan (jumlah kriteria lolos dibagi delapan), status PASS atau FAIL, dan sisa cacat.
- **Pool koreksi:** setiap koreksi Agen 2 dicatat berstatus “belum ditinjau” (FR-16). Peneliti meninjau pool, melatih kandidat model, dan menjalankan uji non-regresi dengan toleransi 0,005, semuanya di luar alur pengguna (FR-17). Pengguna tidak diminta memberi label.
- **Evaluasi penelitian:** delapan eksperimen (EX-1 s.d. EX-8) pada naskah uji baru setelah sistem dibekukan. Diagram ini sengaja tidak memuat angka kinerja, karena evaluasi baru dilakukan pada TA-2.

### Blok 4 — Tampilan pengguna

Halaman Alat menampilkan status ketiga agen dan log proses, lalu skor, hasil 8 kriteria, sisa cacat, log koreksi beserta alasan, dan daftar paragraf yang perlu dicek (FR-14). Berkas diunduh dengan nama “(Asdoku) - nama berkas.docx”, dan salinan unggahan dihapus (FR-15).

---

## 4. Diagram Ringkas untuk Slide (16:9)

```mermaid
flowchart LR
    classDef inputStyle fill:#EDE7F6,stroke:#5E35B1,stroke-width:2px,color:#311B92
    classDef agent1Style fill:#E3F2FD,stroke:#1565C0,stroke-width:2px,color:#0D47A1
    classDef agent2Style fill:#FFF3E0,stroke:#EF6C00,stroke-width:2px,color:#E65100
    classDef agent3Style fill:#E8F5E9,stroke:#2E7D32,stroke-width:2px,color:#1B5E20
    classDef evalStyle fill:#F5F5F5,stroke:#616161,stroke-width:2px,color:#212121

    subgraph IN ["1. Input"]
        A["Naskah .docx<br/>format bebas"] --> B["437 fitur<br/>400 TF-IDF + 37 metadata"]
    end

    subgraph MAS ["2. Tiga agen, dua putaran umpan balik"]
        B --> C["Agen 1 - Inspector<br/>Random Forest"]
        C -->|"Draft Blueprint"| D["Agen 2 - Quality Critic<br/>aturan pedoman + konteks dokumen"]
        D -->|"Tier 1: arahan koreksi"| C
        D -->|"Approved Blueprint"| E["Agen 3 - Formatting Actuator<br/>penyusunan + perbaikan terarah"]
        E -->|"berkas hasil"| D
        D -->|"Tier 2: daftar cacat"| E
    end

    subgraph OUT ["3. Keluaran"]
        D --> G["Skor 8 kriteria, sisa cacat,<br/>log koreksi, paragraf perlu dicek"]
        G --> H["Unduh<br/>(Asdoku) - nama berkas.docx"]
    end

    subgraph EVAL ["4. Di luar alur pengguna"]
        D -.-> F["Pool koreksi<br/>ditinjau peneliti"]
        F -.->|"latih ulang + uji non-regresi"| C
    end

    class A,B,G,H inputStyle
    class C agent1Style
    class D agent2Style
    class E agent3Style
    class F evalStyle
```

---

## 5. Padanan dengan Diagram di Proposal

| Yang digambarkan | Gambar di draf proposal |
| :--- | :--- |
| Arsitektur tiga agen | Gambar 3.4 |
| Alur kerja keseluruhan | Gambar 3.6 |
| Agen 1 | Gambar 3.7 |
| Agen 2: zona dokumen, Tier 1, Tier 2 | Gambar 3.8, 3.9, 3.10 |
| Agen 3: penyusunan, perbaikan terarah | Gambar 3.11, 3.12 |
| Urutan pesan antar-agen | Gambar 3.13 |
| Pembelajaran ulang terkendali | Gambar 3.14 |
| Use case, activity, class, ERD | Gambar 3.15 – 3.18 |
| Rancangan antarmuka halaman Alat | Gambar 3.19, 3.20 |
