# 📘 GitHub Commands & Workflows.

This repository contains a structured collection of **commands and workflows for Git and GitHub**, organized by practical scenarios and real examples.  

---

## 🏫 Academic Information

- **University**: Universidad Técnica Nacional.  
- **Campus**: Pacífico.  
- **Major**: Information Technology Engineering.  

**Author**: Luis Alejandro López Reyes.  

---

## 🚀 Scenarios & Commands.

### Steps to upload a Python file to GitHub for the first time (from the folder to upload using CMD):

```bash
git init
git remote add origin _REPO_URL_
git branch -m main
git add .
# (Optional if already configured): 
git config --global user.name "xxx"
git config --global user.email "xxx@xxx.com"
git commit -m "xxx"
git push -u origin main
```

---

### Steps to create a Pull Request on GitHub from the terminal (example using Python terminal or CMD):

```bash
# Verify that we are inside the folder:
ls

# Verify current branch:
git branch

# Add changes:
git add .

# Add the remote (Not necessary if already linked):
git remote add origin https://github.com/xxx/xxx.git

# Set the main branch (Also not necessary if you're already on the correct branch):
git branch -M main

# Commit:
git commit -m "Update"

# Push changes:
git push -u origin main
```

---

### If the remote repository is already configured:

```bash
git add .
git commit -m "Update"
git push
```

---

### Download updates from others:

```bash
# If the repository is already correctly configured:
git pull

# To specify a branch (for example, the main branch):
git pull origin main
```

---

---

## 👥 Group projects and branching (from CMD).

- Create the repository in GitHub (without a README) and copy the HTTPS address.

- Open CMD and navigate to the Desktop or desired path:
```
C:\Users\Admin\Desktop>
```

- Clone the repository:
```bash
git clone https://github.com/xxx/xxx.git
```

- Enter the folder:
```bash
cd proyectoFinal_Web1
```

- Create folders for the project:
```bash
mkdir css js img php
```

- Create files inside each folder (Windows CMD example):
```bash
echo. > index.html
echo. > css\style.css
echo. > js\script.js
echo. > php\conexion.php
```

- Verify everything was created:
```bash
dir
```

- Once the project structure is ready, push to GitHub:
```bash
git status
git add .
git commit -m "Estructura inicial del proyecto"
git push -u origin main
```

- Each team member creates their own branch to work:
```bash
git checkout -b diseño
```

- Verify current branch:
```bash
git branch
```

- Example of adding changes to the `diseño` branch:
```bash
git add .
git commit -m "Ajustes"
git push -u origin diseño
```

- After pushing changes to the branch, create a Pull Request on GitHub:
  1. Go to the repository on GitHub.
  2. Click the "Pull Requests" tab.
  3. Click "New Pull Request".
  4. Choose the branch you worked on and compare it with `main`.
  5. Review the changes.
  6. Write a clear message in the PR describing what was added or modified.
  7. Click "Create Pull Request".

- Steps for the team leader:
  - Review Pull Requests on GitHub.
    - If everything is OK, approve and click "Merge" to merge changes into `main`.
    - If there are issues, comment on the PR so the teammate can fix them.
  - To merge the PR into `main`:
    1. Open the Pull Request.
    2. Click "Merge Pull Request".
    3. Confirm the merge.
    4. (Optional) Delete the branch if it will not be used anymore.

After merging the PR into `main`, all team members must run the following steps locally:

```bash
git checkout main        # Go to main branch
git pull origin main     # Download the latest version
git checkout diseño      # Go back to your working branch
git merge main           # Update your branch with the latest changes from main
```

This ensures that everyone works with the most up-to-date code.

*** Optional - Share the branch with team members:
```bash
git fetch
git checkout diseño
```

*** Rule: Every branch different from `main` must be merged via a Pull Request, even if you worked on it as the leader.

---

---

## 🔁 Change the remote repository (useful if you linked the wrong remote or need to switch).

```bash
git remote -v
git remote remove origin
git remote add origin https://github.com/xxx/xxx.git
git remote -v
# The remote URL should now be updated.
```

---

---

## 📦 Consolidate multiple existing GitHub repositories into a single repository.

**Goal:** gather content from many repositories into one clean repository.

- Gather all repository content into a single local folder.

  - Create a new folder named `[FolderName]`.
  - Copy all project folders into that new folder.

- Remove internal `.git` folders (if some subfolders were separate repositories).

  - This prevents them from being added as submodules.
  - You can remove `.git` folders manually or with PowerShell:

```powershell
Get-ChildItem -Recurse -Force -Filter ".git" | Where-Object { $_.PSIsContainer } | Remove-Item -Recurse -Force
```

- Initialize the new repository.

  - Inside `[FolderName]`:

```bash
git init
git remote add origin [REPO_URL]
git add .
git commit -m "Agrupación de todas las semanas, tareas y parcial del curso Web I"
git branch -M main
git push -u origin main
```

- Fix submodule warnings.

  - If you see warnings like `adding embedded git repository` on GitHub, run:

```bash
git rm --cached folder_name
```

  - Then re-add files:

```bash
git add .
git commit -m "Eliminar submódulos y añadir contenido directamente"
git push --force
```

- Optional: Reword commit messages and clean history.

  - Rewrite history with:

```bash
git rebase -i --root
```

  - Change `pick` to `reword` and write new, more descriptive commit messages.
  - After finishing:

```bash
git push --force
```

This procedure results in a single clean, consolidated, professional repository that is easy to maintain.

---

---

## 🛠️ Useful Additional Commands

### Daily development
```bash
git status                     # Show status of changes
git add <file>                 # Stage changes
```

### Branch management
```bash
git branch <branch-name>       # Create a new branch
git switch <branch-name>       # Switch to a branch
git branch -d <branch-name>    # Delete a branch
```

### Integration and collaboration
```bash
git merge <branch>             # Merge a branch into current
git remote add <name> <url>    # Add a remote repository
git push <remote> <branch>     # Push changes to a remote branch
git pull <remote> <branch>     # Fetch and merge changes from remote
```

### Recovery and cleanup
```bash
git fetch                      # Fetch changes without merging
git reset --hard HEAD          # Discard all local changes
git revert <commit-hash>       # Revert a commit
```

### Advanced and utilities
```bash
git diff <a> <b>               # Compare two commits, branches or files
git show <hash>                # Show details of a commit
git stash                      # Save temporary changes and clean working tree
git stash pop                  # Restore changes from stash
git cherry-pick <hash>         # Apply a specific commit to current branch
git rebase <base>              # Reapply commits on top of another base
```

---

## 📘 Learning Outcomes

- Complete workflow with Git and GitHub.  
- Managing individual and group repositories.  
- Collaboration strategies with branches and Pull Requests.  
- Remote repository reconfiguration.  
- Consolidation of multiple projects into a single repository.  

---

## 📜 License

This repository was created for **educational** and **personal documentation** purposes.
