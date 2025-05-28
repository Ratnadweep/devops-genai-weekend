# 🚀 DevOps Project Setup with Git and GitHub

This document explains how I, as a DevOps Engineer, set up and collaborated on a project using Git and GitHub.

---

## 🧑‍💻 Developer Setup

1. **Create a GitHub Account**

   * Email: `ratnadweepghosh@gmail.com`
   * Username: `Ratnadweep`
   * Full Name: `Ratnadweep Ghosh`

2. **Configure Git on Local System**

   ```bash
   git config --global user.email "ratnadweepghosh@gmail.com"
   git config --global user.name "Ratnadweep Ghosh"
   ```

---

## 🔐 SSH Key Authentication

To securely connect GitHub with your local Git client:

1. **Generate SSH Key**

   ```bash
   ssh-keygen -t ed25519 -C "ratnadweepghosh@gmail.com"
   ```

2. **Key Storage Location (Windows)**

   ```
   /c/Users/ratna/.ssh/
   ```

   * `id_ed25519` → Private Key (keep it safe, never share)
   * `id_ed25519.pub` → Public Key (to be uploaded to GitHub)

3. **Add Public Key to GitHub**

   * Go to: `github.com/settings/keys`
   * Click **New SSH Key**
   * Add a title and paste your public key

---

## 🏗️ Project Repository Setup (Example: XYZ Project)

1. **Create GitHub Repository** (Private, named "XYZ")

   * Under organization or user account
   * Add developers/testers as **collaborators** via:

     ```
     https://github.com/Ratnadweep/XYZ/settings/access
     ```

2. **Initialize Local Git Repository**

   ```bash
   git init
   git remote add origin git@github.com:Ratnadweep/XYZ.git
   ```

   > You can also set an alias if needed for the remote URL.

3. **Add Files and Push to GitHub**

   ```bash
   git add .
   git commit -m "Initial commit"
   git push -u origin master
   ```

   > 🔹 `-u` sets the **upstream branch** so future `git push` will default to `origin master`.
   > 🔹 Run with `-u` **only the first time** after connecting the remote.

---

## 👥 Git Collaboration Workflow

### Contributor Steps:

1. **Clone the Repository**

   ```bash
   git clone git@github.com:Ratnadweep/XYZ.git
   ```

2. **Create and Switch to a Side Branch**

   ```bash
   git checkout -b sb1
   ```

3. **Make Code Changes and Push**

   ```bash
   git add .
   git commit -m "Feature implemented"
   git push origin sb1
   ```

4. **Open Pull Request**

   * Go to GitHub
   * Click **Compare & Pull Request**
   * Assign a reviewer
   * Reviewer approves and merges into `master`

---

## 🔁 Important Tip: Always Sync Before Starting New Work

Before beginning any new work:

```bash
git checkout master
git pull origin master
git checkout -b new-feature-branch
```

---

### 📌 Summary

This Git + GitHub workflow ensures:

* Clean collaboration across teams
* Minimal merge conflicts
* Centralized and traceable version control

---

