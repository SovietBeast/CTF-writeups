# Nmap

```bash
Starting Nmap 7.92 ( https://nmap.org ) at 2022-03-12 12:51 EST                                                                                                                                   
Nmap scan report for challs.dvc.tf (138.68.106.171)                                                                                                                                               
Host is up (0.0060s latency).                                                                                                                                                                     
Not shown: 1000 filtered tcp ports (no-response)                                                                                                                                                  
PORT      STATE SERVICE VERSION                                                                                                                                                                   
51022/tcp open  ssh     OpenSSH 7.2p2 Ubuntu 4ubuntu2.10 (Ubuntu Linux; protocol 2.0)                                                                                                             
| ssh-hostkey:                                                                                                                                                                                    
|   2048 61:94:04:6e:f3:e6:22:f1:74:2b:f3:d2:62:82:bb:f1 (RSA)                                                                                                                                    
|   256 69:6b:8f:f8:49:b1:a6:1d:87:64:a0:bc:4f:c8:77:d7 (ECDSA)                                                                                                                                   
|_  256 1c:25:bf:62:06:89:a1:f1:ac:99:25:d9:96:9c:f8:de (ED25519)                                                                                                                                 
Warning: OSScan results may be unreliable because we could not find at least 1 open and 1 closed port                                                                                             
Device type: bridge|VoIP phone|general purpose|WAP|broadband router|specialized                                                                                                                   
Running (JUST GUESSING): Oracle Virtualbox (92%), Cisco embedded (89%), Linux 1.0.X (88%), QEMU (88%), Sitecom embedded (87%), ZyXEL embedded (87%), Casio embedded (87%), GNU Hurd (85%)         
OS CPE: cpe:/o:oracle:virtualbox cpe:/h:cisco:unified_ip_phone_7912 cpe:/o:linux:linux_kernel:1.0.9 cpe:/a:qemu:qemu cpe:/h:sitecom:wl-174 cpe:/h:zyxel:b-3000 cpe:/h:zyxel:prestige_660r cpe:/o:g
nu:hurd                                                                                                                                                                                           
Aggressive OS guesses: Oracle Virtualbox (92%), Cisco IP Phone 7912-series (89%), Linux 1.0.9 (88%), QEMU user mode network gateway (88%), Sitecom WL-174 wireless ADSL router or ZyXEL B-3000 WAP
 (87%), ZyXEL Prestige 660R ADSL router (87%), Casio QT-6000 or QT-6100 point-of-sale machine (87%), GNU Hurd 0.3 (85%)                                                                           
No exact OS matches for host (test conditions non-ideal).                                                                                                                                         
Network Distance: 2 hops                                                                                                                                                                          
Service Info: OS: Linux; CPE: cpe:/o:linux:linux_kernel                                                                                                                                           
                                                                                                                                                                                                  
TRACEROUTE (using port 80/tcp)                                                                                                                                                                    
HOP RTT     ADDRESS                                                                                                                                                                               
1   1.40 ms 10.0.2.2                                                                                                                                                                              
2   1.42 ms 138.68.106.171                                                                                                                                                                        

OS and Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 26.95 seconds
```

There is `ssh` service running.

# Website

Website contained some sort of Top Song list, and used two `GET` parameters to filter it.

![image](https://user-images.githubusercontent.com/44019881/158075122-47a8a62b-5faf-4559-98aa-35085fc78ff5.png)

When changing parameter `playlistTop` to something nonexistent like `asdf` server returned error.

![image](https://user-images.githubusercontent.com/44019881/158075127-e9511a2c-728b-482d-a3fe-ea2bebde8f33.png)

Using `php://filter/convert.bse64-encode/resource=` local file inclusion was performed.

![image](https://user-images.githubusercontent.com/44019881/158075138-54d89bb4-b90f-47ca-94b0-ac5c69823378.png)

![image](https://user-images.githubusercontent.com/44019881/158075143-91c3b4be-cae8-413f-a0bb-f74f93db598a.png)

This allowed to read `leonardo` user `private ssh` key.

![image](https://user-images.githubusercontent.com/44019881/158075151-26c845e9-4a26-43dc-bbbc-e6d4cf190ad9.png)

# SSH Connection

Using all obtained information login as user `leonardo` via SSH was possible
![image](https://user-images.githubusercontent.com/44019881/158075157-84e8136c-b29d-4b39-b567-0a4447e3aac4.png)
