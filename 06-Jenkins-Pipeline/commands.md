# Commands

This section contains commonly used commands and pipeline snippets for creating and managing Jenkins Pipelines.

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

# Verify Git Installation

```bash
git --version
```

---

# Verify Java Installation

```bash
java --version
```

---

# Clone a Repository

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

# Create a Jenkinsfile

Linux

```bash
touch Jenkinsfile
```

Windows PowerShell

```powershell
New-Item Jenkinsfile -ItemType File
```

---

# Basic Declarative Pipeline

```groovy
pipeline {
    agent any

    stages {
        stage('Hello') {
            steps {
                echo 'Hello, Jenkins Pipeline!'
            }
        }
    }
}
```

---

# Multiple Stages Example

```groovy
pipeline {
    agent any

    stages {

        stage('Build') {
            steps {
                echo 'Building Application'
            }
        }

        stage('Test') {
            steps {
                echo 'Running Tests'
            }
        }

        stage('Deploy') {
            steps {
                echo 'Deploying Application'
            }
        }

    }
}
```

---

# Execute Linux Commands

```groovy
sh 'pwd'
```

```groovy
sh 'ls -la'
```

```groovy
sh 'whoami'
```

```groovy
sh 'date'
```

---

# Execute Windows Commands

```groovy
bat 'dir'
```

```groovy
bat 'whoami'
```

```groovy
bat 'hostname'
```

---

# Print Message

```groovy
echo 'Pipeline Started'
```

---

# Display Environment Variables

Linux

```groovy
sh 'printenv'
```

Windows

```groovy
bat 'set'
```

---

# Git Checkout

```groovy
git url: 'https://github.com/username/repository.git', branch: 'main'
```

---

# Archive Artifacts

```groovy
archiveArtifacts artifacts: '**/*.jar'
```

---

# Always Execute a Step

```groovy
post {
    always {
        echo 'Pipeline Finished'
    }
}
```

---

# Success Action

```groovy
post {
    success {
        echo 'Build Successful'
    }
}
```

---

# Failure Action

```groovy
post {
    failure {
        echo 'Build Failed'
    }
}
```

---

# Clean Workspace

```groovy
cleanWs()
```

---

# View Console Output

```text
Build History → Console Output
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

# View Jenkins Logs

Linux

```bash
sudo journalctl -u jenkins -f
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

Check current branch:

```bash
git branch
```

---

# Summary

| Command | Purpose |
|----------|---------|
| `touch Jenkinsfile` | Create a Jenkinsfile |
| `git clone` | Clone a Git repository |
| `git status` | Check repository status |
| `git pull` | Pull latest changes |
| `echo` | Print a message in the pipeline |
| `sh` | Execute Linux shell commands |
| `bat` | Execute Windows batch commands |
| `archiveArtifacts` | Save build artifacts |
| `cleanWs()` | Clean the workspace |
| `systemctl restart jenkins` | Restart Jenkins |
| `journalctl -u jenkins -f` | View Jenkins logs |

---

# Notes

- A **Jenkinsfile** defines the entire CI/CD pipeline as code.
- Declarative Pipelines are the recommended approach for most projects.
- Store the `Jenkinsfile` in the root of your Git repository.
- Use `sh` for Linux/macOS agents and `bat` for Windows agents.
- The `post` section allows actions to run after the pipeline completes, regardless of success or failure.