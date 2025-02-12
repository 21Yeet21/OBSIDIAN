
---

## **Task 1: Introduction**  

### **Why Research is Critical for Hackers**  
Research is the most vital skill in hacking. No one knows everything, and every hacker, regardless of experience, will face problems they can’t solve immediately. Research fills this gap, as real-world hacking rarely provides easy answers.  

### **Research Grows with Experience**  
As you gain experience, the complexity of your research will increase. However, in cybersecurity, you’ll always need to look things up—there’s no endpoint where research becomes unnecessary.  


---

## **Task 2: Example Research Question**  

### **Starting with a Research Question**  
You’re given a JPEG image from a remote server and suspect something is hidden inside. The question is: *How can you extract hidden data from the image?*  

---

### **Step 1: Searching for Techniques**  
A Google search for “hiding things inside images” leads to the discovery of **steganography**, a technique for hiding data within images.  

---

### **Step 2: Finding Tools for Steganography**  
Searching for “extract files using steganography” reveals useful tools and resources. The first link points to a collection of steganography tools, including **steghide**, which can extract data from JPEG files.  

---

### **Step 3: Installing Steghide**  
A search for “apt” (a Linux package manager) explains how to install tools like steghide using the command:  
```bash
sudo apt install steghide
```  

---

### **Step 4: Using Steghide**  
The steganography tools page also provides instructions on how to use steghide to extract hidden data from an image.  

---

### **Research Methodology**  
1. Start with a question (e.g., *How can I extract data from this image?*).  
2. Search for an initial answer (e.g., steganography).  
3. Dive deeper into the topic (e.g., tools like steghide).  
4. Continue researching until you fully understand the process.  

---

## **Task 3: Vulnerability Searching**  

### **Why Search for Vulnerabilities?**  
In hacking, you’ll often encounter software that may be exploitable. For example, Content Management Systems (CMS) like WordPress, FuelCMS, or Ghost are common targets due to their frequent vulnerabilities.  

---

### **Key Resources for Vulnerability Research**  
1. **ExploitDB**: A database of exploits that can often be used directly.  
2. **NVD (National Vulnerability Database)**: Tracks CVEs (Common Vulnerabilities and Exposures), even if no exploit is publicly available.  
3. **CVE Mitre**: Another resource for CVE information.  

CVEs follow the format: **CVE-YEAR-IDNUMBER**.  

---

### **Using ExploitDB and Searchsploit**  
- **ExploitDB**: Useful for finding ready-to-use exploits.  
- **Searchsploit**: A CLI tool in Kali Linux that allows offline searching of ExploitDB.  

---

### **Example: Searching for FuelCMS Exploits**  
1. Identify the software (e.g., FuelCMS).  
2. Use `searchsploit fuel cms` or search ExploitDB online.  
3. Find an exploit (e.g., a remote code execution vulnerability in FuelCMS 1.4.1).  
4. Note the CVE number for further research.  

---

### **Important Notes on CVEs**  
- CVEs are assigned when vulnerabilities are discovered, not when they are publicized.  
- A CVE from late in the year might be published the following year.  



---

## **Task 4: Manual Pages**  

### **Why Use Linux Manual Pages?**  
Linux (especially Kali Linux) is the most widely used OS in hacking. The `man` command provides access to manual pages for most tools directly in the terminal, making it a go-to resource for understanding how to use tools and their options.  

---

### **Using the `man` Command**  
- Syntax: `man <tool_name>` (e.g., `man ssh`).  
- Displays detailed information about the tool, including usage, syntax, and available switches.  

---

### **Example: Using `man` for SSH**  
1. Run `man ssh` to view the SSH manual page.  
2. Find the syntax for connecting to a remote computer: `<user>@<host>`.  
3. Search for specific switches (e.g., `-V` to display the SSH version).  

---

### **Searching Within Manual Pages**  
Use `grep` to search for specific keywords within a manual page. For example:  
```bash
man ssh | grep -i "version"
```  

---

