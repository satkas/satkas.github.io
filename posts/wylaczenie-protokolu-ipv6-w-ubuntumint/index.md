<!--
.. title: Wyłączenie protokołu ipv6 w Ubuntu/Mint
.. slug: wylaczenie-protokolu-ipv6-w-ubuntumint
.. date: 2018-04-22
.. tags: linux, bash
.. category: tech
.. link: 
.. description: 
.. type: text
-->

W konsoli sprawdzamy czy jest włączony ipv6

```sh

1: lo: <LOOPBACK,UP,LOWER_UP> mtu 65536 qdisc noqueue state UNKNOWN group default qlen 1000
    link/loopback 00:00:00:00:00:00 brd 00:00:00:00:00:00
    inet 127.0.0.1/8 scope host lo
       valid_lft forever preferred_lft forever
    inet6 ::1/128 scope host
       valid_lft forever preferred_lft forever
2: enp1s0: <NO-CARRIER,BROADCAST,MULTICAST,UP> mtu 1500 qdisc mq state DOWN group default qlen 1000
    link/ether 88:ae:1d:7c:af:4c brd ff:ff:ff:ff:ff:ff
3: wlp2s0: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc noqueue state UP group default qlen 1000
    link/ether 5c:ac:4c:77:43:aa brd ff:ff:ff:ff:ff:ff
    inet 192.168.88.254/24 brd 192.168.88.255 scope global dynamic wlp2s0
       valid_lft 1185sec preferred_lft 1185sec
    inet6 fe80::8058:8160:b21a:b193/64 scope link
       valid_lft forever preferred_lft forever

```

Jak widać protokół ipv6 jest włączony (czerwona czcionka)

Przystępujemy do wyłączenia protokołu ipv6

Edytujemy plik /etc/sysctl.conf i dopisujemy odpowiednie wpisy na końcu pliku

```sh

net.ipv6.conf.all.disable_ipv6 = 1
net.ipv6.conf.default.disable_ipv6 = 1
net.ipv6.conf.lo.disable_ipv6 = 1

```

Aby zmiany weszły w "życie" natychmiast, wykonujemy komendę w konsoli:

```sh

sudo sysctl -p

```

Sprawdzamy czy zmiany weszły w "życie".

```sh

$ ip a
1: lo: <LOOPBACK,UP,LOWER_UP> mtu 65536 qdisc noqueue state UNKNOWN group default qlen 1000
    link/loopback 00:00:00:00:00:00 brd 00:00:00:00:00:00
    inet 127.0.0.1/8 scope host lo
       valid_lft forever preferred_lft forever
2: enp1s0: <NO-CARRIER,BROADCAST,MULTICAST,UP> mtu 1500 qdisc mq state DOWN group default qlen 1000
    link/ether 88:ae:1d:7c:af:4c brd ff:ff:ff:ff:ff:ff
3: wlp2s0: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc noqueue state UP group default qlen 1000
    link/ether 5c:ac:4c:77:43:aa brd ff:ff:ff:ff:ff:ff
    inet 192.168.88.254/24 brd 192.168.88.255 scope global dynamic wlp2s0
       valid_lft 821sec preferred_lft 821sec

```
