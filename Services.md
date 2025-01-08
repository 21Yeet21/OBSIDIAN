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

- ssh  -i ./id_rsa username@hostip

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



