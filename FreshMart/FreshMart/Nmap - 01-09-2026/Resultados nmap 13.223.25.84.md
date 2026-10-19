C:\Windows\System32>nmap -sV -Pn freshmart.net
Starting Nmap 7.991 ( https://nmap.org ) at 2026-09-01 19:42 +0100
Warning: Hostname freshmart.net resolves to 4 IPs. Using 13.223.25.84.
Nmap scan report for freshmart.net (13.223.25.84)
Host is up (0.14s latency).
Other addresses for freshmart.net (not scanned): 2600:1f18:4ae:c605:dd5d:b838:5816:d7fb 2600:1f18:4ae:c606:78d4:4260:db4e:aeee 54.243.117.197
rDNS record for 13.223.25.84: ec2-13-223-25-84.compute-1.amazonaws.com
Not shown: 997 filtered tcp ports (no-response), 1 filtered tcp ports (admin-prohibited)
PORT    STATE SERVICE VERSION
80/tcp  open  http    Microsoft Kestrel httpd
443/tcp open  https?

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 63.04 seconds
