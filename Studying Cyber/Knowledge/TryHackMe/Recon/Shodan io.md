
**H2 Techniques & Tools for Shodan.io Mastery**  

---

### **Core Techniques**  
1. **ASN (Autonomous System Number) Reconnaissance**  
   - **Purpose**: Map a company’s entire IP range.  
   - **Workflow**:  
     - Use `ping` or DNS lookup to get a target’s IP (e.g., `142.93.194.248` for `tryhackme.com`).  
     - Resolve IP to ASN via [UltraTools ASN Lookup](https://www.ultratools.com/tools/asnInfo) (e.g., `AS14061` for DigitalOcean).  
     - Filter Shodan with `asn:AS14061` to scan all devices/services under that network.  
   - **Example**:  
     ```  
     asn:AS14061 product:MySQL → Finds MySQL servers on DigitalOcean’s ASN.  
     ```  

2. **Vulnerability Hunting**  
   - **Filters**:  
     - `vuln:CVE-2014-0160`: Find Heartbleed-vulnerable systems.  
     - `vuln:ms17-010`: Hunt for EternalBlue exploits (premium-only).  
   - **Combine with ASN**:  
     ```  
     asn:AS14061 vuln:CVE-2014-0160 → Heartbleed in a specific network.  
     ```  

3. **Banner Analysis**  
   - **Key Data**: Service versions, open ports, geolocation, OS.  
   - **Example Banner**:  
     ```json  
     {  
       "data": "Pi-hole",  
       "port": 80,  
       "org": "DigitalOcean",  
       "vulns": ["CVE-2020-12345"]  
     }  
     ```  

4. **IoT Device Discovery**  
   - **Use Cases**:  
     - Find public CCTV cameras: `webcam` or `has_screenshot:true`.  
     - Exposed databases: `product:MySQL` or `product:MongoDB`.  

---

### **Advanced Shodan Dorking**  
- **Ransomware Detection**:  
  ```  
  has_screenshot:true encrypted attention → Machines with ransomware screenshots.  
  ```  
- **Industrial Control Systems (ICS)**:  
  ```  
  screenshot.label:ics → Exposed SCADA/ICS devices.  
  ```  
- **SolarWinds Compromise**:  
  ```  
  http.favicon.hash:-1776962843 → Servers with SolarWinds backdoor.  
  ```  
- **Public Pi-Holes**:  
  ```  
  product:"Pi-hole" http.title:"Admin Console" → 5,300+ exposed Pi-Holes.  
  ```  

---

### **Tools & Integrations**  
1. **Shodan.io Web Interface**  
   - **Explore Page**: Pre-built queries for webcams, MySQL, and more.  
   - **Filters**: `city:London`, `port:443`, `os:"Windows 10"`.  

2. **Shodan Monitor**  
   - **Function**: Track network vulnerabilities (open ports, CVEs).  
   - **Setup**: Add IP ranges → Receive alerts for:  
     - Top open ports (e.g., `80`, `443`).  
     - Notable ports (e.g., `8080` for admin panels).  
     - Critical vulnerabilities (e.g., `CVE-2021-44228` Log4j).  

3. **Shodan Chrome Extension**  
   - **Use**: Real-time intel while browsing.  
   - **Output**: IP, open ports, geolocation, vulnerabilities.  

4. **Shodan API + Python Automation**  
   - **Script Example**:  
     ```python  
     from shodan import Shodan  
     api = Shodan('API_KEY')  
     results = api.search('product:"Pi-hole"')  
     for service in results['matches']:  
         print(f"IP: {service['ip_str']}, Org: {service['org']}")  
     ```  

5. **Hydra (Brute-Force Tool)**  
   - **Pi-Hole Attack**:  
     ```bash  
     hydra -l '' -P rockyou.txt 192.168.0.1 http-post-form \  
     "/admin/index.php?login:pw=^PASS^:Forgot password"  
     ```  

---

### **Case Study: Hacking Public Pi-Holes**  
1. **Discovery**:  
   - Shodan Query: `product:"Pi-hole" http.component:"AdminLTE"`.  
   - **Result**: 5,308 public Pi-Holes (578 without passwords).  

2. **Exploitation**:  
   - **Passwordless Access**: Directly visit `/admin/queries.php` to view DNS logs.  
   - **Brute-Force**: Use Hydra with `rockyou.txt` to crack weak passwords.  

3. **Impact**:  
   - View target’s entire browsing history, device IPs, and blocked domains.  
   - Launch **DNS Amplification Attacks** via exposed Pi-Holes.  

---

### **Defensive Strategies**  
1. **Shodan Monitor**: Add your network → Get alerts for exposed services.  
2. **VPNs**: Restrict Pi-Hole/admin panel access to VPN-only.  
3. **Strong Passwords**: Avoid defaults; use 12+ character passwords.  
4. **Shodan Search**: Regularly check if your IP is indexed.  

---

### **Pro Tips**  
- **Combine Filters**: `asn:AS14061 port:22 os:"Linux"` → Linux SSH servers in a network.  
- **Leverage Screenshots**: `has_screenshot:true` → Find exposed GUIs (e.g., routers).  
- **Track Trends**: Use Shodan’s `Explore` page for trending dorks (e.g., ransomware, ICS).  

**Warning**: Use Shodan ethically. Unauthorized access to devices is illegal. Always test only systems you own! 🔒