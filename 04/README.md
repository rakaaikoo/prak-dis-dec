# 04 - Konsistensi dan Replikasi pada Sistem Terdistribusi 4️⃣

| Nama | NIM | KELAS |
| --- | --- | --- |
| M Raka Aiko P | 235410023 | Informatika 1|

## 4.1 - Streaming Replication Menggunakan PostgreSQL
#### Langkah 1: Buat folder & file
<img width="890" height="331" alt="image" src="https://github.com/user-attachments/assets/ced0dc40-15ca-436a-98ed-461e09f9a367" />

#### Langkah 2:Buat file 00_init.sql
```sql
CREATE USER replicator WITH REPLICATION ENCRYPTED PASSWORD 'replicator_password';
SELECT pg_create_physical_replication_slot('replication_slot');
```
#### Langkah 3: Buat file docker-compose.yaml
```yaml
x-postgres-common: &postgres-common
  image: postgres:18.3-alpine3.23
  user: postgres
  restart: always
  healthcheck:
    test: 'pg_isready -U zuser --dbname=zdb'
    interval: 10s
    timeout: 5s
    retries: 5

services:
  postgres_primary:
    <<: *postgres-common
    ports:
      - 5432:5432
    environment:
      POSTGRES_USER: zuser
      POSTGRES_DB: zdb
      POSTGRES_PASSWORD: zpass
      POSTGRES_HOST_AUTH_METHOD: "scram-sha-256\nhost replication replicator 0.0.0.0/0 md5"
      POSTGRES_INITDB_ARGS: "--auth-host=scram-sha-256"
    command: |
      postgres
      -c wal_level=replica
      -c hot_standby=on
      -c max_wal_senders=10
      -c max_replication_slots=10
      -c hot_standby_feedback=on
    volumes:
      - ./00_init.sql:/docker-entrypoint-initdb.d/00_init.sql

  postgres_replica:
    <<: *postgres-common
    ports:
      - 5433:5432
    environment:
      PGUSER: replicator
      PGPASSWORD: replicator_password
      PGDATA: /var/lib/postgresql/18/docker
    command: |
      bash -c "
        until pg_basebackup --pgdata=/var/lib/postgresql/18/docker -R --slot=replication_slot --host=postgres_primary --port=5432 -X stream; do
          echo 'pg_basebackup failed. Retrying in 5 seconds ...'
          sleep 5
        done
        echo 'Backup done, starting replica...'
        chmod 0700 /var/lib/postgresql/18/docker
        postgres
      "
    depends_on:
      - postgres_primary
```

#### Langkah 4: Jalankan
<img width="1455" height="104" alt="image" src="https://github.com/user-attachments/assets/a6d46e38-2666-43ac-90bf-8ab354bc1c14" />

#### Langkah 5: Cek status
<img width="1871" height="197" alt="image" src="https://github.com/user-attachments/assets/3d49f9a2-0035-421e-ab1e-2d913d609737" />

#### Langkah 6: Testing (sama seperti modul)
<img width="664" height="599" alt="image" src="https://github.com/user-attachments/assets/129f4837-a5b6-487d-9a6a-2db106972801" />
<img width="512" height="567" alt="image" src="https://github.com/user-attachments/assets/c6382375-adad-4b12-9847-19ddfd0434a7" />
<img width="456" height="96" alt="image" src="https://github.com/user-attachments/assets/c39fd098-8aa6-40ee-85a8-8e58bf3a5412" />

#### Langkah 7: Buat tabel
<img width="1491" height="412" alt="image" src="https://github.com/user-attachments/assets/af7ec1e4-30ce-4416-b537-a725fd9de77d" />

###  High-Availability
<img width="1892" height="76" alt="image" src="https://github.com/user-attachments/assets/f9e8f529-3da5-417a-a020-3894a95012dc" />
<img width="1528" height="380" alt="image" src="https://github.com/user-attachments/assets/6099514b-93f4-4e93-9bc3-2164591e4428" />

### Matikan semua
<img width="1907" height="162" alt="image" src="https://github.com/user-attachments/assets/575fcaed-c704-4d2a-a5cb-5bbaad389e19" />

---

## 4.2 Replikasi Master-Master Menggunakan Apache Ignite
#### Langkah 1: Buat folder
<img width="791" height="382" alt="image" src="https://github.com/user-attachments/assets/f14e76cb-8699-4339-bed4-191f4fc7a328" />

#### Langkah 2: Download file resmi
<img width="310" height="167" alt="image" src="https://github.com/user-attachments/assets/571a757f-dc39-411c-b33f-cb2af821a651" />

#### Langkah 3: Jalankan cluster
<img width="1915" height="393" alt="image" src="https://github.com/user-attachments/assets/82a15aa7-18a5-46d2-8eec-40d2756f1d23" />

#### Langkah 4: Jalankan Apache Ignite CLI (adaptasi Windows)
<img width="1911" height="655" alt="image" src="https://github.com/user-attachments/assets/24e71efd-4334-44f6-b73f-8523bdc41964" />

