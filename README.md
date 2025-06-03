# 🏛️ Legal Decision Insight Extractor

**Legal Decision Insight Extractor** adalah sebuah proyek pemrosesan dokumen berbasis LLM (Large Language Model) untuk mengolah dokumen putusan hukum dan mengelompokkan substansi masalah ke dalam 13 komisi DPR RI yang relevan.

> ⚖️ Tujuan utama proyek ini adalah membantu lembaga legislatif dalam mengarsipkan, mengklasifikasikan, dan mengekstrak insight dari putusan hukum berdasarkan konteks permasalahan yang termuat di dalamnya.

---

## 📌 Fitur Utama

* ✅ Ekstraksi bagian penting dari dokumen putusan: *Petitum* dan *Amar*
* ✅ Klasifikasi otomatis berdasarkan status putusan hukum
* ✅ Penyesuaian prompt LLM berdasarkan konteks hukum
* ✅ Kompatibel dengan LLM lokal (mis. `GoToCompany/llama3-8b-cpt-sahabatai-v1-instruct`)
* ✅ Output dalam format `.csv` siap pakai untuk pelaporan

---

## 🧠 Arsitektur Proyek

```
[PDF Putusan]
     ↓
[Ekstraksi Text (pdfplumber)]
     ↓
[Preprocessing & Regex Parsing]
     ↓
[Penentuan Status Putusan]
     ↓
[Prompt Generation]
     ↓
[LLM Classification (local HF model)]
     ↓
[Output: Komisi Terkait + Alasan]
```

---

## 🗂️ Struktur Folder

```
.
├── data/                        # Folder berisi file PDF
├── utils/
│   ├── parser.py               # Regex & logic ekstraksi Amar / Petitum
│   └── prompt_generator.py     # Prompt untuk tiap jenis status
├── models/
│   └── classifier.py           # LLM-based classification logic
├── outputs/
│   └── hasil_klasifikasi.csv   # Output hasil klasifikasi
├── classify.py                 # Pipeline utama
├── README.md                   # Dokumentasi proyek
└── requirements.txt            # Library dependensi
```

---

## 🧪 Cara Menjalankan Proyek

### 1. Clone repository

```bash
git clone https://github.com/username/legal-decision-extractor.git
cd legal-decision-extractor
```

### 2. Install dependensi

```bash
pip install -r requirements.txt
```

### 3. Siapkan file PDF putusan

Letakkan semua file PDF pada folder `./data`.

### 4. Jalankan pipeline klasifikasi

```bash
python classify.py
```

### 5. Hasil klasifikasi

File `hasil_klasifikasi.csv` akan muncul di folder `outputs/`.

---

## ⚙️ Konfigurasi Model

Model default menggunakan LLM lokal berbasis HuggingFace:

* **Model**: `GoToCompany/llama3-8b-cpt-sahabatai-v1-instruct`
* **Tokenizer**: `AutoTokenizer.from_pretrained(...)`
* **Device**: GPU (`cuda`) atau CPU

> ⚠️ Pastikan kamu memiliki hardware yang sesuai untuk menjalankan model 8B (RAM & VRAM yang cukup).

---

## 🏛️ Daftar Komisi DPR RI

Model akan mengklasifikasikan dokumen ke dalam salah satu dari 13 komisi berikut:

* Komisi I – Pertahanan, Luar Negeri, Kominfo
* Komisi II – Pemerintahan, Reformasi Birokrasi
* Komisi III – Hukum, HAM, Keamanan
* Komisi IV – Pertanian, Lingkungan Hidup
* Komisi V – Infrastruktur, Perhubungan
* Komisi VI – Perdagangan, Perindustrian, BUMN
* Komisi VII – Energi, Riset, Teknologi
* Komisi VIII – Agama, Sosial, Pemberdayaan Perempuan
* Komisi IX – Kesehatan, Ketenagakerjaan
* Komisi X – Pendidikan, Pariwisata
* Komisi XI – Keuangan, Perbankan

---

## 🧩 Logika Status Putusan

Pengelompokan status digunakan untuk memilih bagian dokumen yang relevan untuk dianalisis:

| Kelompok Status         | Berdasarkan Bagian |
| ----------------------- | ------------------ |
| Dikabulkan, Sela        | Amar               |
| Ditolak, Tidak Diterima | Petitum            |
| Gugur, Tidak Berwenang  | Return langsung    |
| Campuran                | Amar & Petitum     |

---

## 📤 Contoh Output

```csv
filename, komisi, status_putusan, alasan_model
001_putusan.pdf, Komisi III, dikabulkan seluruhnya, Berdasarkan pelanggaran hukum acara pidana
```

---

## 🤖 Model & Prompt Engineering

Prompt disusun untuk:

* Menjelaskan konteks tugas model
* Menyediakan daftar komisi
* Menekankan analisis konteks (bukan keyword matching)

Contoh potongan prompt:

```
Anda adalah seorang ahli hukum yang berpengalaman...
Tugas Anda adalah mengklasifikasikan sebuah teks putusan pengadilan ke dalam salah satu dari 13 komisi DPR RI...
```

---

## 👨‍💼 Kontributor

* **Andra** – AI Engineer, Prompt Strategist
* **Indera** - AI Engineer

---

## 🪪 Lisensi

MIT License. Silakan digunakan dan dikembangkan untuk tujuan riset, edukasi, maupun peningkatan tata kelola lembaga hukum/legislatif.

---

## 📬 Kontak

Jika ingin berdiskusi lebih lanjut tentang proyek ini atau berkolaborasi, silakan hubungi melalui:

