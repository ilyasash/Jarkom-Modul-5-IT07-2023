# Praktikum Modul 5 Jaringan Komputer - Firewall 

Praktikum Modul 5 Jaringan Komputer - **IT07**

## Authors

| Nama                                                | NRP        |
| --------------------------------------------------- | ---------- |
| [Rangga Aldo](https://www.github.com/ranggaaldosas) | 5027211059 |
| [Maulana Ilyasa](https://www.github.com/ilyasahsh)        | 5027211065 |

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
    <img src="https://i.ibb.co/wszLsR3/image.png">


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
