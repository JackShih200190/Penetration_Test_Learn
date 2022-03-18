## nmap指令實作

1. Kali < == > WinServer 2008
2. 雙方都ping得到對方


## 加快掃描速度(default:T3)
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

## Port Scan

-sS 參數代表掃描技術是 TCP SYN Scan    (效率較差)

-sT 參數代表掃描技術是 TCP Connect Scan，掃描時會呼叫作業系統的 System Call Connect API，以送出刺探封包  (效率較佳)
```
nmap -T4 -sT -p 1-65535 192.168.111.130
Starting Nmap 7.92 ( https://nmap.org ) at 2022-03-18 13:16 EDT
Nmap scan report for 192.168.111.130
Host is up (0.00045s latency).
Not shown: 65489 closed tcp ports (conn-refused)
PORT      STATE SERVICE
22/tcp    open  ssh
135/tcp   open  msrpc
139/tcp   open  netbios-ssn
445/tcp   open  microsoft-ds
1617/tcp  open  nimrod-agent
3306/tcp  open  mysql
3389/tcp  open  ms-wbt-server
3700/tcp  open  lrs-paging
3820/tcp  open  scp
4848/tcp  open  appserv-http
5985/tcp  open  wsman
7676/tcp  open  imqbrokerd
8009/tcp  open  ajp13
8019/tcp  open  qbdb
8020/tcp  open  intu-ec-svcdisc
8022/tcp  open  oa-system
8027/tcp  open  papachi-p2p-srv
8028/tcp  open  unknown
8031/tcp  open  unknown
8032/tcp  open  pro-ed
8080/tcp  open  http-proxy
8181/tcp  open  intermapper
8282/tcp  open  libelle
8383/tcp  open  m2mservices
8443/tcp  open  https-alt
8444/tcp  open  pcsync-http
8484/tcp  open  unknown
8585/tcp  open  unknown
8686/tcp  open  sun-as-jmxrmi
9200/tcp  open  wap-wsp
9300/tcp  open  vrace
47001/tcp open  winrm
49152/tcp open  unknown
49153/tcp open  unknown
49154/tcp open  unknown
49155/tcp open  unknown
49156/tcp open  unknown
49159/tcp open  unknown
49166/tcp open  unknown
49207/tcp open  unknown
49219/tcp open  unknown
49232/tcp open  unknown
49233/tcp open  unknown
49432/tcp open  unknown
49435/tcp open  unknown
49436/tcp open  unknown
MAC Address: 00:0C:29:1B:60:89 (VMware)

Nmap done: 1 IP address (1 host up) scanned in 47.15 seconds
```

## 服務的詳細版本

