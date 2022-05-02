# E-Commerce-Challenge_SQL

**#menghitung jumlah baris pada data products**
select * from products;
select count(distinct product_id) as jumlah_baris from products;

**#menghitung jumlah kategori pada data products**
SELECT COUNT(DISTINCT category) FROM products;

**#mencari kolom yang kosong pada data products**
SELECT count(*) as jumlah_null FROM products 
WHERE product_id IS NULL
AND desc_product IS NULL
AND category IS NULL
AND base_price IS NULL;

**#mengetahui jumlah baris pada data orders**
SELECT COUNT(*) AS jumlah_baris FROM orders; 

**#mencari data null pada data orders**
SELECT COUNT(*) AS jumlah_null FROM orders
WHERE order_id IS NULL
AND seller_id IS NULL
AND buyer_id IS NULL
AND kodepos IS NULL
AND subtotal IS NULL
AND discount IS NULL
AND total IS NULL 
AND paid_at IS NULL
AND created_at IS NULL
AND delivery_at IS NULL;

**#menghitung jumlah user pada data users**
SELECT COUNT(*) AS jumlah_user FROM users;

**#menghitung jumlah baris pada data users**
select count(distinct user_id) as jumlah_baris from users;

**#Mencari jumlah data yang kosong pada data users**
select count(*) as jumlah_null from users
where user_id is null
and nama_user is null
and kodepos is null
and email is null;

**#Mencari jumlah baris pada data order_details**
SELECT count(*) as jumlah_baris FROM order_details;

**#Mencari data yang kosong pada data order_details**
select count(*) as jumlah_null from order_details
where order_detail_id is null
and order_id is null
and product_id is null
and price is null
and quantity is null;

**#Mencari jumlah_transaksi tiap bulan**
SELECT DATE_FORMAT(created_at, '%Y-%m') AS bulan_tahun, COUNT(1) AS jumlah_transaksi 
FROM orders
GROUP BY 1
ORDER BY 1;

**#Mencari Data Transaksi yang tidak dibayar**
SELECT COUNT(paid_at) AS jumlah_transaksi_tidak_dibayar
FROM orders
WHERE paid_at ='NA';

**#Mencari jumlah transaksi yang sudah dibayar tapi tidak dikirim**
SELECT COUNT(delivery_at) AS paid_not_deliv FROM orders
WHERE paid_at != 'NA' AND delivery_at ='NA';

**#Mencari jumlah transaksi yang tidak dikirim, baik yang dibayar maupun tidak**
SELECT COUNT(delivery_at) AS not_deliv_paid_unpaid FROM orders
WHERE delivery_at = 'NA';

**#Mencari transaksi yang tgl dikirim sama dengan tgl dibayar**
SELECT COUNT(delivery_at) AS tgl_kirim_sama_dgn_tgl_bayar 
FROM orders WHERE delivery_at = paid_at;

**#Mencari jumlah Pengguna**
SELECT COUNT(user_id) AS jumlah_pengguna FROM users;

**#Mencari pengguna yang pernah menjadi pembeli**
SELECT COUNT(user_id) AS user_buyer FROM users
WHERE user_id IN (SELECT DISTINCT buyer_id FROM orders);

**#Mencari pengguna yang pernah menjadi penjual**
SELECT COUNT(user_id) AS user_seller FROM users
WHERE user_id IN (SELECT DISTINCT seller_id FROM orders);

**#Mencari pengguna yang pernah menjadi penjual dan pembeli**
SELECT COUNT(user_id) AS user_seller_and FROM users
WHERE user_id IN (SELECT DISTINCT seller_id FROM orders) 
AND user_id IN (SELECT DISTINCT buyer_id FROM orders);

**#Mencari pengguna yang tidak pernah menjadi penjual dan pembeli**
SELECT COUNT(user_id) AS user_seller_and FROM users
WHERE user_id NOT IN (SELECT DISTINCT seller_id FROM orders) 
AND user_id NOT IN (SELECT DISTINCT buyer_id FROM orders);

