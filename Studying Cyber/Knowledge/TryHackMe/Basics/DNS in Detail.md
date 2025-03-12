



## **Task 1: What is DNS?**

#### **What is DNS?**

DNS (Domain Name System) provides a user-friendly way to communicate with devices on the internet without needing to remember complex numbers (IP addresses).

- **IP Address**: A unique number assigned to each device on the internet. Example: `104.26.10.229`.
- ![[Screenshot_2025-01-12_21-33-34.png]]
- 
- **DNS Function**: Translates human-readable domain names (like `tryhackme.com`) into IP addresses, making internet navigation easier.


### Q & A
#### **What does DNS stand for?**

DNS stands for **Domain Name System**.




## **Task 2: Domain Hierarchy**

#### **Domain Hierarchy**

A structure where:

- The **root domain** is at the top, branching into:
    - **Top-Level Domains (TLDs)**
    - **Second-Level Domains (SLDs)**

#### **TLD (Top-Level Domain)**

The rightmost part of a domain name. Example: in `tryhackme.com`, the TLD is `.com`.

- **Types of TLDs**:
    - **gTLD (Generic)**: Indicates domain purpose (e.g., `.com` for commercial, `.org` for organizations, `.edu` for education).
    - **ccTLD (Country Code)**: Indicates geographic origin (e.g., `.ca` for Canada, `.co.uk` for the UK).
- Example gTLDs: `.online`, `.club`, `.biz`.
- 
 For a full list of over 2000 TLDS [click here](https://data.iana.org/TLD/tlds-alpha-by-domain.txt).
#### **Second-Level Domain**

Example: In `tryhackme.com`, `tryhackme` is the **Second-Level Domain** (SLD).

- **Length Limit**: Up to 63 characters + TLD.
- **Allowed Characters**: `a-z`, `0-9`, and hyphens (but no hyphens at the start, end, or consecutively).

#### **Subdomain**

A name to the left of the SLD, separated by a period. Example: `admin.tryhackme.com` (`admin` is the subdomain).

- **Length Limit**: 63 characters per subdomain, total domain name limited to 253 characters.
- **Allowed Characters**: Same as SLD (`a-z`, `0-9`, hyphens).
- Example with multiple subdomains: `jupiter.servers.tryhackme.com`.

### **Q & A**

#### **What is the maximum length of a subdomain?**

**63 characters**

#### **Which of the following characters cannot be used in a subdomain (3, b, _, -)?**

**_ (underscore)**

#### **What is the maximum length of a domain name?**

**253 characters**

#### **What type of TLD is .co.uk?**

**ccTLD (Country Code Top-Level Domain)**



## **Task 3: DNS Record Types**

#### **DNS Record Types**

DNS is not limited to websites; it includes different record types for various purposes.

#### **A Record**

- Resolves to an IPv4 address.
- Example: `104.26.10.229`.

#### **AAAA Record**

- Resolves to an IPv6 address.
- Example: `2606:4700:20::681a:be5`.

#### **CNAME Record**

- Resolves to another domain name.
- Example: `store.tryhackme.com` returns a CNAME pointing to `shops.shopify.com`.
- A second DNS request resolves the IP for `shops.shopify.com`.

#### **MX Record**

- Specifies mail server addresses for handling email for a domain.
- Includes a **priority flag** to determine the order of servers to contact.
- Example: `alt1.aspmx.l.google.com`.

#### **TXT Record**

- Free text fields for storing text-based data.
- Common uses:
    - Listing servers authorized to send email on behalf of a domain (helps reduce spam).
    - Verifying domain ownership for third-party services.

### **Q & A**

#### **What type of record would be used to advise where to send email?**

**MX Record**

#### **What type of record handles IPv6 addresses?**

**AAAA Record**



## **Task 4: Making a Request**

#### **What Happens When You Make a DNS Request**

When you request a domain name, your computer follows these steps:

1. **Local Cache Check**:
    
    - Your computer first checks its own cache for the domain’s IP address.
2. **Recursive DNS Server**:
    
    - If not found, the request is sent to the **Recursive DNS Server** (usually provided by your ISP or a custom service).
    - If cached, it returns the result; if not, it contacts the **root DNS servers**.
3. **Root DNS Servers**:
    
    - Directs the request to the appropriate **Top-Level Domain (TLD) Server** based on the domain's extension (e.g., `.com`).
4. **TLD Server**:
    
    - Refers to the **Authoritative DNS Server** for the specific domain.
5. **Authoritative DNS Server**:
    
    - Holds the DNS records for the domain.
    - Sends the record back to the Recursive DNS Server, which caches it for future use and returns it to the original client.
6. **Time To Live (TTL)**:
    
    - Specifies how long the DNS record should be cached locally before expiring.

### **Q & A**

#### **What field specifies how long a DNS record should be cached for?**

**TTL (Time To Live)**

#### **What type of DNS Server is usually provided by your ISP?**

**Recursive DNS Server**

#### **What type of server holds all the records for a domain?**

**Authoritative DNS Server**


## Practice

![[Pasted image 20250112221208.png]]

![[Pasted image 20250112221248.png]]


![[Pasted image 20250112221635.png]]