# 06 - Distributed File System - HDFS 6️⃣

| Nama | NIM | KELAS |
| --- | --- | --- |
| M Raka Aiko P | 235410023 | Informatika 1|

---
### Menginstall JDK 
<img width="932" height="124" alt="image" src="https://github.com/user-attachments/assets/539f4286-6469-417f-af2c-7ba111a3ed65" />

## 1. Install hadoop
<img width="747" height="121" alt="image" src="https://github.com/user-attachments/assets/e7b8fa0a-ca68-423b-97e8-56e60d9c3133" />

---
## 2. Set Environment Variable
<img width="458" height="25" alt="image" src="https://github.com/user-attachments/assets/a273c33f-7e8e-45fa-b211-c6a04ee5e41d" />
<img width="659" height="89" alt="image" src="https://github.com/user-attachments/assets/eb77e3d0-9898-4626-9921-d05caf753fe1" />
<img width="459" height="27" alt="image" src="https://github.com/user-attachments/assets/6f26c649-bf2b-47fc-b243-00b0240cdadf" />

---
## 3. Konfigurasi SSH
<img width="945" height="667" alt="image" src="https://github.com/user-attachments/assets/a1c9f136-cfdd-4671-bf78-ffec011a38eb" />

### test
<img width="945" height="482" alt="image" src="https://github.com/user-attachments/assets/1e78f818-17a5-483f-85fd-fb6bc239897b" />

---
## 4. Konfigurasi Hadoop
### hdfs-site.xml
<img width="909" height="669" alt="image" src="https://github.com/user-attachments/assets/b8729c6a-c025-426e-aeef-8dbb856b41cf" />

### core-site.xml
<img width="867" height="609" alt="image" src="https://github.com/user-attachments/assets/eedee225-5ad8-42bc-b048-349794a10ba8" />

### mapred-site.xml
<img width="837" height="609" alt="image" src="https://github.com/user-attachments/assets/3c226007-aa9a-466f-82e7-6eb3eccfe364" />

### yarn-site.xml
<img width="863" height="575" alt="image" src="https://github.com/user-attachments/assets/e9d93262-0eb3-4ce1-a3e9-3cb38d62e92c" />

---
## 5. Set JAVA_HOME di Hadoop
<img width="921" height="24" alt="image" src="https://github.com/user-attachments/assets/ab5b60bb-8d06-492c-82f0-c0a95c9a470b" />
<img width="770" height="82" alt="image" src="https://github.com/user-attachments/assets/108da308-4579-46ea-aa7c-d097ff1b5e0a" />

---
## 6. Format NameNode
#### jalankan perintah:
```bash
hdfs namenode -format
```
<img width="947" height="504" alt="image" src="https://github.com/user-attachments/assets/06230505-0e34-4726-96b5-a09c4e914c67" />

---
## 7. Jalankan Hadoop
<img width="736" height="171" alt="image" src="https://github.com/user-attachments/assets/f4f20c88-e5ca-4837-99a6-72ce61ea01bb" />

---
## 8. Cek di Browser
#### mengecek dengan membuka `http://localhost:9870`
<img width="1362" height="762" alt="image" src="https://github.com/user-attachments/assets/4af8271a-1132-4ed2-a4c3-1fc4c8184ee1" />

---
# TUGAS 📖
## 1. Buat direktori
<img width="936" height="150" alt="image" src="https://github.com/user-attachments/assets/1ed8cd7c-ea48-466a-a339-6d6b9be274d3" />

## 2. Cari 3 file .csv di Internet dan kemudian copykan 3 file tersebut ke direktori yang baru
saja anda buat pada tugas 1 di atas
<img width="945" height="941" alt="image" src="https://github.com/user-attachments/assets/c0545f9c-70b8-4b94-9dea-15a3bad9d2aa" />
<img width="927" height="48" alt="image" src="https://github.com/user-attachments/assets/fb910c45-5806-467f-94f0-51d1676c4527" />
<img width="952" height="101" alt="image" src="https://github.com/user-attachments/assets/3c5cb3e7-b99d-4bf2-9c5a-18039b382a2a" />

---
### Mematikan HDFS
<img width="703" height="174" alt="image" src="https://github.com/user-attachments/assets/8d7042b4-4628-429d-ad20-d97033dcbb85" />

---
## Penjelasan:
#### Pengerjaan Modul 6 tentang Distributed File System (HDFS) di Windows dilakukan menggunakan WSL2 (Windows Subsystem for Linux 2) karena Apache Hadoop tidak dapat berjalan secara native di Windows tanpa konfigurasi yang sangat rumit. Melalui WSL2, pengguna mendapatkan lingkungan Linux (Ubuntu) yang berjalan langsung di dalam Windows, sehingga semua langkah di modul dapat diikuti hampir identik, mulai dari instalasi JDK 17, pdsh, konfigurasi SSH passwordless, ekstraksi Hadoop 3.5.0, pengaturan file konfigurasi XML seperti hdfs-site.xml, core-site.xml, mapred-site.xml, dan yarn-site.xml, hingga proses format NameNode dan menjalankan daemon HDFS dengan start-dfs.sh. Setelah HDFS aktif, pengguna dapat memantau status cluster melalui Web UI di http://localhost:9870 langsung dari browser Windows, lalu mengerjakan tugas yaitu membuat direktori /user/rakaaiko/datasets menggunakan perintah hdfs dfs -mkdir -p dan mengunggah 3 file CSV ke direktori tersebut menggunakan hdfs dfs -put.

## Kesimpulan:
#### WSL2 adalah solusi terbaik untuk menjalankan Apache Hadoop di Windows karena menyediakan lingkungan Linux yang sesungguhnya tanpa perlu dual-boot. Kunci keberhasilan pengerjaan modul ini adalah memastikan HDFS sudah berjalan (dicek dengan jps) dan direktori HDFS sudah dibuat terlebih dahulu sebelum melakukan operasi upload file, karena HDFS tidak akan otomatis membuat direktori tujuan seperti halnya sistem file biasa.
