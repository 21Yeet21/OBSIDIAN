# FFUF Web Fuzzing (TryHackMe)

A guide to using FFUF for web enumeration, covering file and directory discovery, parameter fuzzing, brute-forcing, and proxying.

## Minimum Required Options

- `-u`: Specifies the target **URL**.
- `-w`: Defines the path to the **wordlist**.
- `FUZZ`: Default keyword indicating where wordlist entries are injected in the URL.

> [!note]  
> Wordlist paths (e.g., SecLists) may vary depending on your setup.

## File and Directory Fuzzing

### Q1 — Generic File Fuzzing

Use a generic file wordlist for initial enumeration:

```bash
ffuf -u http://10.10.42.130/FUZZ -w /usr/share/seclists/Discovery/Web-Content/raft-medium-files-lowercase.txt
```

**Downside**: Large wordlists may include irrelevant file types, reducing efficiency.

### Q2 — Detecting File Extensions via Index Trick

Identify backend technology by fuzzing for `index.<extension>`:

```bash
ffuf -u http://10.10.42.130/indexFUZZ -w /usr/share/seclists/Discovery/Web-Content/web-extensions.txt
```

**Sample Extensions** (from `web-extensions.txt`):

```
.asp, .aspx, .cgi, .php, .txt, .js, .jsp, .html, .dll
```

### Q3 — Smart Wordlist + Known Extensions

After identifying valid extensions, fuzz file names with appended extensions (e.g., `.php`, `.txt`):

```bash
ffuf -u http://10.10.42.130/FUZZ -w /usr/share/seclists/Discovery/Web-Content/raft-medium-words-lowercase.txt -e .php,.txt
```

**Tip**: Avoid 4-letter extensions to reduce false positives.

### Q4 — Directory Discovery

Fuzz for directory names (no extensions):

```bash
ffuf -u http://10.10.42.130/FUZZ -w /usr/share/seclists/Discovery/Web-Content/raft-medium-directories-lowercase.txt
```

**Advantage**: Directory enumeration is a good starting point, independent of backend technology.

## Filters and Matchers

### Q5 — Filter Out 403 Status Codes

Hide HTTP 403 (Forbidden) responses, which are often unhelpful:

```bash
ffuf -u http://10.10.42.130/FUZZ -w /usr/share/seclists/Discovery/Web-Content/raft-medium-files-lowercase.txt -fc 403
```

### Q6 — Show Only 200 OK Responses

Focus on successful responses:

```bash
ffuf -u http://10.10.42.130/FUZZ -w /usr/share/seclists/Discovery/Web-Content/raft-medium-files-lowercase.txt -mc 200
```

**Benefit**: More efficient than filtering multiple unwanted codes (e.g., 403, 500).

### Q7 — Filtering by File Size

Exclude responses with zero size (often false positives, e.g., `config.inc.php [Status: 200, Size: 0]`):

```bash
ffuf -u http://10.10.42.130/config/FUZZ -w /usr/share/seclists/Discovery/Web-Content/raft-medium-files-lowercase.txt -fs 0
```

### Dotfiles and False Positives

Dotfiles (e.g., `.htaccess`, `.env`) often return 403 but may exist. Use regex to match them:

```bash
ffuf -u http://10.10.42.130/FUZZ -w /usr/share/seclists/Discovery/Web-Content/raft-medium-files-lowercase.txt -fr '/\..*'
```

**Warning**: Avoid blanket `-fc 403` to prevent missing real files.

### Other Matchers and Filters

- **Matchers** (`-m*`):
    - `-mc`: HTTP status codes.
    - `-ml`: Number of lines.
    - `-mr`: Regex match.
    - `-ms`: Response size.
    - `-mw`: Number of words.
- **Filters** (`-f*`):
    - `-fc`: Filter HTTP status codes.
    - `-fl`: Filter by number of lines.
    - `-fr`: Filter using regex.
    - `-fs`: Filter by response size.
    - `-fw`: Filter by number of words.

