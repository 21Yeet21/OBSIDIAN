

# HTTP in Detail

## What is HTTP(S)?

### What is HTTP? (HyperText Transfer Protocol)

HTTP, developed between 1989-1991 by Tim Berners-Lee, is used to view websites. It defines rules for communicating with web servers to transmit data like HTML, images, and videos.

### What is HTTPS? (HyperText Transfer Protocol Secure)

HTTPS is the secure version of HTTP. It encrypts data to ensure privacy and confirms communication with the correct server, preventing impersonation.

## Understanding URLs

When you access a website, your browser makes requests to a web server for assets like HTML and images. To locate these resources, you use URLs.

### What is a URL? (Uniform Resource Locator)

A URL provides instructions for accessing a resource on the internet. Below is an example with its components:

![[Pasted image 20250111192852.png]]

- **Scheme**: Specifies the protocol (e.g., HTTP, HTTPS, FTP).
- **User**: Includes login credentials (username and password).
- **Host**: The domain name or IP address of the server.
- **Port**: Connection port (e.g., 80 for HTTP, 443 for HTTPS).
- **Path**: Location of the requested resource.
- **Query String**: Additional data sent to the path (e.g., `/blog?id=1` specifies blog ID 1).
- **Fragment**: A reference to a specific section on the page (e.g., `#task3`).

## Making a Request

A simple request to a web server looks like this:

![[Pasted image 20250111195300.png]]


For a richer web experience, additional data is sent via headers. Headers provide extra information to the web server.

### Example Request

```
GET / HTTP/1.1
Host: tryhackme.com
User-Agent: Mozilla/5.0 Firefox/87.0
Referer: https://tryhackme.com/
```

- **Line 1**: Requests the home page (`/`) using HTTP 1.1.
- **Line 2**: Specifies the host (`tryhackme.com`).
- **Line 3**: Identifies the client as Firefox version 87.
- **Line 4**: Indicates the referring webpage (`https://tryhackme.com`).
- **Line 5**: Blank line signals the end of the request.

## Example Response

```
HTTP/1.1 200 OK
Server: nginx/1.15.8
Date: Fri, 09 Apr 2021 13:34:03 GMT
Content-Type: text/html
Content-Length: 98

<html>
<head>
    <title>TryHackMe</title>
</head>
<body>
    Welcome To TryHackMe.com
</body>
</html>
```

### Breaking Down the Response

- **Line 1**: Protocol version and status code (`200 OK` indicates success).
- **Line 2**: Server software and version.
- **Line 3**: Server's current date and time.
- **Line 4**: Content type (e.g., HTML, images, videos).
- **Line 5**: Content length, indicating the response size.
- **Line 6**: Blank line marks the response end.
- **Lines 7-14**: The requested content, in this case, the homepage.

## Questions

1. **What HTTP protocol is being used in the above example?**
    
    - HTTP/1.1
2. **What response header tells the browser how much data to expect?**
    
    - Content-Length



# HTTP Methods

HTTP methods define the intended action when making a request. While there are many methods, the most commonly used are GET and POST.

### Common HTTP Methods

- **GET**: Retrieves information from a web server.
    
- **POST**: Submits data to a server, often creating new records.
    
- **PUT**: Submits data to update existing information.
    
- **DELETE**: Deletes information or records on the server.
    

### Example Questions

1. **What method would be used to create a new user account?**
    
    - POST
        
2. **What method would be used to update your email address?**
    
    - PUT
        
3. **What method would be used to remove a picture you've uploaded to your account?**
    
    - DELETE
        
4. **What method would be used to view a news article?**
    
    - GET



# HTTP Status Codes

When an HTTP server responds, the first line always contains a status code indicating the outcome of the client's request and potentially how to handle it. These codes are divided into five ranges:

### Status Code Ranges

- **100-199**: _Information Response_ - Indicates the initial part of a request has been received, and the client should continue. Rarely used.
    
- **200-299**: _Success_ - Indicates the client's request was successful.
    
- **300-399**: _Redirection_ - Redirects the client to another resource, such as a different webpage or website.
    
