# Lapres Modul 2 Jarkom IT28
## Yoga Hartono - 5027211023
## Athallah Narda Wiyoga - 5027211041 

### Soal 1 Yudhistira akan digunakan sebagai DNS Master, Werkudara sebagai DNS Slave, Arjuna merupakan Load Balancer yang terdiri dari beberapa Web Server yaitu Prabakusuma, Abimanyu, dan Wisanggeni. Buatlah topologi dengan pembagian sebagai berikut.  
![image](https://github.com/yogahartono/Jarkom-Modul2-IT28-2023/assets/89679766/40b33a71-f6c4-463d-8a21-54eced1ad37e)


### Soal 2 Buatlah website utama pada node arjuna dengan akses ke arjuna.yyy.com dengan alias www.arjuna.yyy.com dengan it28 merupakan kode kelompok.


### Soal 3 Dengan cara yang sama seperti soal nomor 2, buatlah website utama dengan akses ke abimanyu.it28.com dan alias www.abimanyu.it28.com.


### Soal 4 Kemudian, karena terdapat beberapa web yang harus di-deploy, buatlah subdomain parikesit.abimanyu.it28.com yang diatur DNS-nya di Yudhistira dan mengarah ke Abimanyu.


### Soal 5 Buat juga reverse domain untuk domain utama. (Abimanyu saja yang direverse)


### Soal 6 Agar dapat tetap dihubungi ketika DNS Server Yudhistira bermasalah, buat juga Werkudara sebagai DNS Slave untuk domain utama.


### Soal 7 Seperti yang kita tahu karena banyak sekali informasi yang harus diterima, buatlah subdomain khusus untuk perang yaitu baratayuda.abimanyu.it28.com dengan alias www.baratayuda.abimanyu.it28.com yang didelegasikan dari Yudhistira ke Werkudara dengan IP menuju ke Abimanyu dalam folder Baratayuda.


### Soal 8 Untuk informasi yang lebih spesifik mengenai Ranjapan Baratayuda, buatlah subdomain melalui Werkudara dengan akses rjp.baratayuda.abimanyu.it28.com dengan alias www.rjp.baratayuda.abimanyu.it28.com yang mengarah ke Abimanyu.


### Soal 9 Arjuna merupakan suatu Load Balancer Nginx dengan tiga worker (yang juga menggunakan nginx sebagai webserver) yaitu Prabakusuma, Abimanyu, dan Wisanggeni. Lakukan deployment pada masing-masing worker.


### Soal 10 Kemudian gunakan algoritma Round Robin untuk Load Balancer pada Arjuna. Gunakan server_name pada soal nomor 1. Untuk melakukan pengecekan akses alamat web tersebut kemudian pastikan worker yang digunakan untuk menangani permintaan akan berganti ganti secara acak. Untuk webserver di masing-masing worker wajib berjalan di port 8001-8003.


### Soal 11 Selain menggunakan Nginx, lakukan konfigurasi Apache Web Server pada worker Abimanyu dengan web server www.abimanyu.it28.com. Pertama dibutuhkan web server dengan DocumentRoot pada /var/www/abimanyu.it28


### Soal 12 Setelah itu ubahlah agar url www.abimanyu.it28.com/index.php/home menjadi www.abimanyu.it28.com/home.


### Soal 13 Selain itu, pada subdomain www.parikesit.abimanyu.it28.com, DocumentRoot disimpan pada /var/www/parikesit.abimanyu.it28


### Soal 14 Pada subdomain tersebut folder /public hanya dapat melakukan directory listing sedangkan pada folder /secret tidak dapat diakses (403 Forbidden).


### Soal 15 Buatlah kustomisasi halaman error pada folder /error untuk mengganti error kode pada Apache. Error kode yang perlu diganti adalah 404 Not Found dan 403 Forbidden.


### Soal 16 Buatlah suatu konfigurasi virtual host agar file asset www.parikesit.abimanyu.it28.com/public/js menjadi www.parikesit.abimanyu.it28.com/js 


### Soal 17 Agar aman, buatlah konfigurasi agar www.rjp.baratayuda.abimanyu.it28.com hanya dapat diakses melalui port 14000 dan 14400.


### Soal 18 Untuk mengaksesnya buatlah autentikasi username berupa “Wayang” dan password “baratayudait28” dengan it28 merupakan kode kelompok. Letakkan DocumentRoot pada /var/www/rjp.baratayuda.abimanyu.it28.


### Soal 19 Buatlah agar setiap kali mengakses IP dari Abimanyu akan secara otomatis dialihkan ke www.abimanyu.it28.com (alias)


### Soal 20 Karena website www.parikesit.abimanyu.it28.com semakin banyak pengunjung dan banyak gambar gambar random, maka ubahlah request gambar yang memiliki substring “abimanyu” akan diarahkan menuju abimanyu.png.
