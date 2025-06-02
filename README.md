# Laporan Proyek Machine Learning - Labiba Adinda Zahwana

## Project Overview
Sistem rekomendasi telah menjadi komponen penting dalam kehidupan digital modern, membantu pengguna menemukan informasi yang relevan dan personal di tengah banyaknya pilihan yang tersedia. Dalam konteks pariwisata di Indonesia, khususnya Kota Surabaya, keberagaman destinasi wisata menawarkan peluang besar untuk meningkatkan pengalaman wisatawan. Namun, wisatawan sering menghadapi kesulitan dalam menemukan destinasi yang sesuai dengan preferensi pribadi mereka karena tersebarnya informasi dan banyaknya pilihan yang ada. Kondisi ini dapat menyebabkan penurunan kepuasan berwisata dan potensi kunjungan ke destinasi tertentu menjadi kurang optimal.

Permasalahan ini perlu segera diatasi dengan pengembangan sistem rekomendasi destinasi wisata yang cerdas dan personal. Sistem ini bertujuan untuk memberikan rekomendasi destinasi yang relevan berdasarkan preferensi pengguna dan karakteristik destinasi, sekaligus mengenalkan destinasi wisata yang kurang populer namun memiliki potensi menarik. Pendekatan ini tidak hanya meningkatkan kemudahan dalam perencanaan perjalanan wisatawan, tetapi juga mendukung pengembangan sektor pariwisata di Surabaya secara berkelanjutan.

Berdasarkan penelitian oleh Chalkiadakis et al. (2023), penggunaan sistem rekomendasi dalam bidang pariwisata dapat meningkatkan efisiensi pencarian destinasi dan meningkatkan kepuasan pengguna secara signifikan. Selain itu, studi oleh Chanrueang et al. (2024) menunjukkan bahwa integrasi metode Collaborative Filtering dan Content-Based Filtering mampu menghasilkan rekomendasi yang lebih akurat dan personal di sektor wisata. Oleh karena itu, proyek ini mengadopsi pendekatan gabungan tersebut untuk mengatasi tantangan dalam memberikan rekomendasi destinasi wisata yang optimal.

---

## Referensi

