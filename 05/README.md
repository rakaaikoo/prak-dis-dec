# 05 - Fault Tolerance 5️⃣

| Nama | NIM | KELAS |
| --- | --- | --- |
| M Raka Aiko P | 235410023 | Informatika 1|
---
## 4.1 Load Balancing Aplikasi
### 1. Persiapan
### Install uv 
<img width="941" height="681" alt="image" src="https://github.com/user-attachments/assets/e81515cd-c3c0-4463-8466-b8621850d771" />

### Buat folder kerja
<img width="881" height="298" alt="image" src="https://github.com/user-attachments/assets/9c9d3b34-d6cd-4c2c-bb82-60853892f3a1" />

<img width="922" height="777" alt="image" src="https://github.com/user-attachments/assets/f3bc6f0d-01e3-4f45-bc39-8c91abc176a2" />

### install blacksheep
<img width="925" height="942" alt="image" src="https://github.com/user-attachments/assets/19f6b5d2-4325-400a-aa27-575afcb59c93" />

### 2. Membuat Virtual Environment & Aplikasi Blacksheep
<img width="849" height="343" alt="image" src="https://github.com/user-attachments/assets/b778e8a6-56c0-4f9d-a1a3-27c1d1f1cbbf" />

### Masuk ke dalam folder project dan install requirements
<img width="934" height="613" alt="image" src="https://github.com/user-attachments/assets/2d181487-eaf3-430d-be18-d76f35274a92" />

### test aplikasi lokal
<img width="1915" height="1077" alt="image" src="https://github.com/user-attachments/assets/bbbbc1e0-2985-4bbe-a2ed-590e91b8ee9f" />

### Siapkan Struktur Folder & File Docker
```text
workspace-05/
├── blacksheep_lb/          ← sudah ada
├── nginx/
│   ├── Dockerfile
│   └── nginx.conf
├── docker-compose.yml
```

`Dockerfile`
```dockerfile
FROM nginx

# Override the default nginx configuration file
RUN rm /etc/nginx/conf.d/default.conf
COPY nginx.conf /etc/nginx/nginx.conf
```

`nginx.conf`
```nginx
events {
    worker_connections 4096;
}

http {
    # Definisi grup upstream (nama service di docker-compose.yml)
    upstream backend {
        server bs_app:80;
    }

    server {
        listen 80;

        location / {
            # sesuaikan dengan nama upstream di atas
            proxy_pass http://backend;
        }
    }
}
```

`docker-compose.yml`
```YAML
services:
  # aplikasi yang akan di-scale
  bs_app:
    build: ./blacksheep-lb

  # nginx load balancer
  nginx:
    container_name: nginx
    build: ./nginx
    ports:
      - "80:80"
    depends_on:
      - bs_app
```

`Dockerfile`
```dockerfile
# Build the Server
FROM python:3.14.4-slim AS server_builder

WORKDIR /home

RUN echo "APT::Get::Assume-Yes \"true\";" > /etc/apt/apt.conf.d/90assumeyes
RUN apt-get update && apt-get install make apt-utils lsb-release software-properties-common apt-transport-https ca-certificates gnupg sqlite3 build-essential libssl-dev zlib1g-dev libbz2-dev libsqlite3-dev unixodbc-dev libncurses5-dev libgdk3-dev libnss3-dev libreadline-dev libffi-dev libjpeg-dev zlib1g-dev wget

COPY . /home

RUN python -m venv venv && . venv/bin/activate && pip install --upgrade pip && pip install -r requirements.txt

EXPOSE 80

FROM python:3.14.4-slim

WORKDIR /home

COPY --from=server_builder /home/ /home/

ENV APP_ENV=prod BG_COLOR="#1abc9c" APP_ROUTE_PREFIX=""

RUN echo "APT::Get::Assume-Yes \"true\";" > /etc/apt/apt.conf.d/90assumeyes
RUN apt-get update && apt-get install ca-certificates sqlite3 libsqlite3-dev libjpeg-dev zlib1g-dev

CMD ["sh", "-c", ". venv/bin/activate && uvicorn \"app.main:app\" --host 0.0.0.0 --port 80 --log-level info"]
```

### jalankan docker compose
<img width="924" height="993" alt="image" src="https://github.com/user-attachments/assets/e43fd9e5-bc3c-45f2-b723-3ba4971687f2" />

### Cek container yang berjalan
<img width="1659" height="133" alt="image" src="https://github.com/user-attachments/assets/08e50dcb-327a-43e5-996c-ac83f842cebb" />

