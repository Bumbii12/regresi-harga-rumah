# Laporan Proyek Analisis Sentimen dengan BERT – TripAdvisor Hotel Reviews

## 1. Domain Proyek

### Latar Belakang

Industri perhotelan sangat bergantung pada kepuasan pelanggan. Seiring perkembangan teknologi dan kemudahan akses informasi, calon tamu hotel kini semakin mengandalkan ulasan dari pengguna sebelumnya untuk menentukan pilihan mereka. Ulasan-ulasan ini tidak hanya memuat opini, kritik, dan pengalaman pribadi, namun juga mencerminkan sentimen yang bisa dikategorikan sebagai positif atau negatif (Ye, Law, & Gu, 2009).

Mengingat banyaknya jumlah ulasan yang tersedia secara online, proses analisis manual sangat tidak efisien. Oleh karena itu, dibutuhkan pendekatan otomatis berbasis Machine Learning untuk memahami dan mengklasifikasikan sentimen pelanggan (Medhat, Hassan, & Korashy, 2014). Dalam proyek ini, saya mengembangkan model analisis sentimen menggunakan pendekatan Deep Learning berbasis transformer, yaitu BERT (Bidirectional Encoder Representations from Transformers) yang terbukti efektif dalam memahami konteks bahasa alami (Devlin et al., 2019). Dataset yang digunakan berasal dari TripAdvisor, berisi 20.491 ulasan dan rating hotel.

## 2. Business Understanding

### Permasalahan Bisnis

- Bagaimana cara mengevaluasi sentimen pelanggan secara cepat dari ribuan ulasan?
- Bagaimana mengubah data teks ulasan menjadi wawasan strategis bagi pihak manajemen hotel?

### Tujuan

- Membangun sistem otomatis yang dapat mengklasifikasikan ulasan pelanggan menjadi sentimen positif atau negatif.
- Memberikan insight strategis untuk perbaikan layanan dan pengambilan keputusan yang berbasis data.

### Manfaat

- **Efisiensi analisis ulasan** dalam jumlah besar.
- **Identifikasi area perbaikan layanan** berdasarkan opini pelanggan.
- **Penguatan strategi pemasaran** dengan memahami persepsi pelanggan.
- **Keunggulan kompetitif**, melalui pemahaman mendalam terhadap kepuasan tamu hotel.

### Solusi yang Diterapkan

1. **Preprocessing Data**  
   - Mengonversi rating menjadi dua kelas sentimen:  
     - **Positif**: rating 4, 5  
     - **Negatif**: rating 1, 2, 3
   - Menghapus karakter tidak relevan seperti HTML, URL, angka, tanda baca, emoji, dan spasi berlebih
   - Lowercasing dan penghapusan stopwords menggunakan NLTK
   

2. **Modeling dengan BERT**  
   - Menggunakan tokenizer dan model pre-trained BERT untuk klasifikasi biner.  
   - Tokenisasi dengan padding dan truncation untuk panjang maksimum 128 token.  
   - Pembagian data ke dalam set pelatihan, validasi, dan pengujian.

3. **Training**  
   - Model dilatih menggunakan PyTorch dan optimizer AdamW.  
   - Hyperparameter: learning rate 5e-5, batch size 16, dan epoch sebanyak 3.

4. **Evaluasi**  
   - Evaluasi dilakukan dengan akurasi, precision, recall, dan F1-score.  
   - Model diuji pada dataset terpisah untuk mengukur generalisasi.

## 3. Data Understanding

### Informasi Dataset

