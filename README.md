# Jarkom-Modul-5-E09-2021

Setelah kalian mempelajari semua modul yang telah diberikan, Luffy ingin meminta bantuan untuk terakhir kalinya kepada kalian. Dan kalian dengan senang hati mau membantu Luffy.

A. Tugas pertama kalian yaitu membuat topologi jaringan sesuai dengan rancangan yang diberikan Luffy dibawah ini:

[https://lh5.googleusercontent.com/esmHUvvVWK7buNyaT-Pek8VFxEI2qyGjuOTH4wUa3_-irjaT7_EOA56gnBbaDYeGvVImn9TZUpfKffVn_uKfYLuMmY3Ud0UbAuIWs-yV0eJMYKjtaDIGDj_yMfwxj-MRC9gYVnYI](https://lh5.googleusercontent.com/esmHUvvVWK7buNyaT-Pek8VFxEI2qyGjuOTH4wUa3_-irjaT7_EOA56gnBbaDYeGvVImn9TZUpfKffVn_uKfYLuMmY3Ud0UbAuIWs-yV0eJMYKjtaDIGDj_yMfwxj-MRC9gYVnYI)

## Hasil GNS3

![Untitled](JARKOM%20MODUL%205%20f856521d79ca44638366936a669427a3/Untitled.png)

Keterangan : 	Doriki adalah DNS Server

Jipangu adalah DHCP Server

Maingate dan Jorge adalah Web Server

Jumlah Host pada Blueno adalah 100 host

Jumlah Host pada Cipher adalah 700 host

Jumlah Host pada Elena adalah 300 host

Jumlah Host pada Fukurou adalah 200 host

B. Karena kalian telah belajar subnetting dan routing, Luffy ingin meminta kalian untuk membuat topologi tersebut menggunakan teknik CIDR atau VLSM. setelah melakukan subnetting,

## VLSM

Untuk perhitungan IP dengan menggunakan VLSM, hal yang pertama kita lakukan adalah mengelompokkan setiap PC yang terhubung ke router. Jika terdapat 2 atau lebih PC yang terhubung dengan router namun dengan switch yang sama, maka akan dimasukkan ke dalam 1 kelompok.
Setelah itu, kita menjumlahkan usable IP atau host yang dimiliki oleh masing-masing PC, setiap PC yang terhubung dengan 1 router, maka jumlah hostnya akan ditambahkan dengan 1, dan juga ketika terhubung dengan 2 router, maka jumlah hostnya akan ditambahkan dengan 2, lalu untuk router yang berhubungan dengan router lain, jumlah hostnya adalah 2, karena dia terhubung dengan PC dan juga router lain.
## Pemetaan Subnet 
![Untitled](JARKOM%20MODUL%205%20f856521d79ca44638366936a669427a3/Untitled%201.png)

Lalu direpresentasikan dengan tabel, didapatkan data sebagai berikut.
| Subnet | Connection | Jumlah IP | Length |
| --- | --- | --- | --- |
| A1 | Doriki + Jipangu → Water7 | 3 | 29 |
| A2 | Blueno → Water7 | 101 | 25 |
| A3 | Cipher → Water7 | 701 | 22 |
| A4 | Water7 → Foosha | 2 | 30 |
| A5 | Guanhao → Foosha | 2 | 30 |
| A6 | Elena → Guanhao | 301 | 23 |
| A7 | Fukurou → Guanhao | 201 | 24 |
| A8 | Maingate + Jorge → Guanhao | 3 | 29 |
| Total |  | 1314 | 21 |
![tabel subnetting modul](https://user-images.githubusercontent.com/81345045/145210165-a40b1ac3-1b2f-4795-9dd4-95a89c6738f2.png) \
Setelah itu, kita menghitung IP dari setiap subnet. Dari jumlah IP keseluruhan, didapatkan sebesar 1314 IP, jika dikonversikan ke dalam Netmask, didapatkan Netmask = /21. Pada tabel di modul, diketahui bahwa Netmask /21 memiliki Wildcard 0.0.7.255, di mana digit ketiga yaitu 7, karena dimulai dari 0, maka range digit ketiga adalah 0 - 7, yang menandakan ada 8 macam untuk digit ketiga. Dalam perhitungan ini, kita menggunakan tree agar mudah. Prefix IP yang kami gunakan adalah 192.204 dengan IP besar 192.204.0.0 /21.
Dari IP 192.204.0.0 /21 ini, kita membagi rangenya menjadi 2 sama rata. Di sisi kiri memiliki range IP 192.204.0.0 /22 hingga 192.204.3.0 /22. Sedangkan di sisi kanan, rangenya adalah 192.204.4.0 /22 hingga 192.204.7.0 /22. Lalu kita gunakan IP 192.204.0.0/22 untuk subnet A3. Kemudian lakukan pemecahan dengan cara yang sama hingga semua subnet mendapat IP seperti pada gambar di bawah ini.
![modul5 (1).jpg](JARKOM%20MODUL%205%20f856521d79ca44638366936a669427a3/modul5_(1).jpg) \
Dari hasil perhitungan di atas, didapatkan rekap IP setiap subnet sebagai berikut.

| Subnet | Connection | Jumlah IP | Length | IP | Subnet Mask |
| --- | --- | --- | --- | --- | --- |
| A1 | Doriki + Jipangu → Water7 | 3 | 29 | 192.204.7.128 | 255.255.255.248 |
| A2 | Blueno → Water7 | 101 | 25 | 192.204.7.0 | 255.255.255.128 |
| A3 | Cipher → Water7 | 701 | 22 | 192.204.0.0 | 255.255.252.0 |
| A4 | Water7 → Foosha | 2 | 30 | 192.204.7.144 | 255.255.255.252 |
| A5 | Guanhao → Foosha | 2 | 30 | 192.204.7.148 | 255.255.255.252 |
| A6 | Elena → Guanhao | 301 | 23 | 192.204.4.0 | 255.255.254.0 |
| A7 | Fukurou → Guanhao | 201 | 24 | 192.204.6.0 | 255.255.255.0 |
| A8 | Maingate + Jorge → Guanhao | 3 | 29 | 192.204.7.136 | 255.255.255.248 |
| Total |  | 1314 | 21 |  |  |

## IP Configuration

### Doriki

```jsx
auto eth0
iface eth0 inet static
address 192.204.7.130
netmask 255.255.255.248
gateway 192.204.7.129
```

### Jipangu

```jsx
auto eth0
iface eth0 inet static
address 192.204.7.131
netmask 255.255.255.248
gateway 192.204.7.129
```

### Water7

```jsx
auto lo
iface lo inet loopback

auto eth0
iface eth0 inet static
address 192.204.7.193
netmask 255.255.255.252
gateway 192.204.7.194

auto eth1
iface eth1 inet static
address 192.204.7.129
netmask 255.255.255.248

auto eth2
iface eth2 inet static
address 192.204.7.1
netmask 255.255.255.128

auto eth3
iface eth3 inet static
address 192.204.0.1
netmask 255.255.252.0
```

### Blueno

```jsx
auto eth0
iface eth0 inet dhcp
```

### Cipher

```jsx
auto eth0
iface eth0 inet dhcp
```

### Foosha

```jsx
auto lo
iface lo inet loopback

auto eth0
iface eth0 inet dhcp
hwaddress ether de:39:11:3d:8a:21

auto eth1
iface eth1 inet static
address 192.204.7.194
netmask 255.255.255.252

auto eth2
iface eth2 inet static
address 192.204.7.225
netmask 255.255.255.252
```

![Untitled](JARKOM%20MODUL%205%20f856521d79ca44638366936a669427a3/Untitled%202.png)

### Jorge

```jsx
auto eth0
iface eth0 inet static
address 192.204.7.162
netmask 255.255.255.248
gateway 192.204.7.161
```

### Maingate

```jsx
auto eth0
iface eth0 inet static
address 192.204.7.163
netmask 255.255.255.248
gateway 192.204.7.161
```

### Guanhao

```jsx
auto lo
iface lo inet loopback

auto eth0
iface eth0 inet static
address 192.204.7.226
netmask 255.255.255.252
gateway 192.204.7.225

auto eth1
iface eth1 inet static
address 192.204.7.161
netmask 255.255.255.248

auto eth2
iface eth2 inet static
address 192.204.4.1
netmask 255.255.254.0

auto eth3
iface eth3 inet static
address 192.204.6.1
netmask 255.255.255.0
```

### Elena

```jsx
auto eth0
iface eth0 inet dhcp
```

### Fukurou

```jsx
auto eth0
iface eth0 inet dhcp
```

C. Kalian juga diharuskan melakukan Routing agar setiap perangkat pada jaringan tersebut dapat terhubung.

### Routing Foosha

```jsx
route add -net 192.204.7.128 netmask 255.255.255.248 gw 192.204.7.145
route add -net 192.204.7.0 netmask 255.255.255.128 gw 192.204.7.145
route add -net 192.204.0.0 netmask 255.255.252.0 gw 192.204.7.145

route add -net 192.204.4.0 netmask 255.255.254.0 gw 192.204.7.150
route add -net 192.204.6.0 netmask 255.255.255.0 gw 192.204.7.150
route add -net 192.204.7.136  netmask 255.255.255.248 gw 192.204.7.150
```

D. Tugas berikutnya adalah memberikan ip pada subnet Blueno, Cipher, Fukurou, dan Elena secara dinamis menggunakan bantuan DHCP server. Kemudian kalian ingat bahwa kalian harus setting DHCP Relay pada router yang menghubungkannya.

### Foosha

```bash
iptables -t nat -A POSTROUTING -o eth0 -j MASQUERADE -s 192.204.0.0/21
```

## DHCP Server

### Jipangu

```bash
echo "nameserver 192.168.122.1" > /etc/resolv.conf
apt-get install isc-dhcp-server -y
```

/etc/default/isc-dhcp-server

![Untitled](JARKOM%20MODUL%205%20f856521d79ca44638366936a669427a3/Untitled%203.png)

/etc/dhcp/dhcpd.conf

![Untitled](JARKOM%20MODUL%205%20f856521d79ca44638366936a669427a3/Untitled%204.png)

![Untitled](JARKOM%20MODUL%205%20f856521d79ca44638366936a669427a3/Untitled%205.png)

![Untitled](JARKOM%20MODUL%205%20f856521d79ca44638366936a669427a3/Untitled%206.png)

![Untitled](JARKOM%20MODUL%205%20f856521d79ca44638366936a669427a3/Untitled%207.png)

![Untitled](JARKOM%20MODUL%205%20f856521d79ca44638366936a669427a3/Untitled%208.png)

## DHCP Relay

### Water7

```bash
echo "nameserver 192.168.122.1" > /etc/resolv.conf
apt-get install isc-dhcp-relay -y
```

/etc/default/isc-dhcp-relay

![Untitled](JARKOM%20MODUL%205%20f856521d79ca44638366936a669427a3/Untitled%209.png)

### Guanhao

```bash
echo "nameserver 192.168.122.1" > /etc/resolv.conf
apt-get install isc-dhcp-relay -y
```

/etc/default/isc-dhcp-relay

![Untitled](JARKOM%20MODUL%205%20f856521d79ca44638366936a669427a3/Untitled%209.png)

## DHCP Client

### Blueno

![Untitled](JARKOM%20MODUL%205%20f856521d79ca44638366936a669427a3/Untitled%2010.png)

### Cipher

![Untitled](JARKOM%20MODUL%205%20f856521d79ca44638366936a669427a3/Untitled%2011.png)

### Elena

![Untitled](JARKOM%20MODUL%205%20f856521d79ca44638366936a669427a3/Untitled%2012.png)

### Fukurou

![Untitled](JARKOM%20MODUL%205%20f856521d79ca44638366936a669427a3/Untitled%2013.png)

## DNS Server

### Doriki

1. Agar topologi yang kalian buat dapat mengakses keluar, kalian diminta untuk mengkonfigurasi Foosha menggunakan iptables, tetapi Luffy tidak ingin menggunakan MASQUERADE.
    
    ![Untitled](JARKOM%20MODUL%205%20f856521d79ca44638366936a669427a3/Untitled%2014.png)
    
    ```bash
    iptables -t nat -A POSTROUTING -s 192.204.0.0/21 -o eth0 -j SNAT --to-source 192.168.122.8
    ```
    
    Testing
    
    ![Untitled](JARKOM%20MODUL%205%20f856521d79ca44638366936a669427a3/Untitled%2015.png)
    
2. Kalian diminta untuk mendrop semua akses HTTP dari luar Topologi kalian pada server yang merupakan DHCP Server dan DNS Server demi menjaga keamanan.
    
    ### Doriki
    
    ```bash
    iptables -A FORWARD -d 192.204.7.128/29 -i eth0 -p tcp --dport 80 -j DROP
    iptables -A FORWARD -d 192.204.7.128/29 -i eth0 -p tcp --dport 443 -j ACCEPT
    ```
    
    HTTPS
    
    ![Untitled](JARKOM%20MODUL%205%20f856521d79ca44638366936a669427a3/Untitled%2016.png)
    
    HTTP
    
    ![Untitled](JARKOM%20MODUL%205%20f856521d79ca44638366936a669427a3/Untitled%2017.png)
    
    ### Jipangu
    
    ```bash
    iptables -A FORWARD -d 192.204.7.128/29 -i eth0 -p tcp --dport 80 -j DROP
    iptables -A FORWARD -d 192.204.7.128/29 -i eth0 -p tcp --dport 443 -j ACCEPT
    ```
    
    HTTPS
    
    ![Untitled](JARKOM%20MODUL%205%20f856521d79ca44638366936a669427a3/Untitled%2018.png)
    
    HTTP
    
    ![Untitled](JARKOM%20MODUL%205%20f856521d79ca44638366936a669427a3/Untitled%2019.png)
    
3. Karena kelompok kalian maksimal terdiri dari 3 orang. Luffy meminta kalian untuk membatasi DHCP dan DNS Server hanya boleh menerima maksimal 3 koneksi ICMP secara bersamaan menggunakan iptables, selebihnya didrop.
    
    Memasukkan iptables berikut ke dalam DHCP Server (Jipangu) serta DNS Server (Doriki)
    
    ```bash
    iptables -A INPUT -p icmp -m connlimit --connlimit-above 3 --connlimit-mask 0 -j DROP
    ```
    
    ## Jipangu
    
    ![Untitled](JARKOM%20MODUL%205%20f856521d79ca44638366936a669427a3/Untitled%2020.png)
    
    ## Doriki
    
    ![Untitled](JARKOM%20MODUL%205%20f856521d79ca44638366936a669427a3/Untitled%2021.png)
    
    Kemudian kalian diminta untuk membatasi akses ke Doriki yang berasal dari subnet Blueno, Cipher, Elena dan Fukuro dengan beraturan sebagai berikut
    
4. Akses dari subnet Blueno dan Cipher hanya diperbolehkan pada pukul 07.00 - 15.00 pada hari Senin sampai Kamis.
    
    ## Doriki
    
    ### From Cipher
    
    ```bash
    iptables -A INPUT -s 192.204.0.0/22 -m time --timestart 07:00 --timestop 15:00 --weekdays Mon,Tue,Wed,Thu -j ACCEPT
    iptables -A INPUT -s 192.204.0.0/22 -j REJECT
    ```
    
    Selasa, 11:38:39
    
    ![Untitled](JARKOM%20MODUL%205%20f856521d79ca44638366936a669427a3/Untitled%2022.png)
    
    Selasa, 17:00:00
    
    ![Untitled](JARKOM%20MODUL%205%20f856521d79ca44638366936a669427a3/Untitled%2023.png)
    
    ### From Blueno
    
    ```bash
    iptables -A INPUT -s 192.204.7.0/25 -m time --timestart 07:00 --timestop 15:00 --weekdays Mon,Tue,Wed,Thu -j ACCEPT
    iptables -A INPUT -s 192.204.7.0/25 -j REJECT
    ```
    
    Selasa, 10:00:00
    
    ![Untitled](JARKOM%20MODUL%205%20f856521d79ca44638366936a669427a3/Untitled%2024.png)
    
    Selasa, 17:00:00
    
    ![Untitled](JARKOM%20MODUL%205%20f856521d79ca44638366936a669427a3/Untitled%2025.png)
    
5. Akses dari subnet Elena dan Fukuro hanya diperbolehkan pada pukul 15.01 hingga pukul 06.59 setiap harinya.
    
    Selain itu di reject
    
    ## Doriki
    
    ### From Elena
    
    ```bash
    iptables -A INPUT -s 192.204.4.0/23 -m time --timestart 15:01 --timestop 06:59 -j ACCEPT
    iptables -A INPUT -s 192.204.4.0/23 -j REJECT
    ```
    
    Selasa, 16:00:00
    
    ![Untitled](JARKOM%20MODUL%205%20f856521d79ca44638366936a669427a3/Untitled%2026.png)
    
    Selasa, 10:00:00
    
    ![Untitled](JARKOM%20MODUL%205%20f856521d79ca44638366936a669427a3/Untitled%2027.png)
    
    ### From Fukurou
    
    ```bash
    iptables -A INPUT -s 192.204.6.0/24 -m time --timestart 15:01 --timestop 06:59 -j ACCEPT
    iptables -A INPUT -s 192.204.6.0/24 -j REJECT
    ```
    
    Selasa, 16:00:00
    
    ![Untitled](JARKOM%20MODUL%205%20f856521d79ca44638366936a669427a3/Untitled%2028.png)
    
    Selasa, 10:00:00
    
    ![Untitled](JARKOM%20MODUL%205%20f856521d79ca44638366936a669427a3/Untitled%2029.png)
    
6. Karena kita memiliki 2 Web Server, Luffy ingin Guanhao disetting sehingga setiap request dari client yang mengakses DNS Server akan didistribusikan secara bergantian pada Jorge dan Maingate
    
    Guanhao
    
    ```bash
    iptables -A PREROUTING -t nat -p tcp -d 192.204.7.128/29 -m statistic --mode nth --every 2 --packet 0 -j DNAT --to-destination  192.204.7.138
    iptables -A PREROUTING -t nat -p tcp -d 192.204.7.128/29 -j DNAT --to-destination 192.204.7.139
    iptables -t nat -A POSTROUTING -p tcp -d 192.204.7.138 -j SNAT --to-source 192.204.7.128
    iptables -t nat -A POSTROUTING -p tcp -d 192.204.7.139 -j SNAT --to-source 192.204.7.128
    ```
    
    Menginstall Apache2 di Jorge dan Maingate
    
    index.html → Jorge
    
    ![Untitled](JARKOM%20MODUL%205%20f856521d79ca44638366936a669427a3/Untitled%2030.png)
    
    index.html → Maingate
    
    ![Untitled](JARKOM%20MODUL%205%20f856521d79ca44638366936a669427a3/Untitled%2031.png)
    
    Testing dari Elena
    
    ![Untitled](JARKOM%20MODUL%205%20f856521d79ca44638366936a669427a3/Untitled%2032.png)
    
    Luffy berterima kasih pada kalian karena telah membantunya. Luffy juga mengingatkan agar semua aturan iptables harus disimpan pada sistem atau paling tidak kalian menyediakan script sebagai backup.