**#Mencari TOP 5 BUYER ALL TIME (Cara 1)**
SELECT user_id, nama_user, SUM(total) AS total_pembelian
FROM users
JOIN orders ON user_id = buyer_id
GROUP BY 1
ORDER BY 3 DESC, 2 LIMIT 5;

**#Mencari TOP 5 BUYER ALL TIME (Cara 2)**
SELECT user_id, nama_user, SUM(total) AS total_pembelian
FROM users
JOIN orders ON user_id = buyer_id
GROUP BY 1
ORDER BY 3 DESC LIMIT 10;

**#Mencari pengguna yang tidak pernah menggunakan diskon ketika membeli barang 
#dan merupakan 5 pembeli dengan transaksi terbanyak**
SELECT user_id,nama_user, COUNT(created_at) total_frekuensi_beli
FROM users u
JOIN orders o
ON  u.user_id = o.buyer_id
WHERE discount = 0
GROUP BY 1
ORDER BY 3 DESC LIMIT 10;

**#Mencari pengguna yang bertransaksi setidaknya 1 kali setiap bulan 
#di tahun 2020 dengan rata-rata total amount per transaksi 
#lebih dari 1 Juta**
select buyer_id, email, rata_rata, month_count
from (select trnsct.buyer_id, rata_rata, jumlah_order, month_count
       from (select buyer_id, round(avg(total),2) as rata_rata 
		from orders where date_format(created_at,'%Y') = '2020'
        group by 1 having rata_rata > 1000000 order by 1) 
        as trnsct
			join (SELECT buyer_id, count(order_id) as jumlah_order, 
					count(distinct date_format(created_at,'%m')) as month_count from orders
				     where date_format(created_at,'%Y') = '2020'
                     group by 1
                     having month_count >= 5 and jumlah_order >= month_count order by 1) as months 
                     on trnsct.buyer_id = months.buyer_id) as trnsct_month
					 join users on buyer_id = user_id;
                     
**#Mencari Domain Email Seller**
select email as email_seller, substr(email, instr(email, '@') +1) as domain_email from users
where user_id in (select seller_id from orders) order by 2;

**#Mencari top 5 produk yang dibeli di bulan desember 2019 
#berdasarkan total quantity**
select desc_product as nama_barang, sum(quantity) as total_quantity 
from order_details od 
join products p
on od.product_id = p.product_id
join orders o
on od.order_id = o.order_id
where created_at between '2019-12-01' and '2019-12-31'
group by 1
order by 2 desc limit 10;

**#Mencari 5 Produk Terlaris**
select desc_product as nama_barang, sum(quantity) as total_quantity 
from order_details od 
join products p
on od.product_id = p.product_id
join (select order_id from orders
		where created_at between '2019-12-01' and '2019-12-31') as des_2019
on od.order_id = des_2019.order_id
group by 1
order by 2 desc limit 5;

**#Mencari 10 Transaksi terbesar user 12476**
select seller_id, buyer_id, sum(total) as jumlah_transaksi, created_at as tanggal_transaksi
from orders
where buyer_id = 12476
group by 4
order by 3 desc;

**#Mencari summary transaksi per bulan di tahun 2020. **
select date_format(created_at, '%Y-%m') as tahun_bulan, 
count(1) as jumlah_transaksi, sum(total) as total_nilai_transaksi
from orders
where date_format (created_at,'%Y') = '2020'
group by 1
order by 1; 

**#Mencari 10 pembeli dengan rata-rata nilai transaksi terbesar 
#yang bertransaksi minimal 2 kali di Januari 2020**
select buyer_id, count(created_at) as jumlah_transaksi, 
round(avg(total)) as avg_nilai_transaksi
from orders
where created_at between '2020-01-01' and '2020-01-31'
group by 1
having count(1) >= 2
order by 3 desc limit 10;

**#Mencari dan menampilkan semua nilai transaksi minimal 
#20,000,000 di bulan Desember 2019**
select nama_user as nama_pembeli, total as nilai_transaksi, 
created_at as tanggal_transaksi
from users u
join orders o
on u.user_id = o.buyer_id
where created_at between '2019-12-01' and '2019-12-31' 
and total >= 20000000 
group by 1
order by 1 ;

