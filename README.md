<h1 align="center">Data-Visualization-using-Plotnine</h1>

Pada repositori ini digunakan library visualisasi Python yaitu **Plotnine** untuk merepresentasikan data dalam beberapa bentuk grafik.

  **Plotnine** adalah package visualisasi data di Python yang mirip dengan ggplot2 milik R. Plotnine ini merupakan turunan matplotlib dengan fungsi-fungsi yang lebih mempermudah pekerjaan kita. Dataset yang dipakai kali ini adalah:
  * [Kependudukan DKI Jakarta Tahun 2013](https://storage.googleapis.com/dqlab-dataset/datakependudukandki-dqlab.csv)
  * [Inflasi 8 Negara Anggota ASEAN Tahun 1996 - 2019](https://api.worldbank.org/v2/en/indicator/FP.CPI.TOTL.ZG?downloadformat=excel)
 
 
 
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


Sedangkan untuk data Inflasi yang ada adalah data inflasi dari 8 negara anggota ASEAN, yaitu Brunei Darussalam, Filipina, Indonesia, Malaysia, Myanmar, Singapura, Thailand, dan Vietnam dari tahun 1996 sampai tahun 2019. Data ini adalah olahan dari data World Bank yang telah dicantumkan pada link dataset di atas. Dari beberapa kolom, hanya kolom Tahun, Negara, dan Inflasi yang digunakan.
<p align="center">
  <img src="https://user-images.githubusercontent.com/49611937/115339866-d5129880-a1cf-11eb-83d1-d44481ab1c58.png" />
</p>


## geom_col()
Jika memperhatikan kolom-kolom yang terdapat pada data Kependudukan DKI Jakarta Tahun 2013, kita bisa membuat berbagai visualisasi dari beberapa kolom yang memiliki hubungan satu sama lain. Yang pertama, kita akan melihat jumlah penduduk di setiap kabupaten atau kota. Kita juga bisa menambahkan data jenis kelamin untuk mengetahui jumlah penduduk laki-laki jika dibandingkan dengan jumlah penduduk perempuan di masing-masing kabupaten atau kota tersebut. Dalam kasus ini, akan lebih mudah jika kita memakai bar plot atau grafik batang dengan jenis stack, dimana sebuah bar terdiri dari jumlah penduduk berjenis kelamin laki-laki dan perempuan. 
Seperti yang sudah disebutkan sebelumnya, penggunaan plotnine untuk membuat bar plot adalah menggunakan geom_col() seperti kode berikut:
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
Kode tersebut akan menghasilkan bar plot seperti yang terlihat di bawah ini.  
<p align="center">
  <img src="https://user-images.githubusercontent.com/49611937/115344367-836e0c00-a1d7-11eb-8c90-a9a3ad7bc5f1.png" />
</p>
Dari visualisasi tersebut dapat disimpulkan bahwa:
* Jakarta Barat adalah kota di DKI Jakarta yang menyumbangkan jumlah penduduk terbanyak di tahun 2013 dengan jumlah lebih dari 2.000.000 penduduk, sedangkan yang paling sedikit penduduknya adalah dari Kabupaten Adm. Kepulauan Seribu
* Jumlah penduduk laki-laki dan penduduk perempuan memiliki rasio yang seimbang di setiap kabupaten atau kota di DKI Jakarta tahun 2013<br/>


<p align="center">
  <img src:"https://user-images.githubusercontent.com/49611937/115348252-9a632d00-a1dc-11eb-90ab-8e1d4425e3b8.png" />
</p>



sebagaimana dikutip dari laman resmi Bank Indonesia (BI), inflasi adalah diartikan sebagai kenaikan harga barang dan jasa secara umum dan terus menerus dalam jangka waktu tertentu

