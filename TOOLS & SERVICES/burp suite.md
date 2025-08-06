Here's a structured breakdown of **Burp Suite Community Edition** features for quick reference:

---

## **🛠️ Burp Suite Community Edition Cheat Sheet**  
*Free web app testing toolkit with essential pentesting tools*

### **🔑 Core Features**
| Tool | Purpose | Use Case |
|------|---------|----------|
| **Proxy** | Intercept/modify HTTP(S) traffic | Man-in-the-middle (MITM) testing, request tampering |
| **Repeater** | Resend modified requests | Fine-tuning payloads (SQLi, XSS, etc.) |
| **Intruder** | Automated request spraying (rate-limited) | Brute-force, fuzzing, parameter enumeration |
| **Decoder** | Encode/decode data (Base64, URL, etc.) | Obfuscating payloads or analyzing captured data |
| **Comparer** | Diff text/byte-level data | Spotting differences in responses (e.g., after fuzzing) |
| **Sequencer** | Analyze token randomness | Testing session cookies/CSRF tokens for predictability |

---

### **⚡ Pro Tips**
1. **Proxy Workflow**:  
   - Configure browser to `127.0.0.1:8080` → Intercept requests in Burp.  
   - Use **Ctrl+R** to send requests from Proxy to Repeater.  

2. **Intruder Limitations (Community)**:  
   - **Rate-limited** (~5 requests/sec). Bypass with:  
     - **Turbo Intruder** (BApp Store extension).  
     - Manual scripting (Python + `requests`).  

3. **Extensions (BApp Store)**:  
   - **Logger++**: Enhanced traffic logging.  
   - **AuthMatrix**: Auth testing.  
   - **ClickBandit**: Clickjacking exploits.  

---

### **🔌 Extending Burp**
- **Languages**: Python (Jython), Ruby (JRuby), Java.  
- **Install Extensions**:  
  1. Open **Extender** tab → **BApp Store**.  
  2. Install desired tools (e.g., **Turbo Intruder**).  

---

### **🚀 Example Workflow**
1. **Intercept** login request via **Proxy**.  
2. **Send** to **Repeater** → Modify parameters for SQLi testing.  
3. **Fuzz** endpoints with **Intruder** (sniper mode).  
4. **Decode** responses in **Decoder** (Base64 → plaintext).  
5. **Compare** responses in **Comparer** to find anomalies.  

---

### **❓ "Burp Community vs Pro?"**  
> 🟩 **Answer**: Pro adds:  
> - **Unlimited Intruder**, **Scanner (automated vuln detection)**, **Collaborator (out-of-band testing)**.  
> - **No rate limits**, **save project files**, **team collaboration**.  

---

### **📌 Free Alternative**  
- **OWASP ZAP**: Open-source, no rate limits, but less polished UI.  

---