#### Langkah 5: Inisialisasi cluster (sekali saja)
<img width="963" height="97" alt="image" src="https://github.com/user-attachments/assets/8a612592-df97-4669-914f-331480b094ca" />

#### Langkah 6: Eksekusi SQL files
<img width="672" height="504" alt="image" src="https://github.com/user-attachments/assets/d20b193a-14f9-46e3-9259-5cb1a2016477" />
<img width="745" height="807" alt="image" src="https://github.com/user-attachments/assets/9dbdc4ae-7da3-44e5-9425-f4fcce1e4ba6" />

#### Langkah 7: Cek replikasi Master-Master
<img width="1656" height="400" alt="image" src="https://github.com/user-attachments/assets/d3a0d609-fbcc-4c33-b3e1-e7d41e9be7df" />

### Terakhir jangan lupa matikan
<img width="1907" height="186" alt="image" src="https://github.com/user-attachments/assets/96e0d80e-6046-4a42-ad28-572bd807f038" />

---
## Penjelasan:
#### Pada modul ini dilakukan implementasi konsep replikasi data pada sistem terdistribusi menggunakan dua pendekatan, yaitu Streaming Replication pada PostgreSQL dan Master-Master Replication menggunakan Apache Ignite. Praktikum dilakukan pada sistem operasi Windows dengan bantuan Docker Desktop sebagai media virtualisasi container.
#### Pada bagian pertama, dilakukan konfigurasi Streaming Replication PostgreSQL, yang menerapkan arsitektur Primary-Replica. Server primary bertugas menangani seluruh operasi baca dan tulis (read-write), sedangkan server replica hanya berfungsi sebagai standby yang menerima salinan data secara real-time dari primary. Proses ini memanfaatkan mekanisme Write-Ahead Logging (WAL) yang dikirimkan dari primary ke replica. Konfigurasi dilakukan melalui file docker-compose.yaml dan 00_init.sql, di mana file SQL digunakan untuk membuat user replikasi serta slot replikasi. Pada lingkungan Windows, terdapat beberapa penyesuaian seperti penggunaan perintah docker compose (tanpa tanda hubung) serta penghilangan penggunaan file env.sh yang hanya relevan pada sistem Linux.
#### Setelah konfigurasi selesai, container dijalankan menggunakan Docker Desktop. Proses replikasi diuji dengan membuat tabel dan memasukkan data pada server primary, kemudian dilakukan pengecekan pada server replica. Hasil menunjukkan bahwa data berhasil direplikasi secara otomatis, yang menandakan bahwa sistem berjalan dengan baik. Selain itu, dilakukan pula pengujian status replica menggunakan perintah pg_is_in_recovery() yang menghasilkan nilai true, menandakan bahwa server berada dalam mode standby. Dalam skenario kegagalan, replica dapat dipromosikan menjadi primary menggunakan perintah pg_promote(), sehingga mendukung konsep High Availability (HA).
#### Pada bagian kedua, dilakukan implementasi Master-Master Replication menggunakan Apache Ignite. Berbeda dengan PostgreSQL, arsitektur ini memungkinkan setiap node dalam cluster berperan sebagai primary, sehingga semua node dapat melakukan operasi baca dan tulis. Konfigurasi dilakukan menggunakan Docker Compose untuk menjalankan beberapa node sekaligus dalam satu cluster. Setelah cluster diinisialisasi, dilakukan eksekusi perintah SQL untuk membuat dan mengisi data. Pengujian dilakukan dengan mengakses node yang berbeda melalui port yang telah ditentukan, dan hasilnya menunjukkan bahwa data yang dimasukkan pada satu node secara otomatis tersedia pada node lainnya. Hal ini membuktikan bahwa replikasi berjalan secara sinkron antar node.
#### Secara keseluruhan, penggunaan Docker Desktop pada Windows mempermudah proses implementasi tanpa perlu instalasi manual database dan konfigurasi jaringan yang kompleks. Meskipun terdapat beberapa perbedaan perintah dibandingkan Linux, seperti tidak tersedianya perintah touch, seluruh proses tetap dapat dijalankan dengan baik setelah dilakukan penyesuaian.

## Kesimpulan:
#### Berdasarkan praktikum yang telah dilakukan, dapat disimpulkan bahwa replikasi data merupakan komponen penting dalam sistem terdistribusi untuk menjaga konsistensi, ketersediaan, dan keandalan data. Pada PostgreSQL, metode Streaming Replication dengan arsitektur Primary-Replica memungkinkan pemisahan beban kerja antara server utama dan server cadangan, serta mendukung mekanisme failover untuk meningkatkan High Availability. Sementara itu, Apache Ignite menggunakan pendekatan Master-Master yang memberikan fleksibilitas lebih tinggi karena setiap node dapat melakukan operasi baca dan tulis secara bersamaan. Implementasi pada Windows menggunakan Docker Desktop terbukti efektif dan efisien, meskipun memerlukan beberapa penyesuaian dari panduan berbasis Linux. Dengan demikian, praktikum ini memberikan pemahaman yang baik mengenai berbagai strategi replikasi dalam sistem terdistribusi serta penerapannya dalam lingkungan nyata.
