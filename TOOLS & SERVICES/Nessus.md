
Download : 
https://tryhackme.com/room/rpnessusredux
---

## **🔍 Nessus Vulnerability Scanner Cheat Sheet**  
*GUI-powered scanning with free/paid tiers (Tenable)*  

### **🆓 Free vs Paid**  
- **Free (Nessus Essentials)**: Limited to **16 IPs/scan**, no compliance checks.  
- **Paid (Professional)**: Unlimited scans, advanced templates, compliance audits.  
- Pricing: [Tenable Nessus](https://www.tenable.com/products/nessus)  

---

### **🎯 Key UI Elements (Answers to Your Questions)**  
1. **Launch a scan**: ➡️ **`Launch`** button  
2. **Create custom templates**: Side menu → **`Policies`**  
3. **Change plugin properties**: **`Plugins`** menu (hide/change severity)  
4. **Host discovery scan**: **`Host Discovery`** template  
5. **Most versatile scan**: **`Basic Network Scan`** ("suitable for any host")  
6. **Authenticated patch check**: **`Patch Audit`**  
7. **Web App scans**: **`Web Application Tests`**  

---

### **📌 Scan Types Breakdown**  
| Scan Type              | Purpose                                            |     |
| ---------------------- | -------------------------------------------------- | --- |
| **Basic Network Scan** | General-purpose vulnerability scan                 |     |
| **Host Discovery**     | Detects live hosts (Ping sweep)                    |     |
| **Patch Audit**        | Checks missing OS/software updates (requires auth) |     |
| **Web App Tests**      | Focused on HTTP/S services (OWASP Top 10, etc.)    |     |
| **Credentialed Scan**  | Uses login creds for deeper analysis               |     |

---

### **⚡ Pro Tips**  
- **Free Tier Workaround**: Split large networks into chunks (≤16 IPs).  
- **Critical First**: Filter results by **severity** (Critical/High).  
- **Reports**: Export as PDF/CSV for documentation.  

---

### **❓ "Why Nessus Over Nmap?"**  
> 🟩 **Answer**: Nessus provides:  
> - **CVE-based vulnerability ratings** (not just open ports).  
> - **GUI with prioritization** (vs. Nmap’s raw output).  
> - **Compliance checks** (e.g., CIS benchmarks).  

---

**Example Workflow**:  
1. Run **`Host Discovery`** → Find live hosts.  
2. Follow up with **`Basic Network Scan`** on targets.  
3. For web apps: **`Web Application Tests`**.  
4. Authenticate where possible for **`Patch Audit`**.  


### Starting 
sudo /bin/systemctl start nessusd.service
https://localhost:8834/ 


