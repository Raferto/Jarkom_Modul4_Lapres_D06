# Jarkom_Modul4_Lapres_D06


## CIDR Pada UML

Pertama lakukan subnetting dengan cara membagi menjadi subnet subnet kecil sepert berikut

![alt](https://github.com/Raferto/Jarkom_Modul4_Lapres_D06/blob/main/assets/CIDR_UML/CIDR1.png)

Kemudian setiap subnet yang kecil akan digabung mulai dari subnet terjauh dari router Surabaya. Untuk menentukan besar subnet hasil gabungan adalah dengan mengambi subnet yang lebih besar (memiliki /x  lebih kecil) kemudian dinaikan satu ukuranya (/x nya di kurang 1).

Sehingga di dapat seperti berikut

![alt](https://github.com/Raferto/Jarkom_Modul4_Lapres_D06/blob/main/assets/CIDR_UML/CIDR2.png)

![alt](https://github.com/Raferto/Jarkom_Modul4_Lapres_D06/blob/main/assets/CIDR_UML/CIDR3.png)

![alt](https://github.com/Raferto/Jarkom_Modul4_Lapres_D06/blob/main/assets/CIDR_UML/CIDR4.png)

![alt](https://github.com/Raferto/Jarkom_Modul4_Lapres_D06/blob/main/assets/CIDR_UML/CIDR5.png)

![alt](https://github.com/Raferto/Jarkom_Modul4_Lapres_D06/blob/main/assets/CIDR_UML/CIDR6.png)


Kemudian buat lah tree untuk membagi ip yang ada.
Jangan lupa membagi IP untuk server juga.

Sehingga terapat tree seperti berikut.

![alt](https://github.com/Raferto/Jarkom_Modul4_Lapres_D06/blob/main/assets/CIDR_UML/TreeCIDR.PNG)


Dari tree tersebut bisa dilakukan perhitungan untuk setiap subnet nya menjadi seperti berikut

![alt](https://github.com/Raferto/Jarkom_Modul4_Lapres_D06/blob/main/assets/CIDR_UML/PerhitunganCIDR.png)

Setelah itu buat uml nya.

Karena topologi pada uml perlu penyesuaian switch maka dibuat topologi seperti berikut

![alt](https://github.com/Raferto/Jarkom_Modul4_Lapres_D06/blob/main/assets/CIDR_UML/TOPOLOGI.PNG)

Setelah itu buat topologi.sh pada terminal putty

```dotnetcli
# Switch
uml_switch -unix switch01 > /dev/null < /dev/null &
uml_switch -unix switch02 > /dev/null < /dev/null &
uml_switch -unix switch03 > /dev/null < /dev/null &
uml_switch -unix switch04 > /dev/null < /dev/null &
uml_switch -unix switch1 > /dev/null < /dev/null &
uml_switch -unix switch13 > /dev/null < /dev/null &
uml_switch -unix switch15 > /dev/null < /dev/null &
uml_switch -unix switch19 > /dev/null < /dev/null &
uml_switch -unix switch16 > /dev/null < /dev/null &
uml_switch -unix switch17 > /dev/null < /dev/null &
uml_switch -unix switch18 > /dev/null < /dev/null &
uml_switch -unix switch20 > /dev/null < /dev/null &
uml_switch -unix switch21 > /dev/null < /dev/null &
uml_switch -unix switch22 > /dev/null < /dev/null &
uml_switch -unix switch25 > /dev/null < /dev/null &


# Router
# NID TUNTAP 10.151.78.28/30    NID DMZ 10.151.79.56/29
# IP_tuntap_tiap_kelompok = NID_tuntap_tiap_kelompok + 1 = 10.151.78.29
xterm -T SURABAYA -e linux ubd0=SURABAYA,jarkom umid=SURABAYA eth0=tuntap,,,10.151.78.29 eth1=daemon,,,switch1 eth2=daemon,,,switch03 eth3=daemon,,,switch01 eth4=daemon,,,switch13 mem=64M &
xterm -T PASURUAN -e linux ubd0=PASURUAN,jarkom umid=PASURUAN eth0=daemon,,,switch04 eth1=daemon,,,switch19 eth2=daemon,,,switch03 mem=64M &
xterm -T PROBOLINGGO -e linux ubd0=PROBOLINGGO,jarkom umid=PROBOLINGGO eth0=daemon,,,switch15 eth1=daemon,,,switch16 eth2=daemon,,,switch04 mem=64M &
xterm -T BATU -e linux ubd0=BATU,jarkom umid=BATU eth0=daemon,,,switch01 eth1=daemon,,,switch02 eth2=daemon,,,switch21 eth3=daemon,,,switch22 mem=64M &
xterm -T MADIUN -e linux ubd0=MADIUN,jarkom umid=MADIUN eth0=daemon,,,switch22 eth1=daemon,,,switch25 mem=64M &
xterm -T KEDIRI -e linux ubd0=KEDIRI,jarkom umid=KEDIRI eth0=daemon,,,switch02 eth1=daemon,,,switch17 eth2=daemon,,,switch18 mem=64M &
xterm -T BLITAR -e linux ubd0=BLITAR,jarkom umid=BLITAR eth0=daemon,,,switch17 eth1=daemon,,,switch20 mem=64M &



# Server

xterm -T MALANG -e linux ubd0=MALANG,jarkom umid=MALANG eth0=daemon,,,switch18 mem=64M &
xterm -T MOJOKERTO -e linux ubd0=MOJOKERTO,jarkom umid=MOJOKERTO eth0=daemon,,,switch13 mem=64M &

# Klien 1
xterm -T SAMPANG -e linux ubd0=SAMPANG,jarkom umid=SAMPANG eth0=daemon,,,switch1 mem=64M &
xterm -T SIDOARJO -e linux ubd0=SIDOARJO,jarkom umid=SIDOARJO eth0=daemon,,,switch19 mem=64M &
xterm -T BANYUWANGI -e linux ubd0=BANYUWANGI,jarkom umid=BANYUWANGI eth0=daemon,,,switch16 mem=64M &
xterm -T JEMBER -e linux ubd0=JEMBER,jarkom umid=JEMBER eth0=daemon,,,switch16 mem=64M &
xterm -T BONDOWOSO -e linux ubd0=BONDOWOSO,jarkom umid=BONDOWOSO eth0=daemon,,,switch15 mem=64M &
xterm -T JOMBANG -e linux ubd0=JOMBANG,jarkom umid=JOMBANG eth0=daemon,,,switch22 mem=64M &
xterm -T BOJONEGORO -e linux ubd0=BOJONEGORO,jarkom umid=BOJONEGORO eth0=daemon,,,switch25 mem=64M &
xterm -T NGANJUK -e linux ubd0=NGANJUK,jarkom umid=NGANJUK eth0=daemon,,,switch21 mem=64M &
xterm -T LUMAJANG -e linux ubd0=LUMAJANG,jarkom umid=LUMAJANG eth0=daemon,,,switch17 mem=64M &
xterm -T TULUNGAGUNG -e linux ubd0=TULUNGAGUNG,jarkom umid=TULUNGAGUNG eth0=daemon,,,switch20 mem=64M &

```

Kemudian setting networking interface pada tiap uml berdasarkan pembagian ip hasil subnetting sebelumya. Pada modul ini kita pada tiap uml ditambahkan pengaturan interface seperti [berikut](https://github.com/Raferto/Jarkom_Modul4_Lapres_D06/tree/main/assets/CIDR_UML/Interfaces)


Ikuti juga langkah langkah pada modul uml.

Untuk setiap router perlu mengatur sysctl dengan perintah `nano /etc/sysctl.conf` kemudian hilangkan tanda pagar (#) pada bagian `net.ipv4.ip_forward=1`

Lalu ketikan `sysctl -p` untuk mengaktifkan perubahan.

Untuk router surabaya perlu menjalankan iptables untuk bisa akses ke jaringan luar
`iptables –t nat –A POSTROUTING –o eth0 –j MASQUERADE –s 192.168.0.0/16`

Kemudian buat routingnya

```dotnetcli
Surabaya
route add -net 192.168.128.0 netmask 255.255.128.0 gw 192.168.192.2
route add -net 192.168.0.0 netmask 255.255.224.0 gw 192.168.32.2
route add -net 10.151.79.60 netmask 255.255.255.252 gw 192.168.32.2

Pasuruan
route add -net 192.168.128.0 netmask 255.255.240.0 gw 192.168.144.2
route add -net 0.0.0.0 netmask 0.0.0.0 gw 192.168.192.1

Probolinggo
route add -net 0.0.0.0 netmask 0.0.0.0 gw 192.168.144.1

Batu
route add -net 0.0.0.0 netmask 0.0.0.0 gw 192.168.32.1
route add -net 192.168.16.0 netmask 255.255.255.240 gw 192.168.18.2
route add -net 192.168.0.0 netmask 255.255.248.0 gw 192.168.8.2
route add -net 10.151.79.60 netmask 255.255.255.252 gw 192.168.8.2

Madiun
route add -net 0.0.0.0 netmask 0.0.0.0 gw 192.168.18.1

Kediri
route add -net 0.0.0.0 netmask 0.0.0.0 gw 192.168.8.1
route add -net 192.168.0.0 netmask 255.255.252.0 gw 192.168.4.2

Blitar
route add -net 0.0.0.0 netmask 0.0.0.0 gw 192.168.4.1
```


## VLSM Pada CPT

Pertama lakukan subnetting sehingga di dapat

![alt](https://github.com/Raferto/Jarkom_Modul4_Lapres_D06/blob/main/assets/VLSM_CPT/TOPO_VLSM.png)

Kemudian hitung kebutuhan setiap subnet dan tentukan type nya seperti berikut

![alt](https://github.com/Raferto/Jarkom_Modul4_Lapres_D06/blob/main/assets/VLSM_CPT/VLSM_Kebutuhan.png)


Kemudian buat lah tree untuk menentukan pembagian ip. Tree yang dihasilkan seperti berikut/

![alt](https://github.com/Raferto/Jarkom_Modul4_Lapres_D06/blob/main/assets/VLSM_CPT/VLSM_TREE.png)

Setelah itu dari tree bisa diubah menjadi tabel seperti berikut agar memuahkan pembagian ip

![alt](https://github.com/Raferto/Jarkom_Modul4_Lapres_D06/blob/main/assets/VLSM_CPT/VLSM_Pembagian.png)

Setelah itu mengatur subnetting pada tiap device pada cisco sesuai pembagian IP, yang dimana setiap IP address diisi sesuai dengan IP pada range subnetnya masing-masing. Untuk melihat pengaturan setiap device bisa dilihat di [file pkt](https://github.com/Raferto/Jarkom_Modul4_Lapres_D06/blob/main/assets/VLSM_CPT/VLSM.pkt) pada setiap device di bagian config -> interfaces.

Setelah itu menambahkan routing pada setiap router, sebagai berikut:

```
Surabaya
Network 192.168.24.0 Netmask 255.255.252.0 Next Hop 192.168.0.10
Network 192.168.0.12 Netmask 255.255.255.252 Next Hop 192.168.0.10
Network 192.168.8.0 Netmask 255.255.248.0 Next Hop 192.168.0.10
Network 192.168.0.128 Netmask 255.255.255.128 Next Hop 192.168.0.10
Network 192.168.16.0 Netmask 255.255.252.0 Next Hop 192.168.0.6
Network 192.168.1.0 Netmask 255.255.255.0 Next Hop 192.168.0.6
Network 192.168.0.16 Netmask 255.255.255.240 Next Hop 192.168.0.6
Network 192.168.0.0 Netmask 255.255.255.252 Next Hop 192.168.0.6
Network 192.168.20.0 Netmask 255.255.252.0 Next Hop 192.168.0.6
Network 192.168.2.0 Netmask 255.255.254.0 Next Hop 192.168.0.6
Network 10.151.79.60 Netmask 255.255.255.252 Next Hop 192.168.0.6

Pasuruan
Network 0.0.0.0 Netmask 0.0.0.0 Next Hop 192.168.0.9
Network 192.168.8.0 Netmask 255.255.248.0 Next Hop 192.168.0.14
Network 192.168.0.128 Netmask 255.255.255.128 Next Hop 192.168.0.14

Probolinggo
Network 0.0.0.0 Netmask 0.0.0.0 Next Hop 192.168.0.13

Batu
Network 0.0.0.0 Netmask 0.0.0.0 Next Hop 192.168.0.5
Network 192.168.0.16 Netmask 255.255.255.240 Next Hop 192.168.2.2
Network 192.168.16.0 Netmask 255.255.252.0 Next Hop 192.168.0.2
Network 192.168.1.0 Netmask 255.255.255.0 Next Hop 192.168.0.2
Network 10.151.79.60 Netmask 255.255.255.252 Next Hop 192.168.0.2

Madiun
Network 0.0.0.0 Netmask 0.0.0.0 Next Hop 192.168.2.1

Kediri
Network 0.0.0.0 Netmask 0.0.0.0 Next Hop 192.168.0.1
Network 192.168.16.0 Netmask 255.255.252.0 Next Hop 192.168.1.2


Blitar
Network 0.0.0.0 Netmask 0.0.0.0 Next Hop 192.168.1.1
```
