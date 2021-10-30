# Jarkom-Modul-2-T03-2021

## Soal dan Penyelesaian
### 1. Luffy adalah seorang yang akan jadi Raja Bajak Laut. Demi membuat Luffy menjadi Raja Bajak Laut, Nami ingin membuat sebuah peta, bantu Nami untuk membuat peta berikut:

![image](https://user-images.githubusercontent.com/73152464/139418741-f9bb772f-7983-4300-934a-99ae19cb839a.png)

### EniesLobby akan dijadikan sebagai DNS Master, Water7 akan dijadikan DNS Slave, dan Skypie akan digunakan sebagai Web Server. Terdapat 2 Client yaitu Loguetown, dan Alabasta. Semua node terhubung pada router Foosha, sehingga dapat mengakses internet.

**Jawab:**

Berikut adalah topologi yang kami buat:

![image](https://user-images.githubusercontent.com/73152464/139419103-8a24e7ee-afa7-4a80-af66-e730e4bd3c6c.png)

Dengan konfigurasi Client sebagai berikut:
a. Loguetown

![image](https://user-images.githubusercontent.com/73152464/139419351-ac9c8da7-8728-40a0-8c3c-261ac9e8f8a4.png)

b. Alabasta

![image](https://user-images.githubusercontent.com/73152464/139419407-af15b1b3-45d1-469d-a99c-810ffd180cf5.png)

Konfigurasi DNS Server EnniesLobby:

![image](https://user-images.githubusercontent.com/73152464/139419496-6d816510-883b-497b-9d7c-39b96b6044c2.png)

Konfigurasi DNS Slave Water7:

![image](https://user-images.githubusercontent.com/73152464/139419596-a27780cc-35ee-4cd6-9180-7fd1f92bda53.png)

Konfigurasi Webserver Skypie:

![image](https://user-images.githubusercontent.com/73152464/139419657-80918168-70ca-4c29-9668-6972a3da42fe.png)

a. Pada client Loguetown dan Alabasta, kami melakukan konfigurasi berikut pada `/etc/resolv.conf` agar client dapat terhubung dengan Foosha, Ennieslobby, Water7, dan juga Skypie
```
nameserver 192.168.122.1
nameserver 10.43.2.2
nameserver 10.43.2.3
nameserver 10.43.2.4
```
Selain membuat konfigurasi untuk menghubungkan antar node, kami juga memjalankan beberapa command dasar untuk menyiapkan node client
```
apt-get update
apt-get install nano
apt-get install dnsutils
apt-get install lynx -y
```
b. Pada DNS Ennieslobby, konfigurasi pada `/etc/resolv.conf` kami hubungkan dengan router Foosha
``` nameserver 192.168.122.1 ```
Terdapat beberapa perintah dasar sebelum menjalankan DNS Ennieslobby, yang paling utama yaitu menginstall bind9
```
apt-get install nano
apt-get update
apt-get install bind9 -y
```
### 2. Luffy ingin menghubungi Franky yang berada di EniesLobby dengan denden mushi. Kalian diminta Luffy untuk membuat website utama dengan mengakses franky.yyy.com dengan alias www.franky.yyy.com pada folder kaizoku.

**Jawab:**

Pertama adalah membuat folder `kaizoku` pada `etc/bind/` dengan menggunakan perintah `mkdir etc/bind/kaizoku` dan mengcopy file db.local pada path `/etc/bind` ke dalam folder `etc/bind/kaizoku` lalu mengubah namanya menjadi `franky.T03.com`. Setelahnya kami mengonfigurasi kembali file tersebut dengan perintah `nano /etc/bind/kaizoku/franky.T03.com`. Konfigurasinya adalah sebagai berikut:

![image](https://user-images.githubusercontent.com/73152464/139528054-87c13b2a-c793-4112-b7b1-e3e83eaa2af1.png)

Setelah itu dicek melalui client Loguetown

![image](https://user-images.githubusercontent.com/73152464/139528182-abb20ab4-e3e6-4f65-a1ad-37b1ccccef18.png)

### 3. Setelah itu buat subdomain super.franky.yyy.com dengan alias www.super.franky.yyy.com yang diatur DNS nya di EniesLobby dan mengarah ke Skypie

**Jawab:**
Mengedit file `franky.T03.com` pada folder `/etc/bind/kaizoku` menjadi sebagai berikut, menambahkan subdomain `super.franky.T03.com`

![image](https://user-images.githubusercontent.com/73152464/139528356-2af3c7b5-d78b-4e3e-843a-8597500c8831.png)

### 4. Buat juga reverse domain untuk domain utama

**Jawab:**

Mengedit file `/etc/bind/named.conf.local` pada EniesLobby dan menambahkan reverse dari 3 byte awal dari IP 10.43.2.2 yaitu 2.43.10

![image](https://user-images.githubusercontent.com/73152464/139529457-b5cdf79f-f578-454b-b908-a75a78e4f99a.png)

Selanjutnya mengcopy file `db.local` pada path `/etc/bind` ke dalam folder `etc/bind/kaizoku` lalu mengubah namanya menjadi `2.43.10.in-addr.arpa` dan mengedit filenya seperti gambar berikut:

![image](https://user-images.githubusercontent.com/73152464/139529544-7bf59566-9b20-48fd-b96e-7312869f63fc.png)

Dicek dengan client Loguetown

![image](https://user-images.githubusercontent.com/73152464/139529581-58acffc9-278e-4ff5-bd42-d58af64fcb95.png)

### 5. Supaya tetap bisa menghubungi Franky jika server EniesLobby rusak, maka buat Water7 sebagai DNS Slave untuk domain utama

**Jawab:**

Mengedit file `/etc/bind/named.conf.local` pada Ennieslobby dan disesuaikan dengan syntax berikut, diarahkan ke DNS Slave Water7:

![image](https://user-images.githubusercontent.com/73152464/139529752-fa47539d-e9d1-4b37-be1c-a7ca1accf40f.png)

Lalu pada Water7, file `/etc/bind/named.conf.local` diedit dan IP master diarahkan ke EnniesLobby

![image](https://user-images.githubusercontent.com/73152464/139529782-576d26da-4d2e-43e9-afc5-538956ca6932.png)

Mencoba ping dari Loguetown

![image](https://user-images.githubusercontent.com/73152464/139529812-d04c3def-ffbf-4b09-8a31-7b6ecab9a015.png)

### 6. Setelah itu terdapat subdomain mecha.franky.yyy.com dengan alias www.mecha.franky.yyy.com yang didelegasikan dari EniesLobby ke Water7 dengan IP menuju ke Skypie dalam folder sunnygo














### 14. Dan Luffy meminta untuk web www.general.mecha.franky.yyy.com hanya bisa diakses dengan port 15000 dan port 15500 

**Jawab:**
Ketika mengakses www.general.mecha.franky.T03.com tanpa port yang spesifik dengan perintah `lynx http://www.general.mecha.franky.T03.com` akan menghasilkan seperti gambar dibawah

![image](https://media.discordapp.net/attachments/858956223604850688/903888317551083550/unknown.png)

Namun apabila kita menambahkan port spesifik dengan perintah `lynx http://www.general.mecha.franky.T03.com:15000` atau `lynx http://www.general.mecha.franky.T03.com:15500` maka akan menampilkan seperti dibawah. 

![image](https://media.discordapp.net/attachments/858956223604850688/903888524162506762/unknown.png)

**Langkah penyelesaian:**
Pertama kita menyiapkan folder `/var/www/general.mecha.franky.T03.com` kemudian download file zip yang sudah disediakan. 
```
mkdir /var/www/general.mecha.franky.T03.com

wget https://github.com/FeinardSlim/Praktikum-Modul-2-Jarkom/raw/main/general.mecha.franky.zip -P /var/www/general.mecha.franky.T03.com

unzip /var/www/general.mecha.franky.T03.com/general.mecha.franky.zip -d /var/www/general.mecha.franky.T03.com

mv /var/www/general.mecha.franky.T03.com/general.mecha.franky/* /var/www/general.mecha.franky.T03.com
```
Kedua menyiapkan file konfigurasi di `/etc/apache2/sites-available/general.mecha.franky.T03.com.conf` kemudian mengaktifkan file konfigurasi dengan perintah `a2ensite general.mecha.franky.T03.com.conf`.
```
Listen 15000
Listen 15500
<VirtualHost *:15000 *:15500>

        ServerAdmin webmaster@localhost
        DocumentRoot /var/www/general.mecha.franky.T03.com
        ServerName general.mecha.franky.T03.com
        ServerAlias www.general.mecha.franky.T03.com

        <Directory "/var/www/general.mecha.franky.T03.com">
                AuthType Basic
                AuthName "Restricted Content"
                AuthUserFile /var/www/general.mecha.franky.T03
                Require valid-user
        </Directory>

        <Directory /var/www/general.mecha.franky.T03.com>
                Options Indexes FollowSymLinks
                AllowOverride All
                Require all granted
        </Directory>

        ErrorLog ${APACHE_LOG_DIR}/error.log
        CustomLog ${APACHE_LOG_DIR}/access.log combined
</VirtualHost>
```
Ketiga membuat file htaccess di `/var/www/general.mecha.franky.T03.com/.htaccess`.
```
AuthType Basic
AuthName "Restricted Content"
AuthUserFile /var/www/general.mecha.franky.T03
Require valid-user
```


### 15. dengan autentikasi username luffy dan password onepiece dan file di /var/www/general.mecha.franky.yyy 

**Jawab:**
Masukkan username `luffy` dan password `onepiece` pada link `http://www.general.mecha.franky.T03.com:15000` atau `http://www.general.mecha.franky.T03.com:15500`.

![image](https://media.discordapp.net/attachments/858956223604850688/903888524162506762/unknown.png)

Apabila berhasil memasukkan password maka akan menampilkan gambar dibawah.

![image](https://media.discordapp.net/attachments/858956223604850688/903888622690910258/unknown.png)

**Langkah penyelesaian:**
Membuat file htpasswd di `/var/www/general.mecha.franky.T03` dengan perintah berikut
```
htpasswd -cb /var/www/general.mecha.franky.T03 luffy onepiece
```

### 16.  Dan setiap kali mengakses IP Skypie akan dialihkan secara otomatis ke www.franky.yyy.com 

**Jawab:**
Apabila kita mengakses IP Skypie maka akan langsung dialihkan ke www.franky.T03.com dapat dilihat pada gambar dibawah.
![image](https://media.discordapp.net/attachments/858956223604850688/903898328046129152/unknown.png)

![image](https://media.discordapp.net/attachments/858956223604850688/903898407238787122/unknown.png)

**Langkah penyelesaian:**
Dengan menambah htaccess di `/var/www/franky.T03`

### 17. Dikarenakan Franky juga ingin mengajak temannya untuk dapat menghubunginya melalui website www.super.franky.yyy.com, dan dikarenakan pengunjung web server pasti akan bingung dengan randomnya images yang ada, maka Franky juga meminta untuk mengganti request gambar yang memiliki substring “franky” akan diarahkan menuju franky.png. Maka bantulah Luffy untuk membuat konfigurasi dns dan web server ini!

**Jawab:**
Bila kita mengakses gambar yang mengandung nama `franky` selain franky.png di http://www.super.franky.T03.com/public/images maka akan langsung dialihkan ke gambar franky.png. Pada contoh gambar kita mengakses ke gambar not-franky.jpg

![image](https://media.discordapp.net/attachments/858956223604850688/903899223597129768/unknown.png)

![image](https://media.discordapp.net/attachments/858956223604850688/903899328664449084/unknown.png)

Maka akan langsung dialihkan ke franky.png
![image](https://media.discordapp.net/attachments/858956223604850688/903899387447607376/unknown.png)

**Langkah penyelesaian:**
Dengan menambahkan perintah tambahan pada `/var/www/super.franky.T03.com/.htaccess` seperti berikut
```
RewriteEngine On
RewriteCond %{REQUEST_URI} ^/public/images/(.*)franky(.*)
RewriteCond %{REQUEST_URI} !/public/images/franky.png
RewriteRule .* http://super.franky.T03.com/public/images/franky.png [L]
```

## Kendala
1. Masih baru pertama mengoperasikan GNS3 sehingga saat sudah mengerjakan soal shift dan lupa bahwa semua yang sudah ada tidak tersimpan terasa sangat menyayat hati. Ternyata harus disimpan di file bash sehingga tinggal jalankan file bash tersebut.
