# 🏛️ Legisight

**Legisight** adalah solusi otomatis berbasis *Retrieval-Augmented Generation (RAG)* yang membantu mengidentifikasi keterkaitan dokumen resmi (seperti hasil rapat atau kebijakan) dengan salah satu dari 13 Komisi di DPR RI berdasarkan ruang lingkup tugasnya.

---

## 🚀 Fitur Utama

- 📄 Mendownload & membaca isi dokumen dari link file PDF
- 🔍 Menerapkan ekstraksi berbasis RAG untuk memahami konteks isi
- 🧠 Menganalisis isi dokumen menggunakan LLM (Large Language Model)
- 🏷️ Mengklasifikasikan dokumen ke komisi yang relevan di DPR RI

---

## 🛠️ Cara Menjalankan

### 1. Instalasi Dependensi

Jalankan perintah berikut di cell notebook untuk memasang semua dependensi yang dibutuhkan:

```bash
pip install langchain langchain-community faiss-cpu sentence-transformers pypdf
curl -fsSL https://ollama.com/install.sh | sh
ollama serve > /dev/null 2>&1 &
ollama pull deepseek-r1:7b
```

## 📄 2. Unggah File CSV

Unggah file `.csv` yang berisi daftar link dokumen PDF yang akan diproses.

> 💡 **Catatan Penting:** Pastikan file CSV memiliki **kolom bernama `supporting_file`** yang berisi URL dari file PDF.

### 📊 Contoh isi CSV:

| id | title   | supporting_file                    |
|----|---------|------------------------------------|
| 1  | Rapat 1 | https://example.com/file1.pdf      |
| 2  | Rapat 2 | https://example.com/file2.pdf      |

---

## ⚙️ Alur Proses

1. ✅ **Unggah CSV**  
   Sistem membaca link dari kolom `supporting_file`.

2. 📥 **Download PDF**  
   File dari URL diunduh dan diproses.

3. 📚 **Split & Embed**  
   Dokumen dipecah menjadi chunk dan dibuat embedding-nya.

4. 🔍 **Query dengan RAG**  
   Sistem menanyakan isi dokumen untuk menentukan relevansi terhadap 13 Komisi DPR RI.

5. 🧠 **LLM Reasoning**  
   Ollama (dengan model `deepseek-r1:7b`) digunakan untuk menjawab pertanyaan berbasis konteks.

6. 🏷️ **Klasifikasi Komisi**  
   Output akhir berupa komisi yang relevan dengan isi dokumen.

---

## 🧩 Teknologi yang Digunakan

- **LangChain** – Loader, Chunking, Embedding, Retrieval  
- **Nomic-embed-text** – Embedding teks  
- **FAISS** – Semantic search  
- **Ollama** – Model lokal (Deepseek-R1:7b)  
- **pypdf** – Ekstraksi teks dari PDF

---

## 📌 Rekomendasi

- dapat menyesuaikan **model**, **prompt**, dan **logic RAG** sesuai kebutuhan .

---


