

---

## **Linux Modules: Let's Introduce**  

### **Purpose**  
- Familiarize yourself with Linux commands.  
- No rush—focus on learning.  

---

### **Key Commands**  
- `du`, `grep`, `tr`, `awk`, `sed`, `xargs`, `curl`, `wget`, `xxd`, and more.  

---

### **Why Learn?**  
- Boost efficiency in terminal workflows.  
- Essential for pentesting and Linux projects.  

---
Here’s a more detailed summary for **Task 2: du**, including an example in the notes section:

---

## **Task 2: du (Disk Usage)**  

### **What is `du`?**  
- **Purpose**: The `du` command (short for **disk usage**) helps identify how much space files and directories are consuming on your disk.  
- **Default Behavior**: Shows sizes in **kilobytes (KB)** and lists **folders only** (not individual files).  

---

### **Key Flags**  
| Flag       | Description                                                                 |  
|------------|-----------------------------------------------------------------------------|  
| `-a`       | Lists **both files and folders** (not just folders).                        |  
| `-h`       | Displays sizes in **human-readable format** (e.g., KB, MB, GB).             |  
| `-c`       | Adds a **total size** at the end of the output.                             |  
| `-d <num>` | Limits the **depth** of directory listing (e.g., `-d 2` for 2 levels deep). |  
| `--time`   | Includes the **last modified timestamp** for each file/folder.              |  

---

### **Examples**  
1. **List all files and folders in `/home/`**:  
   ```bash  
   du -a /home/  
   ```  
   - This will show every file and folder in `/home/` with their sizes in KB.  

2. **Filter output with `grep`**:  
   ```bash  
   du -a /home/ | grep user  
   ```  
   - This will list only files/folders containing the word `user` in their names.  

3. **Alternate `ls` with `du`**:  
   ```bash  
   du --time -d 1 .  
   ```  
   - This lists the current directory's contents with **timestamps** and limits the depth to **1 level**.  

---

### **Final Notes**  
- **Ownership Info**: `du` does not show file ownership. Use the `stat` command for that:  
  ```bash  
  stat <filename>  
  ```  
  Example:  
  ```bash  
  stat /home/user/file.txt  
  ```  
  - This will display details like ownership, permissions, and timestamps.  

---

## Task 3: Grep, Egrep, Fgrep

### Introduction

Grep is a powerful command-line utility in Linux used for searching text using patterns. It filters lines from files that match a specified pattern, making it an essential tool for text processing and searching.

### The Family Tree

Grep has variants like `egrep` and `fgrep`, which offer different functionalities:
- **egrep**: Uses extended regular expressions (EREs) for more complex pattern matching.
- **fgrep**: Searches for fixed strings without interpreting them as regular expressions.
- **grep**: Can mimic `egrep` and `fgrep` using the `-E` and `-F` flags, respectively.

### Important Flags

| Flag | Description                                                           |
| ---- | --------------------------------------------------------------------- |
| `-R` | Recursively searches directories.                                     |
| `-h` | Suppresses filename prefixes in recursive searches.                   |
| `-c` | Counts matches instead of displaying them.                            |
| `-i` | I==gnores case== distinctions. (Ll , Kk , Aa) no prob                 |
| `-l` | Lists filenames with matches.                                         |
| `-n` | Displays line numbers with matches.                                   |
| `-v` | Inverts the match, showing lines that do ==not== contain the pattern. |
| `-E` | Uses extended regular expressions.                                    |
| `-e` | Specifies multiple patterns.                                          |

### Q&A Section

1. **Is there a difference between egrep and fgrep?**  
   **Answer**: Yes. Egrep uses extended regular expressions, while fgrep searches for fixed strings.

2. **Which flag do you use to list out all the lines NOT containing the 'PATTERN'?**  
   **Answer**: The `-v` flag inverts the match, showing lines that do not contain the pattern.

