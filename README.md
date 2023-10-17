# Lapres Modul 2 Jarkom IT28
## Yoga Hartono - 5027211023
## Athallah Narda Wiyoga - 5027211041 

### Soal 1 Yudhistira akan digunakan sebagai DNS Master, Werkudara sebagai DNS Slave, Arjuna merupakan Load Balancer yang terdiri dari beberapa Web Server yaitu Prabakusuma, Abimanyu, dan Wisanggeni. Buatlah topologi dengan pembagian sebagai berikut.
![image](https://github.com/yogahartono/Jarkom-Modul2-IT28-2023/assets/89679766/40b33a71-f6c4-463d-8a21-54eced1ad37e)


### Soal 2 Buatlah website utama pada node arjuna dengan akses ke arjuna.yyy.com dengan alias www.arjuna.yyy.com dengan it28 merupakan kode kelompok.
Skrip "makeArjuna.sh" dijalankan pada node YudhistiraDNSMaster untuk melakukan berbagai tugas, termasuk menambahkan domain "arjuna.it28.com" ke file "/etc/bind/named.conf.local", mengarahkan alamat IP-nya ke node ArjunaLoadBalancer, dan menambahkan catatan CNAME untuk membuat alias website. Kemudian, perintah di bawah ini digunakan dalam pengetesan:

1. Melakukan ping ke "arjuna.it28.com" sebanyak 2 kali dengan perintah "ping arjuna.it28.com -c 2".
2. Menggunakan perintah "host -t CNAME www.arjuna.it28.com" untuk mengecek informasi CNAME terkait "www.arjuna.it28.com".
3. Melakukan ping ke "www.arjuna.it28.com" sebanyak 2 kali dengan perintah "ping www.arjuna.it28.com -c 2".

### Soal 3 Dengan cara yang sama seperti soal nomor 2, buatlah website utama dengan akses ke abimanyu.it28.com dan alias www.abimanyu.it28.com.
Skrip "makeAbimanyu.sh" dijalankan pada node YudhistiraDNSMaster untuk melakukan berbagai tugas, termasuk menambahkan domain "abimanyu.it28.com" ke file "/etc/bind/named.conf.local", mengarahkan alamat IP-nya ke node AbimanyuWebServer, dan menambahkan catatan CNAME untuk membuat alias website. Kemudian, perintah di bawah ini digunakan dalam pengetesan:

1. Melakukan ping ke "abimanyu.it28.com" sebanyak 2 kali dengan perintah "ping abimanyu.it28.com -c 2".
2. Menggunakan perintah "host -t CNAME www.abimanyu.it28.com" untuk mengecek informasi CNAME terkait "www.abimanyu.it28.com".
3. Melakukan ping ke "www.abimanyu.it28.com" sebanyak 2 kali dengan perintah "ping www.abimanyu.it28.com -c 2".

### Soal 4 Kemudian, karena terdapat beberapa web yang harus di-deploy, buatlah subdomain parikesit.abimanyu.it28.com yang diatur DNS-nya di Yudhistira dan mengarah ke Abimanyu.
Skrip "makeParikesit.sh" dijalankan pada node YudhistiraDNSMaster untuk menambahkan catatan A pada file domain "abimanyu.it28.com" guna membuat subdomain untuk sebuah website. Kemudian, dalam pengetesan, digunakan perintah berikut:

1. Menggunakan perintah "host -t A parikesit.abimanyu.it28.com" untuk mengecek informasi mengenai catatan A terkait subdomain "parikesit.abimanyu.it28.com".
2. Melakukan ping ke "parikesit.abimanyu.it28.com" sebanyak 2 kali dengan perintah "ping parikesit.abimanyu.it28.com -c 2".

### Soal 5 Buat juga reverse domain untuk domain utama. (Abimanyu saja yang direverse)
Skrip "makeReverse.sh" dijalankan pada node YudhistiraDNSMaster untuk menambahkan domain "reverse 3.247.192.in-addr.arpa" ke file "/etc/bind/named.conf.local" dan dalam file domain tersebut membuat catatan nameserver yang mengarahkan ke "abimanyu.it28.com". Kemudian, dalam pengetesan, digunakan perintah berikut:

Menggunakan perintah "host -t PTR 192.247.3." untuk mengecek catatan PTR (Pointer Record) yang terkait dengan alamat IP "192.247.3.".

### Soal 6 Agar dapat tetap dihubungi ketika DNS Server Yudhistira bermasalah, buat juga Werkudara sebagai DNS Slave untuk domain utama.
Dalam proses pengaturan DNS, skrip "makeMaster.sh" yang dieksekusi di node YudhistiraDNSMaster menambahkan konfigurasi berupa baris "also-notify" dan "allow-transfer" di dalam file "/etc/bind/named.conf.local" yang mengarahkan ke alamat IP WerkudaraDNSSlave pada setiap domain yang terdaftar, termasuk domain reverse DNS.

Sementara itu, skrip "makeSlave.sh" yang dijalankan di node WerkudaraDNSSlave juga mengubah konfigurasi di file "/etc/bind/named.conf.local" dengan menambahkan baris "masters" yang mengarahkan ke alamat IP YudhistiraDNSMaster pada tiap domain yang terdaftar, termasuk reverse DNS.

Dalam pengujian, langkah-langkah yang diambil melibatkan:

1. Mematikan node YudhistiraDNSMaster.
2. Menjalankan perintah apapun (contohnya: "ping arjuna.it28.com -c 2").
3. Hal ini menggambarkan bagaimana konfigurasi Master-Slave DNS dilakukan di antara node YudhistiraDNSMaster dan WerkudaraDNSSlave, serta menguji stabilitas dan kinerja konfigurasi DNS tersebut saat node Master dimatikan.

### Soal 7 Seperti yang kita tahu karena banyak sekali informasi yang harus diterima, buatlah subdomain khusus untuk perang yaitu baratayuda.abimanyu.it28.com dengan alias www.baratayuda.abimanyu.it28.com yang didelegasikan dari Yudhistira ke Werkudara dengan IP menuju ke Abimanyu dalam folder Baratayuda.
Skrip "makeDelegator.sh" yang dijalankan di node YudhistiraDNSMaster digunakan untuk melakukan beberapa tugas, termasuk menambahkan catatan A dengan nama root "ns1" dan catatan NS dengan nama root "baratayuda" pada domain "abimanyu.it28.com". Selain itu, juga menambahkan konfigurasi tertentu pada file "/etc/bind/named.conf.options", seperti menutup kode "dnssec-validation auto;" dan menambahkan kode "allow-query { any; };".

Skrip "makeDelegate.sh" yang dijalankan di node WerkudaraDNSSlave digunakan untuk menambahkan konfigurasi yang serupa pada file "/etc/bind/named.conf.options", yaitu menutup kode "dnssec-validation auto;" dan menambahkan kode "allow-query { any; };". Selain itu, skrip ini juga menambahkan domain "baratayuda.abimanyu.it28.com" ke dalam file "/etc/bind/named.conf.local" dan membuat catatan CNAME untuk membuat alias website.

Dalam pengujian, digunakan perintah-perintah berikut:

1. Melakukan ping ke "baratayuda.abimanyu.it28.com" sebanyak 2 kali dengan perintah "ping baratayuda.abimanyu.it28.com -c 2".
2. Menggunakan perintah "host -t CNAME www.baratayuda.abimanyu.it28.com" untuk mengecek informasi mengenai catatan CNAME terkait "www.baratayuda.abimanyu.it28.com".
3. Melakukan ping ke "www.baratayuda.abimanyu.it28.com" sebanyak 2 kali dengan perintah "ping www.baratayuda.abimanyu.it28.com -c 2".

### Soal 8 Untuk informasi yang lebih spesifik mengenai Ranjapan Baratayuda, buatlah subdomain melalui Werkudara dengan akses rjp.baratayuda.abimanyu.it28.com dengan alias www.rjp.baratayuda.abimanyu.it28.com yang mengarah ke Abimanyu.
Skrip "makeRjp.sh" yang dijalankan pada node WerkudaraDNSSlave digunakan untuk melakukan berbagai tugas, termasuk menambahkan catatan A pada file domain "baratayuda.abimanyu.it28.com" untuk membuat subdomain suatu website dan juga menambahkan catatan CNAME untuk membuat alias website. Kemudian, dalam pengetesan, digunakan perintah berikut:

1. Melakukan ping ke "rjp.baratayuda.abimanyu.it28.com" sebanyak 2 kali dengan perintah "ping rjp.baratayuda.abimanyu.it28.com -c 2".
2. Melakukan ping ke "www.rjp.baratayuda.abimanyu.it28.com" sebanyak 2 kali dengan perintah "ping www.rjp.baratayuda.abimanyu.it28.com -c 2".

### Soal 9 Arjuna merupakan suatu Load Balancer Nginx dengan tiga worker (yang juga menggunakan nginx sebagai webserver) yaitu Prabakusuma, Abimanyu, dan Wisanggeni. Lakukan deployment pada masing-masing worker.
Pada setiap worker, digunakan skrip "makeWorker.sh" yang berisi perintah-perintah sebagai berikut:

1. Melakukan instalasi Nginx dan PHP.
2. Mengunduh dan memproses file sumber daya (resource) yang diperlukan untuk worker.
3. Mengkonfigurasi port pada baris "listen 800x;" sesuai dengan port tempat worker tersebut berjalan.

Dalam pengujian, digunakan perintah "nginx -t" untuk memeriksa kebenaran konfigurasi Nginx.

### Soal 10 Kemudian gunakan algoritma Round Robin untuk Load Balancer pada Arjuna. Gunakan server_name pada soal nomor 1. Untuk melakukan pengecekan akses alamat web tersebut kemudian pastikan worker yang digunakan untuk menangani permintaan akan berganti ganti secara acak. Untuk webserver di masing-masing worker wajib berjalan di port 8001-8003.
Skrip "makeLB.sh" yang dijalankan pada node ArjunaLoadBalancer digunakan untuk mengkonfigurasi penyeimbang beban dalam file "/etc/nginx/sites-available/lb-arjuna" dengan algoritma Round Robin. Konfigurasi tersebut mencantumkan server-server yang ada, sesuai dengan worker yang tersedia, seperti:

```nginx
upstream myweb  {
    server 192.247.3.2:8001; #IP PrabukusumaWebServer
    server 192.247.3.3:8002; #IP AbimanyuWebServer
    server 192.247.3.4:8003; #IP WisanggeniWebServer
}
```

Dalam pengujian, digunakan perintah "lynx arjuna.it28.com" untuk mengakses situs web arjuna.it28.com menggunakan perutean yang dikonfigurasi oleh penyeimbang beban, yang dalam hal ini adalah algoritma Round Robin.

### Soal 11 Selain menggunakan Nginx, lakukan konfigurasi Apache Web Server pada worker Abimanyu dengan web server www.abimanyu.it28.com. Pertama dibutuhkan web server dengan DocumentRoot pada /var/www/abimanyu.it28
Untuk mengkonfigurasi www.abimanyu.it28.com, digunakan skrip "abimanyuConf.sh" dengan langkah-langkah sebagai berikut:

1. Melakukan salinan konfigurasi default Apache (file "000-default.conf") dari folder "/etc/apache2/sites-available" dengan nama file "abimanyu.it28.conf" menggunakan perintah "cp".
2. Mengunduh sumber daya dari Google Drive dan mengekstraknya ke folder "/var/www/abimanyu.it28" sebagai direktori root dokumen menggunakan perintah "wget" dan "unzip".
3. Membuat konfigurasi VirtualHost dengan parameter "DocumentRoot /var/www/abimanyu.it28", "ServerName abimanyu.it28.com", dan "ServerAlias www.abimanyu.it28.com", menyimpannya dalam variabel "conf", dan menulisnya ke file "abimanyu.it28.conf".
4. Mengaktifkan konfigurasi dengan perintah "a2ensite abimanyu.it28".
5. Merestart layanan server web Apache2 dengan perintah "service apache2 restart".

### Soal 13 Selain itu, pada subdomain www.parikesit.abimanyu.it28.com, DocumentRoot disimpan pada /var/www/parikesit.abimanyu.it28
Dalam rangka mengonfigurasi www.parikesit.abimanyu.it28.com, digunakan skrip "parikesitConf.sh" dengan urutan tindakan berikut:

1. Membuat salinan dari konfigurasi default Apache (file "000-default.conf") yang berada dalam folder "/etc/apache2/sites-available" dan memberikan nama file "parikesit.abimanyu.it28.conf" dalam folder yang sama dengan menggunakan perintah "cp".
2. Mengunduh sumber daya dari Google Drive dan mengekstraknya ke folder "/var/www/parikesit.abimanyu.it28" sebagai direktori root dokumen dengan perintah "wget" dan "unzip".
3. Membuat direktori "/secret" di dalam folder "/var/www/parikesit.abimanyu.it28" dengan perintah "mkdir".
4. Membuat konfigurasi VirtualHost dengan parameter "DocumentRoot /var/www/parikesit.abimanyu.it28", "ServerName parikesit.abimanyu.it28.com", dan "ServerAlias www.parikesit.abimanyu.it28.com", menyimpannya dalam variabel "conf", dan menulisnya ke file "parikesit.abimanyu.it28.conf".
5. Mengaktifkan konfigurasi menggunakan perintah "a2ensite parikesit.abimanyu.it28".
6. Merestart layanan server web Apache2 dengan perintah "service apache2 restart".
7. Untuk melakukan pengujian, mengakses situs web dengan perintah "lynx parikesit.abimanyu.it28.com" dari klien.

### Soal 14 Pada subdomain tersebut folder /public hanya dapat melakukan directory listing sedangkan pada folder /secret tidak dapat diakses (403 Forbidden).
Untuk mengaktifkan listing direktori (directory listing) pada folder "public" dan membatasi akses pada folder "secret," Anda dapat menambahkan konfigurasi berikut ke dalam file konfigurasi VirtualHost "parikesit.abimanyu.it28.conf":

```apache
<Directory /var/www/parikesit.abimanyu.it28/public>
	Options +Indexes
</Directory>

<Directory /var/www/parikesit.abimanyu.it28/secret>
	Options -Indexes
</Directory>
```

Setelah menambahkan konfigurasi ini, Anda perlu me-restart layanan Apache2 untuk membuat perubahan tersebut aktif. Selanjutnya, Anda dapat melakukan pengujian dengan mengakses folder "public" dan "secret" dari klien.

### Soal 15 Buatlah kustomisasi halaman error pada folder /error untuk mengganti error kode pada Apache. Error kode yang perlu diganti adalah 404 Not Found dan 403 Forbidden.
Dalam konteks ini, halaman error yang ditampilkan akan diubah dengan menggunakan file HTML yang terdapat dalam folder "/error." Perubahan tersebut dapat diimplementasikan dengan menambahkan konfigurasi berikut ke dalam file konfigurasi VirtualHost "parikesit.abimanyu.it28.conf":

```apache
ErrorDocument 403 /error/403.html
ErrorDocument 404 /error/404.html
```

Setelah menambahkan konfigurasi ini, Anda perlu me-restart layanan Apache2 agar perubahan tersebut aktif. Selanjutnya, untuk melakukan pengujian, Anda dapat mencoba mengakses "parikesit.abimanyu.it28.com/secret" untuk menguji error 403, dan "parikesit.abimanyu.it28.com/yyy" untuk menguji error 404.

### Soal 16 Buatlah suatu konfigurasi virtual host agar file asset www.parikesit.abimanyu.it28.com/public/js menjadi www.parikesit.abimanyu.it28.com/js 
Anda dapat membuat direktori alias "www.parikesit.abimanyu.yyy.com/js" dengan menambahkan baris berikut ke dalam konfigurasi VirtualHost pada file "parikesit.abimanyu.it28.conf":

```apache
Alias /js /var/www/parikesit.abimanyu.it28/public/js
```

Untuk mengaktifkan konfigurasi yang baru, Anda perlu me-restart layanan Apache2. Setelah itu, Anda dapat melakukan pengujian dengan mengakses "parikesit.abimanyu.it28.com/public/js" dan "parikesit.abimanyu.it28.com/js".

### Soal 17 Agar aman, buatlah konfigurasi agar www.rjp.baratayuda.abimanyu.it28.com hanya dapat diakses melalui port 14000 dan 14400.
Untuk mengkonfigurasi "rjp.baratayuda.abimanyu.it28.com", langkah-langkahnya adalah sebagai berikut:

1. Salin konfigurasi default Apache (file "000-default.conf") dari folder "/etc/apache2/sites-available" dengan nama file "rjp.baratayuda.abimanyu.it28.conf" ke folder yang sama menggunakan perintah "cp".
2. Unduh sumber daya dari Google Drive dan ekstrak ke folder "/var/www/abimanyu.it28" sebagai direktori root dokumen dengan perintah "wget" dan "unzip".
3. Buat konfigurasi VirtualHost dengan parameter "DocumentRoot /var/www/abimanyu.it28", "ServerName abimanyu.it28.com", dan "ServerAlias www.abimanyu.it28.com", simpan dalam variabel "conf", dan tulis ke file "abimanyu.it28.conf".
4. Dalam konfigurasi VirtualHost, tetapkan agar port hanya dapat diakses pada port 14000 dan 14400 dengan "<VirtualHost *:14000 *:14400>".
5. Ubah konfigurasi port pada file "/etc/apache2/ports.conf" dengan menambahkan "Listen 14000" dan "Listen 14400".
6. Aktifkan konfigurasi menggunakan perintah "a2ensite rjp.baratayuda.abimanyu.it28".
7. Merestart layanan server web Apache2 dengan perintah "service apache2 restart".
8. Untuk melakukan pengujian, mencoba mengakses "rjp.baratayuda.abimanyu.it28.com", "rjp.baratayuda.abimanyu.it28.com:14000", dan "rjp.baratayuda.abimanyu.it28.com:14400".

### Soal 18 Untuk mengaksesnya buatlah autentikasi username berupa “Wayang” dan password “baratayudait28” dengan it28 merupakan kode kelompok. Letakkan DocumentRoot pada /var/www/rjp.baratayuda.abimanyu.it28.
Untuk menambahkan autentikasi pada "rjp.baratayuda.abimanyu.it28.com", langkah-langkahnya adalah sebagai berikut:

1. Membuat username "wayang" dan password yang disimpan dalam file "/etc/apache2/.htpasswd" dengan menggunakan perintah "echo "baratayudait28" | htpasswd -ci /etc/apache2/.htpasswd Wayang".
2. Mengaktifkan mode autentikasi dengan perintah "a2enmod auth_basic" dan "a2enmod authn_file".
3. Menambahkan konfigurasi berikut ke dalam file konfigurasi VirtualHost "rjp.baratayuda.abimanyu.it28.conf":

```apache
<Directory /var/www/rjp.baratayuda.abimanyu.it28>
	AuthType Basic
	AuthName "Private Area"
	AuthUserFile /etc/apache2/.htpasswd
	Require valid-user
</Directory>
```

4. Merestart layanan server web Apache2 dengan perintah "service apache2 restart".
5. Untuk melakukan pengujian, mencoba mengakses "rjp.baratayuda.abimanyu.it28.com," yang kemudian akan meminta username dan password.

### Soal 19 Buatlah agar setiap kali mengakses IP dari Abimanyu akan secara otomatis dialihkan ke www.abimanyu.it28.com (alias)
Akses melalui alamat IP akan mengikuti konfigurasi default, sehingga pengalihan ke "abimanyu.it28.com" dapat dicapai dengan mengubah konfigurasi default sebagai berikut:

```apache
<VirtualHost *:80>
    ServerAdmin webmaster@localhost
    DocumentRoot /var/www/abimanyu.it28
    ServerName abimanyu.it28.com

    ErrorLog \${APACHE_LOG_DIR}/error.log
    CustomLog \${APACHE_LOG_DIR}/access.log combined
</VirtualHost>
```

Untuk melakukan pengujian, menjalankan "lynx 192.247.3.3/home.html" pada klien.

### Soal 20 Karena website www.parikesit.abimanyu.it28.com semakin banyak pengunjung dan banyak gambar gambar random, maka ubahlah request gambar yang memiliki substring “abimanyu” akan diarahkan menuju abimanyu.png.
Untuk mengalihkan permintaan (request) gambar ke "abimanyu.png", langkah-langkahnya adalah sebagai berikut:

1. Tambahkan konfigurasi berikut ke dalam file konfigurasi VirtualHost "parikesit.abimanyu.it28.conf":

```apache
<Directory /var/www/parikesit.abimanyu.it28>
	Options +FollowSymLinks -Multiviews
	AllowOverride All
</Directory>
```

2. Buat file ".htaccess" dalam folder "/var/www/parikesit.abimanyu.it28".

3. Aktifkan mesin perubahan (rewrite engine) dengan menambahkan "RewriteEngine On" ke dalam file ".htaccess".

4. Tambahkan kondisi perubahan untuk memilih permintaan yang akan diubah. Permintaan yang memenuhi kondisi adalah yang mengandung "abimanyu," yang memiliki ekstensi "jpeg, jpg, png, atau gif," dan bukan merupakan permintaan untuk "abimanyu.png." Kondisi ini dapat diimplementasikan dengan menambahkan kode berikut ke dalam file ".htaccess":

```apache
RewriteCond %{REQUEST_URI} abimanyu [NC]
RewriteCond %{REQUEST_URI} \.(jpg|jpeg|png|gif)$ [NC]
RewriteCond %{REQUEST_URI} !/public/images/abimanyu.png
```

5. Arahkan permintaan yang memenuhi semua kondisi di atas dengan menambahkan "RewriteRule ^(.*)$ /public/images/abimanyu.png [R=301,L]" ke dalam file ".htaccess".

6. Untuk melakukan pengujian, coba mengakses "abimanyu-student.jpg" dan "notabimanyujustmuseum.177013".
