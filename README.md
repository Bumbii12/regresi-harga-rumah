# Laporan Proyek Regresi Harga Rumah – Daftar harga rumah di kawasan Tebet dan Jaksel

## 1. Domain Proyek

### Latar Belakang

Pasar perumahan di kawasan perkotaan seperti Tebet, Jakarta Selatan, dipengaruhi oleh berbagai faktor yang kompleks, termasuk kondisi ekonomi, lokasi, dan karakteristik properti (Zhang, Wang, & Li, 2020). Pemahaman mendalam terhadap faktor-faktor ini sangat penting untuk membantu pembeli, penjual, dan pengembang properti dalam pengambilan keputusan. Salah satu metode yang umum digunakan dalam memprediksi harga rumah adalah regresi linear, yang menganalisis hubungan antara variabel-variabel independen dengan harga sebagai variabel dependen (Li & Chen, 2019). Regresi linear memberikan kerangka kerja yang sederhana namun efektif untuk memahami tren pasar real estat dan mengidentifikasi faktor utama yang memengaruhi harga rumah.

Dalam penelitian ini, regresi linear diterapkan untuk memprediksi harga rumah di wilayah Tebet, Indonesia, dan dibandingkan dengan algoritma Random Forest sebagai metode pembanding. Random Forest dikenal memiliki keunggulan dalam menangani data non-linear dan interaksi variabel yang kompleks, sehingga sering digunakan dalam prediksi harga properti (Breiman, 2001). Dengan membandingkan kedua metode tersebut, penelitian ini bertujuan untuk menemukan pendekatan yang paling tepat untuk konteks pasar perumahan Tebet serta memberikan wawasan yang lebih luas mengenai kekuatan dan keterbatasan masing-masing algoritma dalam aplikasi prediksi harga rumah.

## 2. Business Understanding

### Problem Statements

- Bagaimana cara memprediksi harga rumah di kawasan Tebet secara akurat berdasarkan data properti yang tersedia?

- Algoritma prediksi mana yang lebih efektif dalam memodelkan harga rumah, regresi linear atau Random Forest?


### Goals

- Mengembangkan model prediksi harga rumah yang akurat di wilayah Tebet.

- Membandingkan efektivitas algoritma regresi linear dan Random Forest dalam memodelkan harga rumah.

- Menentukan metode terbaik untuk digunakan dalam konteks pasar properti Tebet.
### Manfaat

- Membantu pembeli dan penjual menentukan harga rumah yang lebih objektif dan realistis.

- Mempermudah agen properti dalam proses negosiasi dan pemasaran.

- Meningkatkan transparansi dan efisiensi pasar properti di Tebet.

- Memberikan dasar analisis yang kuat bagi investor dan pengembang properti.
### Solusi yang Diterapkan

1. **Preprocessing Data**  
   Data diperiksa untuk memastikan tidak ada duplikat dan nilai kosong, kemudian kolom diubah namanya agar konsisten dan harga dinormalisasi ke jutaan rupiah dengan penghapusan kolom nomor. Kategori harga baru dibuat berdasarkan kuartil dan median untuk klasifikasi rumah murah, menengah, dan mahal. Visualisasi distribusi, boxplot, dan analisis korelasi dilakukan untuk memahami sebaran data, hubungan antar fitur, serta mendeteksi outlier yang dipertahankan karena mencerminkan kondisi nyata. Distribusi jumlah rumah per kategori harga juga divisualisasikan untuk melihat proporsi data.

2. **Spliting Data**  
   - Data dibagi menjadi 70/30

3. **Training & Evaluasi**  
   - Membandingan model Linear Regression & Random Forest
   - Kedua model dievaluasi menggunakan metrik MAE, MSE, dan R² pada data pelatihan dan pengujian.
   - Model yang memberikan hasil yang lebih baik dalam evaluasi pengujian dipilih sebagai model akhir

4. **Pengujian Model**
   - Model akhir digunakan untuk memprediksi harga rumah pada data pengujian


## 3. Data Understanding

### Informasi Dataset

