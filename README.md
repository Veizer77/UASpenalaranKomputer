---

# 🧠 CBR_Penalaran_Komputer – Analisis Putusan Kasus Peretasan/Malware

Proyek ini adalah implementasi sistem **Case-Based Reasoning (CBR)** untuk menganalisis dan memprediksi putusan perkara *Pidana Khusus Peretasan, Malware, dan Tindak Pidana Siber Lainnya* berdasarkan dokumen hukum dari situs Direktori Mahkamah Agung Indonesia (`https://putusan3.mahkamahagung.go.id/`). Sistem ini meniru pola berpikir manusia—seperti hakim—dengan menggunakan putusan terdahulu untuk menyelesaikan kasus baru yang serupa.

---

## 📘 Deskripsi Proyek

Sistem ini terdiri dari lima tahapan utama yang diimplementasikan dalam lima notebook berikut:

1. **01_case_base.ipynb** – Mengambil dokumen PDF/HTML perkara siber dari Direktori Putusan MA dan mengubahnya menjadi teks mentah.
2. **02_representation.ipynb** – Mengekstrak metadata (nomor perkara, tanggal, pasal, pihak) dan konten kunci (fakta, argumentasi) menjadi format terstruktur (CSV/JSON).
3. **03_retrieval.ipynb** – Menerapkan metode pencarian kasus serupa menggunakan TF-IDF atau IndoBERT.
4. **04_reuse.ipynb** – Melakukan prediksi amar putusan berdasarkan 5 kasus paling mirip dengan pendekatan majority vote atau similarity weighting.
5. **05_evaluation.ipynb** – Mengevaluasi performa sistem dengan metrik klasifikasi (accuracy, precision, recall, F1), visualisasi, dan analisis kesalahan.

---

## 🧾 Prasyarat

Sebelum menjalankan sistem, pastikan Anda memiliki:

- Python 3.10 / 3.11
- Jupyter Notebook atau IDE seperti VSCode bisa juga google colab
- Koneksi internet untuk scraping dan pemanggilan model IndoBERT
- Dependensi yang tersedia di `requirements.txt`

---

## ⚙️ Instalasi

1. **Clone Repositori**
```bash
git clone https://github.com/Veizer77/UASpenalaranKomputer.git
cd Penalaran_Komputer/CBR/notebooks
````

2. **(Opsional) Buat Virtual Environment**

```bash
python -m venv venv
source venv/bin/activate  # Linux/Mac
venv\Scripts\activate     # Windows
```

3. **Instalasi Dependensi**

```bash
pip install -r requirements.txt
```

4. **Download NLTK Resource**

```python
import nltk
nltk.download('punkt')
```

---

## 🗂️ Struktur Direktori

```plaintext
CBR_Penalaran_Komputer/
├── CBR/
│   ├── data/
│   │   ├── raw/               # Teks putusan mentah dari PDF/HTML
│   │   ├── processed/         # Metadata & isi terstruktur
│   │   ├── eval/              # Query uji & metrik evaluasi
│   │   └── results/           # Hasil prediksi
│   ├── logs/                  # File log proses
│   ├── PDF/
│   │   ├── Peretasan/             # PDF putusan perkara peretasan/malware
│   ├── notebooks/
│   │   ├── 01_case_base.ipynb
│   │   ├── 02_representation.ipynb
│   │   ├── 03_retrieval.ipynb
│   │   ├── 04_reuse.ipynb
│   │   └── 05_evaluation.ipynb
├── README.md
├── requirements.txt
```

---

## 🚀 Eksekusi Pipeline

### 1. Bangun Case Base

```bash
jupyter notebook 01_case_base.ipynb
```

* Mengambil 30+ dokumen PDF atau HTML perkara peretasan dari situs MA.
* Menghapus header/footer, menyimpan teks bersih ke `data/raw/`.

### 2. Representasi Kasus

```bash
jupyter notebook 02_representation.ipynb
```

* Mengekstrak metadata (nomor, tanggal, pasal, pihak).
* Menyimpan ke `data/processed/cases.csv`.

### 3. Pencarian Kasus Serupa

```bash
jupyter notebook 03_retrieval.ipynb
```

* Menggunakan TF-IDF atau embedding IndoBERT untuk menghitung similarity.
* Simpan hasil retrieval top-5 di `data/eval/queries.json`.

### 4. Reuse Solusi (Prediksi Putusan)

```bash
jupyter notebook 04_reuse.ipynb
```

* Mengambil amar dari 5 kasus paling mirip.
* Memprediksi hasil kasus baru menggunakan voting/similarity.
* Output: `data/results/predictions.csv`.

### 5. Evaluasi Model

```bash
jupyter notebook 05_evaluation.ipynb
```

* Hitung Accuracy, Precision, Recall, F1-Score.
* Simpan hasil evaluasi ke `data/eval/retrieval_metrics.csv`.
* Tambahkan visualisasi hasil dan analisis kesalahan.

---

## 🧪 Menjalankan Notebook via Terminal

Jalankan notebook satu per satu dari Jupyter:

```bash
cd Penalaran_Komputer/CBR/notebooks
jupyter notebook 01_case_base.ipynb
```

Atau ubah menjadi skrip Python:

```bash
jupyter nbconvert --to script 01_case_base.ipynb
python 01_case_base.py
```

---

## ⚠️ Catatan Teknis

* **Batas Data:** Proyek diuji dengan maksimal 60 dokumen untuk efisiensi.
* **Model IndoBERT:** Secara default akan mengunduh model `indobenchmark/indobert-base-p1` saat pertama kali digunakan.
* **Dependensi Tambahan:** Pastikan `torch`, `transformers`, dan `sentence-transformers` sudah terpasang dengan benar.
* **Logging:** Semua proses tercatat di folder `logs/`.

---
