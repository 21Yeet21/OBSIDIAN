### Active Reconnaissance Summary

In the "Active Reconnaissance" room, the focus shifts from passive to active methods of gathering information about a target. Unlike passive reconnaissance, which relies on publicly available information without direct engagement, active reconnaissance involves direct interaction with the target, such as visiting their website, testing open ports, or even engaging in social engineering tactics.

#### Key Points:

1. **Definition**:
    
    - Active reconnaissance involves direct contact with the target system or organization.
    - It can leave traces, such as logs showing IP addresses and connection times.
2. **Examples of Active Reconnaissance**:
    
    - Visiting websites to simulate regular client activity.
    - Testing firewall configurations or open ports (e.g., SSH).
    - Using social engineering to gather information.
3. **Tools Covered**:
    
    - **Web Browser**: Utilizing developer tools for gathering information.
    - **Ping**: To check connectivity with the target.
    - **Traceroute**: To map the path to the target system.
    - **Telnet and Netcat (nc)**: For connecting to and interacting with target services.
4. **Ethical Considerations**:
    
    - Always obtain signed legal authorization before performing active reconnaissance.
5. **User Considerations**:
    
    - Web browser tools may require practice to master, while command-line tools like ping and traceroute are relatively simple to use.

#### Note:

If not subscribed to the AttackBox service, ensure a VPN connection for tools requiring internet access.


### Summary: Ping

Ping is a network diagnostic tool used to verify connectivity and determine if a target system is online. It operates using ICMP (Internet Control Message Protocol), sending an **ICMP Echo Request** to the target and receiving an **ICMP Echo Reply** if the system is reachable.

#### Key Points:

1. **Purpose**:
    
    - Check if the target system is online and reachable.
    - Ensure network connectivity before proceeding with detailed scans.
2. **How It Works**:
    
    - Ping sends packets to a target system.
    - If the target is online, it replies with an ICMP Echo Reply.
    - Firewalls or network devices may block these packets.
3. **Command Usage**:
    
    - `ping TARGET_IP` sends continuous packets until manually stopped.
    - `ping -c COUNT TARGET_IP` limits the number of packets sent (Linux).
    - Equivalent command on Windows: `ping -n COUNT TARGET_IP`.
4. **Technical Details**:
    
    - Ping uses **ICMP Echo Request (type 8)** and **ICMP Echo Reply (type 0)**.
    - Common issues when no reply is received:
        - Target is offline or unresponsive.
        - Network issues (e.g., unplugged cables or faulty devices).
        - Firewalls blocking ICMP packets (e.g., Windows Firewall blocks ping by default).
5. **Example**:
    
    - Successful ping:
        - 5 packets transmitted, 5 received, 0% packet loss.
    - Unsuccessful ping:
        - "Destination Host Unreachable" message with 100% packet loss.
6. **Penetration Testing Context**:
    
    - Ping helps confirm that the target system is online.
    - It is a precursor to further reconnaissance, such as port and service scans.

#### Questions and Answers:

1. **Which option would you use to set the size of the data carried by the ICMP echo request?**  
    `-s SIZE`
    
2. **What is the size of the ICMP header in bytes?**  
    **==8 bytes==**
    
3. **Does MS Windows Firewall block ping by default? (Y/N)**  
    **Y**
    
4. **Deploy the VM for this task and using the AttackBox terminal, issue the command `ping -c 10 10.10.90.42`. How many ping replies did you get back?**  
    Verify by running the command, but if the target is online, expect **10 replies**.


### **Traceroute Summary**

Traceroute is a network diagnostic tool used to trace the route packets take from your system to a target host. It reveals the IP addresses of intermediate routers (hops) and the number of hops between your system and the target.

- **Purpose:**  
    Traceroute identifies the route and latency to the target host, helping diagnose network issues.
    