* Chalkiadakis, G., Ziogas, I., Koutsmanis, M., Streviniotis, E., Panagiotakis, C., & Papadakis, H. (2023). A Novel Hybrid Recommender System for the Tourism Domain. *Algorithms*, 16(4), 215. [https://doi.org/10.3390/a16040215](https://doi.org/10.3390/a16040215)

* Chanrueang, S., Thammaboosadee, S., & Yu, H. (2024). A Personalized Hybrid Tourist Destination Recommendation System: An Integration of Emotion and Sentiment Approach. *International Journal of Advanced Computer Science and Applications*, 15(8), 18-24. [https://doi.org/10.14569/IJACSA.2024.0150803](https://doi.org/10.14569/IJACSA.2024.0150803)

---

## Business Understanding

Pada bagian ini, dilakukan klarifikasi masalah yang ingin diselesaikan dalam proyek sistem rekomendasi destinasi wisata di Surabaya. Pemahaman yang jelas terhadap masalah akan membantu dalam menentukan tujuan dan pendekatan solusi yang tepat.

### Problem Statements
* Bagaimana sistem dapat merekomendasikan destinasi wisata yang sesuai dengan preferensi unik tiap pengguna di Surabaya?

* Bagaimana sistem dapat mengenali dan merekomendasikan destinasi wisata yang belum pernah diketahui atau dikunjungi pengguna, sehingga meningkatkan peluang eksplorasi destinasi baru?

* Bagaimana mengatasi keterbatasan data pengguna baru (cold start problem) dalam sistem rekomendasi?

* Bagaimana memastikan rekomendasi yang diberikan relevan dan akurat sehingga meningkatkan kepuasan pengguna dalam memilih destinasi wisata di Surabaya?


### Goals

Tujuan dari proyek ini antara lain:

* Mengembangkan sistem rekomendasi destinasi wisata yang memberikan saran berdasarkan kemiripan antar destinasi (content-based filtering).
* Mengembangkan sistem rekomendasi yang memberikan saran destinasi berdasarkan preferensi dan perilaku pengguna lain yang serupa (collaborative filtering).
* Menghasilkan rekomendasi destinasi wisata yang personal dan relevan untuk tiap pengguna.
* Melakukan evaluasi terhadap sistem rekomendasi menggunakan metrik yang sesuai untuk memastikan kualitas, akurasi, dan relevansi hasil yang diberikan. 

### Solution Statements

* Menerapkan pendekatan **content-based filtering** dengan menggunakan representasi fitur destinasi (seperti kategori, lokasi, dan rating) serta perhitungan kemiripan menggunakan cosine similarity untuk menyarankan destinasi yang serupa dengan yang sudah disukai pengguna.
* Menggunakan pendekatan **collaborative filtering** berbasis user-item interaction, memanfaatkan data rating historis pengguna terhadap destinasi untuk mempelajari preferensi dan merekomendasikan destinasi yang disukai oleh pengguna dengan profil serupa.
* Menerapkan metrik evaluasi yang sesuai seperti **Root Mean Squared Error (RMSE)** untuk mengukur akurasi prediksi rating pada collaborative filtering dan untuk menilai kualitas rekomendasi top-N pada content-based filtering, guna memastikan efektivitas dan relevansi sistem rekomendasi.

## Data Understanding
<p align='center'>
  <table>
    <thead>
      <tr>
        <th>Jenis</th>
        <th>Keterangan</th>
      </tr>
    </thead>
    <tbody>
      <tr>
        <td>Title</td>
        <td>Indonesian Tourism Destination</td>
      </tr>
      <tr>
        <td>Source</td>
        <td><a href="https://www.kaggle.com/datasets/aprabowo/indonesia-tourism-destination/data" target="_blank" rel="noopener noreferrer">Kaggle</a></td>
      </tr>
      <tr>
        <td>License</td>
        <td>Database: Open Database, Contents: Database Contents</td>
      </tr>
      <tr>
        <td>Visibility</td>
        <td>Publik</td>
      </tr>
    </tbody>
  </table>
</p>

Dataset yang digunakan dalam proyek ini merupakan kumpulan data terkait destinasi wisata di lima kota besar di Indonesia, yaitu Jakarta, Yogyakarta, Semarang, Bandung, dan Surabaya. Dataset ini berisi informasi mengenai berbagai tempat wisata, preferensi pengguna, serta penilaian (rating) yang diberikan oleh pengguna terhadap tempat-tempat wisata tersebut. Total terdapat sekitar 400 destinasi wisata yang terdata, dengan data penilaian mencapai 10.000 entri dan data pengguna sebanyak 300 entri. Dataset ini bersifat publik dan dapat diakses melalui [Kaggle - Indonesian Tourism Destination](https://www.kaggle.com/datasets/aprabowo/indonesia-tourism-destination/data).

Dalam tahap Data Understanding, dilakukan pengecekan kondisi dataset seperti ukuran data, tipe data, nilai kosong (missing values), dan duplikasi. Hal ini bertujuan untuk mengetahui permasalahan yang ada pada data sehingga pada tahap Data Preprocessing dapat dilakukan pembersihan (cleaning) data dengan tepat, sehingga data menjadi bersih dan siap digunakan dalam pengembangan sistem rekomendasi.

Variabel-variabel penting dalam dataset ini antara lain:

* **Place\_Id**: ID unik untuk setiap destinasi wisata.
* **Place\_Name**: Nama destinasi wisata.
* **Description**: Deskripsi singkat tentang destinasi wisata.
* **Category**: Kategori destinasi (misalnya Budaya, Taman Hiburan, Bahari).
* **City**: Kota tempat destinasi berada.
* **Price**: Harga tiket masuk ke destinasi wisata.
* **Rating**: Rating rata-rata destinasi berdasarkan ulasan pengguna.
* **Time\_Minutes**: Perkiraan waktu yang dibutuhkan untuk mengunjungi destinasi.
* **User\_Id**: ID unik pengguna yang memberikan rating.
* **Place\_Ratings**: Nilai rating yang diberikan pengguna pada destinasi wisata.

Dataset terdiri dari empat file utama:

* `tourism_with_id.csv`: berisi data detail objek wisata sebanyak sekitar 400 tempat, mencakup nama, kategori, kota, harga tiket, rating, dan koordinat.
* `user.csv`: berisi data dummy pengguna yang digunakan untuk fitur rekomendasi berbasis preferensi.
* `tourism_rating.csv`: berisi data rating pengguna terhadap objek wisata, yang digunakan untuk membangun sistem rekomendasi berbasis interaksi.
* `package_tourism.csv`: berisi rekomendasi paket wisata berdasarkan waktu, biaya, dan rating.

Dataset `tourism_with_id.csv` memiliki 437 baris dan 13 kolom, di antaranya:

* `Place_Id`: ID unik tempat wisata.
* `Place_Name`: Nama tempat wisata.
* `Description`: Deskripsi singkat tempat wisata.
* `Category`: Kategori objek wisata (misal Budaya, Taman Hiburan, Bahari, dll).
* `City`: Kota tempat wisata berada.
* `Price`: Harga tiket masuk.
* `Rating`: Rating rata-rata dari pengunjung.
* `Time_Minutes`: Estimasi waktu kunjungan (banyak data kosong).
* `Coordinate`, `Lat`, `Long`: Koordinat geografis tempat wisata.

Dataset `tourism_rating.csv` berisi 10.000 entri dengan kolom:

* `User_Id`: ID pengguna.
* `Place_Id`: ID tempat wisata.
* `Place_Ratings`: Nilai rating yang diberikan pengguna.

Dataset `user.csv` berisi 300 pengguna dengan kolom:

* `User_Id`: ID pengguna.
* `Location`: Lokasi pengguna.
* `Age`: Usia pengguna.

Kondisi Data

* Tidak ditemukan missing value pada dataset `tourism_rating` dan `user`.
* Pada `tourism_with_id`, terdapat missing value pada kolom `Time_Minutes` sebanyak 232 baris dan kolom `Unnamed: 11` seluruhnya kosong (437 baris). Kolom ini akan dihapus pada tahap data preparation karena tidak digunakan.
* Ditemukan 79 duplikat pada dataset `tourism_rating`, yang akan dihapus pada proses pembersihan data.
* Tidak ada duplikat pada dataset `tourism_with_id` dan `user`.

Statistik Singkat Data

| Dataset               | Jumlah Baris | Jumlah Kolom |
| --------------------- | ------------ | ------------ |
| tourism\_with\_id.csv | 437          | 13           |
| tourism\_rating.csv   | 10,000       | 3            |
| user.csv              | 300          | 3            |

Variasi Kategori Wisata di `tourism_with_id.csv`

Kategori wisata yang tersedia antara lain:

* Budaya
* Taman Hiburan
* Cagar Alam
* Bahari
* Pusat Perbelanjaan
* Tempat Ibadah
<br>
<br>
**Exploratory Data Analysis (EDA)**
<br>
<br>
    <p align='center'><img src="https://raw.githubusercontent.com/labibaadinda/surabaya-tourism-destination-recommendation-system/main/img/jumlah_rating.png" alt="jumlah rating" width="400" />
    </p>
<p align='center'>Gambar 1. Tempat dengan Rating terbanyak</p>
<br>

<br>
    <p align='center'><img src="https://raw.githubusercontent.com/labibaadinda/surabaya-tourism-destination-recommendation-system/main/img/jumlah_kategori.png" alt="jumlah kategori" width="400" />
    </p>
<p align='center'>Gambar 2. Perbandingan jumlah kategori  wisata</p>
<br>

<br>
    <p align='center'><img src="https://raw.githubusercontent.com/labibaadinda/surabaya-tourism-destination-recommendation-system/main/img/distribusi_usia.png" alt="distribusi usia" width="400" />
    </p>
<p align='center'>Gambar 3. Distribusi Usia</p>
<br>

<br>
    <p align='center'><img src="https://raw.githubusercontent.com/labibaadinda/surabaya-tourism-destination-recommendation-system/main/img/distribusi_harga.png" alt="distribusi harga" width="400" />
    </p>
<p align='center'>Gambar 4. Distribusi harga masuk tempat wisata</p>
<br>

<br>
    <p align='center'><img src="https://raw.githubusercontent.com/labibaadinda/surabaya-tourism-destination-recommendation-system/main/img/asal_kota.png" alt="jumlah asal kota" width="400" />
    </p>
<p align='center'>Gambar 5. Jumlah asal kota</p>
<br>

Hasil analisis EDA :

- Tempat paling banyak pengunjung di Surabaya Gereja Perawan Maria Tak Berdosa Surabaya.
- Jumlah kategori wisata di Kota Surabaya terbanyak yaitu budaya dan taman hiburan.
- Distribusi usia sekitar 23-34 tahun.
- Distribusi Harga Masuk Wisata di Kota Surabaya sekitar 0-20000, namun ada beberapa outlier / harga diluar range tsb.
- Asal kota dari User terbanyak ada di Kota Bekasi.

## Data Preparation
Tahapan ini bertujuan untuk mempersiapkan dan membersihkan data agar siap digunakan dalam pengembangan sistem rekomendasi.

1. **Pembersihan dan Penghapusan Data Duplikat**

   Dataset `tourism_rating` ditemukan mengandung data duplikat sebanyak 79 baris. Duplikasi ini dihapus agar data tidak bias saat pelatihan model.

   ```python
   data_tourism_rating.drop_duplicates(inplace=True)
   ```

2. **Penanganan Missing Values**

   Dataset `tourism_with_id` memiliki kolom `Unnamed: 11` dan `Time_Minutes` dengan nilai kosong (missing values). Kolom `Unnamed: 11` seluruhnya kosong dan kolom `Time_Minutes` memiliki banyak nilai kosong sehingga kedua kolom tersebut dihapus karena tidak relevan untuk proses rekomendasi.

   ```python
   data_tourism_with_id.drop(columns=['Unnamed: 11', 'Time_Minutes'], inplace=True)
   ```

3. **Pembuatan Fungsi Preprocessing Teks**

   Untuk menyederhanakan dan menormalkan data teks dari kolom `Description` dan `Category`, dibuat fungsi preprocessing yang melakukan:

   * Konversi teks menjadi huruf kecil (lowercase)
   * Stemming (mengubah kata ke bentuk dasar)
   * Menghapus stopword (kata-kata umum yang tidak membawa makna penting)

   ```python
   stem = StemmerFactory().create_stemmer()
   stopword = StopWordRemoverFactory().create_stop_word_remover()

   def preprocessing(text):
       text = text.lower()
       text = stem.stem(text)
       text = stopword.remove(text)
       return text
   ```

4. **Penggabungan dan Pembersihan Kolom untuk Content-Based Filtering**

   Dibuat kolom baru `Tags` dengan menggabungkan kolom `Description` dan `Category` setelah melalui fungsi preprocessing. Kolom lain yang tidak diperlukan seperti `Price`, `Place_Ratings`, `Description`, `Category`, dan `City` dihapus untuk fokus pada fitur yang digunakan dalam model.

   ```python
   data_content_based_filtering = data_rekomendasi.copy()
   data_content_based_filtering['Tags'] = data_content_based_filtering['Description'].apply(preprocessing) + " " + data_content_based_filtering['Category'].apply(preprocessing)
   data_content_based_filtering.drop(['Price','Place_Ratings','Description','Category','City'], axis=1, inplace=True)
   ```

5. **Transformasi Teks dengan TF-IDF Vectorizer**

   Untuk mengubah data teks menjadi bentuk numerik yang dapat diproses oleh algoritma machine learning, dilakukan encoding menggunakan TF-IDF Vectorizer. TF-IDF memberikan bobot pada kata berdasarkan pentingnya dalam deskripsi destinasi, sehingga fitur yang dihasilkan representatif.

   Pembatasan fitur maksimal sebanyak 5000 untuk menjaga efisiensi dan menghindari overfitting.

   ```python
   tv = TfidfVectorizer(max_features=5000)
   vectors = tv.fit_transform(data_content_based_filtering.Tags).toarray()
   ```

---

## Modeling

### Content Based Filtering

Content-Based Filtering adalah metode sistem rekomendasi yang memberikan saran destinasi wisata berdasarkan kemiripan konten atau fitur deskriptif dari tempat wisata yang sudah disukai atau pernah dikunjungi oleh pengguna sebelumnya.

#### Cosine Similarity

Cosine similarity adalah metode untuk mengukur seberapa mirip dua vektor dalam ruang multidimensi. Ini dihitung berdasarkan kosinus sudut antara dua vektor, dimana dimensi dan magnitudo vektor tersebut direpresentasikan sebagai titik dalam ruang. Nilai cosine similarity berkisar antara -1 sampai 1:

* Nilai 1 menunjukkan kedua vektor sepenuhnya sejajar (100% mirip).
* Nilai 0 menunjukkan kedua vektor tegak lurus (tidak ada keterkaitan).
* Nilai -1 menunjukkan kedua vektor sepenuhnya berlawanan arah (100% tidak mirip).

Metode ini sering digunakan dalam pemrosesan teks dan pengelompokan data untuk menentukan tingkat kesamaan antara dokumen atau fitur dalam dataset \[5].

Rumus cosine similarity:

$$
\text{CosineSimilarity}(A,B) = \frac{A \cdot B}{\|A\| \times \|B\|}
$$

Dimana:

* $A \cdot B$ adalah produk titik dari vektor A dan B.
* $\|A\|$ adalah norma Euclidean (magnitudo) dari vektor A.
* $\|B\|$ adalah norma Euclidean (magnitudo) dari vektor B.

#### Cara Kerja

Pertama, data teks dari kolom `Tags` (hasil gabungan dari `Description` dan `Category`) telah diubah menjadi representasi numerik menggunakan TF-IDF Vectorizer. Selanjutnya, dihitung cosine similarity antar semua tempat wisata berdasarkan vektor TF-IDF tersebut.

```python
similarity = cosine_similarity(vectors)
similarity[0][1:10]
```

Output contoh nilai similarity:

```
array([0.09451203, 0.09892528, 0.05760062, 0.05061528, 0.04897005,
       0.21339319, 0.0502913 , 0.16614577, 0.06611817])
```

#### Fungsi Rekomendasi

Berikut fungsi untuk merekomendasikan 9 destinasi wisata paling mirip berdasarkan nama destinasi yang dipilih user:

```python
def recommend_by_content_based_filtering(nama_tempat):
    nama_tempat_index = data_content_based_filtering[data_content_based_filtering['Place_Name'] == nama_tempat].index[0]
    distances = similarity[nama_tempat_index]
    nama_tempat_list = sorted(list(enumerate(distances)), key=lambda x: x[1], reverse=True)[1:10]

    recommended_nama_tempats = []
    for i in nama_tempat_list:
        recommended_nama_tempats.append([data_content_based_filtering.iloc[i[0]].Place_Name, i[1]])

    return recommended_nama_tempats
```

#### Contoh Penggunaan

Misalnya user memilih destinasi "Taman Bungkul", maka sistem akan merekomendasikan destinasi yang paling mirip berdasarkan konten deskripsi dan kategori.

```python
recommend_by_content_based_filtering('Taman Bungkul')
```

Output rekomendasi:

```
[['Taman Mundu', 0.3617],
 ['Taman Barunawati', 0.2650],
 ['Taman Flora Bratang Surabaya', 0.2599],
 ['Taman Prestasi', 0.2581],
 ['Taman Keputran', 0.2339],
 ['Taman Buah Surabaya', 0.2275],
 ['Air Mancur Menari', 0.2077],
 ['Taman Hiburan Rakyat', 0.2026],
 ['Taman Pelangi', 0.1866]]
```

Rekomendasi berbasis content filtering ini berhasil memberikan saran destinasi yang mirip secara konten dengan destinasi yang disukai pengguna. Misalnya, jika pengguna menyukai "Taman Bungkul," maka tempat-tempat lain yang memiliki deskripsi dan kategori serupa akan direkomendasikan, sehingga memberikan pengalaman rekomendasi yang personal dan relevan.

### Collaborative Filtering

Collaborative Filtering (CF) merekomendasikan destinasi wisata kepada pengguna berdasarkan pola interaksi atau preferensi pengguna lain yang memiliki kesamaan minat. Prinsip utamanya adalah "pengguna dengan selera mirip cenderung menyukai destinasi yang sama".

#### Data Interaksi

Dataset rating berisi interaksi antara pengguna dan destinasi wisata, dengan kolom:

* `User_Id`: ID unik pengguna.
* `Place_Id`: ID unik destinasi wisata.
* `Place_Ratings`: Rating yang diberikan pengguna pada destinasi tersebut.

Dataset ini diproses untuk mengubah ID asli menjadi indeks numerik yang diperlukan untuk embedding pada model neural network.

#### Proses Encoding

* `User_Id` di-encode menjadi indeks numerik menggunakan dictionary `user_to_user_encoded`.
* `Place_Id` juga di-encode menjadi indeks numerik dengan dictionary `resto_to_resto_encoded`.
* Data rating dinormalisasi ke skala 0–1 agar sesuai dengan output sigmoid pada model.

#### Pembagian Data

Data dibagi menjadi training (80%) dan validasi (20%) secara acak dengan random seed untuk memastikan reproducibility.

#### Model Neural Network dengan Embedding

Model yang digunakan adalah **RecommenderNet** yang dibangun menggunakan TensorFlow dan Keras, dengan arsitektur sebagai berikut:

* Dua embedding layer: satu untuk pengguna dan satu untuk destinasi wisata.
* Embedding ini memetakan user dan destinasi ke ruang vektor berdimensi rendah yang merepresentasikan preferensi dan karakteristik.
* Interaksi user dan destinasi dihitung dengan dot product antara embedding.
* Bias tambahan untuk pengguna dan destinasi ditambahkan agar model dapat belajar preferensi individual yang lebih akurat.
* Fungsi aktivasi sigmoid di output untuk memprediksi rating ter-normalisasi.



#### Training Model

Model dilatih untuk memprediksi rating pengguna pada destinasi wisata tertentu berdasarkan embedding yang dipelajari. Berikut adalah potongan kode untuk proses training model:

```python
history = model.fit(
    x = x_train,                 # input data training (user dan tempat encoded)
    y = y_train,                 # target rating (dinormalisasi)
    batch_size = 8,              # ukuran batch
    epochs = 100,                # jumlah iterasi training
    validation_data = (x_val, y_val)  # data validasi untuk evaluasi selama training
)
```

* Fungsi loss yang digunakan adalah **Binary Crossentropy**, sesuai dengan output sigmoid pada model.
* Optimizer yang digunakan adalah **Adam** dengan learning rate 0.001.
* Metrik evaluasi yang dipantau adalah **Root Mean Squared Error (RMSE)** untuk melihat performa prediksi model.

Selama proses training, model belajar meminimalkan loss dan RMSE pada data training dan validasi, yang menunjukkan kemampuan model dalam memprediksi rating destinasi wisata secara akurat.

#### Contoh Output Rekomendasi Collaborative Filtering

Output dari model untuk user dengan ID `123`:

```python
recommendations = get_recommendations_for_user(
    model=model,
    user_id=123,
    user_encoder=user_to_user_encoded,
    item_encoder=resto_to_resto_encoded,
    item_decoder=resto_encoded_to_resto,
    user_item_df=data_collaborative_filtering,
    item_df=data_tourism_with_id,
    top_k=10
)

print('-----------------------------------------------------')
print("Tempat Top 10 Rekomendasi untuk user dengan ID 123:")
print('-----------------------------------------------------')
for place in recommendations:
    print(place)
```

**Output:**

```
-----------------------------------------------------
Tempat Top 10 Rekomendasi untuk user dengan ID 123:
-----------------------------------------------------
Taman Pelangi
Taman Keputran
Masjid Nasional Al-Akbar
Keraton Surabaya
Surabaya Museum (Gedung Siola)
Monumen Jalesveva Jayamahe
Waterpark Kenjeran Surabaya
Taman Hiburan Rakyat
Museum Mpu Tantular
Gereja Perawan Maria Tak Berdosa Surabaya
```
## Evaluation

### Metrik Evaluasi yang Digunakan

Dalam proyek ini, metrik evaluasi utama yang digunakan adalah **Root Mean Squared Error (RMSE)**. RMSE mengukur rata-rata selisih kuadrat antara nilai rating aktual dan nilai rating yang diprediksi oleh model, kemudian diakarkan kembali agar hasilnya dalam satuan yang sama dengan rating.

**Formula RMSE:**

$$
\text{RMSE} = \sqrt{\frac{1}{N} \sum_{i=1}^{N} (y_i - \hat{y}_i)^2}
$$

dimana:

* $y_i$ adalah nilai rating asli ke-i
* $\hat{y}_i$ adalah nilai rating prediksi ke-i
* $N$ adalah jumlah data rating yang diuji

Nilai RMSE yang lebih rendah menunjukkan bahwa prediksi model semakin akurat mendekati nilai asli.

---

### Visualisasi Performa Model

Berikut grafik RMSE selama proses training dan validasi model neural network :

```python
import matplotlib.pyplot as plt 
import numpy as np

train_rmse = history.history['root_mean_squared_error']
val_rmse = history.history['val_root_mean_squared_error']
epochs = range(1, len(train_rmse) + 1)

plt.figure(figsize=(12, 6))
plt.plot(epochs, train_rmse, 'b-', label='Train RMSE', linewidth=2)
plt.plot(epochs, val_rmse, 'r--', label='Validation RMSE', linewidth=2)

best_epoch = np.argmin(val_rmse) + 1
best_val_rmse = val_rmse[best_epoch - 1]

plt.scatter(best_epoch, best_val_rmse, color='green', s=100, zorder=5,
            label=f'Best Val RMSE\nEpoch {best_epoch}: {best_val_rmse:.4f}')

plt.title('Training and Validation RMSE over Epochs', fontsize=16)
plt.xlabel('Epoch', fontsize=14)
plt.ylabel('Root Mean Squared Error (RMSE)', fontsize=14)
plt.legend(fontsize=12)
plt.grid(True, linestyle='--', alpha=0.6)
plt.tight_layout()
plt.show()
```

<br>
    <p align='center'><img src="https://raw.githubusercontent.com/labibaadinda/surabaya-tourism-destination-recommendation-system/main/img/rmse.png" alt="RMSE" width="400" />
    </p>
<p align='center'>Gambar 6. RMSE</p>
<br>

**Penjelasan grafik:**

* Garis biru solid menunjukkan RMSE pada data training.
* Garis merah putus-putus menunjukkan RMSE pada data validasi.
* Titik hijau menandai epoch dengan nilai validasi RMSE terbaik (terendah).

Grafik menunjukkan nilai RMSE training dan validasi yang cukup dekat dan stabil, menandakan model tidak mengalami overfitting maupun underfitting yang parah. Nilai RMSE validasi terbaik terjadi pada epoch ke-17 dengan nilai sekitar 0.3615.


### Kesimpulan Evaluasi

Berdasarkan RMSE, model neural network collaborative filtering yang dibangun telah mampu memprediksi rating pengguna dengan performa yang cukup baik dan stabil. Dengan evaluasi ini, sistem dapat merekomendasikan destinasi wisata yang relevan sesuai preferensi pengguna sehingga meningkatkan pengalaman pengguna dalam memilih tempat wisata.