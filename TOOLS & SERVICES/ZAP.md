

## 🛠️ OWASP ZAP Overview

**OWASP ZAP** (Zed Attack Proxy) is a **free**, **open-source** web application security testing framework developed by the **OWASP Foundation**. It is widely used for:

- Web application scanning
    
- Active and passive vulnerability discovery
    
- Manual and automated testing
    

---

## 🆚 Why Use ZAP Over Burp Suite?

### 🔓 Key Advantages of ZAP:

- **100% Free & Open Source**: No feature gating or paywall (unlike Burp Pro).
    
- **Automated Scanning**: Built-in active and passive scanner (free).
    
- **Spidering / Site Mapping**: Automatically crawls and maps target apps.
    
- **Unthrottled Intruder**: Bruteforce with no artificial limits.
    
- **Simplified Manual Testing**: Automatically intercepts without needing to forward every request manually.
    

### 🛠️ Comparable Features to Burp Suite:

|ZAP Feature|Burp Suite Equivalent|Cost in Burp|
|---|---|---|
|Automated Scanner|Active Scanner|💰 Paid|
|Site Spider|Crawler|💰 Paid|
|Bruteforcer|Intruder|💰 Paid|
|Request Interception|Proxy|✅ Free|
|Manual Request Handling|Repeater|✅ Free|

---

## ✅ ZAP Will Teach You To:

- Run **automated scans**
    
- Perform **directory bruteforce**
    
- Conduct **authenticated scans**
    
- Bruteforce **login pages**
    
- Install and use **ZAP extensions**
    

---

### ❓ Question: **What does ZAP stand for?**

> 🟩 **Answer:** **Zed Attack Proxy**


Here's your structured summary of performing an automated scan in ZAP:

---

## 🚀 **ZAP Automated Scan Guide**  

### **🔧 How to Start**  
1. Click the **"Automated Scan"** button in ZAP.  
2. Enter your target URL (e.g., `http://example.com`).  

---

### **🕷️ Spider Options**  
ZAP offers two scan modes:  

| **Spider Type**       | **Pros**                                      | **Cons**                          |  
|-----------------------|-----------------------------------------------|-----------------------------------|  
| **Traditional Spider** | Passive, quiet, builds sitemap fast.          | Misses AJAX-heavy content.        |  
| **AJAX Spider**       | Crawls dynamic pages (e.g., JavaScript apps). | Slower; requires browser/proxy.   |  

**For AJAX Spider:**  
- Install HTMLUnit (for headless browsing):  
  ```bash
  sudo apt install libjenkins-htmlunit-core-js-java
  ```  
- Select **"HtmlUnit"** from the AJAX Spider dropdown.  

---

### **⚡ Expected Output**  
- **Sitemap**: All discovered pages/directories.  
- **Vulnerabilities**: Basic findings (e.g., XSS, outdated libs).  
- **Example**:  
  > *"With minimal setup, we found a login page and 5+ vulnerabilities."*  

---

### **🔧 Advanced Tweaks**  
- **Configure scans** via `Options (Ctrl+Alt+O)`.  
- **Combine both spiders** for maximum coverage (but slower).  

---

### ❓ **"Which spider should I use?"**  
> 🟩 **Answer**: Start with **Traditional Spider** for speed. Use **AJAX Spider** only if the site relies heavily on JavaScript (e.g., React/Angular apps).  

--- 

**💡 Pro Tip**: For CTFs, the Traditional Spider often finds low-hanging fruit fast! 🍒  

