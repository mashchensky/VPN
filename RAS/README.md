# 2. RAS на базе OpenVPN

После разворачивания стенда поднимется вм server с ip 192.168.11.10 с запущенным OpenVPN сервером.
Для подключения к VPN скачать файлы из папки [client](client) и из этой папки на хосте выполнить команду:

```
sudo openvpn --config client.conf
```

После этого произойдет подключение к VPN серверу. Для проверки работоспособности можно выполнить ping:

```
ping -c 4 10.10.10.1
```

Так же проверяем, что сеть туннеля импортирована в таблицу маршрутизации:

```
ip r

default via 192.168.1.1 dev enp7s0 proto dhcp metric 100 
10.10.10.0/24 via 10.10.10.5 dev tun0 
10.10.10.5 dev tun0 proto kernel scope link src 10.10.10.6 
169.254.0.0/16 dev enp7s0 scope link metric 1000 
172.17.0.0/16 dev docker0 proto kernel scope link src 172.17.0.1 linkdown 
172.18.0.0/16 dev br-ae60d272a703 proto kernel scope link src 172.18.0.1 linkdown 
192.168.1.0/24 dev enp7s0 proto kernel scope link src 192.168.1.8 metric 100 
192.168.10.0/24 dev vboxnet2 proto kernel scope link src 192.168.10.1 linkdown 
192.168.11.0/24 dev vboxnet0 proto kernel scope link src 192.168.11.1
```