- **400-499**: _Client Errors_ - Indicates an issue with the client's request.
    
- **500-599**: _Server Errors_ - Indicates a server-side issue, often signifying a significant problem.
    

### Common HTTP Status Codes

- **200 OK**: The request was completed successfully.
    
- **201 Created**: A resource, such as a user or blog post, was successfully created.
    
- **301 Moved Permanently**: The client is redirected to a new webpage or URL permanently.
    
- **302 Found**: A temporary redirect to another resource.
    
- **400 Bad Request**: The request was malformed or missing required information.
    
- **401 Not Authorized**: Access requires authentication, typically via username and password.
    
- **403 Forbidden**: Access is denied, regardless of authentication.
    
- **404 Not Found**: The requested resource does not exist.
    
- **405 Method Not Allowed**: The requested method is not supported by the resource (e.g., GET instead of POST).
    
- **500 Internal Server Error**: The server encountered an error it couldn't handle.
    
- **503 Service Unavailable**: The server is overloaded or undergoing maintenance.
    

### Example Questions

1. **What response code might you receive if you've created a new user or blog post article?**
    
    - 201 Created
        
2. **What response code might you receive if you've tried to access a page that doesn't exist?**
    
    - 404 Not Found
        
3. **What response code might you receive if the web server cannot access its database and the application crashes?**
    
    - 500 Internal Server Error
        
4. **What response code might you receive if you try to edit your profile without logging in first?**
    
    - 401 Not Authorized

# HTTP Headers

Headers are additional bits of data sent during HTTP requests or responses. While headers are not strictly required, they are essential for proper communication between the client and server.

### Common Request Headers

These headers are sent from the client (e.g., browser) to the server:

- **Host**: Specifies the website being requested. Useful when a server hosts multiple websites.
    
- **User-Agent**: Identifies the browser software and version, enabling the server to optimize content for the browser and also some elements of HTML, JavaScript and CSS are only available in certain browsers.
    
- **Content-Length**: Indicates the size of data being sent, ensuring the server knows how much to expect.
    
- **Accept-Encoding**: Lists supported compression methods to reduce data size during transmission.
    
- **Cookie**: Sends stored data to the server for session management (see "Cookies" section).
    

### Common Response Headers

These headers are sent from the server to the client:

- **Set-Cookie**: Sends session information back to the client for storage (see "Cookies" section).
    
- **Cache-Control**: Specifies how long content should be cached before requesting it again.
    
- **Content-Type**: Indicates the type of data being returned (e.g., HTML, CSS, images, videos).
    
- **Content-Encoding**: Specifies the compression method used for the returned data.
    

### Example Questions

1. **What header tells the web server what browser is being used?**
    
    - User-Agent
        
2. **What header tells the browser what type of data is being returned?**
    
    - Content-Type
        
3. **What header tells the web server which website is being requested?**
    
    - Host





# **Cookies in HTTP Requests and Responses**

Cookies are small pieces of data stored on your computer by a web server. They are used to remember certain information about a user, such as authentication details, preferences, or session information.

#### **How Cookies Work**

1. **Set-Cookie Header**: When you access a website, the web server may send a `Set-Cookie` header in the HTTP response, which instructs your browser to store a cookie.
2. **Subsequent Requests**: For every following request to the same web server, your browser sends the cookie data back, allowing the server to recognize your session or preferences.
3. **HTTP Statelesness**: Since HTTP is stateless (it doesn't remember previous requests), cookies help the web server identify the user and maintain a consistent experience.

#### **Common Uses of Cookies**

- **Authentication**: Cookies store tokens for user login sessions, enabling continuous access without needing to log in again.
- **Personalization**: Cookies remember user preferences or settings on the website.
- **Tracking**: Some cookies are used for tracking user behavior across websites.

#### **Viewing Cookies**

To view cookies stored by your browser:

1. Open the **Developer Tools** in your browser (usually accessed with F12 or right-click > Inspect).
2. Navigate to the **Network** tab.
3. View the specific request that sent cookies in the **Cookies** section of the request details.

![[Pasted image 20250111202307.png]]


Which header is used to save cookies to your computer?

Set-Cookie