```
nmap -T4 -sV 192.168.111.130                                                                                                               130 ⨯
Starting Nmap 7.92 ( https://nmap.org ) at 2022-03-18 13:22 EDT
Nmap scan report for 192.168.111.130
Host is up (0.00038s latency).
Not shown: 977 closed tcp ports (reset)
PORT      STATE SERVICE              VERSION
22/tcp    open  ssh                  OpenSSH 7.1 (protocol 2.0)
135/tcp   open  msrpc                Microsoft Windows RPC
139/tcp   open  netbios-ssn          Microsoft Windows netbios-ssn
445/tcp   open  microsoft-ds         Microsoft Windows Server 2008 R2 - 2012 microsoft-ds
3306/tcp  open  mysql                MySQL 5.5.20-log
3389/tcp  open  ms-wbt-server?
3920/tcp  open  ssl/exasoftport1?
4848/tcp  open  ssl/http             Oracle Glassfish Application Server
7676/tcp  open  java-message-service Java Message Service 301
8009/tcp  open  ajp13                Apache Jserv (Protocol v1.3)
8022/tcp  open  http                 Apache Tomcat/Coyote JSP engine 1.1
8031/tcp  open  ssl/unknown
8080/tcp  open  http                 Sun GlassFish Open Source Edition  4.0
8181/tcp  open  ssl/intermapper?
8383/tcp  open  http                 Apache httpd
8443/tcp  open  ssl/https-alt?
9200/tcp  open  wap-wsp?
49152/tcp open  msrpc                Microsoft Windows RPC
49153/tcp open  msrpc                Microsoft Windows RPC
49154/tcp open  msrpc                Microsoft Windows RPC
49155/tcp open  unknown
49156/tcp open  msrpc                Microsoft Windows RPC
49159/tcp open  java-rmi             Java RMI
2 services unrecognized despite returning data. If you know the service/version, please submit the following fingerprints at https://nmap.org/cgi-bin/submit.cgi?new-service :
==============NEXT SERVICE FINGERPRINT (SUBMIT INDIVIDUALLY)==============
SF-Port8181-TCP:V=7.92%T=SSL%I=7%D=3/18%Time=6234C005%P=x86_64-pc-linux-gn
SF:u%r(GetRequest,128C,"HTTP/1\.1\x20200\x20OK\r\nDate:\x20Fri,\x2018\x20M
SF:ar\x202022\x2017:23:18\x20GMT\r\nContent-Type:\x20text/html\r\nConnecti
SF:on:\x20close\r\nContent-Length:\x204626\r\n\r\n<!DOCTYPE\x20HTML\x20PUB
SF:LIC\x20\"-//W3C//DTD\x20HTML\x204\.01\x20Transitional//EN\">\n<html\x20
SF:lang=\"en\">\n<!--\nDO\x20NOT\x20ALTER\x20OR\x20REMOVE\x20COPYRIGHT\x20
SF:NOTICES\x20OR\x20THIS\x20HEADER\.\n\nCopyright\x20\(c\)\x202010,\x20201
SF:3\x20Oracle\x20and/or\x20its\x20affiliates\.\x20All\x20rights\x20reserv
SF:ed\.\n\nUse\x20is\x20subject\x20to\x20License\x20Terms\n-->\n<head>\n<s
SF:tyle\x20type=\"text/css\">\n\tbody{margin-top:0}\n\tbody,td,p,div,span,
SF:a,ul,ul\x20li,\x20ol,\x20ol\x20li,\x20ol\x20li\x20b,\x20dl,h1,h2,h3,h4,
SF:h5,h6,li\x20{font-family:geneva,helvetica,arial,\"lucida\x20sans\",sans
SF:-serif;\x20font-size:10pt}\n\th1\x20{font-size:18pt}\n\th2\x20{font-siz
SF:e:14pt}\n\th3\x20{font-size:12pt}\n\tcode,kbd,tt,pre\x20{font-family:mo
SF:naco,courier,\"courier\x20new\";\x20font-size:10pt;}\n\tli\x20{padding-
SF:bottom:\x208px}\n\tp\.copy,\x20p\.copy\x20a\x20{font-family:geneva,helv
SF:etica,arial,\"lucida\x20sans\",sans-serif;\x20font-size:8pt}\n\tp\.copy
SF:\x20{text-align:\x20center}\n\ttable\.grey1,tr\.grey1,td\.g")%r(HTTPOpt
SF:ions,7A,"HTTP/1\.1\x20405\x20Method\x20Not\x20Allowed\r\nAllow:\x20GET\
SF:r\nDate:\x20Fri,\x2018\x20Mar\x202022\x2017:23:18\x20GMT\r\nConnection:
SF:\x20close\r\nContent-Length:\x200\r\n\r\n")%r(RTSPRequest,76,"HTTP/1\.1
SF:\x20505\x20HTTP\x20Version\x20Not\x20Supported\r\nDate:\x20Fri,\x2018\x
SF:20Mar\x202022\x2017:23:18\x20GMT\r\nConnection:\x20close\r\nContent-Len
SF:gth:\x200\r\n\r\n");
==============NEXT SERVICE FINGERPRINT (SUBMIT INDIVIDUALLY)==============
SF-Port9200-TCP:V=7.92%I=7%D=3/18%Time=6234BFF9%P=x86_64-pc-linux-gnu%r(Ge
SF:tRequest,18C,"HTTP/1\.0\x20200\x20OK\r\nContent-Type:\x20application/js
SF:on;\x20charset=UTF-8\r\nContent-Length:\x20309\r\n\r\n{\r\n\x20\x20\"st
SF:atus\"\x20:\x20200,\r\n\x20\x20\"name\"\x20:\x20\"Alpha\x20Ray\",\r\n\x
SF:20\x20\"version\"\x20:\x20{\r\n\x20\x20\x20\x20\"number\"\x20:\x20\"1\.
SF:1\.1\",\r\n\x20\x20\x20\x20\"build_hash\"\x20:\x20\"f1585f096d3f3985e73
SF:456debdc1a0745f512bbc\",\r\n\x20\x20\x20\x20\"build_timestamp\"\x20:\x2
SF:0\"2014-04-16T14:27:12Z\",\r\n\x20\x20\x20\x20\"build_snapshot\"\x20:\x
SF:20false,\r\n\x20\x20\x20\x20\"lucene_version\"\x20:\x20\"4\.7\"\r\n\x20
SF:\x20},\r\n\x20\x20\"tagline\"\x20:\x20\"You\x20Know,\x20for\x20Search\"
SF:\r\n}\n")%r(HTTPOptions,4F,"HTTP/1\.0\x20200\x20OK\r\nContent-Type:\x20
SF:text/plain;\x20charset=UTF-8\r\nContent-Length:\x200\r\n\r\n")%r(RTSPRe
SF:quest,4F,"HTTP/1\.1\x20200\x20OK\r\nContent-Type:\x20text/plain;\x20cha
SF:rset=UTF-8\r\nContent-Length:\x200\r\n\r\n")%r(FourOhFourRequest,A9,"HT
SF:TP/1\.0\x20400\x20Bad\x20Request\r\nContent-Type:\x20text/plain;\x20cha
SF:rset=UTF-8\r\nContent-Length:\x2080\r\n\r\nNo\x20handler\x20found\x20fo
SF:r\x20uri\x20\[/nice%20ports%2C/Tri%6Eity\.txt%2ebak\]\x20and\x20method\
SF:x20\[GET\]")%r(SIPOptions,4F,"HTTP/1\.1\x20200\x20OK\r\nContent-Type:\x
SF:20text/plain;\x20charset=UTF-8\r\nContent-Length:\x200\r\n\r\n");
MAC Address: 00:0C:29:1B:60:89 (VMware)
Service Info: OSs: Windows, Windows Server 2008 R2 - 2012; CPE: cpe:/o:microsoft:windows

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 166.24 seconds
```
