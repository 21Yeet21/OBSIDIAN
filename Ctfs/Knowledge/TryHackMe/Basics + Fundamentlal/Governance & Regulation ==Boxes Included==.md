
## Important Terminologies

- **Governance**: Managing and directing an organisation or system to achieve its objectives and ensure compliance with laws, regulations, and standards.
	
	![[Pasted image 20250101200427.png]]
	
	Information security governance falls under the purview of top-tier management and includes the following processes:  
	
	- **Strategy**: Developing and implementing a comprehensive information security strategy that aligns with the organisation's overall business objectives.
	- **Policies and procedures**: Preparing policies and procedures that govern the use and protection of information assets.
	- **Risk management**: Conduct risk assessments to identify potential threats to the organisation's information assets and implement risk mitigation measures.
	- **Performance measurement**: Establishing metrics and key performance indicators (KPIs) to measure the effectiveness of the information security governance program.
	- **Compliance**: Ensuring compliance with relevant regulations and industry best practices.

- **Regulation**: A rule or law enforced by a governing body to ensure compliance and protect against harm.
-  **Compliance**: The state of adhering to laws, regulations, and standards that apply to an organisation or system.
	Here's a concise summary of the key benefits of governance and regulation:
	
	Security Benefits
	* Strengthens overall security posture through comprehensive programs
	* Reduces risk of breaches and unauthorized access
	* Enables more informed security decision-making
	
	Business Value
	* Aligns security with business objectives
	* Creates competitive advantage through demonstrated commitment
	* Builds stakeholder trust and confidence
	
	Compliance Impact  
	* Ensures adherence to key regulations (**GDPR, HIPAA, PCI DSS**)
	  ![[Pasted image 20250101201429.png]]
	* Prevents penalties and reputational damage
	* Promotes cost-effective security measures



## Information Security Frameworks

The information security framework provides a comprehensive set of documents that outline the organisation's approach to information security and governs how security is implemented, managed, and enforced within the organisation. 

> This mainly includes:

 - Policies: A formal statement that outlines an organisation's goals, principles, and guidelines for achieving specific objectives.
 - Standards: A document establishing specific requirements or specifications for a particular process, product, or service.
 - Guidelines: A document that provides recommendations and best practices (non-mandatory) for achieving specific goals or objectives.
 - Procedures: Set of specific steps for undertaking a particular task or process.
 - Baselines: A set of minimum security standards or requirements that an organisation or system must meet.


#### Developing Governance Documents
 Purpose
	A structured approach to creating organizational policies, standards, and guidelines
![[Pasted image 20250101203333.png]]

Identify the scope and purpose
* Determine document coverage and specific organizational needs (e.g., password policy for security)

Research and review
* Examine relevant laws, regulations, and industry standards
* Review existing organizational documents to prevent duplication

Draft the document
* Create content following best practices for clarity and actionability
* Ensure alignment with organizational goals and values

Review and approval
* Collect feedback from subject matter experts, legal teams, and management
* Obtain final stakeholder approval

Implementation and communication
* Distribute to relevant employees and stakeholders
* Develop training programs to ensure understanding

Review and update
* Conduct periodic reviews to maintain relevance
* Monitor compliance and adjust based on threat landscape changes


## Governance Risk and Compliance (GRC) ==Boxes Included==


![[Pasted image 20250101204826.png]]


###### Governance Component
Setting organizational direction through security strategy, policies, standards, baselines, frameworks, and establishing monitoring methods to measure performance and outcomes.

###### Risk Management Component
Identifying, assessing, and prioritizing risks, implementing controls, and continuously monitoring and refining risk management programs.

###### Compliance Component
Ensuring adherence to legal, regulatory, and industry obligations while aligning activities with internal policies through compliance programs, audits, and stakeholder reporting.

Here's a clear summary of the guidelines for developing a GRC program:

### How to Develop GRC Program - Generic Guidelines

###### Define the scope and objectives
Determine program boundaries and set specific, measurable goals - like reducing cyber risks by 50% within 12 months for a customer data management system.

###### Conduct a risk assessment
Identify and evaluate cyber risks, such as weak access controls or outdated software, then prioritize them for targeted management.

###### Develop policies and procedures
Create guidelines for cybersecurity practices, including specific policies like password requirements and system access monitoring.

###### Establish governance processes
Set up management structures like security steering committees and clearly define roles and responsibilities for program oversight.

