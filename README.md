# GitOnTheCluster

A tutorial for the McGaugh Lab on how to connect Git on the MSI cluster for script documentation and version control.

---

## Git + SSH Setup on MSI Cluster (ahl01)

This guide walks you through configuring Git with SSH on the MSI cluster so you can securely clone, pull, and push to GitHub without typing a password or token each time.

---

### ⚙️ 1. Load Git and Set Up Identity

```bash
module load git
git config --global user.name "Your Name"
git config --global user.email "your.email@umn.edu"
```

---

### 🔐 2. Generate a New SSH Key

```bash
cd /panfs/jay/groups/26/mcgaughs/YOUR_USERNAME/GitRepos
ssh-keygen -t ed25519 -C "your.email@umn.edu"
```
When prompted:
- File: type `gitkeys.txt`
- Passphrase: leave empty (just press Enter twice)

---

### 💻 3. Add Your Key to the SSH Agent

```bash
eval "$(ssh-agent -s)"
chmod 600 gitkeys.txt
ssh-add gitkeys.txt
```

---

### 🔎 4. Add Public Key to GitHub

```bash
cat gitkeys.txt.pub
```
Then:
1. Go to [GitHub SSH Keys](https://github.com/settings/keys)
2. Click **"New SSH Key"**
3. Title it something like `MSI Cluster Key`
4. Paste the copied key and save

---

### 🧰 5. Test Your Connection

```bash
ssh -T git@github.com
```

Expected output:
```
Hi your-username! You've successfully authenticated, but GitHub does not provide shell access.
```

---

### 📂 6. Convert a Folder into a Git Repo Linked to GitHub

#### 🆕 Creating a brand new Git repo from a folder

```bash
cd /panfs/jay/groups/26/mcgaughs/YOUR_USERNAME/GitRepos/NewProjectFolder
git init
git add *.sh *.py *.R *.txt README.md
git commit -m "Initial commit"
```

🚨 **Gotcha**: You must create the GitHub repo **before pushing**!
- Go to [https://github.com/new](https://github.com/new)
- Name it the same as your folder
- Make it **private**
- ❌ Do **not** initialize with README or license

```bash
git remote add origin git@github.com:your-username/NewProjectFolder.git
git branch -M main
git push -u origin main
```

#### ❌ If push fails with "non-fast-forward" error:

```bash
git pull --rebase
git push
```

If Git complains about tracking:
```bash
git branch --set-upstream-to=origin/main main
```

---

### 🏗️ Cloning an existing repo

```bash
cd /panfs/jay/groups/26/mcgaughs/YOUR_USERNAME/GitRepos/
git clone git@github.com:your-username/RepoName.git
cd RepoName
```

---

### ✍️ Working with Git

```bash
# After editing any files:
git status
git add script.py
git commit -m "Updated logic"
git push
```

To pull updates:
```bash
git pull
```

---

mkdir -p ~/.ssh
cp drabe004/GitRepos/gitkeys.txt ~/.ssh/id_ed25519
cp drabe004/GitRepos/gitkeys.txt.pub ~/.ssh/id_ed25519.pub
chmod 600 ~/.ssh/id_ed25519
chmod 644 ~/.ssh/id_ed25519.pub

Then in the future:

ssh-add ~/.ssh/id_ed25519


### 📅 MSI Help & Snapshots

If you need help, email elp@msi.umn.edu or call (612) 626-0802

To recover deleted files:

```bash
cd ~/.snapshot
ls -lt
```

---

You're now Git-enabled on the cluster. Version all the things! 🚀
