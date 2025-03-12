**H2 Techniques and Tools for OSINT (TryHackMe OHSINT Room)**  

### **Tools & Techniques Used**  
1. **ExifTool**  
   - Extracts metadata from files (e.g., author, GPS coordinates, timestamps).  
   - Command: `exiftool WindowsXP.jpg` → Revealed author **OWoodflint** and location data.  

2. **Google Search**  
   - OSINT cornerstone for finding social profiles (Twitter, GitHub, WordPress) using keywords like "OWoodflint".  

3. **Wigle.net**  
   - Maps Wi-Fi networks using BSSID/MAC addresses.  
   - **Steps**:  
     - Extract BSSID `B4:5D:50:AA:86:41` from Twitter.  
     - Query on Wigle.net → SSID **UnileverWiFi** and location (**London**).  

4. **GitHub**  
   - Source for personal email: OWoodflint@gmail.com (found in `people_finder` repo).  

5. **WordPress Blog Analysis**  
   - **Hidden Text Detection**:  
     - Use **Ctrl+A** to highlight invisible text (white font) → Password: `pennYDr0pper`.  

---

### **Answers to Questions**  
1. **User’s Avatar**:  
   - **Answer**: Cat (found on Twitter profile).  

2. **City**:  
   - **Answer**: London (GitHub profile + Wigle.net BSSID lookup).  

3. **SSID of WAP**:  
   - **Answer**: `UnileverWiFi` (via BSSID `B4:5D:50:AA:86:41` on Wigle.net).  

4. **Personal Email**:  
   - **Answer**: `OWoodflint@gmail.com` (GitHub repository).  

5. **Email Source**:  
   - **Answer**: GitHub.  

6. **Holiday Destination**:  
   - **Answer**: New York (WordPress blog).  

7. **Password**:  
   - **Answer**: `pennYDr0pper` (hidden in WordPress page source).  

---

### **Key Workflow**  
1. **Metadata Extraction**: Use **ExifTool** to gather initial clues (author name, location).  
2. **Profile Discovery**: Google search → Twitter, GitHub, WordPress.  
3. **Wi-Fi Analysis**: BSSID → Wigle.net → SSID and location.  
4. **Hidden Data**: Highlight invisible text on WordPress to uncover passwords.  

**Pro Tip**: Combine metadata analysis with social media scraping and network mapping for comprehensive OSINT! 🔍