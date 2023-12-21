# Praktikum Modul 5 Jaringan Komputer - Firewall

Praktikum Modul 5 Jaringan Komputer - **IT07**

## Authors

| Nama                                                | NRP        |
| --------------------------------------------------- | ---------- |
| [Rangga Aldo](https://www.github.com/ranggaaldosas) | 5027211059 |
| [Maulana Ilyasa](https://www.github.com/ilyasahsh)  | 5027211065 |

## Topologi GNS

<p align="center">
    <img src="https://i.ibb.co/CHV0Pnk/image.png">

## Rute

<p align="center">
    <img src="https://i.ibb.co/JtZbFyF/image.png">

## Tree

<p align="center">
    <img src="https://i.ibb.co/z5jXjPZ/image.png">

## Pembagian IP

<p align="center">
    <img src="https://i.ibb.co/0KfC77L/Screenshot-2023-12-20-160656.png">

## Config

### Aura (Router)

```bash
auto eth0
iface eth0 inet dhcp

#A3
auto eth1
iface eth1 inet static
address 10.67.1.125
netmask 255.255.255.252

#A4
auto eth2
iface eth2 inet static
address 10.67.1.121
netmask 255.255.255.252

#Heiter
up route add -net 10.67.4.0 netmask 255.255.252.0 gw 10.67.1.126
up route add -net 10.67.8.0 netmask 255.255.248.0 gw 10.67.1.126

#Frieren
up route add -net 10.67.1.116 netmask 255.255.255.252 gw 10.67.1.122
up route add -net 10.67.1.112 netmask 255.255.255.252 gw 10.67.1.122
up route add -net 10.67.2.0 netmask 255.255.254.0 gw 10.67.1.122
up route add -net 10.67.1.128 netmask 255.255.255.128 gw 10.67.1.122
up route add -net 10.67.1.108 netmask 255.255.255.252 gw 10.67.1.122
up route add -net 10.67.1.104 netmask 255.255.255.252 gw 10.67.1.122
```

## Heiter

```bash
auto lo
iface lo inet loopback

#A3
auto eth0
iface eth0 inet static
address 10.67.1.126
netmask 255.255.255.252
gateway 10.67.1.125

#A2
auto eth1
iface eth1 inet static
address 10.67.8.1
netmask 255.255.248.0

#A1
auto eth2
iface eth2 inet static
address 10.67.4.1
netmask 255.255.252.0

up route add -net 0.0.0.0 netmask 0.0.0.0 gw 10.67.1.125
```

## Frieren

```bash
auto lo
iface lo inet loopback

#A4
auto eth0
iface eth0 inet static
address 10.67.1.122
netmask 255.255.255.252
gateway 10.67.1.121

#A5
auto eth1
iface eth1 inet static
address 10.67.1.117
netmask 255.255.255.252

#A6
auto eth2
iface eth2 inet static
address 10.67.1.113
netmask 255.255.255.252

up route add -net 10.67.2.0 netmask 255.255.254.0 gw 10.67.1.114
up route add -net 10.67.1.128 netmask 255.255.255.128 gw 10.67.1.114
up route add -net 10.67.1.108 netmask 255.255.255.252 gw 10.67.1.114
up route add -net 10.67.1.104 netmask 255.255.255.252 gw 10.67.1.114
up route add -net 0.0.0.0 netmask 0.0.0.0 gw 10.67.1.121
```

## Himmel

```bash
auto lo
iface lo inet loopback

#A6
auto eth0
iface eth0 inet static
address 10.67.1.114
netmask 255.255.255.252
gateway 10.67.1.113

#A7
auto eth1
iface eth1 inet static
address 10.67.2.1
netmask 255.255.254.0

#A8
auto eth2
iface eth2 inet static
address 10.67.1.129
netmask 255.255.255.128

up route add -net 10.67.1.108 netmask 255.255.255.252 gw 10.67.1.130
up route add -net 10.67.1.104 netmask 255.255.255.252 gw 10.67.1.130
up route add -net 0.0.0.0 netmask 0.0.0.0 gw 10.67.1.113
```

## Fern

```bash
auto lo
iface lo inet loopback

#A8
auto eth0
iface eth0 inet static
address 10.67.1.130
netmask 255.255.255.128
gateway 10.67.1.129

#A9
auto eth1
iface eth1 inet static
address 10.67.1.109
netmask 255.255.255.252

#A10
auto eth2
iface eth2 inet static
address 10.67.1.105
netmask 255.255.255.252

up route add -net 0.0.0.0 netmask 0.0.0.0 gw 10.67.1.129
```

## Richter (Dns)

```bash
auto eth0
iface eth0 inet static
address 10.67.1.110
netmask 255.255.255.252
gateway 10.67.1.109
```

## Revolte (Dhcp)

```bash
auto eth0
iface eth0 inet static
address 10.67.1.106
netmask 255.255.255.252
gateway 10.67.1.105
```

## Sein (web server)

```bash
auto eth0
iface eth0 inet static
address 10.67.4.2
netmask 255.255.252.0
gateway 10.67.4.1
```

## stark (Web server)

```bash
auto eth0
iface eth0 inet static
address 10.67.1.118
netmask 255.255.255.252
gateway 10.67.1.117
```

## Client

```bash
auto eth0
iface eth0 inet dhcp
```

---

## Soal 1

#### Aura

```
nat_ip=$(ip -4 addr show eth0 | grep -oP '(?<=inet\s)\d+(\.\d+){3}')
iptables -t nat -A POSTROUTING -o eth0 -j SNAT --to-source $nat_ip
```

## Soal 2

#### Fern

```
iptables -A INPUT -p udp -j DROP
iptables -A INPUT -p tcp ! --dport 8080 -j DROP
iptables -A INPUT -p tcp -j DROP
```

## Soal 3

```
iptables -A INPUT -m state --state ESTABLISHED,RELATED -j ACCEPT
iptables -A INPUT -p icmp -m connlimit --connlimit-above 3 --connlimit-mask 0 -j DROP
```

## Soal 4

```
iptables -A INPUT -p tcp --dport 22 -m iprange --src-range 10.67.8.3-10.67.10.5 -j ACCEPT
iptables -A INPUT -p tcp --dport 22 -j DROP
```

## Soal 5

```
iptables -A INPUT -p tcp --dport 80 -m time --timestart 08:00 --timestop 16:00 --weekdays Mon,Tue,Wed,Thu,Fri -j ACCEPT
iptables -A INPUT -p tcp --dport 80 -j DROP
```

## Soal 6

```
iptables -A INPUT -p tcp --dport 80 -m time --timestart 12:00 --timestop 13:00 --weekdays Mon,Tue,Wed,Thu -j DROP
iptables -A INPUT -p tcp --dport 80 -m time --timestart 11:00 --timestop 13:00 --weekdays Fri -j DROP
```

## Soal 7

```
echo '
Listen 80
Listen 443

<IfModule ssl_module>
        Listen 443
</IfModule>

<IfModule mod_gnutls.c>
        Listen 443
</IfModule>
' > /etc/apache2/ports.conf

echo '# Sein | Stark
Sein | Stark nih' > /var/www/html/index.html

echo "
<VirtualHost *:80>
    ServerName 10.67.4.2
    DocumentRoot /var/www/html
    ErrorLog \${APACHE_LOG_DIR}/error.log
    CustomLog \${APACHE_LOG_DIR}/access.log combined
</VirtualHost>
<VirtualHost *:443>
    ServerName 10.67.4.2
    DocumentRoot /var/www/html
    ErrorLog \${APACHE_LOG_DIR}/error.log
    CustomLog \${APACHE_LOG_DIR}/access.log combined
</VirtualHost>
" > /etc/apache2/sites-available/sein.conf

a2ensite sein.conf
service apache2 restart
```

```bash
iptables -A PREROUTING -t nat -p tcp --dport 80 -d 10.67.4.2 -m statistic --mode nth --every 2 --packet 0 -j DNAT --to-destination 10.67.4.2:80
iptables -A PREROUTING -t nat -p tcp --dport 80 -d 10.67.4.2 -j DNAT --to-destination 10.67.1.118:80
iptables -A PREROUTING -t nat -p tcp --dport 443 -d 10.67.1.118 -m statistic --mode nth --every 2 --packet 0 -j DNAT --to-destination 10.67.1.118:443
iptables -A PREROUTING -t nat -p tcp --dport 443 -d 10.67.1.118 -j DNAT --to-destination 10.67.4.2:443
```

## Soal 8

```bash
iptables -A INPUT -p tcp --dport 80 -s 10.67.1.104/30 -m time --datestart 2023-12-10 --datestop 2024-02-15 -j DROP
```

## Soal 9

```bash
iptables -N portscan

iptables -A INPUT -m recent --name portscan --update --seconds 600 --hitcount 20 -j DROP
iptables -A FORWARD -m recent --name portscan --update --seconds 600 --hitcount 20 -j DROP

iptables -A INPUT -m recent --name portscan --set -j ACCEPT
iptables -A FORWARD -m recent --name portscan --set -j ACCEPT
```

## Soal 10

```bash
iptables -I INPUT -m recent --name portscan --update --seconds 600 --hitcount 20 -j LOG --log-prefix "Portscan yg terdeteksi: " --log-level 4

iptables -I FORWARD -m recent --name portscan --update --seconds 600 --hitcount 20 -j LOG --log-prefix "Portscan yg terdeteksi: " --log-level 4
```
