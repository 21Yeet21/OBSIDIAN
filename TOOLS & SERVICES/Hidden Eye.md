Here’s a concise, step-by-step summary for using **HiddenEye** (a phishing tool) **safely and correctly**, including virtual environment setup to avoid system conflicts:

---

## **📌 HiddenEye Quick-Start Guide**  
*Modern phishing tool with 34+ cloneable pages, keyloggers, and tunneling support.*  
**⚠️ Legal Note**: Use **only for ethical hacking/education** (e.g., pentesting with permission).  

---

### **🔧 Installation & Setup**  
1. **Clone the Repository**:  
   ```bash
   git clone https://github.com/DarkSecDevelopers/HiddenEye.git
   cd HiddenEye
   ```

2. **Create a Python Virtual Environment** (Avoid `sudo pip` errors):  
   ```bash
   python3 -m venv venv               # Create venv
   source venv/bin/activate           # Activate it
   pip install -r requirements.txt    # Install deps (no sudo!)
   ```

3. **Make Executable**:  
   ```bash
   chmod +x HiddenEye.py
   ```

---

### **🚀 Running HiddenEye**  
```bash
./HiddenEye.py -f
```
**Follow Prompts**:  
- **LOCALTUNNEL**: Enter `N` (unless needed).  
- **Legal Warning**: Enter `Y` (educational use only).  
- **Options**:  
  - Select a site to clone (e.g., Facebook, Instagram).  
  - Add keylogger? (Y/N).  
  - Enable **Cloudflare protection** (recommended).  
  - Email data to yourself? (Optional).  
  - Set **custom redirect link** after phishing.  
  - Choose a port (default: `8080`).  

---

### **🌐 Launching the Attack**  
- Two links will generate:  
  - **Local IP**: For testing on your network.  
  - **Tunneled URL** (e.g., Ngrok): For external targets.  
- Send the link to your target (ethical use only!).  

---

### **🔒 Post-Execution**  
- **Deactivate the venv** when done:  
  ```bash
  deactivate
  ```
- **Delete traces**: Remove the `HiddenEye` folder if unused.  

---

### **💡 Pro Tips**  
- **Avoid `sudo pip`**: Always use a venv to prevent system conflicts.  
- **Ngrok Alternative**: Use `serveo` or `localtunnel` if Ngrok fails.  
- **Debugging**: Run with `-v` flag for verbose logs.  

---

> 🟩 **Remember**: HiddenEye is **for legal pentesting only**. Unauthorized phishing is illegal!  

**Need updates?** Check the [GitHub repo](https://github.com/DarkSecDevelopers/HiddenEye) for new features/fixes.  

--- 

Save this guide for quick reference! 🚀