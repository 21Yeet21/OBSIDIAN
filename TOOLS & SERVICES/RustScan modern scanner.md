
downloaded deb file from https://github.com/bee-san/RustScan/releases 
then run unzip and dpkg -i and thats it

Here's a structured breakdown of RustScan's Scripting Engine (RSE) functionality for quick reference:

---

## **🚀 RustScan Scripting Engine (RSE) Cheat Sheet**

### **🔧 Key Features**
- **Post-scan automation**: Execute scripts after port scanning.
- **Multi-language support**: Python, Shell, Perl, or any `$PATH` binary.
- **Tag-based filtering**: Run scripts only for specific ports/services.

---

### **⚙️ Setup & Usage**
#### **1. Enable Scripts**
| Argument    | Behavior                                  |
|-------------|-------------------------------------------|
| `--scripts=None`    | Disable all scripts.                     |
| `--scripts=Custom`  | Run all scripts in `~/.rustscan_scripts/`.|
| `--scripts=Default` | Run Nmap (default behavior).              |

#### **2. Configure Scripts**
- **Config File**: `~/.rustscan_scripts.toml`
  ```toml
  tags = ["http", "approved"]  # Only run scripts with these tags
  ports = ["80", "443"]        # Trigger only for these ports
  ```

#### **3. Script Metadata (Python Example)**
```python
#!/usr/bin/python3
#tags = ["http", "approved"]
#developer = "your_name"
#trigger_port = "80"
#call_format = "python3 {{script}} {{ip}} {{port}}"

import sys
print(f"Scanning {sys.argv[1]}:{sys.argv[2]}")
```

---

### **📜 Script Templates**
#### **Python**
```python
#!/usr/bin/python3
#tags = ["demo"]
#trigger_port = "22"
#call_format = "python3 {{script}} {{ip}} {{port}}"

import requests
ip, port = sys.argv[1], sys.argv[2]
response = requests.get(f"http://{ip}:{port}")
print(response.headers)
```

#### **Shell (Nmap Wrapper)**
```bash
#!/bin/bash
#tags = ["nmap"]
#call_format = "bash {{script}} {{ip}} {{port}}"

nmap -sV -p {{port}} {{ip}}
```

---

### **🎯 Practical Use Cases**
1. **Automate Nmap Scans**  
   ```bash
   rustscan -a 10.0.0.1 --scripts=Default
   ```

2. **Run HTTP Enumeration**  
   - Save a Python script with `tags = ["http"]`.
   - RustScan auto-executes it when ports 80/443 are open.

3. **Integrate GoBuster**  
   ```bash
   #!/bin/bash
   gobuster dir -u http://{{ip}} -w /usr/share/wordlists/dirb/common.txt
   ```

---

### **💡 Pro Tips**
- **Debugging**: Use `-vv` flag to see script execution logs.
- **Contributing**: Submit scripts to [RustScan’s GitHub](https://github.com/RustScan/RustScan).
- **Security**: Audit third-party scripts before running (`--scripts=Custom`).

---

### **❗ Limitations**
- **No parallel execution**: Scripts run sequentially.
- **No output parsing**: Scripts must handle their own output.

---

> 🟢 **Example**: Scan + auto-enumerate HTTP with one command:  
> ```bash
> rustscan -a 10.0.0.1 --scripts=Custom
> ```

**Happy automating!** 🤖🔍  

*(Remember: Always test scripts in a lab environment first.)*

Here's a concise, action-oriented summary of **RustScan** commands for your TryHackMe room:

---

## **🚀 RustScan Cheat Sheet**  
*Blazing-fast port scanner + Nmap automation*

### **🔧 Basic Syntax**
```bash
rustscan -a <TARGET_IP> -- <NMAP_ARGS>
# Example:
rustscan -a 10.10.10.10 -- -A -sV
```

---

### **🎯 Target Specification**
| Command | Description |
|---------|-------------|
| `-a 192.168.1.1` | Scan single IP |
| `-a 192.168.1.1,10.0.0.1` | Scan multiple IPs |
| `-a hosts.txt` | Scan IPs/hosts from file (one per line) |
| `-a 192.168.1.0/24` | CIDR range scan |
| `-a example.com` | Scan a domain |

---

### **🔎 Port Selection**
| Command | Description |
|---------|-------------|
| `-p 80` | Scan single port |
| `-p 80,443,8080` | Scan multiple ports |
| `--range 1-1000` | Scan port range |
| `--top-ports 100` | Scan top N common ports |
| `--scan-order "Random"` | Evade firewalls with random port order |

---

### **⚡ Nmap Integration**
```bash
# Default (runs `nmap -Pn -p <PORTS> <IP>`):
rustscan -a 10.10.10.10  

# Custom Nmap flags (after `--`):
rustscan -a 10.10.10.10 -- -A -sV -sC -oN scan.txt
```
*Equivalent to:*  
`nmap -Pn -vvv -p <OPEN_PORTS> -A -sV 10.10.10.10`

---

### **💡 Pro Tips**
1. **Speed vs Stealth**:  
   - `-t 5000` → Faster scans (more concurrent threads).  
   - `--scan-order "Random"` → Stealthier scans.  
2. **Output Formats**: Pipe results to files:  
   ```bash
   rustscan -a 10.10.10.10 | tee rustscan.txt
   ```
3. **Combine with other tools**:  
   ```bash
   rustscan -a 10.10.10.10 -p 80,443 -- -sV | grep "open" | cut -d'/' -f1 | xargs -I{} gobuster dir -u http://10.10.10.10:{} -w wordlist.txt
   ```

---

### **📌 Example Workflow**
1. **Fast full scan**:  
   ```bash
   rustscan -a 10.10.10.10 --range 1-65535
   ```
2. **Deep scan open ports**:  
   ```bash
   rustscan -a 10.10.10.10 -- -A -sC -oN full_scan.txt
   ```
3. **HTTP-focused scan**:  
   ```bash
   rustscan -a 10.10.10.10 -p 80,443,8080 -- -sV --script=http-title
   ```

---

> 🟢 **Remember**: RustScan finds open ports → Nmap handles service detection. Always review Nmap results for vulnerabilities!

**Happy hacking!** 🔍💻