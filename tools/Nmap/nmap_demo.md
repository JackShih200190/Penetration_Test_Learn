## nmap指令實作

1. Kali < == > WinServer 2008
2. 雙方都ping得到對方


加快掃描速度(default:T3)
-T4 禁止動態 TCP Port 掃描延遲超過 10 ms
-T5 條件過於嚴苛會失去準度
```
# nmap -T4 192.168.111.130
Starting Nmap 7.92 ( https://nmap.org ) at 2022-03-18 13:10 EDT
Nmap scan report for 192.168.111.130
Host is up (0.0014s latency).
Not shown: 978 closed tcp ports (reset)
PORT      STATE SERVICE
22/tcp    open  ssh
135/tcp   open  msrpc
139/tcp   open  netbios-ssn
445/tcp   open  microsoft-ds
3306/tcp  open  mysql
3389/tcp  open  ms-wbt-server
4848/tcp  open  appserv-http
7676/tcp  open  imqbrokerd
8009/tcp  open  ajp13
8022/tcp  open  oa-system
8031/tcp  open  unknown
8080/tcp  open  http-proxy
8181/tcp  open  intermapper
8383/tcp  open  m2mservices
8443/tcp  open  https-alt
9200/tcp  open  wap-wsp
49152/tcp open  unknown
49153/tcp open  unknown
49154/tcp open  unknown
49155/tcp open  unknown
49156/tcp open  unknown
49159/tcp open  unknown
MAC Address: 00:0C:29:1B:60:89 (VMware)

Nmap done: 1 IP address (1 host up) scanned in 1.51 seconds
``` 

![image](https://user-images.githubusercontent.com/55253641/159050975-a1c7f776-5af4-47aa-95ae-91a71301e00e.png)
