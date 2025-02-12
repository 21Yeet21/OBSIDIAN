
##  Methodology Outline

### What process does a hacker follow?

Contrary to the assumption that hackers act randomly, professional hackers and penetration testers typically follow an established process. This structured methodology ensures consistency and standardization across the industry during assessments.

### Steps in the Hacker Methodology

1. **Reconnaissance**
    
    - Gathering information about the target to identify potential entry points or weaknesses.
2. **Enumeration/Scanning**
    
    - Actively probing the target to gather detailed insights, such as open ports, services, and vulnerabilities.
3. **Gaining Access**
    
    - Exploiting identified vulnerabilities to gain unauthorized access to the system or network.
4. **Privilege Escalation**
    
    - Increasing access privileges within the system to gain full control or access sensitive information.
5. **Covering Tracks**
    
    - Removing evidence of the attack to avoid detection and maintain persistence.
6. **Reporting**
    
    - Documenting findings, including the exploited vulnerabilities and steps taken, to provide a clear understanding of the assessment.



## Reconnaissance Overview

### The First Phase: Reconnaissance

Reconnaissance is the initial phase in the ethical hacker methodology, focused on gathering information about a target without direct interaction with the target system. It involves using publicly available tools and resources to collect data about organizations, technologies, or individuals.

### Tools and Techniques for Reconnaissance

#### Common Tools

- **Google**: A powerful search engine often used for gathering general information or conducting advanced searches (Google Dorking).
- **Wikipedia**: For understanding the target's history and background.
- **Social Media Platforms (e.g., Twitter, YouTube)**: To track updates, news releases, and promotional content.
- **LinkedIn**: For researching the organization's structure, open positions, and employee profiles.

#### Specialized Tools

- **PeopleFinder.com**: For searching individuals' public records.
- **who.is**: For domain and IP ownership information.
- **sublist3r**: A tool for enumerating subdomains of a target domain.
- **hunter.io**: To discover professional email addresses.
- **builtwith.com**: For analyzing the technology stack used by a website.
- **wappalyzer**: A browser extension to detect technologies behind a website.

### Importance of Reconnaissance

Although it may seem straightforward, reconnaissance is the **most critical phase** of penetration testing. It lays the groundwork for identifying potential vulnerabilities and planning subsequent steps effectively.

### Questions

1. **Who is the CEO of SpaceX?**
    
    - **Elon Musk**
2. **What does sublist3r list?**
    
    - Sublist3r lists **subdomains** of a target domain, helping hackers or pentesters identify additional entry points.
3. **What is it called when you use Google to look for specific vulnerabilities or research a specific topic of interest?**
    
    - **Google Dorking**




## Enumeration and Scanning Overview

### The Second Phase: Scanning and Enumeration

In this phase, hackers interact with the target to identify vulnerabilities and determine the attack surface. Specialized tools are used to gain insights into the target’s weaknesses, which are then exploited in the next phase.

### Key Activities in Scanning and Enumeration

#### Interaction with the Target

- The hacker probes the system to uncover its **attack surface**, identifying what it might be vulnerable to.
- Common vulnerabilities include:
    - Improperly secured web pages.
    - Information leakage.
    - SQL Injection.
    - Cross-Site Scripting (XSS).

#### Purpose of Enumeration

- **Identify what the target is vulnerable to**, providing actionable insights for the exploitation phase.

### Tools for Scanning and Enumeration

#### General Tools

- **Nmap**:
    - Scans the target to determine:
        - Open ports.
        - Operating system and its version.
        - Running services and their versions.
- **dirb/dirbuster**:
    - Enumerate commonly-named directories on a website.
- **enum4linux**:
    - Focuses on vulnerabilities specific to Linux systems.
- **metasploit**:
    - Primarily for exploitation but includes enumeration capabilities.
- **Burp Suite**:
    - Scans websites for subdirectories and intercepts network traffic.

#### Example Scenario with Nmap

