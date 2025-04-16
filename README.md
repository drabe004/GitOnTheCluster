# GitOnTheCluster
A tutorial for the McGaugh Lab on how to connect Git on the cluster for script documentation and version control.

---

# Git + SSH Setup on MSI Cluster (ahl01)

This guide walks you through configuring Git with SSH on the MSI cluster so you can securely clone, pull, and push to GitHub without typing a password or token each time.

---

## ⚙️ 1. Load Git and Set Up Identity

```bash
module load git

git config --global user.name "Your Name"
git config --global user.email "your.email@umn.edu"
```

---

## 🔐 2. Generate a New SSH Key

Navigate to your Git repo directory or somewhere safe:

```bash
cd /panfs/jay/groups/26/mcgaughs/YOUR_USERNAME/GitRepos
```

Generate a key:

```bash
ssh-keygen -t ed25519 -C "your.email@umn.edu"
```

When prompted:
- File: type `gitkeys.txt`
- Passphrase: leave empty (just press Enter twice)

---

## 💻 3. Add Your Key to the SSH Agent

Start the SSH agent and add your key:

```bash
eval "$(ssh-agent -s)"
chmod 600 gitkeys.txt
ssh-add gitkeys.txt
```

---

## 🔎 4. Add Public Key to GitHub

Print the public key:

```bash
cat gitkeys.txt.pub
```

Then:
1. Go to [GitHub SSH Keys](https://github.com/settings/keys)
2. Click **"New SSH Key"**
3. Title it something like `MSI Cluster Key`
4. Paste the copied key and save

---

## 🧰 5. Test Your Connection

```bash
ssh -T git@github.com
```

You should see:
```
Hi your-username! You've successfully authenticated, but GitHub does not provide shell access.
```

---

## 📂 6. Convert a Folder into a Git Repo Linked to GitHub

```bash
cd /panfs/jay/groups/26/mcgaughs/YOUR_USERNAME/GitRepos/YourFolder

# Initialize Git
git init

# Add files and commit
git add *.sh *.py *.R README.md
git commit -m "Initial commit"

# Set SSH remote
git remote add origin git@github.com:your-username/YourFolder.git

# Set default branch name (if not already)
git branch -M main
```

---

## ⚠️ If You Created the GitHub Repo First

If GitHub already has a README or other files, do this **before pushing**:

```bash
git pull origin main --allow-unrelated-histories
```

You may be dropped into a `vim` merge message screen — just type `:wq` and press Enter to save and exit.

Then:

```bash
git push -u origin main
```

If Git complains about "no tracking information", run:

```bash
git branch --set-upstream-to=origin/main main
```

---

## ⚖️ 7. Common Git Workflow

```bash
cd your-repo-name

# Edit files

git add script.sh
git commit -m "Updated script"
git push
```

To get updates from GitHub:

```bash
git pull
```

---

## 📅 MSI Help & Snapshots

Need help? Email **elp@msi.umn.edu** or call **(612) 626-0802**

Accidentally delete something? Home directories are snapshot protected:

```bash
cd ~/.snapshot
ls -lt
```

---

You're now Git-enabled on the cluster. Version all the things! 🚀
