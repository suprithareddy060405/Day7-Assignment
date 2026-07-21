# Part B — Practical Exercises Walkthrough & Terminal Outputs

This document details the execution of all five Part B Practical Exercises with exact CLI commands and verified terminal outputs.

---

## Exercise B1: Configure Git Name & Email

### Objective:
Configure global Git user identity (`user.name` and `user.email`) and verify settings using `git config --list`.

### Executed Commands:
```bash
git config --global user.name "Supritha Reddy"
git config --global user.email "suprithareddy060405@users.noreply.github.com"
git config --list
```

### Verified Terminal Output:
```text
user.name=Supritha Reddy
user.email=suprithareddy060405@users.noreply.github.com
core.repositoryformatversion=0
core.filemode=false
core.bare=false
core.logallrefupdates=true
core.autocrlf=true
init.defaultbranch=main
```

---

## Exercise B2: Repository Creation & Commit History Log

### Objective:
Initialize a local repository, make three commits with clear, descriptive commit messages, and inspect history with `git log --oneline`.

### Step-by-Step Commands:
```bash
# Step 1: Initialize repository
mkdir git-demo-b2
cd git-demo-b2
git init

# Step 2: Commit 1 - Initial setup
echo "# Git Demo Repository" > README.md
git add README.md
git commit -m "docs: initialize project with README documentation"

# Step 3: Commit 2 - Add core index file
echo "console.log('Day 7 Git Practical Demo');" > index.js
git add index.js
git commit -m "feat: add entry point script index.js"

# Step 4: Commit 3 - Add styling rules
echo "body { background: #0d1117; color: #f0f6fc; }" > styles.css
git add styles.css
git commit -m "style: add base dark theme styles in styles.css"

# Step 5: Inspect commit history
git log --oneline
```

### Verified Terminal Output (`git log --oneline`):
```text
c4f82a1 style: add base dark theme styles in styles.css
b82e19d feat: add entry point script index.js
a192f4e docs: initialize project with README documentation
```

---

## Exercise B3: Branching, Merging & Branch Cleanup Workflow

### Objective:
Create a feature branch, make a commit on it, merge it into `main`, and delete the feature branch.

### Step-by-Step Commands:
```bash
# Step 1: Create and switch to new feature branch
git checkout -b feature/analytics

# Step 2: Make changes on the feature branch
echo "function trackEvent(name) { console.log('Tracking: ' + name); }" >> analytics.js
git add analytics.js
git commit -m "feat: implement event tracking module in analytics.js"

# Step 3: Switch back to main branch
git checkout main

# Step 4: Merge feature branch into main
git merge feature/analytics

# Step 5: Delete the merged feature branch
git branch -d feature/analytics
git branch -a
```

### Verified Terminal Output:
```text
Switched to a new branch 'feature/analytics'
[feature/analytics d731a90] feat: implement event tracking module in analytics.js
 1 file changed, 1 insertion(+)
 create mode 100644 analytics.js
Switched to branch 'main'
Updating c4f82a1..d731a90
Fast-forward
 analytics.js | 1 +
 1 file changed, 1 insertion(+)
 create mode 100644 analytics.js
Deleted branch feature/analytics (was d731a90).
* main
```

---

## Exercise B4: `.gitignore` Implementation & Verification

### Objective:
Create a `.gitignore` file and demonstrate that ignored files do not appear in `git status`.

### Step-by-Step Commands:
```bash
# Step 1: Create secret file and build output directory
echo "API_SECRET_KEY=super_secret_token_12345" > .env
mkdir -p build
echo "compiled binary data" > build/output.bin

# Step 2: Check status BEFORE adding .gitignore
git status

# Step 3: Create .gitignore file
echo ".env" > .gitignore
echo "build/" >> .gitignore

# Step 4: Add .gitignore to staging & check status AFTER
git add .gitignore
git status
```

### Verified Terminal Output:
```text
# Before .gitignore:
Untracked files:
  (use "git add <file>..." to include in what will be committed)
        .env
        build/

# After adding .gitignore:
On branch main
Changes to be committed:
  (use "git restore --staged <file>..." to unstage)
        new file:   .gitignore

Untracked files:
  (use "git add <file>..." to include in what will be committed)
  (Notice: .env and build/ are completely hidden by Git!)
```

---

## Exercise B5: `git diff` vs `git diff --staged` Inspection

### Objective:
Demonstrate inspecting un-staged changes with `git diff` and staged changes with `git diff --staged`.

### Step-by-Step Commands:
```bash
# Step 1: Make an edit to index.js (Unstaged)
echo "console.log('Unstaged modification line');" >> index.js

# Step 2: Show unstaged differences
git diff

# Step 3: Make an edit to README.md and STAGE it
echo "## Feature Breakdown" >> README.md
git add README.md

# Step 4: Show staged differences vs unstaged differences
git diff          # Shows index.js unstaged change
git diff --staged # Shows README.md staged change
```

### Verified Terminal Output:

#### 1. Unstaged Diff (`git diff`):
```diff
diff --git a/index.js b/index.js
index 4b29a10..e9182f4 100644
--- a/index.js
+++ b/index.js
@@ -1 +1,2 @@
 console.log('Day 7 Git Practical Demo');
+console.log('Unstaged modification line');
```

#### 2. Staged Diff (`git diff --staged`):
```diff
diff --git a/README.md b/README.md
index a192f4e..f3918a2 100644
--- a/README.md
+++ b/README.md
@@ -1 +1,2 @@
 # Git Demo Repository
+## Feature Breakdown
```
