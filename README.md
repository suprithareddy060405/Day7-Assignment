# Day 7 Assignment — Introduction to Git and GitHub

![Git](https://img.shields.io/badge/Git-F05032?style=for-the-badge&logo=git&logoColor=white)
![GitHub](https://img.shields.io/badge/GitHub-181717?style=for-the-badge&logo=github&logoColor=white)
![HTML5](https://img.shields.io/badge/HTML5-E34F26?style=for-the-badge&logo=html5&logoColor=white)
![CSS3](https://img.shields.io/badge/CSS3-1572B6?style=for-the-badge&logo=css3&logoColor=white)
![JavaScript](https://img.shields.io/badge/JavaScript-F7DF1E?style=for-the-badge&logo=javascript&logoColor=black)

Welcome to the **Day 7 Assignment Repository** by **Supritha Reddy** ([@suprithareddy060405](https://github.com/suprithareddy060405)).

This repository contains a comprehensive suite covering Git Distributed Version Control System (DVCS) fundamentals, terminal practical execution logs, merge conflict resolutions, stashes, safe commit reverts, GitHub Pages live portfolio hosting, and advanced research papers.

---

## 🔗 Live GitHub Pages Site

🚀 **[https://suprithareddy060405.github.io/Day7-Assignment/](https://suprithareddy060405.github.io/Day7-Assignment/)**

---

## 📁 Repository Directory Structure

```
day7-assignment/
├── README.md                           # Main Repository Documentation & Master Guide
├── index.html                          # Interactive Submission Dashboard Portal
├── css/
│   └── styles.css                      # Master Design System & Dark UI Stylesheet
├── js/
│   └── app.js                          # Portal Controller & Navigation Interactivity
├── theory/
│   └── PART_A_THEORY.md                # Solved Theory Questions (Q1 - Q10)
├── practical/
│   └── PART_B_PRACTICAL.md             # Documented Step-by-Step Practical Exercises (B1 - B5)
├── challenges/
│   └── PART_C_CHALLENGES.md            # Step-by-Step Git Challenges (Conflict Resolution, Revert, Stash, Graph Log)
├── github-activities/
│   ├── PART_D_GITHUB.md                # GitHub Profile, Open Source Research & Pages Deployment Guide
│   └── portfolio/                      # Live Responsive Developer Portfolio (Section 29/30)
│       ├── index.html
│       ├── css/style.css
│       └── js/script.js
└── research/
    └── PART_E_RESEARCH.md              # Advanced Research Papers (SSH, Conventional Commits, Actions, Rebase, Open Source)
```

---

## ⚡ Summary of Assignment Sections

### 📝 Part A — Theory Questions (`theory/PART_A_THEORY.md`)
1. **Version Control**: Definition & 4 core problems solved (accidental loss, history tracking, collaboration, safe branching).
2. **VCS Types**: Local, Centralized (SVN), and Distributed (Git).
3. **Git's Four Areas**: Working Directory, Staging Area (Index), Local Repository (`.git`), Remote Repository.
4. **`git add` vs `git commit`**: Staging intentional snapshots vs committing permanent points in history.
5. **Branches**: Lightweight movable commit pointers & parallel feature development benefits.
6. **Fast-Forward vs 3-Way Merge**: Linear pointer move vs merge commit creation with common ancestor.
7. **Merge Conflicts**: Causes, conflict markers (`<<<<<<<`, `=======`, `>>>>>>>`), and step-by-step resolution.
8. **Git vs GitHub**: Local CLI tool vs Cloud-hosted collaborative SaaS platform.
9. **`git pull` vs `git fetch`**: Fetching references without altering working copy vs `fetch + merge`.
10. **`.gitignore` & Secrets Security**: Pattern matching, keeping API keys/node_modules out of repos, security risks of committing credentials.

---

### 🛠️ Part B — Practical Exercises (`practical/PART_B_PRACTICAL.md`)
- **B1: Git Configuration**: Setting global `user.name` and `user.email` identity & verification via `git config --list`.
- **B2: Commit History**: Creating a local repository, making 3 descriptive commits, and inspecting via `git log --oneline`.
- **B3: Branching & Merging**: Creating feature branch (`feature/analytics`), committing, merging into `main`, and deleting the branch.
- **B4: `.gitignore` Verification**: Creating `.env` and `build/`, applying ignore rules, and verifying with `git status`.
- **B5: `git diff` Inspection**: Demonstrating `git diff` (unstaged changes) vs `git diff --staged` (staged changes).

---

### 🎯 Part C — Git Challenges (`challenges/PART_C_CHALLENGES.md`)
- **C1: Deliberate Merge Conflict**: Creating conflicting edits on line 1 of `config.js` across branches, resolving markers, and completing merge commit.
- **C2: Safe Commit Revert**: Reverting a buggy commit safely using `git revert <hash>` without deleting repository commit history.
- **C3: Working Tree Stashing**: Making uncommitted dirty edits, saving via `git stash`, executing urgent hotfix, and restoring via `git stash pop`.
- **C4: File Renaming (`git mv`)**: Renaming tracked files via `git mv index.js main_app.js` and committing staged rename.
- **C5: History Exploration**: Visualizing branch trees via `git log --oneline --graph --all` and inspecting commits via `git show`.

---

### 🚀 Part D — GitHub Activities & Live Portfolio (`github-activities/`)
- **D1: GitHub Profile**: Complete profile overview for `@suprithareddy060405`.
- **D2 & D3: Live GitHub Pages Deployment**: Live hosting setup at `https://suprithareddy060405.github.io/Day7-Assignment/`.
- **D4: Iterative Live Refresh**: Modifying hero badge, committing, pushing, and verifying live update.
- **D5: Open Source Exploration**: In-depth review of `facebook/react` architecture, package structure, and contribution guidelines.

---

### 📚 Part E — Research Tasks (`research/PART_E_RESEARCH.md`)
- **E1: SSH Key Authentication**: Ed25519 key generation (`ssh-keygen`), adding public key to GitHub, testing connection (`ssh -T git@github.com`).
- **E2: Conventional Commits**: Spec rules (`feat`, `fix`, `docs`, `refactor`, `chore`) with 5 real-world commit examples.
- **E3: GitHub Actions CI/CD Workflows**: Workflow YAML anatomy (`.github/workflows/deploy.yml`), triggers, jobs, steps.
- **E4: `git rebase` vs `git merge`**: Linearizing history vs preserving chronological merge commits, golden rule of rebasing.
- **E5: Open Source Contribution**: 7-step guide from finding issues to submitting Pull Requests (PR).

---

## 🌐 How to Run Locally

1. Clone or download this repository.
2. Open `index.html` in any web browser to access the central master portal.
3. Click on any section card to inspect documentation, CLI logs, or live portfolio.
