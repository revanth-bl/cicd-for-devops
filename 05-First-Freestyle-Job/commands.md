# Commands

This section covers the commands commonly used while creating and running your first Jenkins Freestyle Project.

---

# Verify Jenkins Service

Linux

```bash
sudo systemctl status jenkins
```

Windows

```powershell
Get-Service Jenkins
```

---

# Open Jenkins Dashboard

```text
http://localhost:8080
```

---

# Check Git Installation

```bash
git --version
```

---

# Check Java Installation

```bash
java --version
```

---

# Clone a Git Repository

```bash
git clone https://github.com/username/repository.git
```

---

# Check Repository Status

```bash
git status
```

---

# Pull Latest Changes

```bash
git pull origin main
```

---

# Basic Linux Shell Commands

Print current directory:

```bash
pwd
```

List files:

```bash
ls -la
```

Display current user:

```bash
whoami
```

Display current date:

```bash
date
```

Display system hostname:

```bash
hostname
```

Print text:

```bash
echo "Hello Jenkins!"
```

Display environment variables:

```bash
printenv
```

---

# Windows Batch Commands

Print text:

```cmd
echo Hello Jenkins!
```

Display current directory:

```cmd
cd
```

List files:

```cmd
dir
```

Display username:

```cmd
whoami
```

Display hostname:

```cmd
hostname
```

---

# Simple Build Step (Linux)

Example shell script executed by a Freestyle Job:

```bash
echo "Build Started..."
pwd
ls -la
echo "Build Completed Successfully."
```

---

# Simple Build Step (Windows)

```cmd
echo Build Started...
dir
echo Build Completed Successfully.
```

---

# Verify Workspace

Linux

```bash
pwd
```

Windows

```cmd
cd
```

---

# View Jenkins Logs

Linux

```bash
sudo journalctl -u jenkins -f
```

---

# Restart Jenkins

Linux

```bash
sudo systemctl restart jenkins
```

Windows

```powershell
Restart-Service Jenkins
```

---

# Useful Git Commands

Clone repository:

```bash
git clone <repository-url>
```

View commit history:

```bash
git log --oneline
```

Check branch:

```bash
git branch
```

---

# Common Build Commands

Linux

```bash
echo "Starting Build"
```

```bash
pwd
```

```bash
ls
```

```bash
date
```

Windows

```cmd
echo Starting Build
```

```cmd
dir
```

```cmd
date /T
```

---

# Summary

| Command | Purpose |
|----------|---------|
| `git clone` | Clone a repository |
| `git status` | View repository status |
| `git pull` | Pull latest changes |
| `pwd` | Show current directory |
| `ls -la` | List files |
| `whoami` | Display current user |
| `hostname` | Show system hostname |
| `date` | Display current date |
| `echo` | Print text |
| `printenv` | View environment variables |
| `systemctl status jenkins` | Check Jenkins service |
| `journalctl -u jenkins -f` | View Jenkins logs |

---

# Notes

- A Freestyle Project is the simplest Jenkins job type.
- Build steps can execute Shell scripts (Linux/macOS) or Batch commands (Windows).
- Every build generates a workspace where source code and build artifacts are stored.
- Console Output is the primary place to debug build failures.