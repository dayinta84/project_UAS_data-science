# 📊 Online Retail Customer Segmentation  
**RFM Analysis, Clustering, and Deep Learning Autoencoder**

---

## 👤 Informasi Proyek
- **Nama Mahasiswa:** Dayinta Ayu Faj'rin  
- **NIM:** 233307042
- **Program Studi:** Teknologi Informasi 
- **Mata Kuliah:** Data Science  
- **Dosen Pengampu:** Gus Nanang Syaifuddin  

🔗 **GitHub Repository:** https://github.com/dayinta84/project_UAS_data-science.git
🎥 **Video Pembahasan:** [ISI LINK VIDEO]

---

## 🎯 Ringkasan Proyek
Proyek ini bertujuan untuk melakukan **segmentasi pelanggan** pada dataset **Online Retail (UCI Machine Learning Repository)** menggunakan pendekatan **RFM (Recency, Frequency, Monetary)**.  
Tiga model dikembangkan dan dibandingkan, yaitu:
1. **K-Means Clustering** sebagai baseline
2. **Gaussian Mixture Model (GMM)** sebagai model advanced
3. **Autoencoder + K-Means** sebagai model deep learning (wajib)

Evaluasi dilakukan menggunakan metrik clustering yang sesuai, yaitu **Silhouette Score**, **Davies-Bouldin Index**, dan **Calinski-Harabasz Index**.

---

## 📁 Struktur Folder
Struktur repository disusun agar rapi dan mendukung reproducibility:

CS2025-main/
│
├── data/
│ ├── Online Retail.xlsx # Dataset (opsional, sumber asli via URL)
│ └── .gitkeep
│
├── notebooks/
│ ├── UAS_Dayinta_dataScience.ipynb
│ └── .gitkeep
│
├── models/
│ ├── scaler.pkl # StandardScaler
│ ├── kmeans_model.pkl # K-Means model
│ ├── gmm_model.pkl # GMM model
│ ├── autoencoder.h5 # Autoencoder (Deep Learning)
│ ├── encoder.h5 # Encoder (Latent Space)
│ └── .gitkeep
│
├── images/
│ ├── 1_kondisi_data.png
│ ├── 2_eda_1.png
│ ├── 3_eda_2.png
│ ├── 4_eda_3.png
│ ├── 5_data_cleaning.png
│ ├── 6_feature_engineering.png
│ ├── 7_data_transformation.png
│ ├── 8_model_1.png
│ ├── 9_model_2.png
│ ├── 10_model_3.png
│ ├── 11_training_model_3.png
│ ├── 12_training_process.png
│ └── 14_visualisasi_perbandingan.png
│
├── src/
│ └── .gitkeep
│
├── requirements.txt
├── README.md
├── LICENSE
└── Cheklist Submit.md



📌 **Catatan:**  
Dataset diunduh langsung dari URL UCI di dalam notebook untuk menjaga ukuran repository tetap kecil.

---

## 📊 Dataset
- **Nama Dataset:** Online Retail
- **Sumber:** UCI Machine Learning Repository  
  https://archive.ics.uci.edu/ml/datasets/online+retail
- **Tipe Data:** Tabular (Transaksi Retail)
- **Jumlah Data:** ± 541.909 baris (sebelum cleaning)
- **Periode:** Desember 2010 – Desember 2011

---

## 🔧 Data Preparation
Tahapan preprocessing yang dilakukan:
1. **Data Cleaning**
   - Menghapus missing CustomerID
   - Menghapus transaksi cancel (InvoiceNo diawali “C”)
   - Menghapus Quantity ≤ 0 dan UnitPrice ≤ 0
2. **Feature Engineering**
   - Membuat fitur **TotalPrice**
   - Agregasi data pelanggan menggunakan **RFM**
3. **Data Transformation**
   - Standardisasi fitur RFM menggunakan **StandardScaler**

---

## 🤖 Modeling
Tiga model yang digunakan dalam proyek ini:

### 🔹 Model 1 – K-Means (Baseline)
- Algoritma clustering berbasis jarak
- Cepat dan sederhana
- Digunakan sebagai pembanding awal

### 🔹 Model 2 – Gaussian Mixture Model (Advanced)
- Clustering berbasis probabilistik
- Lebih fleksibel dibanding K-Means
- Namun performa lebih rendah pada dataset ini

### 🔹 Model 3 – Autoencoder + K-Means (Deep Learning)
- Autoencoder mempelajari **latent representation**
- Clustering dilakukan pada latent space
- Memberikan struktur cluster terbaik

---

## 🧪 Evaluation
Metrik evaluasi yang digunakan:
- **Silhouette Score**
- **Davies-Bouldin Index**
- **Calinski-Harabasz Index**

| Model | Silhouette | Davies-Bouldin | Calinski-Harabasz |
|------|-----------|----------------|------------------|
| K-Means | 0.616 | 0.754 | 3145 |
| GMM | 0.163 | 1.620 | 895 |
| Autoencoder + K-Means | 0.570 | **0.618** | **4172** |

📌 **Model terbaik:** **Autoencoder + K-Means**

---

## 💾 Model Artifacts
Seluruh model yang telah dilatih disimpan dalam folder `models/`:
- `.pkl` → model machine learning & scaler
- `.h5` → model deep learning (TensorFlow/Keras)

Hal ini mendukung **reproducibility** dan penggunaan ulang model tanpa training ulang.

---

## 🔁 Reproducibility

### Menjalankan di Google Colab
- Buka notebook di folder `notebooks/`
- Jalankan seluruh cell dari atas ke bawah

### Menjalankan di Lokal
```bash
pip install -r requirements.txt
jupyter notebook
