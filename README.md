# DQLab SQL Project: Data Analysis for E-Commerce Challenge (SQL)
# Project Background

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
   <br>a. user_id : ID pengguna
   <br>b. nama_user : nama pengguna
   <br>c. kodepos : kodepos alamat utama dari pengguna
   <br>d. email : email dari pengguna
   <br>
   <br>
2. products, berisi detail data dari produk yang dijual. Berisi,
   <br>a. product_id : ID produk
   <br>b. desc_product : nama produk
   <br>c. category : kategori produk
   <br>d. base_price : harga asli dari produk
   <br>
   <br>
3. orders, berisi transaksi pembelian dari pembeli ke penjual. Berisi,
   <br>a. order_id : ID transaksi
   <br>b. seller_id : ID dari pengguna yang menjual
   <br>c. buyer_id : ID dari pengguna yang membeli
   <br>d. kodepos : kodepos alamat pengirimian transaksi (bisa beda dengan alamat utama)
   <br>e. subtotal : total harga barang sebelum diskon
   <br>f. discount : diskon dari transaksi
   <br>g. total : total harga barang setelah dikurangi diskon, yang dibayarkan pembeli
   <br>h. created_at : tanggal transaksi
   <br>i. paid_at : tanggal dibayar
   <br>j. delivery_at : tanggal pengiriman
   <br>k. order_details, berisi detail barang yang dibeli saat transaksi. Berisi,
   <br>l. order_detail_id : ID table ini
   <br>m. order_id : ID dari transaksi
   <br>n. product_id : ID dari masing-masing produk transaksi
   <br>o. price : harga barang masing-masing produk
   <br>p. quantity : jumlah barang yang dibeli dari masing-masing produk
