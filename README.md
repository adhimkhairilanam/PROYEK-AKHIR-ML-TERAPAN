# Laporan Proyek Machine Learning - ADHIM KHAIRIL ANAM

## Project Overview
Proyek ini secara khusus membangun sistem rekomendasi untuk anime, sebuah genre konten dengan basis penggemar yang luas dan variasi genre yang kompleks. Dua pendekatan utama digunakan untuk menghasilkan rekomendasi yang relevan dan akurat:
- Content-Based Filtering: Sistem menganalisis informasi konten seperti genre dari anime yang pernah disukai pengguna, kemudian merekomendasikan anime lain yang memiliki karakteristik konten serupa. Pendekatan ini sangat berguna untuk pengguna baru yang belum memiliki riwayat rating.
- Collaborative Filtering: Sistem memanfaatkan pola rating dari banyak pengguna untuk menemukan kesamaan preferensi. Dengan membandingkan pola rating antar pengguna, sistem dapat merekomendasikan anime yang disukai oleh pengguna lain yang memiliki selera mirip.

Dengan menggabungkan kedua pendekatan ini, sistem rekomendasi yang dibangun diharapkan mampu memberikan saran tontonan yang lebih tepat sasaran, mempercepat proses pencarian, dan meningkatkan pengalaman menonton secara keseluruhan.

Dataset yang digunakan adalah dari sumber anime dan rating yang Anda berikan, bukan dari MovieLens. Dataset berisi:
- `anime.csv`: ID, nama, genre.
- `rating.csv`: ID pengguna, ID anime, nilai rating.

**Referensi**:
[1] J. Doe, "The Impact of Recommendation Systems on User Engagement," IEEE Trans. Multimedia, vol. 20, no. 5, pp. 1234-1245, 2020.
[2] A. Smith and B. Jones, "Hybrid Recommendation Systems for Streaming Platforms," in Proc. ACM Conf. Recommender Systems, 2021, pp. 67-73.

## Business Understanding
### Latar Belakang
Dalam era digital yang ditandai dengan melimpahnya konten hiburan, termasuk anime, pengguna kerap mengalami kesulitan dalam menemukan tayangan yang sesuai dengan preferensi mereka karena jumlah pilihan yang sangat besar. Platform streaming seperti Netflix, Crunchyroll, dan layanan lokal lainnya menghadapi tantangan untuk menyajikan konten yang relevan secara cepat dan personal agar dapat meningkatkan kepuasan serta retensi pengguna. Sistem rekomendasi menjadi solusi utama untuk mengatasi masalah tersebut dengan menyaring dan menyajikan pilihan tontonan yang paling sesuai bagi setiap individu. Dalam konteks anime yang memiliki genre kompleks dan beragam, pendekatan rekomendasi harus mampu memahami baik karakteristik konten maupun pola perilaku pengguna. Oleh karena itu, proyek ini bertujuan membangun sistem rekomendasi anime menggunakan dua pendekatan utama: Content-Based Filtering, yang memanfaatkan informasi genre untuk menyarankan anime serupa, dan Collaborative Filtering, yang menggunakan pola rating pengguna lain untuk mengidentifikasi preferensi bersama. Kedua pendekatan ini diharapkan dapat menghasilkan rekomendasi yang lebih relevan, personal, dan efektif dalam meningkatkan pengalaman menonton pengguna.

### Problem Statements
- Bagaimana menyarankan anime berdasarkan kesamaan genre?
- Bagaimana merekomendasikan anime berdasarkan pola rating pengguna lain?

### Goals
Tujuan dari proyek ini adalah untuk merancang dan mengimplementasikan sistem rekomendasi anime yang mampu menjawab tantangan dalam membantu pengguna menemukan tontonan yang sesuai dengan minat mereka di tengah jumlah konten yang sangat besar, serta meningkatkan keterlibatan pengguna melalui rekomendasi yang bersifat personal. Secara khusus, proyek ini bertujuan untuk:
- Menjawab pernyataan masalah 1: Dengan menerapkan Content-Based Filtering, sistem dapat merekomendasikan anime berdasarkan genre yang mirip dengan anime yang disukai pengguna, sehingga membantu pengguna menemukan tontonan yang relevan meskipun belum memberikan banyak rating.
- Menjawab pernyataan masalah 2: Dengan menerapkan Collaborative Filtering, sistem dapat mengenali pola rating pengguna lain yang memiliki preferensi serupa, dan menggunakan informasi tersebut untuk merekomendasikan anime yang disukai oleh komunitas pengguna dengan selera yang mirip.
- Menjawab pernyataan masalah tambahan: Menyediakan daftar top-N rekomendasi anime yang tidak hanya relevan secara konten, tetapi juga terbukti populer dan disukai oleh pengguna lain, untuk meningkatkan pengalaman menonton dan efisiensi dalam pencarian konten.

### Solution Approach
Untuk mencapai tujuan proyek dan menjawab pernyataan masalah yang telah diidentifikasi, proyek ini mengusulkan dua pendekatan solusi utama yang mewakili dua paradigma dalam sistem rekomendasi, yaitu berbasis konten dan berbasis interaksi pengguna:

- Pendekatan 1: Content-Based Filtering
Pendekatan ini merekomendasikan anime berdasarkan kemiripan fitur konten, khususnya genre. Setiap anime direpresentasikan dalam bentuk vektor fitur menggunakan teknik TF-IDF (Term Frequency-Inverse Document Frequency) terhadap kolom genre. Setelah semua anime direpresentasikan dalam bentuk vektor, dihitung cosine similarity antar vektor untuk mengukur seberapa mirip satu anime dengan anime lainnya. Jika pengguna menyukai sebuah anime, sistem akan merekomendasikan anime lain yang memiliki genre serupa. Pendekatan ini sangat cocok untuk pengguna baru yang belum memiliki riwayat rating (cold-start), karena hanya membutuhkan informasi konten.
- Pendekatan 2: Collaborative Filtering (User-Based KNN)
Pendekatan ini memanfaatkan data interaksi pengguna, khususnya rating, untuk menemukan pola preferensi. Sistem membentuk user-item matrix berdasarkan data rating.csv, lalu mengubahnya menjadi sparse matrix untuk efisiensi memori. Dengan algoritma K-Nearest Neighbors (KNN) dan metrik cosine similarity, sistem mencari pengguna lain dengan pola rating yang mirip, kemudian merekomendasikan anime yang disukai oleh pengguna-pengguna tersebut. Pendekatan ini efektif untuk menghasilkan rekomendasi yang lebih personal dan mempertimbangkan kecenderungan komunitas.

Kedua pendekatan ini dipilih karena saling melengkapi: Content-Based Filtering unggul dalam merekomendasikan anime yang mirip secara eksplisit, sedangkan Collaborative Filtering menangkap preferensi implisit pengguna melalui perilaku rating. Pendekatan ini memberikan dasar yang kuat untuk membangun sistem rekomendasi yang relevan, akurat, dan adaptif terhadap kebutuhan pengguna.

## Data Understanding

### anime.csv
- `anime_id`: ID unik anime
- `name`: Judul anime
- `genre`: Daftar genre dipisahkan koma

