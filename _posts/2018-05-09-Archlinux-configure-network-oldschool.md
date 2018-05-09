---
layout: post
title:  "Archlinux : configure network in the oldschool way."
date:   2018-05-09 22:00:29 +0200
categories: linux admin
---

After a fresh install and its reboot, Archlinux do not have any
network manager or dhcp client. So it is needed to configure a
static ip configuration

with :

* 192.168.3.25 the ip address we want to use
* 192.168.3.1 the address of the gateway
* 192.168.3.1 the address of the nameserver

```
ip address add 192.168.3.25/24 dev eth0
ip link set eth0 up
ip route add default via 192.168.3.1
echo "nameserver 192.168.3.1" > /etc/resolv.conf
```
