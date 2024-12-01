# FINAL-Projek-OS-Server-Sistem-Admiin
## FINAL PROJEK

- Install NginX Web Server
- Install MYSQL Database server
- Install Samba File Server
- Install Node.js Application Server
- Install Postfix Mail Server

## Installation

## Install NginX Web Server
### langkah 1 Update sistem
```sh
sudo apt update && sudo apt upgrade -y

```
### langkah 2 Install Nginx
```sh
sudo apt install nginx
```
### langkah 3 Menyesuaikan firewall
```sh
sudo ufw allow 'Nginx HTTP'
sudo ufw status
```
Dengan Output

![alt text](https://github.com/Tuanvallen/FINAL-Projek-OS-Server-Sistem-Admiin/blob/main/Foto%20Install%20Nginx/Hasil%20Output%20firewall.png?raw=true)

### langkah 4 Memeriksa web server anda
```sh
systemctl status nginx
```
Dengan Output

![alt text](https://github.com/Tuanvallen/FINAL-Projek-OS-Server-Sistem-Admiin/blob/main/Foto%20Install%20Nginx/Hasil%20Output%20Periksa%20web%20server.png?raw=true)

### langkah 5 Cek Nginx dengan Mengetikkan IP anda
```sh
http://your_server_ip
```
Output

![alt text](https://github.com/Tuanvallen/FINAL-Projek-OS-Server-Sistem-Admiin/blob/main/Foto%20Install%20Nginx/Hasil%20Nginx%20Web%20Server.png?raw=true)

### langkah 6 Konfigurasi Blok Server
```sh
sudo nano /var/www/your_domain/html/index.html
```
Buat file html 
```sh
<html>
    <head>
        <title>Selamat Datang Tuan vallen</title>
    </head>
    <body>
        <h1>Sukses Selalu Tuan Vallen</h1>
        <p>Vallen Aji Kurniawan adalah seorang individu luar biasa dengan segudang talenta.
                Dikenal sebagai sosok ganteng, jago dalam berbagai bidang, dan seorang miliarder, Vallen telah menginspirasi b>
                dan kecerdasan, ia terus menciptakan dampak positif di sekitarnya.<p><br>
        <p>Tak hanya sukses secara materi, Vallen juga dikenal sebagai pribadi yang ramah dan berwawasan luas.
            Sosoknya adalah cerminan dari keberanian dan dedikasi untuk selalu menjadi versi terbaik dari dirinya.<p>
    </body>
</html>
```
Konfigurasi Blok Server agar kontent di atas dapat di akses dengan perintah
```sh
sudo nano /etc/nginx/sites-available/your_domain
```
Ganti dengan Domain Anda Disini Domain saya yaitu Tuan_vallen

```sh
server {
        listen 80;
        listen [::]:80;

        root /var/www/Tuan_vallen/html;
        index index.html index.htm index.nginx-debian.html;

        server_name Tuan_vallen www.Tuan_vallen;

        location / {
                try_files $uri $uri/ =404;
        }
}
```
Cek kembali dengan IP Anda dan akan muncul seperti pada gambar berikut

![alt text](https://github.com/Tuanvallen/FINAL-Projek-OS-Server-Sistem-Admiin/blob/main/Foto%20Install%20Nginx/Hasil%20Web%20server%20Nginx.png?raw=true)


## Install MYSQL Database server

### langkah 1 Install mysql dan pastikan berjalan 
```sh
sudo apt install mysql-server
sudo systemctl start mysql.service
```

### langkah 2 Mengonfigurasi MySQL 
Jalankan skrip keamanan dengan
```sh
sudo mysql_secure_installation
```
Ini akan memandu Anda melalui serangkaian perintah yang memungkinkan Anda membuat beberapa perubahan pada opsi keamanan instalasi MySQL Anda. Perintah pertama akan menanyakan apakah Anda ingin menyiapkan Plugin Validasi Kata Sandi, yang dapat digunakan untuk menguji kekuatan kata sandi pengguna MySQL baru sebelum menganggapnya valid.

Output

![alt text](https://github.com/Tuanvallen/FINAL-Projek-OS-Server-Sistem-Admiin/blob/main/Foto%20Install%20MYSQL/Hasil%20Output%20Plugin%20validasi%20mysql.png?raw=true)


