Here’s a structured summary of **Bash Scripting** fundamentals for automation and sysadmin tasks:

more on 
- [https://www.codewars.com/](https://www.codewars.com/)
- [](https://www.hackerrank.com/)[https://www.hackerrank.com/](https://www.hackerrank.com/)

---

## **Bash Scripting Overview**  
Bash (Bourne Again SHell) is a scripting language used to automate tasks in Linux/macOS terminals. Scripts combine commands to perform complex operations, like backups or system monitoring.

---

### **1. Bash Script Syntax**  
- **Shebang Line**: Start scripts with `#!/bin/bash` to specify the interpreter.  
- **Comments**: Use `#` for notes.  
- **File Permissions**: Make scripts executable with `chmod +x script.sh`.  

**Example Script**:  
```bash  
#!/bin/bash  
echo "Hello, $1!"  # $1 accesses the first parameter  
```  
Run with: `./script.sh World` → Output: `Hello, World!`  

---

### **2. Variables**  
- **Declaration**: `var_name="value"` (no spaces).  
- **Usage**: `$var_name` or `${var_name}`.  
- **Quotes**: Use `"` to preserve spaces in values.  

**Example**:  
```bash  
greeting="Welcome"  
echo "${greeting}, user!"  # Output: Welcome, user!  
```  

---

### **3. Parameters**  
- **Positional Parameters**: `$1`, `$2`, ..., `$9` (arguments passed to the script).  
- **Special Variables**:  
  - `$@`: All arguments.  
  - `$#`: Number of arguments.  

**Example**:  
```bash  
echo "First argument: $1"  
echo "Total arguments: $#"  
```  

What if we didn't want to supply them like this however, and instead it would let us type in our name in a more interactive way, we can do this using `read`.

![](https://i.ibb.co/tzK62bK/carbon-13.png)


### **4. Arrays**  
- **Declaration**: `arr=("element1" "element2")`.  
- **Access Elements**: `${arr[0]}` (zero-indexed).  
- **Loop Through Array**:  
  ```bash  
  for item in "${arr[@]}"; do  
    echo "$item"  
  done  
  ```  

**Example**:  
```bash  
files=("file1.txt" "file2.txt")  
echo "First file: ${files[0]}"  # Output: file1.txt  


```  

set :
`transport[1]='trainride'
`
unset:

`unset transport[1]`

---

### **5. Conditionals**  
- **Syntax**:  
  ```bash  
  if [ condition ]; then  
    # code  
  elif [ condition ]; then  
    # code  
  else  
    # code  
  fi  
  ```  
- **Comparison Operators**:  

| **Operator** | **Description**                  | **Example**              |     |
| ------------ | -------------------------------- | ------------------------ | --- |
| `-eq`        | Equal (numbers)                  | `if [ $a -eq $b ]`       |     |
| `-ne`        | Not equal (numbers)              | `if [ $a -ne $b ]`       |     |
| `==`         | Equal (strings)                  | `if [ "$str" == "yes" ]` |     |
| `-z`         | String is empty                  | `if [ -z "$str" ]`       |     |
| `-f`         | File exists                      | `if [ -f "file.txt" ]`   |     |
| `-w`         | checked if the file was writable |                          |     |
| `-r`         | readable                         |                          |     |
| `-d`         | directory                        |                          |     |
|              |                                  |                          |     |

**Example**:  
```bash  
if [ $# -eq 0 ]; then  
  echo "No arguments provided."  
else  
  echo "First argument: $1"  
fi  
```  

---

### **6. Automation Example: Backup Script**  
```bash  
#!/bin/bash  
# Backup directory  
source_dir="/home/user/docs"  
backup_dir="/backup"  

if [ ! -d "$backup_dir" ]; then  
  mkdir -p "$backup_dir"  
fi  

tar -czf "${backup_dir}/docs_$(date +%F).tar.gz" "$source_dir"  
echo "Backup created at ${backup_dir}/docs_$(date +%F).tar.gz"  
```  

---

### **7. Best Practices**  
1. **Quote Variables**: Prevent errors with spaces (e.g., `"$var"`).  
2. **Error Handling**: Use `set -e` to exit on error.  
3. **Command Substitution**: Capture output with `$(command)`.  
   ```bash  
   current_date=$(date +%F)  
   ```  

---

### **8. Resources**  
- **[Bash Cheat Sheet](https://devhints.io/bash)**: Quick reference for syntax.  
- **[TryHackMe Bash Scripting Room](https://tryhackme.com)**: Hands-on practice.  

---

**Next Steps**: Practice writing scripts for file management, log parsing, or automated updates! 🛠️


## Debbuging

  

Debugging is a very important part of programming so we should get used to problem solving and fixing errors as early as possible. And bash has a few built in features that make our life simple.

When running at the command line you can do:

  

`bash -x ./file.sh`

You can make a simple bash script(now you know some basic syntax) and make something completely wrong. Then step through your program with debug mode and see what it looks like when it throws errors!

  

This tells you which lines are working and which lines are not. If you want to debug at a certain point you can insert `set -x` into your script and `set +x` to end the section like the following:

![](https://i.ibb.co/dWYJkjs/carbon-4.png)

  

  

So lets look at an example. This is our script from earlier being ran with `bash -x ./example.sh`

![](https://i.ibb.co/288ynDZ/carbon-5.png)

  

  

You can see its outputting a **+** for the command and then the output of what that command executed. If there was an error it would output a **-** on that line this makes it easy to spot where you have gone wrong so you can fix them.

  

We can also use multiple variables in something like an echo statement. You aren't just limited to using 1!

![](https://i.ibb.co/vVp45SD/carbon-6.png)  

  

  

Answer the following questions and use this piece of code to guide you.