# 🐳 Laporan Praktikum Pertemuan 02
## Docker Fundamentals

---

## 👤 Identitas Mahasiswa

| Item | Keterangan |
|------|------------|
| **Nama** | Wafiq Azizah |
| **NIM** | 105841120923 |
| **Kelas** | 5B |
| **Tanggal** | 2026-02-25 |

---

## 📚 Pemahaman Docker

### Apa itu Docker?

Menurut saya, Docker adalah platform yang digunakan untuk menjalankan aplikasi di dalam sebuah lingkungan terisolasi yang disebut container. Docker membantu developer agar aplikasi bisa berjalan dengan cara yang sama di berbagai komputer tanpa masalah perbedaan sistem atau konfigurasi.

Dengan Docker, aplikasi dan semua dependensinya (library, konfigurasi, dll.) dikemas menjadi satu sehingga mudah dipindahkan dan dijalankan di mana saja.

🔹 Konsep Container, Image, dan Perbedaannya dengan VM
✅ Container

Container adalah lingkungan terisolasi yang digunakan untuk menjalankan aplikasi. Container berbagi kernel dengan sistem operasi host, tetapi tetap terpisah satu sama lain. Karena tidak membawa sistem operasi lengkap, container lebih ringan dan cepat dijalankan.

✅ Image

Image adalah template atau blueprint untuk membuat container. Image berisi aplikasi, library, dan konfigurasi yang dibutuhkan untuk menjalankan aplikasi tersebut. Dari satu image, kita bisa membuat banyak container.

Contohnya saat praktikum, kita menggunakan image seperti:

Nginx

Apache HTTP Server

PostgreSQL

Image tersebut kemudian dijalankan menjadi container.

### Komponen Utama Docker

1️⃣ Docker Images
Docker Images adalah file template yang berisi aplikasi dan semua dependensinya. Image bersifat read-only dan digunakan untuk membuat container. Image dapat dibuat sendiri menggunakan Dockerfile atau diambil dari Docker Hub.

2️⃣ Docker Containers
Docker Containers adalah hasil dari menjalankan image. Container bersifat aktif dan dapat dijalankan, dihentikan, atau dihapus. Container memiliki sistem file sendiri, tetapi tetap ringan karena tidak membawa sistem operasi penuh.

3️⃣ Docker Registry
Docker Registry adalah tempat penyimpanan image Docker. Contohnya adalah Docker Hub. Dari registry, kita bisa melakukan pull (mengambil image) atau push (mengirim image).

### Perbedaan Docker vs Virtual Machine

🖥 Virtual Machine (VM)
Virtual Machine menjalankan sistem operasi lengkap di atas hypervisor. Setiap VM memiliki OS sendiri, kernel sendiri, dan membutuhkan resource yang cukup besar (RAM dan storage).
Contoh teknologi VM:
VirtualBox

🐳 Docker Container
Docker container tidak menjalankan sistem operasi lengkap. Container berbagi kernel dengan host OS sehingga lebih ringan dan cepat dijalankan. Startup container hanya membutuhkan beberapa detik, sedangkan VM bisa membutuhkan menit.

---

## 🔧 Praktik Docker Commands

### Output docker ps -a

```
CONTAINER ID   IMAGE          COMMAND                  CREATED              STATUS              PORTS                                     NAMES
7350ff51c743   nginx:alpine   "/docker-entrypoint.…"   15 seconds ago       Up 15 seconds       0.0.0.0:8080->80/tcp, [::]:8080->80/tcp   web-praktikum

```

### Output docker images

```
praktikum-docker:v1                 60423f2905d3       92.5MB           26MB

```

### Docker Run Command

```bash
$ docker run -d -p 8080:80 --name praktikum-web praktikum-docker:v1

```

---

## 📄 Dockerfile

### Isi Dockerfile

```dockerfile
# Gunakan nginx alpine sebagai base image
FROM nginx:alpine

# Copy file HTML ke direktori nginx
COPY app/index.html /usr/share/nginx/html/index.html

# Expose port 80
EXPOSE 80

# Command default nginx
CMD ["nginx", "-g", "daemon off;"]
```

### Penjelasan Dockerfile

1️⃣ FROM nginx:alpine
Menggunakan image dasar Nginx versi ringan (Alpine) sebagai base untuk membuat image baru.

