# 12 - Teknologi P2P (Peer-to-Peer) 1️⃣2️⃣

| Nama | NIM | KELAS |
| --- | --- | --- |
| M Raka Aiko P | 235410023 | Informatika 1|
---

## 1. Koneksi Antar Nodes
### A. Source code
<img width="1680" height="3292" alt="image" src="https://github.com/user-attachments/assets/6eb00309-c943-4f7c-b905-9792157e5672" />

### B. Menjalankan program (Tugas 1)
<img width="734" height="411" alt="image" src="https://github.com/user-attachments/assets/6ee0bad4-ef5e-41bc-b5fb-87bdd9856340" />
<img width="731" height="720" alt="image" src="https://github.com/user-attachments/assets/84a4b1f0-b787-40dd-b7e6-99537d3a01f1" />

### Jawaban Tugas 1.2
#### a. Membuka port yang akan menerima dan mengirim pesan
#### Bagian berikut digunakan untuk membuka port server:
``` python
server_socket = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
server_socket.bind(('0.0.0.0', port_saya))
server_socket.listen(1)
```

Penjelasan:
- socket() membuat socket TCP.
- bind() menghubungkan socket ke port tertentu.
- listen() membuat socket siap menerima koneksi.

#### B. Menerima pesan
```python
data = koneksi.recv(1024)
```
#### Penjelasan:
#### Fungsi `recv()` menerima data maksimum 1024 byte dari peer yang terhubung. Setelah diterima, data ditampilkan ke layar menggunakan:
``` python
print(f"\n[Peer]: {data.decode('utf-8')}")
```

Penjelasan:
- socket() membuat socket TCP.
- bind() menghubungkan socket ke port tertentu.
- listen() membuat socket siap menerima koneksi.

#### c. Mengirim pesan
``` python
client_socket.sendall(
    pesan.encode('utf-8')
)
```
#### Penjelasan:
#### Pesan yang diketik pengguna diubah menjadi byte menggunakan encode() kemudian dikirim ke node lain menggunakan sendall().
---

## 2. DHT
### A. Source code
<img width="1662" height="4508" alt="image" src="https://github.com/user-attachments/assets/c130f4bb-306a-40b3-bea5-a5e7de0100a2" />

### B. Menjalankan program (Tugas 1)
<img width="730" height="742" alt="image" src="https://github.com/user-attachments/assets/b2e0de3c-4d7a-4fb9-b780-795757643426" />

### Jawaban Tugas 2.2
#### Program ini mensimulasikan cara kerja Distributed Hash Table (DHT) pada jaringan P2P. Setiap node memiliki ID yang diperoleh dari proses hashing. Ketika suatu file disimpan, nama file akan di-hash menjadi key tertentu. Sistem kemudian mencari node yang ID-nya paling dekat dengan key tersebut dan menyimpan data pada node tersebut. Saat pencarian dilakukan, key yang sama dihitung kembali dan sistem langsung mengarahkan pencarian ke node yang bertanggung jawab menyimpan data tersebut.

### Jawaban Tugas 2.3
#### Algoritma Simpan Data:
```
1. Input nama file
2. Hitung hash file menjadi key
3. Cari node dengan ID terdekat
4. Simpan file pada node tersebut
5. Tampilkan lokasi penyimpanan
```
#### Algoritma cari data:
```
1. Input nama file
2. Hitung hash file menjadi key
3. Cari node dengan ID terdekat
4. Periksa apakah key tersedia
5. Jika ada → tampilkan data
6. Jika tidak ada → tampilkan gagal
```
---

## 3. Torrent
### A. Source code
<img width="1818" height="3102" alt="image" src="https://github.com/user-attachments/assets/47951394-2fec-4fc9-a027-68fbbf315149" />

### B. Menjalankan program (Tugas 1)
<img width="733" height="80" alt="image" src="https://github.com/user-attachments/assets/26d8ed5b-8849-48db-9a8b-e4e9d6166b38" />

### Jawaban Tugas 3.2
#### Output tersebut sebenarnya bukan error. Program Anda berjalan dengan benar, tetapi program versi yang sudah dimodifikasi memang mengharuskan nama file .torrent diberikan sebagai parameter.

#### Saat menjalankan:

`python read_torrent.py`

#### program menampilkan:

#### Penggunaan: `python read_torrent.py <namafile.torrent>`

#### karena bagian ini:
``` python
if len(sys.argv) != 2:
    print("Penggunaan:")
    print("python read_torrent.py namafile.torrent")
    sys.exit()
```
#### mengecek apakah ada argumen file yang diberikan.

### Jawaban Tugas 3.3

