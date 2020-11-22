---
layout: single
title: "Instalasi Apache, MySQL, PHP"
date:   2020-11-08 14:28:00 +0700
toc: true
categories:
tags:
  - apache
  - mysql
  - php
  - lamp stack
---
Apache, MySQL, dan PHP adalah satu paket kumpulan software yang populer digunakan untuk membangun website yang sudah lengkap dengan database dan platform web-nya. 

# 1. Instalasi Apache
Apache web server adalah software yang diperlukan untuk menjadikan sebuah komputer sebagai server web. 

## Debian
Untuk Instalasi di Linux berbasis Debian:

    sudo apt install apache2 -y
	
Jika menggunakan Ubuntu, ubah konfigurasi ufw (Ubuntu Firewall) setelah instalasi Apache:

    sudo ufw allow in "Apache Full"

## Redhat/CentOS
Untuk Instalasi di Linux berbasis Redhat/Fedora/CentOS:

    sudo yum install httpd -y

Kemudian jalankan service dan aktifkan autostartnya:

    sudo systemctl start httpd
	sudo systemctl enable httpd

Untuk mengetahui service sedang running atau tidak, jalankan: 

    systemctl status httpd
	
## Arch
Untuk Instalasi di Linux berbasis Arch/Manjaro:

    sudo pacman -S apache

Kemudian jalankan service dan aktifkan autostartnya:

    sudo systemctl start httpd
	sudo systemctl enable httpd

Setelah menginstal Apache, kita perlu mengubah beberapa konfigurasi.

    sudo nano /etc/httpd/conf/httpd.conf