- Sumber: [Kaggle-Daftar harga rumah di kawasan Tebet dan Jaksel](https://www.kaggle.com/code/sateasinpedas/house-prediction-in-tebet-linear-regression/input). 
- Format: EXCEL  
- Jumlah data: 1010 baris dan delapan kolom (NO, NAMA RUMAH, HARGA,LB, LT, KT, KM, GRS)

Kolom:
- NO : nomor data.
NAMA RUMAH : title rumah.
HARGA : harga dari rumah.
LB : jumlah luas bangunan.
LT : jumlah luas tanah.
KT : jumlah kamar tidur.
KM : jumlah kamar mandi.
GRS : jumlah kapasitas mobil dalam garasi.

## Analisis Kuantitatif Dataset
1. Jumlah Data
- Total Baris: 1010 Baris
- Total Kolom: 8

## 2. Statistik Deskriptif Kolom

- **Kolom NO**  
  - **Tipe Data:** Integer  
  - **Rentang Nilai:** 1–1010  
  - **Deskripsi:** Nomor urut unik untuk setiap entri rumah dalam dataset.

- **Kolom NAMA RUMAH**  
  - **Tipe Data:** String (Object)  
  - **Deskripsi:** Nama atau label dari properti rumah yang ditawarkan.

- **Kolom HARGA**  
  - **Tipe Data:** Integer  
  - **Rentang Nilai:** 430 – 65.000 (dalam satuan juta rupiah)  
  - **Deskripsi:** Harga jual dari rumah.

- **Kolom LB (Luas Bangunan)**  
  - **Tipe Data:** Integer  
  - **Rentang Nilai:** 40 – 1126 (m²)  
  - **Deskripsi:** Luas bangunan rumah dalam satuan meter persegi (m²).

- **Kolom LT (Luas Tanah)**  
  - **Tipe Data:** Integer  
  - **Rentang Nilai:** 25 – 1400 (m²)  
  - **Deskripsi:** Luas tanah rumah dalam satuan meter persegi (m²).

- **Kolom KT (Kamar Tidur)**  
  - **Tipe Data:** Integer  
  - **Rentang Nilai:** 2 – 10  
  - **Deskripsi:** Jumlah kamar tidur dalam rumah.

- **Kolom KM (Kamar Mandi)**  
  - **Tipe Data:** Integer  
  - **Rentang Nilai:** 1 – 10  
  - **Deskripsi:** Jumlah kamar mandi dalam rumah.

- **Kolom GRS (Garasi/Carport)**  
  - **Tipe Data:** Integer  
  - **Rentang Nilai:** 0 – 10  
  - **Deskripsi:** Jumlah kapasitas garasi atau carport yang tersedia untuk kendaraan.


3. Kondisi Data
- Pemeriksaan Kualitas Data
  - Missing Values: 0
  - Duplicate Data: 0
  - Distribusi Data

![distribusi data])

  - Tampilan Dataset

Tampilan dataset awal dalam bentuk _DataFrame pandas_.  

| NO | NAMA RUMAH                                                      | HARGA        | LB  | LT  | KT | KM | GRS |
|----|------------------------------------------------------------------|--------------|-----|-----|----|----|-----|
| 1  | Rumah Murah Hook Tebet Timur, Tebet, Jakarta Selatan            | 3.800.000.000 | 220 | 220 | 3  | 3  | 0   |
| 2  | Rumah Modern di Tebet dekat Stasiun, Tebet, Jakarta Selatan     | 4.600.000.000 | 180 | 137 | 4  | 3  | 2   |
| 3  | Rumah Mewah 2 Lantai Hanya 3 Menit Ke Tebet, Tebet, Jakarta     | 3.000.000.000 | 267 | 250 | 4  | 4  | 4   |
| 4  | Rumah Baru Tebet, Tebet, Jakarta Selatan                        |   430.000.000 |  40 |  25 | 2  | 2  | 0   |
| 5  | Rumah Bagus Tebet komp Gudang Peluru lt 350m, Tebet, Jakarta    | 9.000.000.000 | 400 | 355 | 6  | 5  | 3   |


***

## 4. Data Preparation

Langkah-langkah persiapan data:

