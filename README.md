# ติตดั้ง OS almalinux *
ssh root@password

root = user
## Update OS

* yum update -y
* dnf clean all
* dnf group install "Development Tools"

## Install Mariadb
* yum install mariadb mariadb-devel mariadb-server pcre-devel zlib-devel git
* ถ้าไม่ได้ลอง  yum install mariadb mariadb-server pcre-devel zlib-devel git
* yum -y install dos2unix gdb nano unzip wget zip
* rpm --import /etc/pki/rpm-gpg/RPM-GPG-KEY*
* yum -y install epel-release
* systemctl start mariadb.service
* systemctl enable mariadb.service
* mysql_secure_installation


## Create Table

* mysql -u root -p
* CREATE USER ''@'%' IDENTIFIED BY '';   ---> example   CREATE USER 'mint'@'%' IDENTIFIED BY 'password';
* CREATE USER ''@'localhost' IDENTIFIED BY '';  ---> example CREATE USER 'mint'@'localhost' IDENTIFIED BY 'password';

## กำหนดสิทธิ์

* GRANT ALL PRIVILEGES ON * . * TO ''@'%';  ---> example  GRANT ALL PRIVILEGES ON * . * TO 'mint'@'%';
* GRANT ALL PRIVILEGES ON * . * TO ''@'localhost';  ---> example GRANT ALL PRIVILEGES ON * . * TO 'mint'@'localhost';
* FLUSH PRIVILEGES;
* exit;

## firewall setting
* dnf install -y firewalld (ถ้า bash: firewall-cmd: command not found)
* firewall-cmd --zone=public --add-port=80/tcp --permanent  ----> [http]
* firewall-cmd --zone=public --add-port=443/tcp --permanent   ----> [https]
* firewall-cmd --reload

อีกวิธีหนึ่ง ติดตั้ง firewall
* sudo yum install firewalld -y
* sudo systemctl start firewalld
* sudo systemctl enable firewalld

* sudo firewall-cmd --permanent --add-service={http,https}
* sudo firewall-cmd --reload

## How to Install Nginx, MariaDB, and PHP on AlmaLinux 9
* https://linuxiac.com/how-to-install-lemp-stack-on-almalinux-9/
* sudo nano /etc/nginx/nginx.conf
* add --> client_max_body_size 50M; to file //ให้สามารถเพิ่มไฟล์ขนาดใหญ่ได้
* sudo systemctl reload nginx
  
## install certbot
* sudo dnf install epel-release
* sudo dnf install certbot python3-certbot-nginx
* sudo dnf update
* sudo dnf install certbot python3-certbot-nginx

## แก้ไข Permission denied  433
* sudo chown -R nginx:nginx /home
* sudo setenforce 0
* sudo getenforce
* ถ้า status = Permissive ถือว่าโอเค

## Install nodeJS
* https://www.liquidweb.com/kb/install-node-js-linux-almalinux/

## Firewall setting
* sudo firewall-cmd --list-all
* sudo firewall-cmd --permanent --add-port=3306/tcp
* sudo firewall-cmd --reload

## Install PM2
* https://pm2.io/docs/runtime/guide/installation/

## Auto start process (Case reboot)
* ถ้าคุณต้องการ ปิด SELinux ถาวร
* เข้าไปแก้ไขไฟล์ sudo nano /etc/selinux/config แก้ SELINUX=enforcing เป็น SELINUX=permissive และ sudo reboot

* ให้ Nginx ทำงานอัตโนมัติ
* sudo systemctl enable nginx
* sudo systemctl start nginx

* ให้ PM2 restore แอปทุกครั้งที่บูต
* pm2 startup
* sudo env PATH=$PATH:/usr/bin pm2 startup systemd -u root --hp /root
* pm2 save

*  ตรวจสอบว่า nginx
*  sudo systemctl status nginx
*  sudo ss -tulpn | grep :80

*  ตรวจสอบ firewall ว่ายังเปิด port 80, 443
*  sudo firewall-cmd --permanent --add-port=80/tcp
*  sudo firewall-cmd --permanent --add-port=443/tcp
*  sudo firewall-cmd --reload




  