- **How It Works:**  
    Traceroute uses the Time To Live (TTL) field in the IP header to ==“trick”== routers into revealing their IP addresses.
    ![[Pasted image 20250114111837.png]]
    
    - Packets are sent with an increasing TTL value.
    - Each router decrements the TTL by 1; when TTL reaches 0, the router discards the packet and sends back an ICMP "Time-to-Live Exceeded" message.
    - The source system uses these ICMP replies to map the route.
- **Key Points:**
    
    - Different traceroute runs may show varying routes due to dynamic routing protocols.
    - Some routers may not reply to the ICMP messages, leading to incomplete results.
    - Traceroute commands:
        - Linux/macOS: `traceroute MACHINE_IP`
        - Windows: `tracert MACHINE_IP`
- **Examples:**
    
    - **Traceroute A:** Packets passed through 14 routers to reach `tryhackme.com`.
    - **Traceroute B:** Packets passed through 26 routers to reach `tryhackme.com`.
    - In both cases, responses varied due to dynamic routing.

---

#### **Q&A Session**

1. **What is the IP address of the last router/hop before reaching `tryhackme.com` in Traceroute A?**
    
    - **Answer:** `100.92.9.3`.
2. **What is the IP address of the last router/hop before reaching `tryhackme.com` in Traceroute B?**
    
    - **Answer:** `99.83.89.19`.
3. **How many routers are between the two systems in Traceroute B?**
    
    - **Answer:** 26 routers.
4. **How can you identify the number of hops to a target system using traceroute?**
    
    - **Answer:** Run the `traceroute` or `tracert` command and count the numbered lines in the output. Each line corresponds to one hop.
5. **Why do some traceroute runs show different results?**
    
    - **Answer:** Routes may change due to dynamic routing protocols or network conditions.
6. **What does a `*` symbol in the traceroute output mean?**
    
    - **Answer:** It indicates no ICMP reply was received from the router.
7. **How can traceroute help in penetration testing?**
    
    - **Answer:** Traceroute can reveal network topology and intermediate public IPs, which may assist in footprinting during penetration testing.

---

### **How to return to line**

To return to a new line in **Netcat**, press `Shift+Enter`; in **Telnet**, press `Enter` twice.
### **Telnet Summary**

Telnet is a protocol developed in 1969 that allows communication with a remote system via a command-line interface (CLI). It operates on **port 23** by default. However, Telnet sends all data, including credentials, in plaintext, making it insecure for modern usage. The secure alternative is **SSH (Secure Shell)**.

Despite its security issues, Telnet can still be used for tasks like grabbing banners or testing TCP services. It works by connecting to a specific port and sending protocol-specific commands.

#### **Using Telnet to Grab Banners**

1. Use `telnet [IP_ADDRESS] [PORT]` to connect to a service.
2. Communicate with the server using the appropriate protocol (e.g., HTTP, SMTP).
3. Example for HTTP:
    - Enter ==`GET / HTTP/1.1`.==
    - Add ==`host: [hostname]`== in order to get a valid response and press Enter twice.
4. The server responds with details like its software type and version.

#### **Example Interaction**

```plaintext
pentester@TryHackMe$ telnet 10.10.253.149 80
Trying 10.10.253.149...
Connected to 10.10.253.149.
Escape character is '^]'.
GET / HTTP/1.1
host: telnet

HTTP/1.1 200 OK
Server: nginx/1.6.2
Date: Tue, 17 Aug 2021 11:13:25 GMT
...
```

- **Server:** nginx
- **Version:** 1.6.2

---

#### **Q&A Session**

1. **What is the name of the running server?**
    
    - **Answer:** nginx
2. **What is the version of the running server (on port 80 of the VM)?**
    
    - **Answer:** 1.6.2

### **Netcat Summary**

Netcat (often referred to as `nc`) is a versatile networking utility that supports **TCP** and **UDP** protocols. It can act as either a client or a server, making it valuable for pentesters.

#### **Applications of Netcat**