![](https://miro.medium.com/v2/resize:fit:30/0*LpfAjLEZyRTzAucL.png)

Clicking on these icons opens a new window with helpful information specific to that section. These help icons are invaluable when you need assistance or clarification on a particular feature, so make sure to utilise them effectively.




Here's a structured breakdown of Burp Suite's configuration settings, optimized for quick reference:

### **🌐 Burp Suite Configuration Hierarchy**
#### **1. Global Settings (User Options)**
- **Scope**: Applies to *all* Burp sessions
- **Persistence**: Saved between launches
- **Key Configurations**:
  - **Proxy Listeners** (Interface/port settings)
  - **TLS Certificates** (CA certificate management)
  - **Platform Authentication** (Proxy auth credentials)
  - **UI Preferences** (Fonts, layouts, themes)
  - **Project-level defaults** (Default scan configurations)

*Access Path*:  
`Dashboard` → `Settings` (cog icon) → `User options`

#### **2. Project Settings**
- **Scope**: Applies only to *current* session
- **Persistence**: *Lost on exit* (Community Edition limitation)
- **Key Configurations**:
  - **Target Scope** (URLs to include/exclude)
  - **Session Handling Rules** (Cookie management)
  - **Scan Configurations** (Audit depth, speed)
  - **HTTP Headers** (Custom headers for all requests)

*Access Path*:  
`Dashboard` → `Settings` → `Project settings`

---

### **⚡ Community Edition Limitations**
- ❌ No project saving/reloading  
- ❌ No collaborative features  
- ❌ Limited scan configurations  

*Workaround*:  
Manually export data via:  
`Target` → `Save site map` (XML/JSON)  
`Proxy` → `Save history` (XML/CSV)

---

### **🔧 Recommended Baseline Setup**
1. **Global Must-Haves**:
   ```text
   User Options → Connections → 
     [ ] Enable "Force use of TLS 1.2+" 
     [X] Enable "Automatically update CA certificate"
   
   User Options → Display → 
     [X] "Monospace font for HTTP messages"
   ```

2. **Project Essentials**:
   ```text
   Target → Scope → 
     Add your target domain (e.g., *.example.com)
   
   Project Options → HTTP → 
     [X] "Automatically update Content-Length"
   ```

---

### **💡 Pro Tips**
1. **Backup Global Config**:  
   `User options` → `Save settings` (`.json` file)
   
2. **Temporary Persistence Hack** (Community):  
   - Keep Burp running in background (`nohup burpsuite &`)  
   - Use browser's "Restore previous session" feature

3. **Critical Hotkeys**:  
   - `Ctrl+Shift+D`: Toggle intercept  
   - `Ctrl+R`: Send to Repeater  
   - `Ctrl+I`: Send to Intruder

---

### **🚨 Security Note**  
Always clear sensitive data (cookies, auth tokens) before closing Burp in Community Edition:  
`Proxy` → `HTTP history` → Right-click → `Clear history`

---

> 🟢 **Example Workflow**:  
> 1. Set global TLS/display preferences  
> 2. Define target scope for current engagement  
> 3. Export findings before exiting  

Need help with specific settings? Just ask! 🛠️

Here's a distilled, actionable guide to mastering Burp Proxy with key commands and workflows:

---

### **🎯 Burp Proxy Quick-Start Guide**

#### **1. Basic Interception**
- **Enable/Disable Intercept**:  
  `Proxy` → `Intercept` → Toggle **"Intercept is on/off"** button (or `Ctrl+I`)
- **Manual Control**:  
  - **Forward**: Send request to server (`Ctrl+F`)  
  - **Drop**: Block request (`Ctrl+D`)  
  - **Edit**: Modify headers/body before forwarding  

#### **2. Logging & History**
- **View All Traffic**:  
  `Proxy` → `HTTP history` (even when intercept is off)  
- **Filter Traffic**:  
  Use regex in `Filter` bar (e.g., `method=POST && status=200`)  
- **Export Logs**:  
  Right-click → `Save items` (CSV/XML)  

#### **3. Proxy Settings**
| Feature | Path | Use Case |
|---------|------|----------|
| **Response Interception** | `Proxy` → `Options` → `Intercept Server Responses` | Debugging server-side logic |
| **Match & Replace** | `Proxy` → `Options` → `Match and Replace` | Auto-modify User-Agent/Cookies |
| **Invisible Proxy** | `Proxy` → `Options` → `Proxy Listeners` → `Edit` → `Support invisible proxying` | Evade client-side proxy detection |

#### **4. WebSockets**
- **Capture WS Traffic**:  
  `Proxy` → `WebSockets history`  
- **Intercept WS Messages**:  
  `Proxy` → `Options` → `Intercept WebSockets messages`  

---

### **🔥 Pro Tips**
1. **Target Scope**:  
   - Set `Target` → `Scope` to avoid noise from non-target domains.  
2. **Auto-Disable Intercept**:  
   ```text
   Proxy → Options → Intercept Client Requests → 
   [ ] "Intercept requests based on rules" → Add URL exclusion
   ```
3. **Hotkeys**:  
   - `Ctrl+Shift+F`: Send to Repeater  
   - `Ctrl+Shift+I`: Send to Intruder  

---

### **🚨 Critical Security Settings**
1. **Disable Unwanted Protocols**:  
   ```text
   Proxy → Options → Proxy Listeners → Edit → 
   [ ] "Allow HTTP/2" (if testing legacy systems)
   ```
2. **CA Certificate**:  
   Install Burp's CA cert (`http://burp/cert`) to avoid TLS warnings.

---

# Task 12 Scoping and Targeting

Finally, we come to one of the most important aspects of using the Burp Proxy: **Scoping**.

Capturing and logging all of the traffic can quickly become overwhelming and inconvenient, especially when we only want to focus on specific web applications. This is where scoping comes in.

By setting a scope for the project, we can define what gets proxied and logged in Burp Suite. We can restrict Burp Suite to target only the specific web application(s) we want to test. The easiest way to do this is by switching to the `**Target**` tab, right-clicking on our target from the list on the left, and selecting `**Add To Scope**`. Burp will then prompt us to choose whether we want to stop logging anything that is not in scope, and in most cases, we want to select `yes`.

![](https://miro.medium.com/v2/resize:fit:700/0*AHdpbObFkr0sPnQi.gif)

To check our scope, we can switch to the **Scope settings** sub-tab within the **Target** tab.

The Scope settings window allows us to control our target scope by including or excluding domains/IPs. This section is powerful and worth spending time getting familiar with.

However, even if we disabled logging for out-of-scope traffic, the proxy will still intercept everything. To prevent this, we need to go to the **Proxy settings** sub-tab and select `**And**` `**URL**` `**Is in target scope**` from the "Intercept Client Requests" section.

![](https://miro.medium.com/v2/resize:fit:700/0*L66SahcEfOdXhmrw.png)

Enabling this option ensures that the proxy completely ignores any traffic that is not within the defined scope, resulting in a cleaner traffic view in Burp Suite.

Answer the questions below

Add `**http://MACHINE_IP/**` to your scope and change the proxy settings to only intercept traffic to in-scope targets.

See the difference between the amount of traffic getting caught by the proxy before and after limiting the scope.

**Note:** The AttackBox is already configured to solve the problem posed in this task. If you use the AttackBox and don’t wish to read through the information here, you can skip to the next task.

When intercepting HTTP traffic, we may encounter an issue when navigating to sites with TLS enabled. For example, when accessing a site like `**https://google.com**/`, we may receive an error indicating that the PortSwigger Certificate Authority (CA) is not authorised to secure the connection. This happens because the browser does not trust the certificate presented by Burp Suite.

![](https://miro.medium.com/v2/resize:fit:700/0*7TI44MHuGRjqtLrB.png)

To overcome this issue, we can manually add the PortSwigger CA certificate to our browser’s list of trusted certificate authorities. Here’s how to do it:

1. **Download the CA Certificate:** With the Burp Proxy activated, navigate to [**http://burp/cert**.](http://burp/cert.) This will download a file called `**cacert.der**`. Save this file somewhere on your machine.
2. **Access Firefox Certificate Settings:** Type `**about:preferences**` into your Firefox URL bar and press **Enter**. This will take you to the Firefox settings page. Search the page for "certificates" and click on the **View Certificates** button.

![](https://miro.medium.com/v2/resize:fit:700/0*09XYeqdahtVbtbgq.png)

1. **Import the CA Certificate:** In the Certificate Manager window, click on the **Import** button. Select the `**cacert.der**` file that you downloaded in the previous step.
2. **Set Trust for the CA Certificate:** In the subsequent window that appears, check the box that says “Trust this CA to identify websites” and click OK.

![](https://miro.medium.com/v2/resize:fit:678/0*KvEbF4Qcd4yUGOMC.png)

By completing these steps, we have added the PortSwigger CA certificate to our list of trusted certificate authorities. Now, we should be able to visit any TLS-enabled site without encountering the certificate error.

You can watch the following video for a visual demonstration of the full certificate import process:

![](https://miro.medium.com/v2/resize:fit:700/0*DJJ1zQ3uNriDeOze.gif)

By following these instructions, you can ensure that your browser trusts the PortSwigger CA certificate and securely communicates with TLS-enabled websites through the Burp Suite Proxy.

Answer the questions below

**If you are not using the AttackBox, configure Firefox (or your browser of choice) to accept the PortSwigger CA certificate for TLS communication through the Burp Proxy.**
