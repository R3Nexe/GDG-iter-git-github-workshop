#  Git & GitHub — Workshop Resource Guide
> **GDG on Campus ITER** · A beginner-friendly reference for everything covered in the workshop.  
> Bookmark this page and refer back anytime you're stuck!

---

## Index

<strong>Getting Started</strong>

* [What is Git?](#what-is-git)
* [Why Use Git?](#why-use-git)
* [Installing Git](#installing-git)
* [Initial Git Setup](#initial-git-setup)

<strong>Core Workflow</strong>

* [Core Git Workflow](#core-git-workflow)
* [Git vs GitHub](#git-vs-github)
* [Creating a Remote Repository](#creating-a-remote-repository)

<strong>Authentication</strong>

* [SSH Authentication](#ssh-authentication)

<strong>Branching & Collaboration</strong>

* [Branching](#branching)
* [Pull Requests](#pull-requests)

<strong>Fixing Mistakes</strong>

* [Reverting & Fixing Mistakes](#reverting--fixing-mistakes)

<strong>Advanced Topics</strong>

* [Merging and Merge Conflicts](#merging-and-merge-conflicts)
* [Merging vs Rebasing](#merging-vs-rebasing)
* [Understanding .gitignore](#understanding-gitignore)

<strong>Best Practices</strong>

* [Good Practices](#good-practices)

---

## <a name="what-is-git"></a>What is Git?

Git is a **distributed version control system** created by **Linus Torvalds in 2005**.

- Tracks every change made to your files over time
- Allows multiple developers to collaborate on the same project
- Stores your project history as a series of **commits**
- Internally, Git represents history as a **Directed Acyclic Graph (DAG)** of commits

> Think of Git as a **timeline for your project** — you can go back, branch off, and merge timelines.

---

## <a name="why-use-git"></a>Why Use Git?

Without Git, sharing code means sending ZIP files back and forth — prone to overwriting code, missing changes, and bugs.

Git solves this with:

### ✅ Version Control
- See *what* changed, *when* it changed, and *who* changed it
- Restore older versions of code if something breaks

### ✅ Safe Experimentation
- Create **branches** to try new features without touching the main codebase
- Discard experiments safely if they don't work out

### ✅ Collaboration
- Multiple developers can work on the same project simultaneously
- Git merges contributions from different people intelligently

---

## <a name="installing-git"></a>Installing Git

### Windows
Download the installer from: [https://git-scm.com](https://git-scm.com)

Then verify:
```bash
git --version
```

### macOS
```bash
brew install git
git --version
```

### Linux (Debian / Ubuntu / Mint)
```bash
sudo apt update
sudo apt install git
```

### Linux (Fedora / CentOS)
```bash
sudo dnf install git
```

### Linux (Arch)
```bash
sudo pacman -S git
```

---

## <a name="initial-git-setup"></a>Initial Git Setup

Before making any commits, tell Git who you are. This info is attached to every change you make.

```bash
git config --global user.name "Your Name"
git config --global user.email "you@email.com"
git config --global init.defaultBranch main
```

> 💡 Your username and email should ideally match your GitHub account.

---

## <a name="core-git-workflow"></a>Core Git Workflow

This is the everyday loop you'll use with Git.

### Step 1 — Initialize a repository
```bash
git init
```
Creates a hidden `.git` folder that starts tracking your project.

### Step 2 — Check the status of your files
```bash
git status
```
Shows which files are modified, staged, or untracked.

### Step 3 — Stage your changes
```bash
git add .                  # Stage all changed files
git add <filename>         # Stage a specific file
```
Staging is like preparing a "snapshot" before saving it.

### Step 4 — Commit your changes
```bash
git commit -m "Descriptive commit message"
```
A commit saves a permanent snapshot of your staged changes.

### Step 5 — View commit history
```bash
git log
```

### Step 6 — Push to a remote repository
```bash
git remote add origin https://github.com/<username>/<repo-name>.git
git push -u origin main
```
After the first push, you can simply use:
```bash
git push
```

---

## <a name="git-vs-github"></a>Git vs GitHub

| | Git | GitHub |
|---|---|---|
| **What it is** | A version control tool | A cloud platform for hosting Git repos |
| **Runs** | Locally on your machine | In the cloud |
| **Purpose** | Track changes in code | Share, collaborate, and review code |

> 📌 Code changes in your **local repository** are private until you **push** them to your **remote repository** on GitHub.

---

## <a name="creating-a-remote-repository"></a>Creating a Remote Repository

### Step 1 — Create a repo on GitHub
1. Go to [https://github.com](https://github.com)
2. Click **New repository**
3. Give it a descriptive name
4. Choose **Public** or **Private**
5. **Do NOT** initialize with a README (since you have local code)
6. Copy the repository URL (e.g. `https://github.com/<username>/<repo-name>.git`)

### Step 2 — Navigate to your project
```bash
cd <path-to-your-project>
```

### Step 3 — Ensure your branch is named `main`
```bash
git branch -M main
```

### Step 4 — Link local repo to the remote
```bash
git remote add origin <your-repository-url>
```

### Step 5 — Push your code
```bash
git push -u origin main
```

> 💡 After this initial push, future pushes just need `git push`.

---

## <a name="ssh-authentication"></a>SSH Authentication

SSH (Secure Shell) lets you authenticate with GitHub **without entering your password every time**.

### Generate an SSH Key (Mac/Linux)
```bash
ssh-keygen -t ed25519 -C "your_email@example.com"
```

### Start the SSH Agent
```bash
eval "$(ssh-agent -s)"
ssh-add ~/.ssh/id_ed25519
```

### Copy your Public Key
```bash
# Mac
pbcopy < ~/.ssh/id_ed25519.pub

# Windows
clip < ~/.ssh/id_ed25519.pub
```

### Add Key to GitHub
1. Go to **GitHub → Settings → SSH and GPG Keys**
2. Click **New SSH Key**
3. Paste the copied key and save

---

## <a name="branching"></a>Branching

Branching lets you create a **separate version of the codebase** — like making a copy at a specific point in time — so you can work independently without affecting the main project.

> In production, teams use branches for: `main` (stable), `dev` (development), `feature/*`, `bugfix/*`, etc.

### Create a branch
```bash
git branch <branch-name>
```

### Switch to a branch
```bash
git checkout <branch-name>
```

### Create AND switch in one command (shortcut)
```bash
git checkout -b <branch-name>
```

### Go back to the main branch
```bash
git checkout main
```

### Create a branch from a specific source branch
```bash
git branch <new-branch-name> <source-branch-name>
```

> ⚠️ Branching happens **from the branch you're currently on**. Be aware of your HEAD pointer before branching!

---

## <a name="pull-requests"></a>Pull Requests

Pull Requests (PRs) are used to **propose changes** to a repository and request they be reviewed and merged.

### Workflow

**Step 1 — Create and switch to a feature branch**
```bash
git checkout -b feature-login
```

**Step 2 — Make your changes, then stage and commit**
```bash
git add .
git commit -m "feat: add login authentication"
```

**Step 3 — Push the branch to GitHub**
```bash
git push origin feature-login
```

**Step 4 — Open a Pull Request on GitHub**
1. Open your repository on GitHub
2. Click **"Compare & pull request"**
3. Add a clear description of your changes
4. Submit the PR for review

---

## <a name="reverting--fixing-mistakes"></a>Reverting & Fixing Mistakes

Git works across 3 stages: **Working Directory → Staging Area → Commit History**

### Case 1 — Discard changes in the working directory
> The file is modified but not yet staged.
```bash
git restore <filename>
```
> ⚠️ This **permanently deletes** your unsaved edits.

### Case 2 — Unstage a file
> The file is staged but not yet committed.
```bash
git restore --staged <filename>
```
> Your changes still exist — they're just no longer staged.

### Case 3 — Amend the last commit
> You committed but forgot to include something.
```bash
git add <filename>                         # Stage the forgotten file
git commit --amend -m "Updated message"   # Amend the last commit
```
> ⚠️ **Never amend commits that have already been pushed to GitHub.**

### Case 4 — Undo a commit safely (revert)
> Creates a new commit that reverses the previous one — history is preserved.
```bash
git revert <commit-hash>
```

### Case 5 — Reset commits (move the branch pointer)
```bash
git reset --soft HEAD~1    # Keeps new changes staged
git reset --mixed HEAD~1   # New changes are unstaged
git reset --hard HEAD~1    # New changes are deleted
```
> `HEAD~n` refers to how many commits back you want to go.

### Case 6 — Reset to a specific commit
```bash
git reset --hard <commit-hash>
```
> ⚠️ Deleted commits **cannot be easily recovered**.

---

## <a name="merging-and-merge-conflicts"></a>Merging and Merge Conflicts

**Merging** combines the changes from one branch into another.

### Fast-Forward Merge
Happens when the base branch has no new commits since the feature branch was created. Git simply moves the pointer forward — no merge commit is created.

### 3-Way Merge (Diverged Branches)
Both branches have new commits. Git creates a special **merge commit** with two parents, preserving the full history of both.

```bash
git checkout main
git merge <branch-name>
```

### Merge Conflict
Occurs when **both branches edited the same part of the same file**. Git can't decide automatically — you must resolve it manually.

**To resolve:**
1. Open the conflicting file — Git marks conflicts like this:
   ```
   <<<<<<< HEAD
   your changes
   =======
   incoming changes
   >>>>>>> feature-branch
   ```
2. Edit the file to keep what you want
3. Stage and complete the merge:
   ```bash
   git add <filename>
   git commit
   ```

---

## <a name="merging-vs-rebasing"></a>Merging vs Rebasing

| | Merging | Rebasing |
|---|---|---|
| **What it does** | Combines branches without rewriting history | Moves commits to a new base |
| **Creates** | A merge commit | Rewrites commit history |
| **Safe for shared branches?** | ✅ Yes | ❌ No |

```bash
# Rebase your feature branch onto main
git checkout feature-branch
git rebase main
```

> ⚠️ **Never rebase branches that others are working on.** It rewrites history and causes confusion.

---

## <a name="understanding-gitignore"></a>Understanding .gitignore

`.gitignore` tells Git which files or directories **should not be tracked**. This prevents sensitive, environment-specific, or unnecessary files from being committed.

### Create a `.gitignore` file
```bash
touch .gitignore
```

### Common patterns to ignore
```gitignore
# Environment variables
.env

# Python
__pycache__/
*.pyc
venv/

# Node.js
node_modules/

# Logs
*.log

# OS files
.DS_Store

# IDE settings
.vscode/
```

> 💡 GitHub provides [ready-made `.gitignore` templates](https://github.com/github/gitignore) for most languages and frameworks.

---

## <a name="good-practices"></a>Good Practices

### ✍️ Write meaningful commit messages
Commit messages should explain **what changed**, not just that a change happened.

```
feat: add login authentication
fix: resolve API timeout issue
docs: update README installation steps
refactor: simplify user validation logic
```

### 🔬 Commit small, logical changes
Each commit should represent one cohesive change. Avoid "big bang" commits.

### 🌿 Use branches for every feature
Never develop directly on `main`. Always create a feature or bugfix branch.

```bash
git checkout -b feature/user-profile
git checkout -b fix/login-bug
```

### 📥 Pull before you push
Always sync your branch with the remote before pushing to avoid conflicts.

```bash
git pull origin main
```

### 🏷️ Name branches meaningfully
Branch names should describe the task:

```
feature/add-search
fix/null-pointer-crash
docs/api-reference
```

---

## 🔧 Quick Command Reference

| Command | Description |
|---|---|
| `git init` | Initialize a new local repo |
| `git status` | Check changed/staged files |
| `git add .` | Stage all changes |
| `git add <file>` | Stage a specific file |
| `git commit -m "msg"` | Commit staged changes |
| `git log` | View commit history |
| `git push` | Push commits to remote |
| `git pull` | Fetch and merge remote changes |
| `git branch <n>` | Create a branch |
| `git checkout <n>` | Switch to a branch |
| `git checkout -b <n>` | Create and switch to a branch |
| `git merge <branch>` | Merge a branch into current |
| `git revert <hash>` | Safely undo a commit |
| `git restore <file>` | Discard working dir changes |
| `git restore --staged <file>` | Unstage a file |
| `git reset --hard HEAD~1` | Remove last commit (destructive) |
| `git stash` | Temporarily save uncommitted changes |
| `git stash pop` | Restore stashed changes |

---

## 📚 Further Reading

- [Official Git Documentation](https://git-scm.com/doc)
- [GitHub Docs](https://docs.github.com)
- [Pro Git Book (free)](https://git-scm.com/book/en/v2)
- [GitHub's `.gitignore` templates](https://github.com/github/gitignore)
- [Conventional Commits](https://www.conventionalcommits.org/) — a standard for commit messages

---

> Made with ❤️ by **GDG on Campus ITER** · [Instagram](https://www.instagram.com/gdg_iter) · [YouTube](https://youtube.com/@gdgiter) · gdsciter@gmail.com
