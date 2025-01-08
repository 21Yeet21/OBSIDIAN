### CIA

![[58a85d2e5942ebf3e78eb01c82f563be.png]]

- **Confidentiality** ensures that only the intended persons or recipients can access the data.
- **Integrity** aims to ensure that the data cannot be altered; moreover, we can detect any alteration if it occurs.
- **Availability** aims to ensure that the system or service is available when needed.
Going one more step beyond the CIA security triad, we can think of:

- **Authenticity**: Authentic means not fraudulent or counterfeit. Authenticity is about ensuring that the document/file/data is from the claimed source.
- **Nonrepudiation**: Repudiate means refusing to recognize the validity of something. Nonrepudiation ensures that the original source cannot deny that they are the source of a particular document/file/data. This characteristic is indispensable for various domains, such as shopping, patient diagnosis, and banking.

 
 ==Parkerian Hexad==

In 1998, Donn Parker proposed the Parkerian Hexad, a set of six security elements. They are:

1. Availability
2. Utility
3. Integrity
4. Authenticity
5. Confidentiality
6. Possession

We have already covered four of the above six elements. Let's discuss the remaining two elements:

- **Utility**: Utility focuses on the usefulness of the information. For instance, a user might have lost the decryption key to access a laptop with encrypted storage. Although the user still has the laptop with its disk(s) intact, they cannot access them. In other words, although still available, the information is in a form that is not useful, i.e., of no utility.
- **Possession**: This security element requires that we protect the information from unauthorized taking, copying, or controlling. For instance, an adversary might take a backup drive, meaning we lose possession of the information as long as they have the drive. Alternatively, the adversary might succeed in encrypting our data using ransomware; this also leads to the loss of possession of the data.

### DAD

![[1742c9b384adb60b896481b2416d2f8a.png]]

The security of a system is attacked through one of several means. It can be via the disclosure of secret data, alteration of data, or destruction of data.

- **Disclosure** is the opposite of confidentiality. In other words, disclosure of confidential data would be an attack on confidentiality.
- **Alteration** is the opposite of Integrity. For example, the integrity of a cheque is indispensable.
- **Destruction/Denial** is the opposite of Availability.



### Security Models

==Bell-LaPadula Model==

The Bell-LaPadula Model aims to achieve **confidentiality** by specifying three rules:

- **Simple Security Property**: This property is referred to as “no read up”; it states that a subject at a lower security level cannot read an object at a higher security level. This rule prevents access to sensitive information above the authorized level.
- **Star Security Property**: This property is referred to as “no write down”; it states that a subject at a higher security level cannot write to an object at a lower security level. This rule prevents the disclosure of sensitive information to a subject of lower security level.
- **Discretionary-Security Property**: This property uses an access matrix to allow read and write operations. An example access matrix is shown in the table below and used in conjunction with the first two properties.

---
There are certain limitations to the Bell-LaPadula model. For example, it was not designed to handle file-sharing.


==Biba Model==

The Biba Model aims to achieve **integrity** by specifying two main rules:

- **Simple Integrity Property**: This property is referred to as “no read down”; a higher integrity subject should not read from a lower integrity object.
- **Star Integrity Property**: This property is referred to as “no write up”; a lower integrity subject should not write to a higher integrity object.
 ---
 Biba Model suffers from various limitations. One example is that it does not handle internal threats (insider threat).


==Clark-Wilson Model==

The Clark-Wilson Model also aims to achieve integrity by using the following concepts:

- **Constrained Data Item (CDI)**: This refers to the data type whose integrity we want to preserve.
- **Unconstrained Data Item (UDI)**: This refers to all data types beyond CDI, such as user and system input.
- **Transformation Procedures (TPs)**: These procedures are programmed operations, such as read and write, and should maintain the integrity of CDIs.
- **Integrity Verification Procedures (IVPs)**: These procedures check and ensure the validity of CDIs.


We covered only three security models. The reader can explore many additional security models. Examples include:

- Brewer and Nash model
- Goguen-Meseguer model
- Sutherland model
- Graham-Denning model
- Harrison-Ruzzo-Ullman model

# ISO/IEC 19249 Security Architecture Principles

## Overview
ISO/IEC 19249:2017 outlines architectural principles for secure systems, products, and applications development.

## Five Core Principles

### 1. Domain Separation
- Groups related components (apps, data, resources) into distinct entities
- Assigns common security attributes to each domain
- Example: x86 processor rings (kernel in ring 0 (the most privileged level), user apps in ring 3)

### 2. Layering
- Structures systems into abstract levels
- Enables security policy implementation at multiple levels
- Examples: OSI network model, programming language disk operations
- Related to Defense in Depth concept

### 3. Encapsulation
- Hides implementation details and restricts direct data access
- Provides controlled methods for data manipulation
- Examples: OOP methods, API interfaces for database access

### 4. Redundancy
- Ensures system availability and data integrity
- Examples: 
  - Dual power supplies in servers
  - RAID 5 storage configuration
  - Parity checking for data integrity

### 5. Virtualization
- Enables hardware sharing among multiple operating systems
- Provides security through:
  - Sandboxing capabilities
  - Secure environment for malware analysis
  - Enhanced security boundaries

# ISO/IEC 19249 Security Design Principles

## Overview
ISO/IEC 19249:2017 specifies five design principles for secure system development.

## Core Design Principles

### 1. Least Privilege
- Grants minimal permissions required for task completion
- Based on "need-to-know" access model
- Example: Providing read-only access when write permissions aren't needed

### 2. Attack Surface Minimization
- Reduces potential vulnerability points
- Addresses both known and unknown vulnerabilities
- Example: Disabling unnecessary services during Linux system hardening

### 3. Centralized Parameter Validation
- Consolidates input validation in one library/system
- Protects against invalid inputs that could exploit vulnerabilities
- Prevents issues like denial of service and code execution

### 4. Centralized Security Services
- Consolidates security functions in central location
- Example: Centralized authentication server
- Requires redundancy to prevent single point of failure

### 5. Error and Exception Handling
- Designs systems to fail safely
- Accounts for inevitable errors and exceptions
- Key aspects:
  - Fail-safe defaults (e.g., firewall blocking all traffic on crash)
  - Protection of sensitive information in error messages
  - Handling of common scenarios (e.g., out-of-stock items)
---
# Trust Principles in Security

## Trust but Verify
* Maintains trust while requiring verification through logging and monitoring
* Not feasible to verify everything manually - requires automated security tools like proxies and IDS(intrusion detection)/IPS(intrusion prevention systems)
* Balances trust with verification mechanisms

## Zero Trust
* Treats trust itself as a vulnerability, especially addressing insider threats
* Requires authentication and authorization for all resource access
* Does not automatically trust devices based on location or ownership
* Uses Micro segmentation
* to isolate network segments down to individual hosts
* Must be balanced against business needs and practicality

The key difference is that "Trust but Verify" allows for baseline trust with verification, while "Zero Trust" assumes no trust by default and requires proof of trustworthiness for every interaction.


### Threat versus Risk
![[Pasted image 20241227112137.png]]

There are three terms that we need to take note of to avoid any confusion.

- **Vulnerability**: Vulnerable means susceptible to attack or damage. In information security, a vulnerability is a weakness.
- **Threat**: A threat is a potential danger associated with this weakness or vulnerability.
- **Risk**: The risk is concerned with the likelihood of a threat actor exploiting a vulnerability and the consequent impact on the business.
---
Infrastructure as a Service (IaaS) user has complete control (and responsibility) over the operating system.

---
Software as a Service (SaaS) user has no direct access to the underlying operating system


