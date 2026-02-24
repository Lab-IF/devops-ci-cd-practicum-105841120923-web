# 📋 Laporan Praktikum Pertemuan 01
## DevOps Culture & Principles

---

## 👤 Identitas Mahasiswa

| Item | Keterangan |
|------|------------|
| **Nama** | Wafiq Azizah  |
| **NIM** | 105841120923 |
| **Kelas** | 5B |
| **Tanggal** | 2026-02-25 |

---

## 📚 Pemahaman DevOps

### Apa itu DevOps?

DevOps adalah pendekatan dalam pengembangan perangkat lunak yang menggabungkan Development (Dev) dan Operations (Ops) agar bekerja secara kolaboratif dan terintegrasi. Jika dulu tim developer hanya fokus menulis kode dan tim operasional bertugas menjalankan serta memelihara sistem, DevOps menyatukan kedua peran tersebut agar proses pengembangan hingga deployment berjalan lebih cepat, stabil, dan efisien.
Konsep utama DevOps adalah kolaborasi, otomatisasi, integrasi berkelanjutan (Continuous Integration), dan pengiriman berkelanjutan (Continuous Delivery/Deployment). Dengan DevOps, setiap perubahan kode dapat langsung diuji, dibangun, dan dirilis secara otomatis menggunakan pipeline CI/CD. Selain itu, DevOps juga menekankan penggunaan tools seperti Git untuk version control, Docker untuk containerization, serta monitoring tools untuk memastikan aplikasi tetap berjalan dengan baik.
Tujuan utama DevOps adalah mempercepat siklus pengembangan software tanpa mengorbankan kualitas dan keamanan. Manfaatnya antara lain mempercepat waktu rilis produk, mengurangi kesalahan manusia karena otomatisasi, meningkatkan stabilitas sistem, serta meningkatkan kolaborasi antar tim. Dengan DevOps, perusahaan dapat lebih responsif terhadap kebutuhan pasar dan perubahan teknologi.

### Mengapa DevOps Penting?

DevOps sangat penting karena industri software saat ini bergerak sangat cepat. Pengguna mengharapkan fitur baru, perbaikan bug, dan peningkatan performa dalam waktu singkat. Tanpa DevOps, proses rilis software bisa memakan waktu lama dan berisiko tinggi terjadi error saat deployment.
Sebagai contoh, aplikasi e-commerce harus mampu memperbarui fitur promo atau sistem pembayaran dengan cepat tanpa mengganggu layanan. Dengan DevOps, perubahan dapat diuji otomatis dan langsung dirilis tanpa downtime yang lama. DevOps juga penting dalam sistem berbasis cloud yang membutuhkan skalabilitas tinggi.
Selain itu, DevOps membantu perusahaan mengurangi biaya operasional karena proses deployment dan testing dilakukan secara otomatis. Jika terjadi kesalahan, sistem monitoring dapat langsung mendeteksi dan memperbaiki masalah dengan cepat. Dalam era transformasi digital, DevOps menjadi kunci agar perusahaan tetap kompetitif dan inovatif.

### Contoh Perusahaan yang Menerapkan DevOps

1. Netflix menerapkan DevOps dengan sistem cloud berbasis microservices dan otomatisasi deployment. Mereka menggunakan pendekatan Continuous Delivery sehingga dapat melakukan ribuan deployment setiap hari tanpa mengganggu layanan streaming. Netflix juga menggunakan monitoring dan sistem pengujian otomatis untuk menjaga stabilitas layanan yang digunakan jutaan pengguna di seluruh dunia.

2. Amazon menerapkan DevOps untuk mendukung platform e-commerce berskala global. Dengan otomatisasi CI/CD dan infrastruktur cloud, Amazon mampu merilis fitur baru secara cepat dan stabil. DevOps membantu Amazon memastikan sistem tetap berjalan meskipun terjadi lonjakan trafik besar, seperti saat promo besar atau hari belanja nasional.

---

## 🎯 Pemahaman Prinsip CALMS

