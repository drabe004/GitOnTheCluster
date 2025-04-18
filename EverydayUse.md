### Everyday Use


## 1. Load Git module
module load git

## 2. Start the SSH agent and add your key (only needed per session)
eval "$(ssh-agent -s)"
ssh-add ~/.ssh/id_ed25519


## 2. Navigate to your repository directory
cd /panfs/jay/groups/26/mcgaughs/drabe004/GitRepos/YourRepoName

## 3. Pull latest changes from GitHub (if you're collaborating)
git pull

## 4. Make your changes
# edit your scripts, run your jobs, etc.

## 5. Check status of changed files
git status

## 6. Add updated files to staging
git add file1.sh file2.py
# or just
git add .

## 7. Commit your changes with a clear message
git commit -m "Updated IQ-TREE script to fix output dir"

## 8. Push changes to GitHub
git push