1. **Pengecekan Duplikat & Missing Values**  
   Data diperiksa untuk mengetahui apakah terdapat duplikasi dan nilai kosong pada setiap kolom.  
   ✅ Tidak ditemukan data duplikat maupun nilai kosong.

2. **Standarisasi Nama Kolom**  
   Nama-nama kolom diubah menjadi huruf kecil semua agar konsisten dan memudahkan proses analisis selanjutnya.

3. **Normalisasi Harga**  
   Nilai pada kolom `harga` dikonversi dari satuan Rupiah ke juta Rupiah agar lebih mudah dibaca.  
   Kolom `nomor` juga dihapus karena tidak memiliki pengaruh signifikan terhadap analisis.

4. **Pembuatan Label Kategori Harga**  
   Kategori harga ditentukan berdasarkan nilai kuartil:  
   - `Murah`: harga ≤ Q1  
   - `Menengah`: Q1 < harga ≤ Median  
   - `Mahal`: harga > Median  
   Kolom baru bernama `tingkat_harga` ditambahkan ke dataset.

5. **Visualisasi Distribusi Fitur**  
   Distribusi untuk fitur numerik divisualisasikan:  
   - Fitur `harga`, `luas bangunan (lb)`, dan `luas tanah (lt)` memiliki distribusi miring ke kanan (positively skewed).  
   - Fitur `jumlah kamar tidur (kt)`, `kamar mandi (km)`, dan `garasi (grs)` menunjukkan distribusi diskrit dengan puncak pada nilai 3–5.

6. **Deteksi Outlier dengan Boxplot**  
   Hampir semua fitur mengandung outlier, terutama pada `harga`, `lt`, dan `lb`.  
   Outlier **tidak dihapus** karena:
   - Mewakili variasi nyata dalam pasar properti (misal rumah mewah).
   - Penting untuk model pembelajaran, terutama regresi.
   - Tidak mengganggu hubungan antar variabel utama.

7. **Analisis Korelasi**  
   Korelasi antara variabel numerik dihitung dan divisualisasikan:  
   - Korelasi kuat ditemukan antara `harga` dengan `lt (0.81)` dan `lb (0.75)`.  
   - Fitur lain seperti `kt`, `km`, dan `grs` memiliki korelasi lebih rendah tapi tetap memberikan kontribusi.

8. **Visualisasi Kategori Harga**  
   Diagram batang dibuat untuk menunjukkan distribusi jumlah rumah berdasarkan kategori harga:  
   - `Mahal` adalah kategori dengan jumlah rumah terbanyak.  
   - Diikuti oleh `Menengah`, dan terakhir `Murah`.

9. **Data Spliting**
   Data dipecah menjadi 3 bagian:
   - 70% untuk training model
   - 30% untuk pengujian model

## 5. Modeling
   ### 1. Linear Regression
      Linear Regression adalah algoritma regresi yang sederhana dan umum digunakan untuk memodelkan hubungan linear antara fitur (misal: luas bangunan, luas tanah, jumlah kamar) dengan target (harga rumah).

      #### Proses:
      - Model dilatih menggunakan data pelatihan.
      - Tidak memerlukan tuning hyperparameter dalam implementasi dasarnya.
      - Cocok untuk data dengan hubungan linear antar variabel.

      #### Kelebihan:
      - Mudah dipahami dan diinterpretasikan.
      - Proses pelatihan cepat dan efisien.
      - Cocok untuk pola data linear.

      #### Kekurangan:
      - Kurang fleksibel untuk data non-linear.
      - Rentan terhadap outlier dan multikolinearitas.
      - Akurasi menurun jika data tidak linear.

      ---

   ### 2. Random Forest Regressor
      Random Forest Regressor adalah metode ensemble berbasis decision tree yang membangun banyak pohon dan menggabungkan hasilnya untuk prediksi yang lebih baik.

      #### Proses:
      - Dilakukan tuning hyperparameter dengan GridSearchCV.
      - Hyperparameter yang dituning:
      - `n_estimators` (jumlah pohon): 50, 100, 200
      - `max_depth` (kedalaman pohon): None, 10, 20
      - Model terbaik dipilih berdasarkan hasil tuning.

      #### Kelebihan:
      - Mampu menangani pola non-linear.
      - Lebih tahan terhadap outlier.
      - Memberikan estimasi pentingnya fitur.
      - Performa lebih stabil daripada single decision tree.

      #### Kekurangan:
      - Lebih lambat dalam pelatihan dan prediksi.
      - Kurang interpretatif dibanding linear regression.
      - Risiko overfitting jika tuning tidak optimal.

      ---