1. C – Culture (Budaya Kolaborasi)
Culture menekankan pentingnya kolaborasi antara tim development dan operations. Dalam DevOps, tidak ada lagi sekat atau saling menyalahkan ketika terjadi error. Semua tim bekerja bersama untuk mencapai tujuan yang sama, yaitu memberikan layanan terbaik kepada pengguna.

Contoh penerapan:
Sebuah perusahaan startup membuat tim lintas fungsi (developer, QA, dan ops dalam satu tim). Ketika terjadi bug setelah deployment, semua anggota tim bersama-sama melakukan analisis dan perbaikan tanpa menyalahkan pihak tertentu. Mereka juga rutin melakukan retrospective meeting untuk evaluasi proses kerja.

2. A – Automation (Otomatisasi)
Automation berarti mengurangi pekerjaan manual dengan mengotomatiskan proses build, testing, dan deployment menggunakan tools CI/CD.

Contoh penerapan:
Tim menggunakan Git untuk version control dan menghubungkannya dengan pipeline CI/CD. Setiap kali developer melakukan push kode, sistem otomatis menjalankan testing dan melakukan deployment ke server staging. Dengan ini, kesalahan manual dapat dikurangi dan proses rilis menjadi lebih cepat.

3. L – Lean (Efisiensi dan Minimasi Pemborosan)
Lean berfokus pada peningkatan proses secara berkelanjutan dan menghilangkan aktivitas yang tidak memberikan nilai tambah.

Contoh penerapan:
Sebuah perusahaan mengurangi proses approval yang terlalu panjang sebelum deployment. Mereka menyederhanakan alur kerja sehingga fitur baru bisa dirilis dalam hitungan hari, bukan minggu. Evaluasi rutin dilakukan untuk menemukan hambatan dalam proses kerja.

4. M – Measurement (Pengukuran)
Measurement berarti semua proses harus diukur agar dapat dievaluasi dan ditingkatkan. Data digunakan untuk pengambilan keputusan, bukan asumsi.

Contoh penerapan:
Tim memonitor metrik seperti deployment frequency, lead time, error rate, dan downtime server. Jika angka error meningkat, tim segera melakukan investigasi berdasarkan data monitoring tersebut.

5. S – Sharing (Berbagi Pengetahuan)
Sharing menekankan transparansi dan berbagi informasi antar tim agar semua memiliki pemahaman yang sama.

Contoh penerapan:
Tim membuat dokumentasi internal dan melakukan sesi knowledge sharing setiap minggu. Mereka juga menggunakan dashboard bersama agar semua anggota dapat melihat status sistem secara real-time.

---

## 🔧 Setup Development Environment

### Versi Software

| Software | Versi |
|----------|-------|
| Git | git version 2.51.0 |
| Docker | docker version 29.1.2 |

### Konfigurasi Git

```
user.name=Wafiq Azizah
user.email= 105841120923@student.unismuh.ac.id
```

### VS Code Extensions

1. docker 
2. gitlens
3. yaml
4. remote-containers

### GitHub Account

- Username: wafiq_azizah

---

## 📸 Screenshots

| No | Screenshot | Keterangan |
|----|------------|------------|
| 1 | ![Git Version](screenshots/01-git-version.png) | Output git --version |
| 2 | ![Git Config](screenshots/02-git-config.png) | Output git config --list |
| 3 | ![Docker Version](screenshots/03-docker-version.png) | Output docker --version |
| 4 | ![Docker Hello World](screenshots/04-docker-hello-world.png) | Output docker run hello-world |
| 5 | ![VS Code](screenshots/05-vscode-extensions.png) | VS Code dengan extensions |



## ✅ Checklist

- [x] Git terinstall dan terkonfigurasi dengan benar
- [x] Docker dapat menjalankan container hello-world
- [x] VS Code terinstall dengan semua extensions yang diminta
- [x] Laporan ditulis dengan bahasa yang baik dan benar
- [x] Semua screenshot jelas dan terbaca

---

*Laporan ini dibuat pada Rabu, 25 Februari 2026*
