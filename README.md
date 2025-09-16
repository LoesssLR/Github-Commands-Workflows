# 📘 GitHub Commands & Workflows

This repository contains a structured collection of **commands and workflows in Git and GitHub**, organized by practical scenarios:  
- First push of a local project.  
- Working with branches and group projects.  
- Pull requests.  
- Managing remote repositories.  
- Consolidating multiple repositories.  
- Useful everyday commands.  

---

## 🏫 Academic Information

- **University**: Universidad Técnica Nacional  
- **Campus**: Pacífico  
- **Major**: Information Technology Engineering

**Author**: Luis Alejandro López Reyes  

---

## 🚀 Scenarios & Commands

### 1️⃣ First push of a local project

```bash
git init
git remote add origin REPO_URL
git branch -m main
git add .
# (Optional if already configured before)
git config --global user.name "YourUsername"
git config --global user.email "YourEmail"
git commit -m "Project start"
git push -u origin main
```

---

### 2️⃣ Pull Request from the terminal

```bash
# Verify folder and branch
ls
git branch

# Add and commit changes
git add .
git commit -m "Change message"

# (Optional if not configured before)
git remote add origin https://github.com/User/Repo.git
git branch -M main

# Publish changes
git push -u origin main
```

---

### 3️⃣ Remote repository already configured

```bash
git add .
git commit -m "Change message"
git push
```

---

### 4️⃣ Download updates

```bash
# General
git pull

# Main branch
git pull origin main
```

---

### 5️⃣ Group projects with branches

```bash
# Clone repository
git clone https://github.com/User/finalProject.git
cd finalProject

# Create initial structure
mkdir css js img php
echo. > index.html
echo. > css/style.css
echo. > js/script.js
echo. > php/connection.php

# Push to GitHub
git status
git add .
git commit -m "Initial structure"
git push -u origin main
```

📌 **Create and work with branches:**

```bash
git checkout -b design   # Create a new branch
git branch               # Check current branch
git add .
git commit -m "Adjustments"
git push -u origin design
```

📌 **Update branches after a merge:**

```bash
git checkout main
git pull origin main
git checkout design
git merge main
```

⚠️ **Rule:** Every branch different from `main` must be merged through a Pull Request.

---

### 6️⃣ Change the remote repository

```bash
git remote -v
git remote remove origin
git remote add origin https://github.com/User/NewRepo.git
git remote -v
```

---

### 7️⃣ Consolidate multiple repositories

```bash
# Create central folder and move everything inside
mkdir UnifiedProject
# Copy folders and remove internal .git
Get-ChildItem -Recurse -Force -Filter ".git" | `
  Where-Object { $_.PSIsContainer } | `
  Remove-Item -Recurse -Force

# Initialize new repo
git init
git remote add origin REPO_URL
git add .
git commit -m "Project consolidation"
git branch -M main
git push -u origin main
```

Optional: clean commit history.

```bash
git rebase -i --root
git push --force
```

---

## 🛠️ Useful Commands

```bash
# Status and changes
git status
git add <file>
git commit -m "Message"

# Branches
git branch <name>
git switch <name>
git branch -d <name>

# Collaboration
git merge <branch>
git push <remote> <branch>
git pull <remote> <branch>

# Recovery
git fetch
git reset --hard HEAD
git revert <hash>

# Advanced
git diff <a> <b>
git show <hash>
git stash
git stash pop
git cherry-pick <hash>
git rebase <base>
```

---

## 📘 Learning Outcomes

- Complete workflow with Git and GitHub.  
- Managing individual and group repositories.  
- Collaboration strategies with branches and PRs.  
- Remote repository reconfiguration.  
- Consolidation of multiple projects into one.  

---

## 📜 License

This repository was created for **educational** and **personal documentation** purposes.  
