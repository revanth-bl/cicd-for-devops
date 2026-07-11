# Commands

This section contains commonly used Jenkins Declarative Pipeline syntax and commands for creating a production-style Multi-Stage Pipeline.

---

# Verify Jenkins Installation

```bash
java -jar jenkins-cli.jar -s http://localhost:8080/ version
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

# Verify Maven Installation

```bash
mvn --version
```

---

# Verify Docker Installation

```bash
docker --version
```

---

# Clone Repository

```bash
git clone https://github.com/username/project.git
```

---

# Navigate to Project

```bash
cd project
```

---

# Basic Multi-Stage Pipeline

```groovy
pipeline {

    agent any

    stages {

        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Build') {
            steps {
                sh 'mvn clean package'
            }
        }

        stage('Test') {
            steps {
                sh 'mvn test'
            }
        }

        stage('Deploy') {
            steps {
                echo 'Deploying application...'
            }
        }

    }

}
```

---

# Build Docker Image

```groovy
stage('Docker Build') {
    steps {
        sh 'docker build -t my-app:v1 .'
    }
}
```

---

# Push Docker Image

```groovy
stage('Push Image') {
    steps {
        sh 'docker push username/my-app:v1'
    }
}
```

---

# Deploy Container

```groovy
stage('Deploy') {
    steps {
        sh 'docker run -d -p 8080:80 my-app:v1'
    }
}
```

---

# Environment Variables

```groovy
environment {

    APP_NAME = "DemoApp"
    IMAGE_NAME = "my-app"

}
```

---

# Pipeline Parameters

```groovy
parameters {

    string(name: 'VERSION', defaultValue: 'v1')

}
```

---

# Conditional Stage

```groovy
when {
    branch 'main'
}
```

---

# Retry Failed Stage

```groovy
options {

    retry(3)

}
```

---

# Timeout Pipeline

```groovy
options {

    timeout(time: 30, unit: 'MINUTES')

}
```

---

# Archive Artifacts

```groovy
archiveArtifacts artifacts: '**/target/*.jar'
```

---

# Publish Test Results

```groovy
junit '**/target/surefire-reports/*.xml'
```

---

# Clean Workspace

```groovy
cleanWs()
```

---

# Execute Shell Commands

Linux

```groovy
sh 'pwd'
```

Windows

```groovy
bat 'cd'
```

---

# Post Actions

```groovy
post {

    always {
        cleanWs()
    }

    success {
        echo 'Pipeline completed successfully.'
    }

    failure {
        echo 'Pipeline failed.'
    }

}
```

---

# Complete Pipeline Structure

```text
Checkout
     │
     ▼
Build
     │
     ▼
Test
     │
     ▼
Docker Build
     │
     ▼
Push Image
     │
     ▼
Deploy
     │
     ▼
Cleanup
```

---

# Git Commands

Stage changes

```bash
git add .
```

Commit changes

```bash
git commit -m "Add multi-stage pipeline"
```

Push changes

```bash
git push origin main
```

View commit history

```bash
git log --oneline
```

---

# Summary

| Command / Directive | Purpose |
|---------------------|---------|
| `checkout scm` | Clone source code |
| `mvn clean package` | Build application |
| `mvn test` | Execute tests |
| `docker build` | Build Docker image |
| `docker push` | Push image to registry |
| `archiveArtifacts` | Archive build artifacts |
| `junit` | Publish test reports |
| `cleanWs()` | Clean workspace |
| `post {}` | Execute post-build actions |
| `when {}` | Run stage conditionally |

---

# Notes

- Keep each pipeline stage focused on a single responsibility.
- Execute automated tests before deployment.
- Archive important build artifacts.
- Push Docker images only after successful builds.
- Use environment variables instead of hardcoding values.
- Add retry and timeout options to improve pipeline reliability.
- Always clean the workspace after pipeline execution.
- Store credentials securely using Jenkins Credentials.