3. **What is the difference between `-E` and `-e` in grep?**  
   **Answer**: The `-E` flag treats the pattern as an extended regular expression, while the `-e` flag allows specifying multiple patterns in a single grep command.

4. **How do you perform a case-sensitive search using grep?**  
   **Answer**: By default, grep is case-sensitive. To perform a case-insensitive search, use the `-i` flag.

5. **What does the `-n` flag do in grep?**  
   **Answer**: The `-n` flag displays the line numbers of the matching lines in the file.

here using -i had helped allot :
![[Pasted image 20250118144400.png]]



## Task 4: String Manipulations (STROPS)

### Tools for String Manipulations

In Linux, several powerful command-line tools are available for string manipulations. These tools are essential for efficiently processing and transforming text data. The following are some of the most commonly used tools:

- **`tr`**: Translates or deletes characters.
- **`awk`**: A powerful text processing tool.
- **`sed`**: Stream editor for filtering and transforming text.
- **`xargs`**: Builds and executes commands from standard input.

Additionally, the following commands are useful for text manipulation:

- **`sort`**: Sorts lines of text.
- **`uniq`**: Filters out duplicate lines.

### `tr`: Translate or Delete Characters

The `tr` command is used to translate or delete characters in a string.

| Flag | Description |
|------|-------------|
| `-d` | Deletes specified characters. |
| `-s` | Squeezes repeats of the specified characters into a single character. |

**Example**:
```bash
echo "Hello World" | tr 'H' 'h'
```
Output: `hello World`

### `awk`: Text Processing

`awk` is a scripting language designed for text processing.

| Flag | Description |
|------|-------------|
| `-F` | Specifies the field separator. |

**Example**:
```bash
echo "apple,banana,cherry" | awk -F ',' '{print $2}'
```
Output: `banana`

### `sed`: Stream Editor

`sed` is a stream editor for filtering and transforming text.

| Flag | Description |
|------|-------------|
| `-e` | Edits scripts. |
| `-n` | Suppresses automatic printing of pattern space. |

**Example**:
```bash
echo "Hello World" | sed 's/World/universe/'
```
Output: `Hello universe`

### `xargs`: Build and Execute Commands

`xargs` builds and executes commands from standard input.

| Flag | Description |
|------|-------------|
| `-I {}` | Specifies a placeholder for input lines. |
| `-r` | Avoids running the command if there is no input. |

**Example**:
```bash
echo "file1 file2" | xargs -I {} cp {} backup/
```
Copies `file1` and `file2` to the `backup/` directory.

### Additional Commands

- **`sort`**: Sorts lines of text.
  ```bash
  sort file.txt
  ```
- **`uniq`**: Filters out duplicate lines.
  ```bash
  uniq file.txt
  ```

These tools are fundamental for efficient string manipulations in Linux, allowing users to perform complex text processing tasks with concise commands.


## Task 5: tr

### Introduction to tr Command

The `tr` command is a powerful utility in Unix/Linux for translating or deleting characters in a string. It is particularly useful for tasks such as changing character cases, replacing characters, and deleting specific characters from input.

### Syntax of tr Command

The general syntax of the `tr` command is:

```bash
tr [OPTIONS] SET1 [SET2]
```

Where:
- `SET1` is the set of characters to be replaced or deleted.
- `SET2` is the set of characters to replace `SET1`.

### Flags Available with tr

| Flag    | Description                                                                 |
|---------|-----------------------------------------------------------------------------|
| `-d`    | Deletes characters in `SET1` from the input.                                |
| `-t`    | Truncates `SET2` to the length of `SET1` when replacing characters.        |
| `-s`    | Squeezes multiple occurrences of characters in `SET1` to a single character.|
| `-c`    | Complements `SET1`, affecting all characters not in `SET1`.                |

### Examples of Using tr

1. **Convert every alphabetic character to uppercase:**
   ```bash
   cat file.txt | tr '[:lower:]' '[:upper:]'
   ```

