# GitOnTheCluster
A tutorial for the McGaugh Lab on how to connect Git on the cluster for script documentation
# Git + SSH Setup on MSI Cluster (ahl01)

This guide helps lab members set up Git with SSH on the MSI cluster so you can clone, pull, and push to GitHub without re-entering credentials.

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
- Passphrase: leave empty (press Enter twice)

---

## 💻 3. Add Your Key to the SSH Agent

Start the agent:

```bash
eval "$(ssh-agent -s)"
```

Fix permissions and add key:

```bash
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
3. Title: `MSI Cluster Key`
4. Paste your copied public key and save

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

## 📂 6. Clone a GitHub Repo

```bash
git clone git@github.com:your-username/your-repo-name.git
```

---

## ⚖️ 7. Common Git Workflow

```bash
cd your-repo-name

# Edit files

git add filename.py
git commit -m "Describe your change"
git push origin main
```

To get updates:
```bash
git pull origin main
```

---

## 📅 MSI Help & Snapshots

- Need help? Email **elp@msi.umn.edu** or call **(612) 626-0802**
- Accidentally delete something? Home directories are snapshot protected:

```bash
cd ~/.snapshot
ls -lt
```

---

Happy version-controlling! 🚀

