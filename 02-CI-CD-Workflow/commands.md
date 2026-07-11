# Commands

This section covers the common commands involved in a typical CI/CD workflow. These commands are executed by developers or CI/CD tools during different stages of the pipeline.

---

# Check Git Status

Displays the current status of the Git repository.

```bash
git status
```

Example Output

```text
On branch main
Your branch is up to date with 'origin/main'.

nothing to commit, working tree clean
```

---

# Stage Changes

Adds all modified files to the staging area.

```bash
git add .
```

Add a specific file:

```bash
git add filename
```

---

# Commit Changes

Creates a snapshot of the staged changes.

```bash
git commit -m "Add new feature"
```

---

# View Commit History

Displays the project's commit history.

```bash
git log
```

Compact version:

```bash
git log --oneline
```

---

# Push Changes to GitHub

Uploads local commits to the remote repository.

```bash
git push origin main
```

---

# Clone a Repository

Downloads an existing Git repository.

```bash
git clone https://github.com/username/repository.git
```

---

# Pull Latest Changes

Downloads and merges changes from the remote repository.

```bash
git pull origin main
```

---

# Check Branch

Displays the current Git branch.

```bash
git branch
```

---

# Create a New Branch

```bash
git checkout -b feature/login
```

---

# Switch Branch

```bash
git checkout main
```

---

# Verify Java Installation

```bash
java --version
```

---

# Verify Git Installation

```bash
git --version
```

---

# Verify Docker Installation

```bash
docker --version
```

---

# Summary

| Command | Purpose |
|----------|---------|
| `git status` | View repository status |
| `git add .` | Stage changes |
| `git commit -m` | Create a commit |
| `git log --oneline` | View commit history |
| `git push origin main` | Push code to GitHub |
| `git clone` | Download a repository |
| `git pull` | Fetch latest changes |
| `git branch` | View branches |
| `git checkout` | Switch or create branches |
| `git --version` | Verify Git installation |
| `java --version` | Verify Java installation |
| `docker --version` | Verify Docker installation |

---

# CI/CD Workflow Commands

A typical workflow follows these commands:

```text
git status
        │
git add .
        │
git commit -m "message"
        │
git push origin main
        │
GitHub Repository
        │
CI/CD Pipeline Triggered
        │
Build
        │
Test
        │
Deploy
```

---

# Notes

- Commit small and meaningful changes.
- Write descriptive commit messages.
- Push code frequently.
- The CI/CD pipeline automatically starts after a successful push (if configured).
- Avoid committing sensitive files such as `.env`, API keys, or passwords.