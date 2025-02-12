

---  
## Windows Editions  

### History and Evolution  
Windows XP dominated for years but faced security risks. Vista introduced major changes but was poorly received due to compatibility and performance issues. Windows 7 became the post-XP standard, while Windows 8.x was short-lived. Windows 10 (2015) is now the primary desktop OS, succeeded by Windows 11 in 2021.  



### Windows 10 Editions  
Two main editions: **Home** (basic features for consumers) and **Pro** (advanced tools for businesses). Pro includes BitLocker encryption, Group Policy, Remote Desktop, and Hyper-V. Home lacks enterprise-focused features.  

### Windows Server Editions  
Windows Server 2019 is the current server OS (e.g., used in the VM example). Server editions prioritize scalability, security, and management tools for corporate networks.  

### Security Improvements  
Post-XP versions (e.g., Windows 10/11) introduced Defender, Secure Boot, and sandboxing. Microsoft now emphasizes regular updates and extended support timelines (e.g., Windows 10 support until 2025).  

### Transition to Windows 11  
Released in 2021, Windows 11 requires TPM 2.0 and Secure Boot. It refines UI/UX and integrates better with Microsoft ecosystems (Teams, Xbox).  

### Q&A Section  
1. **What encryption can you enable on Pro that you can't enable in Home?**  
   - **BitLocker Drive Encryption**: Available in Pro/Enterprise editions.  
   - **Home lacks BitLocker** but offers limited device encryption (e.g., via "Device Encryption" on compatible hardware).  

---  

Here’s your structured summary with Q&A:  

---  
## The Desktop (GUI)  

### The Desktop  
The desktop displays shortcuts for quick access to programs/files. Customize icons via right-click (resize, arrange, create folders). Adjust resolution, orientation, and multi-screen setups under **Display settings**. Change wallpapers/themes via **Personalize** (right-click > Personalize).  

### The Start Menu  
Accessed via the Windows logo (bottom-left). Divided into:  
1. **Account actions**: Lock, sign out, access Settings, or power options.  
2. **Recently added/installed apps**: Alphabetical list with jump-to-letter navigation.  
3. **Tiles**: Customizable shortcuts (right-click > *Pin to Start*).  

### The Taskbar  
Shows open apps, pinned shortcuts, and toolbars. Right-click the taskbar to enable/disable components like **Search**, **Task View**, or **Toolbars**. Hover over icons for previews.  

### Notification Area  
Located at the bottom-right. Default icons include **Clock**, **Network**, and **Volume**. Customize visibility via **Taskbar settings** (right-click taskbar > Taskbar settings > Notification Area).  

### Q&A Section  
1. **Which selection will hide/disable the Search box?**  
   - Right-click the **Taskbar** > Uncheck **Search** > **Hidden**.  

2. **Which selection will hide/disable the Task View button?**  
   - Right-click the **Taskbar** > Uncheck **Task View**.  

3. **Besides Clock and Network, what other icon is visible in the Notification Area?**  
   - **Volume/Speaker icon** (controls audio settings).  

---

## The File System  

### NTFS Basics  
**NTFS (New Technology File System)** is the modern Windows file system, replacing FAT32/HPFS. Key improvements include:  
- **Journaling**: Auto-repairs data corruption using transaction logs.  
- **Large file support**: Files >4GB allowed (unlike FAT32).  
- **Permissions**: Granular control over file/folder access (Read, Write, Full Control).  
- **Encryption (EFS)**: Built-in file encryption.  

### Permissions  
To view permissions:  
1. Right-click file/folder > **Properties** > **Security** tab.  
2. Select a user/group to see assigned permissions.  

| Permission          | Functionality                       |  
|---------------------|-------------------------------------|  
| **Read & Execute**  | Open and run files/folders.         |  
| **Modify**          | Edit or delete content.             |  
![[Pasted image 20250120225516.png]]
### Alternate Data Streams (ADS)  
- **Hidden streams** within files (e.g., metadata for downloaded files).  
- View ADS in PowerShell:  
```powershell  
Get-Item "file.txt" -Stream *  # Lists all streams  
```  

| ADS Use Case          | Example                              |  
|-----------------------|--------------------------------------|  
| **Legitimate**        | Marking internet-downloaded files.   |  
| **Malicious**         | Hiding malware scripts.              |  

### FAT vs. NTFS  
| Feature               | FAT32                      | NTFS                          |  
|-----------------------|----------------------------|-------------------------------|  
| **Max File Size**     | 4GB                        | ~16TB                         |  
| **Permissions**       | None                       | Granular (user/group-based)   |  
| **Recovery**          | Manual repair              | Journaling (auto-repair)      |  

