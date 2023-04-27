# Laporan Proyek Machine Learning - Andrew

## Domain Proyek

Transformasi digital mengubah proses pengambilan keputusan dan menciptakan konektivitas di antara orang-orang, proses, teknologi, dan data. *Data-Driven Decision Making* (DDDM) didefinisikan sebagai pengambilan keputusan berdasarkan data dibanding dengan intuisi, pengamatan, atau tebakan. Nilai keputusan yang diambil bergantung pada kualitas data serta analisis dan interpretasinya.

Perkembangan data membuat *data-driven decision making*  menjadi komponen penting dalam proses pengelolaan sumber daya manusia. Hal ini terjadi karena akses pada data yang dapat mendukung pengambilan keputusan terkait rekrutmen, performa karyawan, dan ranah lainnya dalam pengelolaan sumber daya manusia seringkali mampu meningkatkan performa bisnis suatu perusahaan. Jac Fitz-Enz dalam bukunya yang berjudul *The New HR Analytics* menyebutkan bahwa setidaknya terdapat delapan hal yang terjadi apabila proses pengambilan keputusan dilakukan berdasarkan data
1. Fokus dapat terjaga.
2. Tujuan dapat diidentifikasi dan diukur.
3. Fakta dan bukan politik mengambil peran yang besar.
4. Wawasan dapat diperoleh secara luas
5. Bias dapat diminimalisasi.
6. Data merupakan bahasa umum yang dapat memfasilitasi komunikasi.
7. Lebih sedikit informasi yang diabaikan.
8. Pengalaman dan pertimbangan dilakukan secara lebih efektif.

