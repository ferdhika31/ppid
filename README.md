# PPID
Website Pejabat Pengelola Informasi dan Dokumentasi

![ppid-web](https://user-images.githubusercontent.com/8111407/44639099-429ca580-a9e4-11e8-81c5-eb8b803572b2.png)

## Laravel 5.4
Laravel is a web application framework with expressive, elegant syntax. We believe development must be an enjoyable, creative experience to be truly fulfilling. Laravel attempts to take the pain out of development by easing common tasks used in the majority of web projects, such as authentication, routing, sessions, queueing, and caching.
Laravel is accessible, yet powerful, providing tools needed for large, robust applications. A superb inversion of control container, expressive migration system, and tightly integrated unit testing support give you the tools you need to build any application with which you are tasked.

### Dokumentasi Resmi

Dokumentasi framework dapat ditemukan di [Laravel website](http://laravel.com/docs/5.4).

# Konten
* [Packages](#packages)
* [Requirement](#requirement)
* [Pengembangan pada Lokal](#pengembangan-pada-lokal)
* [Deploy Proyek di Shared Hosting (CPANEL)](#deploy-proyek-di-shared-hosting-cpanel)
* [Deploy Proyek di VPS (Ubuntu 16.04) Nginx](#deploy-proyek-di-vps-ubuntu-1604-nginx)
* [Akun](#akun)

# Packages
* [Laravel-Gravatar](https://github.com/thomaswelton/laravel-gravatar) by [ThomasWelton](https://github.com/thomaswelton)
* [Laravel-Breadrumbs](https://github.com/davejamesmiller/laravel-breadcrumbs) by [DaveJamesMiller](https://github.com/davejamesmiller)
* [Laravel-Menu](https://github.com/lavary/laravel-menu) by [Lavary](https://github.com/lavary)
* [Laravel-UUID](https://github.com/ramsey/uuid) by [Ramsey](https://github.com/ramsey)
* [Laravel-RoleManagement](https://github.com/zizaco/entrust) by [Zizaco](https://github.com/zizaco)
* [Laravel-Excel](https://github.com/Maatwebsite/Laravel-Excel) by [Maatwebsite](https://github.com/Maatwebsite)
* [Laravel-PDFViewer](https://github.com/goodnesskay/LARAVEL-PDF-VIEWER) by [goodnesskay](https://github.com/goodnesskay)
* [Google Recaptcha](https://github.com/google/recaptcha) by [Google](https://github.com/google)

# Requirement
## Laravel Requirement
Sebelum mencoba menerapkan aplikasi Laravel di environment lokal, shared hosting atau vps, Pastikan bahwa layanan yang akan digunakan menyediakan [persyaratan yang sesuai untuk Laravel](https://laravel.com/docs/5.4#server-requirements). Pada dasarnya, item berikut diperlukan untuk Laravel 5.*:

* PHP >= 5.6.4
* OpenSSL PHP Extension
* PDO PHP Extension
* Mbstring PHP Extension
* Tokenizer PHP Extension
* XML PHP Extension

## Project Requirement
Untuk menerapkan project di environment lokal, shared hosting atau vps, Pastikan bahwa sudah terinstall layanan dibawah :

* MariaDB atau MySQL
* [Register Google Recaptha](https://www.google.com/recaptcha)
* [Mailtrap](https://mailtrap.io) or [Gmail](https://learninglaravel.net/learn-to-send-emails-using-gmail-and-sendgrid-in-laravel-5)
* Phpmyadmin (Optional)

## Local & VPS Requirement
Untuk menerapkan project di environment lokal atau vps, Pastikan bahwa sudah terinstall layanan dibawah : 

* Git
* Composer

# Pengembangan pada Lokal

## Step 1

### Menggunakan GIT
Clone git repository

Menggunakan Git SSH
```
git clone git@gitlab.com:gov/produk/website_ppid.git ppid
```

Atau dengan HTTPS
```
git clone https://git.gamatechno.net/gov/produk/website_ppid.git ppid
```

Masuk ke folder projek dengan perintah
```
cd ppid
```

Lalu lakukan update composer  
```
composer update
```

## Step 2
Salin file ```.env.example``` pada direktori yang sama dengan nama ```.env```

Perintah untuk OS Unix
```
cp .env.example .env
```
Perintah untuk OS Windows
```
copy .env.example .env
```

Lakukan perintah dibawah untuk menggenerate key unik laravel

```
php artisan key:generate
```

Buat database dengan mysql

Konfigurasi file ```.env``` dan ketik perintah dibawah untuk melakukan migration database :
```
php artisan migrate:refresh --seed
```

Untuk menjalankan aplikasi, ketik perintah di bawah :
```
php artisan serve
```
**WARNING** : Untuk auth support, recaptcha support dan email support, configure your ```.env``` file with ```database``` and ```smtp``` connection !

You are ready for a new Laravel 5.4 application !!


# Deploy Proyek di Shared Hosting (CPANEL)

## Step 1 (Optional jika sudah pernah melakukan instalasi pada lokal)

Lakukan perintah seperti di [Pengembangan Lokal](#pengembangan-pada-lokal)

## Step 2
Buka halaman masuk cPanel dengan menggunakan alamat IP aksesnya yang disediakan oleh penyedia hosting. Gunakan **File Manager**, **MySQL® Databases**, dan fitur **phpMyAdmin** di cPanel.

## Step 3
Buka fitur **File Manager** yang ada pada fitur cPanel. Buat Folder baru di direktori home. beri nama folder baru dengan nama "**ppid**". Sebagai contoh : 
![image](https://user-images.githubusercontent.com/8111407/44641105-8ea11780-a9ef-11e8-916d-4313905cead7.png)

Masuklah ke dalam folder proyek yang ada di komputer lokal Anda. Buka terminal Anda di dalam folder proyek PPID dan jalankan ```php artisan cache:clear``` untuk mengosongkan cache aplikasi dan kemudian jalankan ```php artisan config:clear``` untuk menghapus versi file konfig Anda, jika ada.

Sekarang zip seluruh proyek PPID, dan *upload* zip ke dalam direktori "**ppid**" yang ada pada **File Manager Cpanel**. Saat *upload* selesai, unzip semua file yang ada pada zip ke folder **public_html** dengan memilih tujuan masih dalam folder tersebut. Jika penyedia hosting memungkinkan untuk menggunakan SSH (Secure Shell), Maka dapat melakukan cloning repo ini secara langsung dan kemudian jalankan perintah perintah seperti pada [Pengembangan Lokal](#pengembangan-pada-lokal). 

Sekarang masuklah ke folder **public** pada proyek PPID (/**ppid/public**). Aktifkan **Show Hidden Files (dotfiles)** pada Pengaturan (di pojok kanan atas) File Manager untuk menampilkan **dotfiles**. Selanjutnya, salin semua file yang ada di dalam folder public (/**ppid/public**) ke folder public_html (/**public_html**) .

## Step 3
Buka folder **public_html** dan pastikan semua file di dalam folder **public** proyek PPID telah disalin dengan benar ke folder **public_html**. Buka file **index.php** (/**public_html/index.php**) di *Code Editor*. Cari bari code yang ada seperti di bawah :
```php
// ...
require __DIR__.'/../bootstrap/autoload.php';

// ...
$app = require_once __DIR__.'/../bootstrap/app.php';
```

Ubah dengan menambahkan nama folder proyek tepat sebelum nama folder bootstrap (/**ppid/bootstrap/...**) sebagai berikut :
```php
// ...
require __DIR__.'/../ppid/bootstrap/autoload.php';

// ...
$app = require_once __DIR__.'/../ppid/bootstrap/app.php';
```

## Step 4
Buka fitur **MySQL® Databases** yang ada pada fitur cPanel. Buat Database dan User baru setelah dibuat tambahkan user ke database dan beri *privilages*. 

Buka fitur **phpMyAdmin** lalu buka database yang sebelumnya dibuat dan import file sql yang ada di folder project [(/**ppid/database/db_ppid.sql**)](https://git.gamatechno.net/gov/produk/website_ppid/blob/master/database/db_ppid.sql). 

Sekarang buka file ``.env`` di dalam folder proyek ppid (/**ppid/.env**) dan perbarui *field-field* berikut dengan informasi database baru;
```
DB_CONNECTION=mysql
DB_HOST=127.0.0.1
DB_PORT=3306
DB_DATABASE=nama_database_baru
DB_USERNAME=user_baru
DB_PASSWORD=password_baru
```

setelah itu, masih dalam file ``.env`` perbarui *field-field* dengan key [google recaptcha](https://www.google.com/recaptcha) :
```
RE_CAP_SITE=sitekey
RE_CAP_SECRET=secretkey
```

dan untuk setting email, bisa menggunakan [Mailtrap](https://mailtrap.io) atau [Gmail](https://learninglaravel.net/learn-to-send-emails-using-gmail-and-sendgrid-in-laravel-5) dan perbarui *field-field* berikut :
```
MAIL_DRIVER=smtp
MAIL_HOST=smtp.mailtrap.io
MAIL_PORT=2525
MAIL_USERNAME=username
MAIL_PASSWORD=secretpw
MAIL_ENCRYPTION=tls
```

You are ready for a new Laravel 5.4 application on shared hosting !!

Sumber : [Deploy Laravel Projects On Shared Hosting](https://medium.com/laravel-power-devs/deploy-laravel-projects-on-shared-hosting-2008be6f6f03)


# Deploy Proyek di VPS (Ubuntu 16.04) Nginx

## Step 1 (Update and Upgrade Packages)
Yang pertama untuk memastikan kita menggunakan package yang terbaru dan terupdate silahkan jalankan perintah berikut ini pada terminal :
```bash
apt-get update // mengupdate list package terbaru
apt-get upgrade // menginstall package yang sudah di update
```

## Step 2 (Install Nginx)
Untuk web server nya disini, gunakan web server nginx. Untuk menginstall nginx jalankan perintah berikut ini :
```bash
apt install nginx
```
Untuk mengetahui apakah nginx sudah terinstall atau belum, bisa melakukan perintah berikut untuk mengecek nya :
```bash
nginx -v
```

## Step 3 (Install PHP)
Karna server ini akan kita gunakan untuk project laravel maka kita perlu menginstall php. Install saja php dengan versi 7.2.
```bash
apt-get install python-software-properties
sudo add-apt-repository ppa:ondrej/php
apt-get update
apt install php7.2
```
Setelah itu, install module php yang dibutuhkan sesuai [requirement](https://laravel.com/docs/5.4#server-requirements) diantaranya: **OpenSSL PHP Extension, PDO PHP Extension, Mbstring PHP Extension, Tokenizer PHP Extension, XML PHP Extension**.
```bash
apt-get install php7.2-common php7.2-curl php7.2-mysql php7.2-gd php7.2-xml php7.2-xmlrpc php7.2-mbstring php7.2-cli php7.2-sqlite3 php7.2-zip
```

## Step 4 (Instal Composer)
Install composer dengan perintah berikut :
```bash
apt install composer
```

## Step 5 (Install MySQL)
Install MySQL dengan perintah berikut :
```bash
apt install mysql-server
```

Pada saat proses installasi maka nanti kita perlu mengisikan pasword untuk database kita maka silahkan isikan password sesuai dan mudah diingat.

## Step 6 (Install Git)
Disini untuk mengurusi depolyment kita akan menggunakan git sebagai tools nya. Untuk install git sialhakan jalankan perintah berikut ini :
```bash
apt install git
```

## Step 7 (Setting Direktori Project)
Ketik perintah dibawah untuk tempat project dari web yang akan dideploy
```bash
mkdir /server
cd server/
# Digunakan untuk project web kita
mkdir project
# Digunakan untuk menginstall phpmyadmin
mkdir phpmyadmin
# Digunakan untuk menyimpan configurasi nginx
mkdir nginx
```

### Install PHPMyAdmin
Agar mudah untuk manajemen administrasi database. Jalankan peritah berikut untuk menginstall PHPMyAdmin :
```
cd /server/phpmyadmin
git clone https://github.com/phpmyadmin/phpmyadmin
cd phpmyadmin
composer install
```
Jika terdapat error install beberapa extensi php berikut ini
```bash
apt install php7.2-mysqlnd
apt install php7.2-mbstring 
apt install php7.2-curl
apt install php7.2-zip
```

### Setup nginx config directory
Selanjutnya kita perlu mengatur folder configurasi nginx untuk web yang akan kita deploy 

```bash
cd /etc/nginx/
nano nginx.conf
```
Tambahkan ini dibawah Virtual Host Configs
```bash
# Web nginx config
include /server/nginx-config/*.conf;
```

Buat file configurasi untuk phpmyadminya, pertama masuk ke directory konfigurasi nginx nya.
```bash
cd /server/nginx-config/
```
Sekarang buat file nginx config untuk phpmyadmin dan simpan dengan nama file **phpmyadmin.conf**.
```bash
server {
    listen 8082;
    root /server/phpmyadmin/phpmyadmin;
    index index.php index.html index.htm;
    server_name localhost; # localhost bisa kamu ganti dengan nama domain web kamu
    location / {
        try_files $uri $uri/ /index.php?$query_string;
    }
    location ~ \.php$ {
        try_files $uri =404;
        fastcgi_split_path_info ^(.+\.php)(/.+)$;
        fastcgi_pass unix:/var/run/php/php7.2-fpm.sock;
        fastcgi_index index.php;
        fastcgi_param SCRIPT_FILENAME $document_root$fastcgi_script_name;
        include fastcgi_params;
    }
}
```
Restart service nginx dengan menjalankan perintah :
```bash
sudo service nginx restart
```
Dan coba buka phpmyadmin kita di browser apakah sudah berjalan atau belum. Jika berhasil maka akan muncul tampilan seperti ini. jangan lupa untuk membuka alamat ip kamu lalu di tambahkan port nya misalkan **ip:8082**
![image](https://user-images.githubusercontent.com/8111407/44644566-c95e7c00-a9fe-11e8-8c0e-f6bfe29ffa50.png)

### Create User MySQL (Optional)
Ketik perintah berikut untuk membuat user baru pada mysql :
```bash
# login ke mysql 
mysql -u root -p

# create user
create user 'USERNAMEKAMU'@'localhost' IDENTIFIED BY 'PASSWORDKAMU';
grant all privileges on *.* to 'USERNAMEKAMU'@'localhost' with grant option;
flush privileges;
```
​
### Buat database pada MySQL
Ketik perintah berikut untuk membuat database pada mysql :
```bash
# login ke mysql 
mysql -u root -p

# create database
create database db_ppid
```
​
### Clone Projek PPID
Setelah berhasil menyiapkan semuanya dari php, mysql dan nginx maka selanjutnya mencoba menjalankan projek pada server.
Pastikan lokasi direktori terminal ada pada path ```server/project```

```bash
# Clone project menggunakan git:
git clone https://git.gamatechno.net/gov/produk/website_ppid.git ppid
# Change directory to ppid
cd ppid
# Update package 
composer update
# Copy file .env.example
cp .env.example .env
# Generate key 
php artisan key:generate
# Beri permission untuk beberapa folder project nya
chmod -R 7777 storage boostrap/cache
# Migrasi struktur database dan inisiasi data
php artisan migrate:refresh --seed
```

### Konfigurasi Nginx (nginx-config)
```bash
server {
    listen 8081;
root /server/project/ppid/public;
index index.php index.html index.htm;
    server_name localhost; # localhost bisa kamu ganti dengan nama domain web kamu
location / {
        try_files $uri $uri/ /index.php?$query_string;
    }
location ~ \.php$ {
        try_files $uri =404;
        fastcgi_split_path_info ^(.+\.php)(/.+)$;
        fastcgi_pass unix:/var/run/php/php7.2-fpm.sock;
        fastcgi_index index.php;
        fastcgi_param SCRIPT_FILENAME $document_root$fastcgi_script_name;
        include fastcgi_params;
    }
}
```

Akses pada browser dengan alamat url **ipvps:8081**

You are ready for a new Laravel 5.4 application on vps !!

Sumber : [Cara Setting VPS Untuk Laravel](https://medium.com/@ocittwo/cara-setting-vps-untuk-laravel-939b5b89723d)


# Akun
Akses masuk : {base_url}/login

## Role Superadmin 
Username : superadmin
Email : superadmin@example.com
Password : superadmin

## Role PPID Pembantu
Username : birohukum
Email : birohukum@example.com
Password : 123456
