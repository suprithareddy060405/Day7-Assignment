# Part A — Theory Questions & Detailed Solutions

---

## Question 1: Explain what version control is and four problems it solves.

**Version Control System (VCS)** is a software category designed to record changes made to files over time so that developers can recall specific historical versions, track edits, compare revisions, and collaborate safely on codebases without overwriting each other's work.

### Four Core Problems Version Control Solves:
1. **Accidental File Overwriting & Loss**: Eliminates chaotic manual file naming hacks (e.g., `project_final_v2_final2.zip`). If a bad edit corrupts code or deletes files, any past working snapshot can be restored instantly.
2. **Untracked History & Accountability**: Provides an immutable log detailing **who** changed what line of code, **when** the edit occurred, and **why** the change was made (via commit messages).
3. **Collision-Free Team Collaboration**: Allows multiple software engineers to work simultaneously on different features of the same codebase without stepping on each other's changes or breaking the production release.
4. **Safe Feature Experimentation**: Developers can create isolated parallel workspaces (branches) to test new algorithms or refactor core components without risking stability on the primary codebase (`main`).

---

## Question 2: Explain the three types of version control systems and which one Git is.

### The Three Types of Version Control Systems:

1. **Local Version Control Systems**:
   - **Mechanism**: Maintains a simple database (like RCS) on a single local computer that tracks file changes as patches.
   - **Drawback**: No collaborative capability; if the local disk fails, the entire version history is lost permanently.

2. **Centralized Version Control Systems (CVCS)**:
   - **Mechanism**: Features a single central server containing the full repository history (e.g., Subversion / SVN, Perforce). Clients check out files from this central server.
   - **Drawback**: Single point of failure. If the central server goes offline, developers cannot save version commits or collaborate. If the central disk is corrupted without backups, project history is destroyed.

3. **Distributed Version Control Systems (DVCS)**:
   - **Mechanism**: Every developer's local machine clones a **complete, full-fledged copy** of the entire repository database, including all file history, branches, and commits.
   - **Drawback/Advantage**: Operates offline seamlessly without relying on continuous server connectivity. If any server dies, any client clone can restore the full repository.

### What Type Git Is:
**Git is a Distributed Version Control System (DVCS)**. Created by Linus Torvalds in 2005 for Linux kernel development, Git gives every collaborator a complete local copy of the repository, enabling rapid local commits, instant branch switching, offline development, and peer-to-peer syncing.

---

## Question 3: Explain Git's four areas (working directory, staging, local repo, remote repo).

Git manages file state across four distinct logical zones:

```
+-------------------+      git add      +-------------------+
| Working Directory | ----------------> | Staging Area      |
| (Un-tracked/Modified)|                 | (Index)           |
+-------------------+                   +-------------------+
                                                  |
                                                  | git commit
                                                  v
+-------------------+     git push      +-------------------+
| Remote Repo       | <---------------- | Local Repo        |
| (GitHub/GitLab)   | <---------------- | (.git directory)  |
+-------------------+     git fetch/pull+-------------------+
```

1. **Working Directory (Working Tree)**: The physical workspace directory on your local filesystem containing active project files. Files here are either *untracked*, *modified*, or *unmodified*.
2. **Staging Area (Index)**: A lightweight binary file inside `.git` that acts as a preparation area. It holds selective changes intended for the next commit snapshot, allowing developers to organize logical, clean commits before finalizing them.
3. **Local Repository (`.git` directory)**: The local database on your machine where Git permanently records committed snapshots (objects, trees, commits, tags). Once committed here, history is safely preserved locally.
4. **Remote Repository**: A cloud- or server-hosted copy of the repository (e.g., hosted on GitHub, GitLab, or Bitbucket) used to share, sync, and back up code across distributed team members.

---

## Question 4: Explain the difference between `git add` and `git commit`.

While both commands move code along Git's pipeline, they fulfill distinct roles:

### `git add` (Stage Changes):
- **Purpose**: Moves modified or newly created files from the **Working Directory** into the **Staging Area (Index)**.
- **Analogy**: Packing specific items into a shipping box before taping it shut.
- **Scope**: Does not alter repository history. It merely marks specific files as ready to be snapshotted.

### `git commit` (Record Snapshot):
- **Purpose**: Takes all staged changes currently in the **Staging Area** and permanently writes a cryptographically hashed snapshot into the **Local Repository**.
- **Analogy**: Sealing, labeling, and stamping a date/timestamp on the shipping box and storing it permanently in the archive vault.
- **Scope**: Creates a new immutable commit object containing author metadata, timestamp, parent commit pointer, and commit message.

---

## Question 5: Explain what a branch is and why branches are important.

### What a Branch Is:
In Git, a **branch** is not a heavy copy of all files; it is simply a lightweight, movable pointer referencing a specific commit SHA-1 hash (40 characters). The default primary branch is traditionally named `main` or `master`.

### Why Branches Are Important:
1. **Isolated Parallel Workstreams**: Branches allow developers to create isolated workspaces (`feature/login`, `bugfix/header`) without touching or destabilizing the working production code on `main`.
2. **Concurrent Team Productivity**: Multiple engineers can work simultaneously on separate features in parallel branches without code collisions.
3. **Safe Code Review (Pull Requests)**: Before merging new code into `main`, feature branches can be deployed to staging, tested via automated CI/CD pipelines, and peer-reviewed on GitHub.

---