## 6. Evaluasi
   ## 📊 Evaluasi Model

Evaluasi dilakukan untuk mengukur performa kedua model (Linear Regression dan Random Forest Regressor) pada data pelatihan dan data pengujian dengan metrik utama:

- **MAE (Mean Absolute Error):** Rata-rata nilai absolut selisih prediksi dan nilai aktual.
- **MSE (Mean Squared Error):** Rata-rata kuadrat selisih prediksi dan nilai aktual, memberikan penalti lebih besar pada kesalahan besar.
- **R2 Score (Koefisien Determinasi):** Proporsi variansi target yang bisa dijelaskan oleh model, dengan nilai maksimum 1 (semakin tinggi semakin baik).

---

### Linear Regression

- Model ini menghasilkan nilai R2 sekitar 0.70 pada data pelatihan dan 0.76 pada data pengujian, yang menunjukkan model dapat menjelaskan sekitar 70-76% variansi harga rumah.
- Nilai MAE dan MSE cukup besar, menunjukkan masih terdapat kesalahan prediksi yang cukup signifikan, terutama pada data pengujian.

---

### Random Forest Regressor

- Setelah dilakukan tuning hyperparameter dengan GridSearchCV, model Random Forest menunjukkan peningkatan performa.
- Nilai R2 pada data pelatihan sangat tinggi (~0.95), dan pada data pengujian meningkat menjadi sekitar 0.79, menunjukkan model dapat menangkap pola data dengan lebih baik.
- MAE dan MSE pada data pengujian lebih kecil dibanding Linear Regression, menandakan prediksi yang lebih akurat dan kesalahan yang lebih rendah.

---

### Perbandingan Kinerja Model

| Model             | R2 Train | R2 Test | MAE Test   | MSE Test      |
|-------------------|----------|---------|------------|---------------|
| Linear Regression | 0.70     | 0.76    | 2064.45    | 11,744,520.00 |
| Random Forest     | 0.95     | 0.79    | 1757.68    | 9,974,966.00  |

- Random Forest menunjukkan performa yang lebih baik secara keseluruhan, terutama pada data pengujian, dengan R2 lebih tinggi dan error lebih kecil.
- Hal ini menunjukkan Random Forest lebih mampu menangani kompleksitas data harga rumah dibanding Linear Regression.
[Visualisasi Regresi Random Forest: Prediksi vs Nilai Aktual](https://)
---

## 7. Kesimpulan
Proyek ini berhasil mengembangkan dan membandingkan dua model prediksi harga rumah di wilayah Tebet, Jakarta Selatan, yaitu regresi linear dan Random Forest. Berdasarkan evaluasi dengan metrik MAE, MSE, dan R², model Random Forest memberikan performa lebih baik dengan kemampuan menangkap pola data yang kompleks dan non-linear, sehingga menghasilkan prediksi harga yang lebih akurat dibanding regresi linear. Hasil ini menunjukkan bahwa Random Forest lebih sesuai digunakan untuk prediksi harga rumah di pasar properti Tebet yang variatif. Model ini dapat membantu pembeli, penjual, dan pengembang properti dalam pengambilan keputusan harga yang lebih objektif dan realistis.


Referensi:  
  [Breiman, L. (2001). Random forests. Machine Learning, 45(1), 5–32.](https://doi.org/10.1023/A:1010933404324)

  [i, X., & Chen, Y. (2019). Housing price prediction based on multiple linear regression analysis. Journal of Real Estate Finance and Economics, 58(3), 400–415.](https://doi.org/10.1007/s11146-018-9700-3)

  [Zhang, J., Wang, S., & Li, Q. (2020). Factors influencing urban housing prices: A case study of Beijing. Sustainable Cities and Society, 62, 102395.](https://doi.org/10.1016/j.scs.2020.102395)