Salah satu artikel yang diterbitkan oleh James Bell Associates yang berjudul [Guide to Data-Driven Decision Making: Using Data to Inform Practice and Policy Decisions in Child Welfare Organizations](https://www.acf.hhs.gov/sites/default/files/documents/cb/guide_to_dddm.pdf) menyebutkan bahwa proses DDDM dilakukan dengan langkah-langkah berikut
1. Perumusan masalah. Mengidentifikasi
2. Pengumpulan dan analisis data
3. Komunikasi hasil yang diperoleh dengan pembuat keputusan.
4. Perbaikan sistem organisasi.

## Business Understanding
Sebuah perusahaan bernama XYZ, mempekerjakan sekitar 4000 karyawan. Namun, setiap tahun, sekitar 15% karyawannya meninggalkan perusahaan dan perlu diganti dengan sumber daya lain yang tersedia di pasar kerja. Perusahaan yakin bahwa tingkat *attrition* (karyawan keluar, baik karena mereka sendiri atau karena dipecat) ini buruk bagi perusahaan, karena beberapa alasan berikut
1. Pekerjaan karyawan yang keluar tertunda, sehingga sulit untuk memenuhi jadwal, mengakibatkan berkurangnya reputasi di antara konsumen dan mitra.
2. Jumlah karyawan untuk merekrut karyawan baru harus diperatahankan dalam jumlah besar.
3. Seringkali, karyawan baru harus dilatih untuk pekerjaan yang diberikan dan/atau diberikan waktu untuk menyesuaikan diri dengan perusahaan.

Oleh karena itu, perusahaan XYZ telah mengontrak konsultan untuk memahami faktor-faktor apa yang harus mereka fokuskan untuk mengurangi jumlah karyawan yang keluar. Dengan kata lain, mereka ingin tahu perubahan apa yang harus mereka lakukan di tempat kerja mereka, agar sebagian besar karyawan mereka tetap tinggal.

### Problem Statements
Berdasarkan kondisi yang telah diuraikan sebelumnya, konsultan akan mengembangkan sebuah sistem prediksi tingkat *attrition* untuk menjawab permasalahan berikut.
- Faktor apa yang harus difokuskan untuk mengurangi tingkat *attrition*?.
- Siapa sajakah karyawan-karyawan yang berpotensi untuk keluar dari perusahaan?

### Goals
Berikut adalah beberapa tujuan proyek ini untuk menjawab rumusan masalah yang ada
- Mengetahui faktor yang paling berpengaruh terhadap tingkat *attrition*
- Membuat model machine learning yang dapat memprediksi karyawan-karyawan yang berpotensi untuk keluar dari perusahaan.

    ### Solution statements
    Model *machine learning* yang akan dibangun adalah model klasifikasi dengan *attrition* sebagai variabel target. Model-model *machine learning* yang akan digunakan adalah *Logistic Regression*, *K-Nearest Neighbor*, dan *Support Vector Classifier*. Kemudian, model yang paling baik dalam memprediksi akan ditentukan dengan tingkat akurasi model sebagai metrik evaluasi.

## Data Understanding
Dataset yang digunakan dalam proyek berjudul [HR Analytics Case Study](https://www.kaggle.com/vjchoudhary7/hr-analytics-case-study) dan diperoleh dari kaggle.com. Dataset ini berisi enam fail dengan penjelasan masng-masing fail adalah sebagai berikut
1. data_dictionary.xlsx: Fail yang memiliki 3 kolom dan 52 baris. Fail ini berisi detail metadata mengenai dataset yang ada
2. employee_survey_data.csv: Fail yang memiliki 4 kolom dan 4410 baris. Fail ini berisi survei yang dilakukan perusahaan karyawannya
3. general_data.csv: Fail yang memiliki 24 kolom dan 4410 baris. Fail ini berisi data umum karyawan
4. in_time.csv: Fail yang memiliki 262 kolom dan 4410 baris. Fail ini berisi jam masuk karyawan ke kantor pada hari tertentu.
5. manager_survey_data.csv: Fail yang memiliki 3 kolom dan 4410 baris. Fail ini berisi survei umpan balik karyawan kepada manajernya
6. out_time.csv: Fail yang memiliki 262 kolom dan 4410 baris. Fail ini berisi jam keluar karyawan dari kantor pada hari tertentu

Proyek ini hanya akan mengolah data-data yang terdapat pada employee_survey_data.csv, general_data.csv, dan manager_survey_data.csv. Ketiga fail ini akan digabungkan dengan teknik *inner join* terhadap EmployeeID.

### Variabel-variabel pada HR Analytics Case Study adalah sebagai berikut
- Age: Umur karyawan.
- Attrition: Apakah karyawan keluar dari perusahaan dalam satu tahun terakhir atau tidak.
- BusinessTravel: Seberapa sering karyawan bepergian untuk tujuan bisnis dalam satu tahun terakhir.
- Department: Departemen karyawan dalam perusahaan.
- DistanceFromHome: Jarak rumah karyawan dengan perusahaan (dalam kilometer)
- Education: Tingkat pendidikan karyawan
- EducationField: Bidang pendidikan karyawan
- EmployeeCount: Jumlah karyawan
- EmployeeNumber: Nomor induk karyawan
- EnvironmentSatisfaction: Tingkat kepuasan karyawan terhadap lingkungan pekerjaan 
- Gender: Jenis kelamin karyawan
- JobInvolvement: Tingkat keterlibatan manajer terhadap pekerjaan karyawan
- JobLevel: Tingkat pekerjaan dalam perusahaan
- JobRole: Nama peran pekerjaan dalam perusahaan
- JobSatisfaction: Tingkat kepuasan pekerjaan
- MaritalStatus: Status pernikahan
- MonthlyIncome: Pendapatan bulanan (dalam rupee)
- NumCompaniesWorked: Banyaknya perusahaan yang pernah diikuti karyawan
- Over18: Apakah karyawan berumur di atas 18 tahun atau tidak.
- PercentSalaryHike: Persen kenaikan gaji dibanding tahun lalu
- PerformanceRating: Tingkat performa karyawan
- RelationshipSatisfaction: Kepuasan hubungan karyawan
- StandardHours: Waktu bekerja karyawan
- StockOptionLevel: Persentase kepunyaan saham dalam perusahaan
- TotalWorkingYears: Banyaknya tahun bekerja
- TrainingTimesLastYear: Banyaknya pelatihan yang diikuti dalam satu tahun terakhir
- WorkLifeBalance: Tingkat keseimbangan pekerjaan dan hidup
- YearsAtCompany: Banyaknya tahun yang dihabiskan karyawan dalam perusahaan
- YearsSinceLastPromotion: Banyaknya tahun sejak promosi terakhir
- YearsWithCurrManager: Banyaknya tahun di bawah manajer yang sekarang

### Exploratory Data Analysis
Untuk memahami dataset lebih lanjut, dilakukan *exploratory data analysis* untuk setiap variabel. Berikut adalah diagram batang yang menunjukkan persebaran data dari masing-masing kolom dataset untuk data kategorikal. 
![Categorical-Features-Univariate-Analysis](https://i.ibb.co/KqXHDRX/Categorical-Features-Univariate-Analysis.png)
Dari hasil analisis diagram batang "Attrition", diperoleh informasi bahwa sebagian besar sampel merupakan karyawan yang tidak keluar dalam satu tahun terakhir. Persebaran data yang tidak merata ini akan berdampak buruk pada model *machine learning*.

![Numerical-Features-Multivariate-Analysis](https://i.ibb.co/RgNjyCB/Numerical-Features-Multivariate-Analysis.png)
Hasil analisis multivariat untuk variabel numerikal menunjukkan bahwa
1. Tidak ada hubungan yang signifikan antara variabel Age, PercentSalaryHike, DistanceFromHome, StockOptionLevel, YearsSinceLastPromotion, MonthlyIncome, dan TrainingTimesLastYear dengan Attrition
2. Pada variabel YearsAtCompany, mayoritas karyawan keluar sebelum bekerja lebih dari lima tahun pada perusahaan. Penjelasan yang mungkin terjadi adalah karyawan baru sulit untuk beradaptasi dengan budaya perusahaan.
3. Pada variabel TotalWorkingYears, mayoritas karyawan keluar sebelum memiliki pengalaman kerja 10 tahun. Penjelasan yang mungkin adalah karyawan yang keluar masih mencari bidang untuk ditekuni.
4. Pada variabel YearsWithCurrManager, mayoritas karyawan keluar sebelum bekerja lebih dari 2,5 tahun dengan manajer yang sekarang. Penjelasan yang mungkin adalah karyawan tidak mampu beradaptasi dengan gaya kepemimpinan manajer
5. Pada variabel NumCompaniesWorked, karyawan yang keluar dari perusahaan sering berganti-ganti perusahaan. Penjelasan yang mungkin adalah karyawan memiliki kepribadian yang berbeda dengan budaya perusahaan.

## Data Preparation
Selanjutnya, akan dilakukan proses transformasi data sehingga data memiliki bentuk yang cocok untuk proses pemodelan. Beberapa tahap persiapan data yang dilakukan, yaitu:
1. Encoding fitur kategori dengan Label Encoder.
2. Reduksi dimensi dengan Principal Component Analysis (PCA).
3. Pembagian dataset dengan fungsi train_test_split dari library sklearn.
4. Standarisasi data numerikal.

### Encoding fitur kategori dengan Label Encoder
Setelah melakukan eksplorasi data pada tahap sebelumnya, diperoleh informasi bahwa data dalam dataset telah mengalami preprocessing untuk data kategorikal, seperti pada variabel Education, EnvironmentSatisfaction, JobInvolvement, JobSatisfaction, PerformanceRating, RelationshipSatisfaction, dan WorkLifeBalance. Untuk itu, dilakukan proses encoding fitur kategori dengan teknik Label Encoder dari library scikit-learn.

### Reduksi dimensi dengan Principal Component Analysis (PCA)
Berikut adalah matriks korelasi untuk setiap variabel dalam dataset. Perhatikan bahwa terdapat korelasi yang tinggi antara ketiga variabel YearsAtCompany, YearsSinceLastPromotion, dan YearsWithCurrManager. Selain itu, terdapat juga korelasi yang tinggi antara variabel Age dan TotalWorkingYears.
![Heatmap](https://i.ibb.co/9cRQJg7/Heatmap.png)

Korelasi yang tinggi antarvariabel ini menunjukkan informasi yang berulang atau redundan. Untuk itu, perlu dilakukan proses reduksi dimensi agar analisis dapat dilakukan dengan lebih sederhana. Reduksi dimensi dilakukan dengan teknik PCA

### Pembagian dataset dengan fungsi train_test_split dari library sklearn
Pembagian dataset diperlukan untuk melatih model dan mengujinya. Model yang diuji dengan dataset yang sama dengan data latih akan mengakibatkan model menjadi *overfit* sehingga performanya buruk untuk kasus nyata.

### Standardisasi
Algoritma machine learning memiliki performa lebih baik dan konvergen lebih cepat ketika dimodelkan pada data dengan skala relatif sama atau mendekati distribusi normal. Proses scaling dan standarisasi membantu untuk membuat fitur data menjadi bentuk yang lebih mudah diolah oleh algoritma. Standardisasi adalah teknik transformasi yang paling umum digunakan dalam tahap persiapan pemodelan.

## Modeling
Model *machine learning* yang dibangun adalah model klasifikasi dengan *attrition* sebagai variabel target. Model-model *machine learning* yang akan digunakan adalah *Logistic Regression*, *K-Nearest Neighbor*, dan *Support Vector Classifier*.

### Logistic Regression
*Logistic regression* adalah sebuah algoritma klasifikasi. *Logistic regression* biasanya digunakan untuk memprediksi sebuah kejadian berdasarkan sekumpulan variabel terikat. *Logistic regression* biasanya cocok digunakan apabila variabel bebasnya tidak memiliki hubungan linear yang kuat.

Kelebihan algoritma *logistic regression*
1. *Logistic regression* merupakan salah satu algoritma *machine learning* yang mudah dipelajari.
2. Algoritma *logistic regression* mampu mendeskripsikan hubungan asosiatif antarvariabel. Sebagai contoh, model *logistic regression* menunjukkan bahwa mayoritas orang perokok menderita kanker paru-paru. Kita dapat menduga bahwa orang yang merokok memiliki kemungkinan besar menderita kanker paru-paru.

Kekurangan algoritma *logistic regression*
1. *Logistic regression* berasumsi terdapat hubungan linear antara variabel bebas dan terikat. Sebagai contoh, *logistic regression* akan sulit untuk membedakan orang berambut lurus dan keriting. Rambut dapat memiliki panjang 1 meter dan diklasifikasikan sebagai rambut lurus atau keriting.

Berikut merupakan algoritma untuk melatih model *logistic regression*. Perhatikan bahwa tidak ada parameter khusus yang ditambahkan ke dalam fungsi *logistic regression*. Model akan menggunakan parameter *default* .
```
from sklearn.linear_model import LogisticRegression

lr = LogisticRegression()
lr.fit(X_train,y_train)
y_pred_lr = lr.predict(X_test)
```

### K-Nearest Neighbor
*K-nearest neighbors* (KNN) adalah salah satu jenis algoritma *supervised learning* untuk kasus regresi dan klasifikasi. KNN memprediksi label yang benar untuk data uji dengan menghitung jarak antara data uji dengan semua data latih. Kemudian, algoritma akan memiliki K banyaknya titik terdekat pada data uji. Algoritma KNN kemudian menghitung probabilitas data uji tergolong ke dalam K kelas data latih dan memilih kelas dengan probabilitas yang plaing besar.

Kelebihan *K-nearest neighbors* (KNN)
1. Algoritma KNN relatif simpel, mudah dipahami, dan mudah diimplementasikan.
2. Algoritma KNN tidak menguji data secara langsung sehingga dapat dengan cepat dibangun.
3. Algoritma KNN dapat digunakan untuk masalah klasifikasi dan regresi

Kekurangan *K-nearest neighbors* (KNN)
1. Algoritma KNN tergolong lambat karena algoritma ini harus menghitung jarak dari setiap titik data uji ke titik data latih.
2. Algoritma KNN sangat sensitif terhadap outlier karena menentukan label data berdasarkan kriteria jarak.
3. Algoritma KNN tidak mampu berfungsi dengan baik pada data yang tidak seimbang. Apabila mayoritas sampel merupakan label A, model akan cenderung mengklasifikasikan data uji sebagai label A.

Berikut merupakan algoritma untuk melatih model *KNN*. Perhatikan bahwa tidak ada parameter khusus yang ditambahkan ke dalam fungsi *KNN*. Model akan menggunakan parameter *default* .
```
from sklearn.neighbors import KNeighborsClassifier
 
knn = KNeighborsClassifier()
knn.fit(X_train, y_train)
y_pred_knn = knn.predict(X_test)
```

### Support Vector Classifier
*Support Vector Machine* merupakan salah satu algoritma *supervised learning*. *Support Vector Machine* bekerja dengan mencari *hyperplane* terbaik yang mampu mengklasifikasikan data. Salah satu caranya adalah dengan mencari *hyperplane* yang mampu menghasilkan *margin* terbesar dalam data. *Support Vector Classifier* sendiri merupakan salah satu jenis *Support Vector Machine* khusus untuk kasus klasifikasi.

Kelebihan *Support Vector Classifier*
1. SVC bekerja relatif baik ketika ada margin pemisahan yang jelas antarlabel.
2. SVC bekerja efektif dalam ruang dimensi tinggi.
3. SVC efektif dalam kasus dengan jumlah dimensi lebih besar dari jumlah sampel.
4. SVC relatif hemat memori

Kekurangan *Support Vector Classifier*
1. Algoritma SVC tidak cocok untuk kumpulan data yang besar.
2. SVC tidak bekerja dengan baik ketika kumpulan data memiliki banyak noise.

Berikut merupakan algoritma untuk melatih model *SVC*. Perhatikan bahwa tidak ada parameter khusus yang ditambahkan ke dalam fungsi *SVC*. Model akan menggunakan parameter *default* .
```
from sklearn.svm import SVC

svc = SVC()
svc.fit(X_train, y_train)
y_pred_svc = svc.predict(X_test)
```

Model *machine learning* terbaik untuk digunakan adalah *support vector classifier* karena memiliki *balanced accuracy score* yang paling tinggi dari model lainnya. Bagian Evaluation menunjukkan penjelasan lebih lanjut mengenai hal ini.

## Evaluation
Dalam kasus klasifikasi, akurasi menunjukkan persentase label yang tepat diprediksi sehingga cocok sampel dengan label data uji. *Balanced accuracy score* sendiri ekuivalen dengan akurasi, tetapi telah mengalami pembobotan berdasarkan banyaknya data uji untuk masing-masing kelas. Metrik *balanced accuracy score* dipilih karena dalam *exploratory data analysis* telah ditunjukkan bahwa mayoritas sampel data merupakan data untuk karyawan yang masih tetap dalam perusahaan.

Balanced accuracy score diformulasikan sebagai
```
Balanced accuracy = (Sensitivity + Specificity) / 2
```
dengan
*Sensitivity* adalah persentase kasus positif yang dapat dideteksi model dengan tepat.
*Specificity* adalah persentase kasus negatif yang dapat dideteksi model dengan tepat. 

Sebagai contoh, berikut adalah confusion matrix yang dihasilkan oleh model *machine learning* yang telah dibangun
![Confusion Matrix](https://i.ibb.co/gwNgPR9/Confusion-Matrix.png)

Akan dicari nilai *sensitivity* dan *specifity* untuk model *SVC*
```
Sensitivity = 723/(723+7) = 0.9904
Specificity = 56/(56+74) = 0.4307
```

Dengan demikian, nilai *balanced accuracy score*-nya adalah
```
Balanced accuracy = (0.9904+0.4307)/2 = 0.7106
```

Berdasarkan hasil metrik evaluasi, diperoleh nilai *balanced accuracy score* untuk masing-masing model adalah sebagai berikut
![balanced_accuracy_score](https://i.ibb.co/Rz1r322/Capture.png)

Terlihat bahwa SVC merupakan model dengan skor tertinggi untuk metrik evaluasi yang digunakan. Oleh karena itu, SVC merupakan model terbaik. Model ini memiliki skor akurasi sebesar 71% artinya model ini mampu memprediksi data uji dengan benar sebanyak 71%.