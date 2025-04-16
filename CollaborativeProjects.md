
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

## ✅ Recommended Branch Protection Rule for `main`

In your GitHub repo:

1. Go to **Settings** → **Branches**
2. Click **"Add rule"**
3. Set **Branch name pattern** to:
   ```
   main
   ```

4. Enable the following settings:

### ✅ Required

- [x] **Protect matching branches** *(automatically enabled)*
- [x] **Require a pull request before merging**
- [x] **Require conversation resolution before merging**
- [x] **Require linear history**

### ⚠️ Optional (use only if needed)

- [ ] **Require status checks to pass before merging**
  - Enable only if you have automated CI checks (e.g., GitHub Actions).
- [ ] **Require signed commits**
  - For high-security workflows — skip unless needed.
- [ ] **Require deployments to succeed before merging**
  - Use only for GitHub-integrated deployment workflows.

### 🚫 Recommended to leave disabled

- [ ] **Lock branch**
- [ ] **Allow force pushes**
- [ ] **Allow deletions**

---

## 🔐 Access Enforcement

- [x] **Do not allow bypassing the above settings**
- [x] **Apply rules to everyone, including administrators**

---

## 🧠 How Collaborators Will Work

1. Clone the repository:
   ```bash
   git clone git@github.com:your-username/repo-name.git
   ```

2. Create a feature branch:
   ```bash
   git checkout -b my-feature
   ```

3. Make changes, then stage and commit:
   ```bash
   git add file.py
   git commit -m "Added new feature"
   ```

4. Push the feature branch:
   ```bash
   git push origin my-feature
   ```

5. Open a **Pull Request** via GitHub and request review

6. Resolve any comments, then merge into `main`



