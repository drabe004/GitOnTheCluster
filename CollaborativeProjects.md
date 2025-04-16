
# 🧬 Collaborating in a Shared GitHub Repo

This guide shows you how to share a **private GitHub repo** with collaborators and how they can edit, sync, and contribute to the project — from their computer or from the MSI cluster.

---

## 🔒 Part 1: You (the repo owner) — How to Share the Private Repo

1. Go to your private repo on GitHub  
   e.g. https://github.com/your-username/MyProjectRepo

2. Click the **Settings** tab (upper right of the repo)

3. In the left sidebar, select **Collaborators and teams**

4. Click **Add people**

5. Type your collaborator’s GitHub username or email  
   *(e.g., `githubUser123`)*

6. Click **Add** — they’ll get an invite via email and GitHub notification

✅ Done! Now they can collaborate just like you.

---

## 👥 Part 2: Collaborators — How to Accept and Start Working

### ✅ Step 1: Accept the invite
- Visit https://github.com/notifications or check your email
- Click **Accept Invitation**

### ✅ Step 2: Clone the repo to your system or the cluster

```bash
# On MSI cluster or your computer:
cd /path/to/projects/

git clone git@github.com:your-username/MyProjectRepo.git
cd MyProjectRepo


##✍️ Part 3: How to Make Changes
## Pull New Changes from Others
##Before you begin editing, sync your local copy with GitHub:

git pull

git add changed_script.py
git commit -m "Describe what I changed"
git push


#🧠 Tip: Only git add the files you actually changed — this keeps your commits clean and readable.

##errors
Permission denied (publickey).

####Make sure that you:

#Generated an SSH key using ssh-keygen

#Added your public key to GitHub SSH Settings

#Cloned the repo using the SSH URL (git@github.com:...) and not HTTPS