## Parameter Fuzzing and Brute-Forcing

### Q8 — Fuzzing for GET Parameters

Discover valid parameter names for a URL (e.g., `http://10.10.25.120/sqli-labs/Less-1/`):

```bash
ffuf -u 'http://10.10.25.120/sqli-labs/Less-1/?FUZZ=1' -c -w /usr/share/seclists/Discovery/Web-Content/burp-parameter-names.txt -fw 39
```

**Alternative**: Use a generic wordlist like `raft-medium-words-lowercase.txt`.  
`-fw 39`: Filters responses with 39 words (likely irrelevant).

### Q9 — Fuzzing Integer Parameter Values

Test integer values for a known parameter (e.g., `id`):

```bash
ruby -e '(0..255).each{|i| puts i}' | ffuf -u 'http://10.10.25.120/sqli-labs/Less-1/?id=FUZZ' -c -w - -fw 33
```

**Other Number Generation Options**:

```bash
seq 0 255
for i in {0..255}; do echo $i; done
ruby -e 'puts (0..255).to_a'
```

`-fw 33`: Filters responses with 33 words (common for errors).

### Q10 — Brute-Forcing Passwords (POST)

Brute-force a login password via POST:

```bash
ffuf -u http://10.10.25.120/sqli-labs/Less-11/ -c -w /usr/share/seclists/Passwords/Leaked-Databases/hak5.txt -X POST -d 'uname=Dummy&passwd=FUZZ&submit=Submit' -fs 1435 -H 'Content-Type: application/x-www-form-urlencoded'
```

- `-X POST`: Specifies POST method.
    
- `-d`: Sends POST data with `FUZZ` in the password field.
    