2️⃣ COPY app/index.html /usr/share/nginx/html/index.html
Menyalin file index.html dari folder proyek ke direktori default nginx di dalam container.

3️⃣ EXPOSE 80
Menentukan bahwa aplikasi berjalan di port 80.

4️⃣ CMD ["nginx", "-g", "daemon off;"]
Menjalankan nginx saat container dijalankan dan memastikan proses tetap aktif.

---

## 🐙 Docker Compose

### Isi docker-compose.yml

```yaml
version: '3.8'

services:
  web:
    image: nginx:alpine
    ports:
      - "8080:80"
    volumes:
      - ./app:/usr/share/nginx/html:ro
    depends_on:
      - api
    networks:
      - praktikum-net

  api:
    image: httpd:alpine
    ports:
      - "8081:80"
    networks:
      - praktikum-net

  db:
    image: postgres:15-alpine
    environment:
      POSTGRES_USER: praktikum
      POSTGRES_PASSWORD: devops123
      POSTGRES_DB: praktikum_db
    volumes:
      - db_data:/var/lib/postgresql/data
    networks:
      - praktikum-net

networks:
  praktikum-net:
    driver: bridge

volumes:
  db_data:
```

### Penjelasan Docker Compose

version: '3.8' Menunjukkan versi format konfigurasi Docker Compose yang digunakan dalam file ini.

services: Bagian ini berisi daftar container (service) yang akan dijalankan secara bersamaan. Pada konfigurasi ini terdapat tiga service utama, yaitu:

web (Nginx)
* image: nginx:alpine
Menggunakan image resmi Nginx versi Alpine yang berukuran kecil dan ringan.
*ports: "8080:80"
Menghubungkan port 8080 di komputer lokal ke port 80 di dalam container.
* volumes: ./app:/usr/share/nginx/html:ro
Menghubungkan folder app dari host ke direktori default web nginx di container. Opsi :ro berarti hanya bisa dibaca (read-only).
* depends_on: api
Menandakan bahwa service web bergantung pada service api dan akan dijalankan setelah api aktif.
* networks
Menghubungkan service web ke jaringan internal bernama praktikum-net.

api (Apache HTTPD)
* image: httpd:alpine
Menggunakan image Apache HTTP Server versi ringan.
* ports: "8081:80"
Menghubungkan port 8081 di host ke port 80 di dalam container sehingga dapat diakses secara terpisah.
* networks
Terhubung ke jaringan praktikum-net agar dapat berkomunikasi dengan service lain.

db (PostgreSQL)
* image: postgres:15-alpine
Menggunakan image PostgreSQL versi 15.
* environment
Digunakan untuk mengatur konfigurasi awal database seperti username, password, dan nama database melalui variabel lingkungan.
* volumes: db_data:/var/lib/postgresql/data
Menggunakan named volume untuk menyimpan data database secara permanen agar tidak hilang saat container dihentikan atau dihapus.

networks (praktikum-net)
Mendefinisikan jaringan bertipe bridge yang memungkinkan semua service (web, api, dan db) saling terhubung menggunakan nama service sebagai hostname.

volumes (db_data)

Mendefinisikan named volume bernama db_data yang dikelola oleh Docker untuk menyimpan data database secara persisten.

### Output Docker Compose Up

