# Laporan Proyek Akhir Sistem Rekomendasi - M Rama Nopan Ariyadi

## Project Overview
Di zaman yang semakin berkembang dengan digitalisasi di hampir semua bidang, hal ini membuat banyak orang nyaris melupakan buku. Padahal, buku merupakan hal penting yang dulunya kita gunakan sebagai sumber pendidikan, mencari informasi, hingga menemukan hiburan dan kesenangan.[[1]](https://buku.kompas.com/read/1393/manfaat-membaca-buku-ternyata-mampu-meningkatkan-kesehatan-fisik-dan-mental-apa-alasannya)

Peran buku dalam hidup kita tidak dapat diremehkan karena buku tidak hanya membantu memperluas wawasan, tetapi juga bertindak sebagai pintu penghubung dengan dunia di sekitar. Pengantar persepsi kita. Bahkan, tak salah jika buku disebut-sebut berfungsi sebagai perlengkapan bertahan hidup karena memengaruhi dan meninggalkan dampak pada kita.tentu dengan banyaknya manfaat dari buku serta buku tidak hanya satu kategori buku saja yang ada. sehingga banyak sekali jenis bacaan yang dapat dibaca berdasarkan kategori yang di inginkan.

berdasarkan permasalahan yang ada maka di perlukan sebuah inovoasi yang dapat dilakukan untuk melakukan sistem rekomendasi buku yang dapat mempermudahkan pembaca agar dapat menemukan buku yang serupa dengan buku yang dia telah baca sebelumnya. 
    
## Business Understanding
### Problem Statements
- Dengan data yang ada pada dataset, bagaimana perusahaan dapat merekomendasikan buku buku lain yang mungkin disukai pengguna dan belum pernah di baca oleh pengguna

### Goals
 - Membuat semua model machine learning yang dapat menghasilkan sistem rekomendasi berdasarkan item yang mirip dengan item yang disukai pengguna di masa lalu. dengan menggunakan *Content Based Filtering*

### Solution Statement
solusi yang diterapkan pada pengerjaan proyek sistem rekomendasi kali ini yaitu dengan menerapkan algoritma **content based filtering** 

- ***content based filtering***.
        pada tahap pengembangan model dengan model dengan metode content base filtering ini yaitu merekomendasikan item yang mirip dengan item yang disukai pengguna di masa lalu. Content-based filtering mempelajari profil minat pengguna baru berdasarkan data dari objek yang telah dinilai pengguna. Algoritma ini bekerja dengan menyarankan item serupa yang pernah disukai di masa lalu atau sedang dilihat di masa kini kepada pengguna. Semakin banyak informasi yang diberikan pengguna, semakin baik akurasi sistem rekomendasi.

## Data Understanding
**Informasi Dataset** 
Informasi   | Keterangan 
----------- |------------------
Link        | https://www.kaggle.com/datasets/dylanjcastillo/7k-books-with-metadata?select=books.csv
Lisensi     | CC0: Public Domain
Size        | 4.14 MB

**Exploratory Data Analysis (EDA) - Deskripsi Variabel**
berdasarkan informasi dari [kaggle](https://www.kaggle.com/datasets/dylanjcastillo/7k-books-with-metadata?select=books.csv), terdapat 3 tipe data pada variabel-variabel 7k-books-with-metadata dataset yaitu
tipe data int :
- *isbn13* : Pengenal ISBN 13

tipe data object.
- *isbn10* : Pengidentifikasi ISBN 10
- *title* : Judul pada buku
- *subtitle* : sub judul pada buku
- *authors* : penulis pada Buku
- *categories* : kategori pada buku
- *thumbnail* : URL gambar pada buku
- *description* : Deskripsi pada buku
 
tipe data float.
- *pyblished_year* : Tahun buku di terbitkan
- *average_rating*  : Rating rata rata pada buku
- *num_pages* : Jumlah halaman pada buku
- *ratings_count* : jumlah rating pada buku


## Data Preparation
pada data preparation di proyek predictive analytics dilakukan beberapa tahapan yaitu sebagai berikut :
 - **Mengecek Missing value**
 Tujuannya dilakukan proses missing value agar dataset menjadi bersih dari fitur fitur yang valuenya kosong karena dapat menimbulkan hasil akurasi yang kurang baik ataupun hasil bias. untuk mengecek missing value menggunakan fitur *isnull* dan juga fitur *sum()* untuk melihat jumlah data.pada saat fitur itu dijalankan maka akan di cek semua data yang berisi missing value pada dataset. setelah dilakukan pengencekan missing valeu ternyata banyak data missing.sebelum menghapus missing value pada data. terlebih dahulu hapus fitur yang tidak akan di gunakan pada sistem rekomendasi. setelah fitur telah di hapus maka di lakukan penghapusan missing value pada data yang akan di gunakan untuk sistem rekomendasi.

 - **Membuat variabel preparation**
Membuat variabel preparation yang berisi dataframe books_clean kemudian mengurutkan berdasarkan title. kemudian membuang data duplikat pada variable preparation. karena akan menggunakan data unik untuk dimasukkan ke dalam proses pemodelan. pada proyek kali ini akan membuang duplikat data berdasarkan fitur title.

- **Mengonversi data series menjadi dalam bentuk list**
  konversi variable-variable seperti titlr, authors, categories, average rating dan ratings count menjadi bentuk list

- **Membuat dictionary pada data**
Tujuan pembuatan Dictionary ini agar model yang dibuat hanya memprediksi hasil dari fitur fitur yang hanya digunakan sebagai fitur untuk melakukan proses rekomendasi. pada proyek kali ini data ‘books title’, ‘books authors’, 'books categories', 'books average rating' dan ‘books ratings count’ dimuat menjadi dictionary 'books clear' 


## Modeling
pada tahap pengembang model development pada studi kasus rekomendasi buku ini  menerapkan metode content base filtering yaitu dimana dengan menerapkan metode ini diharapkan model mampu menghasilkan sebuah hasil rekemendasi berdasarkan hasil permasalahn yang ada. Kelemahan dari metode content-based filtering adalah terbatasnya rekomendasi hanya pada item-item yang mirip sehingga tidak ada kesempatan untuk mendapatkan item yang tidak terduga. Berikut ini adalah proses tahap development model pada kasus rekomendasi buku:

pertama data yang dimiliki dan assign dataframe dari tahap sebelumnya ke dalam variabel data, kemudian digunakan TF-IDF vectorizer dari library sklearn yang digunakan untuk menemukan representasi fitur penting dari setiap kategori buku. inisialisasi TfidfVectorizer kemudian lakukan perhitungan idf pada data kategori. selanjutnya lakukan fit dan transformasi ke dalam bentuk matriks. selanjutnya ubah vektor tf-idf dalam bentuk matriks dengan fungsi todense(). terakhir  lihat matriks tf-idf untuk beberapa judul buku dan kategori buku.

kedua hitung derajat kesamaan (similarity degree) antar buku dengan teknik cosine similarity. menggunakan fungsi cosine_similarity dari library sklearn.  Dengan satu baris kode untuk memanggil fungsi cosine similarity dari library sklearn, kita telah berhasil menghitung kesamaan (similarity) antar buku. dimana menghasilkan keluaran berupa matriks kesamaan dalam bentuk array. Dengan cosine similarity, kita berhasil mengidentifikasi kesamaan antara satu buku dengan buku lainnya.

tahap selanjutnya pembuatan sebuah algoritma untuk melakukan proses rekomendasi dimana proses rekomendasi ini  dengan tf-idf dan cosine similarity akan cara mencari buku yang mirip dengan kategori buku yang diinginkan. Berdasarkan rekomendasi buku yang mirip dengan ‘rage of angel’ dengan kategori buku 'fiction' didapakan top N rekomendasi sebagai berikut

Tabel 0.1 rekomendasi buku dengan kategori fiction
 
|index|title|categories|
|---|---|---|
|0|Fitzgerald: All The Sad Young Men|Fiction|
|1|The Bride Finder|Fiction|
|2|Murder in Foggy Bottom|Fiction|
|3|Wartime Lies|Fiction|
|4|Your Oasis on Flame Lake|Fiction|

 ## Evaluation
pada evaluasi kali ini dilakukan Penerapan metric precision pada evaluasi Content Based Filtering. [[2]](https://www.dicoding.com/academies/319/discussions/134402)

pada tabel 0.1 rekomendasi buku dengan kategori fiction diatas  merupakan hasil rekomendasi buku dengan judul 'rage of angel' yang detailnya sebagai berikut :

tabel 0.2 detail buku  dengan judul ‘rage of angel’ 
|index|title|authors|categories|average\_rating|ratings\_count|
|---|---|---|---|---|---|
|3|Rage of angels|Sidney Sheldon|Fiction|3\.93|29532\.0|

dari hasil rekomendasi di atas diketahui bahwa 'rage of angel' termasuk kedalam kategori buku 'fiction'. dari 5 item yang di rekomendasikan 5 item yang memiliki kategori fiction(similar).
berdasarkan precision formula pada recommender system precison : ![recommender system precision](https://user-images.githubusercontent.com/110774645/191220365-a77c874a-5b7c-4a58-9221-ea44d99cebcb.png)

didapatkan bahwa precission = 5/5, jadi presisinya =  100%. Dari hasil presisi yang ada goals yang di tetapkan sebelumnya terpenuhi karena sistem merekomendasikan item yang mirip dengan item yang ada.
    


**Referenssi yang digunakankan pada saat pengerjaan proyek**
- studi kasus keempat sistem rekomendari [machine learning terapan](https://www.dicoding.com/academies/319/tutorials/17104)
- template laporan [mlt](https://github.com/dicodingacademy/contoh-laporan-mlt/blob/main/format_laporan_submission_1.md)
- Dataset 7k books with metadata [kaggle](https://www.kaggle.com/datasets/dylanjcastillo/7k-books-with-metadata?select=books.csv)
