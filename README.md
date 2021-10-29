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




