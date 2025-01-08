![[Pasted image 20250101235726.png]]


## Recon

![[Pasted image 20250102000409.png]]

**Reconnaissance Overview**
- Reconnaissance is the initial planning phase where adversaries discover and gather system/victim information
- Functions as prerequisite for subsequent attack phases

**OSINT Component**
- OSINT (Open-Source Intelligence) is a key reconnaissance activity
- Involves collecting publicly available information about the target organization and employees, including:
  - Company size
  - Email addresses 
  - Phone numbers
- Enables attackers to identify optimal targets for their attacks

**Famous Recon Tools**
- [theHarvester](https://github.com/laramies/theHarvester) - other than gathering emails, this tool is also capable of gathering names, subdomains, IPs, and URLs using multiple public data sources 
- [Hunter.io](https://hunter.io/) - this is  an email hunting tool that will let you obtain contact information associated with the domain
- [OSINT Framework](https://osintframework.com/) - OSINT Framework provides the collection of OSINT tools based on various categories

## Weaponization

![[Pasted image 20250102000852.png]]

###### Key Terminology

- **Malware**: Software designed to damage, disrupt, or gain unauthorized access to a system.
- **Exploit**: Code that exploits vulnerabilities in applications or systems.
- **Payload**: Malicious code executed on the target system.

###### Weaponization Phase Actions

1. **Choosing a Payload**:
    
    - "Megatron" opts to purchase a pre-written payload from the [DarkWeb](https://www.kaspersky.com/resource-center/threats/deep-web) to save time.
2. **Methods of Weaponization**:
    
    - **Malicious Documents**:
        - Embedding malicious macros or VBA scripts in Microsoft Office files.
        - Reference: ["Intro to Macros and VBA For Script Kiddies" by TrustedSec](https://www.trustedsec.com/blog/intro-to-macros-and-vba-for-script-kiddies/).
    - **Infected USB Drives**:
        - Crafting sophisticated worms or viruses to implant on USB drives for public distribution.
    - **Command and Control (C2)**:
        - Utilizing C2 techniques to execute commands or deliver additional payloads.
        - Reference: [MITRE ATT&CK](https://attack.mitre.org/tactics/TA0011/).
    - **Backdoor Implants**:
        - Selecting a backdoor method to bypass security mechanisms and maintain access.

This phase is critical for preparing the malicious payload and method of delivery for the target system.

## Delivery

![[Pasted image 20250102005615.png]]


 **Methods of Delivering Malware**

- **Phishing Email**
    
    - Targets individuals or groups using deceptive emails.
    - Example:
        - Attacker impersonates a known contact (e.g., "Scott").
        - Sends a fake invoice email containing malware to a target (e.g., "Nancy").
- **Infected USB Drives**
    
    - USBs left in public places or mailed with deceptive branding.
    - Example:
        - USBs branded with company logos sent as fake gifts.
        - Malware activates when USBs are connected.
        - you can read more [CSO Online "Cybercriminal group mails malicious USB dongles to targeted companies."](https://www.csoonline.com/article/3534693/cybercriminal-group-mails-malicious-usb-dongles-to-targeted-companies.html)
- **Watering Hole Attack**
    
    - Compromises commonly visited websites.
    - Techniques:
        - Exploiting website vulnerabilities.
        - Redirecting visitors to malicious websites.
        - Using drive-by downloads (e.g., fake browser extensions).
    - Example:
        - Attacker sends "harmless" emails linking to compromised websites.

## Exploitation

![[Pasted image 20250102010243.png]]


**Key Actions by the Attacker**

- **Phishing Exploits:**
    
    - **Email with Malicious Link:** Leads to a fake Office 365 login page.
    - **Macro Attachment:** Executes ransomware when opened.
    - Result: Two victims clicked the link and opened the file.
- **Post-Access Exploitation:**
    
    - Exploiting vulnerabilities in software, systems, or servers.
    - Escalating privileges or moving laterally in the network to access sensitive data.
    - **Lateral Movement Definition ([CrowdStrike](https://www.crowdstrike.com/cybersecurity-101/lateral-movement/)):**  
        Techniques to deepen access in a network after initial entry.
- **Zero-Day Exploits:**
    
    - **Definition (FireEye):** Unknown software or hardware vulnerabilities exploited before detection.
    - **Impact:** No early detection opportunities.

#### Examples of Exploitation Techniques

- Triggering exploits through email links or attachments.
- Using zero-day vulnerabilities [FireEye](https://www.fireeye.com/current-threats/what-is-a-zero-day-exploit.html).
- Exploiting software, hardware, or human vulnerabilities.
- Attacking server-based systems.

#### Learn More

If you want to learn more about server-based or web-based vulnerabilities, please refer to the TryHackMe room
- [TryHackMe OWASP Top 10 Room](https://tryhackme.com/room/owasptop10)

## Installation

![[Pasted image 20250102011524.png]]

 ###### Purpose of Persistence

- **Definition:** Persistence ensures that an attacker retains access to a compromised system even if the initial access is lost or removed.
- **Backdoor:** Also called an access point, it bypasses security measures and enables re access. **[persistent backdoor](https://www.offensive-security.com/metasploit-unleashed/persistent-backdoors/)** are essential for long-term access.

Learn more about persistence in the[Windows Persistence Room](https://tryhackme.com/room/windowslocalpersistence).

###### Techniques for Persistence

1. **Web Shell Installation**
    
    - Malicious scripts (e.g., ASP, PHP, JSP) used to maintain access.
    - Often hard to detect due to benign file formats (e.g., `.php`, `.asp`).
    - More details: [Microsoft article on web shell attacks](https://www.microsoft.com/security/blog/2020/08/26/web-shell-attacks-continue-to-rise/).
2. **Backdoor Installation with [Meterpreter](https://www.offensive-security.com/metasploit-unleashed/meterpreter-backdoor/) t
    
    - Interactive shell from the Metasploit Framework to remotely control the victim’s machine.
3. **Windows Services Manipulation (T1543.003)**
    
    - Create or modify services to run malicious scripts or payloads regularly.
    - Tools:
        - `sc.exe` (manages Windows services).
        - `Reg` (modifies service configurations).
    - Masquerades malware under legitimate-sounding service names.
    - Reference: [MITRE ATT&CK Windows Services Manipulation](https://attack.mitre.org/techniques/T1543/003/).
4. **Registry Run Keys / Startup Folder Entries**
    
    - Adds malicious payloads to the registry or startup folder to execute on user login.
    - Reference: [MITRE ATT&CK Registry Run Keys / Startup Folder](https://attack.mitre.org/techniques/T1547/001/).

#### Additional Persistence Techniques

- **[Timestomping](https://attack.mitre.org/techniques/T1070/006/)**: Alters file timestamps (create, access, modify, change) to avoid detection and make malware appear legitimate.

## Command & Control

![[Pasted image 20250102012727.png]]



#### Definition

- **C2 Channel (or C&C):**  
    A malicious communication link between a compromised host and an attacker’s external server, enabling remote control of the victim’s machine.
    - **C2 Beaconing:** Regular communication between the infected host and the C2 server.

#### Process

1. **Establishing Connection:**
    
    - Malware on the victim's machine connects to an attacker-controlled external server.
    - Provides the attacker full control over the system.
2. **Evolution of C2 Channels:**
    
    - Traditional: **IRC (Internet Relay Chat)**—easily detected by modern security solutions.
    - Modern: Protocols designed to blend with legitimate traffic or evade detection.

#### Common C2 Channels

1. **HTTP (Port 80) and HTTPS (Port 443):**
    
    - Blends malicious traffic with legitimate web traffic.
    - Evades firewalls.
2. **DNS (Domain Name System):**
    
    - Uses DNS requests to communicate with attacker-controlled DNS servers.
    - Known as **DNS Tunneling**.

#### Key Notes

- The C2 infrastructure can be owned by an adversary or another compromised host.
- Modern C2 techniques leverage legitimate-looking traffic to avoid detection.

For more insights, explore resources on [DNS Tunneling](https://owasp.org/www-project-dns-tunneling/) and [HTTP/HTTPS C2 traffic](https://www.crowdstrike.com/resources/what-is-command-and-control/).


## Actions on Objectives (Exfiltration)

![[Pasted image 20250102013335.png]]



#### Final Phase Goals

After completing the attack phases, the attacker gains hands-on access to achieve their objectives, which may include:

1. **Credential Collection:**
    
    - Harvesting user credentials for further exploitation.
2. **Privilege Escalation:**
    
    - Gaining elevated privileges (e.g., domain administrator access) by exploiting system misconfigurations.
3. **Internal Reconnaissance:**
    
    - Interacting with internal software to identify vulnerabilities.
4. **Lateral Movement:**
    
    - Navigating through the company’s environment to expand control.
5. **Data Exfiltration:**
    
    - Collecting and transferring sensitive data outside the organization.
6. **Backup and Shadow Copy Deletion:**
    
    - Removing backups and **Shadow Copies** (Microsoft's backup technology) to prevent recovery.
7. **Data Corruption or Overwriting:**
    
    - Altering, corrupting, or erasing data to disrupt operations or conceal traces.

This phase represents the culmination of the attacker’s efforts to meet their original objectives.