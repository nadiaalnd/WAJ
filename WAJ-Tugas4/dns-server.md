<div align="center">
  <h1 style="text-align: center;font-weight: bold">Praktikum 4<br>Instalasi DNS Server</h1>
  <h4 style="text-align: center;">Dosen Pengampu : Dr. Ferry Astika Saputra, S.T., M.Sc.</h4>
</div>
<br />
<div align="center">
  <img src="https://upload.wikimedia.org/wikipedia/id/4/44/Logo_PENS.png" alt="Logo PENS">
  <h3 style="text-align: center;">Disusun Oleh : </h3>
  <p style="text-align: center;">
    <strong>Nadila Aulya Salsabila Mirdianti</strong><br>
    <strong>3122500002</strong>
  </p>

<h3 style="text-align: center;line-height: 1.5">Politeknik Elektronika Negeri Surabaya<br>Departemen Teknik Informatika Dan Komputer<br>Program Studi Teknik Informatika<br>2023/2024</h3>
  <hr>
</div>

## Daftar Isi

- [Daftar Isi](#daftar-isi)
    - [A. Apa itu DNS Server?](#1-apa-itu-dns)
    - [B. Langkah Langkah](#2-langkah-langkah)


### A. Apa itu DNS?
**Pengertian DNS**

![Gambar DNS Server](images/dns.webp)
<p style="text-align:justify">
DNS adalah sebuah sistem yang menghubugkan Uniform Resource Locator (URL) dengan Internet Protocol Address atau IP Address. Kepanjangan dari DNS adalah Domain Name System.
<br>
Dalam sejarah domain tercatat, awalnya kita perlu mengetikkan IP Address untuk mengakses sebuah website. Cara ini cukup merepotkan.
<br>
Maka, ini artinya kita perlu punya daftar IP Address dari semua website yang ingin kita kunjungi dan memasukkannya secara manual. Tentu saja ini tidak efisien.
<br> 
DNS adalah sistem yang memungkinkan kita untuk mengakses website dengan mengetikkan URL. DNS akan menghubungkan URL tersebut dengan IP Address yang sesuai.
</p>

### B. Langkah Langkah
Berikut adalah langkah-lang untuk instalasi DNS sever menggunakan BIND9 pada Debian 12:

#### 1. Konfigurasi file [named.conf](./bind9/named.conf)
lakukan configurasi pada file /etc/bind/named.conf dengan meggunakan perintah: `sudo nano /etc/bind/named.conf`
<br>
(Lihat file [named.conf](./bind9/named.conf))

<div align="center">
    <img src="images/dns1.jpg" alt="Config file named.conf" width="60%" height="auto"><br>
    <img src="images/dns1.1.jpg" alt="">
</div><br>

#### 2. Konfigurasi file [named.conf.local](./bind9/named.conf.local)
Lakukan configurasi pada file /etc/bind/named.conf.local dengan menggunakan perintah: `sudo nano /etc/bind/named.conf.local`
<br>
(Lihat file [named.conf.local](./bind9/named.conf.local))

<div align="center">
    <img src="images/dns2.jpg" alt="Config file named.conf.local" width="60%" height="auto"><br>
</div><br>

File `named.conf.local` mengatur zona-zona DNS lokal. Dalam konfigurasi ini, ada dua zona yang didefinisikan: "kelompok3.local" dan "3.168.192.in-addr.arpa". Server ditetapkan sebagai master untuk kedua zona tersebut. Informasi DNS disimpan dalam file database yang sesuai, dan konfigurasi juga memungkinkan pembaruan dinamis menggunakan kunci yang sesuai.


#### 3. Konfigurasi file [named.conf.option](./bind9/named.conf.options)
Lakukan configurasi pada file /etc/bind/[named.conf.option](./bind9/named.conf.options) dengan menggunakan perintah: `sudo nano /etc/bind/named.conf.options`

<div align="center">
    <img src="images/dns3.jpg" alt="Config file named.conf.options" width="60%" height="auto"><br>
</div><br>

#### 4. Pengecekan Konfigurasi pada file [named.conf](./bind9/named.conf)
Lakukan pengecekan konfigurasi dengan menggunakan perintah: `sudo named-checkconf /etc/bind/named.conf`

<div align="center">
    <img src="images/dns4.jpg" alt="pengecekan config" width="60%" height="auto"><br>
</div><br>

#### 5. Buat file [db.kelompok3.local](./bind9/db.kelompok3.local)
Buat file zone /var/lib/bind/db.kelompok3.local yang digunakan untuk domain, dengan menggunakan perintah: `sudo nano /var/lib/bind/db.kelompok3.local`
<br>
(Lihat file [db.kelompok3.local](./bind9/db.kelompok3.local))

<div align="center">
    <img src="images/dns5.jpg" alt="Buat file db.kelompok3.local" width="60%" height="auto"><br>
</div><br>

#### 6. Buat file db.kelompok3.local.inv
Buat file reverse zone /var/lib/bind/db.kelompok3.local.inv yang digunakan untuk reverse lookup, dengan menggunakan perintah: `sudo nano /var/lib/bind/db.kelompok3.local.inv`
<br>
(Lihat file [named.conf.inv](./bind9/named.conf.inv) dan sesuaikan)

<div align="center">
    <img src="images/dns6.jpg" alt="Buat file db.kelompok3.local.inv" width="60%" height="auto"><br>
</div><br>

#### 7. Restart service BIND
Lakukan restart service BIND dengan menggunakan perintah: `sudo systemctl restart named`

<div align="center">
    <img src="images/dns7.png" alt="Restart service" width="60%" height="auto"><br>
</div><br>

#### 8. Cek status service BIND
Lakukan pengecekan status service BIND dengan menggunakan perintah: `sudo systemctl status named`

<div align="center">
    <img src="images/dns8.png" alt="Cek status service" width="60%" height="auto"><br>
</div><br>

#### 9. Check port 53
Check port 53 dengan menggunakan perintah: `sudo ss -tulnp` pastikan port 53 sudah terbuka 

<div align="center">
    <img src="images/dns9.png" alt="Cek port 53" width="60%" height="auto"><br>
</div><br>

#### 10. Konfigurasi file [resolv.conf](./bind9/resolv.conf)
Lakukan konfigurasi pada file /etc/resolv.conf dengan menggunakan perintah: `sudo nano /etc/resolv.conf`
<br>
(Lihat file [resolv.conf](./bind9/resolv.conf))

<div align="center">
    <img src="images/dns10.png" alt="Config file resolv.conf" width="60%" height="auto"><br>
</div><br>

#### 11. Query DNS domain kelompok3.local
Lakukan query DNS domain kelompok3.local dengan menggunakan perintah: `dig kelompok3.local`

<div align="center">
    <img src="images/dns11.png" alt="Query DNS" width="60%" height="auto"><br>
</div><br>

#### 12. Check nslookup
Lakukan pengecekan nslookup dengan menggunakan perintah: `nslookup kelompok3.local`

<div align="center">
    <img src="images/dns12.png" alt="" width="60%" height="auto"><br>
</div><br>




