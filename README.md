# Text Mining: Analisis Sentimen Tweet Alicorn Twilight

## 📋 Deskripsi Proyek

Proyek ini merupakan implementasi lengkap pipeline text mining untuk menganalisis sentimen tweet tentang transformasi Twilight Sparkle menjadi Alicorn di akhir season 3 dari serial My Little Pony: Friendship is Magic. Dataset berisi sekitar 500 tweet yang dikumpulkan melalui crawling Twitter menggunakan tools oleh Helmi Satria.

Proyek ini mencakup seluruh proses dari preprocessing data, ekstraksi fitur, analisis sentimen, hingga klasifikasi menggunakan algoritma K-Nearest Neighbors (KNN).

## 🎯 Tujuan

- Melakukan preprocessing teks untuk membersihkan data tweet
- Mengekstraksi fitur menggunakan teknik unigram
- Menganalisis sentimen tweet (Positif, Negatif, Netral)
- Mengklasifikasikan sentimen menggunakan algoritma KNN
- Mengevaluasi performa model klasifikasi

## 📂 Struktur Proyek

```
alicorntwi-textmining/
├── alicorn_twilight.csv              # Dataset asli (raw tweets)
├── processed_tweets.csv              # Dataset setelah preprocessing
├── unigram_features_only.csv         # Fitur unigram saja
├── unigram_features.csv              # Fitur unigram + metadata
├── sentiment_analysis_results.csv    # Hasil analisis sentimen
├── Preprocessing.ipynb               # Notebook preprocessing
├── Feature Extraction.ipynb          # Notebook ekstraksi fitur
├── Sentiment Analysis.ipynb          # Notebook analisis sentimen
├── KNN Classification.ipynb          # Notebook klasifikasi KNN
└── README.md                         # Dokumentasi proyek
```

## 🔄 Pipeline Proyek

### 1️⃣ Preprocessing (Preprocessing.ipynb)

Tahap pembersihan dan normalisasi data tweet dengan langkah-langkah:

