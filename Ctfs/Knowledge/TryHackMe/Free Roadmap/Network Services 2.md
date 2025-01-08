## NFS 



---

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

