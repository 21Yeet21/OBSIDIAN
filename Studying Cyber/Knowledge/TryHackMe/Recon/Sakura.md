
**H2 Techniques & Tools for Sakura Room CTF**  

---

### **Task 2: TIP-OFF**  
**Objective**: Find the attacker’s username.  
**Techniques**:  
- **SVG Source Analysis**: Inspect embedded paths in SVG files for hidden data.  
**Tools**:  
- **Browser Developer Tools (F12)**: Revealed username in `/home/SakuraSnowAngelAiko`.  

---

### **Task 3: RECONNAISSANCE**  
**Objective**: Extract email and full name.  
**Techniques**:  
- **PGP Key Decoding**: Parse public keys for email addresses.  
- **LinkedIn Cross-Referencing**: Validate name via social media.  
**Tools**:  
- **Google Search**: Found GitHub repo (`github.com/SakuraSnowAngelAiko/PGP`).  
- **PGP Decoder Tool** (https://cirw.in/gpg-decoder): Extracted `SakuraSnowAngel83@protonmail.com`.  
**Findings**:  
- **Name**: Aiko Abe (LinkedIn).  
- **Email**: `SakuraSnowAngel83@protonmail.com`.  

---

### **Task 4: UNVEIL**  
**Objective**: Cryptocurrency wallet, crypto type, payment pool.  
**Techniques**:  
- **GitHub Commit History Analysis**: Track deleted code (stratum URL).  
- **Blockchain Tracing**: Validate wallet transactions.  
**Tools**:  
- **Etherscan.io**: Identified wallet `0xa102397dbeeBeFD8cD2F73A89122fCdB53abB6ef`.  
**Findings**:  
- **Wallet**: Ethereum address with Tether transactions.  
- **Payment Pool (Jan 23, 2021)**: Ethermine.  

---

### **Task 5: TAUNT**  
**Objective**: Twitter handle, WiFi data URL, BSSID.  
**Techniques**:  
- **Twitter Handle Search**: Reverse image search for "@SakuraLoverAiko".  
- **Dark Web Navigation**: Access DeepPaste via Tor.  
- **WiFi BSSID Mapping**: Use SSID-to-MAC lookup.  
**Tools**:  
- **Tor Browser**: Accessed `.onion` site (`depasteon6cqgrykzrgya52xglohg5ovyuyhte3ll7hzix7h5ldfqsyd.onion`).  
- **Wigle.net**: Mapped SSID "DK1F-G" → BSSID `84:AF:EC:34:FC:F8`.  
**Findings**:  
- **Twitter Handle**: `@SakuraLoverAiko`.  
- **WiFi URL**: DeepPaste link with MD5 hash `0a5c6e136a98a60b8a21643ce8c15a74`.  

---

### **Task 6: HOMEBOUND**  
**Objective**: Geolocation, layover airport, lake, home city.  
**Techniques**:  
- **Landmark Recognition**: Washington Monument → Nearest airport (DCA).  
- **Reverse Image Search**: Identified Haneda Airport (HND) lounge via Google Lens.  
- **WiFi SSID Analysis**: "HIROSAKI_Free_Wi-Fi" → Home city.  
**Tools**:  
- **Google Lens/Yandex**: Matched lounge image to Haneda’s Sakura Lounge.  
- **Visual Geolocation**: Lake Inawashiro via map comparison.  
**Findings**:  
- **Closest Airport**: Ronald Reagan Washington National (DCA).  
- **Layover**: Haneda Airport (HND).  
- **Lake**: Lake Inawashiro (Japan).  
- **Home City**: Hirosaki (via WiFi SSID).  

---

### **Key Tools**  
1. **Browser Inspector (F12)**: For SVG/HTML source analysis.  
2. **PGP Decoder**: Extract emails from public keys.  
3. **Etherscan.io**: Track crypto transactions.  
4. **Tor Browser**: Access .onion sites (e.g., DeepPaste).  
5. **Wigle.net**: Map SSIDs to BSSIDs.  
6. **Google Lens/Yandex**: Reverse image search for geolocation.  

---

### **Core Techniques**  
- **OSINT Cross-Referencing**: Link GitHub, Twitter, and LinkedIn data.  
- **Commit History Mining**: Recover deleted code/URLs.  
- **Dark Web Navigation**: Use Tor for hidden resources.  
- **Geolocation Pivoting**: Combine landmarks, WiFi SSIDs, and image matching.  

---

### **Takeaways**  
- **Username Pivoting**: Start with usernames to uncover social/media profiles.  
- **Blockchain Forensics**: Trace wallets via Etherscan for transaction history.  
- **Multi-Source Validation**: Cross-check findings (e.g., BSSID + SSID + geolocation).  

**Pro Tip**: Always inspect page sources (Ctrl+U) and deleted GitHub commits for hidden clues! 🔍