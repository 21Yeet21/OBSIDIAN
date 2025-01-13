
The reason you need an **OpenVPN connection** in environments like TryHackMe when working with custom domains (like `website.thm`) is due to how **DNS resolution** and **network isolation** work in these simulated environments.

### **Why OpenVPN Is Needed**

1. **Simulated Networks in TryHackMe**:
    
    - Domains such as `website.thm` or other `.thm` domains are **not real internet domains**. They are part of a private, isolated virtual environment created by TryHackMe for learning purposes.
    - These domains are not registered on public DNS servers (which resolve real-world domains like `google.com`). Instead, they are only defined and accessible within TryHackMe’s **virtual network**.
2. **Private DNS Servers**:
    
    - When connected via OpenVPN, your machine routes DNS requests and other traffic related to `.thm` domains through TryHackMe's **private DNS server**.
    - Without this VPN connection, your local DNS resolver (typically provided by your ISP or a public DNS service like Google’s `8.8.8.8`) does not know how to resolve `.thm` domains, resulting in errors like `NXDOMAIN` (non-existent domain).
3. **Simulated Services**:
    
    - The servers hosting content for these custom `.thm` domains are not publicly accessible on the internet. Instead, they exist in a **virtual environment** reachable only through the VPN. This ensures controlled access for learning purposes and security.

### **Why Can’t You Reach the Website Without VPN?**

- **Lack of Public DNS Registration**:  
    Domains like `website.thm` are **not registered** in the global DNS system.  
    Example:
    
    ```bash
    nslookup website.thm 8.8.8.8
    ```
    
    would fail because Google’s public DNS has no record of `.thm` domains.
    
- **No Route to the Private Network**:  
    Even if you manually pointed to a DNS server, your machine would still be unable to reach the **private IP addresses** of these servers without a route through the VPN.
    

### **Summary of Key Points**

|Concept|Public Website (e.g., `example.com`)|TryHackMe Website (e.g., `website.thm`)|
|---|---|---|
|DNS Resolution|Handled by public DNS servers|Handled by TryHackMe’s private DNS server|
|Accessibility|Available on the internet|Only accessible through TryHackMe’s private network|
|VPN Requirement|Not required|Required to route traffic to private servers|

### **Benefits of this Approach**

- **Security**: Keeps exercises and simulated attacks isolated from the public internet.
- **Control**: Provides a custom, controlled environment for learning without risking real-world systems.

### **Conclusion**

Without the VPN, your computer cannot resolve `.thm` domains or access their corresponding servers because these resources do not exist on the public internet—they are part of a **private network** simulated by TryHackMe. The VPN creates a secure connection to this private network, enabling you to complete the tasks.