# Commands

This section contains commonly used Jenkinsfile syntax, directives, and pipeline snippets.

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

# Basic Jenkinsfile

```groovy
pipeline {
    agent any

    stages {
        stage('Hello') {
            steps {
                echo 'Hello, Jenkins!'
            }
        }
    }
}
```

---

# Agent Directive

Run on any available agent:

```groovy
agent any
```

Run on a specific node:

```groovy
agent {
    label 'linux'
}
```

Run inside Docker:

```groovy
agent {
    docker {
        image 'node:20'
    }
}
```

---

# Environment Variables

```groovy
environment {
    APP_NAME = "DevOps-App"
    VERSION = "1.0.0"
}
```

Access variables:

```groovy
echo "${APP_NAME}"
```

Linux:

```groovy
sh 'echo $APP_NAME'
```

Windows:

```groovy
bat 'echo %APP_NAME%'
```

---

# Stages

```groovy
stages {

    stage('Build') {
        steps {
            echo 'Building...'
        }
    }

    stage('Test') {
        steps {
            echo 'Testing...'
        }
    }

    stage('Deploy') {
        steps {
            echo 'Deploying...'
        }
    }

}
```

---

# Shell Commands (Linux)

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

# Batch Commands (Windows)

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

# Git Checkout

```groovy
git branch: 'main',
    url: 'https://github.com/username/repository.git'
```

---

# Tools Directive

```groovy
tools {
    jdk 'JDK17'
    maven 'Maven3'
}
```

---

# Parameters

```groovy
parameters {
    string(name: 'APP_NAME', defaultValue: 'Demo')
}
```

Boolean parameter:

```groovy
booleanParam(
    name: 'RUN_TESTS',
    defaultValue: true
)
```

Choice parameter:

```groovy
choice(
    name: 'ENV',
    choices: ['dev', 'test', 'prod']
)
```

---

# Conditional Execution

```groovy
when {
    branch 'main'
}
```

Branch example:

```groovy
when {
    anyOf {
        branch 'main'
        branch 'develop'
    }
}
```

---

# Post Actions

Always execute:

```groovy
post {
    always {
        echo 'Pipeline Finished'
    }
}
```

Success:

```groovy
post {
    success {
        echo 'Success'
    }
}
```

Failure:

```groovy
post {
    failure {
        echo 'Failed'
    }
}
```

---

# Archive Artifacts

```groovy
archiveArtifacts artifacts: '**/*.jar'
```

---

# Clean Workspace

```groovy
cleanWs()
```

---

# Timeout

```groovy
options {
    timeout(time: 30, unit: 'MINUTES')
}
```

---

# Retry

```groovy
options {
    retry(3)
}
```

---

# Disable Concurrent Builds

```groovy
options {
    disableConcurrentBuilds()
}
```

---

# Input Approval

```groovy
input {
    message "Deploy to Production?"
    ok "Deploy"
}
```

---

# Parallel Stages

```groovy
parallel {

    stage('Unit Tests') {
        steps {
            echo 'Running Unit Tests'
        }
    }

    stage('Integration Tests') {
        steps {
            echo 'Running Integration Tests'
        }
    }

}
```

---

# Complete Pipeline Example

```groovy
pipeline {

    agent any

    environment {
        APP = "Demo"
    }

    stages {

        stage('Build') {
            steps {
                echo "Building ${APP}"
            }
        }

        stage('Test') {
            steps {
                echo "Testing ${APP}"
            }
        }

        stage('Deploy') {
            steps {
                echo "Deploying ${APP}"
            }
        }

    }

    post {

        success {
            echo 'Build Successful'
        }

        failure {
            echo 'Build Failed'
        }

        always {
            cleanWs()
        }

    }

}
```

---

# Useful Git Commands

Clone repository:

```bash
git clone <repository-url>
```

Repository status:

```bash
git status
```

Pull latest changes:

```bash
git pull origin main
```

Commit changes:

```bash
git commit -m "Add Jenkinsfile"
```

Push changes:

```bash
git push origin main
```

---

# Summary

| Command / Directive | Purpose |
|---------------------|---------|
| `agent` | Select execution environment |
| `stages` | Define pipeline phases |
| `steps` | Execute commands |
| `environment` | Define variables |
| `tools` | Configure JDK, Maven, etc. |
| `parameters` | Accept user input |
| `when` | Conditional stage execution |
| `post` | Actions after pipeline completion |
| `archiveArtifacts` | Save build artifacts |
| `cleanWs()` | Clean workspace |
| `parallel` | Run stages simultaneously |
| `timeout` | Limit pipeline execution time |
| `retry()` | Retry failed stages |

---

# Notes

- Always store the **Jenkinsfile** in the root of your Git repository.
- Prefer **Declarative Pipelines** for readability and maintainability.
- Use **environment variables** instead of hardcoding values.
- Store secrets in **Jenkins Credentials**, not directly in the Jenkinsfile.
- Keep stages focused on a single responsibility to simplify debugging and maintenance.