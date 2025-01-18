
## Introduction

### Key Topics:

1. **Passive Reconnaissance**: Gathering information without directly engaging with the target system, making it undetectable.
2. **Active Reconnaissance**: Directly interacting with the target to gather information, which may be detected.
3. **Nmap**: A powerful tool for network scanning and host discovery. You'll learn about:
    - **Live Host Discovery**: Identifying active devices in a network.
    - **Basic and Advanced Port Scans**: Scanning for open ports on a target.
    - **Post Port Scans**: Analyzing results after scanning ports.
4. **Protocols and Servers**: Understanding different network protocols and services.
5. **Network Security Challenge**: A practical challenge to apply what you've learned.

### Tools You'll Learn:

1. **WHOIS**: A command-line tool to query WHOIS servers for domain ownership and registration information.
2. **nslookup**: A command-line tool for querying DNS servers to resolve domain names to IP addresses.
3. **dig**: Another DNS query tool, more flexible than nslookup, used for gathering detailed DNS information.

### Online Services:

1. **DNSDumpster**: An online service for gathering DNS information about a target without direct interaction.
2. **Shodan.io**: A search engine for discovering devices connected to the internet, used for gathering information about a target.

### Pre-requisite Knowledge:

- Basic networking knowledge
- Familiarity with the command line

You will need VPN access to complete tasks that require internet connectivity.

---

As you progress through the module, these tools and services will help you collect important information about your target for network security assessments

## Passive Versus Active Recon

This room expects the user to have a working knowledge of computer networks. If you want to refresh or build on this knowledge, you're encouraged to study the Network Fundamentals module first.

### Reconnaissance: The First Step

In the Art of War, Sun Tzu stated, "If you know the enemy and know yourself, your victory will not stand in doubt." Whether you're an attacker or a defender, gathering information about your target is crucial. As an attacker, reconnaissance helps you understand the weaknesses of a target system, and as a defender, it helps you understand what your adversary can learn about your systems.

Reconnaissance can be broken down into two categories:

### **Passive Reconnaissance**

Passive reconnaissance involves gathering information that is publicly available, without directly interacting with the target system. It's like observing the target from afar, without ever stepping onto their territory.

**Examples of passive reconnaissance activities:**

- Looking up DNS records of a domain from public DNS servers.
- Checking job advertisements related to the target company.
- Reading news articles and reports about the target organization.

This type of reconnaissance does not alert the target, making it useful for stealthy intelligence gathering.

### **Active Reconnaissance**

In contrast, active reconnaissance requires direct interaction with the target. It’s more like physically examining the locks on doors or windows of a building — it involves probing systems and services directly, and it can alert the target to your presence.

**Examples of active reconnaissance activities:**

- Directly connecting to company servers (e.g., HTTP, FTP, SMTP).
- Attempting social engineering (e.g., calling the company to extract information).
- Physically infiltrating company premises under false pretenses (e.g., pretending to be a repairman).

Active reconnaissance can lead to legal issues unless proper authorization is obtained, as it can be considered intrusive.


## Summary: WHOIS Command and Its Output

**WHOIS Overview:** WHOIS is a protocol used to query domain registration information. It allows you to obtain details about a domain name, such as:

- **Registrar**: The company through which the domain is registered.
- **Registrant Info**: Contact details of the domain owner, including name, address, and email.
- **Creation and Expiry Dates**: When the domain was registered and when it will expire.
- **Name Servers**: The servers responsible for resolving the domain name.

**WHOIS for TryHackMe.com:**

1. **Domain Registration Date**: TryHackMe.com was registered on **July 5, 2018**.
2. **Registrar**: The domain is registered with **Namecheap Inc.**.
3. **Name Servers**: This information would typically appear in the "Name Server" field. However, WHOIS often omits it if privacy protection is in place, or you can use tools like `dig` to confirm it.

**Key Points:**

- WHOIS is a valuable tool for gathering domain and contact details.
- Some registrants use privacy services to obscure their details.
- WHOIS data can help identify attack vectors for penetration tests, such as social engineering or targeting specific services linked to the domain.

