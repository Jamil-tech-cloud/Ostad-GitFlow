# GitFlow Practice — Commands Reference

This document records every Git command executed for **Task 1** (Repository Initialization) and **Task 2** (Branching Workflow).

---

## Task 1: Repository Initialization

Create the project directory, initialize a Git repository on `main`, and create the additional starter branches.

```bash
# Create project folder and enter it
mkdir -p "C:/Ostad DevOps/GitFlowPractice"
cd "C:/Ostad DevOps/GitFlowPractice"

# Initialize repo with main as the default branch
git init -b main

# Create an initial commit (branches cannot be created from an empty repo)
echo "# GitFlowPractice" > README.md
git add README.md
git commit -m "Initial commit on main"

# Create the develop and feature/login branches
git branch develop
git branch feature/login

# Verify branches
git branch --list
```

**Result:** branches `main`, `develop`, `feature/login`.

---

## Task 2: Branching Workflow

### 2.1 Create feature and bugfix branches off `develop`

```bash
git checkout develop
git branch feature/payment
git branch feature/profile
git branch bugfix/login-error
git branch --list
```

### 2.2 Add a commit to each new branch

```bash
# feature/payment
git checkout feature/payment
echo "payment module v1" > payment.txt
git add payment.txt
git commit -m "feat(payment): add initial payment module"

# feature/profile
git checkout feature/profile
echo "profile module v1" > profile.txt
git add profile.txt
git commit -m "feat(profile): add initial profile module"

# bugfix/login-error
git checkout bugfix/login-error
echo "fix: login validation" > login-fix.txt
git add login-fix.txt
git commit -m "fix(login): correct login validation error"
```

### 2.3 Integration #1 — Merge strategy (`feature/payment` → `develop`)

`--no-ff` forces a merge commit so the branch topology stays visible.

```bash
git checkout develop
git merge --no-ff feature/payment -m "Merge feature/payment into develop (merge strategy)"

# Inspect history
git log --oneline --graph --all -n 10
```

### 2.4 Integration #2 — Rebase strategy (`feature/profile` → `develop`)

Rebase replays the feature commits on top of `develop`, then a fast-forward merge keeps history linear.

```bash
git checkout feature/profile
git rebase develop

git checkout develop
git merge --ff-only feature/profile

# Inspect history
git log --oneline --graph --all -n 15
```

---

## Push everything to GitHub

```bash
git remote add origin https://github.com/Jamil-tech-cloud/Ostad-GitFlow.git
git remote -v
git push -u origin --all
```

All six branches (`main`, `develop`, `feature/login`, `feature/payment`, `feature/profile`, `bugfix/login-error`) are now tracked against `origin`.
