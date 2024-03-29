```bash
sshuttle -r root@10.200.109.200 10.200.109.0/24 -e "ssh -i wreath_pkey" -x 10.200.x.200

```

================================================================================================================

Port forwarding is accomplished with the -L switch, which creates a link to a Local port. For example, if we had SSH access to 172.16.0.5 and there's a webserver running on 172.16.0.10, we could use this command to create a link to the server on 172.16.0.10:
```bash

ssh -L 8000:10.200.73.150:80 root@10.200.73.200 -fN

```
We could then access the website on 172.16.0.10 (through 172.16.0.5) by navigating to port 8000 on our own attacking machine. 


===============================================================================================================

If you had SSH access to a server (172.16.0.50) with a webserver running internally on port 80 (i.e. only accessible to the server itself on 127.0.0.1:80
```bash
ssh -L 8000:127.0.0.1:80 user@172.16.0.50 -fN
```



==========================================copy over ssh=====================================================
```bash
scp -i ~/.ssh/id_rsa /desktop/pic.png user@10.0.0.23:/usr/bin/pic.png
```
