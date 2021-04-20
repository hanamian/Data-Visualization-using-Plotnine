<h1 align="center">Data-Visualization-using-Plotnine</h1>

Repository ini membahas penggunaan **Plotnine** (salah satu library visualisasi Python) untuk merepresentasikan data dalam beberapa bentuk grafik.

  **Plotnine** adalah package visualisasi data di Python yang mirip dengan *ggplot2* milik R programming. Plotnine ini merupakan turunan matplotlib yang memiliki fungsi-fungsi yang mempermudah pekerjaan kita. Dataset yang dipakai kali ini adalah:
  * [Data Kependudukan DKI Jakarta Tahun 2013](https://storage.googleapis.com/dqlab-dataset/datakependudukandki-dqlab.csv)
  * [Data Inflasi 8 Negara Anggota ASEAN Tahun 1996 - 2019](https://api.worldbank.org/v2/en/indicator/FP.CPI.TOTL.ZG?downloadformat=excel)
 
 
 
 Komponen grafik pada plotnine terdiri dari:
 1. **data**: berisi data yang ingin kita buat visualisasinya
 2. **aes**thetics: fungsi **aes** ini dipakai untuk menentukan data X dan Y dalam grafik. aes juga bisa diisi dengan *fill* serta *color* jika ingin mengikutsertakan data lain, misalnya membuat 2 line chart dalam 1 figure ataupun untuk melihat persebaran data dalam variasi gender atau umur.
 3. geoms (geometric objects): objek geometris (contohnya: lingkaran, titik, dan teks yang ingin dilihat di grafik)
      - **geom_col()**: untuk membuat bar plot. Agar tidak default(stack), bisa ditambahkan parameter *position='position_dodge'*
      - **geom_point()**: untuk membuat scatter plot
      - **geom_histogram()**: untuk membuat histogram (distribusi data)
      - **geom_line()**: untuk membuat line chart
      - **geom_boxplot()**: untuk membuat grafik dalam bentuk boxplot
4. **coord_flip()**: untuk menukar posisi x dan y
5. **labs()**: untuk mengisi judul (*title*) grafik serta keterangan untuk sumbu x dan sumbu y<br/>


Oke, sebelum bisa mengolah data, tentu kita perlu meninjau data yang kita miliki. Berikut adalah data Kependudukan DKI Jakarta Tahun 2013 yang berisi kolom: 
Tahun, Nama provinsi, Nama kabupaten/kota, Nama kecamatan, Nama kelurahan, Luas wilayah (km2), Kepadatan (jiwa/km2), Jenis kelamin, Rentang umur, dan Jumlah  
<p align="center">
  <img src="https://user-images.githubusercontent.com/49611937/115340390-c678b100-a1d0-11eb-8d14-ea8a86f4f96f.png" />
</p>


Sedangkan untuk data Inflasi yang dipakai adalah data inflasi dari 8 negara anggota ASEAN, yaitu Brunei Darussalam, Filipina, Indonesia, Malaysia, Myanmar, Singapura, Thailand, dan Vietnam dari tahun 1996 sampai tahun 2019. Data ini adalah olahan dari data World Bank yang telah dicantumkan pada link dataset di atas. Dari beberapa kolom, hanya kolom Tahun, Negara, dan Inflasi yang digunakan.
<p align="center">
  <img src="https://user-images.githubusercontent.com/49611937/115339866-d5129880-a1cf-11eb-83d1-d44481ab1c58.png" />
</p>


## geom_col()
Jika memperhatikan kolom-kolom yang terdapat pada data Kependudukan DKI Jakarta Tahun 2013, kita bisa membuat berbagai visualisasi dari beberapa kolom yang berhubungan. Pada kasus pertama, kita akan melihat jumlah penduduk di setiap kabupaten/kota. Kita bisa menambahkan data jenis kelamin di bagian *fill* fungsi **aes** untuk mengetahui perbandingan jumlah penduduk laki-laki dan jumlah penduduk perempuan di masing-masing kabupaten/kota tersebut. 

Dalam kasus ini, akan lebih mudah jika kita memakai bar plot atau grafik batang dengan jenis stack, dimana data jumlah penduduk berjenis kelamin laki-laki dan perempuan bertumpuk pada sebuah bar. 
Seperti yang telah disebutkan sebelumnya, **geom_col()** digunakan untuk membuat bar plot. Contoh implementasinya adalah sebagai berikut:
```
p9.options.figure_size=(8,4)

(ggplot(data=data_penduduk)
+ aes(x='NAMA KABUPATEN/KOTA', y='JUMLAH', fill='JENIS KELAMIN') 
+ geom_col() 
+ coord_flip() 
+ labs(title='Jumlah Penduduk DKI Jakarta per Kabupaten/Kota Tahun 2013',   
       x='Kabupaten/Kota',
       y='Jumlah Penduduk')
).draw()

plt.show()
```
Hasil visualisasi: 
<p align="center">
  <img src="https://user-images.githubusercontent.com/49611937/115344367-836e0c00-a1d7-11eb-8c90-a9a3ad7bc5f1.png" />
</p>

*Dari visualisasi tersebut dapat disimpulkan bahwa*:
>   - Jakarta Barat adalah kota di DKI Jakarta yang menyumbangkan jumlah penduduk terbanyak di tahun 2013 dengan jumlah lebih dari 2.000.000 penduduk, sedangkan yang paling sedikit penduduknya adalah dari Kabupaten Adm. Kepulauan Seribu
>   - Jumlah penduduk laki-laki dan penduduk perempuan memiliki rasio yang seimbang di setiap kabupaten atau kota di DKI Jakarta tahun 2013

Kita juga bisa memodifikasi grafik untuk melihat komposisi jumlah penduduk dari berbagai rentang umur, yaitu 35-39, 40-44, 45-49, 50-54, 55-59, 60-64, 65-69, 70-74, dan lebih dari 75 tahun. Sayangnya dataset tidak menyediakan data penduduk dengan umur kurang dari 35 tahun, sehingga rasanya kurang lengkap. Penambahan data rentang umur ini bisa dilakukan dengan menambah parameter *fill* seperti berikut ini:
 ```
+ aes(x='NAMA KABUPATEN/KOTA', y='JUMLAH', fill='RENTANG UMUR') 
```
Hasil visualisasi:
<p align="center">
  <img src="https://user-images.githubusercontent.com/49611937/115348252-9a632d00-a1dc-11eb-90ab-8e1d4425e3b8.png" />
</p>

*Dari visualisasi tersebut dapat disimpulkan bahwa* penduduk dengan umur lebih dari 75 tahun jumlahnya paling sedikit di semua kabupaten/kota DKI Jakarta pada tahun 2013

<br/>

Sekarang kita akan membuat grafik jumlah penduduk di setiap kelurahan yang ada di kecamatan PASAR SENEN. Selain itu, kita juga ingin melihat perbandingan jumlah penduduk laki-laki dan perempuannya. Kita bisa menambahkan parameter *position=position_dodge* untuk membuat data jenis kelamin laki-laki dan perempuan terpisah barnya. Grafik ini bisa dibuat dengan memodifikasi beberapa bagian kode sebagai berikut:
```
(ggplot(data=data_penduduk[data_penduduk['NAMA KECAMATAN']=='SENEN'])
+ aes(x='NAMA KELURAHAN', y='JUMLAH', fill='JENIS KELAMIN') 
+ geom_col(position='position_dodge') 

```
Hasil visualisasi:
<p align="center">
  <img src="https://user-images.githubusercontent.com/49611937/115351816-d6988c80-a1e0-11eb-80e4-2d16076e4b88.png" />
</p>

*Dari visualisasi tersebut dapat disimpulkan bahwa:*
>   - Kramat adalah kelurahan yang memiliki jumlah penduduk paling banyak di kecamatan SENEN, sedangkan yang paling sedikit penduduknya adalah kelurahan Kenari dan Senen
>   - Semua kelurahan di kecamatan SENEN memiliki jumlah penduduk laki-laki lebih banyak dibandingkan penduduk perempuan, kecuali kelurahan Senen yang jumlah perempuannya sedikit lebih banyak dari penduduk laki-lakinya  


## geom_point()
Fungsi geom_point() mempermudah kita membuat scatter plot. Contohnya jika kita ingin melihat hubungan dan sebaran jumlah penduduk terhadap luas wilayah. Wilayah yang akan kita pakai adalah wilayah kelurahan, sehingga kita perlu menggabungkan dan menjumlahkan data luas wilayah perkelurahan terlebih dahulu.
```
p9.options.figure_size=(5,5)
penduduk_luas_kelurahan = data_penduduk.groupby(['LUAS WILAYAH (KM2)', 'NAMA KELURAHAN'])[['JUMLAH']].agg('sum').reset_index()

(ggplot(penduduk_luas_kelurahan)
+ aes(x='JUMLAH', y='LUAS WILAYAH (KM2)', color='JUMLAH')
+ geom_point()     
).draw()

plt.show()
```
Hasil visualisasi:
<p align="center">
  <img src="https://user-images.githubusercontent.com/49611937/115355204-a5ba5680-a1e4-11eb-8fb3-9e7f3831c95f.png" />
</p>

*Dari visualisasi tersebut dapat disimpulkan bahwa*:
>  Sebagian besar kelurahan dengan luas wilayah yang lebih sempit memiliki jumlah penduduk lebih sedikit.

## geom_histogram()
geom_histrogram() ini adalah fungsi untuk membuat histogram plot. Persebaran data akan terlihat dengan jelas jika menggunakan histogram. **stat(count/max(count))** adalah transformasi statistik untuk membuat batasan nilai. Pada kali ini, nilai y yang akan dibatasi agar tidak lebih dari 1.
```
p9.options.figure_size=(5,5)

(ggplot(data=data_penduduk)
+ aes( x='LUAS WILAYAH (KM2)', y='stat(count/max(count))')   
+ geom_histogram()
).draw()

plt.show()
```
Hasil visualisasi:
<p align="center">
  <img src="https://user-images.githubusercontent.com/49611937/115358534-f7b0ab80-a1e7-11eb-9348-d36f345e64fe.png" />
</p>

## geom_boxplot()
Tentu saja, geom_boxplot() digunakan untuk membuat boxplot. Kita hanya perlu menambahkan geom_boxplot() pada kode yang kita buat.
```
+ geom_boxplot()     
```
Hasil visualisasi:
<p align="center">
  <img src="https://user-images.githubusercontent.com/49611937/115358682-1adb5b00-a1e8-11eb-9ebf-503760afb084.png" />
</p>

## geom_line()
geom_line() adalah fungsi yang mempermudah kita membuat line plot. Kita akan menggunakan data Inflasi 8 Negara ASEAN dari tahun 1996 sampai 2019 untuk membuat line plot ini. Selain single line, kita juga bisa membuat multi plot line dengan memanfaatkan geom_line(). Namun sebelum membuat plot ini, sebenarnya apa itu inflasi? 


Oke, berdasarkan laman resmi Bank Indonesia (BI), inflasi adalah kenaikan harga barang dan jasa secara umum dan terus menerus dalam jangka waktu tertentu. Semakin kecil nilai inflasi, maka semakin baik perekonomian sebuah negara, begitupun sebaliknya, nilai inflasi yang besar menunjukkan bahwa keadaan perekonomian sebuah negara sedang tidak baik.
Mari kita lihat pergerakan inflasi di Indonesia dari tahun ke tahun. Untuk membuat line plot di plotnine, kita bisa menggunakan kode berikut:
```
p9.options.figure_size=(8,4)

#mengubah data bulan yang berupa string menjadi datetime

(ggplot(data=inflasi_asean[inflasi_asean['Negara']=='Indonesia'])
+ aes(x='Tahun', y='Inflasi')
+ geom_line()
).draw()

plt.show()
```
Hasil visualisasi:
<p align="center">
  <img src="https://user-images.githubusercontent.com/49611937/115358871-4cecbd00-a1e8-11eb-8135-cec5829b691e.png" />
</p>

*Dari visualisasi tersebut dapat disimpulkan bahwa*:
>      Inflasi melejit secara signifikan di Indonesia pada tahun 1998 dan berangsur-angsur menurun hingga tahun 2019


Kita juga ingin melihat dan membandingkan pergerakan inflasi 7 negara anggota ASEAN lain dari tahun ke tahun, apakah lebih baik atau lebih buruk dibandingkan dengan yang terjadi di Indonesia?
Kita hanya perlu menambahkan parameter *color* untuk membuat multi plot line yang berisi nama-nama 8 negara ASEAN.
```
+ aes(x='Tahun', y='Inflasi', color='Negara')
```
Hasil visualisasi:
<p align="center">
  <img src="https://user-images.githubusercontent.com/49611937/115358917-5b3ad900-a1e8-11eb-9640-e0ab2e493280.png" />
</p>


*Dari visualisasi tersebut dapat disimpulkan bahwa*:
>    - Selain Indonesia, ada negara lain yang mengalami lonjakan inflasi sangat tinggi di tahun 1998, yaitu Myanmar
>    - Myanmar mengalami pundak inflasi tertinggi di tahun 2002
>    - Inflasi tertinggi di tahun 2019 terjadi di Myanmar
>    - Brunei Darussalam adalah negara dengan nilai inflasi terendah dari tahun 1996 hingga 2019 yang pergerakan tiap tahunnya cenderung mendatar 



