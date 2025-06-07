# Laporan Proyek Machine Learning - Labiba Adinda Zahwana

## Project Overview
Sistem rekomendasi telah menjadi komponen penting dalam kehidupan digital modern, membantu pengguna menemukan informasi yang relevan dan personal di tengah banyaknya pilihan yang tersedia. Dalam konteks pariwisata di Indonesia, khususnya Kota Surabaya, keberagaman destinasi wisata menawarkan peluang besar untuk meningkatkan pengalaman wisatawan. Namun, wisatawan sering menghadapi kesulitan dalam menemukan destinasi yang sesuai dengan preferensi pribadi mereka karena tersebarnya informasi dan banyaknya pilihan yang ada. Kondisi ini dapat menyebabkan penurunan kepuasan berwisata dan potensi kunjungan ke destinasi tertentu menjadi kurang optimal.

Permasalahan ini perlu segera diatasi dengan pengembangan sistem rekomendasi destinasi wisata yang cerdas dan personal. Sistem ini bertujuan untuk memberikan rekomendasi destinasi yang relevan berdasarkan preferensi pengguna dan karakteristik destinasi, sekaligus mengenalkan destinasi wisata yang kurang populer namun memiliki potensi menarik. Pendekatan ini tidak hanya meningkatkan kemudahan dalam perencanaan perjalanan wisatawan, tetapi juga mendukung pengembangan sektor pariwisata di Surabaya secara berkelanjutan.

Berdasarkan penelitian oleh Chalkiadakis et al. (2023), penggunaan sistem rekomendasi dalam bidang pariwisata dapat meningkatkan efisiensi pencarian destinasi dan meningkatkan kepuasan pengguna secara signifikan. Selain itu, studi oleh Chanrueang et al. (2024) menunjukkan bahwa integrasi metode Collaborative Filtering dan Content-Based Filtering mampu menghasilkan rekomendasi yang lebih akurat dan personal di sektor wisata.

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
* Menerapkan metrik evaluasi yang sesuai seperti **Root Mean Squared Error (RMSE)** untuk mengukur akurasi prediksi rating pada collaborative filtering. Pada **Content-Based Filtering** menerapkan evaluasi menggunakan **Precision dan Recall** untuk memberikan gambaran tentang relevansi rekomendasi berdasarkan data yang diketahui (true\_relevant), guna memastikan efektivitas dan relevansi sistem rekomendasi.
---
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

---

