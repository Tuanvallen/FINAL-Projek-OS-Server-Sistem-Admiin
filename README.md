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