This covers the information you can gather with WHOIS and its application for reconnaissance. Let me know if you need more details!


## `nslookup` and `dig` for DNS Queries

#### **nslookup**

`nslookup` (Name Server Lookup) is a command-line tool used to query DNS servers to obtain information about domain names, such as IP addresses and mail servers. It is helpful in tasks like penetration testing for gathering domain information.

**Key Parameters for nslookup:**

- **OPTIONS**: The query type, such as:
    - `A`: IPv4 Addresses
    - `AAAA`: IPv6 Addresses
    - `CNAME`: Canonical Name
    - `MX`: Mail Servers
    - `SOA`: Start of Authority
    - `TXT`: TXT Records
- **DOMAIN_NAME**: The domain name you want to look up.
- **SERVER**: The DNS server you want to query (e.g., 1.1.1.1 for Cloudflare or 8.8.8.8 for Google).

**Example Usage:**

- To get IPv4 addresses for a domain:  
    `nslookup -type=A tryhackme.com 1.1.1.1`
- To get mail server information:  
    `nslookup -type=MX tryhackme.com`

**Output Example for `nslookup -type=A tryhackme.com 1.1.1.1`:**

```
Non-authoritative answer:
Name: tryhackme.com
Address: 172.67.69.208
Name: tryhackme.com
Address: 104.26.11.229
```

The query can reveal important data for penetration testing, like available IP addresses or mail servers, which can be further investigated for vulnerabilities.

#### **dig**

`dig` (Domain Information Groper) is another DNS lookup tool that provides more advanced functionality compared to `nslookup`. It can be used to query various DNS records and is known for offering detailed results, including the Time To Live (TTL) for records.

**Key Parameters for dig:**

- **SERVER**: The DNS server to query (optional).
- **DOMAIN_NAME**: The domain name to look up.
- **TYPE**: The DNS record type, similar to `nslookup` (e.g., `MX` for mail servers).

**Example Usage:**

- To get mail exchange records for a domain:  
    `dig tryhackme.com MX`
- To query a specific DNS server (e.g., Cloudflare):  
    `dig @1.1.1.1 tryhackme.com MX`

**Output Example for `dig tryhackme.com MX`:**

```
; <<>> DiG 9.16.19-RH <<>> tryhackme.com MX
;; global options: +cmd
;; Got answer:
;; ->>HEADER<<
```

**Comparison of nslookup and dig:**

- `nslookup` provides concise output, while `dig` returns more detailed information, including TTL and additional DNS data.
- Both tools allow querying specific DNS servers and different types of records.

Both `nslookup` and `dig` are valuable tools for gathering domain-related information during reconnaissance, which can reveal useful details for further investigation or attack preparation.

## DNSDumpster: Discovering Subdomains and DNS Information

DNSDumpster is a valuable online tool for discovering detailed DNS information about domains, including subdomains that might not be easily found through traditional tools like `nslookup` or `dig`. It allows you to search for domain information, including DNS records, subdomains, mail servers (MX records), and more. DNSDumpster can also graphically represent this data, making it easier to visualize.

#### **Steps to Use DNSDumpster:**

