# Burp Suite Repeater: Overview

Burp Suite Repeater is a tool for manually manipulating and resending HTTP requests, ideal for web application testing.

## What is Repeater?

Repeater allows you to:
- **Modify and resend** intercepted requests from Burp Proxy.
- **Craft requests manually**, like using cURL.
- **Test endpoints** by editing and resending requests repeatedly.

Its graphical interface simplifies payload editing and provides multiple response views, including a visual rendering engine.

## Repeater Interface

The interface has six key sections:
![[Pasted image 20250802001032.png]]
1. **Request List**  
   - Top left; shows all active Repeater requests.
   - New requests from other Burp tools appear here.

2. **Request Controls**  
   - Below Request List; buttons to send, cancel, or navigate request history.

3. **Request and Response View**  
   - Main area; edit requests in Request View, see responses in Response View.

4. **Layout Options**  
   - Top-right of Request/Response view; choose horizontal (default), vertical, or tabbed layout.

5. **Inspector**  
   - Right-hand side; intuitive request analysis and modification (details in later tasks).

6. **Target**  
   - Above Inspector; sets target IP/domain, auto-filled from other Burp tools.

## Why Use Repeater?

- **Manual testing**: Tweak requests to explore endpoints.
- **Debugging**: Analyze server responses to specific payloads.
- **Flexibility**: Combine intercepted and manual requests.


Once a request has been captured in the Proxy module, we can send it to Repeater by either right-clicking on the request and selecting Send to Repeater, or by utilizing the keyboard shortcut
==Ctrl + R.==
## Response View Options in Repeater

Burp Suite Repeater offers multiple ways to view and analyze server responses, ranging from formatted text to rendered pages. These options are accessible via four buttons above the Response View.

### View Options

- **Pretty**  
  - Default view; applies light formatting to the raw response for improved readability.

- **Raw**  
  - Displays the unformatted response as received from the server.

- **Hex**  
  - Shows a byte-level representation of the response, ideal for analyzing binary files.

- **Render**  
  - Visualizes the response as it would appear in a web browser.  
  - Less common in Repeater (focus is typically on source code) but useful for visual checks.

> [!tip]  
> The **Pretty** view is sufficient for most tasks, but familiarize yourself with **Raw**, **Hex**, and **Render** for specific use cases.

### Show Non-Printable Characters

- Located to the right of the view buttons, the **Show non-printable characters** button (`\n`) reveals hidden characters (e.g., `\r\n` for carriage return and newline in HTTP headers).
- Useful for debugging or analyzing response formatting, though not always necessary.

#BurpSuite #Repeater #WebTesting

## Modifying Requests in Repeater

Repeater’s **Inspector** allows modification of request components, such as attributes, parameters, cookies, and headers, in a user-friendly tabular format. These changes are reflected in the raw Request View.

### Editable Request Components

- **Request Attributes**  
  - Modify the **location** (target resource), **HTTP method** (e.g., GET to POST), or **protocol** (e.g., HTTP/1 to HTTP/2).  
  - Example: Switch protocol from HTTP/1 to HTTP/2.

- **Request Query Parameters**  
  - Data sent via URL in GET requests (e.g., `https://admin.tryhackme.com/?redirect=false`, where `redirect=false`).  
  - Editable for testing server behavior.

- **Request Body Parameters**  
  - Data sent in POST requests.  
  - Modifiable to adjust parameters before resending.

- **Request Cookies**  
  - View and edit cookies sent with the request.

- **Request Headers**  
  - Add, edit, or remove headers to test server responses to unexpected or modified headers.

- **Response Headers**  
  - Displays headers returned by the server.  
  - View-only, as these cannot be modified.  
  - Visible only after receiving a server response.

> [!tip]  
> Use the **Inspector**’s tabular view to easily modify request components and observe changes in the raw Request View. Experiment with adding or editing headers to understand server behavior.

#BurpSuite #Repeater #WebTesting