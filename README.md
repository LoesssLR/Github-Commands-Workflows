# 📘 GitHub Commands & Workflows.

This repository contains a structured collection of **commands and workflows for Git and GitHub**, organized by practical scenarios and real examples.  

---

## 🏫 Academic Information.

- **University**: Universidad Técnica Nacional.  
- **Campus**: Pacífico.  
- **Major**: Information Technology Engineering.  
- **Author**: Luis Alejandro López Reyes.  

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

### Steps to upload changes to GitHub from the terminal (example using VS Code terminal):

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

### 🧩 Steps for group projects and branching workflow.

1️⃣ **Open the terminal** inside your local project folder.  
(Make sure you are in the root folder that you´re working, example: `FindPropertiesApp`)

---

2️⃣ **Update your local `main` branch** to get the latest version from the remote repository:
```bash
git checkout main
git pull origin main
```

---

3️⃣ **Create a new temporary branch** from `main` (for your specific task):
```bash
git checkout -b task2-FindPropertiesApp
```
🔹 This creates a new branch called `task2-FindPropertiesApp` and automatically switches to it.  
🔹 You’ll work on this branch without modifying the main branch.

---

4️⃣ **Add all your changes (structure, files, mockups, etc.)**
```bash
git add .
```

---

5️⃣ **Commit your changes with a clear message**
```bash
git commit -m "Implement full project structure with controllers, entities, utils and strings"
```

---

6️⃣ **Push your branch to the remote repository**
```bash
git push origin task2-FindPropertiesApp
```
🔹 This uploads the temporary branch to GitHub.  
🔹 It won’t affect the `main` branch yet (that one stays clean).

---

7️⃣ **Create the Pull Request (PR) from GitHub**

Go to your repository:  
👉 https://github.com/LoesssLR/FindPropertiesApp

GitHub will show a message like:  
**“Compare & pull request”** — click on it.

In the PR title, write exactly:  
```
task2-FindPropertiesApp
```

In the description, briefly explain what you added:  
```
Added project structure (Entities, Data, Controllers, Utils, Mockups)
```

Assign the  **Reviewer**:  
```

Select the **main** branch as the base and create the PR ✅

---

After the PR is merged into `main`, update your local repository:
```bash
git checkout main
git pull origin main
```

This ensures your main branch is synchronized with the latest version.

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

### Basic Information.
```bash
git --version                 # Show installed Git version
git help <command>            # Show help for a specific command
```

### Daily development.
```bash
git status                    # Show status of changes
git add <file>                # Stage changes
git add .                     # Stage all changes
git commit -m "msg"           # Commit staged changes with message
git commit --amend            # Modify or replace the last commit
```

### Branch management.
```bash
git branch                    # Show branches
git branch <branch-name>      # Create a new branch
git branch -M <branch-name>   # Rename/move branch
git checkout <branch-name>    # Switch to an existing branch
git checkout -b <branch-name> # Create and switch to a new branch
git switch <branch-name>      # Switch to a branch
git branch -d <branch-name>   # Delete a branch
```

### Integration and collaboration.
```bash
git remote add origin <url>        # Link local repo to remote
git remote set-url origin <url>    # Change URL of the remote repository
git push -u origin <branch>        # Push changes to remote and set upstream
git push                           # Push commits
git pull origin <branch>           # Fetch and merge from remote branch
git clone --branch <branch> <url>  # Clone a remote repo on a specific branch
git merge <branch>                 # Merge a branch into current
git fetch                          # Fetch changes without merging
```

### Checking history.
```bash
git log                       # Show commit history
git show <hash>               # Show details of a commit
git diff <a> <b>              # Compare two commits, branches or files
```

### Recovery and cleanup.
```bash
git checkout -- <file>        # Undo local changes in a file
git reset --soft origin/<br>  # Soft reset (keep changes)
git reset --hard origin/<br>  # Hard reset (discard changes)
git reset --hard HEAD         # Discard all local changes
git revert <commit-hash>      # Revert a commit
```

### Stashing.
```bash
git stash                     # Save temporary changes
git stash pop                 # Restore and delete stash
git stash apply               # Restore stash but keep it saved
git stash list                # Show all stashes
```

### Cherry-pick.
```bash
git cherry-pick <hash>        # Apply a commit from another branch
git cherry-pick --abort       # Abort cherry-pick
git cherry-pick --continue    # Continue after conflict resolution
git cherry-pick --skip        # Skip current commit in sequence
```

### Tag Management.

#### 📘 What are Tags and what are they for?

**Tags** are labels that identify specific points in the Git history — commonly used to mark **releases, milestones, or stable versions** of a project.  
They are not branches; rather, they act as permanent reference points to commits, often representing versions like `v1.0`, `v2.3.5`, etc.

```bash
git tag <tag> -m "<message>"         # Create a new tag
git tag                              # List all tags
git tag -d <tag>                     # Delete a specific tag
git tag -a <tag> <commit> -m "<msg>" # Create a tag on a previous commit
git show <tag>                       # Show information about a specific tag
```

---

### Advanced and utilities.
```bash
git rebase <base>              # Reapply commits on top of another base
```

---

## 📘 Learning Outcomes.

- Complete workflow with Git and GitHub.  
- Managing individual and group repositories.  
- Collaboration strategies with branches and Pull Requests.  
- Remote repository reconfiguration.  
- Consolidation of multiple projects into a single repository.  
- Recovery, stashing and cherry-picking strategies.
- Example of complete workflow used by companies.

---

## 📜 License.

This repository was created for **educational** and **personal documentation** purposes.