- `-fs 1435`: Filters failed login responses (size 1435).FFUF Web Fuzzing (TryHackMe)
    
    A guide to using FFUF for web enumeration, covering file and directory discovery, parameter fuzzing, brute-forcing, and proxying.
    
    ## Minimum Required Options
    
    - `-u`: Specifies the target **URL**.
    - `-w`: Defines the path to the **wordlist**.
    - `FUZZ`: Default keyword indicating where wordlist entries are injected in the URL.
    
    > [!note]  
    > Wordlist paths (e.g., SecLists) may vary depending on your setup.
    
    ## File and Directory Fuzzing
    
    ### Q1 — Generic File Fuzzing
    
    Use a generic file wordlist for initial enumeration:
    
    ```bash
    ffuf -u http://10.10.42.130/FUZZ -w /usr/share/seclists/Discovery/Web-Content/raft-medium-files-lowercase.txt
    ```
    
    **Downside**: Large wordlists may include irrelevant file types, reducing efficiency.
    
    ### Q2 — Detecting File Extensions via Index Trick
    
    Identify backend technology by fuzzing for `index.<extension>`:
    
    ```bash
    ffuf -u http://10.10.42.130/indexFUZZ -w /usr/share/seclists/Discovery/Web-Content/web-extensions.txt
    ```
    
    **Sample Extensions** (from `web-extensions.txt`):
    
    ```
    .asp, .aspx, .cgi, .php, .txt, .js, .jsp, .html, .dll
    ```
    
    ### Q3 — Smart Wordlist + Known Extensions
    
    After identifying valid extensions, fuzz file names with appended extensions (e.g., `.php`, `.txt`):
    
    ```bash
    ffuf -u http://10.10.42.130/FUZZ -w /usr/share/seclists/Discovery/Web-Content/raft-medium-words-lowercase.txt -e .php,.txt
    ```
    
    **Tip**: Avoid 4-letter extensions to reduce false positives.
    
    ### Q4 — Directory Discovery
    
    Fuzz for directory names (no extensions):
    
    ```bash
    ffuf -u http://10.10.42.130/FUZZ -w /usr/share/seclists/Discovery/Web-Content/raft-medium-directories-lowercase.txt
    ```
    
    **Advantage**: Directory enumeration is a good starting point, independent of backend technology.
    
    ## Filters and Matchers
    
    ### Q5 — Filter Out 403 Status Codes
    
    Hide HTTP 403 (Forbidden) responses, which are often unhelpful:
    
    ```bash
    ffuf -u http://10.10.42.130/FUZZ -w /usr/share/seclists/Discovery/Web-Content/raft-medium-files-lowercase.txt -fc 403
    ```
    
    ### Q6 — Show Only 200 OK Responses
    
    Focus on successful responses:
    
    ```bash
    ffuf -u http://10.10.42.130/FUZZ -w /usr/share/seclists/Discovery/Web-Content/raft-medium-files-lowercase.txt -mc 200
    ```
    
    **Benefit**: More efficient than filtering multiple unwanted codes (e.g., 403, 500).
    
    ### Q7 — Filtering by File Size
    
    Exclude responses with zero size (often false positives, e.g., `config.inc.php [Status: 200, Size: 0]`):
    
    ```bash
    ffuf -u http://10.10.42.130/config/FUZZ -w /usr/share/seclists/Discovery/Web-Content/raft-medium-files-lowercase.txt -fs 0
    ```
    
    ### Dotfiles and False Positives
    
    Dotfiles (e.g., `.htaccess`, `.env`) often return 403 but may exist. Use regex to match them:
    
    ```bash
    ffuf -u http://10.10.42.130/FUZZ -w /usr/share/seclists/Discovery/Web-Content/raft-medium-files-lowercase.txt -fr '/\..*'
    ```
    
    **Warning**: Avoid blanket `-fc 403` to prevent missing real files.
    
    ### Other Matchers and Filters
    
    - **Matchers** (`-m*`):
        - `-mc`: HTTP status codes.
        - `-ml`: Number of lines.
        - `-mr`: Regex match.
        - `-ms`: Response size.
        - `-mw`: Number of words.
    - **Filters** (`-f*`):
        - `-fc`: Filter HTTP status codes.
        - `-fl`: Filter by number of lines.
        - `-fr`: Filter using regex.
        - `-fs`: Filter by response size.
        - `-fw`: Filter by number of words.
    
    ## Parameter Fuzzing and Brute-Forcing
    
    ### Q8 — Fuzzing for GET Parameters
    
    Discover valid parameter names for a URL (e.g., `http://10.10.25.120/sqli-labs/Less-1/`):
    
    ```bash
    ffuf -u 'http://10.10.25.120/sqli-labs/Less-1/?FUZZ=1' -c -w /usr/share/seclists/Discovery/Web-Content/burp-parameter-names.txt -fw 39
    ```
    
    **Alternative**: Use a generic wordlist like `raft-medium-words-lowercase.txt`.  
    `-fw 39`: Filters responses with 39 words (likely irrelevant).
    
    ### Q9 — Fuzzing Integer Parameter Values
    
    Test integer values for a known parameter (e.g., `id`):
    
    ```bash
    ruby -e '(0..255).each{|i| puts i}' | ffuf -u 'http://10.10.25.120/sqli-labs/Less-1/?id=FUZZ' -c -w - -fw 33
    ```
    
    **Other Number Generation Options**:
    
    ```bash
    seq 0 255
    for i in {0..255}; do echo $i; done
    ruby -e 'puts (0..255).to_a'
    ```
    
    `-fw 33`: Filters responses with 33 words (common for errors).
    
    ### Q10 — Brute-Forcing Passwords (POST)
    
    Brute-force a login password via POST:
    
    ```bash
    ffuf -u http://10.10.25.120/sqli-labs/Less-11/ -c -w /usr/share/seclists/Passwords/Leaked-Databases/hak5.txt -X POST -d 'uname=Dummy&passwd=FUZZ&submit=Submit' -fs 1435 -H 'Content-Type: application/x-www-form-urlencoded'
    ```
    
    - `-X POST`: Specifies POST method.
    - `-d`: Sends POST data with `FUZZ` in the password field.
    - `-fs 1435`: Filters failed login responses (size 1435).
    - `-H`: Sets `Content-Type` (required, as FFUF doesn’t set it automatically).
    
    ## Proxying Traffic
    
    ### Q11 — Sending FFUF Traffic Through a Proxy
    
    Proxy traffic for replay in Burp Suite, network pivoting, or debugging.
    
    #### Full Proxy Mode
    
    Send all traffic through a proxy (HTTP or SOCKS5):
    
    ```bash
    ffuf -u http://10.10.25.120/FUZZ -c -w /usr/share/seclists/Discovery/Web-Content/common.txt -x http://127.0.0.1:8080
    ```
    
    #### Replay Proxy Mode
    
    Send only matching responses to the proxy to reduce noise:
    
    ```bash
    ffuf -u http://10.10.25.120/FUZZ -c -w /usr/share/seclists/Discovery/Web-Content/common.txt -replay-proxy http://127.0.0.1:8080
    ```
    
    **Benefits**:
    
    - Avoids overloading the proxy.
    - Reduces Burp history clutter.
    - Saves bandwidth and compute resources.
    
    ## Custom Keyword Usage
    
    Replace `FUZZ` with a custom keyword (e.g., `NORAJ`):
    
    ```bash
    ffuf -u http://10.10.42.130/NORAJ -w /usr/share/wordlists/SecLists/Discovery/Web-Content/big.txt:NORAJ
    ```
    
    Format: `wordlist.txt:KEYWORD`.
    
    ## Notes
    
    - **Wordlists**: Use SecLists (e.g., `raft-medium-files-lowercase.txt`, `web-extensions.txt`) for reliable results.
    - **Efficiency**: Combine filters (`-fc`, `-fs`) and matchers (`-mc`) to focus on relevant responses.
    - **Proxying**: Use `-replay-proxy` for Burp Suite integration to minimize noise.
    
    #FFUF #TryHackMe #WebFuzzing
    
