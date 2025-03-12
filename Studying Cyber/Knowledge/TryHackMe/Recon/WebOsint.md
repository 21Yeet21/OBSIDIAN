**H2 Techniques & Tools for WebOSINT Room**  

---

### **Task 1: Domain Reconnaissance**  
**Tools**:  
- **Google Search**: Initial domain lookup (though domain is defunct).  
**Techniques**:  
- **Defunct Domain Analysis**: Even non-existent domains leave traces (registrar data, historical snapshots).  

---

### **Task 2: Whois Lookup**  
**Tools**:  
- **ICANN Lookup** (lookup.icann.org): Retrieve domain registration details.  
**Techniques**:  
- **Registrar Identification**: Found **NAMECHEAP INC** as registrar.  
- **Nameserver Extraction**: First nameserver: `dns1.registrar-servers.com`.  
- **Privacy Detection**: Registrant name/address redacted (WhoisGuard).  

---

### **Task 3: Wayback Machine Analysis**  
**Tools**:  
- **Internet Archive (Wayback Machine)**: Analyze historical snapshots.  
**Techniques**:  
- **Author Identification**: Blog author **Steve** via oldest snapshot (Dec 2015).  
- **Geolocation**: Blog posts revealed **Gwangju, South Korea**.  
- **Landmark Research**: Google search for temple in **Mudeungsan National Park** → **Jeungsimsa Temple**.  

---

### **Task 4: DNS & IP Analysis**  
**Tools**:  
- **ViewDNS.info**: IP history and reverse IP lookup.  
**Techniques**:  
- **IP History Check**: Oct 2016 IP: **104.18.53.31**.  
- **Hosting Type Inference**: **Shared hosting** (97 domains on same IP).  
- **IP Change Tracking**: 4 IP changes in domain history.  

---

### **Task 5: Heat.net Domain Investigation**  
**Tools**:  
- **Whois**: Second nameserver: `ns2.heat.net`.  
- **Wayback Machine**: Earliest capture (06/01/97).  
**Techniques**:  
- **Historical IP Retrieval**: Dec 2011 IP: **72.52.192.30**.  
- **Hosting Correlation**: **Shared hosting** (Liquid Web, L.L.C).  
- **Content Analysis**: First header in 2010 snapshot: **"HVAC Heating & Cooling"**.  

---

### **Task 6: Website & Link Analysis**  
**Tools**:  
- **Browser Inspector** (Ctrl+U): Source code analysis.  
- **NerdyData**: Track Google Analytics code reuse.  
**Techniques**:  
- **Link Enumeration**:  
  - **Internal Links**: 8 (e.g., `/commercial-contractors`).  
  - **External Links**: 1 (non-ad): `purchase.org`.  
- **Google Analytics ID**: `UA-133728643-1` (found via `UA-` search in source code).  
- **Affiliate Code Check**: No codes in `purchase.org` link (**Nay**).  

---

### **Final Task: Connecting the Dots**  
**Tools**:  
- **ViewDNS.info Reverse IP Lookup**: Correlate IP ownership.  
**Techniques**:  
- **Hosting Provider Link**: Both `heat.net` and `purchase.org` use **Liquid Web, L.L.C**.  
- **PBN Identification**: Private Blog Network (PBN) for SEO manipulation.  

---

### **Key Tools Summary**  
1. **ICANN Lookup**: Domain registration details.  
2. **Wayback Machine**: Historical content analysis.  
3. **ViewDNS.info**: IP/DNS history and reverse lookups.  
4. **NerdyData**: Track code/script reuse.  
5. **Browser Inspector**: Source code analysis (GA codes, links).  

---

### **Core Techniques**  
1. **Historical Snapshot Mining**: Extract author/location data from archived pages.  
2. **Reverse IP Analysis**: Identify shared hosting and PBNs.  
3. **Source Code Scraping**: Uncover tracking codes and hidden links.  
4. **Registrar/Privacy Checks**: Detect redacted registrant info (WhoisGuard).  

---

### **Takeaways**  
- **Pivot on IPs**: Shared hosting IPs reveal connected domains (e.g., PBNs).  
- **Combine OSINT Sources**: Use Whois + Wayback + DNS tools for full domain profiling.  
- **Affiliate/SEO Tricks**: Check for subtle links between sites (shared IPs, analytics codes).  

**Pro Tip**: Always cross-reference historical data with current DNS records to uncover hidden relationships! 🔍
