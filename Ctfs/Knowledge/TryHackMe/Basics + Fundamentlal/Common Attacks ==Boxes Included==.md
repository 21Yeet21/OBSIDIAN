

## Social Engineering

 - Social Engineering is the term used to describe any cyberattack where a _human_ (rather than a computer) is the target; for this reason, it is sometimes referred to as "People Hacking".

The best way to understand social engineering is to see it in action! These videos from [Defcon23](https://youtu.be/fHhNWAKw0bY?t=100) (one of the largest hacking conferences in the world) and [CNN](https://youtu.be/PWVN3Rq4gzw) demonstrate some of the immense power in social engineering. They are both well worth a watch!

###### How to protect yourself from social engineering

by adding layers of authentication 


## Social Engineering: Phishing


###### Definition

- **Phishing**: A type of social engineering attack where an attacker tricks a victim into opening a malicious webpage via email, text, or other online correspondence.
- **Related Terms**:
    - **Smishing**: Phishing via SMS.
    - **Vishing**: Phishing via voice or video calls.

###### Key Characteristics

- Exploits human vulnerabilities rather than system flaws.
- Often involves large-scale deployment using stolen or leaked contact information.

###### Psychological Tactics

- Induces a false sense of urgency to prompt rash decisions.

###### Typical Attack Flow

1. Victim receives a phishing message containing a malicious link.
2. Victim clicks the link and is directed to a fake website.
3. Victim provides sensitive information (e.g., login credentials or credit card data) or downloads malware.
4. Attacker collects the information or gains access to the victim's device.

###### Impacts

- Compromised credentials or personal data.
- Potential malware infection and unauthorized network access.


![[Pasted image 20250103172331.png]]

#### **Identifying Phishing Attacks**


**Common Traits of Generic Phishing**

- **Easy to Spot**:
    - Poor grammar.
    - Generic greetings (e.g., "Dear customer").
- **Advanced Attacks**:
    - Some are sophisticated enough to fool even cybersecurity professionals.

###### Plausible Pretexts

- Examples:
    - Fake messages from "banks" about unusual account activity.
    - Scams mimicking trusted services like Amazon.
- **Spearphishing/Whaling**:
    - Highly targeted and carefully crafted to deceive specific individuals.

###### Domain Name Tricks

- **Similar Domains**:
    - Slight alterations to legitimate domain names (e.g., replacing “L” with “1”).
    - Example: Using `royalmai1.co.uk` instead of `royalmail.co.uk`.
- **HTML Emails**:
    - Fake links masked with legitimate-looking URLs.
    - Example: Displayed as `https://amazon.co.uk` but links to `https://am4zon.co.uk`.
		- e.g.![[Pasted image 20250103173910.png]]
		
###### Email Red Flags

- **Suspicious "From" Addresses**:
    - Generic Gmail or unrelated domain names instead of official ones.

###### Best Practice for Detection

- Stay vigilant and look for mistakes or inconsistencies in emails, links, and domains.

## Malware and Ransomware


###### Overview

- **Malware**: Software designed for malicious actions.
    - Goals: Steal information, cause damage, or execute commands on infected systems.
    - Common use: Enables "Command and Control" (C2), allowing remote control of infected devices.
    - Features: May include keylogging and other malicious tasks.

###### Ransomware

- **Definition**: A specialized type of malware that encrypts data and demands a ransom for decryption.
- **Spread**: Exploits known software vulnerabilities (e.g., Microsoft Windows).
    - Extremely fast-spreading.
- **Objective**:
    - Infect as many systems as possible.
    - Encrypt and make data inaccessible.
- **Ransom Payment**:
    - Demands are typically in cryptocurrency (e.g., Bitcoin).
    - Ransomware displays a message demanding payment to decrypt data.
	    - ![[Pasted image 20250103175202.png]]
#### **Delivery Methods**


1. **Social Engineering & Phishing**

- Attackers often use emails with malicious attachments (e.g., Word or Excel files containing macros).
- Macros only run if the victim clicks the _Enable Content_ button.
	- ![[Pasted image 20250103175656.png]]
	
- Attackers exploit pretexts to convince users to enable macros.

2. **Malicious File Formats**

Attackers may deliver malware in various formats:

- Compiled executables (.exe)
- PDF documents
- PowerShell scripts (.ps1)
- Batch scripts (.bat)
- HTML application files (.hta)
- JavaScript files (.js)

3. **Exploiting Infrastructure Vulnerabilities**

- Attackers may exploit vulnerabilities in public-facing infrastructure, like web servers, in corporate environments.
- This provides access to internal networks for larger attacks facilitated by malware.

  

#### **Staying Safe**


##### Key Practices

- **Update and Patch**:
    
    - Accept software updates promptly, especially for operating systems.
    - Updates often address security vulnerabilities.
- **Avoid Suspicious Links and Attachments**:
    
    - Do not click on links or open attachments from suspicious emails.
    - Delete or report suspicious messages, especially in a work environment.
- **Beware of Downloads**:
    
    - Avoid downloading or running files sent via email or messaging unless verified.
- **Handle Unknown Media Safely**:
    
    - Never plug unknown USB or other media devices into important computers.
- **Back Up Data**:
    
    - Regular backups can be crucial for recovering from ransomware attacks.
- **Keep Antivirus Active**:
    
    - Ensure antivirus software is updated and always running.

##### ==Ransomware Response==

- **Do Not Pay the Ransom**:
    - Contact local authorities immediately.
    - Isolate the infected device by disabling its internet connection.
    - Avoid powering off the device to preserve potential decryption options.


## Passwords and Authentication

#### **Overview of Password Security**

- Passwords are crucial but often insecure.
- Security risks include:
    - Weak passwords.
    - Password reuse.
    - Poor storage practices.

#### **Strong vs. Weak Passwords**

- **Strong Passwords:**
    - Emphasize length over complexity.
    - Examples:
        - Traditional: `@Ed1nburgh#1988-2000!`
        - Passphrase: `Vim is _obviously_, indisputably the best text editor!`
        - Random: `w41=V1)S7KIJGPN,dII>cHEh>FRVQsj3M^]CB`
    - Best practice: Use a password manager.
- **Weak Passwords:**
    - Follow predictable patterns (e.g., `Gareth2012!`).
    - Are short or easily guessed (e.g., personal info).

#### **Exposed Passwords**

- **Storage Methods:**
    
    - Plaintext: Unsafe.
    - Encrypted: Better but still vulnerable.
    - Hashed: Industry standard (secure, irreversible).
- **Risks of Data Breaches:**
    
    - Best case: Email leaked, password safe.
    - Worst case: Password cracked, credential stuffing possible.
    - Mitigation: Use services like ==_Have I Been Pwned?_== for breach notifications.

#### **Password Attacks**

- **Local Attacks:**
    
    - Use stolen hashed passwords.
    - Techniques:
        - Brute-force: Random characters.
        - Wordlists: Pre-generated passwords.
        - Hybrid: Mutated wordlists.
- **Remote Attacks:**
    
    - Brute-force usernames.
    - Credential stuffing using leaked credentials.

## Multi-Factor Authentication and Password Managers



###### **Multi-Factor Authentication (MFA)**

- **Definition**: Requires more than one factor to log in.
- **Common Example**: Password + Time-based One-Time Password (TOTP) via phone.
- **Three Authentication Factors**:
    - **Something you have**: Smart card, TOTP, or hardware key (e.g., YubiKey).
    - **Something you know**: Password.
    - **Something you are**: Biometric data (e.g., fingerprint, iris scan).
- **Recommendation**: Use MFA wherever possible, preferably with authenticator apps (e.g., Authy, Google Authenticator) over SMS-based TOTP, which is less secure.

######  **Password Managers**

- **Purpose**: Securely store and manage passwords in encrypted "vaults."
- **Features**:
    - Generate and auto-fill strong, random passwords.
    - Store additional data (e.g., files, images).
    - Accessible via master password or biometrics.
- **Popular Tools**:
    - 1Password
    - LastPass
    - KeePass
    - Bitwarden
- **Caution**: Master password must be strong, as it secures the entire vault.

###### **Key Takeaways**

- Always enable MFA for added security.
- Use a password manager to store unique, strong passwords securely.

## Public Network Safety


- **Public WiFi Risks**: Common in public spaces like cafés and restaurants, but often insecure.
- **Man-in-the-Middle Attacks**: Attackers can set up fake networks to intercept and monitor your traffic.
    - **Example**: Logging into a website over HTTP (not HTTPS) on a malicious network allows attackers to steal your credentials.
- **Network Visibility**: Devices on public networks are exposed to other users, increasing the risk of attack.

###### Solutions for Staying Safe

- **Avoid Untrusted Networks**: The safest option is to avoid public networks altogether. Use private networks or mobile hotspots instead.
- **Use a VPN**:
    - Encrypts all your traffic, making it unreadable to attackers.
    - Commercial VPNs like ProtonVPN and Mullvad VPN are recommended, though free VPNs often compromise security by selling user data.

###### Website Connection Security

- **Encrypted Connections**: Websites should use HTTPS (via TLS) to protect user data.
    - **Indication**: A padlock icon in the browser shows that the connection is secure.
- **HTTPS**: Prevents attackers from reading or modifying traffic, ensuring data safety on public networks.
	- ![[Pasted image 20250103185515.png]]



###### **Secure Connections**

- **Padlock Symbol**: Indicates an encrypted connection (TLS) but does not guarantee the website's safety.
    - A site may have TLS encryption but still be malicious.

###### **Avoiding Untrusted Networks**

- **No Padlock**: Never enter sensitive information on a site without the padlock symbol, especially on untrusted networks.

###### **Altered Padlock Icon**

- **Crossed or Exclamation Mark**: Indicates potential issues with the certificate, ranging from an expired certificate to possible interference from attackers.
    - **Do not trust** connections with these icons.

###### **Certificate Errors**

- **Full-page Certificate Errors**: If you encounter these errors (e.g., in Firefox), avoid proceeding, as the connection might be insecure.
    - Action: **Go back** to prevent exposure to risks.
	    - ![[Pasted image 20250103185849.png]]

#### **Vs**

![[Pasted image 20250103191302.png]]

![[Pasted image 20250103191416.png]]


![[Pasted image 20250103191449.png]]


## Backups ==Boxes Included==

###### Importance of Backups

- Backups are essential for protecting data.
- They ensure data recovery regardless of damage severity.
- They can be personal (e.g., family photos) or business-critical (e.g., work data).

###### The Golden 3,2,1 Rule

- **3 Copies:** Keep at least three copies of data.
- **2 Different Mediums:** Store backups on at least two different types of storage (e.g., cloud, USB).
- **1 Off-Site:** Store one backup off-site (e.g., cloud services like Google Drive).
	- ![[Pasted image 20250103192945.png]]
	- 

###### Backup Frequency

- Backup frequency depends on data sensitivity and risk level.
- High-risk businesses may back up multiple times a day.
- Personal users may back up weekly or bi-weekly.

## Updates and Patches 
###### Software Updates

- **Importance of Updates**:
    
    - Essential for adding features, fixing bugs, and addressing security vulnerabilities.
    - Patches are released to fix vulnerabilities once discovered.
- **Case Study: Eternal Blue**:
	    ["Blue" room on TryHackMe](https://tryhackme.com/room/blue)
    - A vulnerability in Windows discovered by NSA, leaked in April 2017.
    - Allowed attackers remote control of a target system.
    - Microsoft quickly released a patch (the infamous [MS17-010](https://docs.microsoft.com/en-us/security-updates/SecurityBulletins/2017/ms17-010)), but many administrators didn't apply it.
    - Exploited by the WannaCry ransomware to spread and infect unpatched systems.
    - You can read more about Eternal Blue [here](https://www.sentinelone.com/blog/eternalblue-nsa-developed-exploit-just-wont-die/).
- **End of Life (EOL)**:
    
    - Software eventually loses support and stops receiving updates (e.g., Windows 7).
    - Must be replaced or segregated to minimize exploitation risks.

###### Antivirus Updates

- **Frequent Updates**:
    
    - Antivirus software updates regularly to keep malware signatures current.
- **Signatures**:
    
    - New malware generates unique signatures.
    - These signatures are distributed globally to antivirus users for detection.
- **Consequences of Outdated Antivirus**:
    
    - Without updates, the local malware database becomes outdated.
    - New malware may evade detection.
- **Key Point**:
    
    - Always allow antivirus software to update to ensure protection.