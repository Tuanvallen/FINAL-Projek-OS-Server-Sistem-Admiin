# FINAL-Projek-OS-Server-Sistem-Admiin
## FINAL PROJEK

- Install NginX Web Server
- Install MYSQL Database server
- Install Samba File Server
- Install Node.js Application Server
- Install Postfix Mail Server

## Installation

## Install Nginx
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

![alt text](https://github.com/Tuanvallen/FINAL-Projek-OS-Server-Sistem-Admiin/blob/main/SS%20foto%20Final%20Projek/Hasil%20Output%20firewall.png?raw=true)

### langkah 4 Memeriksa web server anda
```sh
systemctl status nginx
```
Dengan Output

![alt text](https://github.com/Tuanvallen/FINAL-Projek-OS-Server-Sistem-Admiin/blob/main/SS%20foto%20Final%20Projek/Hasil%20Output%20Periksa%20web%20server.png?raw=true)

### langkah 5 Cek Nginx dengan Mengetikkan IP anda
```sh
http://your_server_ip
```
Output

![alt text](https://github.com/Tuanvallen/FINAL-Projek-OS-Server-Sistem-Admiin/blob/main/SS%20foto%20Final%20Projek/Hasil%20Nginx%20Web%20Server.png?raw=true)

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
        <h1>Sukses Selalu Tuan Vallen untuk yang ke 20</h1>
    </body>
</html>
```
Ganti yourdomain dengan domain Anda disini saya sudah ganti dengan domain saya yaitu Tuan_vallen 
```sh
sudo nano /etc/nginx/sites-available/your_domain
```
Ganti lagi

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

![alt text](https://github.com/Tuanvallen/FINAL-Projek-OS-Server-Sistem-Admiin/blob/main/SS%20foto%20Final%20Projek/Hasil%20Web%20server%20Nginx.png?raw=true)
