
### **Putting It All Together**

When you request a website, multiple processes work together to deliver the page to you. Here's a summary of these steps:

![[Pasted image 20250112232635.png]]

#### **1. DNS Resolution**

- Your computer needs to know the IP address of the web server hosting the website. It uses the Domain Name System (DNS) to look up the domain name and resolve it to an IP address.

#### **2. HTTP Protocol Communication**

- After resolving the server's IP, your computer communicates with the web server using the Hypertext Transfer Protocol (HTTP). This protocol defines the set of rules for requesting and transferring data between the client (your computer) and the server.

#### **3. Server Response**

- The server processes the request and returns various elements necessary for the website to display properly. This includes:
    - HTML (structure of the webpage)
    - CSS (styling for the webpage)
    - JavaScript (interactivity and dynamic behavior)
    - Images and other media

#### **4. Rendering the Website**

- Your browser takes the server's response and renders the content, combining HTML, CSS, JavaScript, and media files, to display the webpage in a way you can interact with and navigate.

This process happens quickly and seamlessly, allowing you to view and interact with websites almost instantly!




### Other Components

![[Pasted image 20250112233600.png]]

#### **Load Balancers**

When websites experience high traffic or need high availability, a **load balancer** is used to distribute incoming requests across multiple servers. This ensures the servers can handle the load and provides failover if one server becomes unresponsive. Load balancers use algorithms like **round-robin** or **weighted** to decide which server should handle a request. They also perform **health checks** on servers to ensure they are operational, stopping traffic from being sent to a non-responding server.

#### **CDN (Content Delivery Networks)**

A **CDN** is used to speed up website performance by hosting static files (such as JavaScript, CSS, images, and videos) on multiple servers distributed globally. When a user requests these files, the CDN directs the request to the server physically closest to the user, improving load times and reducing traffic to the main web server.

#### **Databases**

Websites often need to store and retrieve user data. **Databases** are used to store this information, which can range from simple text files to complex clusters of servers for better speed and resilience. Common databases include **MySQL, MSSQL, MongoDB**, and **PostgreSQL**.

#### **WAF (Web Application Firewall)**

A **WAF** sits between the user and the web server to protect against attacks like hacking or denial of service. It inspects web requests for signs of malicious activity, filters out suspicious traffic, and uses **rate limiting** to control the number of requests from a single IP, preventing overloads or attacks.

---

### **Q & A**

1. **What can be used to host static files and speed up a client's visit to a website?**
    
    - A **CDN (Content Delivery Network)** can be used to host static files and speed up a client's visit by serving the content from the nearest server.
2. **What does a load balancer perform to make sure a host is still alive?**
    
    - A load balancer performs **health checks** to ensure that the server is responsive and functioning properly.
3. **What can be used to help against the hacking of a website?**
    
    - A **WAF (Web Application Firewall)** helps protect a website from hacking by inspecting web traffic and blocking malicious requests.
	    - ![[Pasted image 20250112233619.png]]


## How Web Servers Work

#### **What is a Web Server?**

A **web server** is software that listens for incoming connections and uses the HTTP protocol to deliver content to clients. Popular web server software includes **Apache, Nginx, IIS,** and **NodeJS**. Web servers serve files from their **root directory**, a location defined in their settings (e.g., `/var/www/html` on Linux for Apache and Nginx, or `C:\inetpub\wwwroot` on Windows for IIS).

#### **Virtual Hosts**

Web servers can host multiple websites by using **virtual hosts**. These are configuration files that allow the server to serve different websites based on the requested hostname. For example, `one.com` can be mapped to `/var/www/website_one`, while `two.com` is mapped to `/var/www/website_two`.

#### **Static Vs Dynamic Content**

- **Static content** does not change, such as images, CSS, JavaScript, and static HTML. It is directly served by the web server.
- **Dynamic content** can change based on different requests. For example, a blog's homepage shows the latest entries, which update when new content is added. This dynamic behavior is created using **backend scripting languages**.

#### **Scripting and Backend Languages**

Backend languages like **PHP, Python, Ruby, NodeJS,** and **Perl** process data, interact with databases, and generate dynamic content. These languages enable interactivity, such as personalized greetings or search results. A PHP script might output customized content based on a user's input without revealing the backend code to the client.

---

### **Q & A**

1. **What does web server software use to host multiple sites?**
    
    - Web server software uses **virtual hosts** to host multiple websites with different domain names.
2. **What is the name for the type of content that can change?**
    
    - The type of content that can change is called **dynamic content**.
3. **Does the client see the backend code? Yay/Nay**
    
    - **Nay**, the client does not see the backend code. They only see the output generated by the backend, typically in HTML format.

![[Pasted image 20250112234434.png]]
![[Pasted image 20250112234457.png]]
![[Pasted image 20250112234512.png]]



![[Pasted image 20250112235316.png]]


## Skills for a Penetration Tester

Read enough of job descriptions, and the usual suspects start to crop up. Let’s break down the core capabilities required.

_As an entry-level Penetration Tester, your role involves evaluating the security posture of computer systems, networks, and applications through simulated cyberattacks. You will collaborate with cyber security teams to perform comprehensive penetration testing activities, including:_

Vulnerability Assessment

Conducting thorough assessments to identify potential vulnerabilities in systems, networks, and applications.

Penetration Testing

Utilising ethical hacking techniques to exploit identified vulnerabilities and assess the extent of potential security risks.

Web Application Testing

Evaluating the security of web applications by assessing vulnerabilities such as SQL injection, cross-site scripting (XSS), and authentication bypass.

Network Security Testing

Analysing network infrastructure for weaknesses such as misconfigurations, insecure protocols, and unauthorised access points.

Social Engineering Testing

Simulating social engineering attacks to assess the effectiveness of security awareness training and measures.

Reporting and Documentation

Documenting findings, testing methodologies, and recommended remediation actions in clear and detailed reports.

Collaboration and Communication

Working closely with developers, system administrators, and stakeholders to prioritise and address security issues effectively.

Continuous Learning

Keeping abreast of emerging cybersecurity threats, trends, and best practices to enhance testing methodologies and security measures.

### Required Skills:

Technical Proficiency

Knowledge of networking protocols, operating systems (e.g., Windows, Linux), and web technologies (e.g., HTTP/HTTPS, HTML, JavaScript)

Security Tools

Familiarity with penetration testing tools such as Nmap, Metasploit, Burp Suite, Wireshark, and vulnerability scanners

Cyber Security Concepts

Understanding of encryption, authentication mechanisms, access control models, and common security frameworks (e.g., NIST, ISO 27001)

Analytical Skills

Ability to analyse vulnerability scan results, penetration test findings, and system logs to identify security issues and potential attack vectors

Problem-Solving Abilities

Strong critical thinking and problem-solving skills to devise creative solutions for complex security challenges

Communication Skills

Excellent verbal and written communication skills to effectively report findings, articulate technical concepts, and collaborate with diverse teams

Certifications

[Industry certifications](https://tryhackme.com/r/resources/blog/certifications-in-cyber-security) such as Certified Ethical Hacker (CEH), Offensive Security Certified Professional (OSCP), or related credentials are advantageous.


![[Pasted image 20250113001115.png]]
