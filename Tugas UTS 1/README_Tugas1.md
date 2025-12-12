## 1. Tujuan Repositori
Repositori ini dibuat untuk memenuhi UTS Mata Kuliah **Machine Learning**, di mana mahasiswa diminta untuk membangun sistem pendeteksian transaksi penipuan (*fraud detection*) secara **end-to-end**, mulai dari preprocessing, penanganan imbalance, pemodelan Machine Learning, hingga membuat file submission untuk data uji.

Target utama:
- Membangun pipeline end-to-end yang efisien dan optimal.  
- Menghasilkan model dengan performa tinggi menggunakan metrik ROC-AUC & PR-AUC.  
- Menerapkan teknik *feature engineering*, balancing, dan OOF validation.  
- Menghasilkan file prediksi untuk *test set* (`submission.csv`).

---

## 2. Gambaran Singkat Proyek
Dataset transaksi online memiliki label biner **isFraud** (0 = normal, 1 = fraud).  
Dataset memiliki ratusan fitur dari berbagai kategori:

- Informasi transaksi (waktu, jumlah, merchant, device)
- Informasi identitas pengguna
- Fitur kartu kredit/debit
- Alamat dan domain email
- Variabel kategorikal & numerikal dengan missing value besar

Proyek ini membangun sistem lengkap mulai dari:
1. Explorasi dan pembersihan data  
2. Preprocessing + Optimisasi memori  
3. Feature engineering  
4. Imbalance handling (UnderSampling + SMOTE)  
5. Model training (LightGBM + Stacking)  
6. Out-of-Fold validation (5-Fold)  
7. Pembuatan submission final  

Pipeline ini dirancang agar tetap berjalan di Google Colab **gratis**, dengan optimasi RAM 12GB.

---

## 3. Model yang Digunakan & Hasil Evaluasi

### ** Model Utama: LightGBM**
Model utama menggunakan **LightGBM Gradient Boosting**, dipilih karena:
- Performa sangat tinggi untuk dataset tabular
- Konsumsi memori rendah
- Training cepat
- Mampu menangani missing value

#### **Hasil Validasi (OOF – 5 Fold):**
| Metrik | Skor |
|-------|-------|
| **ROC-AUC** | **0.9757** |
| **PR-AUC** | **0.9798** |

Hasil ini menunjukkan model sangat kuat dan stabil pada banyak fold.

---

###  **Model Tambahan (Stacking Layer)**
Model sekunder digunakan untuk *stacking*:

- **XGBoost**
- **Random Forest**
Keluaran probabilitas dari masing-masing model digabungkan untuk membuat prediksi yang lebih stabil.

---

###  Feature Importance (Top)
1. C8  
2. C14  
3. C4  
4. C13  
5. card1_card2  
6. TransactionAmt  
7. addr1  
8. P_emaildomain  

Model menggunakan kombinasi fitur asli + feature engineering seperti:
- `TransactionAmt_log`
- `DT_hour`
- `DT_day`
- Kombinasi fitur kartu (`card1_card2`, dll)

---

###  Handling Class Imbalance
Dataset sangat tidak berimbang:
0 → 96.5%
1 → 3.5%
Untuk mengatasi ini, digunakan:
- **RandomUnderSampler** → mengurangi mayoritas
- **Small SMOTE** → menambah minoritas secukupnya
- Kombinasi aman untuk RAM Google Colab

Metode ini terbukti memberikan OOF AUC sangat tinggi.

---
## 4. Navigasi 





### 5. Identitas
Nama : Eggy Alfan Ananta
Kelas : TK4602
NIM  : 1103223194

