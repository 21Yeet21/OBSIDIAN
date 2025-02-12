## Nmap EXPLANATION

to look for **scripts**
- grep "ftp-anon" /usr/share/nmap/scripts/script.db  


good tcp aggressive scan and saving the file on current dir named : nmapthm
 
- └─$ sudo nmap -p- -A -T5 -sT 10.10.212.180  -oN nmapthm

also this works fine and simple using syn scan

- nmap -vv  -T5 -oN NmapScan -p- 10.10.147.81

after getting open ports you need to scan specific port like this in order to foxus on it

	sudo nmap -A -T4 -vv -p 8012 -oN NmapPortScan 10.10.147.81

Explanation of Changes:

- Removed `-sT`: It's unnecessary unless a full TCP connect scan is specifically needed.
- Removed `-sC`: It's included in `-A`.
- Adjusted `-T5` to `-T4`: `-T4` is fast but more reliable and less likely to cause issues with firewalls.


did an nmap scan 

found one open port now focus on it

**import**
	PORT     STATE SERVICE REASON  VERSION
	8012/tcp open  unknown syn-ack
	| fingerprint-strings: 
	|   DNSStatusRequestTCP, DNSVersionBindReqTCP, FourOhFourRequest, GenericLines, GetRequest, HTTPOptions, Help, Kerberos, LANDesk-RC, LDAPBindReq, LDAPSearchReq, LPDString, NCP, NULL, RPCCheck, RTSPRequest, SIPOptions, SMBProgNeg, SSLSessionReq, TLSSessionReq, TerminalServer, TerminalServerCookie, X11Probe: 
	|_    SKIDY'S BACKDOOR. Type .HELP to view commands


that scan says that this can be used ass a backdoor .   SKIDY'S BACKDOO.

