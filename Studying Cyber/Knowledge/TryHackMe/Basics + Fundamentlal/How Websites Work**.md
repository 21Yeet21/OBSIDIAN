

## **Website Basics**

When visiting a website, your browser (e.g., Chrome or Safari) makes a **request** to a **web server**. The server responds with data your browser uses to display the webpage.

A **web server** is a dedicated computer handling these requests.

### **Website Components**

1. **Front End (Client-Side)**: The website part your browser displays.
    
2. **Back End (Server-Side)**: The server that processes requests and returns data.
    

In summary:

- **Request** → Sent to the server.
    
- **Response** → Data sent back for rendering.
	- ![[Pasted image 20250112224248.png]]


## **Website Technologies**

Websites are built using:

- **HTML**: Defines structure and content.
    
- **CSS**: Styles and enhances visual appearance.
    
- **JavaScript**: Adds interactivity and dynamic content.
    

### **HTML Structure Overview**

- `<!DOCTYPE html>`: Specifies HTML5 standard.
    
- `<html>`: Root element of the page.
    
- `<head>`: Contains metadata and title.
    
- `<body>`: Contains content displayed on the page.
    
- `<h1>`: Defines headings.
    
- `<p>`: Defines paragraphs.
    

### **HTML Tags and Attributes**

- **Attributes** provide extra information:
    
    - `class`: Used for styling multiple elements.
        
    - `id`: Unique identifier for styling or JavaScript.
        
    - Example: `<img src="img/cat.jpg">` specifies an image location.
        

**Note**: To view HTML source, right-click and select "View Page Source" (Chrome) / "Show Page Source" (Safari).


### **JavaScript (JS) Basics**

JavaScript makes websites interactive, unlike static HTML.

- **Dynamic Updates**: JS can modify elements in real-time, such as changing button styles or displaying animations.
- **Adding JavaScript**:
    - Inline: `<script>...</script>`
    - External: `<script src="path/to/script.js"></script>`

Example:

```javascript
document.getElementById("demo").innerHTML = "Hack the Planet";
```

This code changes the content of the element with the `id` "demo."

- **Event Handling**:
    
    - `onclick` triggers actions on user interaction:
    
    ```html
    <button onclick='document.getElementById("demo").innerHTML = "Button Clicked";'>Click Me!</button>
    ```

### **Sensitive Data Exposure**

Sensitive Data Exposure occurs when a website fails to protect sensitive information in its source code, leaving it visible to users. This could include login credentials, hidden links, or other private data. Attackers can exploit this to gain further access to the web application.

- **Example**: Temporary login credentials in HTML comments may allow unauthorized access.
    
- **Assessment Tip**: Always review a web page’s source code to check for exposed sensitive data.
		![[Pasted image 20250112230507.png]]
		



### **HTML Injection**

HTML Injection occurs when unfiltered user input is used directly on a web page. This allows attackers to inject malicious HTML or JavaScript.

- **Example**: A form outputting user input directly without sanitization lets an attacker insert harmful code.
    
- **Key Prevention Techniques**:
    
    - Sanitize user inputs to remove HTML and JavaScript tags.
        
    - Use output encoding to prevent browsers from interpreting content as code.
        
    - Utilize libraries like DOMPurify for input sanitization.
        
    - Avoid using `innerHTML`; prefer `textContent` or `innerText`.
        

**General Rule**: Never trust user input—validate and sanitize everything.


### HTML injection  in Depth
HTML Injection is a security vulnerability that arises when a web application fails to properly sanitize user input, allowing attackers to inject malicious HTML code into web pages. This can lead to unauthorized content display, website defacement, or even the execution of malicious scripts.

**Understanding HTML Injection**

When user inputs are directly incorporated into web pages without adequate validation or encoding, attackers can insert HTML tags or scripts. For instance, if a comment section on a website doesn't filter inputs correctly, an attacker might submit a comment containing harmful HTML or JavaScript code. When other users view this comment, the injected code executes, potentially compromising their experience or security.

**Real-World Example**

A notable instance of HTML injection involved the "SamSam" ransomware campaign, which targeted various organizations in the United States in 2018. Attackers exploited vulnerabilities to inject malicious HTML content, facilitating the spread of ransomware. citeturn0search15

**Preventing HTML Injection**

To safeguard against HTML injection attacks, consider the following best practices:

- **Input Validation**: Ensure that all user inputs are validated against a strict set of rules, accepting only expected data formats. Reject any input that doesn't conform to these rules.
    
- **Output Encoding**: Encode user inputs before displaying them on web pages. This process converts special characters into a safe format, preventing browsers from interpreting them as executable code.
    
- **Use Safe Methods**: When updating the DOM, utilize methods that don't interpret content as HTML. For example, in JavaScript, prefer `textContent` or `innerText` over `innerHTML` to prevent the execution of injected code. citeturn0search4
    
- **Employ Security Libraries**: Implement reputable security libraries designed to sanitize inputs and outputs, effectively neutralizing potential threats. For instance, libraries like DOMPurify can help mitigate risks associated with HTML injection. citeturn0search18
    
- **Content Security Policy (CSP)**: Configure a robust CSP to control the sources from which content can be loaded. This reduces the risk of executing malicious scripts by restricting the domains from which resources can be fetched. citeturn0search18
    

**Conclusion**

HTML injection poses significant risks to web applications, potentially leading to unauthorized content manipulation and security breaches. By implementing stringent input validation, proper output encoding, and adhering to security best practices, developers can effectively mitigate the threat of HTML injection attacks.