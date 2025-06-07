# Laporan Proyek Machine Learning - Haiqel Aziizul Hakeem - Anime Recommendation System
## Project Overview

Industri hiburan digital, khususnya anime, telah mengalami pertumbuhan yang sangat pesat dalam dekade terakhir. Dengan semakin banyaknya judul anime yang diproduksi setiap tahunnya, pengguna platform streaming dan komunitas anime menghadapi kesulitan dalam menemukan konten yang sesuai dengan preferensi mereka. Fenomena "information overload" atau kelebihan informasi ini menjadi tantangan utama bagi konsumen dalam memilih anime yang tepat dari ribuan pilihan yang tersedia.

Sistem rekomendasi telah terbukti efektif dalam mengatasi masalah ini di berbagai domain, mulai dari e-commerce hingga platform streaming musik dan video. Netflix, sebagai contoh, melaporkan bahwa 80% konten yang ditonton pengguna berasal dari sistem rekomendasi mereka [[1]](https://dl.acm.org/doi/10.1145/2843948). Menurut Ricci et al. (2015), sistem rekomendasi modern menggunakan berbagai pendekatan termasuk collaborative filtering, content-based filtering, dan hybrid approaches untuk memberikan rekomendasi yang personal dan akurat [[2]](https://www.researchgate.net/publication/227268858_Recommender_Systems_Handbook). Dalam konteks anime, sistem rekomendasi yang akurat dapat meningkatkan engagement pengguna, mengurangi waktu pencarian, dan meningkatkan kepuasan konsumen secara keseluruhan.

Dataset Anime Recommendations Database dari Kaggle menyediakan data rating dan informasi anime yang komprehensif, mencakup lebih dari 73.000 pengguna dan 12.000 judul anime. Dataset ini memungkinkan pengembangan sistem rekomendasi yang dapat menganalisis pola preferensi pengguna dan karakteristik anime untuk memberikan rekomendasi yang personal dan akurat.

Pengembangan sistem rekomendasi anime ini relevan karena:
1. **Personalisasi Pengalaman**: Setiap pengguna memiliki preferensi genre, durasi, dan tema yang berbeda
2. **Efisiensi Waktu**: Mengurangi waktu yang dibutuhkan pengguna untuk mencari anime baru
3. **Peningkatan Engagement**: Rekomendasi yang akurat dapat meningkatkan waktu tonton dan kepuasan pengguna
4. **Analisis Tren**: Memahami pola konsumsi anime untuk insights industri

### Referensi:
- Gomez-Uribe, C. A., & Hunt, N. (2015). The Netflix Recommender System: Algorithms, Business Value, and Innovation. *ACM Transactions on Management Information Systems*, 6(4), 1-19.
- Ricci, F., Rokach, L., & Shapira, B. (2015). *Recommender Systems Handbook*. Springer.
  
## Business Understanding

Dalam era digital yang dipenuhi dengan konten hiburan yang melimpah, pengguna anime menghadapi tantangan signifikan dalam menemukan konten yang sesuai dengan preferensi mereka. Proses klarifikasi masalah ini penting untuk memahami kebutuhan pengguna dan mengembangkan solusi yang tepat sasaran.

### Problem Statements

1. Information Overload dalam Pemilihan Anime
Pengguna menghadapi kesulitan dalam memilih anime yang sesuai dengan preferensi mereka dari ribuan judul yang tersedia. Dengan lebih dari 12.000 judul anime dalam dataset, pengguna seringkali merasa kewalahan dan akhirnya menonton anime secara acak atau berdasarkan popularitas semata.
2. Keterbatasan Pendekatan Rekomendasi Tunggal
Sistem rekomendasi yang hanya menggunakan satu pendekatan (content-based atau collaborative filtering) memiliki keterbatasan dalam memberikan rekomendasi yang komprehensif dan akurat untuk semua situasi.

### Goals
1. Implementasi Content-Based Filtering System Recommendation dengan TF-IDF dan Cosine Similarity
Mengembangkan sistem content-based filtering menggunakan TF-IDF dan Cosine Similarity untuk menganalisis kesamaan antar anime berdasarkan karakteristik konten (genre, tipe, episode), sehingga dapat memberikan rekomendasi yang relevan tanpa bergantung pada data rating pengguna lain.
2. Implementasi Collaborative Filtering dengan SVD
Membangun model collaborative filtering menggunakan Singular Value Decomposition (SVD) yang dapat memprediksi rating pengguna terhadap anime yang belum ditonton berdasarkan pola rating historis dan kesamaan preferensi antar pengguna.

### Solution Statements
1. Content-Based Filtering dengan TF-IDF dan Cosine Similarity
Mengimplementasikan sistem rekomendasi berdasarkan kesamaan konten anime menggunakan:
- TF-IDF Vectorization: Mengkonversi fitur kategorikal anime (genre, tipe, episode) menjadi representasi vektor numerik
- Cosine Similarity: Mengukur kesamaan antar anime berdasarkan sudut vektor fitur
- Rekomendasi: Memberikan anime dengan skor kesamaan tertinggi terhadap anime yang disukai pengguna
- Keunggulan: Tidak memerlukan data rating pengguna lain, cocok untuk mengatasi cold start problem

2. Collaborative Filtering dengan Singular Value Decomposition (SVD)
Menggunakan matrix factorization untuk memprediksi rating pengguna terhadap anime yang belum ditonton:

- SVD Algorithm: Mendekomposisi user-item rating matrix menjadi faktor laten pengguna dan anime
- Prediksi Rating: Menggunakan dot product antara faktor laten untuk memprediksi rating
- Evaluasi: Menggunakan Root Mean Square Error (RMSE) untuk mengukur akurasi prediksi
- Keunggulan: Dapat menangkap pola preferensi tersembunyi dan memberikan rekomendasi personal

  Model SVD akan dievaluasi menggunakan metrik RMSE untuk memastikan kualitas prediksi rating yang optimal, dengan target meminimalkan error antara rating aktual dan prediksi.

## Data Understanding
Dataset yang digunakan berasal dari Kaggle dengan nama [[Anime Recommendations Database]](https://www.kaggle.com/datasets/CooperUnion/anime-recommendations-database). Dataset terdiri dari file `anime.csv` (Informasi terkait anime) dan `rating.csv` (Interaksi pengguna berupa rating terhadap anime). Pada `anime.csv` terdiri dari beberapa kolom, seperti: anime_id, name, genre, type, episodes, rating, dan members. Sementara `rating.csv` terdiri dari beberapa kolom, seperti: user_id, anime_id, dan rating.

Deskripsi `anime.csv`
Jumlah Data: 12.294 baris, 7 kolom  
Terdapat missing values pada kolom `genre`, `type`, dan `rating`.

| Kolom       | Deskripsi                                               |
|-------------|---------------------------------------------------------|
| `anime_id`  | ID unik tiap anime                                      |
| `name`      | Nama anime                                              |
| `genre`     | Genre anime, dapat lebih dari satu                      |
| `type`      | Tipe anime (TV, Movie, OVA, dll)                        |
| `episodes`  | Jumlah episode anime                                    |
| `rating`    | Rating dari pengguna                                    |
| `members`   | Jumlah user yang memberi rating di MyAnimeList         |

---

Deskripsi `rating.csv`
Jumlah Data: ±7 juta baris, 3 kolom  
Dataset ini digunakan untuk collaborative filtering.

#### Fitur/Variabel:
| Kolom      | Deskripsi                                               |
|------------|---------------------------------------------------------|
| `user_id`  | ID unik pengguna                                        |
| `anime_id` | ID anime yang dirating                                  |
| `rating`   | Rating yang diberikan pengguna terhadap anime (1–10)    |
> *Rating = -1 berarti pengguna telah menonton tetapi tidak memberi rating.*

---

Exploratory Data Analysis (EDA)

Beberapa visualisasi dan analisis yang dilakukan:
- Distribusi `type` anime (TV paling dominan)
- Korelasi antara `rating` dan `members`
- Visualisasi jumlah episode
- Visualisasi distribusi `rating`
- Missing value analysis

## Data Preparation
1. Penanganan Missing Value

```python
anime_df['genre'] = anime_df['genre'].fillna('Unknown')
```
Kolom `genre` yang kosong diidi dengan nilai `'Unknown'` agar dapat dilakukan preprocessing selanjutnya

```python
type_mode = anime_df['type'].mode()[0]
anime_df['type'] = anime_df['type'].fillna(type_mode)
```
Kolom `type` diisi menggunakan modus (nilai yang paling sering muncul), karena `type` merupakan kategori (TV, Movie, dll), maka pengisian terbaik adalah dengan nilai paling umum.

```python
episode_medians = anime_df.groupby('type')['episodes'].median()
anime_df['episodes'] = anime_df.apply(
    lambda row: episode_medians[row['type']] if pd.isna(row['episodes']) else row['episodes'],
    axis=1
)
```
Nilai kosong pada kolom `episodes` diisi dengan nilai median episode berdasarkan type masing-masing. Teknik ini menghindari bias akibat nilai ekstrim dan mempertimbangkan konteks `type`.

```python
avg_rating = np.average(
    anime_df['rating'].dropna(),
    weights=anime_df.loc[anime_df['rating'].notna(), 'members']
)
anime_df['rating'] = anime_df['rating'].fillna(avg_rating)
```
Rating yang kosong diisi menggunakan weighted average berdasarkan jumlah `members`. Tujuannya agar rating lebih representatif karena memperhitungkan popularitas.

2. Preprocessing Content Based Filtering
```python
anime_df['genre_list'] = anime_df['genre'].str.split(', ')
```
Genre diubah menjadi list agar dapat digunakan dalam proses tokenization genre.

```python
anime_df['genre_features'] = anime_df['genre'].str.replace(', ', ' ')
```
Genre diubah menjadi format string tunggal tanpa koma agar cocok digunakan oleh TF-IDF.

```python
rating_df_clean = rating_df[rating_df['rating'] > 0].dropna()
```
Menghapus baris rating yang tidak valid (rating = -1), karena artinya user tidak memberikan rating. Langkah ini penting agar model collaborative tidak dilatih dengan data kosong atau noise.

3. Pembersihan Data Rating
```python
   rating_df_clean = rating_df[rating_df['rating'] > 0].dropna()
```
Menghapus baris rating yang tidak valid (rating = -1), karena artinya user tidak memberikan rating. Langkah ini penting agar model collaborative tidak dilatih dengan data kosong atau noise.

4. Ekstraksi Fitur Content-Based dengan TF-IDF
```python
tfidf = TfidfVectorizer(tokenizer=lambda x: x, preprocessor=lambda x: x)
genre_matrix = tfidf.fit_transform(anime_df['genre_list'])
```
Menggunakan TF-IDF untuk menghasilkan representasi vektor dari genre. Vektor ini digunakan untuk menghitung kemiripan antar anime dalam content-based filtering.

5. Skor Popularitas
```python
anime_df['popularity_score'] = (
    anime_df['rating'] * np.log1p(anime_df['members'])
)
```
Skor popularitas dihitung sebagai hasil dari rating dikalikan logaritma dari jumlah `members`. Metrik ini menggabungkan kualitas (rating) dan kuantitas (jumlah pengguna) untuk menilai kepopuleran sebuah anime.

## Modeling and Results
1. Content-Based Filtering (TF-IDF + Cosine)
```python
cosine_sim = cosine_similarity(genre_matrix, genre_matrix)

def content_recommend(title, n=5):
    idx = anime_df[anime_df['name']==title].index[0]
    sim_scores = list(enumerate(cosine_sim[idx]))
    sim_scores = sorted(sim_scores, key=lambda x: x[1], reverse=True)
    return anime_df.iloc[[i[0] for i in sim_scores[1:n+1]]]
```
Menggunakan kemiripan genre antara anime untuk memberikan rekomendasi. Fungsi `content_recommend()` memberikan n anime yang paling mirip berdasarkan genre dengan judul tertentu. Outputnya adalah Top-N recommendation berdasarkan genre similarity.

Berikut adalah contoh hasil rekomendasi dari anime 'Naruto':
![image](https://github.com/user-attachments/assets/3227e483-9ef0-42c3-a361-2768b2abd558)

2. Collaborative Filtering dengan SVD (Matrix Factorization)
```python
reader = Reader(rating_scale=(1, 10))
data = Dataset.load_from_df(rating_df_clean[['user_id', 'anime_id', 'rating']], reader)

svd = SVD()
cross_val_results = cross_validate(svd, data, measures=['RMSE'], cv=3)
svd.fit(data.build_full_trainset())
```
Menggunakan model Singular Value Decomposition (SVD) dari library Surprise. Model dilatih pada data interaksi user-anime-rating. Outputnya adalah prediksi rating user terhadap anime yang belum ditonton.

| Aspek                | Content-Based (TF-IDF)                      | Collaborative Filtering (SVD)                   |
| -------------------- | ------------------------------------------- | ----------------------------------------------- |
| Berdasarkan          | Kesamaan konten (genre)                     | Pola rating dari user lain                      |
| Data yang Dibutuhkan | Metadata anime (genre)                      | Data interaksi user (rating)                    |
| Kelebihan            | Bisa digunakan untuk item baru | Menangkap preferensi tersembunyi antar pengguna |
| Kelemahan            | Tidak mempertimbangkan preferensi user yang lain | Tidak bisa bekerja tanpa data interaksi user yang cukup   |

Berikut adalah rekomendasi berdasarkan SVD dengan user id = 1:
![image](https://github.com/user-attachments/assets/2ad57b24-d57e-48ab-b1b1-bdd4ca1ce36b)

## Evaluation
RMSE (Root Mean Square Error) digunakan untuk mengevaluasi model Collaborative Filtering (SVD).
```python
cross_val_results = cross_validate(svd, data, measures=['RMSE'], cv=3)
```

$$
  \text{RMSE} = \sqrt{\frac{1}{n} \sum_{i=1}^{n} (y_i - \hat{y}_i)^2}
$$

RMSE mengukur rata-rata akar dari kuadrat kesalahan prediksi. Makin kecil nilai RMSE, makin baik model memprediksi rating sebenarnya. RMSE cocok untuk sistem rekomendasi ini. Dari hasil cross-validation, nilai RMSE yang diperoleh mencerminkan kemampuan model untuk memprediksi rating dengan cukup baik, meskipun dapat bervariasi tergantung data dan parameter model.
Hasil dari RMSE SVD adalah 1.1528

Sementara untuk Content-Based Filtering menggunakan Precision@K, Recall@K dan F1-Score tidak bisa terhitung dikarenakan data training tidak cukup untuk membentuk profil pengguna yang valid. Akan tetapi berikut adalah rumus perhitungannya:

Precision@K:
Mengukur proporsi item relevan di antara K item teratas yang direkomendasikan.

$$
\text{Precision@K} = \frac{|\text{Recommended}_K \cap \text{Relevant}|}{K}
$$

- `Recommended_K`: Daftar K item yang direkomendasikan oleh sistem.
- `Relevant`: Item yang relevan (misalnya, item dengan rating ≥ 4 dari pengguna).

Recall@K:

Mengukur proporsi item relevan yang berhasil ditemukan dari seluruh item relevan.

$$
\text{Recall@K} = \frac{|\text{Recommended}_K \cap \text{Relevant}|}{|\text{Relevant}|}
$$

F1-Score@K:

Mengukur keseimbangan antara Precision@K dan Recall@K.

$$
\text{F1@K} = 2 \times \frac{\text{Precision@K} \times \text{Recall@K}}{\text{Precision@K} + \text{Recall@K}}
$$