- Sumber: [Kaggle - TripAdvisor Hotel Reviews](https://www.kaggle.com/datasets/andrewmvd/trip-advisor-hotel-reviews)  
- Format: CSV  
- Jumlah data: 20.491 baris dan 2 kolom (Review, Rating)

Kolom:
- **Review**: berisi teks ulasan
- **Rating**: angka 1 sampai 5 yang menunjukkan penilaian pelanggan

## Analisis Kuantitatif Dataset
1. Jumlah Data
- Total Baris: 20491 Baris
- Total Kolom: 2 (Review dan Rating)

2. Statistik Deskriptif Kolom
- Kolom Review
  - Tipe Data: String
  - Deskripsi: Kalimat/sentimen/pendapat/kritik yang ditulis oleh individu

- Kolom Rating
  - Tipe Data: Integer
  - Rentang Nilai: 1-5
  - Deskripsi: Perasaan yang dirasakan oleh individu yang digambarkan dengan skala angka

3. Kondisi Data
- Pemeriksaan Kualitas Data
  - Missing Values: 0
  - Distribusi Rating

![distribusi data](https://github.com/Bumbii12/submission-predictive-analysis/blob/main/images/distribusi_data.png)

  - Tampilan Dataset

Tampilan dataset awal dalam bentuk _DataFrame pandas_.  

|   | Review                                               | Rating   |
| - | ---------------------------------------------------- | ---------|
| 0 | nice hotel expensive parking got good deal sta...    | 4        |  
| 1 | ok nothing special charge diamond member hilto...    | 2        |  
| 2 | nice rooms experience hotel monaco seattle goo...    | 3        |    
| 3 | unique great stay wonderful time hotel monaco ...    | 5        | 
| 4 | great stay great stay went seahawk game awesom...    | 5        |

***

## 4. Data Preparation

Langkah-langkah persiapan data:

1. **Label Sentimen**  
   - Positif (1): rating 4, 5  
   - Negatif (0): rating 1, 2, 3

2. **Pembersihan Teks**  
   - Menghapus HTML, URL, angka, tanda baca, emoji  
   - Lowercasing dan stopword removal

3. **Pembagian Data**  
   - Stratified sampling: 70% data pelatihan dan 30% data testing

4. **Tokenisasi**  
   - Menggunakan tokenizer BERT  
   - Padding dan truncation ke 128 token

5. **Konversi ke Tensor Dataset**  
   - Dataset diubah menjadi objek tensor PyTorch agar dapat digunakan dalam proses pelatihan model.

## 5. Modeling

### Arsitektur Model

- Menggunakan model bert-base-uncased dari HuggingFace Transformers.
- Model BertForSequenceClassification digunakan untuk klasifikasi biner.
- Tokenisasi dilakukan menggunakan BertTokenizer.
- Seluruh parameter BERT difine-tune selama pelatihan.
- Layer klasifikasi linear (dengan softmax) ditambahkan di atas representasi BERT.

### Penjelasan Cara Kerja BERT
BERT (Bidirectional Encoder Representations from Transformers) adalah model pra-latih berbasis arsitektur Transformer, yang dirancang untuk memahami konteks kata dalam kalimat secara bidirectional.

#### Arsitektur Transformer

BERT terdiri dari beberapa lapisan encoder dari Transformer, yang menggunakan mekanisme self-attention untuk memproses kata-kata dalam sebuah urutan. Tidak seperti model sekuensial tradisional (misalnya RNN), Transformer memungkinkan pemrosesan paralel dan menangkap dependensi kata yang jauh dalam teks.

#### Mekanisme Self-Attention

Dalam setiap layer encoder, BERT menghitung attention score antar kata dalam kalimat. Mekanisme self-attention ini memungkinkan model untuk menimbang pentingnya setiap kata terhadap kata lainnya, sehingga dapat memahami makna kontekstual secara lebih mendalam.

#### Pemrosesan Bidirectional

BERT memproses input secara bidirectional, artinya ia melihat konteks di kiri dan kanan suatu kata secara bersamaan saat melakukan pretraining. Ini berbeda dari model unidirectional seperti GPT, yang hanya melihat satu arah konteks (misalnya, dari kiri ke kanan). Sifat ini memungkinkan BERT menangkap makna kata yang lebih akurat dalam konteksnya.

#### Pretraining dan Fine-tuning

BERT dilatih terlebih dahulu (pretraining) menggunakan dua tugas: Masked Language Modeling (MLM) dan Next Sentence Prediction (NSP). Setelah pretraining, BERT dapat disesuaikan (fine-tuned) untuk tugas spesifik seperti klasifikasi sentimen, hanya dengan menambahkan layer klasifikasi di atasnya dan melatih ulang pada data spesifik.
### Hyperparameter dan Konfigurasi

| Parameter        | Nilai     |
|------------------|-----------|
| Learning Rate    | 5e-5      |
| Batch Size       | 16        |
| Epoch            | 3         |
| Optimizer        | AdamW     |
| Loss Function    | CrossEntropyLoss  |


> Catatan: Meski tugas ini adalah klasifikasi biner, CrossEntropyLoss tetap digunakan karena arsitektur BertForSequenceClassification mengasumsikan kelas >1 dan output logits, bukan probabilitas.

### Proses Training

- Input: input_ids dan attention_mask
- Loss: Binary Cross Entropy
- Optimizer: AdamW
- Performa divalidasi setiap epoch
- Checkpoint model disimpan jika validasi meningkat



## 6. Evaluasi

### Hasil Akurasi
![Akurasi](https://github.com/Bumbii12/submission-predictive-analysis/blob/main/images/acuracy.png)
- Akurasi pelatihan mencapai ~94%
- Akurasi validasi mencapai ~89%


### Confusion Matrix

![Confusion Matrix](https://github.com/Bumbii12/submission-predictive-analysis/blob/main/images/confusion_matrix.png)

- True Positive: 4264  
- True Negative: 1248  
- False Positive: 372 
- False Negative: 264

### Classification Report

| Sentimen | Precision | Recall | F1-Score | Support |
|----------|-----------|--------|----------|---------|
| Negatif  | 0.83      | 0.77   | 0.80     | 1620     |
| Positif  | 0.92      | 0.94   | 0.93     | 4528    |
| **Akurasi** |     |      | **0.90**  | 6148    |

### Analisis Hasil

- Model menunjukkan performa sangat baik dalam mengklasifikasikan ulasan positif (F1 93%)
- Performa pada kelas negatif juga cukup solid dengan F1-score 80%
- Skor weighted average F1 mencapai 90%, menunjukkan model sangat andal pada data uji

## 7. Kesimpulan

Model BERT yang dikembangkan berhasil melakukan klasifikasi sentimen ulasan hotel dengan akurasi tinggi. Evaluasi menunjukkan bahwa model sangat andal dalam mendeteksi sentimen positif dan cukup baik dalam menangkap sentimen negatif. Sistem ini dapat diandalkan untuk membantu hotel memahami umpan balik pelanggan dan meningkatkan kualitas layanan berdasarkan data.


Referensi:  
  [Devlin, J., Chang, M. W., Lee, K., & Toutanova, K. (2019). BERT: Pre-training of Deep Bidirectional Transformers for Language Understanding. arXiv preprint arXiv:1810.04805](https://arxiv.org/abs/1810.04805)
  [Medhat, W., Hassan, A., & Korashy, H. (2014). Sentiment analysis algorithms and applications: A survey. Ain Shams Engineering Journal, 5(4), 1093–1113.](https://doi.org/10.1016/j.asej.2014.04.011)
  [Ye, Q., Law, R., & Gu, B. (2009). The impact of online user reviews on hotel room sales. International Journal of Hospitality Management, 28(1), 180–182.](https://doi.org/10.1016/j.ijhm.2008.06.011)