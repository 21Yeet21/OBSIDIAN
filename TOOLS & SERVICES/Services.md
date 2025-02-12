
## SMB


### Syntax:

```bash
smbclient //[IP]/[SHARE] -U [name] -p [port]
```

- **-U [name]**: Specify the username
- **-p [port]**: Specify the port
- no -p == default port

this  opens the txt file in SMB server !

smb: \>  more "Working From Home Information.txt" 

## SSH
so imortant its like your password:
id_rsa 

its a public key can find in it the username
id_rsa.pub

then we can use and dont forget to do chmod 600 id_rsa

```
- ssh  -i ./id_rsa username@hostip
```

to connect

## Telnet

You can connect to a telnet server with the following syntax: **"telnet ip port"**
elnet Exploit Summary

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



## FTP

###### **Types of FTP Exploits**

FTP, like Telnet, is vulnerable due to the fact that both the **command** and **data channels** transmit data in **plaintext**. This can allow attackers to intercept sensitive information, such as passwords, especially if a **man-in-the-middle (MITM)** attack occurs.

**Key FTP Exploit:**

- **Man-in-the-Middle (MITM) Attack**: Since FTP data is unencrypted, an attacker could use techniques like **ARP Poisoning** to intercept sensitive data (including passwords) sent during the FTP session.

**FTP Server Misconfiguration:**

- One common exploit is when FTP servers use **weak or default passwords**, which attackers can exploit through **brute-force** attacks.

---

###### **Method Breakdown for Brute-Forcing FTP Passwords**

From the information gathered during enumeration, we know that:

- An **FTP server** is running.
- We have a **possible username**.

With this, we can try to brute-force the FTP password using tools like **Hydra**.




## NFS 

### NFS (Network File System) Summary

**What is NFS?**  
NFS is a protocol that allows file systems on a network to be shared between machines. It enables a client to access files on a remote server as if they were local files.

**How to Enumerate NFS?**

1. **Scan for NFS service**: Use Nmap to scan for open ports (e.g., `2049` for NFS).
2. **List NFS shares**: Use `showmount -e [IP]` to list available NFS shares on the target server.
3. **Check NFS exports**: Inspect `/etc/exports` to see which directories are shared and any special configurations like `root_squash`.

**Exploitation**

1. **Gain access**: Mount NFS shares on the client system.
2. **Set SUID on files**: If `root_squash` is disabled, upload a bash executable, set the SUID bit, and change the file owner to `root`.
3. **Escalate Privileges**: Run the SUID-enabled file to escalate privileges and gain a root shell.

NFS misconfigurations can be exploited to escalate privileges, especially if `root_squash` is not enabled.


### SMTP (Simple Mail Transfer Protocol) Summary

**What is SMTP?**  
SMTP is a protocol used for sending and relaying emails over the internet. It typically operates on port `25`, but other ports like `587` and `465` can also be used for secure connections.

**How to Enumerate SMTP?**

1. **Scan for SMTP service**: Use Nmap to check if SMTP is running on the target system.  
    Example:
    
    ```bash
    nmap -p 25,587,465 -sV [IP]
    ```
    
2. **Check SMTP Banner**: Connect using `telnet` or `nc` to gather information from the banner.  
    Example:
    
    ```bash
    telnet [IP] 25
    ```
    
3. **Enumerate Users**: Use the `VRFY` or `EXPN` commands to validate existing users.  
    Example:
    
    ```bash
    VRFY root
    ```
    
4. **Automated Enumeration**: Use tools like `smtp-user-enum` or **Metasploit modules** to automate the process.  
    Example with Metasploit:
    
    ```bash
    use auxiliary/scanner/smtp/smtp_enum
    set RHOSTS [IP]
    run
    ```
    

**Exploitation**

1. **Relay Exploitation**: Exploit misconfigured SMTP servers that allow unauthenticated email relaying.  
    Example with Metasploit:
    
    ```bash
    use exploit/windows/smtp/email_harvester
    set RHOSTS [IP]
    run
    ```
    
2. **Email Spoofing**: Use the server to forge emails if authentication is not required.
    
3. **Sensitive Information Leak**: SMTP banners, user enumeration, and misconfigurations may reveal valuable information about the target.
    

Using **Metasploit** for both enumeration and exploitation enhances efficiency, providing powerful modules tailored for SMTP vulnerabilities. Misconfigurations can expose vulnerabilities aiding in reconnaissance or privilege escalation.