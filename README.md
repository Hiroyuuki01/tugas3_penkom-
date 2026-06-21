#  CBR Putusan Narkotika — Case-Based Reasoning System

---

## Tim

Nama | NIM
Muhammad Aulia Rahman  202310370311005 
Iqbal Alfathi Bagarib  202310370311122

**Mata Kuliah:** Penalaran Komputer  
**Kelas:** Penalaran Komputer B  
**Universitas:** Universitas Muhammadiyah Malang  

---

## Deskripsi Proyek

Proyek ini mengimplementasikan siklus lengkap Case-Based Reasoning (CBR) untuk menganalisis putusan pengadilan perkara narkotika. Sistem ini mampu:

- Membangun **case base** dari dokumen putusan PDF
- Merepresentasikan kasus dalam format terstruktur (CSV/JSON)
- Melakukan **retrieval** kasus mirip menggunakan model IndoBERT
- Memberikan **rekomendasi solusi** berdasarkan kasus historis
- Mengevaluasi performa model dengan metrik standar

---

## Hasil Evaluasi

 Metrik | Nilai 
 Hit@5 | 90.00% 
 Accuracy | 90.00% 
 Precision | 100.00% 
 Recall | 90.00% 
 F1-Score | 94.74% 

**Model:** `paraphrase-multilingual-MiniLM-L12-v2`  
**Dataset:** 48 putusan pidana khusus narkotika & psikotropika  
**Domain:** Mahkamah Agung Republik Indonesia  

---
---

## Cara Menjalankan

### Tahap 1 & 2 — Case Base + Representation

```bash
notebooks/01_case_base_and_representation.ipynb
```

Output yang dihasilkan:
- `data/raw/txt/*.txt` — teks putusan hasil konversi
- `data/processed/cases.csv` — metadata kasus terstruktur
- `data/processed/cases.json` — metadata dalam format JSON
- `logs/cleaning.log` — log proses pembersihan

### Tahap 3, 4 & 5 — Retrieval + Reuse + Evaluasi

```bash
notebooks/02_case_retrieval.ipynb
```

Output yang dihasilkan:
- `data/processed/embeddings.npy` — vektor IndoBERT
- `data/results/predictions.csv` — prediksi solusi kasus baru
- `data/eval/retrieval_metrics.csv` — metrik evaluasi
- `data/eval/prediction_metrics.csv` — detail per query

---

---

## Model & Teknologi

 Komponen | Detail 
 **Embedding Model** | `paraphrase-multilingual-MiniLM-L12-v2` 
 **Similarity** | Cosine Similarity 
 **PDF Extraction** | pdfminer.six 
 **Data Processing** | pandas, numpy 
 **ML Framework** | scikit-learn, sentence-transformers 
 **Deep Learning** | PyTorch, transformers 

---

## Format Dataset (cases.csv)

 Kolom | Deskripsi 
 `case_id` | ID unik kasus (case_001, case_002, ...) 
 `filename` | Nama file TXT 
 `no_perkara` | Nomor perkara pengadilan 
 `tanggal` | Tanggal putusan 
 `jenis_perkara` | Pidana Khusus Narkotika & Psikotropika 
 `terdakwa` | Nama terdakwa 
 `pasal` | Pasal yang digunakan 
 `dakwaan` | Ringkasan dakwaan 
 `amar_putusan` | Amar putusan pengadilan 
 `ringkasan_fakta` | Ringkasan fakta persidangan 
 `word_count` | Jumlah kata dalam dokumen 

---

## Analisis Kegagalan

Dari 10 query evaluasi, terdapat **1 kasus gagal** (case_044):

- **Penyebab:** Teks kasus memiliki kemiripan konten tinggi dengan kasus lain (similarity = 0.9084), namun ground truth tidak masuk top-5

---