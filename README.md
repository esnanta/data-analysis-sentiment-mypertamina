# Sentimen Analisis MyPertamina

Analisis ini merupakan alur belajar **Data Scientist** pada platform **Dicoding** dan bagian dari program **IDCamp 2024 Level Menengah**. Tujuan dari analisis adalah mengetahui **sentimen** menggunakan **klasifikasi teks** untuk mengidentifikasi dan mengevaluasi opini, sikap, atau emosi yang terkandung dalam teks ulasan aplikasi **MyPertamina**.
![Sentiment Analysis Word Clouds](https://github.com/esnanta/data-analysis-sentiment-mypertamina/blob/7a068c158104299e13bdf1a88d0980761d8918ac/image/sentiment_analysis_word_clouds.png?raw=true)


## Struktur Proyek

### 1. Import Library
Proyek ini menggunakan berbagai library Python untuk **web scraping**, **pemrosesan teks**, dan **machine learning**.

### 2. Pengumpulan Data
1. **Web scraping** dilakukan menggunakan **Google Play Scraper** untuk mengumpulkan ulasan aplikasi MyPertamina.
2. Dataset yang digunakan memiliki **minimal 10.000 sampel**.
3. **Pelabelan sentimen** dilakukan berdasarkan **leksikon Bahasa Indonesia** dengan tiga kelas sentimen: **positif, negatif, dan netral**.

### 3. Preprocessing Data
Proses preprocessing dilakukan untuk membersihkan dan menyiapkan data agar siap digunakan dalam model machine learning. Langkah-langkahnya meliputi:
1. **Cleaning data** (menghapus karakter khusus, emoji, dll.)
2. **Case folding** (mengubah semua teks menjadi huruf kecil)
3. **Tokenization** (memisahkan teks menjadi kata-kata)
4. **Stopword Removal** (menghapus kata-kata yang tidak memiliki makna signifikan dalam analisis sentimen)

### 4. Pelabelan Data
1. Digunakan **leksikon kata positif dan negatif** dalam **Bahasa Indonesia**.
2. Kolom target (label sentimen) adalah **text_akhir**.
3. **Distribusi sentimen** dihitung untuk memastikan keseimbangan kelas dalam dataset.

![Distribusi Sentimen](https://github.com/esnanta/data-analysis-sentiment-mypertamina/blob/65bceab3c68ba8795f28c1f2cd5625aad12d0f18/image/distribution_of_sentiment.png?raw=true)


### 5. Pelatihan Machine Learning
Model machine learning yang digunakan dalam proyek ini:
1. **Ekstraksi fitur menggunakan TF-IDF** (Term Frequency-Inverse Document Frequency)
2. **Ekstraksi fitur menggunakan Word2Vec** (untuk menangkap hubungan semantik antar kata)

## Hasil Analisis

### 1. Support Vector Machine (SVM) dengan TF-IDF + SMOTE
- **Akurasi tertinggi** sebesar **92,26%**.
- **Precision, recall, dan f1-score** rata-rata di atas **0,90** untuk setiap kelas.
- **Kelas 1** memiliki recall tertinggi (**0,95**), sedangkan **kelas 2** memiliki precision tertinggi (**0,94**).
- **Confusion Matrix:** Sedikit misclassification, terutama pada kelas **0 dan 2**.

### 2. RandomForest dengan TF-IDF + SMOTE
- **Akurasi 91,46%**, sedikit di bawah SVM namun masih tinggi.
- **Kelas 1** memiliki recall tertinggi (**0,96**), menunjukkan model dapat menangkap data kelas ini dengan baik.
- **Kelas 2** memiliki precision **0,93**, menandakan tingkat kesalahan prediksi yang rendah.

### 3. Confusion Matrix TF-IDF SVM & RandomForest
- **SVM lebih sedikit salah memprediksi** kelas **0 dan 2**, menghasilkan akurasi lebih tinggi.
- **RandomForest lebih akurat dalam memprediksi kelas 1**, tetapi mengalami lebih banyak kesalahan pada kelas **0 dan 2**.
- **Kesalahan prediksi sering terjadi antara kelas 0 ↔ 1 dan 1 ↔ 2**, menandakan kemiripan ekspresi antara sentimen netral dan positif/negatif.

![Confusion Matrix TF-IDF](https://github.com/esnanta/data-analysis-sentiment-mypertamina/blob/65bceab3c68ba8795f28c1f2cd5625aad12d0f18/image/confusion_matrix_tf-idf_svm_rf.png?raw=true)

### 4. RandomForest dengan Word2Vec + SMOTE
- **Akurasi lebih rendah** (78,93%) dibandingkan TF-IDF.
- **Kelas 1 memiliki precision tertinggi (0,92)**, sedangkan **kelas 0 memiliki recall tertinggi (0,85)**.
- Word2Vec memerlukan **fine-tuning lebih lanjut** agar dapat menangkap konteks lebih baik dibandingkan TF-IDF.

### 5. Confusion Matrix RandomForest + Word2Vec
- Model masih mengalami **banyak misclassification**, terutama untuk kelas **2**.
- Kelas 0: 902 sampel diklasifikasikan dengan benar.
- Kelas 1: 920 sampel diklasifikasikan dengan benar.
- Kelas 2: 640 sampel diklasifikasikan dengan benar.
- Kelas 1 memiliki kesalahan yang cukup merata, salah diprediksi sebagai kelas 0 (149 kasus) dan kelas 2 (114 kasus).
- Kelas 2 masih sering diklasifikasikan sebagai kelas 0 (211 kasus) dan kelas 1 (44 kasus).

![Confusion Matrix Word2Vec](https://github.com/esnanta/data-analysis-sentiment-mypertamina/blob/65bceab3c68ba8795f28c1f2cd5625aad12d0f18/image/confusion_matrix_word2vec_rf.png?raw=true)


## Kesimpulan
- **SVM dengan TF-IDF + SMOTE adalah model terbaik** untuk analisis sentimen ulasan MyPertamina dengan **akurasi 92,26%**.
- **RandomForest dengan TF-IDF** memiliki performa yang hampir setara dengan SVM (**91,46%**), tetapi lebih banyak kesalahan pada kelas tertentu.
- **Word2Vec memerlukan penyesuaian lebih lanjut**, karena hasilnya masih di bawah TF-IDF dalam menangkap pola sentimen dari teks ulasan.

## Teknologi yang Digunakan
- **Python** (pandas, numpy, scikit-learn, TensorFlow, gensim, Sastrawi, Google Play Scraper)
- **Google Colab** untuk eksperimen dan training model

---

## Cara Menjalankan Proyek
1. Clone repositori ini:
   ```sh
   git clone https://github.com/username/sentiment-analysis-mypertamina.git
   ```
2. Install dependensi yang dibutuhkan:
   ```sh
   pip install -r requirements.txt
   ```
3. Jalankan notebook **sentiment_analysis.ipynb** di Google Colab atau Jupyter Notebook.

## Lisensi
Proyek ini dilisensikan di bawah **MIT License**.

