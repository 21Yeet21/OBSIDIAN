Set Global Identity (first time only)

git config --global user.name "Your Name"
git config --global user.email "your.email@example.com"

create private key

└─$ ssh-keygen -t ed25519 -C "ayoub.touihri11@gmail.com"


Add Your SSH Key to the SSH Agent

eval "$(ssh-agent -s)"
ssh-add ~/.ssh/id_ed25519

then need to copy 

cat ~/.ssh/id_ed25519.pub

### **4. Add the Public Key to GitHub**

1. Go to GitHub and log in.
2. Navigate to **Settings** > **SSH and GPG keys**.
3. Click **New SSH key**.
4. Paste the key from step 3 into the provided field.
5. Save the key.




git config --global user.name "Your Name"
git config --global user.email "your.email@example.com"


## 2. Add the Remote Repository

git remote add origin https://github.com/your-username/your-repo.git


git@github.com:21Yeet21/OBSIDIAN.git




** Verify the Remote**

git remote -v

### **3. Add and Commit Files**

Add the files you want to sync and commit them.

git add .
git commit -m "Initial commit"



### **4. Push to the Remote Repository**

Push your code to the main branch of the remote repository:

git branch -M main
git push -u origin main

- **`-M main`**: Renames the local branch to `main`.
- **`-u origin main`**: Sets `origin` as the default remote for the `main` branch.