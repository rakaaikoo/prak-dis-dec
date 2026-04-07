# 03 - Sinkronisasi pada Sistem Terdistribusi

## 3.1 Sinkronasi Waktu
#### Menggunakan Network Time Synchronize 
<img width="511" height="368" alt="image" src="https://github.com/user-attachments/assets/d91aee25-90e6-4fc3-850f-2db53ee25335" />

#### Penjelasan:
#### Komputer (lab informatika 2) melakukan request ke server NTP (misalnya 0.nettime.pool.ntp.org)
- Server mengirimkan waktu saat ini
- Sistem menghitung:
  - Offset → selisih waktu lokal dengan server (+33 ms)
  - Lag (delay) → waktu tempuh komunikasi (26 ms)
- Jika selisih kecil → waktu langsung disesuaikan
- Jika selisih besar → dilakukan penyesuaian bertahap (tidak langsung loncat)

Alur proses:
1. Client kirim permintaan waktu ke NTP server
2. Server membalas dengan timestamp
3. Client menghitung delay & offset
4. Waktu lokal dikoreksi
5. Sinkronisasi dilakukan berkala (misalnya setiap beberapa jam)
