# Transaction Data Validation & Risk Review

Sebuah proyek validasi data dan pengidentifikasi risiko berbasis atas data transaksi ritel,
yang dirancang untuk mendukung alur kerja pemantauan risiko dan kepatuhan.

## Latar Belakang
Sebelum data transaksi digunakan untuk pelaporan bisnis, perlu terlebih dahulu dipastikan
kelengkapan, konsistensi, dan validitasnya terhadap data induk (pelanggan, produk, toko).
Kumpulan data ritel ini digunakan sebagai simulasi—pendekatan validasi data dan
penandaan berdasarkan aturan yang dijelaskan di sini dapat diterapkan pada konteks pemantauan risiko
dan kepatuhan di bidang apa pun, termasuk keamanan informasi.

## Apa yang Telah Dilakukan
- Memeriksa kelengkapan dan duplikat dalam data master (pelanggan, produk, toko)
- Verifikasi integritas referensial (customer_id, product_id, store_id dibandingkan dengan data master)
- Verifikasi kepatuhan harga transaksi terhadap daftar harga resmi
- Penandaan berdasarkan aturan: diskon yang melebihi batas kebijakan, biaya pengiriman yang tidak tercatat
- Ringkasan pengendalian dalam bentuk tabel status (Lulus / Anomali)

## Alat
Python (pandas, matplotlib) — Google Colab

## Temuan Utama
- Seluruh data utama telah diverifikasi dalam kondisi bersih—0 ID duplikat, 0 nilai kosong
- Seluruh 10.970 transaksi menggunakan harga sesuai dengan daftar harga resmi (0 penyimpangan)
- 327 transaksi (3,0%) memiliki diskon yang melebihi batas kebijakan 30%, tersebar merata
  di ketiga saluran (Toko 3,1%, Marketplace 3,0%, Online 2,9%)
- 156 transaksi online/marketplace tidak memiliki data biaya pengiriman yang tercatat
- 358 transaksi langsung di toko fisik tidak memiliki customer_id — pola yang normal, bukan anomali

## Rekomendasi
- Tinjau 327 transaksi dengan diskon tinggi untuk memastikan otorisasi yang sah
- Koordinasikan dengan tim pencatatan transaksi untuk menutup kesenjangan data biaya pengiriman di
  saluran online/marketplace

## Keterbatasan & Asumsi
Ambang batas diskon 30% digunakan sebagai asumsi kewajaran untuk tujuan pelatihan,
bukan sebagai kebijakan resmi perusahaan asal data ini.

## File
- `data/` — kumpulan data pelanggan, produk, toko, dan transaksi
- `notebook/Data Validation_Risk_Review.ipynb` — proses analisis