**#Mencari kategori produk terlaris 2020
# 5 Kategori dengan total quantity terbanyak di tahun 2020, 
#hanya untuk transaksi yang sudah terkirim ke pembeli.**
select category, sum(quantity) as total_quantity, sum(price) as total_price
from order_details od
join products p
on od.product_id = p.product_id
join (select order_id from orders
		where created_at >= '2020-01-01' and delivery_at IS NOT NULL) as year
        on od.order_id = year.order_id
group by 1
order by 2 desc limit 5; 

**#Mencari pembeli high value yang sudah bertransaksi lebih dari 5 kali, 
#dan setiap transaksi lebih dari 2,000,000**
select nama_user as nama_pembeli, count(created_at) as jumlah_transaksi,
sum(total) as total_nilai_transaksi, min(total) as min_nilai_transaksi
from users u
join orders o 
on  buyer_id = user_id
group by 1
having count(created_at) > 5 and min(total) > 2000000 
order by 3;

**#Mencari mencari tahu pengguna yang menjadi dropshipper, 
#yakni pembeli yang membeli barang akan tetapi dikirim ke orang lain. 
#Ciri-cirinya yakni transaksinya banyak, dengan alamat yang berbeda-beda
#Mencari pembeli dengan 10 kali transaksi atau lebih yang alamat pengiriman 
#transaksi selalu berbeda setiap transaksi**
select nama_user as nama_pembeli, jumlah_transaksi, 
distinct_kodepos, total_nilai_transaksi, avg_nilai_transaksi
from users
join (select buyer_id, count(distinct kodepos) as distinct_kodepos, count(buyer_id) as jumlah_transaksi, 
	    sum(total) as total_nilai_transaksi, round(avg(total),0) as avg_nilai_transaksi
        from orders
        group by 1
        having count(created_at) >= 10 and count(created_at) = count(distinct kodepos)
        order by 3 desc) as transaksi_dropshipper
on users.user_id = transaksi_dropshipper.buyer_id
group by 1
order by 2 desc;

**#Mencari Reseller Offline
#Mencari pembeli yang punya 8 tau lebih transaksi 
#yang alamat pengiriman transaksi sama dengan alamat pengiriman utama, 
#dan rata-rata total quantity per transaksi lebih dari 10**
select nama_user as nama_pembeli, count(created_at) as jumlah_transaksi, 
sum(total) as total_nilai_transaksi, avg(total) as avg_nilai_transaksi, 
avg(total_quantity) as avg_quantity_per_transaksi
from orders
inner join users on buyer_id = user_id
inner join (select order_id, sum(quantity) as total_quantity from order_details group by 1) 
as summary_order using(order_id) 
where orders.kodepos = users.kodepos
group by user_id, nama_user
having count(created_at)>=8  and avg(total_quantity)>10
order by 3 desc;

**#Mencari mencari penjual yang juga pernah bertransaksi 
#sebagai pembeli minimal 7 kali**
select 
	nama_user as nama_pengguna
	, jumlah_transaksi_beli
	, jumlah_transaksi_jual 
from users
inner join 
	(select 
	 buyer_id
	 , count(created_at) as jumlah_transaksi_beli 
	 from orders 
	 group by 1) as buyer on buyer_id = user_id
inner join 
	(select 
	 seller_id
	 , count(created_at) as jumlah_transaksi_jual 
	 from orders 
	 group by 1) as seller on seller_id = user_id 
where jumlah_transaksi_beli >= 7 
order by 1;

**#Mencari Lama Transaksi Dibayar**
select
 extract(year_month from created_at) as tahun_bulan, 
 count(1) as jumlah_transaksi,
 avg(datediff(paid_at, created_at)) as avg_lama_dibayar,
 min(datediff(paid_at, created_at)) as min_lama_dibayar,
 max(datediff(paid_at, created_at)) as max_lama_dibayar 
from orders 
where paid_at is not null
group by 1 
order by 1;

        