1. **Go to DNSDumpster**: Open the web browser and visit [DNSDumpster](https://dnsdumpster.com/).
2. **Enter the Domain Name**: Type the domain you're interested in (e.g., `tryhackme.com`).
3. **Review Results**:
    - **Subdomains**: DNSDumpster will list known subdomains, including those that may not be immediately visible through standard queries.
    - **DNS Servers**: Information about DNS servers and their IP addresses.
    - **Mail Servers**: Mail exchange (MX) records with their associated IP addresses.
    - **TXT Records**: Additional metadata about the domain.

#### **Example for `tryhackme.com` on DNSDumpster**:

In addition to the common subdomains like `www` and `blog`, DNSDumpster might reveal additional subdomains like:

- **`wiki.tryhackme.com`**
- **`webmail.tryhackme.com`**

These subdomains could hold valuable information and are typically overlooked by basic queries.

Additionally, DNSDumpster provides:

- **DNS servers**: Their IP addresses and geolocation.
- **MX records**: The mail servers associated with the domain.
- **Graphical Representation**: The data is displayed as a graph for easier visualization and analysis.

By using DNSDumpster, you can quickly uncover subdomains and other DNS-related data that would be time-consuming to find manually through other means.

### Shodan.io: Discovering Exposed Devices and Services

Shodan.io is a powerful search engine that indexes information about internet-connected devices, including servers, routers, webcams, and more. Unlike traditional search engines that index web pages, Shodan focuses on identifying and collecting data from devices reachable online. This makes it an excellent tool for passive reconnaissance in penetration testing, as it allows you to gather detailed information about a target network without actively interacting with it.

#### **How Shodan Works:**

1. **Scanning and Indexing**: Shodan continuously scans the internet for devices connected to it. When a device responds, Shodan collects various pieces of information, such as:
    
    - IP address
    - Geolocation
    - Service information (e.g., web server type/version)
    - Hosting company and more.
2. **Database**: All the collected data is saved and indexed, making it searchable for anyone interested in learning about specific devices or networks.
    
3. **Search Engine**: You can search Shodan for details about a specific domain (e.g., `tryhackme.com`), or directly search for IP addresses that you've obtained through other reconnaissance tools (e.g., `nslookup` or `dig`).
    

#### **Example:**

When searching for `tryhackme.com` on Shodan.io, you might find details such as:

- **IP Address**: The public IP address of the server hosting the domain.
- **Hosting Company**: Information about the company that provides hosting for the server.
- **Geographic Location**: The physical location of the server.
- **Server Type and Version**: Details about the server's software, which can help you identify potential vulnerabilities or outdated versions.

#### **How Shodan Helps in Penetration Testing:**

- **Passive Reconnaissance**: Shodan allows you to gather valuable information without directly interacting with the target. This minimizes the risk of alerting the target.
- **Discover Exposed Devices**: It helps identify devices and services that are unintentionally exposed to the internet, such as unsecured webcams, routers, and legacy servers.
- **Service Fingerprinting**: By identifying the software and version running on a device, Shodan allows you to spot outdated or vulnerable services that might be exploitable.

### Summary: Passive Reconnaissance

In this room, we focused on **passive reconnaissance**, specifically using various **command-line tools** and **public services** to gather information about targets without actively connecting to them. Mastering these tools can yield a wealth of information about a target, providing valuable insights during penetration testing.

#### **Covered Tools and Services:**

- **Command-Line Tools**:
    - **WHOIS**: Used to gather domain registration details.
    - **nslookup**: Queries DNS servers for various types of records.
    - **dig**: An advanced DNS query tool offering more detailed results.
- **Public Services**:
    - **DNSDumpster**: An online service to discover subdomains, DNS records, and more, often revealing information not easily found with basic tools.
    - **Shodan.io**: A search engine that indexes internet-connected devices, offering valuable data about servers, services, and more.

#### **Common Reconnaissance Commands**:

|**Purpose**|**Command-line Example**|
|---|---|
|Lookup WHOIS record|`whois tryhackme.com`|
|Lookup DNS A records|`nslookup -type=A tryhackme.com`|
|Lookup DNS MX records at DNS server|`nslookup -type=MX tryhackme.com 1.1.1.1`|
|Lookup DNS TXT records|`nslookup -type=TXT tryhackme.com`|
|Lookup DNS A records|`dig tryhackme.com A`|
|Lookup DNS MX records at DNS server|`dig @1.1.1.1 tryhackme.com MX`|
|Lookup DNS TXT records|`dig tryhackme.com TXT`|

By using these tools and services, you can collect detailed information about a target's domain, DNS records, and even discover exposed devices or subdomains that could be potential attack vectors. With practice, you can leverage these results to improve your penetration testing and reconnaissance efforts.