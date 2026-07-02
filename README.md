# GitHub Commands & Workflows.

This repository contains a structured collection of **commands and workflows for Git and GitHub**, organized by practical scenarios and real examples.  

---

## Academic Information.

- **University**: Universidad Técnica Nacional.  
- **Campus**: Pacífico.  
- **Major**: Information Technology Engineering.  
- **Author**: Luis Alejandro López Reyes.  

---

## Scenarios & Commands.

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

# Git Workflow for Collaborative Projects (From terminal).

This document explains two common workflow scenarios in team projects:  
1) Working directly from `main` with task branches.  
2) Working with a shared team branch (`dev-team1`) and a personal temporary branch (`devLuisAle`).

---

## Scenario 1: Working directly with `main` and task branches.

### 1. Clean up references to deleted remote branches.
```bash
git fetch -p
```

### 2. Switch to `main` and update it.
```bash
git switch main
git pull origin main
```

### 3. List local branches.
```bash
git branch
```

### 4. Delete the previous task branch.
```bash
git branch -d <branch>
git branch -D <branch>  # forced deletion
```

### 5. Create a new task branch.
```bash
git checkout -b task6-LuisLopez-FindPropertiesApp
```

### 6. Stage changes and commit.
```bash
git add .
git commit -m "Clear description of the changes"
```

### 7. Push the branch.
```bash
git push -u origin task6-LuisLopez-FindPropertiesApp
```

### 8. Create a Pull Request on GitHub.
Base: `main`  
Compare: your task branch

---

# Scenario 2: Working with a base branch (`dev-team1`) and a temporary personal branch (`devLuisAle`) + conflict resolution

## Branches involved
- **Base branch (references `main`):** `dev-team1`  
- **Temporary branch (created on GitHub before cloning):** `devLuisAle`

---

## 1. Clone the project
```bash
git clone <URL>
cd project
```

---

## 2. Inside the project terminal
List your branches:
```bash
git branch
```

Pull updates from the remote:
```bash
git pull
```

Switch to your personal temporary branch:
```bash
git switch devLuisAle
```

---

## Important Note  
Always **pull before pushing**, so you get the latest changes from `dev-team1` if any exist.  
This ensures your **push + PR** will be conflict-free.

---

## When you are already working on the branch (`devLuisAle`)

Check branches:
```bash
git branch
```

Check file status:
```bash
git status
```

Stage your changes:
```bash
git add .
```

Commit:
```bash
git commit -m "Your commit message"
```

Pull the latest changes from the team base branch:
```bash
git pull origin dev-team1
```

---

## Resolve merge conflicts (if any)

When a conflict appears, you will see three sections:

- **Left (devLuisAle)** → your local version (your changes)  
- **Center (Result)** → the final merged output you will save  
- **Right (origin/dev-team1)** → the team’s latest remote version  

After fixing conflicts, stage your fixes:
```bash
git add .
```
or add a specific file:
```bash
git add FILE
```

Commit the merge resolution:
```bash
git commit -m "Resolve conflicts and merge dev-team1 into devLuisAle"
```

---

## Push your temporary branch
```bash
git push -u devLuisAle
```

---

## Create your Pull Request
- **Base:** `dev-team1`  
- **Compare:** `devLuisAle`

---

## Summary

| Scenario | Base Branch | Working Branch | Purpose |
|----------|-------------|----------------|----------|
| **1** | `main` | `taskX-user` | Direct tasks merged into main |
| **2** | `dev-team1` | `devUser` | Team workflow with frequent integration |

---

## Change the remote repository (useful if you linked the wrong remote or need to switch).

```bash
git remote -v
git remote remove origin
git remote add origin https://github.com/xxx/xxx.git
git remote -v
# The remote URL should now be updated.
```

---

## Example of Real Business Workflow with Git.

In a real business environment, several branches are created that work like folders or a large directory. Typically, a branch is created for each environment or section of the company (`PRODUCTION`, `QA`, `DEV`, etc.).

**Workflow Steps:**
- **Branching:** Developers take the latest version of `DEV` and create a copy. This becomes a temporary branch (usually named after the requirement) where they will work.
- **Committing:** Developers make commits on this branch (each with an associated ID, linked to user stories), continuing this process until the requirement is completed.
- **Pull Requests:** Before pushing changes to `DEV`, they must be reviewed to ensure they work correctly and meet the assigned requirement. A Pull Request is created to review the code before integrating it into `DEV`, where it will either be approved or rejected.
- **CI/CD & Deployment to DEV:** Once requirements are approved and merged into `DEV`, a CI/CD pipeline runs all unit tests defined in a YAML file. If tests pass, the changes are deployed to the WEB DEV server. If not, they must be fixed.
- **QA Testing:** The QA team tests each requirement by using `git cherry-pick <commit_id>` from the WEB DEV server in an isolated branch. They test the delivered code against the acceptance criteria to see if it works or produces errors.
- **Production:** If the code passes the tests, it is integrated into `PRODUCTION`. A QA team member verifies the production environment to ensure everything functions correctly. If it fails QA, the developer is notified to fix issues and repeat the process.

> **Note:** Because of this workflow, it is essential to clearly and correctly write the requirements and acceptance criteria. If a requirement is poorly written or ambiguous, it could cause problems—even in production.

The workflow looks like this:

### Step by Step with Commands.

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

### Summary of Workflow.

1. **Developer** → feature branch → commits → Pull Request.  
2. **Approver** → reviews and approves/rejects.  
3. **DEV branch + CI/CD** → automated tests and deploy to DEV.  
4. **QA branch + Cherry-pick** → isolated testing.  
5. **Main/Master branch** → final deploy to Production.  

---

## Useful Additional Commands.

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

#### What are Tags and what are they for?

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

## Learning Outcomes.

- Complete workflow with Git and GitHub.  
- Managing individual and group repositories.  
- Collaboration strategies with branches and Pull Requests.  
- Remote repository reconfiguration.  
- Consolidation of multiple projects into a single repository.  
- Recovery, stashing and cherry-picking strategies.
- Example of complete workflow used by companies.

---

## License.

This repository was created for **educational** and **personal documentation** purposes.
