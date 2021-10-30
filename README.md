# Jarkom-Modul-2-T03-2021

### 1. Luffy adalah seorang yang akan jadi Raja Bajak Laut. Demi membuat Luffy menjadi Raja Bajak Laut, Nami ingin membuat sebuah peta, bantu Nami untuk membuat peta berikut:

![image](https://user-images.githubusercontent.com/73152464/139418741-f9bb772f-7983-4300-934a-99ae19cb839a.png)

EniesLobby akan dijadikan sebagai DNS Master, Water7 akan dijadikan DNS Slave, dan Skypie akan digunakan sebagai Web Server. Terdapat 2 Client yaitu Loguetown, dan Alabasta. Semua node terhubung pada router Foosha, sehingga dapat mengakses internet.
#### Berikut adalah topologi yang kami buat:

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

Pada client Loguetown dan Alabasta, kami melakukan konfigurasi berikut pada `/etc/resolv.conf` agar client dapat terhubung dengan Foosha, Ennieslobby, Water7, dan juga Skypie

### 2. Luffy ingin menghubungi Franky yang berada di EniesLobby dengan denden mushi. Kalian diminta Luffy untuk membuat website utama dengan mengakses franky.yyy.com dengan alias www.franky.yyy.com pada folder kaizoku.

Pertama adalah membaut folder `kaizoku` pada `etc/bind/kaizoku`

![image](https://user-images.githubusercontent.com/73152464/139478598-41eb570c-3697-42f8-bccc-9a5ae29f0468.png)

Di dalam folder `kaizoku`, 








### 14. Dan Luffy meminta untuk web www.general.mecha.franky.yyy.com hanya bisa diakses dengan port 15000 dan port 15500 

**Jawab:**
Ketika mengakses www.general.mecha.franky.T03.com tanpa port yang spesifik dengan perintah `lynx www.general.mecha.franky.T03.com` akan menghasilkan seperti gambar dibawah

![image](https://media.discordapp.net/attachments/858956223604850688/903888317551083550/unknown.png)

Namun apabila kita menambahkan port spesifik dengan perintah `lynx www.general.mecha.franky.T03.com:15000` maka akan menampilkan seperti dibawah. 

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


### (15) dengan autentikasi username luffy dan password onepiece dan file di /var/www/general.mecha.franky.yyy 

**Jawab:**
Masukkan username `luffy` dan password `onepiece` pada link `www.general.mecha.franky.T03.com`.

![image](https://media.discordapp.net/attachments/858956223604850688/903888524162506762/unknown.png)

Apabila berhasil memasukkan password maka akan menampilkan gambar dibawah.

[image](https://media.discordapp.net/attachments/858956223604850688/903888622690910258/unknown.png)

### (16)  Dan setiap kali mengakses IP Skypie akan dialihkan secara otomatis ke www.franky.yyy.com 


### (17). Dikarenakan Franky juga ingin mengajak temannya untuk dapat menghubunginya melalui website www.super.franky.yyy.com, dan dikarenakan pengunjung web server pasti akan bingung dengan randomnya images yang ada, maka Franky juga meminta untuk mengganti request gambar yang memiliki substring “franky” akan diarahkan menuju franky.png. Maka bantulah Luffy untuk membuat konfigurasi dns dan web server ini!
