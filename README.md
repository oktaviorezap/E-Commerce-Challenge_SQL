# DQLab SQL Project: Data Analysis for E-Commerce Challenge (SQL)
# Project Background
**Business Problem:**
1. DQLab Store ingin memahami kontribusi pelanggan tertentu terhadap pendapatan total perusahaan. Salah satu pengguna, user 12476, telah melakukan sejumlah transaksi yang signifikan. Namun
   belum ada analisis yang dilakukan untuk mengidentifikasi transaksi terbesar dari pengguna ini. Tanpa informasi ini, DQLab Store mungkin melewatkan peluang untuk menawarkan insentif atau
   layanan khusus yang bisa meningkatkan loyalitas dan volume transaksi dari pelanggan bernilai tinggi ini.
   <br>
   <br>
2. Perusahaan mengalami kesulitan dalam memahami kinerja penjualan tahunan mereka. Pada tahun 2020, tidak ada analisis mendalam mengenai jumlah transaksi dan total nilai transaksi yang terjadi.
   Kekurangan data ini membuat perusahaan tidak memiliki dasar yang kuat untuk merencanakan target penjualan dan strategi pemasaran yang efektif untuk tahun berikutnya. Tanpa pemahaman yang
   jelas tentang tren penjualan tahunan, DQLab Store berisiko merencanakan strategi yang tidak akurat dan kehilangan peluang pertumbuhan.
   <br>
   <br>
3. DQLab Store belum melakukan identifikasi pengguna dengan rata-rata transaksi terbesar pada tahun 2020. Hal ini mengakibatkan perusahaan kesulitan untuk mengenali pelanggan bernilai tinggi
   yang berpotensi memberikan kontribusi signifikan terhadap pendapatan. Tanpa pengetahuan ini, DQLab Store tidak dapat merancang program loyalitas atau penawaran eksklusif yang dapat
   meningkatkan retensi dan loyalitas pelanggan.
   <br>
   <br>
4. Perusahaan belum melakukan analisis mendalam tentang kategori produk yang paling laris di tahun 2020. Tanpa informasi ini, DQLab Store mungkin kesulitan mengoptimalkan stok dan strategi
   pemasaran mereka. Kekurangan data ini dapat mengakibatkan ketidakseimbangan dalam inventaris, dimana produk yang laris cepat habis sementara produk yang kurang diminati menumpuk di gudang.
   Selain itu, tanpa fokus yang jelas pada kategori produk yang populer, kampanye pemasaran mungkin tidak mencapai hasil maksimal.
   <br>
   <br>
5. DQLab Store tidak memiliki sistem yang efektif untuk mengidentifikasi pembeli yang masuk dalam kategori High Value. Tanpa mengetahui siapa saja pelanggan bernilai tinggi ini, perusahaan tidak
   bisa memberikan layanan khusus atau promosi yang ditargetkan untuk mempertahankan mereka. Akibatnya, ada risiko kehilangan pelanggan-pelanggan penting yang dapat memberikan kontribusi
   signifikan terhadap pendapatan perusahaan.
   <br>
   <br>
6. Perusahaan belum memiliki mekanisme yang jelas untuk mengidentifikasi pengguna yang termasuk dropshipper. Hal ini membuat DQLab Store kesulitan dalam menyusun strategi pemasaran yang spesifik
   untuk segmen ini. Dropshipper memiliki kebutuhan dan perilaku pembelian yang berbeda dari konsumen akhir, dan tanpa informasi ini, perusahaan mungkin tidak dapat memaksimalkan potensi
   kolaborasi dan penjualan dari segmen dropshipper.
   <br>
   <br>
7. DQLab Store belum mampu mengidentifikasi dengan tepat siapa saja pengguna yang termasuk reseller offline. Reseller offline memainkan peran penting dalam distribusi produk, dan tanpa informasi
   ini, perusahaan tidak dapat merancang program dukungan atau insentif yang sesuai. Hal ini dapat menghambat pertumbuhan penjualan dan mengurangi efektivitas strategi pemasaran yang ditujukan
   untuk reseller.
   <br>
   <br>
8. Perusahaan belum mengidentifikasi pengguna yang berperan ganda sebagai penjual dan pembeli. Pengguna seperti ini memiliki wawasan yang unik dan dapat menjadi mitra strategis dalam
   mengembangkan ekosistem bisnis. Tanpa mengetahui siapa mereka, DQLab Store melewatkan peluang untuk memahami dinamika pasar lebih baik dan memaksimalkan potensi kerjasama bisnis.
   <br>
   <br>
9. DQLab Store belum melakukan analisis tentang berapa lama transaksi setiap bulannya dibayar. Tanpa informasi ini, perusahaan kesulitan mengelola arus kas dan kebijakan kredit dengan efektif.
   Kekurangan data ini dapat mengakibatkan masalah likuiditas dan menghambat kemampuan perusahaan untuk merencanakan pengeluaran dan investasi dengan tepat.

# Dataset
<br> ![image](https://github.com/user-attachments/assets/49607237-d615-4351-9f0d-8e77604cbda2)
<br>
<br>**Dataset Link:** https://storage.googleapis.com/dqlab-dataset/dataset%20lomba%204%20sept%202020.zip
<br>
<br>Dataset yang digunakan merupakan data dari DQLab Store yang merupakan e-commerce dimana pembeli dan penjual saling bertemu. 
<br>Pengguna bisa membeli barang dari pengguna lain yang berjualan. Setiap pengguna bisa menjadi pembeli sekaligus penjual.
<br>
<br>Ada 4 tabel yang tersedia,
1. users, berisi detail data pengguna. Berisi,
   <br> a. user_id : ID pengguna
   <br> b. nama_user : nama pengguna
   <br> c. kodepos : kodepos alamat utama dari pengguna
   <br> d. email : email dari pengguna
   <br>
   <br>
2. products, berisi detail data dari produk yang dijual. Berisi,
   <br> a. product_id : ID produk
   <br> b. desc_product : nama produk
   <br> c. category : kategori produk
   <br> d. base_price : harga asli dari produk
   <br>
   <br>
3. orders, berisi transaksi pembelian dari pembeli ke penjual. Berisi,
   <br> a. order_id : ID transaksi
   <br> b. seller_id : ID dari pengguna yang menjual
   <br> c. buyer_id : ID dari pengguna yang membeli
   <br> d. kodepos : kodepos alamat pengirimian transaksi (bisa beda dengan alamat utama)
   <br> e. subtotal : total harga barang sebelum diskon
   <br> f. discount : diskon dari transaksi
   <br> g. total : total harga barang setelah dikurangi diskon, yang dibayarkan pembeli
   <br> h. created_at : tanggal transaksi
   <br> i. paid_at : tanggal dibayar
   <br> j. delivery_at : tanggal pengiriman
   <br> k. order_details, berisi detail barang yang dibeli saat transaksi. Berisi,
   <br> l. order_detail_id : ID table ini
   <br> m. order_id : ID dari transaksi
   <br> n. product_id : ID dari masing-masing produk transaksi
   <br> o. price : harga barang masing-masing produk
   <br> p. quantity : jumlah barang yang dibeli dari masing-masing produk