2. **Delete all lowercase letters and specific symbols:**
   ```bash
   cat file.txt | tr -d '[:lower:]: '
   ```

### Q&A Section

1. **How to select any digit character in a string using `tr`?**
   - Use the sequence `[:digit:]`.
   - Example: `tr -d '[:digit:]'` will delete all digits from the input string.

2. **What sequence is equivalent to `[a-zA-Z]` set?**
   - Use the sequence `[:alpha:]`.
   - Example: `tr '[:alpha:]' 'X'` replaces all alphabetic characters with 'X'.

3. **What sequence is equivalent to selecting hexadecimal characters?**
   - Use the sequence `[:xdigit:]`.
   - Example: `tr '[:xdigit:]' 'Y'` replaces all hexadecimal characters (0-9, A-F, a-f) with 'Y'.

## Task 6: The AWK Command

AWK is a powerful scripting language used for data manipulation and report generation. It is highly versatile and can handle a wide range of tasks, from simple text processing to complex data analysis.

### Syntax and Usage

The basic syntax of AWK is:

```bash
awk [flags] 'pattern {action}' input_file
```

- **Flags**: Various flags can be used to modify the behavior of AWK (see table below).
- **Pattern**: Specifies the condition that lines must meet to be processed.
- **Action**: The operations to perform on lines that match the pattern.

AWK also supports input from pipes:

```bash
command | awk 'pattern {action}'
```

For scripts, use the `-f` flag:

```bash
awk -f script.awk input.txt
```

### Built-In Variables

AWK has several built-in variables that are useful for data manipulation:

- **Field Variables**: `$1, $2, ..., $n` represent fields in a line, separated by the field separator (default is space).
- **$0**: Represents the entire line.
- **NR**: Keeps track of the number of records (lines) processed.
- **FS**: Field Separator, default is space, can be changed using `BEGIN`.
- **OFS**: Output Field Separator, default is space.
- **RS**: Record Separator, default is newline.
- **ORS**: Output Record Separator, default is newline.

Example:

```bash
awk '{print $1, $3}' file.txt
```

This prints the first and third fields of each line in `file.txt`.

### Important Flags

| Flag | Description |
|------|-------------|
| `-F` | Specifies the field separator (FS). |
| `-v` | Sets a variable (e.g., `-v var=value`). |
| `-D` | Debug mode for `.awk` scripts. |
| `-o` | Specifies the output file (default is `awkprof.out`). |

### Q&A Section

1. **What is the difference between FS and OFS in AWK?**
   - **FS** is the input field separator, while **OFS** is the output field separator.

2. **How do you print the total number of lines in a file using AWK?**
   - Use the `NR` variable:
     ```bash
     awk 'END {print NR}' file.txt
     ```

3. **What is the purpose of the `BEGIN` and `END` blocks in AWK?**
   - `BEGIN` is executed before processing any input, useful for initializing variables.
   - `END` is executed after all input has been processed, useful for final operations.

4. **How can you change the field separator in AWK without using the `-F` flag?**
   - Use the `FS` variable in the `BEGIN` block:
     ```bash
     awk 'BEGIN {FS=","} {print $1}' file.txt
     ```

5. **What is the difference between `print` and `printf` in AWK?**
   - `print` outputs with default formatting.
   - `printf` allows for formatted output similar to C's `printf`.



## Task 7: The `sed` Command

`sed` (Stream EDitor) is a powerful tool for performing text transformations on an input stream (a file or input from a pipeline). It is widely used for tasks like **find and replace**, **insertion**, **deletion**, and **text manipulation**. Its simplicity and efficiency make it a favorite for quick text processing.

---

### **Syntax and Usage**

The basic syntax of `sed` is:

```bash
sed [flags] 'pattern/script' [input_file]
```

- **Flags**: Modify the behavior of `sed` (see table below).
- **Pattern/Script**: Specifies the operations to perform on the input.
- **Input File**: The file to process. If omitted, `sed` reads from standard input.

---

