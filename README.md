# Laporan Proyek Machine Learning - Putu Padmanaba

## Domain Proyek
### Latar belakang
<br>

![air](https://github.com/Padmanaba231/Predictive-Analytic-Update/assets/157343566/6aa8687a-b7fc-4d8d-a98b-1e070d2e52a5) <br>
Gambar 1 penampakan dari bawah laut
<br>
<br>
Pemantauan kualitas air sangat penting untuk melindungi kesehatan manusia dan lingkungan serta mengendalikan kualitas air [[1](https://www.sciencedirect.com/science/article/pii/S2214714422003646)] .Kehidupan manusia tidak pernah lepas akan kebutuhan terhadap air. Terutama air bersih dan air yang layak untuk dikonsumsi. Oleh karena itu, Penyediaan air dan sanitasi yang baik, serta pengelolaan sumber daya air yang baik merupakan hal yang wajib dalam menjaga kualitas air agar bisa digunakan dengan aman oleh masyarakat. Jika tidak diperhatikan dengan benar dan teliti, air tersebut dapat terkontaminasi dan tentunya menyebabkan air tersebut tidak layak dikonsumsi. Air yang terkontaminasi dan sanitasi yang tidak memadai memfasilitasi penularan penyakit seperti kolera, diare, disentri, hepatitis A, tifoid, dan polio [[2](https://dspace.umkt.ac.id/handle/463.2017/1040)] [[3](https://ppjp.ulm.ac.id/journal/index.php/jht/article/view/2883)]. Mereka yang tidak memiliki akses ke air bersih dan sanitasi menghadapi risiko kesehatan yang dapat dicegah. Sehingga pemantauan terhadap kualitas air sangatlah penting untuk terus dipantau. 
<br>
<br>
Kualitas air dipengaruhi oleh beberapa faktor, seperti banyaknya bakteri yang terkandung, tingkat kejernihan air, kandungan amonia yang terkandung, dan masih banyak faktor lainnya. Oleh karena faktor-faktor tersebut, yang juga tersedia pada _dataset_, maka pada proyek ini diharapkan dapat diprediksi layak atau tidaknya air untuk dikonsumsi serta melihat kisaran korelasi dari setiap faktor-faktor tersebut. Kecerdasan Buatan menawarkan peluang besar untuk membantu meningkatkan klasifikasi dan prediksi kualitas air[[1](https://www.sciencedirect.com/science/article/pii/S2214714422003646)]. Banyak cara algoritma yang dapat digunakan dalam kasus ini. Salah satunya adalah algoritma klasifikasi. Pada proyek ini diharapkan dapat membantu dalam memprediksi layak dan tidak layaknya suatu air untuk dikonsumsi dengan cara menggunakan algoritma klasifikasi lalu memasukan faktor-faktor yang mempengaruhi kualitas air.
<br>


## Business Understanding
### Problem Statement
Berdasarkan latar belakang di atas, permasalahan yang didapatkan sebagai berikut:
+ Seberapa pengaruh fitur dalam menentukan kelayakan konsumsi air?
+ Bagaimana cara memproses data agar dapat dilatih dengan baik oleh model?
+ Algoritma apa yang memiliki kinerja paling baik?

### Goals
+ Mengetahui besarnya pengaruh fitur dalam menentukan kelayakan konsusi air
+ Mengetahui cara pemrosesan data agar dapat dilatih dengan baik oleh model
+ Mengetahui model yang memiliki kinerja terbaik

### Solution Steatment
+ Menggunakan hubungan korelasi antar fitur untuk mengetahui pengaruh setiap fitur dalam menentukan kelayakan konsumsi air. 
+ Menerapkan beberapa metode dalam melakukan pemrosesan data seperti menghapus _missing value_ , membagi _dataset_ menjadi data latih dan data pengujian, serta menerapkan _downsampling_ ketika data mengalami ketidakseimbangan
+ Menggunakan lebih dari 1 model yang dapat menyelesaikan masalah klasifikasi. Algoritma yang dipakai adalah _K-Nearest Neighbour_, _Random Forest_, dan _Suport Vector Classification_

# Data Understanding
_dataset_ yang digunakan dalam proyek ini merupakan data yang berisikan beberapa parameter yang digunakan dalam menentukan kualitas air. _dataset_ ini dapat diunduh di [Kaggle: Water Quality]([https://www.kaggle.com/_dataset_s/adityakadiwal/water-potability/data](https://www.kaggle.com/_dataset_s/mssmartypants/water-quality))

Informasi _dataset_:
+ _dataset_ dalam format CSV 
+ _dataset_ ini memiliki 21 fitur dengan 7999 sample
+ Data set memiliki 19 fitur bertipe numerik dan 2 fitur bertipe obyek
+ Terdapat _missing value_ pada _dataset_

### Variable pada _dataset_
+ aluminium: Kadar aluminium dalam air per liter.
+ ammonia: Tingkat amonia dalam air per liter.
+ arsenic: Kadar arsenik dalam air per liter.
+ barium: Kadar barium dalam air per liter.
+ cadmium: Kadar kadmium dalam air per liter.
+ chloramine: Kadar chloramine dalam air per liter.
+ chromium: Level od chromium in water per liter.
+ copper: Level od copper in water per liter.
+ flouride: Tingkat fluorida dalam air per liter.
+ bacteria: Tingkat bakteri dalam air per liter.
+ viruses: Tingkat virus dalam air per liter.
+ lead: Tingkat timbal dalam air dalam ukuran ppm.
+ nitrates: Tingkat nitrat dalam air per liter.
+ nitrites: Tingkat nitrit dalam air per liter.
+ mercury: Tingkat merkuri dalam air dalam ukuran ppm.
+ perchlorate: Tingkat perklorat dalam air per liter.
+ radium: Tingkat radium dalam air per liter.
+ selenium: Tingkat selenium dalam air per liter.
+ silver: Tingkat silver dalam air per liter.
+ uranium: Tingkat uranium dalam air per liter.
+ is_safe: Menunjukan apakah air layak dikonsumsi (1-layak, 0-tidak layak)


### Exploratory Data Analys
#### Mengecek fitur pada _dataset_
Sebelum memproses data dari _dataset_, perlu di cek kembali fitur-fitur yang terdapat pada _dataset_.
![Screenshot 2024-02-26 191251](https://github.com/Padmanaba231/Predictive-Analytic-Update/assets/157343566/449e0d97-7c3f-4f79-8a37-d8ebd8349b7d)
<br> 
Gambar 2.1 Analisis fitur _dataset_
<br>
![Screenshot 2024-02-26 191745](https://github.com/Padmanaba231/Predictive-Analytic-Update/assets/157343566/c9053e29-bd60-4953-8e21-9e716a47bf62)
<br>
Gambar 2.2 Analisis fitur ammonia

<br>
Bisa dilihat pada gambar 2.1 terdapat satu hal yang terasa janggal. Pada fitur ammonia memiliki tipe data obyek. Padahal setelah diperiksa, ternyata fitur ammonia memiliki data tipe numerik. Oleh karena itu, tipe data pada kolom fitur ammonia perlu diubah menjadi data tipe numerik menggunakan fungsi yang telah disediakan oleh pandas yaitu fungsi to_numeric.



#### Missing value
![missing_val](https://github.com/Padmanaba231/Predictive-Analytic-Update/assets/157343566/83762d39-9550-4bf4-b5e7-e24158494cac)
<br>
Gambar 2.3 Analisis _missing value_
<br>
perlu untuk mengecek jumlah _missing value_ yang dimiliki _dataset_. Dengan menggunakan fungsi isnull().sum() untuk mengetahui jumlah _missing value_ dan fitur yang memiliki _missing value_. Terdapat 3 _missing value_ pada _dataset_ yaitu pada fitur ammonia.


#### Persebaran data
![Screenshot 2024-02-22 144156](https://github.com/Padmanaba231/Predictive-Analytic-Update/assets/157343566/1ad74e6b-d70f-4515-8597-5e2d1ea7f2d2)
<br>
Gambar 2.4
<br>
Selanjutnya persebaran pada _dataset_ perlu untuk di cek kembali. Pada gambar 2.4 dapat dilihat bahwa persebaran data terkumpul pada kelas 0 (air tidak layak konsumsi). Jika dibiarkan hal ini dapat menyebabkan bias terhadap model yang akan dibuat. Permasalahan ini nantinya akan diselesaikan pada bagian Data Preparation.
<br>
### Korelasi antar fitur
Kita akan menghitung korelasi antar fitur yang ada menggunakan bantuan metode heatmap correlation. Didapatkan hasil heatmap sebagai berikut:
<br>
![Screenshot 2024-02-22 144950](https://github.com/Padmanaba231/Predictive-Analytic-Update/assets/157343566/b8fe243b-f745-470e-b42a-f59d89545e3a)
<br>
Gambar 2.5
<br>
Berdasarkan gambar 2.5 beberapa fitur mempunyai nilai korelasi yang kuat dengan fitur lainnya. Jika diamati, pasangan fitur yang memiliki nilai korelasi paling besar adalah antara fitur virus dan bakteri. Hal ini dapat diartikan bahwa air yang terindikasi memiliki kandungan virus di dalamnya cenderung juga memiliki kandungan bakteri di dalamnya.

# Data Preparation
### Menangani Missing Value
Seperti yang sudah dijelaskan sebelumnya, pada _dataset_ memiliki 3 _missing value_, yakni pada fitur ammonia. Karena jumlah _missing value_ yang dimiliki sedikit, _missing value_ tersebut dapat dihapus menggunakan fungsi dropna().

### Membagi _dataset_
_Dataset_ akan dibagi_ menjadi data latih dan data uji. Data latih akan digunakan untuk membangun model, sedangkan data uji akan digunakan untuk menguji performa model. Dengan menggunakan metode train_test_split dari liblary sklearn untuk melakukan hal ini. Rasio dari pambagian _dataset_ sebesar 75% untuk data latih dan 25% untuk data uji. Data latih digunakan untuk melatih model sementara data uji digunakan untuk mengevaluasi model. Perlu diperhatikan bahwa pembagian _dataset_ harus dilakukan terlebih dahulu sebelum melakukan standarisasi. Hal ini dilakukan agar tidak terjadi kebocoran informasi pada data uji. Selain itu, ketika ingin menyeimbangkan persebaran data menggunakan metode _downsampling_, dapat menerapkan _downsampling_ pada data latih saja.
<br>

### Balancing data menggunakan resampling
<br>
<div><img src="https://github.com/Padmanaba231/Predictive-Analytic/blob/8e6f181e97942945bd355c3284118a6722e4043a/ML/IMG/1_CeOd_Wbn7O6kpjSTKTIUog.png" width="600"/></div>
<br>
<br>
Seperti yang telah kita ketahui sebelumnya, data kita mengalami ketidakseimbangan. Kita akan menangani hal ini menggunakan metode oversampling dengan bantuan fitur SMOTE. Kita akan mencoba menyeimbangkan _dataset_ dengan meningkatkan ukuran sampel langka. Daripada membuang sampel berlimpah, sampel langka baru dihasilkan dengan menggunakan fitur SMOTE (Sintetis Minoritas Sampling Teknik). Setelah menerapkan metode ini, data kita akan lebih seimbang yang diharapkan dapat meningkatkan kinerja model kita nantinya.

### Standarisasi
Algoritma machine learning cenderung memberikan hasil yang lebih baik dan konvergen lebih cepat ketika data memiliki skala yang seragam atau mendekati distribusi normal. Untuk mencapai ini, proses scaling dan standarisasi sangat membantu dalam mengubah bentuk fitur data sehingga lebih mudah dipahami dan diolah oleh algoritma. Kita akan memanfaatkan fungsi standarisasi yang dimiliki oleh liblary sklearn.

# Modeling
Proyek ini menggunakan 3 algoritma Machine Learning:
1. KNN (K-Nearest Neighbour)
2. SVC (Suport Vector Classification)
3. Random Forest

## KNN
KNN merupakan singkatan dari K-Nearest Neighbor,algoritma ini bekerja dengan prinsip bahwa objek/kelas yang mirip cenderung berada pada jarak yang dekat satu sama lain.Dengan kata lain, data yang memiliki karakteristik serupa akan cenderung saling bertetangga dalam ruang fitur. Hal inilah yang membuat KNN salah satu algoritma yang cocok untuk menyelesaikan kasus klasifikasi. 
#### Tahapan Kerja Umum KNN
+ Memilih jumlah tetangga terdekat (K) yang akan digunakan untuk memutuskan kelas suatu data baru. 
+ Hitung jarak antara data baru yang akan diprediksi dengan setiap titik data dalam set pelatihan. 
+ Menentukan K tetangga berdasarkan jarak terkecil. Ini merupakan data pelatihan yang memiliki nilai atribut paling mirip dengan data baru.
+ Lakukan prehitungan mayoritas di antara tetangga terpilih untuk menentukan kelas dari data baru. Artinya, kelas yang paling umum di antara K tetangga tersebut akan menjadi prediksi kelas untuk data baru.

Pada kasus proyek ini menggunakan <strong>n_neighbors = 25</strong> tetangga. Penentuan nilai <strong>K</strong> sangat berpengaruh pada kinerja model. Setelah mencoba berbagai nilai <strong>K</strong> didapatkan nilai <strong>K</strong> yang terbaik adalah sebesar 25. Untuk parameter yang lain, pada proyek ini menggunakan parameter default

#### Kelebihan & Kekurangan KNN
##### Kelebihan
Algoritma KNN relatif sederhana dan mudah dipahami. Konsep dasarnya cukup simple, yaitu mengambil mayoritas kelas dari tetangga terdekat. Algoritma KNN cocok untuk data non linear karena KNN dapat bekerja dengan baik pada data yang memiliki batas keputusan non-linier atau kompleks.
##### Kekurangan
KNN memerlukan penentuan nilai <strong>K</strong> yang tepat agar model dapat bekerja dengan baik. Nilai <strong>K</strong> yang terlalu kecil dapat menyebabkan model sensitif terhadap noise, sedangkan nilai <strong>K</strong> yang terlalu besar dapat menyebabkan model terlalu halus dan kurang responsif terhadap perubahan lokal dalam data.

## SVC
SVC sebenarnya termasuk kedalam algoritma SVM(Support Vector Machine). SVM merupakan model Machine Learning multifungsi yang dapat digunakan untuk menyelesaikan permasalahan klasifikasi, regresi, dan pendeteksian outlier. Algoritma Support Vector Machine (SVM) bertujuan untuk mengidentifikasi hyperplane optimal dalam ruang berdimensi-N (dengan N fitur) yang dapat efektif memisahkan titik-titik data input secara optimal. Pada kasus klasifikasi menggunakan SVC(Support Vector Classifier).

#### Tahapan Kerja SVC secara umum
+ SVC berupaya menemukan hyperplane yang memisahkan dua atau lebih kelas secara optimal. Hyperplane ini memiliki sifat yang dapat memaksimalkan margin, yaitu jarak antara hyperplane dan titik-titik terdekat dari setiap kelas, yang disebut sebagai Support Vectors.
+ SVM berusaha untuk memaksimalkan margin ini, karena margin yang lebih besar memberikan tingkat kepercayaan yang lebih baik terhadap klasifikasi yang dilakukan oleh model.
+ Ketika data tidak dapat dipisahkan secara linier, SVC menggunakan konsep kernel untuk mentransformasikan data ke ruang fitur yang lebih tinggi. Kernel membantu model SVC menangani kasus-kasus di mana batas keputusan antara kelas tidak dapat dijelaskan secara linear dalam ruang fitur asli.
+ Setelah menemukan hyperplane yang optimal, SVC menggunakan batas keputusan untuk mengklasifikasikan data baru. Data yang berada di satu sisi hyperplane dianggap sebagai satu kelas, sedangkan data di sisi lainnya dianggap sebagai kelas yang berbeda.

Pada proyek ini menggunakan nilai parameter <strong>C</strong> sebesar 5. Parameter C pada model Support Vector Classifier (SVC) menentukan sejauh mana model ini akan memberikan toleransi terhadap kesalahan klasifikasi pada data pelatihan. Parameter ini disebut juga sebagai parameter penalti kesalahan (error penalty) atau parameter keberatan (regularization parameter). Parameter selain parameter <strong>C</strong> menggunakan parameter default SVC.
#### Kelebihan & Kekurangan SVC
##### Kelebihan 
+ SVC dapat bekerja dengan baik bahkan dalam ruang fitur yang memiliki dimensi tinggi, karena mampu menangani kompleksitas data.
+ Melalui penggunaan kernel, SVC dapat menangani data yang tidak dapat dipisahkan secara linier dalam ruang fitur asli(menggunakan kernel).
+ Dengan adanya margin dan fungsi soft margin, SVC dapat menjadi tahan terhadap pengaruh dari data pencilan (outliers).

##### Kekurangan
+ Proses pelatihan pada SVC dapat menjadi komputasi yang intensif, terutama pada _dataset_ besar, karena melibatkan perhitungan jarak dan optimasi yang kompleks.
+ SVC mungkin kurang efisien pada _dataset_ yang sangat besar atau memiliki banyak fitur, karena dapat memerlukan memori yang signifikan dan waktu komputasi yang lebih lama.

## Random Forest
Random Forest merupakan model prediksi yang menggunakan teknik bagging dengan menggabungkan beberapa model untuk bekerja secara kolaboratif. Konsep di balik model ensemble adalah grup model yang bekerja bersama-sama untuk menyelesaikan suatu masalah, yang dapat menghasilkan tingkat keberhasilan yang lebih tinggi daripada model yang beroperasi secara independen. Pada model ensemble, setiap model membuat prediksi secara independen, dan hasil prediksi dari masing-masing model tersebut digabungkan untuk membentuk prediksi akhir.
Teknik bagging ini cocok diterapkan pada algoritma decision tree. Random forest, pada dasarnya, merupakan bentuk bagging dari algoritma decision tree. Anda dapat membayangkan random forest sebagai sebuah tas (bag) yang berisi beberapa model decision tree. Setiap model decision tree memiliki hyperparameter yang berbeda dan dilatih pada subset data yang berbeda. Strategi pembagian data pada algoritma decision tree melibatkan pemilihan acak sejumlah fitur dan sampel dari _dataset_ yang terdiri dari n fitur dan m sampel.
Inilah sebabnya mengapa algoritma ini disebut sebagai random forest, karena terdiri dari banyak pohon keputusan (decision tree) di mana pembagian data dan fitur dilakukan secara acak.

#### Tahapan Umum Random Forest
+ Membangun decision tree untuk setiap subsample data yang telah dipilih. Pada tahap ini, juga dilakukan pemilihan acak sejumlah fitur yang akan digunakan untuk membagi setiap simpul dalam decision tree.
+ Menggunakan setiap decision tree yang telah dibangun untuk membuat prediksi pada data yang tidak terlihat (testing) atau data validasi. Setiap decision tree memberikan prediksi berdasarkan fitur yang dipilih secara acak.
+ Pada tahap ini, hasil prediksi dari setiap decision tree dijumlahkan (voting) jika tugasnya klasifikasi, atau diambil rata-ratanya jika tugasnya regresi. Ini menghasilkan prediksi akhir dari Random Forest.

Pada proyek ini menggunakan nilai parameter <strong>n_estimators=110</strong>, <strong>max_depth=16</strong>, <strong>random_state=126</strong>, <strong>n_jobs=1</strong>. <strong>n_estimators</strong> menentukan jumlah pohon keputusan yang akan dibangun dalam ensemble (hutan). <strong>max_depth</strong>  menentukan kedalaman maksimum dari setiap pohon keputusan dalam ensemble. <strong>random_state=126</strong> menentukan seed untuk menghasilkan angka acak. Sehingga model menghasilkan yang sama setiap dilatih.  <strong>n_jobs=1</strong> menentukan jumlah pekerjaan paralel yang akan digunakan selama pelatihan. Selain parameter diatas menggunakan parameter default.

#### Kelebihan dan Kekurangan Random Forest
##### Kelebihan
Random Forest biasanya memberikan akurasi yang tinggi karena menggabungkan prediksi dari beberapa tree decision yang berbeda. Karena menggunakan banyak pohon keputusan dan mengambil rata-rata atau modus dari prediksi mereka, Random Forest cenderung lebih tahan terhadap overfitting dibandingkan dengan tree dicision tunggal.
##### Kekurangan
Random Forest dapat menghasilkan model yang cukup besar, terutama jika jumlah pohon dan fitur cukup besar. Ini dapat menjadi masalah jika perlu mengoptimalkan penggunaan memori atau mempercepat waktu prediksi.

#### Pemilihan Model
Pada bagian Business Understanding kita ingin mengetahui dan memilih algoritma yang paling baik. Ketiga algoritma yang kita pakai memiliki kelebihan dan kekurangannya masing-masing. Berdasarkan kelebihan dan kelemahan tiap model, pada proyek ini kami memutuskan untuk memilih model <trong>Random Forest</strong> sebagai model terbaik. Hal ini dikarenakan Random Forest membangun banyak pohon keputusan secara parallel dan menggabungkan hasil prediksi mereka. Kemampuan ini membantu dalam menangani keragaman dan kompleksitas data dengan lebih baik daripada model tunggal seperti KNN atau SVM. Selain itu Random Forest dapat menangani _dataset_ dengan jumlah fitur yang besar dan mampu mengatasi fitur-fitur yang tidak teratur atau tidak relevan. Hal ini sesuai dengan _dataset_ kita yang memiliki nilai korelasi yang rendah antar fiturnya. Pada bagian Evaluation nantinya kita akan mengkonfirmasi apakah benar model <trong>Random Forest</strong> merupakan yang terbaik daripada model <trong>KNN</strong> dan juga <trong>SVC</strong>

# Evaluation
Pada Proyek ini menggunakan model machine learning bertipe klasifikasi yang berarti Jika prediksi cocok dengan label kelas sebenarnya, performanya baik. Sedangkan jika tidak, performanya buruk. Secara teknis, perbedaan antara kelas sebenarnya dan kelas yang diprediksi disebut kesalahan klasifikasi. Maka, semua metrik mengukur seberapa kecil nilai kesalahan klasifikasi tersebut. Beberapa metrik yang akan kita gunakan adalah accuracy, precision, recall, f1_score.
<br>
<div><img src="https://github.com/Padmanaba231/Predictive-Analytic/blob/1e5595f91d1606c2a49c3a54ef07b0e140191616/ML/IMG/Screenshot%202024-02-23%20163401.png" width="600"/></div>
<br>
Keterangan:
<br>
<strong>True Positive (TP)</strong>: Jumlah observasi positif yang benar-benar diprediksi sebagai positif oleh model.
<br>
<strong>True Negative (TN)</strong>: Jumlah observasi negatif yang benar-benar diprediksi sebagai negatif oleh model.
<br>
<strong>False Positive (FP)</strong>: Model salah memberi label pada data kategori negatif sebagai positif.
<br>
<strong>False Negative (FP)</strong>: Model salah memberi label pada data kategori positif sebagai negatif.
<br>
<br>
<br>


<strong>Accuracy</strong> mengukur persentase prediksi yang tepat dari total prediksi yang dilakukan. Skor akurasi berkisar antara 0 hingga 1, di mana nilai 1 mencerminkan prediksi yang sempurna, sementara nilai 0 menunjukkan bahwa tidak ada prediksi yang benar.
<br>
<strong>Precision</strong> mengukur rasio prediksi positif yang akurat dari total prediksi positif yang dibuat. Presisi memberikan wawasan tentang seberapa tepat model machine learning dalam membuat prediksi positif. Rentang nilai presisi adalah antara 0 hingga 1, di mana nilai 1 menunjukkan tingkat presisi tertinggi, sementara nilai 0 menandakan ketidakakuratan total dalam prediksi positif. Recall mengukur proporsi data positif yang berhasil diidentifikasi dari total data positif yang sebenarnya. 
<br>
<strong>Recall</strong> memberikan gambaran tentang seberapa efektif model machine learning dalam menemukan semua data positif yang ada. Rentang nilai recall adalah antara 0 hingga 1, di mana nilai 1 mencerminkan kemampuan model dalam menemukan semua data positif, sementara nilai 0 menandakan bahwa model gagal mengidentifikasi data positif. 
<br>
<strong>F1 Score</strong> rata-rata harmonis dari precision dan recall. F1 Score adalah ukuran keseimbangan antara precision dan recall, dengan nilai yang tinggi menunjukkan keseimbangan yang baik antara kedua metrik tersebut.
<br>
<br>
### Hasil Evaluasi Ketiga Model
<br>
<div><img src="https://github.com/Padmanaba231/Predictive-Analytic/blob/c5ffe142a2d8d6a05d8b9edb7ef60b7e48f4f64c/ML/IMG/Screenshot%202024-02-23%20165515.png" width="600"/></div>
<br>
<br>

Dari tabel di atas kita bisa melihat bahwa ketiga model memiliki nilai evaluasi yang cukup kecil. Padalah ketiga model tersebut sangat cocok digunakan pada kasus ini yakni kasus klasifikasi. Hal ini mungkin disebabkan korelasi antar fitur pada _dataset_ yang rendah, mengakibatkan evaluasi model yang rendah juga. Dari tabel tersebut kita juga mendapatkan informasi bahwa model <trong>Random Forest</strong> memiliki nilai evaluasi yang paling tinggi. Ini berarti pernyataan kita sebelumnya bahwa <trong>Random Forest</strong> merupakan model terbaik diantara model lain yang kita gunakan adalah benar.


## Kesimpulan 
Berdasarkan dari apa yang telah kita lakukan selama ini, kita dapat menjawab semua dari problem statement yang kita nyatakan sebelumnya. Pertama, pengaruh fitur pada _dataset_ dalam menentukan kelayakan konsumsi air terbilang rendah. Hal ini dikarenakan korelasi antar fitur pada _dataset_ memiliki nilai yang rendah. Hal ini juga didukung oleh fakta bahwa ketiga model memiliki niali evaluasi yang relatif rendah terhadap _dataset_ yang kita gunakan. Kedua, cara yang kita gunakan agar data dapat dilatih dengan baik oleh model dengan beberapa metode. Mulai dari menangani missing value, membagi _dataset_ menjadi data latih dan data uji, menangani ketidakseimbangan data menggunakan metode oversampling, hingga melakukan standarisasi pada data. Ketiga, algoritma yang memiliki kinerja paling baik terhadap _dataset_ yang kita miliki adalah algoritma <trong>Random Forest</strong>. Hal ini dibuktikan <trong>Random Forest</strong> memiliki nilai evaluasi tertinggi diantara model lainnya.


![1_CeOd_Wbn7O6kpjSTKTIUog](https://github.com/Padmanaba231/Predictive-Analytic/assets/157343566/17a3c212-31a6-4e85-99df-8dbbd58450a2)










