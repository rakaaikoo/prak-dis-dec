# 02 2️⃣
| Nama | NIM | KELAS |
| --- | --- | --- |
| M Raka Aiko P | 235410023 | Informatika 1|

## 2.1 Task Manager
### 1. Menampilkan proses dikomputer 
Cara:
- Tekan Ctrl + Shift + Esc
- Buka Task Manager
#### Menampilkan semua proses aktif termasuk sistme dan user proses
<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/53d61fb4-5d4e-4375-8149-2394a1b0da80" />

### 2. Menjalankan aplikasi & melihat prosesnya
Cara:
- Buka aplikasi apapun, kali ini saya membuka WhatsApp
#### Setiap aplikasi bisa punya lebih dari 1 proses (tab, GPU, dll)

<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/51d5f062-fba6-40fe-ab8b-a79e0ce491df" />

### 3. Restart & Mematikan Proses
Cara:
- Klik kanan proses lalu, End Task
<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/c5244271-2c2e-40e6-a9bd-e6517acde42e" />

#### Setelah pilih End Task, Aplikasi WhatsApp akan langsung terhenti

<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/e032707f-d1dc-4b04-b1c1-96a965fadcea" />

### Penjelasan:
#### Pada praktikum ini, langkah pertama yang dilakukan adalah menampilkan seluruh proses yang sedang berjalan pada sistem operasi menggunakan Task Manager (Ctrl + Shift + Esc) pada Windows, sehingga dapat dilihat berbagai proses aktif beserta penggunaan sumber daya seperti CPU dan memori. Selanjutnya, dilakukan percobaan dengan menjalankan salah satu aplikasi seperti WhatsApp, kemudian diamati bahwa aplikasi tersebut memunculkan satu atau lebih proses baru di Task Manager, yang menunjukkan bahwa aplikasi modern umumnya menggunakan arsitektur multi-proses untuk meningkatkan kinerja dan stabilitas. Setelah itu, dilakukan pencarian dan praktik cara mematikan proses tanpa menggunakan fitur keluar (exit) aplikasi, yaitu dengan memilih proses pada Task Manager lalu menekan tombol End Task, sehingga proses dihentikan secara paksa oleh sistem operasi.
---
## 2.2 Komunikasi Antar Proses pada Sistem Terdistribusi
### 1. Membuat workspace dan menggunakan versi python
<img width="952" height="173" alt="image" src="https://github.com/user-attachments/assets/71ec6936-d107-45e6-8b7d-1592c0eb5ade" />
<img width="958" height="554" alt="image" src="https://github.com/user-attachments/assets/48d9e53d-a6a4-4b6c-b886-c8c395acee69" />

### 2. Buat environment dan mengaktifkannya
<img width="961" height="282" alt="image" src="https://github.com/user-attachments/assets/516d7a4a-fe41-48bf-8d30-8576d4c36c12" />

#### Mengecek lokasi python
<img width="868" height="95" alt="image" src="https://github.com/user-attachments/assets/ac401cf6-a899-4261-aa41-3372c7b008ff" />

### 3. Instalasi paket-paket yang diperlukan
<img width="1002" height="737" alt="image" src="https://github.com/user-attachments/assets/9de75314-734d-401a-9d9c-3788784676a7" />
<img width="711" height="696" alt="image" src="https://github.com/user-attachments/assets/046c62c6-2470-474b-a2a9-92635479f422" />

### 4. Membuat file schema GraphQL
<img width="773" height="61" alt="image" src="https://github.com/user-attachments/assets/3fc3d620-510a-4511-a728-429b421288b6" />
<img width="655" height="702" alt="image" src="https://github.com/user-attachments/assets/96a568bc-b202-4843-ba22-56e77fb9c6db" />

### 5. Inisialisasi project dan instalasi dependency
#### inisialisasi project
<img width="671" height="74" alt="image" src="https://github.com/user-attachments/assets/01589818-0539-45ca-a141-49a4a5b658f8" />

#### instalasi dependency
<img width="977" height="224" alt="image" src="https://github.com/user-attachments/assets/b8c6c5a1-2cb8-4357-be1b-a3d3edd507a5" />

#### Membuat file utama
<img width="628" height="36" alt="image" src="https://github.com/user-attachments/assets/0b19600c-e94b-46d6-9a25-9b2fbc584da8" />
<img width="501" height="260" alt="image" src="https://github.com/user-attachments/assets/07b18666-b558-4788-8daf-639d17a17eb2" />

### 6. Menjalankan GraphQl Server
<img width="755" height="124" alt="image" src="https://github.com/user-attachments/assets/2d8c2546-ac13-4600-a495-ceec837c7a78" />

#### Server  berjalan pada link yang tertera
<img width="775" height="229" alt="image" src="https://github.com/user-attachments/assets/464128df-5ec9-4f3f-b4af-242232a109ed" />
<img width="1913" height="1071" alt="image" src="https://github.com/user-attachments/assets/1efbe3ce-6214-45ad-a493-74af1724836b" />

### 7. Pengujian
<img width="1913" height="1071" alt="image" src="https://github.com/user-attachments/assets/81d15a15-4bab-4454-9d34-18d3ea5f3b4b" />

#### masukkan query:
```
{
  books {
    title
    author
  }
}
```
<img width="1912" height="1073" alt="image" src="https://github.com/user-attachments/assets/fb3610ab-8fd4-447a-85b4-5eb30f6f6989" />

---

## 3. Memuat client sederhana
### pastikan server sudah berjalan
<img width="648" height="40" alt="image" src="https://github.com/user-attachments/assets/d6881dbc-cb02-44e4-b24c-a976a13ada94" />

### Menyiapkan environment client 
<img width="714" height="171" alt="image" src="https://github.com/user-attachments/assets/cc2f8728-63ba-4ce8-9982-eabfa9fcaa62" />

### membuat file client.py
<img width="519" height="456" alt="image" src="https://github.com/user-attachments/assets/eee05de5-f7fe-4715-b826-f73749607e1b" />


### jalankan client
<img width="723" height="85" alt="image" src="https://github.com/user-attachments/assets/ee748b04-a3b9-4307-8fa5-5724ca13fffc" />

### Penjelasan:
#### Pada tugas GraphQL client, langkah pertama yang dilakukan adalah memastikan bahwa server GraphQL telah berjalan dengan baik, yaitu dengan menjalankan file schema.py menggunakan Python, kemudian mengaksesnya melalui browser pada alamat http://127.0.0.1:8000/graphql untuk memastikan server aktif dan dapat menerima query. Setelah itu, langkah berikutnya adalah menentukan bahasa pemrograman yang akan digunakan untuk membuat client, misalnya Python dengan library requests. Selanjutnya, dibuat sebuah program sederhana yang berfungsi untuk mengirim request ke server GraphQL dengan metode HTTP POST, di mana request tersebut berisi query dalam format string, seperti permintaan data buku yang mencakup title dan author. Setelah query dikirim ke server, client akan menerima response dalam bentuk JSON yang kemudian ditampilkan ke layar menggunakan perintah print. Langkah terakhir adalah melakukan pengujian program untuk memastikan bahwa client berhasil berkomunikasi dengan server dan data yang diterima sesuai dengan query yang dikirimkan. Dari proses ini dapat dipahami bahwa client berperan sebagai pihak yang meminta data, sedangkan server GraphQL bertugas memproses query dan mengembalikan hasilnya sesuai permintaan.
