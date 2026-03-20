#  Contributing Guide — How to Mark Your Attendance

> Follow these steps carefully. This is a real Git workflow — the same one developers use every day when contributing to open source projects.

---

##  Prerequisites

Make sure you have completed these before starting:

- [ ] Git installed on your machine (`git --version` to verify)
- [ ] A GitHub account — [create one here](https://github.com/signup) if you haven't
- [ ] Git configured with your name and email:
  ```bash
  git config --global user.name "Your Name"
  git config --global user.email "you@email.com"
  ```

---

##  Step-by-Step

### Step 1 — Fork this repository

Click the **Fork** button at the top-right of this page on GitHub.

This creates your own copy of the repo under your GitHub account.

> 💡 A fork is your personal copy of someone else's repo. You can make changes without affecting the original.

---

### Step 2 — Clone your fork

Copy the URL of **your fork** (not the original repo) and run:

```bash
git clone https://github.com/<your-username>/GDG-iter-git-github-workshop.git
cd GDG-iter-git-github-workshop
```

> 💡 Cloning downloads the repo to your local machine so you can work on it.

---

### Step 3 — Create a new branch

**Never make changes directly on `main`.** Always create a branch:

```bash
git checkout -b attendance/<your-name>
```

For example:
```bash
git checkout -b attendance/nishant-kuamr
```

> 💡 Branches let you work on changes in isolation without touching the stable main codebase.

---

### Step 4 — Add your details to [`ATTENDEES.md`](./ATTENDEES.md)

Open `ATTENDEES.md` in any text editor and add a new row to the table.

**Follow this exact format:**

```markdown
| # | Your Full Name | Your Reg. Number | [@your-github](https://github.com/your-github) | Your Branch |
```

 **Rules:**
- Do **not** change anyone else's row
- Do **not** change the table headers
- The `#` column should be the next number in sequence
- Use your actual GitHub username with the correct link format
- Keep one space inside each `|` cell

---

### Step 5 — Stage your changes

```bash
git add ATTENDEES.md
```

> 💡 Staging tells Git which changes you want to include in your next commit.

---

### Step 6 — Commit with a meaningful message

```bash
git commit -m "feat: add <your-name> to attendees"
```

For example:
```bash
git commit -m "feat: add nishant-kumar to attendees"
```

> 💡 A good commit message tells others *what* changed and *why*, not just that it changed.

---

### Step 7 — Push your branch to GitHub

```bash
git push origin attendance/<your-name>
```

This uploads your branch to your forked repo on GitHub.

---

### Step 8 — Open a Pull Request

1. Go to **your fork** on GitHub
2. You'll see a banner: **"Compare & pull request"** — click it
3. Make sure the base repo is `R3Nexe/GDG-iter-git-github-workshop` and the base branch is `main`
4. Give your PR a clear title, e.g. `feat: add nishant-kumar to attendees`
5. Click **"Create pull request"**

> 💡 A Pull Request (PR) is your way of saying: "Hey, I made some changes — can you review and merge them?"

---

## ✅ PR Checklist

Before submitting, make sure:

- [ ] Your branch is named `attendance/<your-name>`
- [ ] You only edited `ATTENDEES.md`
- [ ] Your row follows the correct table format
- [ ] Your commit message starts with `feat:`
- [ ] You opened the PR against the `main` branch of the **original repo** (not your fork)

---

## ❓ Common Issues

**"I cloned the original repo instead of my fork"**
```bash
# Remove the wrong remote and add your fork
git remote remove origin
git remote add origin https://github.com/<your-username>/gdg-iter-git-workshop.git
git push origin attendance/<your-name>
```

**"I made changes directly on main"**
```bash
# Create a new branch from your current state
git checkout -b attendance/<your-name>
git push origin attendance/<your-name>
```

**"My PR has a merge conflict"**  
Ask a GDG volunteer for help — resolving merge conflicts is a great learning moment!

---

##  Need Help?

Contact the Official Email address of _GDGoC@SOA ITER_ at **gdsciter@gmail.com**

---

<p align="center">Happy Gitting! — GDG on Campus ITER</p>