```
time="2026-02-25T20:49:38-08:00" level=warning msg="C:\\Users\\ASUS\\praktikum-docker\\docker-compose.yml: the attribute `version` is obsolete, it will be ignored, please remove it to avoid potential confusion"
[+] Running 22/22
 ✔ api Pulled                                                                         64.9s
   ✔ abd702cd48c8 Pull complete                                                        2.8s
   ✔ b9df760bab4a Pull complete                                                       58.7s
   ✔ 79273eb2147b Pull complete                                                        2.1s
   ✔ 987f24f891f4 Pull complete                                                        2.8s
   ✔ 3688fd767e4a Pull complete                                                       58.0s
   ✔ 4f4fb700ef54 Pull complete                                                        0.0s
   ✔ 2bd78f43169f Download complete                                                    0.0s
   ✔ 8c8ca383ec3c Download complete                                                    1.6s
 ✔ db Pulled                                                                         191.0s
   ✔ e2808358fab6 Pull complete                                                        3.0s
   ✔ d9fee99ceaeb Pull complete                                                        1.3s
   ✔ fbd2333a8b2e Pull complete                                                      185.0s
   ✔ 6385d21b1497 Pull complete                                                      185.4s
   ✔ 2af348483d54 Pull complete                                                        1.6s
   ✔ 49d5e74d1649 Pull complete                                                      185.5s
   ✔ 1cc5032597da Pull complete                                                        1.7s
   ✔ 2b183e31c9f8 Pull complete                                                        1.5s
   ✔ 8b6feeda4732 Pull complete                                                        3.3s
   ✔ 22021ae8a283 Pull complete                                                        8.6s
   ✔ 19681da0b740 Download complete                                                    0.1s
   ✔ 9543e0459960 Download complete                                                    0.1s
[+] Running 5/5
 ✔ Network praktikum-docker_praktikum-net  Created                                     0.2s
 ✔ Volume praktikum-docker_db_data         Create...                                   0.0s
 ✔ Container praktikum-docker-db-1         Starte...                                   3.2s
 ✔ Container praktikum-docker-api-1        Start...                                    3.3s
 ✔ Container praktikum-docker-web-1        Start...                                    2.3s


```

---

## 📸 Screenshots

| No | Screenshot | Keterangan |
|----|------------|------------|
| 1 | ![Container Running](screenshots/01-container-running.png) | Container yang sedang berjalan |
| 2 | ![Docker Images](screenshots/02-docker-images.png) | Daftar Docker images |
| 3 | ![Dockerfile](screenshots/03-dockerfile-content.png) | Isi file Dockerfile |
| 4 | ![Docker Build](screenshots/04-docker-build.png) | Proses docker build |
| 5 | ![App Browser](screenshots/05-app-browser.png) | Aplikasi berjalan di browser |
| 6 | ![Compose Up](screenshots/06-compose-up.png) | Docker Compose up |

---

## 💭 Refleksi & Kesimpulan

### Yang Dipelajari

Dari praktikum ini, saya belajar tentang konsep dasar kontainerisasi dan perbedaannya yang signifikan dengan virtualisasi tradisional (VM), di mana Docker terbukti lebih ringan dan cepat karena berbagi kernel OS host. Saya memahami siklus hidup container dan berlatih menggunakan perintah dasar Docker CLI (seperti pull, run, ps, logs, dan exec). Selain itu, saya juga belajar cara membangun custom image secara otomatis menggunakan instruksi dalam Dockerfile, serta cara mendefinisikan dan mengelola aplikasi multi-container yang kompleks (web, API, dan database) secara bersamaan menggunakan Docker Compose, lengkap dengan implementasi network untuk komunikasi antar-container dan volume untuk persistensi data.

### Manfaat Docker

Docker sangat membantu dalam memecahkan masalah klasik "it works on my machine" karena Docker mengemas aplikasi beserta seluruh dependensi dan konfigurasinya ke dalam satu unit standar (container). Hal ini memastikan aplikasi akan berjalan secara konsisten di lingkungan apa pun (development, testing, maupun production). Selain itu, isolasi yang diberikan Docker mencegah konflik antar dependensi aplikasi di komputer yang sama. Docker juga mempercepat proses onboarding developer baru dan menyederhanakan workflow deployment CI/CD karena infrastruktur direpresentasikan sebagai kode (Infrastructure as Code) melalui Dockerfile dan docker-compose.yml.

### Tantangan dan Solusi

Ada momen di mana container yang baru dibuat langsung berstatus exited dan tidak bisa diakses.

Solusi: Saya menggunakan perintah docker logs [nama_container] untuk melakukan troubleshooting dan melihat pesan error di dalamnya. Ternyata ada kesalahan typo pada nama environment variable, Setelah diperbaiki dan image di-build ulang, container berhasil berjalan normal.

---

## ✅ Checklist

- [x] Berhasil membuat Dockerfile yang valid
- [x] Berhasil build Docker image
- [x] Container berjalan dan aplikasi bisa diakses
- [x] Docker Compose berhasil dijalankan
- [x] Semua screenshot lengkap dan jelas
- [x] Penjelasan ditulis dengan bahasa sendiri

---

*Laporan ini dibuat pada Rabu, 25 Februari 2026*
