
### run the script manually
cd to the script folder wich is ==documents== then run it
./sync_git.sh  
this will update the repo



### Summary: Setting Up Git Synchronization Script

Here's a step-by-step guide on how to set up the script to sync a folder with your Git repository, and ensure everything works correctly.

---

###### 1. **Create Git Repository**

If you haven't already, create a new Git repository on GitHub.

1. Go to [GitHub](https://github.com/).
2. Click on **New Repository**.
3. Name the repository (e.g., `OBSIDIAN`).
4. Copy the repository URL (e.g., `https://github.com/username/OBSIDIAN.git`).

---

###### 2. **Set Up Local Git Repository**

Navigate to the folder you want to sync with Git (e.g., `YeeT'S`).

```bash
cd /home/lableb/Insync/zvayndj@gmail.com/Dropbox/obsidian/YeeT'S
```

Initialize the Git repository:

```bash
git init
```

---

###### 3. **Add Remote Repository**

Add your GitHub repository as a remote:

```bash
git remote add origin https://github.com/username/OBSIDIAN.git
```

---

###### 4. **Set Up SSH Key (Optional)**

If you haven’t already, set up SSH keys for GitHub:

1. Generate an SSH key:
    
    ```bash
    ssh-keygen -t rsa -b 4096 -C "your_email@example.com"
    ```
    
2. Add the SSH key to your GitHub account following the instructions [here](https://docs.github.com/en/github/authenticating-to-github/connecting-to-github-with-ssh).
    

---

###### 5. **Create and Edit Sync Script**

Create a new script to automate the sync process:

```bash
nano /home/lableb/Documents/sync_git.sh
```

Add the following script to automatically commit and push your changes:

```bash
#!/bin/bash

# Change directory to your Git folder
cd "/home/lableb/Insync/zvayndj@gmail.com/Dropbox/obsidian/YeeT'S"

# Git commands
git add .
git commit -m "Automated commit"
git push origin main
```

**Important:** Use double quotes for paths with spaces or special characters (e.g., `YeeT'S`).

Save and close the file (`Ctrl + X`, `Y`, then `Enter`).

Make the script executable:

```bash
chmod +x /home/lableb/Documents/sync_git.sh
```

---

###### 6. **Test the Script**

Run the script manually to check if everything works:

```bash
bash /home/lableb/Documents/sync_git.sh
```

If the script runs successfully and pushes the changes to your GitHub repository, it’s ready to go!

---

###### 7. **Automate with Cron**

To run the script automatically every 30 minutes, set up a cron job:

1. Edit the crontab:
    
    ```bash
    crontab -e
    ```
    
2. Add this line to run the script every 30 minutes:
    
    ```bash
    */30 * * * * /home/lableb/Documents/sync_git.sh >> /home/lableb/sync_git.log 2>&1
    ```
    
3. Save and exit the crontab.
    

---

###### 8. **Check Cron Logs**

To check if the cron job is running correctly:

```bash
sudo journalctl -u cron
```

If there are any issues, check the cron log file (`/home/lableb/sync_git.log`), or verify the script path and permissions.

---

###### Troubleshooting

- **Permission Issues**: Ensure that the script is executable and the user running cron has permission to access the necessary directories.
- **Authentication Errors**: If you encounter authentication issues when pushing, ensure you’re using the correct Git credentials (SSH key or personal access token).

---

By following these steps, your folder will be synced with the GitHub repository automatically every 30 minutes. You can modify the cron job as needed to adjust the frequency.



### Steps to Upload a New Repository to GitHub

When you want to upload a new repository to GitHub, here are the steps to follow. Some steps are done only once (initial setup), and some steps are repeated every time you want to upload new changes.

---

###### **1. Initial Setup (Done Once)**

These steps are only done once when you're setting up your local repository or linking it to GitHub for the first time.

###### **a. Create a Repository on GitHub**

1. Go to [GitHub](https://github.com/).
2. Click **New** to create a new repository.
3. Choose a name for your repository (e.g., `my-repo`).
4. Optionally, add a description and select whether it’s public or private.
5. Copy the repository URL (e.g., `https://github.com/username/my-repo.git`).

---

###### **b. Initialize the Local Repository (Done Once)**

Navigate to the folder you want to sync with GitHub, then:

```bash
cd /path/to/your/folder
git init
```

---

###### **c. Link Local Repository to Remote Repository (Done Once)**

Add the GitHub repository as the remote:

```bash
git remote add origin https://github.com/username/my-repo.git
```

---

###### **d. Set Up Git (Done Once)**

Set up your username and email for Git (done once):

```bash
git config --global user.name "Your Name"
git config --global user.email "your_email@example.com"
```

---

###### **2. Repeated Steps (Every Time You Want to Upload/Push Changes)**

These are the steps you'll repeat every time you want to upload new changes to GitHub.

###### **a. Stage and Commit Your Changes**

After modifying files, stage the changes:

```bash
git add .
```

Commit the changes:

```bash
git commit -m "Your commit message"
```

###### **b. Push Changes to GitHub**

Push the changes to the GitHub repository:

```bash
git push origin main
```

> **Note:** The first time you push, GitHub may ask for authentication. After that, you can set up SSH keys or use a Git credential helper to avoid entering your password repeatedly.

---

###### **3. Optional: Set Up Automatic Push (Cron Job)**

If you want to automate the process of pushing changes, you can use the `sync_git.sh` script with a cron job, as we did earlier, to automatically add, commit, and push your changes periodically.

---

###### **Summary of Steps to Repeat:**

1. **Stage changes**: `git add .`
2. **Commit changes**: `git commit -m "Your commit message"`
3. **Push changes**: `git push origin main`

###### **Steps Done Once:**

1. **Create the GitHub repo**.
2. **Initialize local repo**: `git init`.
3. **Link remote repo**: `git remote add origin <URL>`.
4. **Set up Git config**: `git config --global user.name` and `git config --global user.email`.

By following this flow, you can easily update your repository on GitHub whenever you make changes to your local folder.