- `-H`: Sets `Content-Type` (required, as FFUF doesn’t set it automatically).
    

## Proxying Traffic

### Q11 — Sending FFUF Traffic Through a Proxy

Proxy traffic for replay in Burp Suite, network pivoting, or debugging.

#### Full Proxy Mode

Send all traffic through a proxy (HTTP or SOCKS5):

```bash
ffuf -u http://10.10.25.120/FUZZ -c -w /usr/share/seclists/Discovery/Web-Content/common.txt -x http://127.0.0.1:8080
```

#### Replay Proxy Mode

Send only matching responses to the proxy to reduce noise:

```bash
ffuf -u http://10.10.25.120/FUZZ -c -w /usr/share/seclists/Discovery/Web-Content/common.txt -replay-proxy http://127.0.0.1:8080
```

**Benefits**:

- Avoids overloading the proxy.
- Reduces Burp history clutter.
- Saves bandwidth and compute resources.

## Custom Keyword Usage

Replace `FUZZ` with a custom keyword (e.g., `NORAJ`):

```bash
ffuf -u http://10.10.42.130/NORAJ -w /usr/share/wordlists/SecLists/Discovery/Web-Content/big.txt:NORAJ
```

Format: `wordlist.txt:KEYWORD`.

## Notes

- **Wordlists**: Use SecLists (e.g., `raft-medium-files-lowercase.txt`, `web-extensions.txt`) for reliable results.
- **Efficiency**: Combine filters (`-fc`, `-fs`) and matchers (`-mc`) to focus on relevant responses.
- **Proxying**: Use `-replay-proxy` for Burp Suite integration to minimize noise.

#FFUF #TryHackMe #WebFuzzing