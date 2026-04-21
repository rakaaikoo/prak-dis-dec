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
