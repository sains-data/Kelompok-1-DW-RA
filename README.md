# Data Warehouse Dalam Industri Retail

## 📊 Dataset Overview
Proyek ini menganalisis dataset Superstore dari Kaggle, dengan fokus pada kinerja penjualan, perilaku pelanggan, dan wawasan bisnis untuk jaringan superstore ritel.

**Dataset Source**: [Kaggle - Superstore Dataset](https://www.kaggle.com/datasets/roopacalistus/superstore)

---

## 1. Ringkasan Proyek dan Latar Belakang

### Latar Belakang
Superstore merupakan salah satu retailer terbesar yang menjual berbagai produk mulai dari furniture, office supplies, hingga technology. Dengan pertumbuhan bisnis yang pesat, perusahaan membutuhkan analisis mendalam terhadap data penjualan untuk mengoptimalkan strategi bisnis dan meningkatkan profitabilitas.

### Permasalahan Bisnis
- Bagaimana tren penjualan dan profitabilitas di berbagai kategori produk?
- Siapa customer segment yang paling menguntungkan?
- Wilayah mana yang memberikan kontribusi revenue tertinggi?
- Produk apa yang perlu difokuskan atau dihentikan?

### Objektif Proyek
- Menganalisis performa penjualan berdasarkan kategori, region, dan customer segment.
- Mengidentifikasi produk dan customer yang paling profitable.
- Memberikan rekomendasi strategis untuk meningkatkan profitabilitas.
- Membangun dashboard interaktif untuk monitoring KPI.

---

## 2. Tujuan dan Ruang Lingkup Sistem

### Tujuan Utama
1. **Analisis Deskriptif**: Memahami pola penjualan historis dan tren bisnis
2. **Analisis Profitabilitas**: Mengidentifikasi produk dan segmen yang paling menguntungkan
3. **Segmentasi Customer**: Mengelompokkan customer berdasarkan behavior pembelian
4. **Forecasting**: Memprediksi tren penjualan untuk periode mendatang
5. **Dashboard Development**: Membangun visualisasi interaktif untuk stakeholder

### Ruang Lingkup
- **Data Temporal**: 2014-2017 (4 tahun data penjualan)
- **Geografis**: United States (3 regions, 49 states, 531 cities)
- **Produk**: 3 kategori utama (Furniture, Office Supplies, Technology)
- **Customer**: 3 segmen (Consumer, Corporate, Home Office)

---

## 3. Metodologi

### Tools dan Teknologi
- **Storage**: MySQL/PostgreSQL database
- **Processing**: SQL queries dan Excel/Google Sheets
- **Analytics**: SQL untuk data analysis
- **Visualization**: Tableau Desktop/Public
- **Data Import**: CSV import ke SQL database

### Tahapan Analisis

#### **Misi 1: Analisis Kebutuhan & Pemecahan Masalah**
- Identifikasi stakeholder utama dan tujuan bisnis
- Analisis kebutuhan informasi setiap divisi
- Penentuan metrik kunci (fakta) dan dimensi
- Pemecahan masalah bisnis melalui pendekatan data-driven

#### **Misi 2: Desain Konseptual**
- Perancangan model dimensional (star schema/snowflake)
- Identifikasi fact table dan dimension table
- Penentuan grain level dan hierarchy dimensi
- Pemodelan hubungan antar tabel

#### **Misi 3: Desain Logikal & Fisik**
- Transformasi model konseptual ke struktur database
- Optimalisasi struktur tabel dan indexing
- Penentuan tipe data dan constraint
- Desain ETL (Extract, Transform, Load) process

#### **Misi 4: Implementasi, Reporting, & Produksi**
- Implementasi data warehouse di environment produksi
- Pengembangan dashboard dan laporan bisnis
- Testing dan validasi data quality
- Deployment dan maintenance system

---

## 4. Analisis Kebutuhan (Misi 1)
Analisis kebutuhan berfokus pada identifikasi stakeholder utama dan tujuan bisnis mereka dalam konteks analisis data superstore. Dari sini, ditentukan metrik (fakta) dan konteks (dimensi) yang krusial untuk data warehouse.

## Stakeholder Utama & Tujuan Bisnis Kunci:

### 🏢 **CEO**
- Memastikan pertumbuhan bisnis dan profitabilitas menyeluruh
- Mengidentifikasi peluang ekspansi pasar dan segmen baru
- Menentukan strategi kompetitif berdasarkan performa regional

### 👨‍💼 **Manajer Umum**
- Merencanakan, mengarahkan, dan mengelola operasi bisnis secara menyeluruh
- Mengoptimalkan efisiensi operasional dan alokasi sumber daya
- Memantau kinerja seluruh divisi dan mengidentifikasi area perbaikan

### 💰 **Tim Keuangan**
- Mengoptimalkan profitabilitas dan kontrol biaya operasional
- Menganalisis margin keuntungan per produk, kategori, dan wilayah
- Mengelola anggaran dan mengidentifikasi peluang penghematan

### 📊 **Tim Pemasaran**
- Meningkatkan konversi penjualan dan retensi pelanggan
- Menganalisis efektivitas strategi pemasaran per segmen
- Menyesuaikan penawaran produk ke wilayah dan kelompok pelanggan tertentu

### 🚚 **Tim Logistik**
- Meminimalkan stok berlebih dan kekurangan stok
- Mengoptimalkan distribusi dan pengiriman berdasarkan wilayah
- Mengelola inventory berdasarkan pola penjualan historis

### 📈 **Tim Analisis Data**
- Menyediakan *insights* bisnis dan analisis prediktif
- Membuat segmentasi pelanggan dan analisis perilaku konsumen
- Mengidentifikasi tren penjualan dan pola musiman

## Fakta Utama yang Diidentifikasi:
- **Sales** (Nilai Penjualan)
- **Quantity** (Jumlah Unit Terjual)
- **Discount** (Diskon yang Diberikan)
- **Profit** (Keuntungan Bersih)

## Dimensi Utama yang Diidentifikasi:
- **DimCustomer** (Segmen Pelanggan)
- **DimProduct** (Kategori, Sub-Kategori Produk)
- **DimGeography** (Negara, State, Kota, Region, Kode Pos)
- **DimShipMode** (Mode Pengiriman)
---

## 5. Desain Konseptual, Logikal, dan Fisikal (Misi 2 & 3)
Pendekatan Star Schema diterapkan dalam perancangan data warehouse untuk memaksimalkan kinerja analisis data dan kemudahan navigasi struktur informasi.

![Diagram Star Schema](images/schema-star.png)

*Gambar 1. Skema bintang*

### Desain Konseptual

**Fact Tables**:
- **fakta_sales**: Tabel utama yang menyimpan data penjualan

**Dimension Tables**:
- **dim_location**: Data lokasi (country, city, state, region, postal_code)
- **dim_customer**: Data pelanggan (customer_id, segment)
- **dim_product**: Data produk (product_id, category, sub_category)
- **dim_time**: Data waktu (time_id, year, month, day)
  
### Desain Logikal

**Relasi Tabel**:
- **Semua dimension tables** terhubung ke **fact table** melalui foreign keys
- Menggunakan model **star schema** untuk optimasi query analytical

### Desain Fisikal
Desain fisikal pada data warehouse Superstore menerapkan strategi pengindeksan (indexing) yang optimal untuk meningkatkan performa query, terutama untuk operasi yang melibatkan penyaringan (WHERE), penggabungan tabel (JOIN), dan pengelompokan data (GROUP BY). Index berperan krusial dalam mempercepat akses data, mengurangi waktu eksekusi query, dan meningkatkan efisiensi sistem secara keseluruhan, terutama ketika menangani volume data yang besar. 

### Rasionalisasi Pemilihan Kolom Index

- **`Customer_ID`**:  
  Mempercepat join dengan tabel `dim_customer` untuk analisis:
  - Segmentasi pelanggan
  - Analisis RFM (Recency, Frequency, Monetary)
  - Analisis loyalitas pelanggan

- **`Product_ID`**:  
  Dioptimalkan untuk query terkait kinerja produk seperti:
  - `"produk terlaris"`
  - `"analisis margin per item"`

- **`Region` dan `Category` (Composite Index)**:  
  Mendukung query multidimensi seperti:
  - `"penjualan kategori Furniture di Region Barat"`
---

## 6. Proses Implementasi (Misi 4)
1. memasukkan data
    proses ini merupakan tahap awal dari pembangunan awal dalam data warehouse
   data ini mencakup pelanggan, informasi geografis, kategori produk, serta metrik bisnis utama seperti pengiriman, diskon, dan profit.

![Superstore](images/memasukkan-data.jpg)

*Gambar 2. Input data*

Hasil: Pada tahap ekstraksi, data mentah dari Superstore yang tersimpan dalam format CSV diproses. Data yang diekstrak mencakup berbagai dimensi penting seperti segmentasi pelanggan, informasi geografis, kategori produk, serta metrik bisnis utama seperti pengiriman, diskon, dan profit. 

![Superstore](images/dataset.jpg)

*Gambar 3. Dataset Superstore*

2. Mengembangkan Scrit PHP untuk Melakukan Proses ETL(Extract,Transform,Load)
   pengembangan ini dimulai dari koneksi ke database, pembacaan file CSV, hingga load data pengembangan ini merupakan tahap awal integrasi data dari sumber eksternal
   
![Superstore](images/pengembangan-ETL.jpg)

*Gambar 4. Pengembangan ETL*

3. Analisis Data
Implementasi *Online Analytical Processing* (OLAP) dalam sistem data warehouse ini fokus pada proses agregasi data untuk memberikan pandangan menyeluruh terhadap kinerja bisnis perusahaan. Melalui teknik agregasi, data transaksional yang kompleks diolah menjadi informasi strategis yang mudah dipahami, dengan emphasis utama pada evaluasi total keuntungan dan analisis profit yang dihasilkan dari berbagai dimensi bisnis seperti kategori produk, wilayah geografis, dan segmentasi pelanggan.
  
---

## 7. Hasil Implementasi
1. Analisis ini menunjukkan performa bisnis secara keseluruhan dengan menghitung akumulasi penjualan dan profit. Data mengungkapkan bahwa perusahaan berhasil mencapai total penjualan sebesar $2.3 juta dengan profit $286 ribu, yang berarti margin profit keseluruhan berada di kisaran 12.5%. Dari hasil tersebut, dapat diinterpretasikan bahwa total penjualan yang cukup besar menunjukkan volume transaksi yang tinggi. Angka ini memberikan gambaran dasar tentang keberjalanan finansial perusahaan yang baik dan dapat membantu jalannya analisis staratergi pemasaran produk mana yang lebih menguntungkan, mengeliminasi kategori produk yang merugikan perusahaan, serta menilai performa perusahaan secara keseluruhan pada waktu rentang tertentu.

![Superstore](images/analitik1.jpg)

*Gambar 5. Performa bisnis berdasarkan total keuntungan dan profit*

2. Selanjutnya dilakukan analisis profit berdasarkakn performa, dengan menganalisi pembagian penjualan berdasarkan kategori produk. Dari data dapat diinterpretasikan bahwa *Technology* menjadi penyumbang terbesar dengan nilai $836 ribu, diikuti *Furniture* ($742 ribu) dan *Office Supplies* ($719 ribu). Yang menarik, meskipun *Technology* menjadi kategori tertinggi, ketiga kategori yang lain sebenarnyaa menunjukkan distribusi yang cukup seimbang dengan selisih tidak lebih dari 15% antara kategori tertinggi dan terendah, mengindikasikan diversifikasi produk yang baik.
Oleh karena itu, karena data menunjukkan keseimbangan penjualan antar kategori cukup baik maka data dapat digunakan untuk merancang strategy promosi dan pengembangan produk berdasarkan kinerja kategori 
![Superstore](images/analitik2.jpg)

*Gambar 6. Profit berdasarkan kategori*

3. Analisis regional mengungkap disparitas profit yang signifikan di mana wilayah *West* unggul dengan profit $108 ribu, hampir tiga kali lipat dibanding wilayah *Central* yang hanya $39 ribu. Pola ini menunjukkan bahwa performa *West* merupakan penjualan yang paling unggul dibanding wilayah lainnya, yang kemungkinan disebabkan oleh strategi pemasaran yang lebih efektif atau tingkat permintaan pasar yang tinggi di wilayah tersebut. Sebaliknya, wilayah *Central* mencatatkan profit terendah, yang mengindikasikan perlunya evaluasi terhadap strategi distribusi, promosi, atau preferensi konsumen di wilayah tersebut. Perbedaan signifikan antar wilayah ini menunjukkan adanya ketimpangan performa regional yang dapat dijadikan dasar untuk perbaikan strategi bisnis secara lebih spesifik dan tersegmentasi.
![Superstore](images/analitik3.jpg)

*Gambar 7. Profit berdasarkan wilayah*

4. Pemetaan geografis mengkonfirmasi bahwa 80% penjualan terkonsentrasi di lima kota utama, dengan New York City sebagai pasar terbesar ($256 ribu). Disusul oleh Los Angeles sebesar 175.851,34, kemudian Seattle (135.540,12), San Francisco (119.579,51), dan Philadelphia (109.077,03).Interpretasi data menunjukkan bahwa New York City menjadi pasar terbesar dikarenakan New York merupakan kota besar dengan populasi yang tinggi menjadikannya  kota tersbut memiliki aktivitas ekonomi yang tinggi.  Sementara dengan kota lainnya, meskipun tidak sebesar kota New York tetapi menunjukkan performa penjualan yang kuat, hanya saja dapat lebih lagi difokuskan dalam hal  pengembangan pasar yang tepat. Data ini dapat menjadi acuan dalam merancang strategi pemasaran dan distribusi, dengan memberikan perhatian khusus pada kota-kota dengan kontribusi penjualan tertinggi untuk memaksimalkan potensi pasar dan meningkatkan efisiensi operasional.
![Superstore](images/analitik4.jpg)

*Gambar 8. Profit berdasarkan kota*

5. Ketika melihat lebih detail ke setiap kategori, terungkap bahwa meskipun Furniture memiliki volume penjualan tinggi, margin profitnya hanya 2.49% karena tingginya diskon (rata-rata 17.39%). Sebaliknya, *Technology* dengan transaksi lebih sedikit justru memberikan kontribusi profit terbesar berkat margin sehat 17.4%, menunjukkan efisiensi bisnis yang lebih baik.
![Superstore](images/Analisis-Performa-Kategori.jpg)

*Gambar 9. Analisis performa berdasarkan kategori*

6. Berdasarkan kombinasi wilayah dan segmen konsumen mengungkap bahwa segmen *Home Office* di *East* memberikan margin profit tertinggi (20.95%), sementara *Consumer* di *Central* hanya 3.4%. Temuan ini mengindikasikan perlunya penyesuaian strategi pemasaran khususnya untuk segmen *Consumer* di wilayah *Central*  yang kurang profitable.
![Superstore](images/Analisis-Region-Segment.jpg)

*Gambar 10. Analisis region dan segmentasi*

7. Analisis sub-kategori menunjukkan *Copiers* sebagai bintang profit dengan margin 37.2%, jauh di atas rata-rata. Yang mengejutkan, meskipun *Phones* memiliki volume transaksi tertinggi (889 transaksi), marginnya relatif rendah (13.49%), menunjukkan bahwa popularitas tidak selalu berbanding lurus dengan profitabilitas.
![Superstore](images/Analisis-Top-Performing-Products.jpg)

*Gambar 11. Analisis top performing product*


---

## 8. Evaluasi
### Pencapaian Tujuan

Implementasi data warehouse Superstore telah berhasil mencapai beberapa tujuan utama:

1. **Integrasi Data**: Berhasil mengintegrasikan data dari berbagai sumber menjadi satu repositori terpusat
2. **Proses ETL**: Script PHP berhasil melakukan ekstraksi, transformasi, dan loading data secara efektif
3. **Analisis OLAP**: Implementasi analisis multidimensional memberikan insight bisnis yang berharga

### Tantangan dan Solusi

1. **Kualitas Data**: Tantangan dalam memastikan konsistensi dan akurasi data
   - Solusi: Implementasi validasi data dalam proses ETL
2. **Performa Query**: Optimasi query untuk analisis data yang besar
   - Solusi: Implementasi indeks dan optimasi struktur database

---

# 9. Rencana Pengembangan ke Depan

## **Perbaikan Jangka Pendek (3 bulan)**
- **Enhanced SQL Analytics**:  
  Mengembangkan stored procedure untuk perhitungan kompleks seperti:  
  ✅ Customer lifetime value  
  ✅ Tren profitabilitas produk  

---

## **Tujuan Jangka Menengah (6-12 bulan)**  
- **Analisis Musiman**:  
  Kueri SQL untuk identifikasi:  
  🍂 Tren seasonal berdasarkan ship mode  
  🗺️ Pola regional  

- **Segmentasi Pelanggan**:  
  Analisis RFM lanjutan dengan SQL untuk:  
  🎯 Target pelanggan lebih akurat berdasarkan perilaku segment  

---

## **Visi Jangka Panjang (1-2 tahun)**  
- **Integrasi Prediktif Analytics**:  
  Model forecasting dasar di Excel untuk:  
  🔮 Prediksi penjualan berdasarkan tren historis  

- **Sistem Pelaporan Otomatis**:  
  Pembuatan:  
  ⏰ Laporan Tableau terjadwal untuk review bisnis bulanan  

---

## 10. Tim Proyek

- Marhanny Zahra Nurendra 	120450017
- Eunike Bunga Santa		121450095
- Muhammad Bayu Syuhada	122450007
- Johannes Krisjon Silitonga	122450043
- Rian Bintang Wijaya		122450094
- Bastian Heskia Silaban	122450130

---

## 📁 Project Structure
```
superstore-analysis/
├── data/
│   ├── raw/
│   │   └── superstore.csv
│   ├── processed/
│   │   └── cleaned_superstore.csv
│   └── sql/
│       └── database_schema.sql
├── excel_analysis/
│   ├── data_exploration.xlsx
│   ├── pivot_analysis.xlsx
│   └── summary_report.xlsx
├── sql_queries/
│   ├── basic_analysis.sql
│   ├── advanced_queries.sql
│   └── kpi_calculations.sql
├── tableau/
│   ├── superstore_dashboard.twb
│   ├── executive_summary.twb
│   └── detailed_analysis.twb
└── documentation/
    ├── data_dictionary.xlsx
    └── user_guide.pdf
```