### Test Load Balancing
<img width="1915" height="1077" alt="image" src="https://github.com/user-attachments/assets/603e3895-d11c-4ecc-ab48-fa65bc185efd" />

### Cek log
<img width="1913" height="793" alt="image" src="https://github.com/user-attachments/assets/390fb9b9-134d-4d63-a3bd-004da33dc931" />

### Stop semua container
<img width="1915" height="167" alt="image" src="https://github.com/user-attachments/assets/74d231ff-70d6-4651-bcd3-4097f59a15ca" />

---
## 4.2 Failure Detection (Heartbeat, Retry, Circuit Breaker)
### 1. Heartbeat
<img width="925" height="102" alt="image" src="https://github.com/user-attachments/assets/0fee8bc5-29ce-42d0-b1fd-83c595505f80" />

#### di beda terminal
<img width="948" height="292" alt="image" src="https://github.com/user-attachments/assets/cada8872-eb33-498e-b823-d4a56c3c2033" />
<img width="931" height="1025" alt="image" src="https://github.com/user-attachments/assets/5802848c-ddbf-436c-9922-42ee288511a5" />

### 2. Retry dengan Tenacity – check-retry.py
#### install library
<img width="956" height="123" alt="image" src="https://github.com/user-attachments/assets/34330e55-58ef-46cd-93ef-1aa1fadf8875" />

#### menjalankannya
<img width="948" height="107" alt="image" src="https://github.com/user-attachments/assets/3ff8d6ec-4a87-4169-b7ad-ae9c3278520f" />

#### beda terminal
<img width="948" height="100" alt="image" src="https://github.com/user-attachments/assets/a5534db0-254b-4bd9-bd33-2860249fc312" />

### 3. Circuit Breaker – check-circuit-breaker.py
#### install library
<img width="949" height="126" alt="image" src="https://github.com/user-attachments/assets/faa4561f-141e-42bc-b546-a7531d4261e2" />

#### menjalankannya
<img width="952" height="166" alt="image" src="https://github.com/user-attachments/assets/b535f194-75be-451f-ba01-3044d6526f64" />

#### beda terminal
<img width="948" height="99" alt="image" src="https://github.com/user-attachments/assets/30e3cf25-b891-4761-a7b7-20e818da9470" />

---

## 📖 Penjelasan:
#### Modul 5 membahas konsep Fault Tolerance dalam sistem terdistribusi, yaitu kemampuan sistem untuk tetap beroperasi meskipun terjadi kegagalan pada salah satu komponennya. Pada bagian 4.1 Load Balancing Aplikasi, dijelaskan proses pembuatan aplikasi web berbasis Python menggunakan framework Blacksheep, kemudian aplikasi tersebut dikemas menggunakan Docker agar dapat dijalankan dalam container. Selanjutnya digunakan Nginx sebagai load balancer untuk mendistribusikan request ke lebih dari satu instance aplikasi sehingga tercapai high availability dan performa yang lebih stabil. Pengelolaan container dilakukan menggunakan docker-compose.yml yang memudahkan proses scaling, misalnya menjalankan dua instance bs_app secara bersamaan. Pada bagian 4.2 Failure Detection, modul menjelaskan beberapa teknik untuk mendeteksi kegagalan sistem, yaitu heartbeat untuk memeriksa apakah service masih aktif, retry menggunakan library Tenacity untuk mencoba kembali koneksi yang gagal, serta circuit breaker untuk mencegah kegagalan berantai dengan memutus sementara akses ke service yang sedang bermasalah. Ketiga teknik ini sangat penting dalam menjaga keandalan aplikasi terdistribusi

## 🎯 Kesimpulan:
#### Kesimpulannya, modul ini menunjukkan bahwa penerapan fault tolerance sangat penting dalam pengembangan sistem terdistribusi modern. Dengan menggunakan load balancing, aplikasi dapat menangani banyak request secara lebih efisien dan tetap tersedia walaupun salah satu instance mengalami masalah. Sementara itu, mekanisme failure detection seperti heartbeat, retry, dan circuit breaker membantu sistem mengenali gangguan lebih cepat serta mengurangi dampak kegagalan terhadap keseluruhan layanan. Melalui praktik ini, dapat dipahami bahwa kombinasi antara Docker, Nginx, dan strategi deteksi kegagalan merupakan solusi yang efektif untuk membangun sistem yang andal, scalable, dan tahan terhadap error
