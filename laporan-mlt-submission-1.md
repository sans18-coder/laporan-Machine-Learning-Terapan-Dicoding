# Laporan Proyek Machine Learning - Iksan Wijaya

## Domain Proyek - Pendidikan

### Latar Belakang
  
  Di tengah persaingan dunia kerja yang semakin ketat akibat globalisasi, sertifikasi profesi menjadi indikator penting dalam menilai kompetensi seseorang di berbagai bidang [1](https://proceeding.unnes.ac.id/snpasca/article/view/281). Sertifikasi ini tidak hanya meningkatkan kredibilitas dan daya saing individu, tetapi juga memberikan kepastian bagi pemberi kerja terkait kemampuan serta pengetahuan calon karyawan [2](https://jimfeb.ub.ac.id/index.php/jimfeb/article/view/6853). Dengan demikian, sertifikasi profesional berperan sebagai bukti resmi atas keterampilan yang dimiliki, sehingga dapat memperbesar peluang kerja dan pengembangan karier.

  Namun, proses memperoleh sertifikasi tidaklah mudah. Asesor memiliki peran penting dalam menilai kompetensi peserta untuk memastikan bahwa mereka benar-benar memenuhi standar yang ditetapkan. Penilaian ini mencakup berbagai aspek, seperti pemahaman teori, keterampilan praktis, dan pengalaman kerja. Seiring bertambahnya jumlah peserta dan semakin kompleksnya kriteria penilaian, tantangan bagi asesor juga meningkat [3](https://stiemmamuju.e-journal.id/FJIIM/article/download/115/70). Hal ini dapat menimbulkan potensi ketidakkonsistenan dan subjektivitas dalam proses penilaian, yang pada akhirnya dapat mempengaruhi keadilan serta akurasi hasil sertifikasi.

<br>

## Business Understanding

### Problem Statements

Menjelaskan pernyataan masalah latar belakang:

- Bagaimana penggunaan algoritma Neural Network dapat meningkatkan akurasi dan konsistensi dalam prediksi penilaian sertifikasi?

- Bagaimana pemanfaatan riwayat belajar peserta dapat mengurangi subjektivitas dalam penilaian asesor?

- Bagaimana sistem berbasis Neural Network dapat diintegrasikan ke dalam proses sertifikasi untuk meningkatkan efisiensi dan efektivitas penilaian?

### Goals

Menjelaskan tujuan dari pernyataan masalah:

- Mengimplementasikan algoritma Neural Network untuk meningkatkan akurasi dan konsistensi penilaian sertifikasi.

- Mengurangi subjektivitas dalam penilaian asesor dengan menganalisis riwayat belajar peserta.

- Mengembangkan sistem prediksi berbasis Neural Network yang dapat diterapkan dalam sertifikasi profesi guna meningkatkan efisiensi dan efektivitas proses penilaian.


#### Solution Statements

Solusi yang dapat dilakukan untuk memenuhi tujuan dari proyek ini diantaranya:

- Untuk pra-pemrosesan data dapat dilakukan beberapa teknik, diantaranya :

  - Melakukan _drop_ pada kolom `Unnamed: 0`, `NAME`, `USER_ID`.
  - Mengatasi masalah data yang kosong dengan median.
  - Melakukan pembagian dataset menjadi dua bagian dengan rasio 80% untuk data latih dan 20% untuk data uji.
  - Melakukan _Standard Scaler_.

- Untuk pembuatan model dipilih penggunaan model dengan algoritma Multi-Layer Perceptron dan K-Nearest Neighbor. Algoritma tersebut dipilih karena mudah digunakan dan juga cocok untuk kasus ini. Berikut cara kerja, kelebihan dan kekurangan algoritma Multi-Layer Perceptron dan K-Nearest Neighbor:
  - Cara kerja Algoritma Multi-Layer Perceptron (MLP) [4](https://ejurnal.stmik-budidarma.ac.id/index.php/mib/article/view/2035):

    - Gunakan dataset untuk membangun model MLP.
    - Proses feedforward dilakukan dengan mengalirkan data dari lapisan input ke lapisan tersembunyi hingga mencapai lapisan output.
    - Proses backpropagation digunakan untuk menyesuaikan bobot berdasarkan selisih antara prediksi dan nilai aktual.
    - Iterasi feedforward dan backpropagation dilakukan berkali-kali pada dataset pelatihan hingga model mencapai kinerja yang optimal.
  - Kelebihan dan kekurangan Algoritma Multi-Layer Perceptron (MLP) [5](http://publication.petra.ac.id/index.php/teknik-informatika/article/view/10496):

    - Kelebihan:
      - MLP mampu menangani hubungan non-linear dalam data, sehingga cocok untuk masalah yang lebih kompleks.
      - Mampu belajar dari data dan meningkatkan kinerja seiring waktu tanpa perlu pemrograman eksplisit.
    - Kekurangan:
      - Proses training membutuhkan waktu yang lebih lama dibanding algoritma yang lebih sederhana.
      - Sulit untuk memahami bagaimana model MLP membuat keputusan, sehingga kurang interpretatif.
  - Cara kerja Algoritma K-Nearest Neighbor (KNN) [[6]](https://publikasi.dinus.ac.id/index.php/jais/article/view/1189/):

    - Menentukan jumlah tetangga terdekat K.
    - Menghitung jarak antara data uji dan seluruh data latih menggunakan metrik jarak (misalnya Euclidean Distance).
    - Mengurutkan data berdasarkan jarak terkecil.
    - Menentukan kelas data uji berdasarkan mayoritas label dari K tetangga terdekat.
  - Kelebihan dan kekurangan Algoritma K-Nearest Neighbor (KNN) [[7]](https://simdos.unud.ac.id/uploads/file_penelitian_1_dir/721bdb509a6f0bb9ccca6d7374b86759.pdf):

    - Kelebihan:
      - Algoritma KNN tangguh terhadap data latih yang noisy.
      - Efektif apabila data latih berukuran besar dan memiliki distribusi yang baik.
    - Kekurangan:
      - Perlu menentukan nilai parameter K yang optimal.
      - Sensitif terhadap pemilihan metrik jarak, karena tidak semua jenis jarak cocok untuk setiap dataset.
      - Biaya komputasi cukup tinggi karena harus menghitung jarak dari setiap sampel uji ke semua sampel latih.

<br>

## Data Understanding
---

![Image of Dataset](https://i.postimg.cc/wvJvn0n2/image.png)

Informasi dataset dapat dilihat pada tabel dibawah ini:
Jenis | Keterangan
--- | ---
Sumber | [Kaggle Dataset : Tech-Student Profile Prediction](https://www.kaggle.com/datasets/scarecrow2020/tech-students-profile-prediction/data)
Lisensi | Data files © Original Authors
Kategori | Education, Multiclass Classification, Clustering
Jenis dan Ukuran Berkas | CSV (2.08 MB)

DataFrame ini memiliki 20.000 baris data dan 16 kolom. Terdapat beberapa tipe data yang digunakan, yaitu:

* float64: HOURS_DATASCIENCE, HOURS_BACKEND, HOURS_FRONTEND,  NUM_COURSES_BEGINNER_DATASCIENCE, NUM_COURSES_BEGINNER_BACKEND, NUM_COURSES_BEGINNER_FRONTEND, NUM_COURSES_ADVANCED_DATASCIENCE, NUM_COURSES_ADVANCED_BACKEND, NUM_COURSES_ADVANCED_FRONTEND, AVG_SCORE_DATASCIENCE, AVG_SCORE_BACKEND, AVG_SCORE_FRONTEND
* int64: Unnamed, USER_ID
* object: NAME, PROFILE

> DataFrame ini masih memiliki nilai null (missing values) yang perlu ditangani sebelum dilakukan analisis atau pemodelan lebih lanjut.

---

Pada berkas yang diuduh yakni dataset-tortuga.csv berisi 20000 baris dan 16 kolom. untuk penjelasan mengenai variabel-variabel pada dataset ini dapat dilihat sebagai berikut:

- Unnamed: 0: Kolom indeks yang dibuat secara otomatis saat membaca data dari file (misalnya, CSV). Kolom ini mungkin tidak memiliki arti khusus dan bisa diabaikan atau dihapus jika tidak diperlukan.
- NAME: Nama pengguna atau peserta, bisa berupa nama lengkap atau nama panggilan.
- USER_ID: ID unik pengguna sebagai pengenal dalam dataset.
- HOURS_DATASCIENCE: Total waktu yang dihabiskan untuk belajar atau mengikuti kursus data science.
- HOURS_BACKEND: Total waktu yang dihabiskan untuk belajar atau mengikuti kursus pengembangan backend.
- HOURS_FRONTEND: Total waktu yang dihabiskan untuk belajar atau mengikuti kursus pengembangan frontend.
- NUM_COURSES_BEGINNER_DATASCIENCE: Jumlah kursus tingkat pemula yang diikuti dalam bidang data science.
- NUM_COURSES_BEGINNER_BACKEND: Jumlah kursus tingkat pemula yang diikuti dalam bidang pengembangan backend.
- NUM_COURSES_BEGINNER_FRONTEND: Jumlah kursus tingkat pemula yang diikuti dalam bidang pengembangan frontend.
- NUM_COURSES_ADVANCED_DATASCIENCE: Jumlah kursus tingkat lanjutan yang diikuti dalam bidang data science.
- NUM_COURSES_ADVANCED_BACKEND: Jumlah kursus tingkat lanjutan yang diikuti dalam bidang pengembangan backend.
- NUM_COURSES_ADVANCED_FRONTEND: Jumlah kursus tingkat lanjutan yang diikuti dalam bidang pengembangan frontend.
- AVG_SCORE_DATASCIENCE: Skor rata-rata yang diperoleh dalam kursus terkait data science.
- AVG_SCORE_BACKEND: Skor rata-rata yang diperoleh dalam kursus terkait pengembangan backend.
- AVG_SCORE_FRONTEND: Skor rata-rata yang diperoleh dalam kursus terkait pengembangan frontend.
- PROFILE: Profil pengguna, yang bisa berupa deskripsi singkat, tingkat keahlian, atau kategori berdasarkan pola pembelajaran mereka.

- Men-drop kolom `Unnamed: 0`, `NAME`, `USER_ID`
  ![image](https://github.com/user-attachments/assets/cbce6ac4-f189-4839-9241-850a049c9093)
- Menampilkan kolom unik <br />
  ![image](https://github.com/user-attachments/assets/6c645f7f-6b69-42f6-b660-77d7474763f1)
- Menghapus kolom `PROFILE` sehingga menyisakan kolom untuk analisis lebih lanjut <br />
  ![image](https://github.com/user-attachments/assets/f4c09fc8-144a-44f0-a624-e95d63d1b07a)
- Men-check missing value pada setiap kolom <br />
  ![image](https://github.com/user-attachments/assets/d077b228-216f-400d-911e-4c313e865be8)


## Data Preparation
Berikut adalah tahapan-tahapan dalam melakukan pra-pemrosesan data:

- Menangani Nilai yang Hilang: Data yang memiliki nilai hilang diatasi dengan menggantinya menggunakan median dari setiap kolom. Langkah ini dilakukan agar tidak ada data yang hilang yang dapat mengganggu proses pelatihan model.
  ![image](https://github.com/user-attachments/assets/e1913182-7c7e-4538-9a28-706bd41e1384)
- Membagi Dataset: Dataset dibagi menjadi dua bagian:

    * Data latih (80%) – Digunakan untuk melatih model machine learning.
    * Data uji (20%) – Digunakan untuk mengukur kinerja model pada data yang belum pernah dilihat sebelumnya. Pembagian ini bertujuan untuk mencegah overfitting dan memastikan model dapat bekerja dengan baik pada data baru.
  ![image](https://github.com/user-attachments/assets/cc5e77b0-992f-4946-8f23-cfe0e6f9195b)
- Standardisasi Fitur: Semua fitur dalam data latih dan data uji dinormalisasi sehingga memiliki rata-rata 0 dan standar deviasi 1. Standardisasi ini penting untuk algoritma seperti K-Nearest Neighbors dan Neural Network karena dapat membantu model belajar lebih baik dan meningkatkan performanya.
  ![image](https://github.com/user-attachments/assets/00773410-b274-4650-8f80-3b2653bfac7d)
- Pemisahan Fitur dan Target: Dataset dipisahkan menjadi fitur (X) dan target (y) untuk data latih maupun data uji. Fitur digunakan sebagai input bagi model, sedangkan target merupakan nilai yang akan diprediksi oleh model.
  ![image](https://github.com/user-attachments/assets/b04edd32-9223-4b31-8339-103a83676ce8)

## Modeling

Setelah dilakukan pra-pemrosesan pada dataset, langkah selanjutnya adalah modeling terhadap data. Pada tahap ini menggunakan 2 algoritma yaitu K-Nearest Neighbor (KNN) dan Neural Network (NN) dengan tanpa parameter tambahan. Pertama-tama kedua model ini dilatih menggunakan data latih. Setelah itu kedua model akan diuji dengan data uji. Terakhir kedua model akan diukur nilai akurasinya. Perbandingan hasil dari kedua model akan dianalisis untuk menentukan algoritma terbaik.

Perbandingan Hasil dari kedua model sebagai berikut:<br />
![image](https://github.com/user-attachments/assets/44134961-d8b1-440a-8e5a-720ff53481a2)


- _Confussion Matrix_ algoritma K-Nearest Neighbor:<br />
  ![image](https://github.com/user-attachments/assets/007b5792-56cb-4af8-bfae-f9770c87b019)

- _Confussion Matrix_ algoritma Multi-Layer Perceptron:<br />
  ![image](https://github.com/user-attachments/assets/e2d1c0f2-6523-4661-9d5a-ff930df71cf6)


### Cara Kerja Algoritma KNN:

KNN adalah algoritma klasifikasi yang bekerja berdasarkan prinsip "majority vote" atau suara terbanyak dari tetangga terdekat. Ketika ada data baru yang perlu diklasifikasikan, algoritma ini akan:

Mengukur Jarak: Menghitung jarak antara data baru tersebut dengan semua data yang sudah ada di dataset pelatihan. Jarak ini bisa diukur dengan berbagai metode, seperti Euclidean distance, Manhattan distance, atau lainnya.
Menemukan Tetangga Terdekat: Mengidentifikasi sejumlah 'K' data dari dataset pelatihan yang memiliki jarak terdekat dengan data baru tersebut. 'K' ini adalah parameter yang perlu ditentukan sebelumnya.
Melakukan Voting: Melihat label kelas dari 'K' tetangga terdekat tersebut. Label kelas yang paling banyak muncul di antara tetangga-tetangga ini akan menjadi label kelas yang diberikan kepada data baru tersebut.
Parameter yang Digunakan:

Pada laporan klasifikasi yang ditampilkan, terlihat bahwa model KNN menggunakan parameter n_neighbors=5. Artinya, algoritma ini akan mempertimbangkan 5 tetangga terdekat untuk melakukan voting dan menentukan kelas dari data baru.

* Kelebihan KNN:
  * Sederhana dan mudah dipahami.
  * Tidak memerlukan asumsi tentang distribusi data (non-parametric).
  * Dapat digunakan untuk klasifikasi maupun regresi.

* Kekurangan KNN:
  * Bisa menjadi lambat jika dataset pelatihan sangat besar karena harus menghitung jarak dengan semua data.
  * Sensitif terhadap fitur yang tidak relevan atau memiliki skala yang berbeda-beda.
  * Memerlukan pemilihan nilai 'K' yang tepat, yang bisa mempengaruhi performa model.

### Cara Kerja Algoritma MLP:

* MLP terdiri dari beberapa lapisan neuron yang saling terhubung:

  * Lapisan Input: Menerima data masukan (fitur-fitur yang digunakan untuk klasifikasi).
  * Lapisan Tersembunyi: Terdiri dari satu atau lebih lapisan neuron yang melakukan transformasi non-linear pada data masukan. Setiap neuron di lapisan ini menerima input dari lapisan sebelumnya, melakukan pemrosesan dengan fungsi aktivasi, dan meneruskan output ke lapisan berikutnya.
  * Lapisan Output: Menghasilkan prediksi kelas. Jumlah neuron di lapisan ini biasanya sama dengan jumlah kelas yang mungkin.
Proses pembelajaran MLP melibatkan penyesuaian bobot koneksi antar neuron untuk meminimalkan kesalahan prediksi pada data pelatihan. Ini dilakukan dengan algoritma optimasi seperti backpropagation dan gradient descent.

* Parameter yang Digunakan:
  * `hidden_layer_sizes=(128, 64, 32)`: Menentukan arsitektur jaringan dengan 3 lapisan tersembunyi yang memiliki masing masing 128, 64, dan 32 neuron.
  * `solver='adam'`: Menggunakan algoritma optimasi Adam untuk melatih model.
  * `max_iter=500`: Menetapkan jumlah maksimum iterasi (epoch) selama pelatihan.

## Evaluation

* Metrik Evaluasi <br />
  Dalam analisis ini, beberapa metrik evaluasi digunakan untuk menilai kinerja model K-Nearest Neighbors (KNN) dan Multi-Layer Perceptron (MLP):

  * Akurasi: Mengukur proporsi prediksi yang benar dari keseluruhan prediksi.
  * Presisi: Mengukur proporsi prediksi positif yang benar dari keseluruhan prediksi positif.
  * Recall: Mengukur proporsi prediksi positif yang benar dari keseluruhan sampel yang sebenarnya positif.
  * F1-score: Merupakan rata-rata harmonik antara presisi dan recall, memberikan keseimbangan antara keduanya.

* Evaluasi Metrik <br />
Berdasarkan laporan klasifikasi, model Multi-Layer Perceptron (MLP) menunjukkan kinerja yang sedikit lebih baik dibandingkan K-Nearest Neighbors (KNN) dalam hal akurasi keseluruhan:
  * Akurasi MLP: 0.9527
    ![image](https://github.com/user-attachments/assets/ebcce84c-0048-4b69-aa21-82994c5cc740)

  * Akurasi KNN: 0.9270
  ![image](https://github.com/user-attachments/assets/155ec117-e547-4008-8227-fcf96690dde4)

  Selain itu, MLP juga memiliki presisi, recall, dan F1-score yang lebih tinggi atau setara untuk sebagian besar kelas dibandingkan dengan KNN. Hal ini menunjukkan bahwa MLP lebih efektif dalam mengidentifikasi kelas dengan benar serta mengurangi kesalahan klasifikasi.
  
* Evaluasi terhadap Business Understanding<br />
  * Prediksi penilaian yang lebih akurat dan konsisten:
Model KNN dan MLP, dengan akurasi di atas 90%, menunjukkan kemampuan yang cukup baik dalam menghasilkan prediksi yang akurat. Dengan performa yang lebih stabil, model ini berpotensi memberikan hasil yang lebih andal dibandingkan metode penilaian tradisional yang bisa dipengaruhi oleh subjektivitas dan perbedaan penilaian antar asesor.
  * Mengurangi subjektivitas dalam penilaian:
Meskipun model ini tidak sepenuhnya menghilangkan subjektivitas asesor, mereka dapat memberikan informasi objektif berdasarkan riwayat pembelajaran peserta. Informasi ini dapat membantu asesor dalam mengambil keputusan yang lebih akurat dan mengurangi potensi bias yang mungkin muncul dalam penilaian manual.
  * Meningkatkan efisiensi dan efektivitas penilaian:
Dengan mengotomatiskan sebagian proses penilaian, sistem prediksi dapat mempercepat sertifikasi peserta. Hal ini memungkinkan asesor untuk lebih fokus pada tugas yang lebih kompleks, seperti memberikan umpan balik yang lebih mendalam atau mengembangkan materi pelatihan. Dengan demikian, model ini berpotensi meningkatkan efisiensi dan efektivitas keseluruhan dalam proses penilaian.
