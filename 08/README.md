# 08 - Arsitektur Microservices untuk Sistem Terdistribusi 8️⃣

| Nama | NIM | KELAS |
| --- | --- | --- |
| M Raka Aiko P | 235410023 | Informatika 1|
---
## 1. Membuat project 
<img width="722" height="611" alt="image" src="https://github.com/user-attachments/assets/56e500d3-22a4-49ab-8553-5d01a4bc07f4" />

## 2. Membuat Database SQLite
<img width="557" height="583" alt="image" src="https://github.com/user-attachments/assets/ce6d1729-32e6-4595-8300-7752eb681a1c" />
<img width="528" height="52" alt="image" src="https://github.com/user-attachments/assets/b5a2d374-030a-4240-ae27-24cc9045ab4d" />

## 3. Membuat REST API
<img width="518" height="455" alt="image" src="https://github.com/user-attachments/assets/e51a76fd-90f5-4e87-a5a3-2b6d5148e9c5" />

## 4.Menjalankan API
<img width="721" height="177" alt="image" src="https://github.com/user-attachments/assets/61ffdadb-0298-4f9d-b0ab-143e37bd34c0" />

## 5. Mengakses dari API dari browser
<img width="1049" height="238" alt="image" src="https://github.com/user-attachments/assets/d6724f43-6858-4444-aa00-8fdddc21a192" />

## 6. Menampilkan hasil dengan CURL
<img width="1119" height="105" alt="image" src="https://github.com/user-attachments/assets/2ba9e4d2-ffad-4090-99c0-e3bb15bca24e" />

---
### Penjelasan: 
#### Pada praktikum Modul 8 ini dilakukan implementasi arsitektur microservices sederhana menggunakan FastAPI, SQLModel, dan SQLite pada sistem operasi Windows. Langkah pertama yang dilakukan adalah membuat lingkungan pengembangan menggunakan uv serta menginstal pustaka yang dibutuhkan, yaitu FastAPI sebagai framework REST API, SQLModel sebagai ORM, dan Uvicorn sebagai ASGI server. Selanjutnya dibuat database SQLite bernama produk.db yang berisi tabel produk dengan atribut id (INT dan primary key), nama (CHAR), kategori (VARCHAR), stok (INT), tersedia (BOOLEAN), dan harga (FLOAT). Setelah struktur tabel dibuat, dilakukan pengisian lima data produk menggunakan script Python. Tahap berikutnya adalah membuat RESTful API endpoint /produk/ pada file main.py untuk mengambil seluruh data yang tersimpan di database dan menampilkannya dalam format JSON. API kemudian dijalankan menggunakan perintah uvicorn main:app --reload dan diuji melalui browser maupun perintah curl. Meskipun sempat ditemukan kendala saat mengakses endpoint menggunakan curl, permasalahan tersebut terjadi karena server FastAPI belum berjalan sehingga tidak ada layanan yang menerima koneksi pada port 8000. Setelah server aktif, endpoint dapat diakses dan menampilkan seluruh data produk yang tersimpan pada database.

### Kesimpulan:
#### Berdasarkan praktikum yang telah dilakukan, dapat disimpulkan bahwa FastAPI dan SQLModel dapat digunakan untuk membangun layanan microservices sederhana yang terhubung dengan database SQLite. Praktikum ini berhasil menunjukkan proses pembuatan database, pengisian data menggunakan Python, pembuatan RESTful API untuk menampilkan data, serta pengujian endpoint menggunakan browser dan curl. Selain itu, praktikum memberikan pemahaman mengenai integrasi antara database, ORM, dan web service dalam lingkungan sistem terdistribusi. Dengan demikian, tujuan praktikum untuk membangun dan menjalankan layanan REST API berbasis microservices telah berhasil tercapai.