1. **Connecting to a Server**
    
    - Similar to Telnet, Netcat can connect to a server and retrieve its banner using:
        
        ```bash
        nc [IP_ADDRESS] [PORT]
        ```
        
    - Example: Retrieving a banner from a web server (port 80):
        
        ```bash
        nc 10.10.253.149 80
        GET / HTTP/1.1
        host: netcat
        ```
        
        Response:
        
        ```plaintext
        HTTP/1.1 200 OK
        Server: nginx/1.6.2
        ...
        ```
        
2. **Listening on a Port**
    
    - Netcat can listen on a specific port for incoming connections using:
        
        ```bash
        nc -vnlp [PORT]
        ```
        
    - Options explained:
        ![[Pasted image 20250114114236.png]]
3. **Echo Mode**
    
    - After establishing a connection, Netcat allows bidirectional communication.
    - Example:
        - Server-side:
            
            ```bash
            nc -vnlp 1234
            ```
            
        - Client-side:
            
            ```bash
            nc 10.10.253.149 1234
            ```
            
        - Whatever is typed on one side will echo on the other.

---

#### **Q&A Session**

1. **What is the version of the running server (on port 21 of the VM)?**
    - To find the version:
        
        1. Start the VM and open the AttackBox.
        2. Use Netcat to connect to the VM's port 21:
            
            ```bash
            nc [VM_IP] 21
            ```
            
        3. Review the banner information returned by the server.
    - **Answer:** The banner retrieved from the FTP server on port 21 should include the server version. If you share the output, I can help confirm the answer.

### **Putting It All Together: A Primitive Network and System Scanner**


#### Tools Overview and Use Cases

1. **Ping**  
    Used to test connectivity and determine if a target is responsive.
    
    - **Linux/macOS:**
        
        ```bash
        ping -c 10 10.10.182.117
        ```
        
    - **Windows:**
        
        ```bash
        ping -n 10 10.10.182.117
        ```
        
2. **Tracero
3. ute/Tracert**  
    Maps the path to the target, showing the network hops between your system and the destination.
    
    - **Linux/macOS:**
        
        ```bash
        traceroute 10.10.182.117
        ```
        
    - **Windows:**
        
        ```bash
        tracert 10.10.182.117
        ```
        
3. **Telnet**  
    Checks for open and reachable ports by attempting to connect to them.
    
    ```bash
    telnet 10.10.182.117 PORT_NUMBER
    ```
    
4. **Netcat**  
    Used as both a client and server for testing ports and connections.
    
    - **As a Client:**
        
        ```bash
        nc 10.10.182.117 PORT_NUMBER
        ```
        
    - **As a Server:**
        
        ```bash
        nc -lvnp PORT_NUMBER
        ```
        

---

### Combining These Tools

These commands can be combined into a simple shell script to perform basic reconnaissance:

```bash
#!/bin/bash

TARGET=$1

echo "Pinging the target..."
ping -c 4 $TARGET

echo "Tracing the route to the target..."
traceroute $TARGET

echo "Checking common open ports with Telnet..."
for PORT in 22 80 443 3389; do
    echo "Testing port $PORT..."
    telnet $TARGET $PORT
done

echo "Using Netcat to test ports..."
for PORT in 21 23 25; do
    echo "Testing port $PORT..."
    echo "Test message" | nc -v $TARGET $PORT
done
```

- Save this script as `scanner.sh` and run it with:
    
    ```bash
    ./scanner.sh 10.10.182.117
    ```
    

---

### Using Developer Tools for Reconnaissance

Modern web browsers can also play a role in reconnaissance. They come with built-in **Developer Tools**, which can be accessed via the following shortcuts:

- **Linux/Windows:** `Ctrl + Shift + I`
- **macOS:** `Option + Command + I`

These tools allow you to inspect websites, analyze network requests, and understand a target's web structure without alerting the system.

---

### Next Steps

While the tools covered here form the foundation of network scanning, more advanced and sophisticated scanning can be achieved with tools like **nmap**. In subsequent rooms, you'll explore how to use nmap for deeper network and port scanning tasks.