- Scanning reveals open ports, such as FTP, HTTP, or SSH.
- The operating system and service versions are identified, enabling targeted exploitation.

### Questions

1. **What does enumeration help to determine about the target?**
    
    - Enumeration helps determine **the vulnerabilities present in the target** and the **overall attack surface**.
2. **What company developed the tool Metasploit?**
    
    - **Rapid7**
3. **What company developed the technology behind Burp Suite?**
    
    - **PortSwigger**



## Exploitation Overview

### The Fourth Phase: Exploitation

The exploitation phase is often portrayed as the most exciting part of penetration testing, but its success heavily depends on the groundwork laid during the **reconnaissance** and **enumeration** phases. Without proper preparation, chosen exploits may fail, or key vulnerabilities may be overlooked.

### Key Points about Exploitation

- It involves using identified vulnerabilities to gain unauthorized access to the target.
- The process requires a solid understanding of the vulnerabilities discovered earlier.
- Tools make exploitation easier, but thorough preparation ensures success.

### Common Exploitation Tools

- **Metasploit**: A versatile exploitation framework with built-in scripts for a variety of vulnerabilities.
- **Burp Suite**: Can exploit web application vulnerabilities like SQL Injection and Cross-Site Scripting.
- **SQLMap**: Automates SQL Injection attacks.
- **msfvenom**: Used to create custom payloads.
- **BeEF**: Specialized in browser-based exploitation.

### Question

**What is one of the primary exploitation tools that pentester(s) use?**

- **Metasploit**



## Privilege Escalation Overview

### The Fifth Phase: Privilege Escalation

After gaining initial access during the exploitation phase, the next step is to escalate privileges to gain full control of the target system. This typically involves accessing higher-level accounts such as:

- **Windows**: Administrator or SYSTEM accounts.
- **Linux**: Root account.

### Key Concepts in Privilege Escalation

- **Operating System Identification**:  
    Knowing the operating system is crucial to determine the appropriate privilege escalation methods.
    
- **Methods of Privilege Escalation**:
    
    - Cracking password hashes.
    - Exploiting vulnerable services or their versions.
    - Password spraying or reusing credentials.
    - Using default credentials.
    - Finding secret keys (e.g., SSH keys) stored on the system.
    - Enumerating system settings using commands like:
        - `ifconfig`: To identify network configurations.
        - `find / -perm -4000 -type f 2>/dev/null`: To locate files with SUID permissions, which may allow privilege escalation.

### Ultimate Goal

To gain administrative or root-level access to "own" the machine or pivot to another target within the network.

### Questions

1. **In Windows, what is usually the other target account besides Administrator?**
    
    - **SYSTEM**
2. **What thing related to SSH could allow you to log in to another machine (even without knowing the username or password)?**
    
    - **SSH keys**
## Covering Tracks Overview

### The Sixth Phase: Covering Tracks

While **covering tracks** is part of the hacker methodology, ethical penetration testers rarely need to perform this step due to the planned and agreed-upon nature of professional assessments.

### Key Points

#### Ethical Penetration Testing

- Ethical hackers always have **explicit permission** from the system owner before testing.
- The **rules of engagement** outline:
    - When the test will occur.
    - How it will proceed.
    - The scope of targets to be assessed.

#### Avoid Covering Tracks

- **Professionals do not cover their tracks**, as transparency and accountability are critical in ethical hacking.
- Once privilege escalation is achieved, the penetration tester stops and **reports findings** to the client.

#### Responsibilities After Exploitation

- **Assist in Cleanup**:
    - Remove exploit code and artifacts left during testing.
- **Provide Recommendations**:
    - Suggest how to fix vulnerabilities and prevent similar attacks in the future.
- **Document Tasks**:
    - Keep a detailed record of all activities performed during the assessment.

### Summary

Covering tracks may be part of the hacker methodology, but ethical hackers focus on transparency, cleanup, and clear communication with the client to ensure security improvements.