Hapus comment (\#) pada bagian depan LoadModule unique_id_module sehingga menjadi seperti ini:

    LoadModule unique_id_module modules/mod_unique_id.so

Simpan file, kemudian restart service dengan menggunakan command:

    sudo systemctl restart httpd

Untuk mengetahui service sedang running atau tidak, jalankan:

    systemctl status httpd

*****
Test layanan Apache dengan membuka browser dan masukkan IP address kedalam address bar.
Contoh: http://192.168.0.1/

**Khusus Arch**, jika localhost / IP address tidak bisa diakses, tambahkan entri baru pada file hosts

    sudo nano /etc/hosts

Kemudian, tambahkan line ini:

    127.0.0.1       localhost.localdomain   localhost droplet1

Simpan file, kemudian restart service dengan menggunakan command:

    sudo systemctl restart httpd

Untuk mengetahui IP address, gunakan command ini (pilih salah satu):

    hostname -I #debian
	ifconfig eth0 | grep inet | awk '{ print $2 }' #debian
	ip addr show eth0 | grep inet | awk '{ print $2; }' | sed 's/\/.*$//'` #arch
	
# 2. Instalasi MySQL
MySQL server adalah software yang diperlukan untuk menjadikan sebuah komputer sebagai server database. MariaDB adalah implementasi open source dari MySQL yang diciptakan untuk menggantikan MySQL yang saat ini menggunakan lisensi propietary. Oleh karena itu, MariaDB fully compatible dengan MySQL.

## Debian
Untuk instalasi di Linux berbasis Debian:

    sudo apt install mariadb-server -y

## Redhat/CentOS
Untuk instalasi di Linux berbasis Redhat/Fedora/CentOS:

    sudo yum install mariadb-server mariadb -y
	
Kemudian jalankan service dan aktifkan autostartnya:

    sudo systemctl start mariadb
	sudo systemctl enable mariadb
	
Untuk mengetahui service sedang running atau tidak, jalankan:

    systemctl status mariadb

## Arch
Untuk instalasi di Linux berbasis Arch/Manjaro:

    sudo pacman -S mysql
	
Initialize MariaDB directory sebelum menjalankan service dengan command:

    sudo mysql_install_db --user=mysql --basedir=/usr --datadir=/var/lib/mysql

Kemudian jalankan service dan aktifkan autostartnya:

    sudo systemctl start mysqld
	sudo systemctl enable mysqld
	
Untuk mengetahui service sedang running atau tidak, jalankan:

    systemctl status mysqld
	
*****
# Konfigurasi MySQL
Setelah MySQL selesai diinstal, kemudian jalankan secure installation dengan command: 

    sudo mysql_secure_installation

Kemudian akan muncul prompt seperti di bawah ini. Ikuti langkah-langkahnya dengan memasukkan password root saat ini. 
```
NOTE: RUNNING ALL PARTS OF THIS SCRIPT IS RECOMMENDED FOR ALL MariaDB
 SERVERS IN PRODUCTION USE! PLEASE READ EACH STEP CAREFULLY!

In order to log into MariaDB to secure it, we'll need the current
password for the root user. If you've just installed MariaDB, and
you haven't set the root password yet, the password will be blank,
so you should just press enter here.

Enter current password for root (enter for none): ## Press Enter
OK, successfully used password, moving on...
```
Kita bisa mengatur untuk mengeset password root untuk MariaDB dengan mengetik `y` ataupun melewatkannya dengan mengetik `n`. Jika ingin menjalankan aplikasi web ataupun melakukan instalasi Wordpress, masukkan password pada tahap ini.
```
Setting the root password ensures that nobody can log into the MariaDB
root user without the proper authorisation.

Set root password? [Y/n]## Press Enter
New password:##  Enter password
Re-enter new password:  ## Re-enter password
Password updated successfully!
Reloading privilege tables..
 ... Success!
```
Untuk memanfaatkan secure installation sepenuhnya, ketikkan `y` atau tekan **Enter** pada setiap prompt yang muncul 
```
By default, a MariaDB installation has an anonymous user, allowing anyone
to log into MariaDB without having to have a user account created for
them. This is intended only for testing, and to make the installation
go a bit smoother. You should remove them before moving into a
production environment.

Remove anonymous users? [Y/n]## Press Enter
 ... Success!

Normally, root should only be allowed to connect from 'localhost'. This
ensures that someone cannot guess at the root password from the network.

Disallow root login remotely? [Y/n]## Press Enter
 ... Success!

By default, MariaDB comes with a database named 'test' that anyone can
access. This is also intended only for testing, and should be removed
before moving into a production environment.

Remove test database and access to it? [Y/n]## Press Enter
 - Dropping test database...
 ... Success!
 - Removing privileges on test database...
 ... Success!

Reloading the privilege tables will ensure that all changes made so far
will take effect immediately.

Reload privilege tables now? [Y/n]## Press Enter
 ... Success!

Cleaning up...

All done! If you've completed all of the above steps, your MariaDB
installation should now be secure.

Thanks for using MariaDB!
```

# 3. Instalasi PHP
PHP (Hypertext Preprocessor) adalah bahasa pemrograman scripting berbasis server-side yang berfungsi untuk menampilkan halaman web yang dinamis. PHP adalah salah satu bahasa yang paling populer digunakan untuk pengembangan web.

## Debian
Untuk Instalasi di Linux berbasis Debian:

    sudo apt install php php-mysql -y

Kemudian agar Apache mengenali PHP, restart Apache web server:

    sudo service apache2 restart

## Redhat/CentOS
Untuk Instalasi di Linux berbasis Redhat/Fedora/CentOS:

    sudo yum install php php-mysql -y
	
Kemudian agar Apache mengenali PHP, restart Apache web server:

    sudo systemctl restart httpd.service

## Arch
Untuk Instalasi di Linux berbasis Arch/Manjaro:

    sudo pacman -S php php-apache
	
Setelah menginstal PHP, kita perlu mengubah beberapa konfigurasi.

    sudo nano /etc/httpd/conf/httpd.conf
    
Beri comment (\#) pada bagian LoadModule mpm_event_module sehingga menjadi seperti ini: 

    #LoadModule mpm_event_module modules/mod_mpm_event.so
	
Hapus comment (\#) pada bagian depan \#LoadModule mpm_prefork_module sehigga menjadi seperti ini:

    LoadModule mpm_prefork_module modules/mod_mpm_prefork.so`

Tambahkan line ini pada bagian paling bawah LoadModule:

    LoadModule php7_module modules/libphp7.so
	AddHandler php7-script php
	
Tambahkan line ini pada bagian paling bawah Include:

    Include conf/extra/php7_module.conf

Kemudian agar Apache mengenali PHP, restart Apache web server:

    sudo systemctl restart httpd

*****
Untuk mengecek versi PHP yang terpasang, gunakan command `php -v`

Untuk memastikan PHP sudah bisa digunakan, buat file info.php pada folder /var/www/html/

Menggunakan echo:

    echo "<?php phpinfo(); ?>" > /var/www/html/info.php

Menggunakan nano text editor:

    sudo nano /var/www/html/info.php

Ketikkan teks ini kedalam file tersebut:
```php
<?php phpinfo(); ?>
```
Kemudian simpan file tersebut.

> **Khusus Arch**, buat file info.php pada folder `/srv/http/`

Test file PHP yang sudah disimpan dengan membuka browser dan masukkan IP address kedalam address bar.
Contoh: http://192.168.0.1/info.php

Server telah siap digunakan untuk implementasi aplikasi berbasis PHP. Konfigurasi ini sering disebut sebagai LAMP Stack (Linux, Apache, MySQL, PHP). Salah satu aplikasi web populer berbasis LAMP Stack adalah WordPress.

**Keterangan**:
\*)  `-y` digunakan untuk persetujuan instalasi tanpa konfirmasi.  
\*) DocumentRoot pada Arch terletak di `srv/http/`  
\*) DocumentRoot pada Debian/Redhat terletak di `/var/www/html/`  

**Referensi**:
* [Arch Linux Wiki - Apache HTTP Server](https://wiki.archlinux.org/index.php/Apache_HTTP_Server)
* [Arch Linux Wiki - MariaDB](https://wiki.archlinux.org/index.php/MariaDB)
* [Arch Linux Wiki - PHP](https://wiki.archlinux.org/index.php/PHP)
* [DigitalOcean - LAMP Stack on Arch Linux](https://www.digitalocean.com/community/tutorials/how-to-install-linux-apache-mysql-php-lamp-stack-on-arch-linux)
* [DigitalOcean - LAMP Stack on Debian](https://www.digitalocean.com/community/tutorials/how-to-install-linux-apache-mysql-php-lamp-stack-on-debian)
* [DigitalOcean - LAMP Stack on CentOS 7](https://www.digitalocean.com/community/tutorials/how-to-install-linux-apache-mysql-php-lamp-stack-on-centos-7)
* [HowToForge - CentOS LAMP Server](https://www.howtoforge.com/tutorial/centos-lamp-server-apache-mysql-php/)