### **Important Flags**

| Flag | Description |
|------|-------------|
| `-e` | Adds a script/command to execute. |
| `-f` | Specifies a file containing `sed` scripts. |
| `-E` | Enables extended regular expressions. |
| `-n` | Suppresses automatic printing of pattern space. |

---

### **Modes/Commands**

| Command | Description |
|---------|-------------|
| `s`     | **Substitute mode**: Find and replace text. |
| `y`     | **Transliterate mode**: Replace individual characters. |
| `d`     | **Delete mode**: Delete lines matching a pattern. |
| `p`     | **Print mode**: Print lines matching a pattern. |

---

### **Common Examples**

#### 1. **Find and Replace**
Replace all occurrences of `john` with `JOHN` in a file:

```bash
sed 's/john/JOHN/g' file.txt
```

- `s`: Substitute mode.
- `/john/`: Pattern to find.
- `/JOHN/`: Replacement text.
- `g`: Global replacement (all occurrences in a line).

#### 2. **Delete Lines**
Delete lines containing the word `youtube`:

```bash
sed '/youtube/d' file.txt
```

- `/youtube/`: Pattern to match.
- `d`: Delete mode.

#### 3. **Print Specific Lines**
Print lines 1 to 3:

```bash
sed -n '1,3p' file.txt
```

- `-n`: Suppress automatic printing.
- `1,3p`: Print lines 1 to 3.

#### 4. **Case-Insensitive Replacement**
Replace `youtube` with `YouTube` (case-insensitive):

```bash
sed 's/youtube/YouTube/i' file.txt
```

- `i`: Case-insensitive flag.

#### 5. **Add a Bullet Point to Each Line**
Add a bullet point (`=>`) to the start of each line:

```bash
sed 's/^/=> /' file.txt
```

- `^`: Matches the start of a line.
- `=> `: Replacement text.

---

### **Advanced Example: Enclose Digits in Square Brackets**

Use `sed` with regex to enclose digits in square brackets:

```bash
sed 's/\([[:digit:]]\+\)/[\1]/g' file.txt
```

- `\([[:digit:]]\+\)`: Matches one or more digits and captures them as a group.
- `[\1]`: Replaces the matched digits with the same digits enclosed in square brackets.

---

### **Q&A Section**

1. **What is the difference between `s` and `y` commands in `sed`?**
   - `s`: Substitutes a pattern with another string.
   - `y`: Transliterates individual characters (e.g., `y/abc/ABC/` replaces `a` with `A`, `b` with `B`, etc.).

2. **How do you delete empty lines in a file using `sed`?**
   ```bash
   sed '/^$/d' file.txt
   ```
   - `^$`: Matches empty lines.
   - `d`: Deletes the matched lines.

3. **How do you replace only the second occurrence of a pattern in a line?**
   ```bash
   sed 's/pattern/replacement/2' file.txt
   ```
   - `2`: Replaces only the second occurrence.

4. **How do you insert a line after a specific pattern?**
   ```bash
   sed '/pattern/a\New Line' file.txt
   ```
   - `/pattern/`: Matches the pattern.
   - `a\New Line`: Inserts "New Line" after the matched pattern.

5. **How do you use `sed` to edit a file in place?**
   ```bash
   sed -i 's/old/new/g' file.txt
   ```
   - `-i`: Edits the file in place.

---

### **Resources**

