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
[Output: Komisi Terkait + Bidang Koordinator]
```

---

## 🧪 Cara Menjalankan Proyek

### 1. Clone repository

```bash
git clone https://github.com/andradhf/Legisight.git
cd Legislight
```

### 2. Open in Jupyter/Colab

* Buka melalui visual studio code untuk menggunakan jupyter notebook
* Upload notebook ke google colab untuk menggunakan colab

### 3. Run

* Run all cell

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
komisi, bidang koordinator
Komisi III, Polkam
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


---

## 📬 Kontak

Jika ingin berdiskusi lebih lanjut tentang proyek ini atau berkolaborasi, silakan hubungi melalui:
dhafa71110@gmail.com

