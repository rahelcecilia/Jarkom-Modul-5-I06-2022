# Jarkom-Modul-5-I06-2022

- Muhammad Naufal Alif - 05111942000008
- Denta Bramasta Hidayat - 5025201116
- Rahel Cecilia Purba - 5025201155

MODUL 5
---
![image](https://user-images.githubusercontent.com/112471006/206718270-9d967a1a-984b-455e-af8d-36f28db16aef.png)
---

## A
![image](https://user-images.githubusercontent.com/112471006/206860750-c20ed1d3-75ef-43ef-9ea7-a23c7c7f3449.png)
<br>Eden is a DNS Server <br>
WISE is DHCP Server <br>
Garden and SSS are Web Servers <br>
The number of hosts on Forger is 62 hosts <br>
Host count on Desmond is 700 hosts <br>
The number of hosts on Blackbell is 255 hosts <br>
The number of hosts on Briar is 200 hosts <br>

## B
VLSM <br>
![image](https://user-images.githubusercontent.com/112471006/206860780-ca471ddc-1ea0-4e0e-bcf5-bea1f2eee331.png)

Tree
![image](https://user-images.githubusercontent.com/112471006/206860866-ae6e3ea8-468b-485a-b376-6c400625b563.png) <br>
![image](https://user-images.githubusercontent.com/112471006/206860860-45b2ad85-5f00-4f73-b624-547b30f32f7a.png)

config ETH
```
Eden 
auto eth0 
iface eth0 inet static 
address 10.39.7.130
netmask 255.255.255.248
gateway 10.39.7.129 
```

WISE 
```
auto eth0 
iface eth0 inet static 
address 10.39.7.131 
netmask 255.255.255.248 
gateway 10.39.7.129 
```

Westalis
```
auto eth0
iface eth0 inet static
address 10.39.7.145
netmask 255.255.255.252
gateway 10.39.7.146
auto eth1
iface eth1 inet static
address 10.39.7.129
netmask 255.255.255.248
auto eth2
iface eth2 inet static
address 10.39.7.1
netmask 255.255.255.128
auto eth3
iface eth3 inet static
address 10.39.0.1
netmask 255.255.252.0
```
Strix
```
auto eth0
iface eth0 inet dhcp
hwaddress ether c6:2a:2d:a8:ff:97 //fix address

auto eth1
iface eth1 inet static
address 10.39.7.146
netmask 255.255.255.252

auto eth2
iface eth2 inet static
address 10.39.7.149
netmask 255.255.255.252
```

Garden
```
auto eth0
iface eth0 inet static
address 10.39.7.138
netmask 255.255.255.248
gateway 10.39.7.137
```

SSS
```
auto eth0
iface eth0 inet static
address 10.39.7.139
netmask 255.255.255.248
gateway 10.39.7.137
```

Ostania
```
auto eth0
iface eth0 inet static
address 10.39.7.150
netmask 255.255.255.252
gateway 10.39.7.149

auto eth1
iface eth1 inet static
address 10.39.7.137
netmask 255.255.255.248

auto eth2
iface eth2 inet static
address 10.39.4.1
netmask 255.255.254.0

auto eth3
iface eth3 inet static
address 10.39.6.1
netmask 255.255.255.0
```

## Routing
`Strix`
```
route add -net 10.39.7.128 netmask 255.255.255.248 gw 10.39.7.145
route add -net 10.39.7.0 netmask 255.255.255.128 gw 10.39.7.145
route add -net 10.39.0.0 netmask 255.255.252.0 gw 10.39.7.145

route add -net 10.39.4.0 netmask 255.255.254.0 gw 10.39.7.150
route add -net 10.39.6.0 netmask 255.255.255.0 gw 10.39.7.150
route add -net 10.39.7.136  netmask 255.255.255.248 gw 10.39.7.150
```

## DHCP
`Forger`, `Desmond`, `Balckbell`, `Briar`
```
auto eth0
iface eth0 inet dhcp
```

`WISE`
```
echo nameserver 192.168.122.1 > /etc/resolv.conf
apt-get update
apt-get install isc-dhcp-server -y
service isc-dhcp-server start

/etc/default/isc-dhcp-server
INTERFACES="eth0"

/etc/dhcp/dhcpd.conf
# Forger A2
subnet 10.39.7.0 netmask 255.255.255.128 {
	range 10.39.7.2 10.39.7.126;
	option routers 10.39.7.1;
	option broadcast-address 10.39.7.127;
	option domain-name-servers 10.39.7.130;
	default-lease-time 600;
	max-lease-time 7200;
}
# Desmond A3
subnet 10.39.0.0 netmask 255.255.252.0 {
	range 10.39.0.2 10.39.3.254;
	option routers 10.39.0.1;
	option broadcast-address 10.39.3.255;
	option domain-name-servers 10.39.7.130;
	default-lease-time 600;
	max-lease-time 7200;
}


# Blackbell A6
subnet 10.39.4.0 netmask 255.255.254.0 {
	range 10.39.4.2 10.39.5.254;
	option routers 10.39.4.1;
	option broadcast-address 10.39.5.255;
	option domain-name-servers 10.39.7.130;
	default-lease-time 600;
	max-lease-time 7200;
}


# Briar A7
subnet 10.39.6.0 netmask 255.255.255.0 {
	range 10.39.6.2 10.39.6.254;
	option routers 10.39.6.1;
	option broadcast-address 10.39.6.255;
	option domain-name-servers 10.39.7.130;
	default-lease-time 600;
	max-lease-time 7200;
}

# Routing from WISE to router
subnet 10.39.7.128 netmask 255.255.255.248 {
        option routers 10.39.7.129;
}
```

## DNS Eden
```
echo nameserver 192.168.122.1 > /etc/resolv.conf
apt-get update
apt-get install bind9 -y
service bind9 restart

/etc/bind/named.conf.options
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
        //dnssec-validation auto;
        allow-query{any;};

        auth-nxdomain no;    # conform to RFC1035
				listen-on-v6 { any; };
};
```
## Relay
`Westalis`, `Ostania`
```
echo nameserver 192.168.122.1 > /etc/resolv.conf
apt-get update
apt-get install isc-dhcp-relay -y
service isc-dhcp-relay restart



/etc/default/isc-dhcp-relay
# What servers should the DHCP relay forward requests to?
SERVERS="10.39.7.131"

# On what interfaces should the DHCP relay (dhrelay) serve DHCP requests?
INTERFACES="eth0 eth1 eth2 eth3"

# Additional options that are passed to the DHCP relay daemon?
OPTIONS=""
```




