# Commands

This section contains commonly used commands and Jenkins Pipeline snippets for creating, running, and troubleshooting Jenkins Pipelines.

---

# Verify Jenkins Service

Check Jenkins status:

```bash
sudo systemctl status jenkins
```

Start Jenkins:

```bash
sudo systemctl start jenkins
```

Restart Jenkins:

```bash
sudo systemctl restart jenkins
```

---

# Verify Java

```bash
java --version
```

---

# Verify Docker

```bash
docker --version
```

Check Docker service:

```bash
sudo systemctl status docker
```

Test Docker access as Jenkins:

```bash
sudo -u jenkins docker ps
```

---

# Verify Docker Compose

```bash
docker compose version
```

Test Docker Compose as Jenkins:

```bash
sudo -u jenkins docker compose version
```

---

# Git Commands

Clone a repository:

```bash
git clone https://github.com/username/project.git
```

Navigate to the project:

```bash
cd project
```

Check repository status:

```bash
git status
```

Pull the latest changes:

```bash
git pull origin main
```

View commit history:

```bash
git log --oneline
```

---

# Basic Jenkins Pipeline

```groovy
pipeline {

    agent any

    stages {

        stage('Build') {
            steps {
                echo 'Building application...'
            }
        }

        stage('Test') {
            steps {
                echo 'Running tests...'
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

# Pipeline with Shell Commands

Linux:

```groovy
pipeline {

    agent any

    stages {

        stage('System Information') {
            steps {
                sh 'whoami'
                sh 'pwd'
                sh 'ls -la'
            }
        }

    }

}
```

Windows:

```groovy
pipeline {

    agent any

    stages {

        stage('System Information') {
            steps {
                bat 'whoami'
                bat 'cd'
                bat 'dir'
            }
        }

    }

}
```

---

# Common Shell Commands in Jenkins

Print the current user:

```groovy
sh 'whoami'
```

Print the current directory:

```groovy
sh 'pwd'
```

List files:

```groovy
sh 'ls -la'
```

Print environment variables:

```groovy
sh 'printenv'
```

---

# Windows Commands in Jenkins

Print the current user:

```groovy
bat 'whoami'
```

Display the current directory:

```groovy
bat 'cd'
```

List files:

```groovy
bat 'dir'
```

Display environment variables:

```groovy
bat 'set'
```

---

# Jenkins Pipeline with Git

```groovy
pipeline {

    agent any

    stages {

        stage('Checkout') {
            steps {
                git branch: 'main',
                    url: 'https://github.com/username/project.git'
            }
        }

    }

}
```

---

# Checkout Source Code

Using the Jenkins Pipeline checkout step:

```groovy
pipeline {

    agent any

    stages {

        stage('Checkout') {
            steps {
                checkout scm
            }
        }

    }

}
```

---

# Build Pipeline

```groovy
pipeline {

    agent any

    stages {

        stage('Build') {
            steps {
                sh 'mvn clean package'
            }
        }

    }

}
```

Windows:

```groovy
pipeline {

    agent any

    stages {

        stage('Build') {
            steps {
                bat 'mvn clean package'
            }
        }

    }

}
```

---

# Test Pipeline

```groovy
pipeline {

    agent any

    stages {

        stage('Test') {
            steps {
                sh 'mvn test'
            }
        }

    }

}
```

---

# Docker Pipeline

Build a Docker image:

```groovy
pipeline {

    agent any

    stages {

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t my-app .'
            }
        }

    }

}
```

Run a Docker container:

```groovy
pipeline {

    agent any

    stages {

        stage('Run Container') {
            steps {
                sh 'docker run -d -p 8080:8080 my-app'
            }
        }

    }

}
```

---

# Docker Pipeline with Build and Run

```groovy
pipeline {

    agent any

    stages {

        stage('Build Image') {
            steps {
                sh 'docker build -t my-app .'
            }
        }

        stage('Run Container') {
            steps {
                sh 'docker run -d -p 8080:8080 my-app'
            }
        }

    }

}
```

---

# Docker Compose Pipeline

Start services:

```groovy
stage('Deploy') {
    steps {
        sh 'docker compose up -d --build'
    }
}
```

Stop services:

```groovy
stage('Cleanup') {
    steps {
        sh 'docker compose down'
    }
}
```

Check running services:

```groovy
stage('Verify') {
    steps {
        sh 'docker compose ps'
    }
}
```

---

# Environment Variables

Define environment variables:

```groovy
pipeline {

    agent any

    environment {
        APP_NAME = 'my-app'
        ENVIRONMENT = 'production'
    }

    stages {

        stage('Display Variables') {
            steps {
                echo "Application: ${APP_NAME}"
                echo "Environment: ${ENVIRONMENT}"
            }
        }

    }

}
```

---

# Build Environment Variables

Jenkins provides built-in environment variables.

Print all environment variables:

```groovy
sh 'printenv'
```

Print the current build number:

```groovy
echo "${BUILD_NUMBER}"
```

Print the job name:

```groovy
echo "${JOB_NAME}"
```

Print the workspace:

```groovy
echo "${WORKSPACE}"
```

---

# Pipeline Options

Set a timeout:

```groovy
pipeline {

    agent any

    options {
        timeout(time: 20, unit: 'MINUTES')
    }

    stages {
        // Stages
    }

}
```

Disable concurrent builds:

```groovy
options {
    disableConcurrentBuilds()
}
```

Keep only a limited number of builds:

```groovy
options {
    buildDiscarder(
        logRotator(
            numToKeepStr: '10'
        )
    )
}
```

---

# Post Actions

Run commands after the Pipeline finishes:

```groovy
post {

    always {
        echo 'Pipeline finished'
    }

    success {
        echo 'Pipeline succeeded'
    }

    failure {
        echo 'Pipeline failed'
    }

}
```

---

# Complete Pipeline Example

```groovy
pipeline {

    agent any

    environment {
        APP_NAME = 'my-app'
    }

    stages {

        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Build') {
            steps {
                echo "Building ${APP_NAME}"
            }
        }

        stage('Test') {
            steps {
                echo 'Running tests'
            }
        }

        stage('Docker Build') {
            steps {
                sh "docker build -t ${APP_NAME} ."
            }
        }

    }

    post {

        always {
            echo 'Pipeline completed'
        }

        success {
            echo 'Pipeline succeeded'
        }

        failure {
            echo 'Pipeline failed'
        }

    }

}
```

---

# Jenkins Pipeline Commands

Run a Pipeline from the Jenkins CLI:

```bash
java -jar jenkins-cli.jar -s http://localhost:8080 build <job-name>
```

View Jenkins jobs:

```bash
java -jar jenkins-cli.jar -s http://localhost:8080 list-jobs
```

Get Jenkins version:

```bash
java -jar jenkins-cli.jar -s http://localhost:8080 version
```

---

# Workspace Commands

Display the workspace:

```groovy
sh 'pwd'
```

List workspace files:

```groovy
sh 'ls -la'
```

Clean the workspace:

```groovy
cleanWs()
```

---

# Archive Build Artifacts

Archive JAR files:

```groovy
archiveArtifacts artifacts: '**/target/*.jar'
```

Archive ZIP files:

```groovy
archiveArtifacts artifacts: '**/*.zip'
```

Archive WAR files:

```groovy
archiveArtifacts artifacts: '**/*.war'
```

---

# Publish Test Results

Publish JUnit test results:

```groovy
junit '**/target/surefire-reports/*.xml'
```

---

# Retry Failed Steps

Retry a command:

```groovy
retry(3) {
    sh 'some-command'
}
```

Example:

```groovy
stage('Build') {
    steps {
        retry(3) {
            sh 'mvn clean package'
        }
    }
}
```

---

# Timeout a Stage

```groovy
stage('Build') {

    options {
        timeout(time: 10, unit: 'MINUTES')
    }

    steps {
        sh 'mvn clean package'
    }

}
```

---

# Useful Git Commands

Add changes:

```bash
git add .
```

Commit changes:

```bash
git commit -m "Update Jenkins Pipeline"
```

Push changes:

```bash
git push origin main
```

---

# Validate Docker Access Before Running a Pipeline

Check Docker:

```bash
docker --version
```

Check Docker service:

```bash
sudo systemctl status docker
```

Check Jenkins Docker access:

```bash
sudo -u jenkins docker ps
```

Check Docker Compose:

```bash
sudo -u jenkins docker compose version
```

---

# Summary

| Command / Directive | Purpose |
|---------------------|---------|
| `pipeline` | Defines a Declarative Pipeline |
| `agent` | Defines where the Pipeline runs |
| `stages` | Contains Pipeline stages |
| `stage` | Defines one phase of the Pipeline |
| `steps` | Contains commands to execute |
| `sh` | Executes Linux shell commands |
| `bat` | Executes Windows commands |
| `echo` | Prints a message |
| `checkout scm` | Checks out source code |
| `environment` | Defines environment variables |
| `options` | Configures Pipeline behavior |
| `post` | Runs actions after Pipeline execution |
| `archiveArtifacts` | Saves build artifacts |
| `junit` | Publishes test reports |
| `cleanWs()` | Cleans the Jenkins workspace |
| `retry()` | Retries failed steps |
| `timeout()` | Stops long-running operations |
| `docker build` | Builds a Docker image |
| `docker run` | Runs a Docker container |
| `docker compose up` | Starts Compose services |
| `docker compose down` | Stops Compose services |