### Q&A Section  
1. **What is the meaning of NTFS?**  
   - **New Technology File System**.  

---

No extra fluff! Let me know if this aligns better. 😊

To learn more about ADS, refer to the following link from MalwareBytes [here](https://blog.malwarebytes.com/101/2015/07/introduction-to-alternate-data-streams/). 

**Bonus**: If you wish to interact hands-on with ADS, I suggest exploring Day 21 of [Advent of Cyber 2](https://tryhackme.com/room/adventofcyber2).
### Q&A Section  
1. **What is the meaning of NTFS?**  
   - **New Technology File System**.  

---  

Here’s the concise summary with the Q&A:  

---  
## The Windows\System32 Folders  

### Windows Folder Overview  
- Location: Typically `C:\Windows`, but customizable via the **`%windir%`** system environment variable.  
- Purpose: Stores critical OS files, utilities, and configuration data. **Avoid modifying/deleting contents** to prevent system instability.  

### System32 Folder  
- Path: `%windir%\System32` (e.g., `C:\Windows\System32`).  
- Contains: Essential executables (e.g., `cmd.exe`), DLLs, and system tools. Tampering can render Windows inoperable.  

### Q&A Section  
1. **What is the system variable for the Windows folder?**  
   - **`%windir%`**  

---  

Here’s a **detailed yet concise summary** with strict focus on your provided content and key technical specifics:  

---

## User Accounts, Profiles, and Permissions  

### **Account Types**  
- **Administrator**:  
  - Full system control: install software, modify users/groups, adjust system settings.  
  - Accessible via `lusrmgr.msc` (Local Users and Groups Management).  
- **Standard User**:  
  - Restricted to personal files/settings (e.g., `C:\Users\<Username>`).  
  - Cannot install programs or modify system-wide settings.  

---

### **User Profiles**  
- **Location**: `C:\Users\<Username>` (e.g., `C:\Users\Max`).  
- **Creation**:  
  - Automatically generated during **first login** (triggered by User Profile Service).  
  - Includes default folders:  
    ```plaintext  
    Desktop | Documents | Downloads | Music | Pictures  
    ```  
- **Modification**:  
  - Administrators can reset/delete profiles via `lusrmgr.msc` or `System Properties > Advanced > User Profiles`.  

---

### **Managing Users/Groups**  
1. **Access Local Users and Groups**:  
   - Press `Win + R` > type ==`lusrmgr.msc`== > Enter.  
   - Navigate to **Users** (accounts) or **Groups** (permission sets).  

2. **Groups**:  
   - Predefined groups with inherited permissions (e.g., **Administrators**, **Users**, **Guests**).  
   - Example group descriptions:  

| Group Name       | Description                                  |  
|------------------|----------------------------------------------|  
| **Guests**       | Temporary access with restricted privileges. |  
| **Users**        | Default group for standard accounts.         |  

1. **Adding Users**:  
   - Administrators: Go to `Settings > Other users > Add someone else to this PC` (redirects to `lusrmgr.msc`).  

---

### **Built-in Accounts**  
- **Guest Account**:  
  - **Name**: `Guest`  
  - **Description**: *"Built-in account for guest access to the computer/domain."*  
  - **Status**: Disabled by default (enable via `lusrmgr.msc > Users > Guest > Properties`).  

---

### **Q&A Section**  
1. **What is the name of the other user account?**  
   - **Max** (example from profile path `C:\Users\Max`).  

2. **What groups is this user a member of?**  
   - **Users** (default group for standard accounts).  

3. **What built-in account is for guest access to the computer?**  
   - **Guest**  

4. **What is the account description?**  
   - *"Built-in account for guest access to the computer/domain."*  

--- 

Here’s the structured summary adhering to your guidelines:  

---

## User Account Control (UAC)  

### Purpose of UAC  
UAC prevents unauthorized system changes by requiring explicit approval for elevated actions. Introduced in Windows Vista, it reduces malware risk by ensuring applications/actions needing admin privileges prompt for user consent.  

### UAC Operation for Administrator Accounts  
- Administrators run with **limited privileges** by default.  
- Actions requiring elevation (e.g., installing software) trigger a UAC prompt for confirmation.  
- Example: Installing a program displays a UAC dialog; execution halts until approval.  

### UAC Behavior for Standard Users  
- **Shield icon** on programs indicates elevated privileges are needed.  
- Standard users receive a UAC prompt requiring **admin credentials** (username/password).  
- Example: Double-clicking an installer prompts for admin login; action cancels if credentials aren’t entered.  

### Built-in Administrator Account Exemption  
- The **built-in local administrator account** bypasses UAC prompts by default.  
- Security Note: This exemption increases risk if the account is misused.  

### Security Benefits of UAC  
- Limits malware’s ability to silently escalate privileges.  
- Ensures users consciously approve system-level changes.  

---

### Q&A Section  
1. **What is the primary purpose of UAC?**  
   - To reduce system compromise risk by requiring user approval for elevated actions.  

2. **How does UAC affect administrator accounts by default?**  
   - Admins run with standard privileges until elevation is requested via UAC prompt.  

3. **What visual indicator signifies a program requires elevated privileges?**  
   - A **shield icon** on the program’s executable or shortcut.  

4. **Why is the built-in local administrator account exempt from UAC?**  
   - Microsoft configures it to bypass UAC by default for legacy compatibility (not recommended for regular use).  

5. **What happens if a standard user tries to install a program needing admin rights?**  
   - UAC prompts for an administrator’s credentials; installation halts if credentials aren’t provided.  


---

## Settings and the Control Panel  

### **Key Differences**  
- **Control Panel**: Legacy interface for advanced settings (e.g., network adapters, user accounts).  
- **Settings**: Modern, streamlined UI for common tasks (e.g., wallpaper, updates).  

### **Accessing Both**  
- **Control Panel**: Start Menu > Search "Control Panel" > Open.  
- **Settings**: Start Menu > Click the gear icon (⚙️) or search "Settings".  

### **View Options in Control Panel**  
- **Category View**: Grouped by function (default).  
- **Small Icons View**: Alphabetical list of all settings (right-click menu for quick access).  

### **Q&A Section**  
1. **In the Control Panel, change the view to Small icons. What is the last setting in the Control Panel view?**  
   - **Work Folders** (alphabetically last entry in standard Windows 10 installations).  

---  

**Steps to Verify**:  
1. Open **Control Panel** > Click **View by** (top-right) > Select **Small icons**.  
2. Scroll to the bottom of the list.  

**Note**: If "Work Folders" is unavailable (e.g., disabled/not configured), the last entry may vary slightly (e.g., "Windows Defender Firewall").
![[Pasted image 20250120232957.png]]


Here’s a deeper, structured summary adhering strictly to your content while expanding on key details:  

---  

## Task Manager  

### **Overview**  
Task Manager is a system monitoring tool in Windows that displays real-time data about **applications**, **background processes**, and **resource usage** (CPU, RAM, disk, network). It enables users to:  
- Terminate unresponsive programs.  
- Monitor performance metrics.  
- Manage startup applications.  

---

### **Key Features**  
#### **Processes Tab**  
- Lists **apps** (user-facing programs) and **background processes** (system services).  
- Right-click any process to **End Task**, **Restart**, or view **File Location**.  

#### **Performance Tab**  
- Graphs for **CPU**, **Memory**, **Disk**, **GPU**, and **Network** utilization.  
- Example: Identify RAM bottlenecks by checking **Memory** > **In Use (GB)**.  

#### **Startup Tab**  
- Manage programs that launch at boot. Disable unnecessary apps to improve boot time.  

---

### **Access Methods**  
1. **Right-click Taskbar** > **Task Manager**.  
2. **Keyboard Shortcuts**:  
   | Shortcut              | Action                                  |  
   |-----------------------|-----------------------------------------|  
   | `Ctrl + Shift + Esc`  | Directly opens Task Manager.            |  
   | `Ctrl + Alt + Delete` | Opens security screen > Select Task Manager. |  

#### **View Modes**  
- **Simple View**: Minimal details (running apps only).  
- **More Details**: Expands to show **Processes**, **Performance**, **Startup**, etc.  

---

### **Practical Use Cases**  
- **Force-Quit Frozen Apps**: Select unresponsive app > **End Task**.  
- **Diagnose High CPU Usage**: Sort processes by **CPU%** to identify resource hogs.  
- **Track Malicious Activity**: Check unknown processes against trusted sources.  

---

### **Q&A Section**  
1. **What is the keyboard shortcut to open Task Manager?**  
   - **`Ctrl + Shift + Esc`**  

---
You can refer to this [blog post](https://www.howtogeek.com/405806/windows-task-manager-the-complete-guide/) for more detailed information about the Task Manager.

If you wish to learn more about the core Windows processes and what each process is responsible for, visit the [Core Windows Processes room](https://tryhackme.com/jr/btwindowsinternals).