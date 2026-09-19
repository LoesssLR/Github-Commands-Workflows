# GitHub Commands & Workflows

This repository contains a structured collection of **commands and workflows for Git and GitHub**, organized by practical scenarios and real-world examples, including team collaboration, CI/CD and conflict resolution.

## Table of Contents

- [Academic Information](#academic-information)
- [Basic Workflows](#basic-workflows)
  - [First-time upload: from local folder to GitHub](#first-time-upload-from-local-folder-to-github)
  - [Upload changes to GitHub (VS Code terminal example)](#upload-changes-to-github-vs-code-terminal-example)
  - [When the remote repository is already configured](#when-the-remote-repository-is-already-configured)
  - [Download updates from others](#download-updates-from-others)
  - [Change the remote repository](#change-the-remote-repository)
- [Git Workflow for Collaborative Projects](#git-workflow-for-collaborative-projects)
  - [Scenario 1: Working directly with `main` and task branches](#scenario-1-working-directly-with-main-and-task-branches)
  - [Scenario 2: Base branch (`dev-team1`) and personal branch (`devLuisAle`) plus conflict resolution](#scenario-2-base-branch-dev-team1-and-personal-branch-devluisale-plus-conflict-resolution)
- [Real Business Workflow](#real-business-workflow)
- [Useful Additional Commands](#useful-additional-commands)
  - [Basic Information](#basic-information)
  - [Daily Development](#daily-development)
  - [Branch Management](#branch-management)
  - [Integration and Collaboration](#integration-and-collaboration)
  - [Checking History](#checking-history)
  - [Recovery and Cleanup](#recovery-and-cleanup)
  - [Stashing](#stashing)
  - [Cherry-pick](#cherry-pick)
  - [Tag Management](#tag-management)
  - [Advanced and Utilities](#advanced-and-utilities)
- [Extra Topics](#extra-topics)
  - [.gitignore](#gitignore)
  - [HTTPS vs SSH](#https-vs-ssh)
  - [Conventional Commits](#conventional-commits)
  - [Resolving Merge Conflicts from the Terminal](#resolving-merge-conflicts-from-the-terminal)
  - [GitHub Actions (CI/CD)](#github-actions-cicd)
- [Security Practices in Git and GitHub](#security-practices-in-git-and-github)
- [Learning Outcomes](#learning-outcomes)
- [Purpose](#purpose)

## Academic Information

- **University**: Universidad Técnica Nacional
- **Campus**: Pacífico
- **Major**: Information Technology Engineering
- **Author**: Luis Alejandro López Reyes

## Basic Workflows

### First-time upload: from local folder to GitHub

Steps to upload a local project to a new GitHub repository using CMD/PowerShell:

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

### Upload changes to GitHub (VS Code terminal example)

```bash
# Verify that we are inside the folder:
ls

# Verify current branch:
git branch

# Add changes:
git add .

# Add the remote (not necessary if already linked):
git remote add origin https://github.com/xxx/xxx.git

# Set the main branch (not necessary if already on the correct branch):
git branch -m main

# Commit:
git commit -m "Update"

# Push changes:
git push -u origin main
```

### When the remote repository is already configured

```bash
git add .
git commit -m "Update"
git push
```

### Download updates from others

```bash
# If the repository is already correctly configured:
git pull

# To specify a branch (for example, the main branch):
git pull origin main
```

### Change the remote repository

Useful if you linked the wrong remote or need to migrate to a new URL:

```bash
git remote -v
git remote remove origin
git remote add origin https://github.com/xxx/xxx.git
git remote -v
# The remote URL should now be updated.
```

## Git Workflow for Collaborative Projects

Two common scenarios in team projects:

1. Working directly from `main` with task branches
2. Working with a shared team branch (`dev-team1`) and a personal temporary branch (`devLuisAle`)

### Scenario 1: Working directly with `main` and task branches

#### 1. Clean up references to deleted remote branches

```bash
git fetch -p
```

#### 2. Switch to `main` and update it

```bash
git switch main
git pull origin main
```

#### 3. List local branches

```bash
git branch
```

#### 4. Delete the previous task branch

```bash
git branch -d <branch>
git branch -D <branch>  # forced deletion
```

#### 5. Create a new task branch

```bash
git checkout -b task6-LuisLopez-FindPropertiesApp
```

#### 6. Stage changes and commit

```bash
git add .
git commit -m "Clear description of the changes"
```

#### 7. Push the branch

```bash
git push -u origin task6-LuisLopez-FindPropertiesApp
```

#### 8. Create a Pull Request on GitHub

- **Base:** `main`
- **Compare:** your task branch

### Scenario 2: Base branch (`dev-team1`) and personal branch (`devLuisAle`) plus conflict resolution

#### Branches involved

- **Base branch (references `main`):** `dev-team1`
- **Temporary branch (created on GitHub before cloning):** `devLuisAle`

#### 1. Clone the project

```bash
git clone <URL>
cd project
```

#### 2. Inside the project terminal

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

#### Important note

Always **pull before pushing**, so you get the latest changes from `dev-team1` if any exist. This ensures your **push + PR** will be conflict-free.

#### When you are already working on the branch (`devLuisAle`)

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

#### Resolve merge conflicts (if any)

When a conflict appears, you will see three sections:

- **Left (devLuisAle)** → your local version (your changes)
- **Center (Result)** → the final merged output you will save
- **Right (origin/dev-team1)** → the team's latest remote version

After fixing conflicts, stage your fixes:

```bash
git add .
```

Or add a specific file:

```bash
git add FILE
```

Commit the merge resolution:

```bash
git commit -m "Resolve conflicts and merge dev-team1 into devLuisAle"
```

#### Push your temporary branch

```bash
git push -u origin devLuisAle
```

#### Create your Pull Request

- **Base:** `dev-team1`
- **Compare:** `devLuisAle`

#### Summary

| Scenario | Base Branch | Working Branch | Purpose |
|----------|-------------|----------------|---------|
| **1** | `main` | `taskX-user` | Direct tasks merged into main |
| **2** | `dev-team1` | `devUser` | Team workflow with frequent integration |

## Real Business Workflow

In a real business environment, several branches are created that work like folders or a large directory. Typically, a branch is created for each environment or section of the company (`PRODUCTION`, `QA`, `DEV`, etc.).

### How it works

- **Branching:** Developers take the latest version of `DEV` and create a copy. This becomes a temporary branch (usually named after the requirement) where they will work.
- **Committing:** Developers make commits on this branch (each with an associated ID, linked to user stories), continuing this process until the requirement is completed.
- **Pull Requests:** Before pushing changes to `DEV`, they must be reviewed to ensure they work correctly and meet the assigned requirement. A Pull Request is created to review the code before integrating it into `DEV`, where it will either be approved or rejected.
- **CI/CD & Deployment to DEV:** Once requirements are approved and merged into `DEV`, a CI/CD pipeline runs all unit tests defined in a YAML file. If tests pass, the changes are deployed to the WEB DEV server. If not, they must be fixed.
- **QA Testing:** The QA team tests each requirement by using `git cherry-pick <commit_id>` from the WEB DEV server in an isolated branch. They test the delivered code against the acceptance criteria to see if it works or produces errors.
- **Production:** If the code passes the tests, it is integrated into `PRODUCTION`. A QA team member verifies the production environment to ensure everything functions correctly. If it fails QA, the developer is notified to fix issues and repeat the process.

> **Note:** Because of this workflow, it is essential to clearly and correctly write the requirements and acceptance criteria. If a requirement is poorly written or ambiguous, it could cause problems—even in production.

The workflow looks like this:

### Step by step with commands

#### 1. Developer creates a feature branch from DEV

```bash
git checkout dev
git pull origin dev
git checkout -b feature/login
```

#### 2. Developer makes changes and commits

```bash
git status
git add .
git commit -m "feat: add login screen with validation"
```

#### 3. Push branch and create Pull Request

```bash
git push -u origin feature/login
```

#### 4. Pull Request is reviewed and merged into DEV

The approver reviews the code and either approves or rejects the changes.

#### 5. CI/CD deploys to DEV environment automatically

The pipeline runs the unit tests defined in the YAML file. If they pass, the changes are deployed to the DEV server.

#### 6. QA tests with cherry-pick on QA branch

```bash
git checkout qa
git pull origin qa
git cherry-pick <commit_id>
```

#### 7. If approved, changes are deployed to PROD

```bash
git checkout main
git pull origin main
git cherry-pick <commit_id>
git push origin main
```

### Workflow summary

1. **Developer** → feature branch → commits → Pull Request
2. **Approver** → reviews and approves/rejects
3. **DEV branch + CI/CD** → automated tests and deploy to DEV
4. **QA branch + Cherry-pick** → isolated testing
5. **Main/Master branch** → final deploy to Production

## Useful Additional Commands

### Basic Information

```bash
git --version                 # Show installed Git version
git help <command>            # Show help for a specific command
```

### Daily Development

```bash
git status                    # Show status of changes
git add <file>                # Stage changes
git add .                     # Stage all changes
git commit -m "msg"           # Commit staged changes with message
git commit --amend            # Modify or replace the last commit
```

### Branch Management

```bash
git branch                    # Show branches
git branch <branch-name>      # Create a new branch
git branch -M <branch-name>   # Rename/move branch
git checkout <branch-name>    # Switch to an existing branch
git checkout -b <branch-name> # Create and switch to a new branch
git switch <branch-name>      # Switch to a branch
git switch -c <branch-name>   # Create and switch to a new branch
git branch -d <branch-name>   # Delete a branch
```

### Integration and Collaboration

```bash
git remote add origin <url>        # Link local repo to remote
git remote set-url origin <url>    # Change URL of the remote repository
git push -u origin <branch>        # Push changes to remote and set upstream
git push                           # Push commits
git pull origin <branch>           # Fetch and merge from remote branch
git clone --branch <branch> <url>  # Clone a remote repo on a specific branch
git merge <branch>                 # Merge a branch into current
git fetch                          # Fetch changes without merging
git fetch --prune                  # Remove references to deleted remote branches
```

### Checking History

```bash
git log                           # Show commit history
git log --oneline --graph --all   # Compact history with branch graph
git show <hash>                   # Show details of a commit
git diff <a> <b>                  # Compare two commits, branches or files
git blame <file>                  # Show who last changed each line of a file
```

### Recovery and Cleanup

```bash
git checkout -- <file>             # Undo local changes in a file (classic)
git restore <file>                 # Undo local changes in a file (modern alternative)
git restore --staged <file>        # Unstage a file, keeping the working directory changes
git reset --soft origin/<branch>   # Soft reset (keep changes)
git reset --hard origin/<branch>   # Hard reset (discard changes)
git reset --hard HEAD              # Discard all local changes
git revert <commit-hash>           # Revert a commit, creating a new one
git reflog                         # Show history of HEAD movements (recover lost commits)
git merge --abort                  # Abort a merge that has conflicts
```

### Stashing

```bash
git stash                     # Save temporary changes
git stash pop                 # Restore and delete stash
git stash apply               # Restore stash but keep it saved
git stash list                # Show all stashes
```

### Cherry-pick

```bash
git cherry-pick <hash>        # Apply a commit from another branch
git cherry-pick --abort       # Abort cherry-pick
git cherry-pick --continue    # Continue after conflict resolution
git cherry-pick --skip        # Skip current commit in sequence
```

### Tag Management

**Tags** are labels that identify specific points in the Git history — commonly used to mark **releases, milestones, or stable versions** of a project. They are not branches; rather, they act as permanent reference points to commits, often representing versions like `v1.0`, `v2.3.5`, etc.

```bash
git tag <tag> -m "<message>"         # Create a new annotated tag
git tag                              # List all tags
git tag -d <tag>                     # Delete a specific tag
git tag -a <tag> <commit> -m "<msg>" # Create a tag on a previous commit
git show <tag>                       # Show information about a specific tag
git push origin <tag>                # Push a specific tag to the remote
git push origin --tags               # Push all tags to the remote
```

### Advanced and Utilities

```bash
git rebase <base>              # Reapply commits on top of another base
git rebase -i HEAD~<n>         # Interactively rewrite the last n commits
```

## Extra Topics

### .gitignore

A `.gitignore` file (placed at the root of the repository) tells Git which files or folders to exclude from version control, such as dependencies, secrets or build output.

Example:

```gitignore
# Dependencies
node_modules/

# Environment and secrets
.env

# Build output
dist/
build/

# Logs
*.log
```

> **Note:** If a file is already tracked, adding it to `.gitignore` has no effect. Remove it from the index first with `git rm --cached <file>`.

### HTTPS vs SSH

```bash
# HTTPS (works anywhere, no extra setup)
git clone https://github.com/user/repo.git

# SSH (requires an SSH key configured on GitHub)
git clone git@github.com:user/repo.git
```

- **HTTPS:** Works out of the box, but since 2021 GitHub asks for a **Personal Access Token (PAT)** instead of your password.
- **SSH:** Requires generating a key (`ssh-keygen`) and adding the public key to GitHub, but afterwards you never enter credentials again.

### Conventional Commits

A commit message convention that makes history readable and enables automatic changelogs and versioning:

```
<type>(<scope>): <description>

feat: add login screen
fix: correct email validation error
docs: update README
refactor: simplify auth service
test: add unit tests for login
chore: update dependencies
```

Common types: `feat` (new feature), `fix` (bug fix), `docs`, `style`, `refactor`, `test`, `chore`.

### Resolving Merge Conflicts from the Terminal

When a `git pull` or `git merge` produces conflicts, `git status` shows the affected files as `both modified`. Open each file and find the sections delimited by the conflict markers:

| Marker | Meaning |
|--------|---------|
| `<<<<<<< HEAD` | Start of your local version |
| `=======` | Separator between both versions |
| `>>>>>>> branch-name` | Start of the incoming version from the other branch |

Keep the code you want (or a combination of both), remove the markers, then:

```bash
git add <file>
git commit -m "Resolve conflicts"
```

To cancel the merge and go back to the previous state:

```bash
git merge --abort
```

### GitHub Actions (CI/CD)

GitHub Actions automates tasks when events happen in the repository (push, pull request, etc.). Workflows are YAML files inside `.github/workflows/`.

Example `.github/workflows/ci.yml` that runs the tests on every push or pull request:

```yaml
name: CI

on:
  push:
    branches: [main, dev]
  pull_request:
    branches: [main]

jobs:
  test:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - uses: actions/setup-node@v4
        with:
          node-version: 20
      - run: npm ci
      - run: npm test
```

- **`on`:** events that trigger the workflow
- **`jobs`:** units of work that run in parallel or sequentially
- **`steps`:** individual commands or reusable actions

## Security Practices in Git and GitHub

Best practices to keep repositories, pipelines and credentials secure — essential knowledge in Blue Team, SOC and Cloud Defense roles.

### Branch protection rules

Enable them in **Settings → Branches** for the main branches:

- Require Pull Request reviews before merging
- Require status checks (CI/tests) to pass
- Block force pushes and branch deletion
- Require conversation resolution

### Signed commits (GPG or SSH)

Signed commits prove that the author is who they claim to be. GitHub shows a **Verified** badge on the commit.

```bash
# Generate a GPG key
gpg --full-generate-key

# Or use SSH signing with an existing SSH key
git config --global user.signingkey <key>
git config --global commit.gpgsign true
```

### Secret scanning and push protection

- Enable **Secret scanning** and **Push protection** in the repository security settings.
- Never commit `.env`, tokens or credentials; use `.gitignore` and environment variables.
- Scan locally before committing with tools like [gitleaks](https://github.com/gitleaks/gitleaks) or [trufflehog](https://github.com/trufflesecurity/trufflehog).

```bash
# Detect secrets in the working copy
gitleaks detect --source .
```

### Code scanning with CodeQL

GitHub CodeQL analyzes the code on every push or PR and reports vulnerabilities as security alerts.

Example `.github/workflows/codeql.yml`:

```yaml
name: CodeQL

on:
  push:
    branches: [main]
  pull_request:
    branches: [main]

permissions:
  security-events: write

jobs:
  analyze:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - uses: github/codeql-action/init@v3
      - uses: github/codeql-action/autobuild@v3
      - uses: github/codeql-action/analyze@v3
```

### Dependabot alerts and updates

Dependabot monitors dependencies and opens Pull Requests to update vulnerable versions.

Example `.github/dependabot.yml`:

```yaml
version: 2
updates:
  - package-ecosystem: "npm"
    directory: "/"
    schedule:
      interval: "weekly"
```

### Secrets in GitHub Actions

- Store credentials in **Settings → Secrets and variables → Actions**, never hardcode them.
- Reference them in workflows as `${{ secrets.MY_TOKEN }}`.
- Grant each workflow the minimum required permissions with the `permissions:` key.
- Pin third-party actions by full commit SHA (e.g. `actions/checkout@<full-sha>`) instead of tags.
- In cloud environments, prefer **OIDC** to authenticate (e.g. Azure or AWS) without long-lived credentials.

### Rotating exposed credentials

If a secret gets committed, removing it from history is not enough — rotate it immediately:

```bash
# Remove the file from the index but keep it locally
git rm --cached .env
```

Then revoke/rotate the credential in the provider and enable push protection to prevent it from happening again.

## Learning Outcomes

- Complete workflow with Git and GitHub
- Managing individual and group repositories
- Collaboration strategies with branches and Pull Requests
- Remote repository reconfiguration
- Consolidation of multiple projects into a single repository
- Recovery, stashing and cherry-picking strategies
- Merge conflict resolution strategies
- CI/CD automation with GitHub Actions
- Security practices in Git and GitHub (secret management, code scanning, signed commits)
- Example of a complete workflow used by companies

## Purpose

This repository was created for **educational** and **personal documentation** purposes.
