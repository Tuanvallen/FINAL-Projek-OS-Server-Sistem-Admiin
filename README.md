# FINAL-Projek-OS-Server-Sistem-Admin
## FINAL PROJEK
# Pengaturan Server Web pada Ubuntu 22.04

Panduan ini memberikan langkah-langkah untuk mengatur server web di Ubuntu 22.04 dengan Apache2, Flask, Gunicorn, dan SSH Server.

---

## Prasyarat

- Mesin dengan sistem operasi Ubuntu 22.04.
- Akses root atau pengguna dengan hak `sudo`.
- Koneksi internet yang stabil.

---

## Langkah-Langkah Pengaturan Server Web

### 1. Perbarui Paket Sistem
```bash
sudo apt update && sudo apt upgrade -y
```

### 2. Instal Apache2 Web Server
```bash
sudo apt install apache2 -y
```
- Aktifkan dan mulai Apache:
```bash
sudo systemctl enable apache2
sudo systemctl start apache2
```

### 3. Instal Python3 dan Pip
```bash
sudo apt install python3 python3-pip -y
```

### 4. Instal Framework Flask
```bash
pip3 install flask
```

### 5. Instal Gunicorn
```bash
pip3 install gunicorn
```

### 6. Instal dan Konfigurasi SSH Server
```bash
sudo apt install openssh-server -y
```
- Aktifkan dan mulai SSH:
```bash
sudo systemctl enable ssh
sudo systemctl start ssh
```

### 7. Konfigurasi Aplikasi Flask
- Buat direktori untuk aplikasi Flask Anda:
```bash
mkdir ~/my_flask_app
cd ~/my_flask_app
```
- Buat file `app.py` sederhana:
```python
from flask import Flask

app = Flask(__name__)

@app.route('/')
def home():
    return "Hello, World!"

if __name__ == "__main__":
    app.run()
```

### 8. Jalankan Flask dengan Gunicorn
```bash
gunicorn --bind 0.0.0.0:8000 app:app
```

### 9. Konfigurasi Apache untuk Meneruskan Permintaan ke Gunicorn
- Aktifkan modul Apache yang diperlukan:
```bash
sudo a2enmod proxy proxy_http
sudo systemctl restart apache2
```
- Buat file konfigurasi Apache untuk aplikasi Flask Anda:
```bash
sudo nano /etc/apache2/sites-available/my_flask_app.conf
```
Tambahkan konten berikut:
```apache
<VirtualHost *:80>
    ServerName yourdomain.com

    ProxyPass / http://127.0.0.1:8000/
    ProxyPassReverse / http://127.0.0.1:8000/

    ErrorLog ${APACHE_LOG_DIR}/error.log
    CustomLog ${APACHE_LOG_DIR}/access.log combined
</VirtualHost>
```
- Aktifkan situs dan restart Apache:
```bash
sudo a2ensite my_flask_app
sudo systemctl restart apache2
```

### 10. Uji Pengaturan
- Buka browser dan akses `http://<ip-server-anda>`.
- Anda seharusnya melihat pesan "Hello, World!" ditampilkan.

---

## Langkah Hosting dengan Cloudflare Tunnel

### 11. Instal Cloudflare Tunnel
- Unduh dan instal Cloudflare Tunnel:
```bash
curl -L https://github.com/cloudflare/cloudflared/releases/latest/download/cloudflared-linux-amd64 -o cloudflared
sudo mv cloudflared /usr/local/bin/
sudo chmod +x /usr/local/bin/cloudflared
```

### 12. Login ke Akun Cloudflare
- Jalankan perintah berikut untuk login ke akun Cloudflare Anda:
```bash
cloudflared tunnel login
```
- Ikuti tautan yang diberikan untuk mengautentikasi dan memilih domain Anda.

### 13. Buat dan Jalankan Tunnel
- Buat tunnel baru:
```bash
cloudflared tunnel create my_flask_app
```
- Konfigurasi tunnel:
```bash
sudo nano /etc/cloudflared/config.yml
```
Tambahkan konten berikut:
```yaml
tunnel: my_flask_app
credentials-file: /root/.cloudflared/<credentials-file>.json

ingress:
  - hostname: yourdomain.com
    service: http://localhost:80
  - service: http_status:404
```
- Jalankan tunnel:
```bash
sudo cloudflared tunnel run my_flask_app
```

### 14. Konfigurasi DNS di Cloudflare
- Masuk ke dashboard Cloudflare dan tambahkan DNS record dengan tipe `CNAME`:
  - Nama: `yourdomain.com`
  - Target: `my_flask_app` (sesuai nama tunnel Anda)

---

---

## Kesimpulan
Anda telah berhasil mengatur server web di Ubuntu 22.04 menggunakan Apache2, Flask, Gunicorn, SSH Server, dan Cloudflare Tunnel. Dengan konfigurasi ini, aplikasi Flask Anda dapat diakses secara aman melalui domain yang terhubung ke Cloudflare.

---