Dataset yang digunakan dalam proyek ini merupakan kumpulan data terkait destinasi wisata di lima kota besar di Indonesia, yaitu Jakarta, Yogyakarta, Semarang, Bandung, dan Surabaya. Dataset ini berisi informasi mengenai berbagai tempat wisata, preferensi pengguna, serta penilaian (rating) yang diberikan oleh pengguna terhadap tempat-tempat wisata tersebut. Total terdapat sekitar 400 destinasi wisata yang terdata, dengan data penilaian mencapai 10.000 entri dan data pengguna sebanyak 300 entri. Dataset ini bersifat publik dan dapat diakses melalui [Kaggle - Indonesian Tourism Destination](https://www.kaggle.com/datasets/aprabowo/indonesia-tourism-destination/data).


Data diload dari URL (CSV online di Github Repository saya) ke dalam DataFrame pandas:

- package_tourism.csv: Paket wisata (tidak digunakan langsung di sini).
- tourism_rating.csv: Data rating pengguna ke tempat wisata.
- tourism_with_id.csv: Data tempat wisata dengan ID.
- user.csv: Data pengguna.

Pada tahap **Data Understanding**, dilakukan pengecekan kondisi dataset untuk memahami struktur, kualitas data, serta potensi masalah yang mungkin muncul. Beberapa hal yang diperiksa meliputi ukuran data, tipe data, nilai kosong (missing values), duplikasi, dan analisis eksplorasi data (Exploratory Data Analysis). Tujuannya adalah untuk mengidentifikasi masalah yang ada pada data, sehingga pada tahap **Data Preprocessing**, pembersihan data dapat dilakukan dengan tepat dan memastikan data siap digunakan dalam pengembangan sistem rekomendasi.

### Tampilkan Sekilas Data

 mulai dengan periksa sekilas data pada beberapa dataset yang tersedia. Ini dilakukan dengan menampilkan beberapa baris pertama data menggunakan metode `head()`, yang memberikan gambaran umum mengenai informasi yang terkandung dalam setiap dataset.

* **`data_tourism_rating.head()`**: Menampilkan sekilas data rating tempat wisata yang diberikan oleh pengguna.
* **`data_tourism_with_id.head()`**: Menampilkan sekilas data tempat wisata lengkap dengan informasi tambahan seperti kategori, deskripsi, harga, dan lainnya.
* **`data_user.head()`**: Menampilkan sekilas data pengguna dengan informasi seperti ID pengguna, lokasi, dan usia.

### Periksa Ukuran Data dan Tipe Data

Setelah menampilkan sekilas data, langkah selanjutnya adalah periksa ukuran dataset dan tipe data yang terkandung di dalamnya. Ini dilakukan menggunakan metode `info()` yang menunjukkan jumlah entri (baris), jumlah nilai non-null, dan tipe data masing-masing kolom.

Dataset `tourism_rating.csv`, data tersebut disimpan dalam dataframe data_tourism_rating.  Cek ukuran tipe data dengan syntax `data_tourism_rating.info()` data nya berisi 10.000 baris dengan 3 kolom:

* `User_Id`: ID pengguna.
* `Place_Id`: ID tempat wisata.
* `Place_Ratings`: Nilai rating yang diberikan pengguna.
<br>
dtypes: int64(3) -> artinya ketiga kolom tersebut type data nya integer

Dataset `tourism_with_id.csv`, data tersebut disimpan dalam dataframe data_tourism_with_id.  Cek ukuran tipe data dengan syntax `data_tourism_with_id.info()` memiliki 437 baris dan 13 kolom, di antaranya:

* `Place_Id`: ID unik tempat wisata.
* `Place_Name`: Nama tempat wisata.
* `Description`: Deskripsi singkat tempat wisata.
* `Category`: Kategori objek wisata (misal Budaya, Taman Hiburan, Bahari, dll).
* `City`: Kota tempat wisata berada.
* `Price`: Harga tiket masuk.
* `Rating`: Rating rata-rata dari pengunjung.
* `Time_Minutes`: Estimasi waktu kunjungan (banyak data kosong).
* `Coordinate`, `Lat`, `Long`: Koordinat geografis tempat wisata.
<br>
dtypes: float64(5), int64(3), object(5) -> artinya terdapat 5 kolom bertype data float, 3 kolom bertipe data integer, dan 5 kolom bertipe categorical data

Dataset `user.csv`, data tersebut disimpan dalam dataframe data_user.  Cek ukuran tipe data dengan syntax `data_user.info()` berisi 300 pengguna dengan kolom:

* `User_Id`: ID pengguna.
* `Location`: Lokasi pengguna.
* `Age`: Usia pengguna.
<br>
dtypes: int64(2), object(1) -> artinya 2 kolom bertipe integer, 1 kolom categorical data

### Periksa Nilai Null

Selanjutnya, periksa apakah ada nilai null dalam dataset yang dapat memengaruhi analisis. Ini dilakukan menggunakan metode `isnull().sum()` untuk menghitung jumlah nilai null di setiap kolom.

**Output:**

* **`data_tourism_rating.isnull().sum()`**: Tidak ada nilai null pada dataset ini.
* **`data_tourism_with_id.isnull().sum()`**: Beberapa kolom memiliki nilai null, seperti kolom `Time_Minutes` yang memiliki 232 nilai null dan kolom `Unnamed: 11` yang seluruhnya null.
* **`data_user.isnull().sum()`**: Tidak ada nilai null dalam dataset ini.

### Periksa Duplikasi
 juga periksa apakah terdapat duplikasi data di dalam dataset, yang dapat menyebabkan analisis yang bias. menggunakan metode `duplicated().sum()` untuk menghitung jumlah baris duplikat.

**Output:**

* **`data_tourism_with_id.duplicated().sum()`**: Tidak ada duplikasi data dalam dataset ini.
* **`data_user.duplicated().sum()`**: Tidak ada duplikasi data dalam dataset pengguna.
* **`data_tourism_rating.duplicated().sum()`**: Terdapat 79 baris duplikat, yang menunjukkan adanya pengguna yang memberikan rating lebih dari sekali untuk tempat wisata yang sama.

### Cek data berdasarkan kategori tempat wisata nya

* **Kategori Wisata**: Berdasarkan output dari `data_tourism_with_id['Category'].unique()`, terdapat enam kategori wisata yang teridentifikasi dalam dataset ini:

  * Budaya
  * Taman Hiburan
  * Cagar Alam
  * Bahari
  * Pusat Perbelanjaan
  * Tempat Ibadah
  Ini menunjukkan bahwa data ini mencakup beragam jenis tempat wisata yang berfokus pada aspek budaya, hiburan, alam, dan tempat ibadah.


### Exploratory Data Analysis (EDA)

Pada tahap EDA, analisis lebih dalam dilakukan untuk menggali informasi tambahan yang dapat membantu dalam pemahaman dataset. Beberapa analisis yang dilakukan meliputi:

* **Distribusi Kategori Wisata di Surabaya**: Visualisasi kategori wisata yang ada di Surabaya.
* **Distribusi Usia Pengguna**: Menganalisis distribusi usia pengguna untuk mengetahui kelompok usia yang dominan.
* **Distribusi Harga Masuk Wisata**: Visualisasi harga tiket wisata untuk melihat distribusi harga dan mendeteksi adanya outlier.

<br>
    <p align='center'><img src="https://raw.githubusercontent.com/labibaadinda/surabaya-tourism-destination-recommendation-system/main/img/jumlah_kategori.png" alt="jumlah kategori" width="400" />
    </p>
<p align='center'>Gambar 1. Distribusi Kategori Wisata di Surabaya</p>
<br>

<br>
    <p align='center'><img src="https://raw.githubusercontent.com/labibaadinda/surabaya-tourism-destination-recommendation-system/main/img/distribusi_usia.png" alt="distribusi usia" width="400" />
    </p>
<p align='center'>Gambar 2. Distribusi Usia</p>
<br>

<br>
    <p align='center'><img src="https://raw.githubusercontent.com/labibaadinda/surabaya-tourism-destination-recommendation-system/main/img/distribusi_harga.png" alt="distribusi harga" width="400" />
    </p>
<p align='center'>Gambar 3. Distribusi harga masuk tempat wisata</p>
<br>

Hasil analisis EDA :

- Jumlah kategori wisata di Kota Surabaya terbanyak yaitu budaya dan taman hiburan.
- Distribusi usia sekitar 23-34 tahun.
- Distribusi Harga Masuk Wisata di Kota Surabaya sekitar 0-20000, namun ada beberapa outlier / harga diluar range tsb.

---
## Data Preparation / Preprocessing


Data preparation adalah langkah penting dalam proses pembuatan model rekomendasi. Tahap ini bertujuan untuk membersihkan dan mempersiapkan data agar siap digunakan dalam analisis lebih lanjut. Berikut adalah penjelasan detail mengenai proses preprocessing yang dilakukan pada dataset ini:

###  Data Tourism with ID

1. **Menghapus Kolom yang Tidak Relevan atau Mengandung Nilai Null**

   Penghapusan kolom diperlukan agar dataset lebih siap untuk analisis lebih lanjut. 
   
   Kolom yang mengandung nilai null dan tidak relevan akan dihapus, yaitu:
<br>

   * `Unnamed: 11` (437 nilai null)
   * `Time_Minutes` (232 nilai null)

   Selain itu, beberapa kolom dalam dataset `data_tourism_with_id` yang tidak digunakan juga akan dihapus untuk membersihkan dataset. beberapa kolom diantaranya :
   * `Rating`
   * `Coordinate`
   * `Lat`
   * `Long`
   * `Unnamed: 12`

   ```python
   data_tourism_with_id.drop(['Rating', 'Time_Minutes', 'Coordinate', 'Lat', 'Long', 'Unnamed: 11', 'Unnamed: 12'], axis=1, inplace=True)
   ```


2. **Filtering Data Berdasarkan Kota**

   Selanjutnya, dilakukan filtering pada data untuk hanya menyertakan destinasi wisata yang berada di **Kota Surabaya**.

   ```python
   place = data_tourism_with_id[data_tourism_with_id['City'] == 'Surabaya']
   ```

   Setelah langkah ini, dataset hanya akan berisi tempat wisata yang ada di Surabaya.


### Data Tourism Rating

1. **Menghapus Data Duplikat**

   Pada dataset `data_tourism_rating`, terdapat duplikasi data yang perlu dihapus. Duplikasi ini mungkin terjadi karena pengguna memberikan lebih dari satu rating untuk tempat wisata yang sama.

   ```python
   data_tourism_rating.drop_duplicates(inplace=True)
   ```

   Setelah duplikasi dihapus, kita dapat memastikan data lebih akurat.

2. **Memfilter Data Rating untuk Tempat Wisata di Surabaya**

   Data rating yang tidak terkait dengan tempat wisata di Surabaya dihapus. Hal ini dilakukan dengan menggabungkan (`merge`) antara `data_tourism_rating` dan `place`, sehingga hanya rating dari tempat wisata di Surabaya yang tersisa.

   ```python
   rating = pd.merge(data_tourism_rating, place[['Place_Id']], on='Place_Id', how='right')
   ```

3. **Menghitung Rata-Rata Rating per Tempat Wisata**

   Setelah mendapatkan data rating untuk tempat wisata di Surabaya, langkah selanjutnya adalah menghitung rata-rata rating untuk setiap tempat wisata. Data ini akan membantu memberikan gambaran umum tentang popularitas tempat wisata tersebut.

   ```python
   data_rekomendasi = pd.merge(rating.groupby('Place_Id')['Place_Ratings'].mean(), place, on='Place_Id')
   ```

### Data User

**Memfilter Data Pengguna yang Mengunjungi Wisata di Surabaya**

   Pada tahap ini, dilakukan penyaringan pada data pengguna, sehingga hanya pengguna yang telah memberi rating pada tempat wisata di Surabaya yang akan digunakan dalam analisis. Hal ini dilakukan dengan menggabungkan (`merge`) antara `data_user` dan `rating` berdasarkan `User_Id`.

   ```python
   user = pd.merge(data_user, rating[['User_Id']], on='User_Id', how='inner')
   ```

   Proses ini memastikan hanya pengguna yang pernah memberi rating pada destinasi wisata di Surabaya yang disertakan dalam dataset.

### **Preprocessing Content-Based Filtering (CBF)**

#### 1. **Preprocessing Data dengan `.apply(preprocessing)`**
Pada tahap ini diawali dengan membuat fungsi preprocessing data.

```python
# Fungsi Preprocessing
stem = StemmerFactory().create_stemmer()
stopword = StopWordRemoverFactory().create_stop_word_remover()

def preprocessing(data):
    data = data.lower()  # Mengubah teks menjadi huruf kecil
    data = stem.stem(data)  # Stemming
    data = stopword.remove(data)  # Menghapus stopwords
    return data
```
Proses **preprocessing** ini dilakukan dengan cara menerapkan fungsi `preprocessing` pada kolom **Description** dan **Category** di dataset untuk menyiapkan data teks yang bersih dan siap diproses lebih lanjut. Fungsi `.apply(preprocessing)` digunakan untuk memanggil fungsi **preprocessing** pada setiap elemen dalam kolom tersebut.

**Langkah-langkah:**

* **Deskripsi dan kategori tempat wisata** akan diproses untuk menghilangkan kata-kata umum (stopwords) dan mengubah kata-kata menjadi bentuk dasar (stemming).
* Kolom **Description** dan **Category** akan diproses terlebih dahulu sebelum digabungkan menjadi kolom **Tags**.

```python
# Preprocessing kolom 'Description' dan 'Category' untuk menghasilkan 'Tags'
data_content_based_filtering['Description'] = data_content_based_filtering['Description'].apply(preprocessing)
data_content_based_filtering['Category'] = data_content_based_filtering['Category'].apply(preprocessing)
```

**Penjelasan:**

* **`data_content_based_filtering['Description'].apply(preprocessing)`** akan menerapkan fungsi **preprocessing** pada setiap entri dalam kolom **Description**.
* **`data_content_based_filtering['Category'].apply(preprocessing)`** melakukan hal yang sama untuk kolom **Category**.
* Hasilnya, kolom **Description** dan **Category** akan menjadi versi yang lebih bersih dan terstruktur, siap untuk analisis lebih lanjut.

#### 2. **Membuat Kolom 'Tags'**

Setelah kedua kolom tersebut diproses, kita bisa menggabungkannya menjadi kolom **Tags** yang akan digunakan dalam analisis.

```python
# Menggabungkan 'Description' dan 'Category' menjadi kolom 'Tags'
data_content_based_filtering['Tags'] = data_content_based_filtering['Description'] + " " + data_content_based_filtering['Category']
```

Kolom **Tags** ini akan berisi kombinasi dari **Description** dan **Category** yang sudah melalui proses **preprocessing**.

#### 3. **Menghapus Kolom yang Tidak Diperlukan**

Setelah kolom **Tags** dibentuk, kita menghapus kolom yang tidak diperlukan untuk analisis lebih lanjut.

```python
# Drop kolom yang tidak relevan
data_content_based_filtering.drop(['Price', 'Place_Ratings', 'Description', 'Category', 'City'], axis=1, inplace=True)
```

Kolom **Price**, **Place\_Ratings**, **Description**, **Category**, dan **City** dihapus dari dataset karena tidak diperlukan untuk analisis **Content-Based Filtering**.

#### 4. **Lanjutan Proses: Mengubah Teks ke Representasi Numerik dengan TF-IDF**

**Konsep Perhitungan TF-IDF**

**TF-IDF** adalah metode yang digunakan untuk mengukur seberapa penting sebuah kata dalam suatu dokumen, dengan mempertimbangkan seberapa sering kata tersebut muncul dalam dokumen dan seberapa jarang kata tersebut muncul di seluruh koleksi dokumen. Berikut adalah dua komponen utama yang digunakan untuk menghitung **TF-IDF**:

* **Term Frequency (TF):**
  Rumus untuk menghitung **Term Frequency** adalah sebagai berikut:

  $$\text{TF}(t, d) = \frac{\text{Jumlah kemunculan kata t dalam dokumen d}}{\text{Jumlah kata dalam dokumen d}}$$

  Dimana:

  * $t$ adalah kata yang dihitung frekuensinya,
  * $d$ adalah dokumen tertentu.

  **Contoh**: Jika dalam sebuah dokumen terdapat kata "pantai" sebanyak 5 kali dan total kata dalam dokumen tersebut adalah 100, maka **TF** untuk kata "pantai" adalah $\frac{5}{100} = 0.05$.

* **Inverse Document Frequency (IDF):**
  Rumus untuk menghitung **Inverse Document Frequency** adalah:

  $$\text{IDF}(t) = \log \left( \frac{N}{df(t)} \right)$$

  Dimana:

  * $N$ adalah jumlah total dokumen dalam koleksi,
  * $df(t)$ adalah jumlah dokumen yang mengandung kata $t$.

  **Contoh**: Jika kata "pantai" muncul di 20 dokumen dari 100 dokumen, maka **IDF** untuk kata "pantai" adalah $\log \left( \frac{100}{20} \right) = 1.69897$.

* **TF-IDF:**
  Setelah menghitung **TF** dan **IDF**, kita bisa menggabungkannya untuk menghitung **TF-IDF** kata dalam sebuah dokumen:

  $$\text{TF-IDF}(t, d) = \text{TF}(t, d) \times \text{IDF}(t)$$

  **Contoh**: Jika **TF** untuk kata "pantai" adalah 0.05 dan **IDF** untuk kata "pantai" adalah 1.69897, maka **TF-IDF** untuk kata "pantai" adalah $0.05 \times 1.69897 = 0.08495$.

Hasil dari **TF-IDF** ini memberikan nilai yang lebih tinggi pada kata-kata yang sering muncul dalam suatu dokumen, tetapi jarang muncul di seluruh koleksi dokumen. Dengan cara ini, kita dapat menilai kata-kata yang lebih relevan dalam dokumen dibandingkan dengan kata-kata yang sering muncul di banyak dokumen dan tidak memberikan banyak informasi.

Untuk implementasi python code nya. Langkah berikutnya setelah data siap, adalah mengubah teks dalam kolom **Tags** menjadi representasi numerik dengan menggunakan **TF-IDF Vectorizer**.

```python
from sklearn.feature_extraction.text import TfidfVectorizer

# Buat instance TfidfVectorizer dengan maksimal 5000 fitur
tv = TfidfVectorizer(max_features=5000)

# Ubah teks menjadi representasi numerik
tfidf_matrix = tv.fit_transform(data_content_based_filtering['Tags']).toarray()
tfidf_matrix
```

Output tfidf_matrix :
```
array([[0., 0., 0., ..., 0., 0., 0.],
       [0., 0., 0., ..., 0., 0., 0.],
       [0., 0., 0., ..., 0., 0., 0.],
       ...,
       [0., 0., 0., ..., 0., 0., 0.],
       [0., 0., 0., ..., 0., 0., 0.],
       [0., 0., 0., ..., 0., 0., 0.]])
```

**Matriks TF-IDF** ini berisi representasi numerik dari teks yang ada di kolom **Tags** untuk setiap tempat wisata, yang **nantinya akan digunakan** untuk menghitung kemiripan antar tempat wisata menggunakan **Cosine Similarity** (di tahap modeling). Matriks ini memungkinkan sistem untuk memahami dan membandingkan kemiripan antara item (dalam hal ini, tempat wisata) berdasarkan fitur teks yang telah diolah.

### **Preprocessing Collaborative Filtering**

#### 1. **Mempersiapkan Data**

Langkah pertama adalah mempersiapkan data interaksi antara pengguna dan tempat wisata. Data yang digunakan terdiri dari `User_Id`, `Place_Id`, dan `Place_Ratings`, yang menggambarkan rating yang diberikan pengguna terhadap tempat wisata tertentu.

```python
data_collaborative_filtering = rating.copy()
```

#### 2. **Proses Encoding untuk User dan Place**

Pada langkah berikutnya, kita mengubah ID pengguna (`User_Id`) dan ID tempat wisata (`Place_Id`) menjadi indeks numerik agar bisa digunakan dalam model deep learning (RecommenderNet).

```python
user_ids = data_collaborative_filtering['User_Id'].unique().tolist()
user_to_user_encoded = {x: i for i, x in enumerate(user_ids)} 
user_encoded_to_user = {i: x for i, x in enumerate(user_ids)} 
```

Selanjutnya, lakukan hal yang sama untuk tempat wisata (`Place_Id`).

```python
place_ids = data_collaborative_filtering['Place_Id'].unique().tolist()
place_to_place_encoded = {x: i for i, x in enumerate(place_ids)}
place_encoded_to_place = {i: x for i, x in enumerate(place_ids)}
```

#### 3. **Menambahkan Kolom User dan Place pada Dataframe**

Kemudian, kita akan menambahkan kolom baru pada `data_collaborative_filtering` yang berisi ID yang telah dienkode.

```python
data_collaborative_filtering['user'] = data_collaborative_filtering['User_Id'].map(user_to_user_encoded)
data_collaborative_filtering['place'] = data_collaborative_filtering['Place_Id'].map(place_to_place_encoded)
```

#### 4. **Hitung max dan min rating**
Kemudian hitung nilai max dan min rating dengan kode ini yang mana menghitung jumlah pengguna dan tempat terlebih dahulu, mengubah rating tempat jadi angka desimal, serta mencari rating terkecil dan terbesar, lalu menampilkannya.

```python
# Mendapatkan jumlah user
num_users = len(user_to_user_encoded)
print(num_users)

# Mendapatkan jumlah place
num_place = len(place_encoded_to_place)
print(num_place)

# Mengubah rating menjadi nilai float
data_collaborative_filtering['Place_Ratings'] = data_collaborative_filtering['Place_Ratings'].values.astype(np.float32)

# Nilai minimum rating
min_rating = min(data_collaborative_filtering['Place_Ratings'])

# Nilai maksimal rating
max_rating = max(data_collaborative_filtering['Place_Ratings'])

print('Number of User: {}, Number of place: {}, Min Rating: {}, Max Rating: {}'.format(
    num_users, num_place, min_rating, max_rating
))
```

#### 5. Acak urutan data `data_collaborative_filtering`
```python
data_collaborative_filtering = data_collaborative_filtering.sample(frac=1, random_state=42)
```
Kode tersebut digunakan untuk mengacak urutan data pada `data_collaborative_filtering`. Fungsi `.sample(frac=1)` mengacak seluruh baris data, sementara `random_state=42` memastikan hasil acakan yang konsisten setiap kali kode dijalankan.


#### 6. **Membagi Data Menjadi Training dan Validation**

Data akan dibagi menjadi dua bagian: data latih dan data validasi. Ini untuk memastikan bahwa model dapat dilatih dan dievaluasi dengan data yang berbeda.

```python
x = data_collaborative_filtering[['user', 'place']].values
y = data_collaborative_filtering['Place_Ratings'].apply(lambda x: (x - min_rating) / (max_rating - min_rating)).values

train_indices = int(0.8 * data_collaborative_filtering.shape[0])
x_train, x_val, y_train, y_val = x[:train_indices], x[train_indices:], y[:train_indices], y[train_indices:]
```

---

## Modeling


### Content Based Filtering

Content-Based Filtering adalah metode sistem rekomendasi yang memberikan saran destinasi wisata berdasarkan kemiripan konten atau fitur deskriptif dari tempat wisata yang sudah disukai atau pernah dikunjungi oleh pengguna sebelumnya.


#### Menerapkan metode **Cosine Similarity** 

---
#### **Cosine Similarity**

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
similarity = cosine_similarity(tfidf_matrix, tfidf_matrix)
print(similarity[0][1:10])
```

Output nilai similarity:

```
array([0.0696098, 0.05875268, 0.01923046, 0.02888786, 0.02165435, 0.22933779, 0.02817197, 0.15322766, 0.03327171])
```

Hasil **similarity** adalah matriks yang menunjukkan kemiripan antar tempat wisata berdasarkan fitur teksnya. Nilai dalam matriks **similarity** ini berkisar antara 0 hingga 1, dengan 1 berarti sangat mirip dan 0 berarti tidak mirip sama sekali.

#### **Fungsi Rekomendasi Content-Based Filtering**

Terakhir, kita membuat fungsi untuk memberikan rekomendasi **top-N** tempat wisata berdasarkan kemiripan yang dihitung menggunakan **Cosine Similarity**.

```python
def recommend_place_content_based_filtering(place_name, similarity, data_content_based_filtering):
    idx = data_content_based_filtering[data_content_based_filtering['Place_Name'] == place_name].index[0]
    sim_scores = list(enumerate(similarity[idx]))
    
    # Mengurutkan berdasarkan skor kesamaan (Cosine Similarity)
    sim_scores = sorted(sim_scores, key=lambda x: x[1], reverse=True)
    
    # Mengambil 10 rekomendasi teratas
    sim_scores = sim_scores[1:11]  # Menghindari tempat itu sendiri
    place_indices = [i[0] for i in sim_scores]
    return data_content_based_filtering['Place_Name'].iloc[place_indices].reset_index(drop=True)
```

> Fungsi ini akan memberikan rekomendasi **top-N** tempat wisata berdasarkan tempat yang dipilih pengguna, berdasarkan nilai **Cosine Similarity** tertinggi.

#### Contoh Penggunaan

Misalnya user memilih destinasi "Taman Bungkul", maka sistem akan merekomendasikan destinasi yang paling mirip berdasarkan konten deskripsi dan kategori.

```python
# Menampilkan rekomendasi untuk 'Taman Bungkul'
print("Rekomendasi untuk 'Taman Bungkul':")
recommend_place_content_based_filtering('Taman Bungkul', similarity, data_content_based_filtering)
```

Output rekomendasi:

```
Place_Name
0	Taman Mundu
1	Taman Flora Bratang Surabaya
2	Taman Barunawati
3	Taman Prestasi
4	Taman Keputran
5	Taman Hiburan Rakyat
6	Taman Buah Surabaya
7	Taman Pelangi
8	Atlantis Land Surabaya
9	Air Mancur Menari
```

#### Kesimpulan dari Content-Based Filtering:

Content-Based Filtering memberikan rekomendasi berdasarkan kemiripan konten dari tempat wisata yang telah disukai atau dikunjungi oleh pengguna sebelumnya. Proses ini melibatkan tahap preprocessing data teks, penggunaan TF-IDF untuk merepresentasikan teks, dan penghitungan Cosine Similarity untuk menilai kemiripan antar tempat wisata. Pendekatan ini sangat berguna ketika kita ingin memberikan rekomendasi berdasarkan konten yang mirip, tanpa memerlukan data interaksi pengguna sebelumnya.

Selanjutnya, untuk mengevaluasi efektivitas dari sistem rekomendasi ini, akan dilakukan evaluasi menggunakan **Precision** dan **Recall** pada **Tahap Evaluasi**. **Precision** mengukur seberapa akurat rekomendasi yang diberikan (berapa banyak tempat wisata yang direkomendasikan benar-benar relevan dengan pengguna), sementara **Recall** mengukur seberapa banyak tempat wisata relevan yang berhasil ditemukan oleh sistem di antara semua tempat wisata relevan yang tersedia. Evaluasi ini penting untuk memastikan bahwa sistem rekomendasi dapat memberikan rekomendasi yang bermanfaat dan tepat sasaran.



### Collaborative Filtering

Collaborative Filtering (CF) adalah teknik dalam sistem rekomendasi yang memberikan rekomendasi berdasarkan pola interaksi atau preferensi pengguna lain yang memiliki kesamaan dengan pengguna yang sedang dianalisis. Dalam hal ini, CF akan merekomendasikan tempat wisata kepada pengguna berdasarkan kesamaan preferensi mereka dengan pengguna lain yang telah memberikan rating terhadap tempat-tempat wisata sebelumnya.

Misalnya, jika pengguna A dan B memiliki kesukaan yang mirip terhadap beberapa tempat wisata, maka tempat wisata yang disukai oleh pengguna A, yang belum dikunjungi oleh pengguna B, dapat direkomendasikan kepada pengguna B.



#### **Membangun Model Neural Network dengan Embedding**

Model rekomendasi dibangun dengan menggunakan **Embedding** untuk pengguna dan tempat wisata. Embedding memetakan ID pengguna dan tempat wisata ke dalam ruang vektor berdimensi rendah yang merepresentasikan karakteristik dan preferensi mereka.

```python
class RecommenderNet(tf.keras.Model):
    def __init__(self, num_users, num_place, embedding_size, **kwargs):
        super(RecommenderNet, self).__init__(**kwargs)
        self.user_embedding = layers.Embedding(num_users, embedding_size)
        self.user_bias = layers.Embedding(num_users, 1)
        self.place_embedding = layers.Embedding(num_place, embedding_size)
        self.place_bias = layers.Embedding(num_place, 1)

    def call(self, inputs):
        user_vector = self.user_embedding(inputs[:, 0])
        user_bias = self.user_bias(inputs[:, 0])
        place_vector = self.place_embedding(inputs[:, 1])
        place_bias = self.place_bias(inputs[:, 1])

        dot_user_place = tf.tensordot(user_vector, place_vector, 2)
        return tf.nn.sigmoid(dot_user_place + user_bias + place_bias)
```

#### **Melatih Model**

Setelah model dibangun, kita dapat mulai melatihnya menggunakan data latih.

```python
model.compile(
    loss=tf.keras.losses.BinaryCrossentropy(),
    optimizer=tf.keras.optimizers.Adam(learning_rate=0.001),
    metrics=[tf.keras.metrics.RootMeanSquaredError()]
)

history = model.fit(x_train, y_train, batch_size=8, epochs=100, validation_data=(x_val, y_val))
```

#### Recommender
##### 1. **Memberikan Rekomendasi untuk Banyak Pengguna**
Fungsi `get_bulk_recommendations` digunakan untuk memberikan rekomendasi **top-k** tempat wisata untuk banyak pengguna berdasarkan model yang telah dilatih.

```python
def get_bulk_recommendations(model, user_ids, user_encoder, item_encoder, item_decoder, user_item_df, item_df, top_k=10):
    all_recommendations = {}

    for user_id in user_ids:
        visited = user_item_df[user_item_df['User_Id'] == user_id]['Place_Id'].values
        not_visited = item_df[~item_df['Place_Id'].isin(visited)]['Place_Id']
        not_visited = list(set(not_visited).intersection(set(item_encoder.keys())))

        if len(not_visited) == 0:
            all_recommendations[user_id] = []
            continue

        user_encoded = user_encoder[user_id]
        not_visited_encoded = [[item_encoder[x]] for x in not_visited]
        user_input = np.hstack((np.array([[user_encoded]] * len(not_visited_encoded)), not_visited_encoded))

        preds = model.predict(user_input).flatten()
        top_indices = preds.argsort()[-top_k:][::-1]

        recommended_ids = [not_visited[i] for i in top_indices]
        recommended_names = item_df[item_df['Place_Id'].isin(recommended_ids)]['Place_Name'].values
        all_recommendations[user_id] = recommended_names.tolist()

    return all_recommendations
```

**Menampilkan Rekomendasi**

Setelah mendapatkan rekomendasi untuk semua pengguna, kita dapat menampilkan rekomendasi untuk pengguna pertama sebagai contoh.

```python
all_users = data_collaborative_filtering['User_Id'].unique()
bulk_rekom = get_bulk_recommendations(
    model=model,
    user_ids=all_users,
    user_encoder=user_to_user_encoded,
    item_encoder=place_to_place_encoded,
    item_decoder=place_encoded_to_place,
    user_item_df=data_collaborative_filtering,
    item_df=data_tourism_with_id,
    top_k=10
)

first_user = all_users[0]
print(f"Rekomendasi untuk user {first_user}:")
print(bulk_rekom[first_user])
```

#### Output:

```bash
Rekomendasi untuk user 209:
['Masjid Nasional Al-Akbar', 'Keraton Surabaya', 'House of Sampoerna', 'Atlantis Land Surabaya', 'Taman Hiburan Rakyat', 'Taman Mundu', 'Museum Mpu Tantular', 'Taman Air Mancur Menari Kenjeran', 'Taman Flora Bratang Surabaya', 'Gereja Perawan Maria Tak Berdosa Surabaya']
```
Fungsi `get_bulk_recommendations` memberikan rekomendasi **top-k** untuk **banyak pengguna sekaligus**. Meskipun **contoh kode untuk yang di print** menampilkan rekomendasi untuk *first_user*. Namun fungsi ini sudah menghitung dan mengembalikan rekomendasi untuk semua pengguna dalam dataset, juga bisa mengakses rekomendasi untuk pengguna lain dengan cara yang sama, misalnya untuk user kedua `bulk_rekom[all_users[1]]`.


##### 2. **Mendapatkan Rekomendasi untuk Satu Pengguna**

Fungsi `get_recommendations_for_user` digunakan untuk memberikan rekomendasi **top-k** tempat wisata untuk satu pengguna berdasarkan model yang telah dilatih.

```python
def get_recommendations_for_user(model, user_id, user_encoder, item_encoder, item_decoder, user_item_df, item_df, top_k=10):
    if user_id not in user_encoder:
        return f"User ID {user_id} tidak ditemukan dalam data."

    # Tempat yang sudah pernah dikunjungi user
    visited = user_item_df[user_item_df['User_Id'] == user_id]['Place_Id'].values

    # Tempat yang belum dikunjungi
    not_visited = item_df[~item_df['Place_Id'].isin(visited)]['Place_Id']
    not_visited = list(set(not_visited).intersection(set(item_encoder.keys())))

    # Encode user dan tempat yang belum dikunjungi
    user_encoded = user_encoder[user_id]
    not_visited_encoded = [[item_encoder[x]] for x in not_visited]

    # Bentuk array input untuk model
    user_input = np.hstack((np.array([[user_encoded]] * len(not_visited_encoded)), not_visited_encoded))

    # Prediksi rating untuk tempat belum dikunjungi
    preds = model.predict(user_input).flatten()

    # Urutkan indeks rating tertinggi
    top_indices = preds.argsort()[-top_k:][::-1]

    # Decode item_id rekomendasi
    recommended_ids = [not_visited[i] for i in top_indices]

    # Ambil nama tempat dari item_df
    recommended_names = item_df[item_df['Place_Id'].isin(recommended_ids)]['Place_Name'].values

    return recommended_names.tolist()
```

**Menampilkan Rekomendasi untuk Pengguna Tertentu**

Sekarang kita bisa mendapatkan rekomendasi untuk pengguna tertentu (misalnya pengguna dengan `user_id=123`).

```python
recommendations = get_recommendations_for_user(
    model=model,
    user_id=123,
    user_encoder=user_to_user_encoded,
    item_encoder=place_to_place_encoded,
    item_decoder=place_encoded_to_place,
    user_item_df=data_collaborative_filtering,
    item_df=data_tourism_with_id,
    top_k=10
)

print("-----------------------------------------------------")
print("Top 10 Tempat Rekomendasi untuk User dengan ID 123:")
print("-----------------------------------------------------")
for place in recommendations:
    print(place)
```

#### Output:

```bash
-----------------------------------------------------
Tempat Top 10 Rekomendasi untuk user dengan ID 123:
-----------------------------------------------------
Taman Prestasi
Monumen Kapal Selam
Taman Pelangi
Taman Keputran
Taman Ekspresi Dan Perpustakaan
Rumah Batik
Masjid Nasional Al-Akbar
Keraton Surabaya
Surabaya Museum (Gedung Siola)
Monumen Jalesveva Jayamahe
```

> Fungsi ini memberikan cara untuk merekomendasikan **tempat wisata** bagi **satu pengguna** berdasarkan model deep learning yang telah dilatih menggunakan data interaksi pengguna dan destinasi wisata. Ini merupakan implementasi dasar dari **Collaborative Filtering** yang memanfaatkan teknik embedding neural network untuk mendapatkan rekomendasi yang relevan.
---
### **Kelebihan dan Kekurangan dari Content-Based Filtering dan Collaborative Filtering**

1. **Content-Based Filtering (CBF)**

**Kelebihan:**

* **Independen dari Data Pengguna:** Content-Based Filtering dapat memberikan rekomendasi berdasarkan konten (misalnya, tag, deskripsi, kategori) yang terkait dengan item (seperti tempat wisata). Ini tidak memerlukan interaksi atau preferensi pengguna lain untuk menghasilkan rekomendasi, yang berarti sistem dapat bekerja meskipun data interaksi pengguna terbatas atau tidak ada.
* **Personalization:** Karena sistem ini memanfaatkan atribut item yang disukai oleh pengguna sebelumnya, rekomendasi bisa sangat personal dan relevan dengan preferensi individu pengguna.
* **Sistem yang Mudah Dipahami:** Proses rekomendasi menggunakan CBF sangat mudah dipahami karena menggunakan atribut jelas dari item untuk memutuskan item yang serupa dengan yang disukai pengguna sebelumnya.

**Kekurangan:**

* **Masalah Cold Start:** Untuk pengguna baru yang belum memiliki riwayat interaksi atau rating, sistem ini kesulitan memberikan rekomendasi yang baik karena tidak ada data sebelumnya tentang preferensi pengguna.
* **Over-Specialization:** CBF dapat cenderung memberi rekomendasi yang terlalu mirip dengan item yang sudah disukai pengguna sebelumnya. Hal ini bisa membatasi keberagaman rekomendasi dan membuat pengalaman pengguna menjadi monoton.
* **Kesulitan dalam Menangani Preferensi yang Kompleks:** CBF mengandalkan pada atribut eksplisit dari item, yang bisa membuatnya kesulitan dalam menangani preferensi pengguna yang lebih kompleks atau nuansa tertentu yang tidak tercermin dalam data atribut item.

---

2. **Collaborative Filtering (CF)**

**Kelebihan:**

* **Mampu Mengatasi Cold Start pada Item:** Collaborative Filtering tidak memerlukan atribut eksplisit dari item untuk memberikan rekomendasi. Sebagai gantinya, sistem ini menggunakan pola interaksi atau preferensi pengguna lain yang serupa. Hal ini membuatnya efektif untuk item-item yang tidak memiliki banyak informasi atau atribut eksplisit.
* **Lebih Menyediakan Rekomendasi Beragam:** CF memberikan rekomendasi yang lebih beragam karena tidak terikat pada atribut item tertentu. Pengguna bisa mendapatkan rekomendasi item yang sangat berbeda, yang mereka mungkin tidak tahu atau coba sebelumnya.
* **Skalabilitas:** Dengan menggunakan data interaksi yang ada, Collaborative Filtering dapat memanfaatkan data dari banyak pengguna untuk meningkatkan akurasi rekomendasi, terutama ketika ada banyak data interaksi pengguna yang tersedia.

**Kekurangan:**

* **Masalah Cold Start pada Pengguna Baru:** Collaborative Filtering kesulitan dalam memberikan rekomendasi untuk pengguna baru yang belum memberikan rating atau interaksi apapun. Ini membuat sistemnya kurang efektif untuk pengguna baru, yang dikenal sebagai masalah "Cold Start".
* **Ketergantungan pada Data Pengguna:** CF bergantung sepenuhnya pada data interaksi pengguna. Ketika data interaksi terbatas atau tidak mencakup preferensi yang luas, rekomendasi yang dihasilkan bisa kurang tepat.
* **Rentan Terhadap Bias Popularitas:** Collaborative Filtering cenderung lebih sering merekomendasikan item-item yang populer, karena lebih banyak pengguna yang memberi rating positif terhadap item tersebut. Hal ini dapat mengurangi keberagaman rekomendasi, membuat sistem sering memberikan rekomendasi yang terlalu mainstream.
* **Kompleksitas dalam Skalabilitas:** Ketika jumlah pengguna dan item semakin banyak, perhitungan similarity antar pengguna atau antar item bisa memerlukan komputasi yang sangat besar, membuat sistem ini kurang efisien dari sisi waktu dan sumber daya.

## Evaluation

Pada bagian ini, kita akan mengevaluasi dua metode rekomendasi yang digunakan dalam sistem ini: **Content-Based Filtering** (CBF) dan **Collaborative Filtering** (CF). Evaluasi dilakukan untuk memastikan kualitas dari rekomendasi yang diberikan oleh masing-masing metode, baik dari segi relevansi maupun akurasi.

### 1. **Evaluasi Content-Based Filtering**

Content-Based Filtering (CBF) memberikan rekomendasi berdasarkan kemiripan konten dari item yang sudah disukai atau dikunjungi sebelumnya. Evaluasi metode ini dilakukan dengan menggunakan dua metrik: **Precision** dan **Recall**.

#### **Definisi Precision dan Recall**

* **Precision** mengukur berapa banyak dari rekomendasi yang diberikan benar-benar relevan dengan preferensi pengguna.

  Formula Precision:
  $\text{Precision} = \frac{\text{Jumlah rekomendasi relevan}}{K}$

* **Recall** mengukur berapa banyak item relevan yang berhasil ditemukan oleh sistem dari seluruh item relevan yang ada.

  Formula Recall:
  $\text{Recall} = \frac{\text{Jumlah rekomendasi relevan}}{\text{Jumlah total item relevan}}$

#### **Langkah Evaluasi**

1. **Mendefinisikan Data Relevan (true\_relevant)**:
   Data relevan ini berisi tempat-tempat yang seharusnya direkomendasikan oleh sistem berdasarkan pengetahuan yang ada. Dalam contoh ini, kita mendefinisikan `true_relevant` yang berisi tempat wisata yang relevan dengan preferensi pengguna.

   Contoh:

   ```python
   true_relevant = ['Taman Mundu', 'Taman Barunawati']
   ```

2. **Mendapatkan Rekomendasi**:
   Sistem memberikan rekomendasi berdasarkan metode Content-Based Filtering, dan kita memilih 3 rekomendasi teratas.

   ```python
   recommended_places = recommend_place_content_based_filtering('Taman Bungkul', similarity, data_content_based_filtering)
   ```

3. **Menghitung Precision dan Recall**:
   Fungsi `precision_recall_at_k` digunakan untuk menghitung nilai Precision dan Recall pada rekomendasi teratas.

   ```python
   precision, recall = precision_recall_at_k(recommended_places, true_relevant, k=3)
   ```

4. **Output Evaluasi**:
   Hasil evaluasi ditampilkan dalam bentuk Precision dan Recall untuk 3 rekomendasi teratas.

   ```python
   print(f"Precision at 3: {precision}")
   print(f"Recall at 3: {recall}")
   ```

#### **Contoh Hasil Evaluasi**:

```plaintext
Rekomendasi Top 3:
['Taman Mundu', 'Taman Flora Bratang Surabaya', 'Taman Barunawati']
Precision at 3: 0.6666666666666666
Recall at 3: 1.0
```

**Penjelasan**:

* **Precision**: Dari 3 rekomendasi, 2 di antaranya relevan (Taman Mundu dan Taman Barunawati), sehingga Precision adalah 0.6666666666666666.
* **Recall**: Dari 2 tempat relevan yang ada (Taman Mundu dan Taman Barunawati), keduanya ditemukan dalam rekomendasi, sehingga Recall adalah 1.0.

---

### 2. **Evaluasi Collaborative Filtering**

Collaborative Filtering (CF) memberikan rekomendasi berdasarkan pola interaksi atau preferensi pengguna lain yang serupa. Evaluasi untuk metode ini dilakukan menggunakan **Root Mean Squared Error** (RMSE) sebagai metrik utama untuk mengukur seberapa akurat prediksi rating yang dihasilkan oleh model.


#### Metrik Evaluasi yang Digunakan

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


#### **Langkah Evaluasi**

1. **Mempersiapkan Data RMSE**:
   Kita akan memplot **RMSE** selama proses pelatihan untuk memantau apakah model mengalami overfitting atau underfitting. RMSE dihitung selama proses pelatihan pada data training dan validasi.

2. **Plotting RMSE**:
   Grafik ini menunjukkan nilai RMSE untuk data training dan validasi sepanjang epoch pelatihan. RMSE yang lebih rendah menunjukkan bahwa model lebih baik dalam memprediksi rating dengan akurasi tinggi.

   ```python
   train_rmse = history.history['root_mean_squared_error']
   val_rmse = history.history['val_root_mean_squared_error']
   ```

3. **Menampilkan Grafik RMSE**:
   Berikut adalah cara untuk memplot grafik RMSE.

   ```python
   plt.plot(epochs, train_rmse, 'b-', label='Train RMSE', linewidth=2)
   plt.plot(epochs, val_rmse, 'r--', label='Validation RMSE', linewidth=2)
   ```

   Titik terbaik pada grafik menandai epoch dengan RMSE validasi terendah.

4. **Menentukan Epoch Terbaik**:
   Titik hijau pada grafik menunjukkan epoch dengan RMSE validasi terbaik (terendah).

   ```python
   best_epoch = np.argmin(val_rmse) + 1
   best_val_rmse = val_rmse[best_epoch - 1]
   ```

#### **Grafik Evaluasi**:

Output berupa grafik berikut menunjukkan perbandingan antara RMSE pada data training dan validasi sepanjang epoch.


<br>
    <p align='center'><img src="https://raw.githubusercontent.com/labibaadinda/surabaya-tourism-destination-recommendation-system/main/img/rmse.png" alt="RMSE" width="400" />
    </p>
<p align='center'>Gambar 4. RMSE</p>
<br>

**Penjelasan grafik:**

* Garis biru solid menunjukkan RMSE pada data training.
* Garis merah putus-putus menunjukkan RMSE pada data validasi.
* Titik hijau menandai epoch dengan nilai validasi RMSE terbaik (terendah).

**Penjelasan**:

* **RMSE Training**: Menunjukkan seberapa baik model dapat memprediksi rating pada data training.
* **RMSE Validasi**: Menunjukkan seberapa baik model dapat memprediksi rating pada data validasi.
* **Best Epoch**: Epoch dengan nilai RMSE validasi terendah menunjukkan model yang paling optimal.

Grafik menunjukkan nilai RMSE training dan validasi yang cukup dekat dan stabil, menandakan model tidak mengalami overfitting maupun underfitting yang parah. Nilai RMSE validasi terbaik terjadi pada epoch ke-8 dengan nilai sekitar 0.3621.


### **Kesimpulan Evaluasi**:

Evaluasi menggunakan **Precision dan Recall** untuk Content-Based Filtering memberikan gambaran tentang relevansi rekomendasi berdasarkan data yang diketahui (true\_relevant). Sedangkan untuk **Collaborative Filtering**, grafik RMSE memberikan informasi tentang kualitas prediksi model terhadap data pengguna. 
---

## Conclusion
Sistem **Rekomendasi Destinasi Wisata Surabaya** berhasil dikembangkan dengan dua pendekatan utama, yaitu **Content-Based Filtering** dan **Collaborative Filtering** menggunakan deep learning.

Proyek ini dimulai dengan pemahaman data (Data Understanding), yang mencakup analisis data mengenai destinasi wisata, rating pengguna, dan kategori wisata di Surabaya. Melalui Exploratory Data Analysis (EDA), diperoleh wawasan penting, seperti tempat wisata yang paling banyak dikunjungi dan distribusi kategori wisata di kota tersebut. Selanjutnya, pada tahap data preprocessing, kami membersihkan dan memfilter data untuk memastikan kualitasnya. Fokus utama pada tahap ini adalah menangani nilai yang hilang, menghapus duplikasi, dan memfilter data yang relevan untuk destinasi wisata di Surabaya.

Setelah data siap, sistem rekomendasi ini dibangun dengan mengombinasikan dua pendekatan utama yang dapat memberikan hasil rekomendasi yang lebih akurat dan relevan untuk pengguna, yaitu **Content-Based Filtering** dan **Collaborative Filtering**. Kedua pendekatan ini memiliki kelebihan masing-masing dalam memberikan rekomendasi berdasarkan karakteristik destinasi atau pola interaksi antar pengguna.

1. **Content-Based Filtering** diimplementasikan dengan menganalisis data teks, seperti deskripsi dan kategori tempat wisata. Pendekatan ini menggunakan **TF-IDF** dan **Cosine Similarity** untuk memberikan rekomendasi tempat yang mirip dengan yang sudah disukai atau dikunjungi pengguna. Hal ini membantu pengguna menemukan tempat wisata baru yang memiliki karakteristik serupa dengan yang mereka sukai.

2. **Collaborative Filtering**, dengan menggunakan model deep learning dan **embedding neural network**, mampu menangkap pola interaksi yang lebih kompleks antara pengguna dan destinasi wisata. Model ini memprediksi rating untuk tempat wisata yang belum dikunjungi oleh pengguna dan memberikan rekomendasi yang lebih personal, berdasarkan preferensi pengguna yang serupa. Metode ini sangat berguna untuk menyesuaikan dengan perubahan selera pengguna.

Hasil evaluasi menggunakan metrik **Precision** dan **Recall** untuk Content-Based Filtering serta **RMSE** untuk Collaborative Filtering menunjukkan bahwa sistem ini efektif dan dapat diandalkan.

Secara keseluruhan, sistem ini **berhasil** memberikan rekomendasi yang akurat dan relevan untuk memberikan rekomendasi tempat wisata di Surabaya.

