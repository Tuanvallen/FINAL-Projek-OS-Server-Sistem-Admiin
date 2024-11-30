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