**Proses:**
- **Cleaning Text**: Menghapus URL, mention (@), hashtag (#), tanda baca, angka, dan whitespace berlebih
- **Case Normalization**: Mengubah semua teks menjadi lowercase
- **Stopword Removal**: Menghapus kata-kata umum bahasa Inggris yang tidak memberikan makna signifikan
- **Tokenization**: Memecah teks menjadi token-token individual
- **Lemmatization**: Mengubah kata ke bentuk dasarnya menggunakan WordNetLemmatizer
- **Handle Emoji**: Menghapus emoji dari teks
- **Handle Slang**: Mengganti kata slang dengan kata formal (u → you, lol → laughing out loud, dll)

**Input:** `alicorn_twilight.csv`  
**Output:** `processed_tweets.csv`

**Libraries yang digunakan:**
- `pandas`: Manipulasi data
- `re`: Regular expression untuk cleaning
- `nltk`: Tokenization, stopword removal, lemmatization

### 2️⃣ Feature Extraction (Feature Extraction.ipynb)

Ekstraksi fitur dari teks menggunakan teknik **Unigram** (bag-of-words dengan 1 kata).

**Proses:**
- Menggunakan `CountVectorizer` dari scikit-learn
- Menghasilkan matriks fitur dengan setiap kolom mewakili satu kata unik
- Setiap baris berisi frekuensi kemunculan kata pada tweet tersebut

**Input:** `processed_tweets.csv`  
**Output:** `unigram_features_only.csv`, `unigram_features.csv`

**Libraries yang digunakan:**
- `pandas`: Manipulasi data
- `sklearn.feature_extraction.text.CountVectorizer`: Ekstraksi fitur unigram

### 3️⃣ Sentiment Analysis (Sentiment Analysis.ipynb)

Analisis sentimen menggunakan pendekatan **Lexicon-based** dengan VADER (Valence Aware Dictionary and sEntiment Reasoner).

**Proses:**
- Menggunakan `SentimentIntensityAnalyzer` dari vaderSentiment
- Menghitung compound score untuk setiap tweet
- Klasifikasi sentimen:
  - **Positive**: compound ≥ 0.05
  - **Negative**: compound ≤ -0.05
  - **Neutral**: -0.05 < compound < 0.05

**Input:** `processed_tweets.csv`  
**Output:** `sentiment_analysis_results.csv`

**Libraries yang digunakan:**
- `pandas`: Manipulasi data
- `vaderSentiment.vaderSentiment.SentimentIntensityAnalyzer`: Analisis sentimen

### 4️⃣ KNN Classification (KNN Classification.ipynb)

Klasifikasi sentimen menggunakan algoritma **K-Nearest Neighbors** dengan supervised learning.

**Proses:**
- Menggunakan fitur unigram sebagai input (X)
- Menggunakan label sentimen dari VADER sebagai target (y)
- Split data: 80% training, 20% testing
- Training model KNN dengan k=3
- Evaluasi menggunakan classification report dan accuracy score

**Input:** `unigram_features_only.csv`, `sentiment_analysis_results.csv`  
**Output:** Model evaluation metrics

**Libraries yang digunakan:**
- `pandas`: Manipulasi data
- `sklearn.model_selection.train_test_split`: Split data
- `sklearn.neighbors.KNeighborsClassifier`: Model KNN
- `sklearn.metrics`: Evaluasi model (classification_report, accuracy_score)

## 🛠️ Teknologi & Libraries

### Core Libraries:
- **Python 3.x**
- **pandas**: Data manipulation
- **numpy**: Numerical operations
- **scikit-learn**: Machine learning algorithms
- **NLTK**: Natural Language Processing
- **vaderSentiment**: Sentiment analysis

### NLTK Resources:
- `stopwords`
- `punkt`
- `punkt_tab`
- `wordnet`

## 📊 Dataset

**Sumber:** Twitter (crawling menggunakan tools oleh Helmi Satria)  
**Topik:** Transformasi Twilight Sparkle menjadi Alicorn (My Little Pony Season 3)  
**Jumlah:** ~500 tweets  
**Bahasa:** Inggris  

**Kolom Dataset:**
- `conversation_id_str`: ID konversasi
- `created_at`: Timestamp tweet
- `favorite_count`: Jumlah like
- `full_text`: Konten tweet
- `id_str`: ID tweet
- `image_url`: URL gambar (jika ada)
- `in_reply_to_screen_name`: Username yang direply
- `lang`: Bahasa tweet
- `location`: Lokasi user
- `quote_count`: Jumlah quote
- `reply_count`: Jumlah reply
- `retweet_count`: Jumlah retweet
- `tweet_url`: URL tweet
- `user_id_str`: ID user
- `username`: Username

## 🚀 Cara Menggunakan

### Prerequisites:
```bash
pip install pandas numpy scikit-learn nltk vaderSentiment
```

### Download NLTK Resources:
```python
import nltk
nltk.download('stopwords')
nltk.download('punkt')
nltk.download('punkt_tab')
nltk.download('wordnet')
```

### Urutan Eksekusi:

1. **Preprocessing**
   ```
   Buka dan jalankan: Preprocessing.ipynb
   ```

2. **Feature Extraction**
   ```
   Buka dan jalankan: Feature Extraction.ipynb
   ```

3. **Sentiment Analysis**
   ```
   Buka dan jalankan: Sentiment Analysis.ipynb
   ```

4. **KNN Classification**
   ```
   Buka dan jalankan: KNN Classification.ipynb
   ```

## 📈 Hasil & Evaluasi

Model KNN dievaluasi menggunakan:
- **Classification Report**: Precision, Recall, F1-Score untuk setiap kelas
- **Accuracy Score**: Akurasi keseluruhan model
- **Confusion Matrix**: (dapat ditambahkan untuk visualisasi)

## 🔍 Insights

Proyek ini mendemonstrasikan:
- ✅ Pipeline lengkap text mining dari raw data hingga klasifikasi
- ✅ Preprocessing teks yang komprehensif (8 langkah)
- ✅ Kombinasi pendekatan lexicon-based dan machine learning
- ✅ Implementasi praktis NLP untuk analisis media sosial

## 👥 Kontributor

- **Dataset:** Helmi Satria (Twitter Crawling Tools)

## 📝 Catatan

- Proyek ini menggunakan Jupyter Notebook untuk kemudahan eksplorasi dan visualisasi
- Setiap notebook dapat dijalankan secara independen setelah prerequisites terpenuhi
- Dataset dapat diganti dengan dataset tweet lain dengan struktur serupa
- Parameter model (seperti k pada KNN) dapat disesuaikan untuk optimasi

## 📜 Lisensi

Proyek ini dibuat untuk keperluan akademis (Text Mining - Semester 5)

---

**⚠️ Disclaimer:** Dataset tweet dikumpulkan untuk tujuan penelitian dan pendidikan. Harap menghormati kebijakan privasi dan terms of service Twitter.
