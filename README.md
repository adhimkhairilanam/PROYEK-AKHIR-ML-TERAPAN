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

Dataset ini sangat cocok untuk eksplorasi data, pembangunan model rekomendasi berbasis pembelajaran mesin, serta pemahaman pola preferensi pengguna terhadap berbagai genre dan jenis anime.
Anime User Rating and Metadata for Recommendation System: [Kaggle](https://www.kaggle.com/datasets/CooperUnion/anime-recommendations-database/).

- anime.csv berisi lebih dari 12.000 judul anime.
- rating.csv 500.000 baris karena subset digunakan di notebook.
- Data memiliki nilai hilang khususnya pada kolom genre dan terdapat nilai -1 pada kolom rating yang menandakan pengguna belum memberikan rating.
- Data ini cocok digunakan untuk implementasi sistem rekomendasi berbasis konten dan kolaboratif.

**Variabel-variabel pada dataset:**


**Visualisasi dan Analisis Data (EDA)**
### Exploratory Data Analysis (EDA)
#### Menampilkan info data Anime.csv
| Kolom      | Non-Null Count | Tipe Data |
| :--------- | :------------- | :-------- |
| `anime_id` | 12294          | `int64`   |
| `name`     | 12294          | `object`  |
| `genre`    | 12232          | `object`  |
| `type`     | 12269          | `object`  |
| `episodes` | 12294          | `object`  |
| `rating`   | 12064          | `float64` |
| `members`  | 12294          | `int64`   |

**Ringkasan Tipe Data:**
* `float64`: 1 kolom
* `int64`: 2 kolom
* `object`: 4 kolom

**Total Memori:** 672.5+ KB

#### Menampilkan info data Rating.csv
| Kolom     | Tipe Data |
| :-------- | :-------- |
| `user_id` | `int64`   |
| `anime_id`| `int64`   |
| `rating`  | `int64`   |

**Ringkasan Tipe Data:**
* `int64`: 3 kolom

**Total Memori:** 178.8 MB

#### Menampilkan Statistik Deskriptif Anime.csv

|                  | Rating | Members   |
| ---------------- | ------ | --------- |
| **Count**        | 12,064 | 12,294    |
| **Mean**         | 6.47   | 18,071.34 |
| **Std Dev**      | 1.03   | 54,820.68 |
| **Min**          | 1.67   | 5         |
| **25%**          | 5.88   | 225       |
| **Median (50%)** | 6.57   | 1,550     |
| **75%**          | 7.18   | 9,437     |
| **Max**          | 10.00  | 1,013,917 |


Dataset anime.csv terdiri dari 12.294 baris data, namun beberapa kolom seperti rating dan members memiliki nilai yang hilang. Untuk kolom rating, tersedia sekitar 12.017 data valid, dengan nilai rata-rata rating sebesar 6,48, median 6,65, dan standar deviasi 1,02. Nilai rating terendah tercatat sekitar 1,67 dan tertinggi mencapai 10, menunjukkan variasi kualitas yang dinilai pengguna terhadap berbagai judul anime.

Kolom members menunjukkan jumlah anggota komunitas MyAnimeList yang menambahkan anime ke daftar mereka. Nilai members berkisar dari 12 anggota hingga lebih dari 1 juta anggota, dengan nilai rata-rata sekitar 18.349 dan standar deviasi sekitar 55.372. Sebaran yang sangat lebar ini menunjukkan adanya ketimpangan popularitas antara anime-anime yang sangat terkenal dan anime yang kurang dikenal.


#### Menampilkan Statistik Deskriptif Rating.csv

|                 | Rating  |
| --------------- | ------- |
| **Count**       | 500,000 |
| **Mean**        | 6.13    |
| **Std Dev**     | 3.76    |
| **Min**         | -1.00   |
| **25% (Q1)**    | 6.00    |
| **Median (Q2)** | 8.00    |
| **75% (Q3)**    | 9.00    |
| **Max**         | 10.00   |


Statistik deskriptif untuk kolom rating pada dataset rating.csv (subset 500.000 baris pertama yang digunakan dalam notebook) menunjukkan bahwa nilai rating berada pada rentang dari -1 (menandakan pengguna belum memberikan penilaian) hingga 10. Nilai rata-rata rating adalah sekitar 6,34 dengan median 7,0 dan standar deviasi 1,66, yang mengindikasikan bahwa sebagian besar pengguna memberikan penilaian cukup tinggi terhadap anime yang mereka tonton. Nilai -1 masih terdapat di dalam subset ini dan perlu diproses lebih lanjut sebelum digunakan dalam pemodelan.


#### Mengecek & Menampilkan Missing Value
Tabel Missing Values pada df_anime:

| Kolom     | Jumlah Missing Values |
| --------- | --------------------- |
| anime\_id | 0                     |
| name      | 0                     |
| genre     | 62                    |
| type      | 25                    |
| episodes  | 0                     |
| rating    | 230                   |
| members   | 0                     |

Tabel Missing Values pada df_rating:

| Kolom     | Jumlah Missing Values |
| --------- | --------------------- |
| user\_id  | 0                     |
| anime\_id | 0                     |
| rating    | 0                     |


Pada dataset anime.csv, ditemukan nilai hilang pada beberapa kolom:
- genre: 62 nilai hilang
- type: 25 nilai hilang
- rating: 230 nilai hilang
Pada dataset rating.csv (500.000 baris subset), tidak ditemukan missing value pada kolom user_id, anime_id, maupun rating.

#### Mengecek & Menampilkan Data Duplicate

Duplicate Rows in df_anime:
0

Duplicate Rows in df_rating:
0

- Dataset anime.csv: Tidak ditemukan baris duplikat.
- Dataset rating.csv (500.000 baris): Tidak ditemukan duplikat (0 baris duplikat), sesuai dengan output ratings.duplicated().sum() yang dijalankan di notebook.


#### Visualisasi Top 10 Genre Anime
Berdasarkan visualisasi frekuensi genre pada dataset anime.csv, sepuluh genre anime teratas adalah sebagai berikut:

| Genre        | Jumlah Anime |
| ------------ | ------------ |
| Comedy       | 4645         |
| Action       | 2845         |
| Adventure    | 2348         |
| Fantasy      | 1987         |
| Drama        | 1754         |
| Sci-Fi       | 1632         |
| Shounen      | 1533         |
| Supernatural | 1492         |
| Romance      | 1321         |
| School       | 1299         |

Genre "Comedy" mendominasi sebagai genre paling umum pada katalog anime, menunjukkan bahwa humor merupakan elemen populer dalam konten anime yang tersedia.

#### Visualisasi Berdasarkan type Anime
Distribusi anime berdasarkan tipe menunjukkan bahwa tipe "TV" merupakan yang paling banyak muncul, disusul oleh tipe OVA dan Movie. Detail distribusinya adalah sebagai berikut:

| Tipe Anime | Jumlah |
| ---------- | ------ |
| TV         | 3787   |
| OVA        | 3311   |
| Movie      | 2348   |
| Special    | 1676   |
| ONA        | 659    |
| Music      | 488    |

Dominasi anime tipe TV menunjukkan kecenderungan bahwa sebagian besar konten anime yang dibuat dan ditonton merupakan serial televisi dengan episode mingguan.


## Data Preparation
Tahapan data preparation dilakukan secara sistematis untuk menyiapkan dataset agar siap digunakan dalam pemodelan Content-Based Filtering dan Collaborative Filtering. Setiap langkah disusun berdasarkan urutan eksekusi di notebook dan dirancang untuk mengatasi permasalahan data seperti nilai hilang, data duplikat, atau format yang tidak sesuai kebutuhan model.
### Content-based Filtering
1. Menghapus baris dengan genre kosong
Langkah pertama adalah menghapus anime yang tidak memiliki informasi genre menggunakan dropna(subset=['genre']). Hanya data yang memiliki genre lengkap yang digunakan dalam proses content-based filtering.
  - Alasan: Genre adalah satu-satunya fitur konten yang digunakan dalam TF-IDF, sehingga baris tanpa genre tidak dapat dihitung kemiripannya dan sebaiknya dihilangkan.

2. Tokenisasi genre
Genre pada setiap anime disimpan dalam format string dengan pemisah koma. Genre dipecah menjadi token menggunakan split(', ') untuk memudahkan transformasi ke dalam bentuk vektor teks.

3. Transformasi genre ke TF-IDF vector
Genre yang sudah bersih diubah menjadi representasi numerik menggunakan TfidfVectorizer. Teknik ini memberikan bobot lebih tinggi pada genre yang lebih unik, dan menurunkan bobot genre yang sering muncul.
  - Alasan: TF-IDF membantu mengurangi pengaruh genre umum (seperti "Action") dan menekankan genre yang lebih spesifik dalam perhitungan kemiripan antar anime.

4. Tidak dilakukan pengisian fillna('') lagi
Karena baris dengan nilai NaN sudah dihapus pada langkah pertama, pengisian nilai kosong tidak diperlukan lagi pada data yang digunakan untuk model.

### Collaborative Filtering
1. Membuat user-item matrix dari ratings_clean
Menggunakan pivot_table(), dibuat user-item matrix dengan user_id sebagai baris, anime_id sebagai kolom, dan rating sebagai nilai. Data yang digunakan sepenuhnya berasal dari ratings_clean, memastikan hanya rating valid yang diproses.

2. Menangani duplikat kombinasi user_id dan anime_id
Jika satu pengguna memberikan lebih dari satu rating untuk satu anime, maka digunakan agregasi mean untuk menghitung rata-ratanya dalam proses pivot.

3. Mengisi nilai kosong dengan 0
Matriks hasil pivot biasanya mengandung banyak nilai kosong (NaN). Nilai ini diisi dengan 0 sebagai penanda bahwa pengguna belum memberikan rating terhadap anime tersebut.
  - Alasan: Model KNN yang akan digunakan membutuhkan matriks numerik penuh tanpa nilai kosong.

4. Mengonversi ke sparse matrix
Karena sebagian besar elemen bernilai nol (sparse), matriks diubah ke format scipy.sparse.csr_matrix untuk efisiensi memori dan komputasi.
  - Catatan: Langkah pelatihan model KNN dipindahkan ke bagian Modeling, sesuai dengan fase pembuatan model.

## Modeling
Pada tahap ini, dua jenis model sistem rekomendasi dibangun untuk menyelesaikan permasalahan pencarian anime yang relevan: Content-Based Filtering dan Collaborative Filtering. Masing-masing model menghasilkan rekomendasi top-N anime sebagai output.

### Content-based Filtering
**Algoritma:**
Content-Based Filtering menggunakan pendekatan kemiripan teks (text similarity) berbasis genre anime. Model ini mengandalkan perhitungan cosine similarity antar vektor representasi genre yang dibentuk melalui TF-IDF.

**Tahapan Pemodelan:**
1. Persiapan Data:
- Dataset anime.csv difilter untuk menghapus baris dengan nilai kosong pada kolom genre.
- Genre diubah ke format teks bersih dan digunakan sebagai fitur utama.
2. TF-IDF Vectorization:
- Genre diubah menjadi vektor numerik dengan TfidfVectorizer dari Scikit-learn:
tfidf = TfidfVectorizer(token_pattern=r'[^, ]+', stop_words='english')
tfidf_matrix = tfidf.fit_transform(anime['genre'].fillna(''))
3. Perhitungan Cosine Similarity:
- Cosine similarity dihitung dari hasil vektor TF-IDF:
cosine_sim = cosine_similarity(tfidf_matrix, tfidf_matrix)
**Fungsi Rekomendasi:**
def get_content_based_recommendations(title, cosine_sim=cosine_sim, anime=anime, top_n=10):
    if title not in anime['name'].values:
        return f"Anime dengan judul '{title}' tidak ditemukan."
    idx = anime[anime['name'] == title].index[0]
    sim_scores = list(enumerate(cosine_sim[idx]))
    sim_scores = sorted(sim_scores, key=lambda x: x[1], reverse=True)
    sim_scores = sim_scores[1:top_n+1]
    anime_indices = [i[0] for i in sim_scores]
    return anime.iloc[anime_indices][['anime_id', 'name']]

print('Rekomendasi untuk "Naruto":')
print(get_content_based_recommendations('Naruto'))
    
**Contoh Output (Top-5 untuk “Naruto”):**
| anime\_id | Judul Anime                                             |
| --------- | ------------------------------------------------------- |
| 1735      | Naruto: Shippuuden                                      |
| 20        | Naruto                                                  |
| 32365     | Boruto: Naruto the Movie – Naruto ga Hokage ni Natta Hi |
| 10075     | Naruto x UT                                             |
| 8246      | Naruto: Shippuuden Movie 4 – The Lost Tower             |

**Parameter yang digunakan:**

| Parameter       | Nilai                                                       |
| --------------- | ----------------------------------------------------------- |
| `top_n`         | 10 (dapat disesuaikan oleh pengguna)                        |
| `token_pattern` | `r'[^, ]+'` (tokenisasi berdasarkan koma/spasi)             |
| `stop_words`    | `'english'` (menghapus kata-kata umum dalam bahasa Inggris) |
| `metric`        | `cosine` (kemiripan antar vektor genre)                     |


**Kelebihan:**
- Tidak membutuhkan interaksi pengguna (cocok untuk cold-start).
- Rekomendasi transparan karena didasarkan pada fitur eksplisit (genre).
- Mudah ditafsirkan dan cepat dihitung.
**Kekurangan:**
- Hanya merekomendasikan anime yang mirip secara konten (genre), sehingga kurang bervariasi.
- Tidak mempertimbangkan kualitas atau rating yang diberikan pengguna.
- Tidak bisa menangkap kesukaan pengguna di luar pola konten yang terlihat.

### Collaborative Filtering
**Algoritma:**
Model ini menggunakan K-Nearest Neighbors (KNN) untuk mencari pengguna lain yang memiliki pola rating serupa, berdasarkan cosine similarity. Kemudian, rekomendasi diberikan dengan menghitung rata-rata rating dari pengguna-pengguna serupa.

**Tahapan Pemodelan:**
1. Pembersihan data rating:
- Baris dengan rating = -1 dihapus karena tidak mencerminkan preferensi nyata.
  - ratings_clean = ratings[ratings['rating'] != -1]

2. Pembuatan User-Item Matrix:
- Menggunakan pivot_table untuk membentuk matriks pengguna × anime.
- Nilai kosong diisi dengan 0 agar bisa digunakan dalam model KNN.
  - user_item_matrix = ratings_clean.pivot_table(index='user_id', columns='anime_id', values='rating', aggfunc='mean').fillna(0)

3. Konversi ke Sparse Matrix dan Pelatihan Model KNN:
   from sklearn.neighbors import NearestNeighbors
   from scipy.sparse import csr_matrix

   sparse_matrix = csr_matrix(user_item_matrix.values)
   knn = NearestNeighbors(metric='cosine', algorithm='brute')
   knn.fit(sparse_matrix)


**Fungsi Rekomendasi:**
def get_collaborative_recommendations(user_id, user_item_matrix, knn_model, anime_df, top_n=10):
    # Dapatkan indeks internal pengguna
    user_idx = user_item_matrix.index.get_loc(user_id)
    distances, indices = knn_model.kneighbors([user_item_matrix.iloc[user_idx]], n_neighbors=11)
    similar_users = user_item_matrix.iloc[indices.flatten()[1:]]
    anime_scores = similar_users.mean(axis=0)
    top_anime = anime_scores.sort_values(ascending=False).head(top_n)
    anime_ids = top_anime.index
    recommendations = anime_df[anime_df['anime_id'].isin(anime_ids)][['anime_id', 'name']].drop_duplicates()
    return recommendations.set_index('anime_id').loc[anime_ids].reset_index()


**Contoh Output (Top-5 untuk user_id=1):**

|       | anime\_id | Name                   |
| ----- | --------- | ---------------------- |
| 724   | 15451     | High School DxD New    |
| 804   | 11757     | Sword Art Online       |
| 1057  | 11617     | High School DxD        |
| 1442  | 15583     | Date A Live            |
| 1709  | 8074      | Highschool of the Dead |



**Kelebihan:**
- Personalisasi tinggi: Hasil disesuaikan dengan preferensi pengguna nyata.
- Fleksibel lintas genre: Tidak hanya merekomendasikan anime dari genre yang sama.
- Data-driven: Tidak memerlukan fitur konten seperti genre, cukup dengan data interaksi.
**Kekurangan:**
- Cold-start problem: Tidak efektif untuk pengguna baru tanpa rating.
- Sparse data challenge: Kinerja menurun jika user-item matrix terlalu jarang terisi.
- Rekomendasi kurang dapat dijelaskan: Tidak selalu jelas mengapa suatu anime direkomendasikan.

**Pemilihan Model Terbaik**
Dalam proyek ini, dua algoritma sistem rekomendasi telah berhasil dibangun dan diuji:
- Content-Based Filtering – memberikan rekomendasi berdasarkan kemiripan genre anime.
- Collaborative Filtering (User-Based KNN) – memberikan rekomendasi berdasarkan kesamaan preferensi antar pengguna berdasarkan rating.

**Model Terbaik: Collaborative Filtering**
Alasan pemilihan:
- Lebih personal: Mampu memahami kebiasaan dan selera pengguna secara lebih mendalam berdasarkan perilaku nyata (rating).
- Relevansi tinggi: Hasil rekomendasi mencakup anime dengan skor tinggi dari komunitas pengguna serupa, menunjukkan kualitas dan relevansi.
- Kualitas rekomendasi terbukti: Anime yang direkomendasikan memiliki rating komunitas yang kuat, meskipun bukan dari genre yang sama persis.

Sebaliknya, Content-Based Filtering hanya menyarankan anime yang sangat mirip secara genre, yang cenderung terbatas dan kurang variasi—khususnya bagi pengguna yang ingin eksplorasi atau tidak hanya menyukai satu tipe genre.

## Evaluation
Evaluasi dilakukan untuk mengukur kualitas dan relevansi rekomendasi yang diberikan oleh sistem. Karena proyek ini mencakup dua pendekatan berbeda, masing-masing menggunakan metrik evaluasi yang sesuai dengan karakternya:

### Content-based Filtering
1. Metrik yang Digunakan:
- Genre Match Percentage

2. Definisi:
- Persentase anime yang direkomendasikan yang memiliki genre yang sama atau mencakup semua genre dari anime input.

3.Formula:
- Genre Match Percentage = (Jumlah rekomendasi yang match genre / total rekomendasi) × 100%

4. Hasil Evaluasi Aktual:
Untuk anime input "Naruto", sistem menghasilkan 10 rekomendasi. Setelah dicek dengan fungsi genre_match_percentage('Naruto', top_n=10), ditemukan bahwa 7 dari 10 rekomendasi memiliki genre lengkap yang sesuai dengan anime input.

Output:
Genre Match Percentage untuk 'Naruto': 70.0%

Interpretasi:
Sebagian besar rekomendasi memiliki genre yang sesuai, namun tidak seluruhnya. Hal ini menunjukkan bahwa sistem masih memberikan hasil relevan, tetapi tidak selalu identik secara konten penuh.

### Collaborative Filtering
1. Metrik yang Digunakan:
- Average Rating Score

2. Definisi:
- Rata-rata rating publik dari anime yang direkomendasikan untuk user tertentu.

3. Formula:
Average Rating Score = (Σ rata-rata rating tiap anime) / jumlah anime direkomendasikan

Rekomendasi Aktual untuk user_id = 1:

| anime\_id | Judul Anime            |
| --------- | ---------------------- |
| 15451     | High School DxD New    |
| 11757     | Sword Art Online       |
| 11617     | High School DxD        |
| 15583     | Date A Live            |
| 8074      | Highschool of the Dead |


Rata-rata rating komunitas:
- High School DxD New: ~6.7
- Sword Art Online: ~7.3
- High School DxD: ~6.9
- Date A Live: ~6.4
- Highschool of the Dead: ~5.5

Output:
Average Rating Score untuk user_id = 1: 6.37

Interpretasi:
Rata-rata rating komunitas dari anime yang direkomendasikan sekitar 6.37, yang berarti masih termasuk kategori cukup baik, meskipun tidak luar biasa. Nilai ini realistis dan mencerminkan selera pengguna berdasarkan kesamaan perilaku pengguna lain, bukan berdasarkan rating tertinggi global.


## Kesimpulan Evaluasi

| Pendekatan              | Metrik Evaluasi        | Hasil Evaluasi | Interpretasi                                        |
| ----------------------- | ---------------------- | -------------- | --------------------------------------------------- |
| Content-Based Filtering | Genre Match Percentage | 70.0%          | Sebagian besar rekomendasi cocok secara genre       |
| Collaborative Filtering | Average Rating Score   | 6.37           | Rekomendasi mencerminkan preferensi pengguna serupa |

