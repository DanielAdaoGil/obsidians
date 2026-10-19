C:\Windows\System32>nmap -Pn -sV --script vuln www.ucall.co.ao
Starting Nmap 7.991 ( https://nmap.org ) at 2026-09-13 00:30 +0100
Nmap scan report for www.ucall.co.ao (169.239.78.252)
Host is up (0.010s latency).
rDNS record for 169.239.78.252: webmail.peoplesummitangola.co.ao
Not shown: 993 filtered tcp ports (no-response), 1 filtered tcp ports (admin-prohibited)
PORT    STATE  SERVICE    VERSION
80/tcp  open   http       OpenResty web app server
|_http-server-header: openresty
|_http-dombased-xss: Couldn't find any DOM based XSS.
|_http-csrf: Couldn't find any CSRF vulnerabilities.
|_http-stored-xss: Couldn't find any stored XSS vulnerabilities.
|_http-aspnet-debug: ERROR: Script execution failed (use -d to debug)
|_http-vuln-cve2014-3704: ERROR: Script execution failed (use -d to debug)
110/tcp open   pop3?
113/tcp closed ident
143/tcp open   imap?
179/tcp open   tcpwrapped
443/tcp open   ssl/http   OpenResty web app server
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
|_http-dombased-xss: Couldn't find any DOM based XSS.
|_http-csrf: Couldn't find any CSRF vulnerabilities.
|_http-stored-xss: Couldn't find any stored XSS vulnerabilities.
|_http-majordomo2-dir-traversal: ERROR: Script execution failed (use -d to debug)
|_http-server-header: openresty
|_http-vuln-cve2017-1001000: ERROR: Script execution failed (use -d to debug)

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 521.22 seconds