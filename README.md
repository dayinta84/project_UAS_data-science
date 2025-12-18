# 🛒 Segmentasi Pelanggan E-Commerce Menggunakan RFM, Clustering, dan Deep Learning Autoencoder

### 👤 Informasi Mahasiswa

* **Nama:** Dayinta Ayu Faj’rin
* **NIM:** 233307042
* **Program Studi:** D-III Teknologi Informasi
* **Mata Kuliah:** Data Science
* **Dosen Pengampu:** Gus Nanang Syaifuddiin, S.Kom., M.Kom.
* **Tahun Akademik:** 2025 / Semester 5
* **Repo:** (https://github.com/dayinta84/project_UAS_data-science.git)
* **Video:** https://drive.google.com/file/d/164qatlW8iDpALv_4J22cjZ7tBAWfPvru/view?usp=drive_link 

---

### 1. 🎯 Ringkasan Proyek

Proyek ini bertujuan untuk melakukan segmentasi pelanggan pada dataset **Online Retail** menggunakan pendekatan analisis **RFM (Recency, Frequency, Monetary)**. Proyek ini membandingkan efektivitas tiga metode clustering: Baseline (K-Means), Advanced Machine Learning (Gaussian Mixture Model), dan Deep Learning (Autoencoder).

**Aktivitas Utama:**
* Melakukan *data cleaning* dan preprocessing pada dataset transaksi retail yang besar.
* Membangun fitur perilaku pelanggan menggunakan metode **RFM**.
* Mengembangkan arsitektur **Autoencoder** untuk mempelajari fitur laten sebelum proses clustering.
* Mengevaluasi model menggunakan metrik *Silhouette Score*, *Davies-Bouldin Index*, dan *Calinski-Harabasz Index*.

---

### 2. 📄 Problem & Goals

**Latar Belakang & Masalah:**
* Perusahaan retail online memiliki data transaksi besar namun belum dimanfaatkan optimal untuk memahami perilaku pelanggan.
* Data transaksi memiliki isu kualitas (missing CustomerID, transaksi cancel, outliers) yang memerlukan pembersihan intensif.
* Diperlukan metode segmentasi otomatis untuk mengidentifikasi pelanggan bernilai tinggi (*High Value*) dan pelanggan berisiko (*Churn*).

**Goals:**
1.  Melakukan pembersihan data dan membangun fitur pelanggan berbasis **RFM**.
2.  Membangun 3 model segmentasi: **K-Means**, **GMM**, dan **Autoencoder + Clustering**.
3.  Menemukan model terbaik berdasarkan metrik evaluasi clustering untuk menghasilkan *insight* bisnis yang akurat.

---

### 📁 Struktur Folder

```text
UAS_Ecommerce_Segmentation/
│
├── data/
│   └── Online Retail.xlsx         # Dataset Sumber (UCI)
│
├── images/                        # Hasil Visualisasi & Evaluasi
│   ├── EDA_Distribution.png
│   ├── Elbow_Method.png
│   ├── Cluster_Visualization.png
│   └── Model_Comparison_Chart.png
│
├── models/                        # Model yang disimpan
│   ├── kmeans_baseline.pkl
│   ├── gmm_model.pkl
│   ├── autoencoder_model.h5       # Model Deep Learning (Keras/Tensorflow)
│   └── scaler.pkl                 # StandardScaler
│
├── notebooks/                     # Jupyter Notebook Utama
│   └── UAS_DATA_SCIENCE_DAYINTA.ipynb
│
├── requirements.txt               # Dependencies (Pandas, TensorFlow, Scikit-learn, dll)
└── README.md
```

---

### 3. 📊 Dataset & Data Understanding

* **Sumber:** [UCI Machine Learning Repository - Online Retail](https://archive.ics.uci.edu/dataset/352/online+retail)
* **Periode:** 01/12/2010 – 09/12/2011
* **Jumlah Data Awal:** 541,909 baris

**Fitur Utama:**

| Nama Fitur | Tipe Data | Deskripsi |
| :--- | :--- | :--- |
| **InvoiceNo** | String | Nomor invoice (awalan 'C' = Cancel) |
| **StockCode** | String | Kode produk |
| **Description** | String | Nama produk |
| **Quantity** | Integer | Jumlah item dibeli |
| **InvoiceDate** | Datetime | Waktu transaksi |
| **UnitPrice** | Float | Harga per unit (GBP) |
| **CustomerID** | Integer | ID unik pelanggan |
| **Country** | String | Negara asal pelanggan |

**Kondisi Data:**
* Terdapat *missing values* signifikan pada `CustomerID`.
* Terdapat transaksi pembatalan (Cancel) dan nilai negatif pada `Quantity`/`UnitPrice`.
* Distribusi data sangat *skewed* (timpang), didominasi oleh transaksi dari UK.

---

### 4. 🔧 Data Preparation

Langkah-langkah yang dilakukan dalam preprocessing:

1.  **Data Cleaning:**
    * Menghapus baris dengan `CustomerID` kosong karena fokus analisis adalah pelanggan.
    * Menghapus transaksi pembatalan (`InvoiceNo` diawali 'C').
    * Menghapus baris dengan `Quantity` ≤ 0 dan `UnitPrice` ≤ 0.
    * Menghapus data duplikat.
2.  **Feature Engineering (RFM):**
    * **Recency:** Selisih hari antara tanggal terakhir dataset dan transaksi terakhir pelanggan.
    * **Frequency:** Jumlah invoice unik per pelanggan.
    * **Monetary:** Total nilai belanja (`Quantity` × `UnitPrice`).
3.  **Scaling:**
    * Menggunakan `StandardScaler` untuk menormalisasi fitur RFM agar memiliki skala yang seimbang untuk algoritma berbasis jarak.

---

### 5. 🤖 Modeling

Tiga pendekatan model dikembangkan untuk perbandingan:

**Model 1: K-Means Clustering (Baseline)**
* Algoritma berbasis jarak yang membagi data ke dalam K cluster.
* *Parameter:* `n_clusters=4`.
* *Fungsi:* Sebagai tolok ukur (baseline) performa.

**Model 2: Gaussian Mixture Model (Advanced)**
* Algoritma probabilistik yang mengasumsikan data berasal dari campuran distribusi Gaussian.
* *Parameter:* `n_components=4`.
* *Fungsi:* Menangkap bentuk cluster yang lebih fleksibel.

**Model 3: Deep Learning (Autoencoder + K-Means)**
* Menggunakan **Autoencoder** untuk kompresi data dan mempelajari fitur laten (tersembunyi) sebelum di-cluster.
* *Arsitektur:* Input (3) → Encoder (8, 2) → Decoder (8, 3).
* *Training:* Optimizer Adam, Loss MSE, Epochs 50 (dengan EarlyStopping).
* *Fungsi:* Menangani kompleksitas data dan menghasilkan representasi fitur yang lebih informatif.

---

### 6. 🧪 Evaluation Results

Evaluasi dilakukan menggunakan tiga metrik utama:

| Model | Silhouette Score | Davies-Bouldin Index (Lower is Better) | Calinski-Harabasz Index (Higher is Better) |
| :--- | :--- | :--- | :--- |
| **K-Means (Baseline)** | **0.616** | 0.754 | 3145.06 |
| **GMM (Advanced)** | 0.163 | 1.620 | 894.83 |
| **Autoencoder + K-Means** | 0.570 | **0.618** | **4172.64** |

**Analisis Hasil:**
* **Model Terbaik:** **Autoencoder + K-Means**.
* **Alasan:** Model ini menghasilkan **Davies-Bouldin Index terendah** (0.618) dan **Calinski-Harabasz Index tertinggi** (4172.64). Hal ini menunjukkan bahwa penggunaan Deep Learning berhasil membentuk struktur cluster yang paling terpisah dengan jelas dan padat dibandingkan metode konvensional.

---

### 7. 🏁 Kesimpulan & Business Insight

**Kesimpulan:**
Integrasi **Deep Learning (Autoencoder)** terbukti meningkatkan kualitas segmentasi dibandingkan metode tradisional pada dataset ini. Representasi fitur laten membantu algoritma memisahkan karakteristik pelanggan dengan lebih tegas.

**Key Insights:**
1.  **Pelanggan Bernilai Rendah:** Mayoritas transaksi berasal dari pelanggan dengan frekuensi rendah dan nilai belanja kecil.
2.  **Potensi Loyal:** Teridentifikasi kelompok pelanggan dengan frekuensi tinggi dan nilai belanja besar yang harus menjadi prioritas strategi retensi.
3.  **Efektivitas Deep Learning:** Autoencoder mampu mempelajari representasi fitur yang lebih optimal dibanding fitur RFM mentah.

---

### 8. 🔮 Future Work

* **Data:** Menambah variasi data atau fitur baru seperti *Customer Tenure*.
* **Model:** Mencoba arsitektur Deep Learning yang lebih kompleks atau melakukan *Hyperparameter Tuning* yang lebih ekstensif.
* **Deployment:** Mengembangkan API menggunakan Flask/FastAPI atau dashboard interaktif.

---

### 9. 🔁 Reproducibility

Untuk menjalankan proyek ini di lokal komputer Anda:

1.  **Clone Repository:**
    ```bash
    git clone https://github.com/dayinta84/project_UAS_data-science.git
    ```

2.  **Install Dependencies:**
    ```bash
    pip install -r requirements.txt
    ```

3.  **Jalankan Notebook:**
    Buka `notebooks/UAS_DATA_SCIENCE_DAYINTA.ipynb` menggunakan Jupyter Notebook atau Google Colab.

---
Created by Dayinta Ayu Faj’rin © 2025

