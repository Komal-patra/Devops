# 🚀 GIT for DevOps

## 📌 Introduction
GIT stands for **Global Information Tracker** and is also known as a **Version Control System (VCS)** or **Source Code Management (SCM)** tool.

### 🔥 Features:
- **Platform Independent**
- **Free & Open Source**
- **Source Code Management** (Tracks multiple versions of files)
- **3rd Generation of VCS**
- **Developed using C programming language**

## 🔹 Why Use VCS?
✅ **Backup & Restore**
✅ **Collaboration**
✅ **Branching & Merging**
✅ **Tracking Changes**

Version Control Systems (VCS) help in managing changes to source code, enabling multiple developers to collaborate efficiently.

---
## 📌 Types of Version Control Systems
### 1️⃣ **Local Version Control System (LVCS)**
- Entire code is stored on the local machine.
- If the local computer crashes, code is lost.
- **Examples**: SCCS, RCS

### 2️⃣ **Centralized Version Control System (CVCS)**
- The source code is stored on a central server.
- If the central repository crashes, the entire codebase is lost.
- Requires network access.

### 3️⃣ **Distributed Version Control System (DVCS)**
- Code is stored both locally and in a central repository.
- **Local repo:** GIT, **Central repo:** GITHUB
- Workflow: **ACP (Add → Commit → Push)**

---
## 📌 Stages in Git
1️⃣ **Working Directory** → Where we write the source code.
2️⃣ **Staging Area** → Where changes are tracked.
3️⃣ **Repository** → Where tracked code is stored.
4️⃣ **Remote Repository** → Stores code in a remote location (GitHub, GitLab, Bitbucket).

---
## 🛠 Installing Git on AWS EC2 Instance
```sh
yum install git -y
```
### ✅ Verify Installation
```sh
git --version
```

---
## 📌 Essential Git Commands
### 🔍 Checking Status
```sh
git status
```

### 🔨 Initializing Git Repository
```sh
git init
```

### 📂 Viewing Hidden Files
```sh
ls -al
```

### 📌 Adding Files to Staging Area
```sh
git add filename
# OR
git add .  # Stages all files
```

### 📝 Committing Files
```sh
git commit -m "Your commit message"
```

### 🔧 Configuring Git User Details
```sh
git config --global user.name "Your Name"
git config --global user.email "your.email@example.com"
```

### 📜 Viewing Commit Logs
```sh
git log
```
#### View Last N Commits in One Line
```sh
git log --oneline -n
```

### 🔄 Checking Differences
```sh
git diff
```

---
## 🔄 Restoring & Resetting
### ✅ Restore Before Commit
```sh
git restore filename
```

### ❌ Uncommit Changes
```sh
git reset --soft HEAD^  # Keeps changes

git reset --hard HEAD^  # Discards changes
```

---
## 📌 Git Stash
If you need to temporarily save your work and switch to another task:
```sh
git stash
```

Retrieve the stashed changes:
```sh
git stash apply
```

---
## 🌍 GitHub Integration
### 🔗 Connecting Local Repository to GitHub
```sh
git remote add origin https://github.com/username/repository.git
```

### 🚀 Pushing Code to GitHub
```sh
git push -u origin master
```

### 📥 Pulling Code from Remote Repo
```sh
git pull
```

---
## 📌 Git Branching
### 📜 Viewing Branches
```sh
git branch
```

### ➕ Creating a New Branch
```sh
git branch branch_name
```

### 🔄 Switching Branches
```sh
git checkout branch_name
```

### 🔗 Merging Branches
```sh
git merge branch_name
```

### 🔙 Reverting a Merge
```sh
git revert branch_name  # Recommended
# OR

git rebase branch_name  # Rewrites commit history (Not Recommended)
```

---
## ⚡ Additional Commands
### 🚫 Avoid Entering Password Every Time
```sh
git config --global credential.helper cache
```

---
## 🎯 Conclusion
This **Git Cheat Sheet** provides all essential commands for DevOps and software development workflows. Mastering Git helps in **collaboration, version control, and efficient code management!** 🚀
