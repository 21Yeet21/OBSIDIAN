
## From Scratch
To upload your wallpapers to a GitHub repository, follow these steps:

### 1. Create a GitHub Repository
- Go to [GitHub](https://github.com).
- Log in to your account.
- Click the "+" icon in the upper-right corner and select "New repository."
- Choose a name for the repository, e.g., `wallpapers`, and click "Create repository."

### 2. Set Up Git Locally
If you haven't already, set up Git on your local machine:
- **Install Git** (if not already installed):
  - [Download Git](https://git-scm.com/downloads).
- Open a terminal and configure Git with your username and email:
  ```bash
  git config --global user.name "Your Name"
  git config --global user.email "your_email@example.com"
  ssh-keygen -t rsa -b 4096 -C "ayoub.touihri11@gmail.com"

  ```

- When prompted, press Enter to save the key in the default location (`~/.ssh/id_rsa`).
    
- To add the SSH key to the SSH agent, run the following:- When prompted, press Enter to save the key in the default location (`~/.ssh/id_rsa`).
    
- To add the SSH key to the SSH agent, run the following:
- 
eval "$(ssh-agent -s)"
ssh-add ~/.ssh/id_rsa


## Accessing with token for the first time 

It looks like you're trying to use HTTPS to push to your GitHub repository, and Git is asking for your username and password. GitHub has recently changed how it handles authentication, and now **Personal Access Tokens (PATs)** are required instead of your regular password.

Here’s how you can fix the issue:

### Step 1: Create a Personal Access Token (PAT)

GitHub no longer allows using your GitHub password for authentication when pushing via HTTPS. Instead, you’ll need to use a **Personal Access Token (PAT)**.

1. Go to [GitHub's Token Settings page](https://github.com/settings/tokens).
2. Click **Generate new token**.
3. Give your token a name (e.g., "GitHub push token").
4. Select the appropriate scopes:
    - For pushing to a repository, you'll need `repo` scope. If you're just interacting with public repos, you may need only `public_repo`.
    - Click **Generate token**.
5. Copy the generated token to your clipboard. **Note: Once you leave this page, you won’t be able to see the token again.**

### Step 2: Use the Personal Access Token (PAT) when pushing

Now, when you push to GitHub, instead of entering your password, you'll use the **Personal Access Token (PAT)**.

1. In the terminal, when you're prompted for your GitHub **username**, enter your GitHub username.
2. When prompted for your **password**, paste the **Personal Access Token** you just generated (not your GitHub password).

### Step 3: Cache your credentials (optional)

To avoid being asked for your username and PAT every time, you can enable Git's credential caching. Here’s how:

1. Run the following command to cache your credentials:
    
    ```bash
    git config --global credential.helper cache
    ```
    
    This will store your credentials in memory for 15 minutes by default, so you won’t have to re-enter them for each push.
    
2. Alternatively, to store your credentials permanently, use the following:
    
    ```bash
    git config --global credential.helper store
    ```
    
    With this, Git will store your credentials in a plain text file (`~/.git-credentials`), so it won't ask you for them again.
    

### Step 4: Push Again

Now, try pushing again with:

```bash
git push origin main
```

When prompted for a password, paste your **Personal Access Token** instead.

---

Let me know if you encounter any issues while trying this!


## Else

### 3. Initialize a Local Repository and Add Files
- Navigate to the folder containing your wallpapers in your terminal.
  ```bash
  cd /path/to/your/wallpapers
  ```
- Initialize a Git repository:
  ```bash
  git init
  ```
- Add all your wallpaper files to the repository:
  ```bash
  git add .
  ```

### 4. Commit Your Changes
- Commit the added files with a message:
  ```bash
  git commit -m "Initial commit of wallpapers"
  ```

### 5. Link to the GitHub Repository
- Add the URL of your GitHub repository as the remote:
  ```bash
  git remote add origin https://github.com/your-username/wallpapers.git
  ```

### 6. Push Files to GitHub
- Push your files to the GitHub repository:
  ```bash
  git push -u origin master
  ```

### 7. Verify
- Go to your GitHub repository page, and you should see the wallpapers uploaded!

---

Let me know if you need help with any of these steps!
## Update

To add more wallpapers to your GitHub repository in the future, you can follow these steps:

### 1. Navigate to the Repository Folder

- Open your terminal and navigate to the folder where your repository is stored locally:
    
    ```bash
    cd /path/to/your/wallpapers
    ```
    

### 2. Add New Files or Modify Existing Files

- Add new wallpapers to the folder or modify existing files.

### 3. Stage the Changes

- Use `git add` to stage the changes (new or modified files):
    - To add specific files:
        
        ```bash
        git add file1.jpg file2.png
        ```
        
    - To add all changes (new files and modifications):
        
        ```bash
        git add .
        ```
        

### 4. Commit the Changes

- Commit the staged changes with a descriptive message:
    
    ```bash
    git commit -m "Added new wallpapers"
    ```
    

### 5. Push the Changes to GitHub

- Push the committed changes to the remote repository on GitHub:
    
    ```bash
    git push
    ```
    

That's it! The new or modified wallpapers will now be available in your GitHub repository. Repeat these steps as needed to keep adding new wallpapers.


## 2nd PC

If you want to log in from another PC and add pictures to your GitHub repository, follow these steps:

### 1. Set Up Git on the New PC

- Install Git if it's not already installed:
    - On Ubuntu:
        
        ```bash
        sudo apt update
        sudo apt install git
        ```
        
    - On Windows or macOS, follow the [Git installation guide](https://git-scm.com/book/en/v2/Getting-Started-Installing-Git).

### 2. Configure Git (If Not Done Already)

- Set up your user name and email on the new PC (you only need to do this once):
    
    ```bash
    git config --global user.name "Your Name"
    git config --global user.email "your_email@example.com"
    ```
    

### 3. Clone the Repository to the New PC

- Go to your GitHub repository page and copy the repository URL (either HTTPS or SSH).
- Open the terminal on the new PC and clone the repository:
    
    ```bash
    git clone https://github.com/your-username/your-repo-name.git
    ```
    

### 4. Navigate to the Repository Folder

- Change to the directory where the repository was cloned:
    
    ```bash
    cd your-repo-name
    ```
    

### 5. Add New Pictures to the Repo

- Copy the pictures you want to upload into the repository folder, or create a subfolder like `wallpapers` to organize them.

### 6. Stage the Changes

- Add the new pictures to Git staging area:
    
    ```bash
    git add .
    ```
    

### 7. Commit the Changes

- Commit the changes with a meaningful message:
    
    ```bash
    git commit -m "Added new pictures"
    ```
    

### 8. Push the Changes to GitHub

- Push the commit to your GitHub repository:
    
    ```bash
    git push
    ```
    

### 9. Authentication (If Required)

- If you’re using HTTPS, you’ll be prompted to log in with your GitHub username and password (or a personal access token if 2FA is enabled).
- If using SSH, ensure you have your SSH key set up and added to GitHub. If not, follow the [SSH key setup guide](https://docs.github.com/en/github/authenticating-to-github/connecting-to-github-with-ssh).

Once these steps are complete, your pictures will be added to the GitHub repository from the new PC.