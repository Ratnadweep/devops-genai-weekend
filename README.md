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

## 🔀 Conflict Management & Resolution in Git

When working in a collaborative environment, merge conflicts are common. Here are two effective approaches to resolve them:

---

### ✅ Approach 1: Using `git rebase`

**Use Case**:
When multiple developers create feature branches from the same base code (say version `v1`), and one branch is merged into `master` before the others, the remaining branches may face merge conflicts due to overlapping changes.

#### 👇 Scenario:

* **Dev1** and **Dev2** both pull the same base code `v1` from `master`.
* They create their own branches:

  * Dev1 → `x1`
  * Dev2 → `y1`
* Each developer makes changes:

  * Dev1 → changes `dx`
  * Dev2 → changes `dy`
* Both commit and push:

  ```bash
  git add .
  git commit -m "Dev changes"
  git push origin x1  # for Dev1
  git push origin y1  # for Dev2
  ```

#### 🧩 Conflict:

* Dev2's PR gets merged into `master` first.
* Dev1’s PR now shows a merge conflict.

#### 🔧 Steps to Rebase and Resolve Conflict (for Dev1):

```bash
# 1. Switch to master
git checkout master

# 2. Pull the latest code from GitHub (now contains dy)
git pull

# 3. Switch back to your feature branch
git checkout x1

# 4. Rebase your branch on top of the updated master
git rebase master
```

* If conflicts occur, manually resolve them by editing the conflicting files.
* Once resolved:

```bash
# 5. Stage the resolved files
git add .

# 6. Continue the rebase
git rebase --continue
```

🔎 The above step may open a `vim` editor — it’s used to edit the commit message or confirm the rebase. You can simply press:

```
Esc :wq! Enter
```

```bash
# 7. Push your updated branch forcefully (as rebase rewrites history)
git push origin x1 -f
```

🎯 Now go to GitHub, create the PR from `x1`, and merge.

---

### ✅ Approach 2: Using `git stash`

**Use Case**:
When your working branch has local changes, but you realize that another developer has already updated `master` and you want to first pull those changes **without losing your local work**.

#### 👇 Scenario:

* Dev1 and Dev2 both pull `v1`, then create branches `x1` and `y1`.
* Dev2 completes work (`dy`) and merges `y1` into `master`.
* Dev1 is still working on changes (`dx`) in branch `x1`, **but hasn't committed yet**.
* Dev1 needs to pull latest changes **without losing local uncommitted work**.

#### 🧰 Steps to Stash, Rebase, and Restore:

```bash
# 1. Stash current local changes (dx)
git stash

# 2. Switch to master and pull the latest changes
git checkout master
git pull

# 3. Switch back to your working branch
git checkout x1

# 4. Rebase with updated master
git rebase master

# 5. Re-apply your stashed changes
git stash pop
```

* If conflicts arise, resolve them manually.

```bash
# 6. Stage and commit
git add .
git commit -m "Rebased with latest master and resolved conflicts"

# 7. Push your updated branch
git push origin x1
```

🔁 Then go to GitHub, create a PR, and proceed to merge after review.

---

### 🧠 Summary: When to Use What?

| Situation                           | Use `rebase` | Use `stash` |
| ----------------------------------- | ------------ | ----------- |
| Working on outdated feature branch  | ✅            | ✅           |
| Changes already committed           | ✅            | ❌           |
| Changes not committed (still local) | ❌            | ✅           |
| Need to clean history               | ✅            | ❌           |
| Want to temporarily store work      | ❌            | ✅           |

---