## Question 6: Explain the difference between a fast-forward merge and a three-way merge.

When integrating changes from a feature branch back into `main`, Git executes either a Fast-Forward or Three-Way merge depending on branch commit history.

### 1. Fast-Forward Merge (`FF`):
- **Condition**: Occurs when the target branch (`main`) has **no new commits** since the feature branch was created.
- **Mechanic**: Git simply advances (fast-forwards) the `main` branch pointer forward to point at the latest commit of the feature branch.
- **Result**: No extra "merge commit" is generated; commit history remains completely linear.

```
Linear Fast-Forward:
C1 ---> C2 (main) ---> C3 ---> C4 (feature)
                \ (fast-forward main to C4)
                 =========================>
```

### 2. Three-Way Merge (`3-Way`):
- **Condition**: Occurs when **both** `main` and the feature branch have diverged with new independent commits since they split.
- **Mechanic**: Git uses three commits (the common ancestor commit, the tip of `main`, and the tip of `feature`) to compute the merged state.
- **Result**: Creates a brand new **Merge Commit** with two parent commit pointers to join the histories.

```
Three-Way Merge:
C1 ---> C2 ---> C3 (main) ---------> M (New Merge Commit)
          \                        /
           ---> C4 ---> C5 (feature)
```

---

## Question 7: Explain what a merge conflict is and how to resolve it.

### What a Merge Conflict Is:
A **merge conflict** occurs when Git attempts to automatically merge two branches that contain **competing changes to the exact same line(s) of a file**, or when one branch deleted a file that another branch modified. Git stops the merge process and requires human intervention to specify which code to keep.

### Conflict Marker Anatomy:
When a conflict occurs, Git embeds conflict markers directly inside affected files:

```text
<<<<<<< HEAD (Current Branch - e.g. main)
const themeColor = "#0f172a";
=======
const themeColor = "#6366f1";
>>>>>>> feature-theme (Incoming Branch)
```

### Step-by-Step Resolution Workflow:
1. **Identify Conflict Files**: Run `git status` to see all unmerged files listed under "Unmerged paths".
2. **Open & Edit Affected Files**: Manually inspect the code, delete conflict markers (`<<<<<<<`, `=======`, `>>>>>>>`), and edit the code to the final desired state.
3. **Stage Resolved Files**: Run `git add <resolved-file>` to mark the conflict as resolved in the staging area.
4. **Finalize Merge Commit**: Run `git commit -m "Fix merge conflict between main and feature-theme"` to complete the merge process.

---

## Question 8: Explain the difference between Git and GitHub.

Though closely related, Git and GitHub are fundamentally distinct technologies:

| Comparison Dimension | Git | GitHub |
| :--- | :--- | :--- |
| **Core Definition** | Open-source command-line **Distributed Version Control System (DVCS)** tool. | Cloud-hosted web platform & SaaS for hosting Git repositories. |
| **Installation** | Runs locally on your operating system (Windows, macOS, Linux). | Accessible via web browser or REST API at `github.com`. |
| **Key Responsibilities** | Tracking file changes, branching, committing, stashing, local history. | Cloud backup, Pull Request code reviews, issue tracking, GitHub Actions CI/CD, GitHub Pages hosting. |
| **Network Dependency** | Completely functional offline without internet access. | Requires internet connectivity to push, pull, or view web UI. |
| **Creator** | Created by Linus Torvalds in 2005. | Founded in 2008 by Tom Preston-Werner, Chris Wanstrath, and PJ Hyett (Acquired by Microsoft in 2018). |

---

## Question 9: Explain the difference between `git pull` and `git fetch`.

Both commands retrieve remote updates from GitHub, but they differ in how they impact your local working copy:

### `git fetch`:
- **Operation**: Downloads remote commits, refs, and branches from GitHub into your local `.git` repository database, but **does NOT touch or alter your active Working Directory or current branch**.
- **Use Case**: Safe inspection. Allows you to run `git log origin/main` or `git diff main origin/main` to inspect remote changes before deciding to integrate them.

### `git pull`:
- **Operation**: Performs two actions in a single command: `git fetch` followed immediately by `git merge`.
- **Use Case**: Quick synchronization when you want remote changes fetched and immediately merged into your active branch.

```
git pull  ===  git fetch  +  git merge
```

---

## Question 10: Explain what a `.gitignore` file is and why you should never commit secrets.

### What a `.gitignore` File Is:
A `.gitignore` file is a plain text file placed in a Git repository root directory that specifies pattern rules for files and folders that Git should intentionally ignore and exclude from version tracking.

#### Common `.gitignore` Pattern Rules:
```gitignore
# Dependencies
node_modules/

# Environment Variables & Secrets
.env
.env.local
secrets.json

# Build Outputs & OS System Files
dist/
.DS_Store
Thumbs.db
```

### Why You Should NEVER Commit Secrets:
1. **Public Exposure & Instant Exploitation**: Pushing API keys, AWS credentials, database passwords, or private keys to public GitHub repositories leads to automated bot scanners harvesting credentials within seconds of publication.
2. **Immutable History Persistence**: Once a secret is committed and pushed, it remains embedded in Git commit history objects even if deleted in a subsequent commit. Purging it requires complex repository rewriting tools like `git-filter-repo` or BFG Repo-Cleaner.
3. **Financial & Security Liability**: Compromised cloud API keys can result in massive unauthorized cloud infrastructure billing, data breaches, regulatory compliance fines, and legal liability.
