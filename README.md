# Data-Visualization-using-Plotnine
Pada repositori ini akan digunakan library visualisasi di Python yaitu **Plotnine** untuk merepresentasikan data dalam beberapa bentuk.

  **Plotnine** adalah package visualisasi data di Python yang mirip dengan ggplot2 milik R. Plotnine ini dibuat dari matplotlib dengan fungsi-fungsi yang lebih mempermudah pekerjaan kita. Dataset yang dipakai kali ini adalah:
  * Kependudukan DKI Jakarta : https://storage.googleapis.com/dqlab-dataset/datakependudukandki-dqlab.csv
  * Inflasi : https://storage.googleapis.com/dqlab-dataset/inflasi.csv
 
 Komponen grafik pada plotnine terdiri dari:
 * data: berisi data yang ingin kita buat visualisasinya
 * aesthetics: fungsi **aes** ini dipakai untuk menentukan data X dan Y dalam grafik. aes juga bisa diisi dengan *fill* serta *color*.
 * geoms (geometric objects): objek geometris (contohnya: lingkaran, titik, dan teks yang ingin dilihat di grafik)
   1. geom_col(): untuk membuat bar plot. Agar tidak default(stack), bisa ditambahkan parameter position='position_dodge'
   2. geom_point(): untuk membuat scatter plot
   3. geom_histogram(): untuk membuat histogram (distribusi data)
   4. geom_line(): untuk membuat line chart
   5. geom_boxplot(): untuk membuat grafik dalam bentuk boxplot
* coord_flip(): untuk mengubah posisi x dan y
* labs(): untuk mengisi judul (*title*) grafik serta keterangan untuk sumbu x dan sumbu y



