>>>>>>>>> # Data-Visualization-using-Plotnine
Pada repositori ini digunakan library visualisasi Python yaitu **Plotnine** untuk merepresentasikan data dalam beberapa bentuk grafik.

  **Plotnine** adalah package visualisasi data di Python yang mirip dengan ggplot2 milik R. Plotnine ini merupakan turunan matplotlib dengan fungsi-fungsi yang lebih mempermudah pekerjaan kita. Dataset yang dipakai kali ini adalah:
  * [Kependudukan DKI Jakarta](https://storage.googleapis.com/dqlab-dataset/datakependudukandki-dqlab.csv)
  * [Inflasi](https://storage.googleapis.com/dqlab-dataset/inflasi.csv)
 
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
5. **labs()**: untuk mengisi judul (*title*) grafik serta keterangan untuk sumbu x dan sumbu y

## Melihat data
Oke, sebelum bisa mengolah data, tentu kita perlu meninjau data yang kita miliki. Berikut adalah data kependudukan DKI 2013 yang berisi kolom: TAHUN, NAMA PROVINSI, NAMA KABUPATEN/KOTA, NAMA KECAMATAN, NAMA KELURAHAN, LUAS WILAYAH (KM2), KEPADATAN (JIWA/KM2), JENIS KELAMIN, RENTANG UMUR, JUMLAH  
![image](https://user-images.githubusercontent.com/49611937/115325104-3ed17900-a1b5-11eb-94cd-eca0378a5a6d.png)



