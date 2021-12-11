# Jarkom-Modul-5-D14-2021

##  Nama anggota kelompok
1.  A. Zidan Abdillah Majid (05111940000070)
2.  Cliffton Delias Perangin Angin (05111940000181)
3.  Abdurrahman Fauzan Firmansyah (05111940000231)

Prefix IP kelompok kami adalah `10.28.x.x`

### VLSM

1.  **Kebutuhan IP tiap Subnet**

    ![image](https://user-images.githubusercontent.com/72073667/145677084-a1fb0347-d53a-4b60-8844-8eefa93124ca.png)

2.  **Subnetting**

    ![Bulet_Bulet](https://user-images.githubusercontent.com/72073667/145677091-72f645ab-e5f9-4eaf-90fb-647582cc135e.jpg)

3.  **Pohon pemagian IP**

    ![Pohon_Faktor](https://user-images.githubusercontent.com/72073667/145677110-8e7365d8-f414-417a-9e0a-e4e7c5e839a5.jpg)

4.  **Hasil pembagian IP**

    ![image](https://user-images.githubusercontent.com/72073667/145677133-420ddbce-cca2-49de-8e7e-10a77b5ec7ca.png)

5.  **Setting Interface tiap node**

    - Foosha
      ```bash
      auto eth0
      iface eth0 inet dhcp

      auto eth1
      iface eth1 inet static
         address 10.28.255.149
         netmask 255.255.255.252

      auto eth2
      iface eth2 inet static
         address 10.28.255.145
         netmask 255.255.255.252
      ```
      
    - Water7
      ```bash
      auto eth0
      iface eth0 inet static
          address 10.28.255.146
          netmask 255.255.255.252
          gateway 10.28.255.145

      auto eth1
      iface eth1 inet static
          address 10.28.255.1
          netmask 255.255.255.128

      auto eth2
      iface eth2 inet static
          address 10.28.248.1
          netmask 255.255.252.0

      auto eth3
      iface eth3 inet static
          address 10.28.255.129
          netmask 255.255.255.248
      ```
      
    - Guanhao
      ```bash
      auto eth0
      iface eth0 inet static
          address 10.28.255.150
          netmask 255.255.255.252
          gateway 10.28.255.149

      auto eth1
      iface eth1 inet static
          address 10.28.252.1
          netmask 255.255.254.0

      auto eth2
      iface eth2 inet static
          address 10.28.254.1
          netmask 255.255.255.0

      auto eth3
      iface eth3 inet static
          address 10.28.255.137
          netmask 255.255.255.248
      ```
      
    - Doriki
      ```bash
      auto eth0
      iface eth0 inet static
          address 10.28.255.131
          netmask 255.255.255.248
          gateway 10.28.255.129
      ```
      
    - Jipangu
      ```bash
      auto eth0
      iface eth0 inet static
          address 10.28.255.130
          netmask 255.255.255.248
          gateway 10.28.255.129
      ```
      
    - Jorge
      ```bash
      auto eth0
      iface eth0 inet static
          address 10.28.255.139
          netmask 255.255.255.248
          gateway 10.28.255.137
      ```
      
    - Maingate
      ```bash
      auto eth0
      iface eth0 inet static
          address 10.28.255.138
          netmask 255.255.255.248
          gateway 10.28.255.137
      ```
      
    - Blueno, Chiper, Elena, dan Fukurou
      ```bash
      auto eth0
      iface eth0 inet dhcp
      ```

6.  **Routing**

    - Foosha
      ```bash
      route add -net 10.28.255.0 netmask 255.255.255.128 gw 10.28.255.146
      route add -net 10.28.255.128 netmask 255.255.255.248 gw 10.28.255.146
      route add -net 10.28.248.0 netmask 255.255.252.0 gw 10.28.255.146
      route add -net 10.28.252.0 netmask 255.255.254.0 gw 10.28.255.150
      route add -net 10.28.255.136 netmask 255.255.255.248 gw 10.28.255.150
      route add -net 10.28.254.0 netmask 255.255.255.0 gw 10.28.255.150
      ```
      
    - Water7
      ```bash
      route add -net 0.0.0.0 netmask 0.0.0.0 gw 10.28.255.145
      ```
      
    - Guanhao
      ```bash
      route add -net 0.0.0.0 netmask 0.0.0.0 gw 10.28.255.149
      ```
      
### DHCP
    
1.  DHCP Server (Jipangu)
    - Install dhcp server menggunakan `apt install isc-dhcp-server`
    - Ubah file config pada `/etc/dhcp/dhcpd.conf` menjadi seperti dibawah
      ```bash
      ddns-update-style none;

      option domain-name-servers 10.28.255.131;

      default-lease-time 600;
      max-lease-time 7200;

      log-facility local7;

      #A1
      subnet 10.28.255.0 netmask 255.255.255.128 {
          range 10.28.255.2 10.28.255.126;
          option routers 10.28.255.1;
          option broadcast-address 10.28.255.127;
      }

      #A2
      subnet 10.28.252.0 netmask 255.255.254.0 {
          range 10.28.252.2 10.28.253.254;
          option routers 10.28.252.1;
          option broadcast-address 10.28.253.255;
      }
      
      #A3
      subnet 10.28.255.128 netmask 255.255.255.248 {
      }
      
      #A6
      subnet 10.28.255.136 netmask 255.255.255.248 {
      }

      #A7
      subnet 10.28.248.0 netmask 255.255.252.0 {
          range 10.28.248.2 10.28.251.254;
          option routers 10.28.248.1;
          option broadcast-address 10.28.251.255;
      }

      #A8
      subnet 10.28.254.0 netmask 255.255.255.0 {
          range 10.28.254.2 10.28.254.254;
          option routers 10.28.254.1;
          option broadcast-address 10.28.254.255;
      }
      ```
      
    - Ubah file config pada `/etc/default/isc-dhcp-server` menjadi seperti dibawah
      ```bash
      INTERFACES="eth0"
      ```
      
    - Hidupkan service menggunakan `service isc-dhcp-server start`
    
2.  DHCP Relay (Water7, Foosha, dan Guanhao)
    - Install dhcp relay menggunakan `apt install isc-dhcp-relay` menjadi seperti dibawah
    - Ubah config pada `/etc/default/isc-dhcp-relay` menjadi seperti dibawah
      - Water7 dan Guanhao
        ```bash
        SERVERS="10.28.255.130"

        INTERFACES="eth0 eth1 eth2 eth3"

        OPTIONS=""
        ```
        
      - Foosha
        ```bash
        SERVERS="10.28.255.130"

        INTERFACES="eth1 eth2"

        OPTIONS=""
        ```
        
    - Hidupkan service menggunakan `service isc-dhcp-relay start`

### DNS Server (Doriki)

1.  Install bind9 menggunakan `apt install bind9`

2.  Ubah file config pada `/etc/bind/named.conf.options` menjadi seperti dibawah
    ```bash
    options {
    directory "/var/cache/bind";

    // If there is a firewall between you and nameservers you want
    // to talk to, you may need to fix the firewall to allow multiple
    // ports to talk.  See http://www.kb.cert.org/vuls/id/800113
    // If your ISP provided one or more IP addresses for stable
    // nameservers, you probably want to use them as forwarders.
    // Uncomment the following block, and insert the addresses replacing
    // the all-0's placeholder.

    forwarders {
    192.168.122.1;
    };

    //========================================================================
    // If BIND logs error messages about the root key being expired,
    // you will need to update your keys.  See https://www.isc.org/bind-keys
    //========================================================================

    allow-query{any;};                                    
    auth-nxdomain no;    # conform to RFC1035             
    listen-on-v6 { any; };                                
    };
    ```

3.  Restart bind9 menggunakan `service bind9 restart`

### Soal

1.  No 1

    Agar topologi yang kalian buat dapat mengakses keluar, kalian diminta untuk mengkonfigurasi Foosha menggunakan iptables, tetapi Luffy tidak ingin menggunakan MASQUERADE.
    
    Setting di Foosha
    ```bash
    iptables -t nat -A POSTROUTING -s 10.28.248.0/21 -o eth0 -j SNAT --to-source [IP eth0 FOOSHA]
    ```
    
    Untuk IP yang didapat Foosha bisa dilihat menggunakan command `ifconfig eth0`
    
2.  No 2

    Kalian diminta untuk mendrop semua akses HTTP dari luar Topologi kalian pada server yang merupakan DHCP Server dan DNS Server demi menjaga keamanan.
    
    Setting di Water7
    ```bash
    iptables -A FORWARD -d 10.28.255.128/29 ! -s 10.28.248.0/21 -p tcp --dport 80 -j DROP
    ```
    
    Keterangan:
    Jika paket yang akan diteruskan destinationnya merupakan subnet A3 atau Subnet milik DHCP Server (Jipangu) dan DNS Server (Doriki), sourcenya berasal dari luar topologi (luar subnet 10.28.248.0/21) dan menggunakan protokol tcp dengan port 80 (http) maka paket akan di DROP

3.  No 3

    Karena kelompok kalian maksimal terdiri dari 3 orang. Luffy meminta kalian untuk membatasi DHCP dan DNS Server hanya boleh menerima maksimal 3 koneksi ICMP secara bersamaan menggunakan iptables, selebihnya didrop.
    
    Setting di Jipangu dan Doriki
    ```bash
    iptables -A INPUT -p icmp -m connlimit --connlimit-above 3 --connlimit-mask 0 -j DROP
    ```
    
    Keterangan:
    Apabila paket yang masuk menggunakan protokol ICMP dan koneksi yang terhubung bersamaan terdapat > 3 maka paket akan didrop

4.  No 4

    Akses dari subnet Blueno dan Cipher hanya diperbolehkan pada pukul 07.00 - 15.00 pada hari Senin sampai Kamis.
    ```bash
    #Blueno
    iptables -A INPUT -s 10.28.255.0/25 -m time --weekdays Mon,Tue,Wed,Thu --timestart 07:00 --timestop 15:00 -j ACCEPT
    iptables -A INPUT -s 10.28.255.0/25 -j REJECT
    
    #Cipher
    iptables -A INPUT -s 10.28.248.0/22 -m time --weekdays Mon,Tue,Wed,Thu --timestart 07:00 --timestop 15:00 -j ACCEPT
    iptables -A INPUT -s 10.28.248.0/22 -j REJECT
    ```
    
    Ide:
    Pertama, accept paket yang sesuai dengan ketentuan (Senin-Kamis pukul 07:00-15:00) kemudian tambahkan setting untuk mereject semua paket.
    
    Keterangan:
    iptables 1: Apabila paket yang masuk berasal dari subnet Blueno atau Cipher dan masuk pada hari Senin-Kamis pukul 07:00-15:00 maka paket akan diaccept
    iptables 2: Apabila paket yang masuk berasal dari subnet Blueno atau Cipher maka maket akan direject
    
5.  No 5

    Akses dari subnet Elena dan Fukuro hanya diperbolehkan pada pukul 15.01 hingga pukul 06.59 setiap harinya.
    ```bash
    #Elena
    iptables -A INPUT -s 10.28.252.0/23 -m time --timestart 07:00 --timestop 15:00 -j REJECT
    iptables -A INPUT -s 10.28.252.0/23 -j ACCEPT
    
    #Fukurou
    iptables -A INPUT -s 10.28.254.0/24 -m time --timestart 07:00 --timestop 15:00 -j REJECT
    iptables -A INPUT -s 10.28.254.0/24 -j ACCEPT
    ```
    
    Ide:
    Pertama, reject paket yang masuk diluar jam ketentuan kemudian tambahkan setting untuk accept semua paket.
    
    Keterangan:
    iptables 1: Apabila paket yang masuk berasal dari subnet Elena atau Fukurou dan masuk pada pukul 07:00-15:00 maka paket akan direject
    iptables 2: Apabila paket yang masuk berasal dari subnet Elena atau Fukurou maka maket akan diaccept
    
### Kendala

No 6 sebenarnya sudah menemukan setting iptablesnya, cuman ketika coba cek menggunakan **netcat** terdapat error karena semua port ditutup. Sudah coba buka port INPUT, OUTPUT, FORWARD menggunakan iptables tapi tetap tertutup portnya. Untuk setting iptablesnya seperti dibawah:

```bash
iptables -t nat -A PREROUTING -d 10.28.255.131 -m statistic --mode nth --every 2 --packet 0 -j DNAT --to-destination 10.28.255.138
iptables -t nat -A PREROUTING -d 10.28.255.131 -m statistic --mode nth --every 2 --packet 1 -j DNAT --to-destination 10.28.255.139

iptables -t nat -A POSTROUTING -d 10.28.255.138 -j SNAT --to-source 10.28.255.131
iptables -t nat -A POSTROUTING -d 10.28.255.139 -j SNAT --to-source 10.28.255.131
```