###### Implement controls
Deploy both technical controls (firewalls, [Intrusion Prevention System (IPS)](https://tryhackme.com/room/idsevasion), [Intrusion Detection System (IDS)](https://tryhackme.com/room/redteamnetsec),  [Security Information and Event Management (SIEM)](https://tryhackme.com/room/introtosiem)) and non-technical measures (employee training) to address identified risks.

###### Monitor and measure performance
Create processes to track metrics and policy compliance, using the data to evaluate program effectiveness.

###### Continuously improve
Regularly review and update the program based on metrics, changing risks, and post-incident analyses to prevent future security issues.

## Privacy and Data Protection

###### General Data Protection Regulation (GDPR)

The [GDPR](https://gdpr-info.eu/) is a data protection law implemented by the EU in May 2018 to protect personal data. Personal data is "_Any data associated with an individual that can be utilised to identify them either directly or indirectly_". 

Key points of the law include the following:  
-  **Prior approval** must be obtained before collecting any personal data.
-  Personal data should be kept to a **minimum** and only collected when necessary.
-  **Adequate measures** are to be adopted to protect stored personal data.

![[Pasted image 20250101221205.png]]

**Payment Card Industry Data Security Standard (PCI DSS)**

[PCI DSS](https://www.pcisecuritystandards.org/) is focused on maintaining secure card transactions and protecting against data theft and fraud. It is widely used by businesses, primarily online, for card-based transactions. It was established by major credit card brands (Visa, MasterCard & American Express). It requires strict control access to cardholder information and monitoring unauthorised access, using recommended measures such as web application firewalls and encryption. You can learn more about the standard [here](https://docs-prv.pcisecuritystandards.org/PCI%20DSS/Supporting%20Document/PCI_DSS-QRG-v4_0.pdf).

## NIST Special Publications

###### NIST
[NIST 800-53](https://nvlpubs.nist.gov/nistpubs/SpecialPublications/NIST.SP.800-53r5.pdf)  is a publication titled "**Security and Privacy Controls for Information Systems and Organisations**",  developed by the National Institute of Standards and Technology (NIST), US, that provides a catalogue of security controls to protect the CIA triad of information systems. The publication serves as a framework for organisations to assess and enhance the security and privacy of their information systems and comply with various laws, regulations, and policies. It incorporates best practices from multiple sources, including industry standards, guidelines, and international frameworks.

###### Key Points
NIST 800-53 offers a comprehensive set of security and privacy controls that organisations can use to safeguard their operations, assets, personnel, and other organisations from various threats and risks. These include intentional attacks, unintentional errors, natural disasters, infrastructure failures, foreign intelligence activity, and privacy concerns. NIST 800-53 Revision 5 organises security controls into twenty families, each addressing a specific security concern category. You can learn more about the controls [here](https://nvlpubs.nist.gov/nistpubs/SpecialPublications/NIST.SP.800-53r5.pdf) (Section 2.2).

![[Pasted image 20250101225231.png]]


###### Developing and Implementing NIST 800-53 based Information Security Program

Among all the families, "**Program Management**" is one of the crucial control of the NIST 800-53 framework. Program Management control mandates establishing, implementing, and monitoring organisation-wide programs for information security and privacy while safeguarding the processed, stored, or transmitted through systems. To ensure program management, the following subcontrols are necessary to be implemented:

![[Pasted image 20250101225615.png]]

![[Pasted image 20250101230155.png]]

## Information Security Management and Compliance

 **Information Security Management Overview**
- IS management encompasses planning, executing, and maintaining security measures to protect information assets
- Focuses on preventing unauthorized access, use, disclosure, disruption, modification, and destruction
- Includes risk assessment, security controls, incident response, and training

**Compliance**
- Involves adherence to legal, regulatory, contractual, and industry-specific standards in information security

**ISO/IEC 27001 Standard**
Core components:
- Scope: Defines ISMS boundaries and covered assets
- Security Policy: High-level document outlining organizational security approach
- Risk Assessment: Evaluates threats to information confidentiality, integrity, and availability
- Risk Treatment: Implements controls to mitigate identified risks
- Statement of Applicability: Documents applicable and non-applicable controls
- Internal Audit: Conducts periodic ISMS effectiveness reviews
- Management Review: Regular evaluation of ISMS performance

Note: The ISO/IEC 27001 standard is available for purchase through official channels.[link](https://www.iso.org/standard/27001)

![[Pasted image 20250101231452.png]]

###### SOC 2 Overview

**Core Concept**
- Compliance framework developed by AICPA to assess data security effectiveness based on CIA triad
- Primarily evaluates how service providers handle client data and sensitive information

**Key Components**
- Evaluates controls for:
  - Confidentiality
  - Availability
  - Integrity
  - Privacy

**Significance**
- Demonstrates security commitment to stakeholders
- Provides competitive advantage
- Required by many customers
- Independent auditors verify security controls

**Audit Process**
- Management must:
  - Define scope of systems and processes
  - Select qualified auditor
  - Plan audit timeline and criteria
  - Review existing controls and address gaps
  - Undergo control testing and interviews
  - Receive detailed audit report with findings

**Primary Purpose**
- Ensures third-party service providers securely handle sensitive data
- Validates security controls meet industry standards
- Provides documentation of security practices for stakeholders
![[Pasted image 20250101232323.png]]
