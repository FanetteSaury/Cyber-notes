#THM #Cybersecurity101-Networking #Cybersecurity101-NetworkingCoreProtocols
# Domain Name System
video 📹 : https://www.youtube.com/watch?v=HnUDtycXSNE, https://youtube.com/shorts/5ZCvW1XSX_E?feature=shared
- Layer 7 ISO OSI
- Traffic
	- default UDP port 53
	- default fallback TCP port 53
## DNS Records
### Types
### A record
The A (Address) record maps a hostname to one or more IPv4 addresses. 
For example, you can set `example.com` to resolve to `172.17.2.172`.
### AAAA record
A record is for IPv4, AAAA is for IPv6.
*💡AAAA comme pour l'andouillette*
### CNAME record
Canonical Name
Mapping domain name to another domain name.
For example, `www.example.com` can be mapped to `example.com` or even to `example.org`.
### MX record
The MX (Mail Exchange) record specifies the mail server responsible for handling emails for a domain.
### Looking up with nslookup
If you want to look up the IP address of a domain from the command line, you can use a tool such as `nslookup`. Consider the example in the terminal below where we look up `example.com`.

```shell-session
user@TryHackMe$ nslookup www.example.com
Server:         127.0.0.53
Address:        127.0.0.53#53

Non-authoritative answer:
Name:   www.example.com
Address: 93.184.215.14
Name:   www.example.com
Address: 2606:2800:21f:cb07:6820:80da:af6b:8b2c
```
