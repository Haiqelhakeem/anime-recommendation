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

## Data Preparation

## Modeling

## Evaluation
