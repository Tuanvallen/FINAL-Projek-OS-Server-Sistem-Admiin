# FINAL-Projek-OS-Server-Sistem-Admiin
## FINAL PROJEK
# Web Server Setup on Ubuntu 22.04

This guide provides step-by-step instructions to set up a web server on Ubuntu 22.04 with Apache2, Flask, Gunicorn, and SSH Server.

---

## Prerequisites

- A machine running Ubuntu 22.04.
- Root or user with `sudo` privileges.
- Stable internet connection.

---

## Steps to Set Up the Web Server

### 1. Update System Packages
```bash
sudo apt update && sudo apt upgrade -y
```

### 2. Install Apache2 Web Server
```bash
sudo apt install apache2 -y
```
- Enable and start Apache:
```bash
sudo systemctl enable apache2
sudo systemctl start apache2
```

### 3. Install Python3 and Pip
```bash
sudo apt install python3 python3-pip -y
```

### 4. Install Flask Framework
```bash
pip3 install flask
```

### 5. Install Gunicorn
```bash
pip3 install gunicorn
```

### 6. Install and Configure SSH Server
```bash
sudo apt install openssh-server -y
```
- Enable and start SSH:
```bash
sudo systemctl enable ssh
sudo systemctl start ssh
```

### 7. Configure Flask Application
- Create a directory for your Flask application:
```bash
mkdir ~/my_flask_app
cd ~/my_flask_app
```
- Create a sample `app.py` file:
```python
from flask import Flask

app = Flask(__name__)

@app.route('/')
def home():
    return "Hello, World!"

if __name__ == "__main__":
    app.run()
```

### 8. Run Flask with Gunicorn
```bash
gunicorn --bind 0.0.0.0:8000 app:app
```

### 9. Configure Apache to Proxy Requests to Gunicorn
- Enable the necessary Apache modules:
```bash
sudo a2enmod proxy proxy_http
sudo systemctl restart apache2
```
- Create an Apache configuration file for your Flask app:
```bash
sudo nano /etc/apache2/sites-available/my_flask_app.conf
```
Add the following content:
```apache
<VirtualHost *:80>
    ServerName yourdomain.com

    ProxyPass / http://127.0.0.1:8000/
    ProxyPassReverse / http://127.0.0.1:8000/

    ErrorLog ${APACHE_LOG_DIR}/error.log
    CustomLog ${APACHE_LOG_DIR}/access.log combined
</VirtualHost>
```
- Enable the site and restart Apache:
```bash
sudo a2ensite my_flask_app
sudo systemctl restart apache2
```

### 10. Test the Setup
- Open a browser and navigate to `http://<your-server-ip>`.
- You should see "Hello, World!" displayed.

---

## Troubleshooting

- Check Apache logs:
```bash
sudo tail -f /var/log/apache2/error.log
```
- Check Flask/Gunicorn logs:
```bash
journalctl -u gunicorn
```

---

## Optional: Secure Your Server with SSL (Let's Encrypt)
- Install Certbot:
```bash
sudo apt install certbot python3-certbot-apache -y
```
- Obtain and install an SSL certificate:
```bash
sudo certbot --apache
```
- Test SSL renewal:
```bash
sudo certbot renew --dry-run
```

---

## Conclusion
You have successfully set up a web server on Ubuntu 22.04 using Apache2, Flask, Gunicorn, and SSH Server. Customize your Flask app as needed and deploy it confidently.

---


