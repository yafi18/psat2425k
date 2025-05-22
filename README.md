# cara deploy aplikasi psat2425 menurut saya hehe 😊👍

bismillah dahulu

# langkah langkah 👍

1. unduh repo dari atau file zipnya https://github.com/paknux/psat2425 kemudian kita ekstrak
2. buka vscode buka folder psat2425 kemudian edit readme.md ini tutornya
3. kemudian masuk ke akun github kalian buat repositori baru dengan nama psat2425 terus kalian push file download tadi di vscode
4. jika sudah kalian pergi ke akun aws kalian terus pergi ke moduls terus luncurkan aws terus cari RDS pergi ke database lalu buat database,kalian bisa gunakan security groups yang serverDB dan serverWeb jika belum kalian bisa buat security grupnya seperti langkah ini

# Buat security group SG-ServerDB

allow inbound MySQL (3306) from anywhereIPv4 (0.0.0.0/0)

# Buat security group SG-ServerWeb

allow inbound SSH (22) from anywhereIPv4 (0.0.0.0/0)  
 allow inbound HTTP (80) from anywhereIPv4 (0.0.0.0/0)  
 allow inbound HTTPS (443) from anywhereIPv4 (0.0.0.0/0)

untuk security groups ada di vpc kalian bisa cari dan buat disitu

5. jika sudah buat SG(security groups) kalian bisa lanjut buat databasenya
   # buat database
   1. kalian pilih yang standard aja lalu pilih yang mysql
   2. untuk templates nya pilih yang free tier lalu DB cluster identifier= ini bebas namannya apa aja
   3. kemdian untuk Master Username : (biarkan admin ) Master Password : isi misal P4ssw0rdd untuk public akses = no ya masa db dapat diakses publik
   4. Untuk Security group pastikan buat/pilih yang accept port inbound 3306 dari 0.0.0.0/0 (SG-ServerDB)
   5. Klik Create Database
   6. Tunggu sampai EndPoint muncul, bisa dicek dengan MySQL client (MySQLFront, HeidiSQL)
   7. Buat Database dan tabel jika diperlukan dengan MySQL Client kita

6. buat instance,oergi ke EC2 pilih yg instance kemudian buat 
   # cara membuat instance 
   1. kalian buat namanaya sesuai yg kalian inginkan 
   2. terus pilih yang ubuntu terus pilih yg nano atau micro terserah 
   3. nah untuk key pair pilih yg vockey
   4. nah untuk SG kalian pilih yg Select existing security group dan pilih yang SGserverWeb
   5. terus tiggal kta buat selesai 

7. jika database dan instancenya sudah tinggal kita konek ke instancenya
8. kalian klik instance tersebut kemudian pilih connect terus pilih connect lagi 
9. jika sudah kalian akan masuk ke ubuntu servernya nah di ubuntu ini kalian tinnggal masukan bash scriptingnya seperti ini

# bash scripting

sudo apt update -y

sudo apt install -y apache2 php php-mysql libapache2-mod-php mysql-client

sudo rm -rf /var/www/html/{,.}

sudo git clone https://github.com/paknux/crudsiswa.git /var/www/html >> nah ini githubnya ganti punya kita yang sudah kita push ya 

sudo chmod -R 777 /var/www/html

echo DB_USER=admin > /var/www/html/.env >> biarkan admin
echo DB_PASS=P4ssw0rd123  >> /var/www/html/.env >> ini kita masukan passwondr seperti di database
echo DB_NAME=crudsiswa  >> /var/www/html/.env >> ini nama database kalian
echo DB_HOST=rds11tjkt1.czt6n8ylfvyb.us-east-1.rds.amazonaws.com >> /var/www/html/.env >> nah in endpoint database kalian

sudo apt install openssl
sudo a2enmod ssl
sudo a2ensite default-ssl.conf
sudo systemctl reload apache2

10. jika sudah kalian bisa salin ip publick yg di bawah tempel ke browser terus masukan sandi apk nya yaitu user admin passwordnya 123
11. jika sudah kalian bisa tambahkan data kalian atau edit data kalian selesai 


# sekian tutorial dari saya 😊✔

