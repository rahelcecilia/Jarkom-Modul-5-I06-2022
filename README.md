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
<br>Eden is a DNS Server
WISE is DHCP Server
Garden and SSS are Web Servers
The number of hosts on Forger is 62 hosts
Host count on Desmond is 700 hosts
The number of hosts on Blackbell is 255 hosts
The number of hosts on Briar is 200 hosts

## B
VLSM <br>
![image](https://user-images.githubusercontent.com/112471006/206860780-ca471ddc-1ea0-4e0e-bcf5-bea1f2eee331.png)

Tree
![image](https://user-images.githubusercontent.com/112471006/206860866-ae6e3ea8-468b-485a-b376-6c400625b563.png) <br>
![image](https://user-images.githubusercontent.com/112471006/206860860-45b2ad85-5f00-4f73-b624-547b30f32f7a.png)




## No 1
In order for your topology to have external access, you are required to configure Strix using iptables, but Loid doesn't want to use MASQUERADE.

## No 2
You are asked to drop all TCP and UDP from outside your topology on a server which is a DHCP server in order to maintain security.

## No 3
Loid asks you to limit DHCP and DNS servers to only receive a maximum of 2 ICMP connections simultaneously using iptables, the rest are dropped.

## No 4
Access to the Web Server is only permitted during working hours, namely Monday to Friday at 07.00 - 16.00.

## No 5
Because we have 2 Web Servers, Loid wants Ostania to be arranged so that every request from a client accessing Garden with port 80 will be distributed alternately to SSS and Garden respectively and requests from clients accessing SSS with port 443 will be distributed alternately to Garden and SSS sequentially.

## No 6
Because Loid wants to know what packets were dropped, each server and router node added logging packets that were dropped at the standard syslog level.

Loid berterima kasih pada kalian karena telah membantunya. Loid juga mengingatkan agar semua aturan iptables harus disimpan pada sistem atau paling tidak kalian menyediakan script sebagai backup.
