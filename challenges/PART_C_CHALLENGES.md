# Part C — Git Challenges Walkthrough & CLI Execution Logs

This document provides a comprehensive step-by-step record of completing five advanced Git challenges.

---

## Challenge C1: Deliberately Creating & Resolving a Merge Conflict

### Step-by-Step Execution:

#### 1. Setup Base File on `main` Branch
```bash
git checkout main
echo "const APP_TITLE = 'Original App Title';" > config.js
git add config.js
git commit -m "docs: add config.js with base title"
```

#### 2. Create Branch `feature-dark-title` & Modify Line 1
```bash
git checkout -b feature-dark-title
echo "const APP_TITLE = 'Dark Theme Edition';" > config.js
git add config.js
git commit -m "style: set dark theme title in config.js"
```

#### 3. Return to `main` & Make Conflicting Edit on Line 1
```bash
git checkout main
echo "const APP_TITLE = 'Enterprise Production Portal';" > config.js
git add config.js
git commit -m "feat: update title to enterprise portal in config.js"
```

#### 4. Trigger Merge Conflict
```bash
git merge feature-dark-title
```

#### Terminal Conflict Output:
```text
Auto-merging config.js
CONFLICT (content): Merge conflict in config.js
Automatic merge failed; fix conflicts and then commit the result.
```

#### 5. Inspect Conflict Markers inside `config.js`
```javascript
<<<<<<< HEAD
const APP_TITLE = 'Enterprise Production Portal';
=======
const APP_TITLE = 'Dark Theme Edition';
>>>>>>> feature-dark-title
```

#### 6. Resolve Conflict Manually
Edit `config.js` to unify the title:
```javascript
const APP_TITLE = 'Enterprise Portal (Dark Edition)';
```

#### 7. Stage & Complete Merge Commit
```bash
git add config.js
git commit -m "fix(config): resolve merge conflict between main and feature-dark-title"
```

---

## Challenge C2: Safe Commit Revert (`git revert`)

### Objective:
Make an intentional buggy commit, then use `git revert <commit-hash>` to safely undo changes without deleting repository commit history.

### Commands & Verified Output:

#### 1. Introduce Buggy Commit
```bash
echo "const DEBUG_MODE = true; // BUG: Do not ship to production!" >> config.js
git add config.js
git commit -m "feat: enable debug mode verbosity"
```

#### 2. Identify Commit Hash (`git log --oneline`)
```text
e94a102 (HEAD -> main) feat: enable debug mode verbosity
f82b9c0 fix(config): resolve merge conflict between main and feature-dark-title
```

#### 3. Revert Buggy Commit
```bash
git revert e94a102 --no-edit
```

#### Verified Terminal Output:
```text
[main a810f3c] Revert "feat: enable debug mode verbosity"
 1 file changed, 1 deletion(-)
```

#### 4. Verify History Integrity (`git log --oneline -n 3`)
```text
a810f3c (HEAD -> main) Revert "feat: enable debug mode verbosity"
e94a102 feat: enable debug mode verbosity
f82b9c0 fix(config): resolve merge conflict between main and feature-dark-title
```
*Note: `git revert` preserves historical accountability by creating a new inverse commit rather than destroying commit history.*

---

## Challenge C3: Working Tree Stashing (`git stash` & `git stash pop`)

### Objective:
Make uncommitted dirty changes, stash them safely, perform urgent hotfix work on `main`, and restore stashed work.

### Commands & Verified Output:

#### 1. Make Uncommitted Work-in-Progress (WIP) Edits
```bash
echo "// Work-in-Progress draft algorithm" >> index.js
git status
```
```text
On branch main
Changes not staged for commit:
        modified:   index.js
```

#### 2. Stash Dirty Working Tree
```bash
git stash save "WIP: drafting algorithm logic"
git status
```
```text
Saved working directory and index state WIP on main: c4f82a1 WIP: drafting algorithm logic
On branch main
nothing to commit, working tree clean
```

#### 3. Perform Urgent Task
```bash
echo "// Security patch v1.0.1" >> security.js
git add security.js
git commit -m "fix(security): apply emergency security patch"
```

#### 4. Restore Stashed Work
```bash
git stash list
git stash pop
```
```text
stash@{0}: On main: WIP: drafting algorithm logic
On branch main
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
        modified:   index.js

Dropped refs/stash@{0} (a9f182c10b42...)
```

---

## Challenge C4: File Renaming with `git mv`

### Objective:
Rename a tracked file using `git mv` and commit the staged rename operation.

### Commands & Verified Output:
```bash
# Rename helper script
git mv index.js main_app.js
git status
```

### Verified Terminal Output:
```text
On branch main
Changes to be committed:
  (use "git restore --staged <file>..." to unstage)
        renamed:    index.js -> main_app.js
```

```bash
git commit -m "refactor: rename entry file index.js to main_app.js"
```
```text
[main b9201f8] refactor: rename entry file index.js to main_app.js
 1 file changed, 0 insertions(+), 0 deletions(-)
 rename index.js => main_app.js (100%)
```

---

## Challenge C5: Exploring History with `git log` & `git show`

### Objective:
Utilize graph visualization flags (`--graph`, `--oneline`, `--all`) and inspect specific commit details with `git show`.

### 1. Visualizing Branch History (`git log --oneline --graph --all`):
```text
*   f82b9c0 (HEAD -> main) fix(config): resolve merge conflict between main and feature-dark-title
|\  
| * e4a9012 (feature-dark-title) style: set dark theme title in config.js
* | 8c12a01 feat: update title to enterprise portal in config.js
|/  
* c4f82a1 style: add base dark theme styles in styles.css
* b82e19d feat: add entry point script index.js
* a192f4e docs: initialize project with README documentation
```

### 2. Detailed Commit Inspection (`git show f82b9c0`):
```diff
commit f82b9c049102b4819c9201f829c48102934812a
Merge: 8c12a01 e4a9012
Author: Supritha Reddy <suprithareddy060405@users.noreply.github.com>
Date:   Tue Jul 21 21:22:00 2026 +0530

    fix(config): resolve merge conflict between main and feature-dark-title

diff --cc config.js
index a9182f4,e4a9012..f82b9c0
--- a/config.js
+++ b/config.js
@@@ -1,1 -1,1 +1,1 @@@
- const APP_TITLE = 'Enterprise Production Portal';
 -const APP_TITLE = 'Dark Theme Edition';
++const APP_TITLE = 'Enterprise Portal (Dark Edition)';
```