1. [Sed Command in Linux/Unix with Examples - GeeksforGeeks](https://www.geeksforgeeks.org/sed-command-in-linux-unix-with-examples/)
2. [GNU `sed` Documentation](https://www.gnu.org/software/sed/manual/sed.html)
3. [15 Useful `sed` Command Tips and Tricks - Tecmint](https://www.tecmint.com/sed-command-tips-tricks/)

---

By mastering `sed`, you can efficiently manipulate text files and automate repetitive tasks. Practice with the examples provided and explore the resources to deepen your understanding!




## Task 8: Understanding xargs

### Important Flags of xargs

xargs is a powerful command-line utility that processes input from standard input and passes it as arguments to another command. Below are some key flags used with xargs:

| Flag      | Description                                                                 |
|-----------|-----------------------------------------------------------------------------|
| `-0`      | Terminates input items with a null character, useful for handling spaces in filenames. |
| `-a file` | Reads items from a specified file instead of standard input.                 |
| `-d delimiter` | Specifies a custom delimiter for input items.                             |
| `-n number` | Limits the number of arguments passed to the command at once.               |
| `-t`      | Prints the command to be executed before running it.                         |
| `-I replacement` | Replaces occurrences of `replacement` in the command with input items. |

### Practical Examples of xargs

xargs is often used in conjunction with commands like `find` and `grep` to handle files and search for patterns efficiently.

- **Example 1**: Deleting all `.log` files in a directory:
  ```bash
  find . -name "*.log" -print0 | xargs -0 rm
  ```
- **Example 2**: Searching for a pattern in multiple files:
  ```bash
  find . -name "*.txt" | xargs grep "pattern"
  ```

### Advanced Usage: Privilege Escalation with xargs and tar

In certain scenarios, xargs can be used for privilege escalation by creating files that are interpreted as command-line flags by other utilities like `tar`.

- **Example**: Creating files that mimic `tar` flags:
  ```bash
  echo -e "--checkpoint=1\n--checkpoint-action=exec=/bin/sh" | xargs -n1 touch --
  ```
  This creates files that, when processed by `tar`, can execute a shell with elevated privileges.

### Q&A

1. **What is the purpose of the `-0` flag in xargs?**
   - The `-0` flag tells xargs to expect input items terminated by a null character, which is useful for handling filenames with spaces or special characters.

2. **How can xargs be used with the `find` command?**
   - xargs can take output from `find` and pass it as arguments to another command, such as `rm` or `grep`, often using the `-print0` and `-0` flags to handle special characters.

3. **What does the `-I` flag in xargs do?**
   - The `-I` flag allows you to specify a replacement string that xargs will substitute with each input item in the command.

4. **Why is xargs useful in privilege escalation scenarios?**
   - xargs can create files that are interpreted as command-line flags by other utilities, potentially leading to unintended privilege escalation.

5. **How do you prevent xargs from executing a command if no input is provided?**
   - Use the `-r` flag, which tells xargs not to run the command if there is no input.

## Task 9: sort and uniq

### Understanding `sort`

The `sort` command is used to sort lines of text in a specific order, which can be alphabetical or numerical. It can handle different collations based on language settings.

- **Key Points:**
  - Arranges lines in a specified order.
  - Can handle numerical and alphabetical sorting.
  - Uses language settings for correct sorting of characters.

- **Example:**
  ```bash
  sort input.txt
  ```

### Understanding `uniq`

The `uniq` command filters out consecutive duplicate lines from a sorted list. It can also count occurrences or show only unique lines based on flags.

- **Key Points:**
  - Removes consecutive duplicates by default.
  - Works effectively when combined with `sort`.
  - Can show counts or only unique lines.

- **Example:**
  ```bash
  sort input.txt | uniq
  ```

### Combining `sort` and `uniq`

To remove duplicates from an unsorted file, it's common to use `sort` followed by `uniq`.

- **Key Points:**
  - `sort` arranges lines, making duplicates adjacent.
  - `uniq` then filters out duplicates.

- **Example:**
  ```bash
  sort input.txt | uniq > output.txt
  ```

### Important Flags

#### Flags for `sort`

| Flag | Description |
|------|-------------|
| `-r` | Sort in reverse order. |
| `-c` | Check if the file is already sorted. |
| `-u` | Sort and remove duplicates. |
| `-n` | Sort numerically. |

#### Flags for `uniq`

| Flag | Description |
|------|-------------|
| `-c` | Count occurrences of each line. |
| `-d` | Show only duplicate lines. |
| `-u` | Show only unique lines. |
| `-i` | Ignore case differences. |

### Practical Examples

- **Counting Occurrences:**
  ```bash
  sort input.txt | uniq -c
  ```

- **Finding Position of a Word:**
  ```bash
  sort input.txt | uniq | grep -n "word"
  ```

can use ==cat -n== 
### Q&A

1. **What does the `uniq` command do?**
   - `uniq` removes consecutive duplicate lines from a sorted list.

2. **Why is it important to sort a file before using `uniq`?**
   - `uniq` only removes duplicates if they are adjacent, which requires sorting.

3. **How do you count the number of occurrences of each line in a file?**
   - Use `sort` followed by `uniq -c`: `sort input.txt | uniq -c`

4. **What is the purpose of the `-u` flag in `sort`?**
   - The `-u` flag sorts the input and removes duplicates in one step.

5. **How can you find the position of a specific word in a sorted and unique list?**
   - Use `grep -n` on the sorted and unique list: `sort input.txt | uniq | grep -n "word"`

## Summary of `curl` Command

The `curl` command is a versatile tool for transferring data over various protocols, including HTTP, HTTPS, FTP, and more. It offers a wide range of flags to customize data transfer operations. Here are some key points:

- **Basic Usage**: `curl https://google.com/` fetches the content of the specified URL.
- **Important Flags**:
  - `-#`: Displays a progress meter.
  - `-o <file>`: Saves output to a specified file.
  - `-O`: Saves the file with the server's original name.
  - `-C -`: Resumes a broken download automatically.
  - `--limit-rate <rate>`: Limits the download or upload rate.
  - `-u <user:password>`: Provides user authentication.
  - `-T <file>`: Uploads a file to a server.
  - `-x <proxy>`: Specifies a proxy server.
  - `-I`: Fetches only HTTP headers.
  - `-A <user-agent>`: Sets the user-agent string.
  - `-L`: Follows HTTP redirects.
  - `-b <cookie>`: Specifies cookies for the request.
  - `-d <data>`: Posts data to the server.
  - `-X <method>`: Sets the HTTP method (e.g., GET, POST).

### Answers to Questions

1. **Which flag allows you to limit the download/upload rate of a file?**
   - The flag to limit the download or upload rate is `--limit-rate`.

2. **How will you curl the webpage of https://tryhackme.com/ specifying user-agent as 'juzztesting'?**
   - The command to fetch the webpage with a specified user-agent is:
     ```bash
     curl -A "juzztesting" https://tryhackme.com/
     ```

3. **Can curl perform upload operations? (Yea/Nah)**
   - Yes, `curl` can perform upload operations using the `-T` flag.
   - Answer: Yea.


## Task 11: wget

### Introduction

`wget` is a command-line utility used to download files from the web. It supports HTTP, HTTPS, and FTP protocols. This tool is particularly useful for downloading files in the background or resuming interrupted downloads.

### Important Flags

| Flag             | Description                                                                 |
|------------------|-----------------------------------------------------------------------------|
| `-b`             | Background the downloading process.                                        |
| `-c`             | Continue a partially downloaded file.                                      |
| `-t int`         | Specify the number of retries for a URL.                                    |
| `-O download.txt`| Specify the output name of the downloaded file.                             |
| `-o file`        | Overwrite the logs into another file.                                       |
| `-a file`        | Append logs to an existing file without deleting previous contents.          |
| `-i file`        | Read the list of URLs from a file.                                          |
| `--user=username`| Provide a login username (use `--ftp-user` or `--http-user` if necessary).   |
| `--password=password` | Provide a login password (use `--ftp-password` or `--http-password` if necessary). |
| `--ask-password` | Prompt for a password if login is required.                                 |
| `--limit-rate=10k` | Limit the download speed (supports k and m notation for kB and mB).       |
| `-w=<int>`       | Specify the waiting time before retrieval from a URL (in seconds).          |
| `-T=<int>`       | Timeout the retrieval after a specified amount of time (in seconds).        |
| `-N`             | Enable timestamping.                                                       |
| `-U`             | Specify the user-agent while downloading the file.                          |

### Examples

- **Downloading a file with a different name:**
  ```bash
  wget -O download.txt http://example.com/file
  ```

- **Specifying logfile as `log.txt` with timestamping enabled:**
  ```bash
  wget -o log.txt -N http://example.com/file
  ```

### Q&A Section

1. **How will you enable time logging at every new activity that this tool initiates?**

   - Use the `-a` flag to append logs to an existing file.
   - Use the `-o` flag to overwrite logs into a new file.
   - Use the `-N` flag to enable timestamping in logs.

2. **What command will you use to download `https://xyz.com/mypackage.zip` using wget, appending logs to an existing file named "package-logs.txt"?**

   ```bash
   wget -a package-logs.txt https://xyz.com/mypackage.zip
   ```

3. **Write the command to read URLs from "file.txt" and limit the download speed to 1mbps.**

   ```bash
   wget -i file.txt --limit-rate=1m
   ```



## **xxd** (view last Q)

The `xxd` command is a versatile tool for creating hex dumps of binary data and converting hex dumps back into binary format. It offers several flags to customize the output:

- `-b`: Displays data in binary format.
- `-c <number>`: Sets the number of bytes per row.
- `-g <number>`: Sets the number of bytes per group.
- `-i`: Outputs in C include format.
- `-l <number>`: Specifies the length of the output in bytes.
- `-p`: Generates a plain hexdump without addresses or ASCII.
- `-r`: Reverses a hexdump back to binary.
- `-s <offset>`: Seeks to a specific offset before dumping.
- `-u`: Uses uppercase for hex letters.

The `-c` flag takes precedence over the `-g` flag if they conflict.

**Answers to Questions:**

1. **Seek at the 10th byte (in hex) in `file.txt` and display only 50 bytes:**

   ```bash
   xxd -s 0xA -l 50 file.txt
   ```

2. **Display n bytes of hexdump in 3 columns with a group of 3 octets per row from `file.txt` (Use flags alphabetically):**

   ```bash
   xxd -c 9 -g 3 -l n file.txt
   ```

3. **Which flag has more precedence: `-c` or `-g`?**

   The `-c` flag has more precedence than the `-g` flag.



==this worked better than only -r==

└─$ xxd -r -p flag_1611749859927.txt 
flag{wh3sdw0lw1gl9oqasad2fs48as}




## Task 13: Other Modules

### GPG Command

- **Explanation**: GPG (GNU Privacy Guard) is an open-source alternative to PGP (Pretty Good Privacy), using AES encryption by default. Understanding GPG is crucial when dealing with encrypted files.
- **Resources**: 
- [gpg - Unix, Linux Command - Tutorialspoint](https://www.tutorialspoint.com/unix_commands/gpg.htm)
- [GPG Cheat Sheet (hawaii.edu)](http://irtfweb.ifa.hawaii.edu/~lockhart/gpg/)

### Tar Command

- **Explanation**: The `tar` command is used for creating and extracting tar archives, and it can handle various compression formats like gzip and bzip2.
- **Resources**:
- [Linux Tar Commands Cheatsheet | Never Ending Security (wordpress.com)](https://neverendingsecurity.wordpress.com/2015/04/13/linux-tar-commands-cheatsheet/)
- [tar command in Linux with examples - GeeksforGeeks](https://www.geeksforgeeks.org/tar-command-linux-examples/)

### id/pwd/uname Commands

- **Explanation**: These are fundamental commands for retrieving user information (`id`), current directory (`pwd`), and system information (`uname`).

### ps/kill Commands

- **Explanation**: The `ps` command lists running processes, and `kill` is used to terminate processes by their PID.
- **Alternative**: The `ss` command can be used as an alternative to `netstat` for viewing network connections.
- List processes, and kill processes with PID. To know more about ps command you can find some help [here](https://man7.org/linux/man-pages/man1/ps.1.html).

### netstat Command

- **Explanation**: `netstat` displays network connections, routing tables, interface statistics, etc. Use `man netstat` for more details.
- **Alternative**: The `ss` command provides similar functionality to `netstat` but with more features.
- [Ultimate Netstat Cheat Sheet - Master Netstat in 20 Minutes (rekha.com)](https://www.rekha.com/netstat-cheat-sheet-for-newbies.html)
- [netstat(8) - Linux man page (die.net)](https://linux.die.net/man/8/netstat)
- [SS – Socket Statistics Commands Cheatsheet | Never Ending Security (wordpress.com)](https://neverendingsecurity.wordpress.com/2015/04/13/ss-socket-statistics-commands-cheatsheet/)
### less/more Commands

- **Explanation**: `less` and `more` are pager programs for viewing text files. `less` is more powerful with backward and forward navigation.
- **Additional Command**: The `most` command improves upon `less` and can be installed with `sudo apt install most`.
- [The Difference Between more, less And most Commands - OSTechNix](https://ostechnix.com/the-difference-between-more-less-and-most-commands/)
- [Less and More command (Explained)](https://www.tecmint.com/linux-more-command-and-less-command-examples/#:~:text=Learn%20Linux%20%27less%27%20Command,using%20page%20up%2Fdown%20keys.)
### diff/comm Commands

- **Explanation**: The `diff` command compares two files byte by byte, while `comm` compares two sorted files line by line.
- **Resources**:
  - [Comparing files and directories with the diff and comm Linux commands | Network World](https://www.networkworld.com/article/3279724/comparing-files-and-directories-with-diff-and-comm.html#:~:text=The%20diff%20command%20would%20make,both%20commands%20is%20the%20same.&text=The%20comm%20command%20can%20provide,it%20can%20compare%20two%20files.)
- [diff command in Linux with examples - GeeksforGeeks](https://www.geeksforgeeks.org/diff-command-linux-examples/)
- [comm command in Linux with examples - GeeksforGeeks](https://www.geeksforgeeks.org/comm-command-in-linux-with-examples/)
### base64 Command

- **Explanation**: The `base64` command is used for encoding and decoding data in base64 format.

### tee Command

- **Explanation**: The `tee` command reads from standard input and writes to standard output and files. Use the `-a` flag to append to a file.

### file/stat Commands

- **Explanation**: The `file` command determines file type, and `stat` provides detailed information about a file or filesystem.

### export Command

- **Explanation**: The `export` command sets environment variables for the current shell session.[here](https://www.geeksforgeeks.org/export-command-in-linux-with-examples/).

### reset Command

- **Explanation**: The `reset` command resets the terminal settings to default, useful for fixing a malfunctioning terminal.

### systemctl/service Commands

- **Explanation**: `systemctl` manages systemd services, while `service` manages sysvinit services. Use `systemctl` for systemd-based systems.
- **Caution**: Be cautious with `systemctl` as it can affect system-wide settings.

-  [Difference between Systemctl and service command - Stack Overflow](https://stackoverflow.com/questions/43537851/difference-between-systemctl-and-service-command#:~:text=service%20operates%20on%20the%20files,file%20in%20%2Fetc%2Finit.)
- [Systemctl Cheatsheet (github.com)](https://gist.github.com/adriacidre/307d2f9f5179fc748f22edac5af3d218) (A small cheatsheet you wanna read before working with systemctl).

### Q&A Section

1. **Is it safe to run `systemctl` commands on your main Linux system without proper guidance?**
   - Wrong

2. **How do you import a given PGP private key (e.g., `key.gpg`)?**
   - Use `gpg --import key.gpg`

3. **What command can be used to list all port activity if `netstat` is not available?**
   - `ss`

4. **What command can be used to fix a broken or irregular terminal shell?**
   - `reset`