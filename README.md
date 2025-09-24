# 📘 GitHub Commands & Workflows.

This repository contains a structured collection of **commands and workflows for Git and GitHub**, organized by practical scenarios and real examples.  

---

## 🏫 Academic Information.

- **University**: Universidad Técnica Nacional.  
- **Campus**: Pacífico.  
- **Major**: Information Technology Engineering.  

**Author**: Luis Alejandro López Reyes.  

---

## 🚀 Scenarios & Commands.

### Steps to upload a project to GitHub for the first time (from the folder to upload using CMD/PowerShell):

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

### Steps to create a Pull Request on GitHub from the terminal (example using VS Code terminal):

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

## 👥 Group projects and branching (from terminal).

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

## 🔁 Change the remote repository (useful if you linked the wrong remote or need to switch).

```bash
git remote -v
git remote remove origin
git remote add origin https://github.com/xxx/xxx.git
git remote -v
# The remote URL should now be updated.
```

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

## 🏢 Example of Real Business Workflow with Git.

Several branches are created, which work like folders or a large directory.

A branch is created for each section of the company (PRODUCTION, QA, DEV, etc.).

Developers take the latest version of DEV and create a copy, which becomes a temporary branch (usually named after the requirement) from DEV. This is where they will work, making commits (each with an associated ID, essentially linked to user stories), continuing this process until the requirement is completed.

Before pushing changes to DEV, they must be reviewed to ensure they work correctly and meet the assigned requirement. For this, a Pull Request is created (a request to review the version of the code before integrating it into DEV, where it will either be approved or rejected).

Once all requirements are approved and merged into DEV, a CI/CD pipeline runs all unit tests defined in a YAML file. If all tests pass, the changes are deployed to the WEB DEV server. If not, they must be fixed. After this stage, the QA team starts requesting each requirement using git cherry-pick <commit_id> from the WEB DEV server in order to test the code delivered by developers, checking whether it works or produces errors. These tests are based on acceptance criteria. If the code passes the tests, it is integrated into PRODUCTION; otherwise, the developer is notified to fix the issues and repeat the process.

Once everything has been verified, compiled, and confirmed error-free, the changes are added to PRODUCTION. At that point, a QA team member may also access the production environment to verify that everything is functioning correctly. In most companies, new requirements are added on a weekly basis.

For this reason, it is essential to clearly and correctly write the requirements and acceptance criteria. If a requirement is poorly written or ambiguous, it could cause problems—even in production.

The workflow looks like this:

### 🔄 Step by Step with Commands.

#### 1. Developer creates a feature branch from DEV.
```bash
git checkout dev
git pull origin dev
git checkout -b feature/login
```

#### 2. Developer makes changes and commits.
```bash
git status
git add .
git commit -m "feat: add login screen with validation"
```

#### 3. Push branch and create Pull Request.
```bash
git push -u origin feature/login
```

#### 4. Pull Request is reviewed and merged into DEV.

#### 5. CI/CD deploys to DEV environment automatically.

#### 6. QA tests with cherry-pick on QA branch.
```bash
git checkout qa
git pull origin qa
git cherry-pick <commit_id>
```

#### 7. If approved, changes are deployed to PROD.
```bash
git checkout main
git pull origin main
git cherry-pick <commit_id>
git push origin main
```

### 📌 Summary of Workflow.

1. **Developer** → feature branch → commits → Pull Request.  
2. **Approver** → reviews and approves/rejects.  
3. **DEV branch + CI/CD** → automated tests and deploy to DEV.  
4. **QA branch + Cherry-pick** → isolated testing.  
5. **Main/Master branch** → final deploy to Production.  

---

## 🛠️ Useful Additional Commands.

### Daily development
```bash
git status                     # Show status of changes
git add <file>                 # Stage changes
git add .                      # Stage all changes
git commit -m "msg"            # Commit staged changes with message
```

### Branch management
```bash
git branch                     # Show branches
git branch <branch-name>       # Create a new branch
git branch -M <branch-name>    # Rename/move branch
git checkout <branch-name>     # Switch to an existing branch
git checkout -b <branch-name>  # Create and switch to a new branch
git switch <branch-name>       # Switch to a branch
git branch -d <branch-name>    # Delete a branch
```

### Integration and collaboration
```bash
git remote add origin <url>    # Link local repo to remote
git push -u origin <branch>    # Push changes to remote and set upstream
git push                       # Push commits
git pull origin <branch>       # Fetch and merge from remote
git merge <branch>             # Merge a branch into current
git fetch                      # Fetch changes without merging
```

### Checking history
```bash
git log                        # Show commit history
git show <hash>                # Show details of a commit
git diff <a> <b>               # Compare two commits, branches or files
```

### Recovery and cleanup
```bash
git checkout -- <file>         # Undo local changes in a file
git reset --soft origin/<br>   # Soft reset (keep changes)
git reset --hard origin/<br>   # Hard reset (discard changes)
git reset --hard HEAD          # Discard all local changes
git revert <commit-hash>       # Revert a commit
```

### Stashing
```bash
git stash                      # Save temporary changes
git stash pop                  # Restore and delete stash
git stash apply                # Restore stash but keep it saved
git stash list                 # Show all stashes
```

### Cherry-pick
```bash
git cherry-pick <hash>         # Apply a commit from another branch
git cherry-pick --abort        # Abort cherry-pick
git cherry-pick --continue     # Continue after conflict resolution
git cherry-pick --skip         # Skip current commit in sequence
```

### Advanced and utilities
```bash
git rebase <base>              # Reapply commits on top of another base
```

---

## 📘 Learning Outcomes

- Complete workflow with Git and GitHub.  
- Managing individual and group repositories.  
- Collaboration strategies with branches and Pull Requests.  
- Remote repository reconfiguration.  
- Consolidation of multiple projects into a single repository.  
- Recovery, stashing and cherry-picking strategies.
- Example of complete workflow used by companies.

---

## 📜 License

This repository was created for **educational** and **personal documentation** purposes.
