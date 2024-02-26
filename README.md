# Laporan Proyek Machine Learning - Putu Padmanaba

## Domain Proyek
### Latar belakang
<br>

![air](https://github.com/Padmanaba231/Predictive-Analytic-Update/assets/157343566/6aa8687a-b7fc-4d8d-a98b-1e070d2e52a5) <br>
Gambar 1 penampakan dari bawah laut
<br>
<br>
Pemantauan kualitas air sangat penting untuk melindungi kesehatan manusia dan lingkungan serta mengendalikan kualitas air [[1](https://www.sciencedirect.com/science/article/pii/S2214714422003646)] .Kehidupan manusia tidak pernah lepas akan kebutuhan terhadap air. Terutama air bersih dan air yang layak untuk dikonsumsi. Oleh karena itu, Penyediaan air dan sanitasi yang baik, serta pengelolaan sumber daya air yang baik merupakan hal yang wajib dalam menjaga kualitas air agar bisa digunakan dengan aman oleh masyarakat. Jika tidak diperhatikan dengan benar dan teliti, air tersebut dapat terkontaminasi dan tentunya menyebabkan air tersebut tidak layak dikonsumsi. Air yang terkontaminasi dan sanitasi yang tidak memadai memfasilitasi penularan penyakit seperti kolera, diare, disentri, hepatitis A, tifoid, dan polio [[2](https://journal.universitaspahlawan.ac.id/index.php/prepotif/article/view/13459)]. Mereka yang tidak memiliki akses ke air bersih dan sanitasi menghadapi risiko kesehatan yang dapat dicegah. Sehingga pemantauan terhadap kualitas air sangatlah penting untuk terus dipantau. 
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
<br>
Bisa dilihat pada gambar 2.1 terdapat satu hal yang terasa janggal. Pada fitur ammonia memiliki tipe data obyek. Padahal setelah diperiksa, ternyata fitur ammonia memiliki data tipe numerik. Oleh karena itu, tipe data pada kolom fitur ammonia perlu diubah menjadi data tipe numerik menggunakan fungsi yang telah disediakan oleh pandas yaitu fungsi to_numeric.



#### Missing value
![missing_val](https://github.com/Padmanaba231/Predictive-Analytic-Update/assets/157343566/83762d39-9550-4bf4-b5e7-e24158494cac)
<br>
Gambar 2.3 Analisis _missing value_
<br><br>
perlu untuk mengecek jumlah _missing value_ yang dimiliki _dataset_. Dengan menggunakan fungsi isnull().sum() untuk mengetahui jumlah _missing value_ dan fitur yang memiliki _missing value_. Terdapat 3 _missing value_ pada _dataset_ yaitu pada fitur ammonia.


#### Persebaran data
![Persebaran data](https://github.com/Padmanaba231/Predictive-Analytic-Update/assets/157343566/46d650ec-cf0f-42f3-9b41-89efab88f0ff)

<br>
Gambar 2.4
<br><br>
Selanjutnya persebaran pada _dataset_ perlu untuk di cek kembali. Pada gambar 2.4 dapat dilihat bahwa persebaran data terkumpul pada kelas 0 (air tidak layak konsumsi). Jika dibiarkan hal ini dapat menyebabkan bias terhadap model yang akan dibuat. Permasalahan ini nantinya akan diselesaikan pada bagian Data Preparation.
<br>

### Korelasi antar fitur

Menghitung korelasi antar fitur yang ada menggunakan bantuan metode heatmap correlation. Didapatkan hasil heatmap sebagai berikut:
<br>
![korelasi](https://github.com/Padmanaba231/Predictive-Analytic-Update/assets/157343566/024518f4-8b5b-4ed6-9929-1a8fa612af56)
<br>
Gambar 2.5
<br><br>
Berdasarkan gambar 2.5 beberapa fitur mempunyai nilai korelasi yang kuat dengan fitur lainnya. Jika diamati, pasangan fitur yang memiliki nilai korelasi paling besar adalah antara fitur virus dan bakteri. Hal ini dapat diartikan bahwa air yang terindikasi memiliki kandungan virus di dalamnya cenderung juga memiliki kandungan bakteri di dalamnya.

# Data Preparation
### Menangani Missing Value
Seperti yang sudah dijelaskan sebelumnya, pada _dataset_ memiliki 3 _missing value_, yakni pada fitur ammonia. Karena jumlah _missing value_ yang dimiliki sedikit, _missing value_ tersebut dapat dihapus menggunakan fungsi dropna().

### Membagi _dataset_
_Dataset_ akan dibagi_ menjadi data latih dan data uji. Data latih akan digunakan untuk membangun model, sedangkan data uji akan digunakan untuk menguji performa model. Dengan menggunakan metode train_test_split dari liblary sklearn untuk melakukan hal ini. Rasio dari pambagian _dataset_ sebesar 75% untuk data latih dan 25% untuk data uji. Data latih digunakan untuk melatih model sementara data uji digunakan untuk mengevaluasi model. Perlu diperhatikan bahwa pembagian _dataset_ harus dilakukan terlebih dahulu sebelum melakukan standarisasi. Hal ini dilakukan agar tidak terjadi kebocoran informasi pada data uji. Selain itu, ketika ingin menyeimbangkan persebaran data menggunakan metode _undersampling_, dapat menerapkan _undersampling_ pada data latih saja.
<br>

### Balancing data menggunakan _undersampling_
<br>

![RESAMPLING](https://github.com/Padmanaba231/Predictive-Analytic-Update/assets/157343566/f89460af-2109-4ecc-af09-680c474a7b74)
<br>
Gsmbar 3.1
<br><br>
Seperti yang telah diketahui sebelumnya, data mengalami ketidakseimbangan.Permasalahan ini akan diselesaikan dengan metode _undersampling_. Dengan cara menyeimbangkan _dataset_ dengan mengurangi jumlah sampel pelatihan yang berada di bawah kelas mayoritas. Walau akan kehilangan beberapa informasi jika menggunakan metode ini, data yang dimiliki tetap termasuk banyak. Jumlah data setelah menerapkan metodei ini sebesar 1824 data.

### Standarisasi
Algoritma _machine learning_ cenderung memberikan hasil yang lebih baik dan konvergen lebih cepat ketika data memiliki skala yang seragam atau mendekati distribusi normal. Untuk mencapai ini, proses _scaling_ dan standarisasi sangat membantu dalam mengubah bentuk fitur data sehingga lebih mudah dipahami dan diolah oleh algoritma. Pada proyek ini akan memanfaatkan fungsi standarisasi yang dimiliki oleh liblary sklearn.

# Modeling
Proyek ini menggunakan 3 algoritma Machine Learning:
1. KNN
2. SVC
3. _Random Forest_

## KNN
KNN merupakan singkatan dari _K-Nearest Neighbor_,algoritma ini bekerja dengan prinsip bahwa objek/kelas yang mirip cenderung berada pada jarak yang dekat satu sama lain.Dengan kata lain, data yang memiliki karakteristik serupa akan cenderung saling bertetangga dalam ruang fitur. Hal inilah yang membuat KNN salah satu algoritma yang cocok untuk menyelesaikan kasus klasifikasi. 
#### Tahapan Kerja Umum KNN
+ Memilih jumlah tetangga terdekat (K) yang akan digunakan untuk memutuskan kelas suatu data baru. 
+ Hitung jarak antara data baru yang akan diprediksi dengan setiap titik data dalam set pelatihan. 
+ Menentukan K tetangga berdasarkan jarak terkecil. Ini merupakan data pelatihan yang memiliki nilai atribut paling mirip dengan data baru.
+ Lakukan prehitungan mayoritas di antara tetangga terpilih untuk menentukan kelas dari data baru. Artinya, kelas yang paling umum di antara K tetangga tersebut akan menjadi prediksi kelas untuk data baru.

Pada kasus proyek ini menggunakan <strong>_n_neighbors_ = 25</strong> tetangga. Penentuan nilai <strong>K</strong> sangat berpengaruh pada kinerja model. Setelah mencoba berbagai nilai <strong>K</strong> didapatkan nilai <strong>K</strong> yang terbaik adalah sebesar 25. Untuk parameter yang lain, pada proyek ini menggunakan parameter _default_

#### Kelebihan & Kekurangan KNN
##### Kelebihan
Algoritma KNN relatif sederhana dan mudah dipahami. Konsep dasarnya cukup mudah, yaitu mengambil mayoritas kelas dari tetangga terdekat. Algoritma KNN cocok untuk data non linear karena KNN dapat bekerja dengan baik pada data yang memiliki batas keputusan _non-linier_ atau kompleks.
##### Kekurangan
KNN memerlukan penentuan nilai <strong>K</strong> yang tepat agar model dapat bekerja dengan baik. Nilai <strong>K</strong> yang terlalu kecil dapat menyebabkan model sensitif terhadap noise, sedangkan nilai <strong>K</strong> yang terlalu besar dapat menyebabkan model terlalu halus dan kurang responsif terhadap perubahan lokal dalam data.

## SVC
SVC sebenarnya termasuk kedalam algoritma SVM(_Support Vector Machine_). SVM merupakan model Machine Learning multifungsi yang dapat digunakan untuk menyelesaikan permasalahan klasifikasi, regresi, dan pendeteksian _outlier_. Algoritma _Support Vector Machine_ (SVM) bertujuan untuk mengidentifikasi _hyperplane_ optimal dalam ruang berdimensi-N (dengan N fitur) yang dapat efektif memisahkan titik-titik data _input_ secara optimal. Pada kasus klasifikasi menggunakan SVC(_Support Vector Classifier_).

#### Tahapan Kerja SVC secara umum
+ SVC berupaya menemukan _hyperplane_ yang memisahkan dua atau lebih kelas secara optimal. _Hyperplane_ ini memiliki sifat yang dapat memaksimalkan _margin_, yaitu jarak antara _hyperplane_ dan titik-titik terdekat dari setiap kelas, yang disebut sebagai _Support Vectors_.
+ SVM berusaha untuk memaksimalkan _margin_, karena _margin_ yang lebih besar memberikan tingkat kepercayaan yang lebih baik terhadap klasifikasi yang dilakukan oleh model.
+ Ketika data tidak dapat dipisahkan secara linier, SVC menggunakan konsep _kernel_ untuk mentransformasikan data ke ruang fitur yang lebih tinggi. _Kernel_ membantu model SVC menangani kasus-kasus di mana batas keputusan antara kelas tidak dapat dijelaskan secara linear dalam ruang fitur asli.
+ Setelah menemukan _hyperplane_ yang optimal, SVC menggunakan batas keputusan untuk mengklasifikasikan data baru. Data yang berada di satu sisi _hyperplane_ dianggap sebagai satu kelas, sedangkan data di sisi lainnya dianggap sebagai kelas yang berbeda.

Pada proyek ini menggunakan nilai parameter <strong>C</strong> sebesar 5. Parameter C pada model _Support Vector Classifier_ (SVC) menentukan sejauh mana model ini akan memberikan toleransi terhadap kesalahan klasifikasi pada data pelatihan. Parameter ini disebut juga sebagai parameter penalti kesalahan (_error penalty_) atau parameter keberatan (_regularization parameter_). Parameter selain parameter <strong>C</strong> menggunakan parameter _default_ SVC.
#### Kelebihan & Kekurangan SVC
##### Kelebihan 
+ SVC dapat bekerja dengan baik bahkan dalam ruang fitur yang memiliki dimensi tinggi, karena mampu menangani kompleksitas data.
+ Melalui penggunaan _kernel_, SVC dapat menangani data yang tidak dapat dipisahkan secara linier dalam ruang fitur asli.
+ Dengan adanya _margin_ dan fungsi _soft margin_, SVC dapat menjadi tahan terhadap pengaruh dari data pencilan (_outliers_).

##### Kekurangan
+ Proses pelatihan pada SVC dapat menjadi komputasi yang intensif, terutama pada _dataset_ besar, karena melibatkan perhitungan jarak dan optimasi yang kompleks.
+ SVC mungkin kurang efisien pada _dataset_ yang sangat besar atau memiliki banyak fitur, karena dapat memerlukan memori yang signifikan dan waktu komputasi yang lebih lama.

## _Random Forest_
_Random Forest_ merupakan model prediksi yang menggunakan teknik bagging dengan menggabungkan beberapa model untuk bekerja secara kolaboratif. Konsep di balik model ensemble adalah grup model yang bekerja bersama-sama untuk menyelesaikan suatu masalah, yang dapat menghasilkan tingkat keberhasilan yang lebih tinggi daripada model yang beroperasi secara independen. Pada model ensemble, setiap model membuat prediksi secara independen, dan hasil prediksi dari masing-masing model tersebut digabungkan untuk membentuk prediksi akhir. Teknik bagging ini cocok diterapkan pada algoritma _decision tree_. _Random Forest_, pada dasarnya, merupakan bentuk bagging dari algoritma _decision tree_.Dapat dibayangkan _Random Forest_ sebagai sebuah tas yang berisi beberapa model _decision tree_. Setiap model _decision tree_ memiliki _hyperparameter_ yang berbeda dan dilatih pada subset data yang berbeda. Strategi pembagian data pada algoritma decision tree melibatkan pemilihan acak sejumlah fitur dan sampel dari _dataset_ yang terdiri dari n fitur dan m sampel. Inilah sebabnya mengapa algoritma ini disebut sebagai _Random Forest_, karena terdiri dari banyak pohon keputusan (_decision tree_) di mana pembagian data dan fitur dilakukan secara acak.

#### Tahapan Umum _Random Forest_
+ Membangun _decision tree_ untuk setiap subsample data yang telah dipilih. Pada tahap ini, juga dilakukan pemilihan acak sejumlah fitur yang akan digunakan untuk membagi setiap simpul dalam _decision tree_.
+ Menggunakan setiap _decision tree_ yang telah dibangun untuk membuat prediksi pada data yang tidak terlihat (_testing_) atau data _validasi_. Setiap _decision tree_ memberikan prediksi berdasarkan fitur yang dipilih secara acak.
+ Tahap terakhir, hasil prediksi dari setiap _decision tree_ dijumlahkan (_voting_) jika tugasnya klasifikasi, atau diambil rata-ratanya jika tugasnya regresi. Ini menghasilkan prediksi akhir dari _Random Forest_.

Pada proyek ini menggunakan nilai parameter <strong>_n_estimators_=110</strong>, <strong>_max_depth_=16</strong>, <strong>_random_state_=123</strong>, <strong>_n_jobs_=1</strong>. <strong>_n_estimators_</strong> menentukan jumlah pohon keputusan yang akan dibangun dalam _ensemble_ (hutan). <strong>_max_depth_</strong>  menentukan kedalaman maksimum dari setiap pohon keputusan dalam ensemble. <strong>_random_state_=123</strong> menentukan seed untuk menghasilkan angka acak. Sehingga model menghasilkan yang sama setiap dilatih.  <strong>_n_jobs_=1</strong> menentukan jumlah pekerjaan paralel yang akan digunakan selama pelatihan. Selain parameter diatas menggunakan parameter _default_.

#### Kelebihan dan Kekurangan _Random Forest_
##### Kelebihan
_Random Forest_ biasanya memberikan akurasi yang tinggi karena menggabungkan prediksi dari beberapa pohon keputusan yang berbeda. Karena menggunakan banyak pohon keputusan dan mengambil rata-rata atau modus dari prediksi, _Random Forest_ cenderung lebih tahan terhadap overfitting dibandingkan dengan tree dicision tunggal.
##### Kekurangan
_Random Forest_ dapat menghasilkan model yang cukup besar, terutama jika jumlah pohon dan fitur cukup besar. Ini dapat menjadi masalah jika perlu mengoptimalkan penggunaan memori atau mempercepat waktu prediksi.

#### Pemilihan Model
Pada bagian Business Understanding ingin mengetahui dan memilih algoritma yang paling baik. Ketiga algoritma yang telah dipakai memiliki kelebihan dan kekurangannya masing-masing. Berdasarkan kelebihan dan kelemahan tiap model, pada proyek ini ditentukan bahwa model <trong>_Random Forest_</strong> sebagai model terbaik. Hal ini dikarenakan _Random Forest_ membangun banyak pohon keputusan secara parallel dan menggabungkan hasil prediksi. Kemampuan ini membantu dalam menangani keragaman dan kompleksitas data dengan lebih baik daripada model tunggal seperti KNN atau SVM. Selain itu _Random Forest_ dapat menangani _dataset_ dengan jumlah fitur yang besar dan mampu mengatasi fitur-fitur yang tidak teratur atau tidak relevan. Pada bagian Evaluation nantinya akan dikonfirmasi apakah benar model <trong>_Random Forest_</strong> merupakan yang terbaik daripada model <trong>KNN</strong> dan juga <trong>SVC</strong>

# Evaluation
Pada Proyek ini menggunakan model machine learning bertipe klasifikasi yang berarti Jika prediksi cocok dengan label kelas sebenarnya, performanya baik. Sedangkan jika tidak, performanya buruk. Secara teknis, perbedaan antara kelas sebenarnya dan kelas yang diprediksi disebut kesalahan klasifikasi. Maka, semua metrik mengukur seberapa kecil nilai kesalahan klasifikasi tersebut. Beberapa metrik yang akan digunakan adalah accuracy, precision, recall, f1_score.
<br>
$$Accuracy = {TP + TN \over TP + TN + FP + FN}$$
$$Precision = {TP \over TP + FP}$$
$$Recall = {TP \over TP + FN}$$
$$F1 = {2 * Precision * Recall \over Precision + Recall}$$
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


<strong>_Accuracy_</strong> mengukur persentase prediksi yang tepat dari total prediksi yang dilakukan. Skor akurasi berkisar antara 0 hingga 1, di mana nilai 1 mencerminkan prediksi yang sempurna, sementara nilai 0 menunjukkan bahwa tidak ada prediksi yang benar.
<br>
<strong>_Precision_</strong> mengukur rasio prediksi positif yang akurat dari total prediksi positif yang dibuat. Presisi memberikan wawasan tentang seberapa tepat model machine learning dalam membuat prediksi positif. Rentang nilai presisi adalah antara 0 hingga 1, di mana nilai 1 menunjukkan tingkat presisi tertinggi, sementara nilai 0 menandakan ketidakakuratan total dalam prediksi positif. Recall mengukur proporsi data positif yang berhasil diidentifikasi dari total data positif yang sebenarnya. 
<br>
<strong>_Recall_</strong> memberikan gambaran tentang seberapa efektif model machine learning dalam menemukan semua data positif yang ada. Rentang nilai recall adalah antara 0 hingga 1, di mana nilai 1 mencerminkan kemampuan model dalam menemukan semua data positif, sementara nilai 0 menandakan bahwa model gagal mengidentifikasi data positif. 
<br>
<strong>_F1 Score_</strong> rata-rata harmonis dari precision dan recall. F1 Score adalah ukuran keseimbangan antara precision dan recall, dengan nilai yang tinggi menunjukkan keseimbangan yang baik antara kedua metrik tersebut.
<br>
<br>
### Hasil Evaluasi Ketiga Model


|           | KNN      | SVM      | Randomforest |
|-----------|----------|----------|--------------|
| accuracy  | 0.813596 | 0.905702 | 0.910088     |
| precision | 0.757679 | 0.903766 | 0.980296     |
| recall    | 0.940678 | 0.915254 | 0.84322      |
| f1_score  | 0.839319 | 0.909474 | 0.906606     |
<br>
Tabel 1 Hasil Evaluasi Model
<br>
Dari tabel 1 bisa dilihat bahwa ketiga ketiga model mempunyai performa yang cukup baik. Pada model __KNN__ mempunyai nilai evaluasi paling rendah diantar yang lain. Sementara model <strong>_Random Forest_</strong> memiliki nilai akurasi yang paling tinggi. Walau demikian, tampaknya model <strong>_Random Forest_</strong> memiliki nilai _recall_ yang lebih rendah dari model lainnya. Sementara itu, tampaknya model __SVC__ memiliki nilai evaluasi yang paling stabil diantara model lainnya. Nilai evaluasinya berada di kisaran 90 pada ke-empat metriks. Jadi bisa disimpulkan bahwa model __SVC__ lah yang terbaik dan paling cocok berdasarkan permasalahan dan _Dataset_ yang digunakan pada proyek ini.


## Kesimpulan 
Berdasarkan dari apa yang telah dilakukan selama ini, dapat menjawab semua dari _problem statement_ yang telaj nyatakan sebelumnya. Pertama, pengaruh fitur pada _dataset_ dalam menentukan kelayakan konsumsi air terbilang cukup kuat. Hal ini dikarenakan bebrapa pasangan fitur memiliki nilai korelasi yang cukup kuat. Hal ini juga didukung oleh fakta bahwa ketiga model memiliki niali evaluasi yang relatif tinggi terhadap _dataset_ yang digunakan. Kedua, pada proyek ini telah menerapkan berbagai metode dalam menganalisa dan mengolah data agar dapat digunakan dengan baik oleh model. Mulai dari menangani _missing value_, membagi _dataset_ menjadi data latih dan data uji, menangani ketidakseimbangan data menggunakan metode _undersampling_, hingga melakukan standarisasi pada data. Ketiga, algoritma yang memiliki kinerja paling baik terhadap _dataset_ adalah algoritma <trong>SVC</strong>. Hal ini dibuktikan <trong>SVC</strong> memiliki nilai evaluasi tinggi dan stabil diantara model lainnya.
<br>
# Referensi
[1] Nasir, Nidia & Kansal, Afreen & Alshaltone, Omar & Barneih, Feras & Sameer, Mustafa & Shanableh, Abdallah & Al-Shamma'a, Ahmed. (2022). Water quality classification using machine learning algorithms. 10.1016/j.jwpe.2022.102920
<br>
[2] Setiawan, Dennis & Hendra. (2023). Uji Bakteriologis Air Minum Isi Ulang dengan Bakteri Escherichia coli dan Coliform sebagai Indikator. 10.31004/prepotif.v7i1.13459











