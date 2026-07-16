# 06 — Jenkins Pipeline

This section introduces Jenkins Pipelines and explains how to automate software delivery using a Pipeline as Code approach.

Instead of manually configuring every build step through the Jenkins Dashboard, a Pipeline allows the entire CI/CD workflow to be defined as code.

---

# What Is a Jenkins Pipeline?

A Jenkins Pipeline is an automated sequence of steps used to build, test, and deploy an application.

A basic Pipeline looks like this:

```text
Source Code
    │
    ▼
Checkout
    │
    ▼
Build
    │
    ▼
Test
    │
    ▼
Package
    │
    ▼
Deploy
```

Jenkins executes these steps automatically.

---

# Traditional Jenkins Job vs Pipeline

## Freestyle Job

In a Freestyle Job, configuration is mainly performed through the Jenkins web interface.

```text
Jenkins Dashboard
        │
        ▼
Configure Job Manually
        │
        ▼
Build Steps
        │
        ▼
Execute Build
```

This can become difficult to manage as the project grows.

---

## Jenkins Pipeline

A Pipeline defines the workflow as code:

```text
Jenkinsfile
     │
     ▼
Pipeline
     │
     ├── Build
     ├── Test
     ├── Package
     └── Deploy
```

The Pipeline can be stored in a Git repository and version controlled.

---

# Pipeline as Code

The Pipeline as Code approach means that the CI/CD workflow is stored as a file.

The most common file is:

```text
Jenkinsfile
```

Example:

```text
Project Repository
        │
        ├── application/
        │
        ├── Dockerfile
        │
        └── Jenkinsfile
```

This allows the pipeline configuration to be:

- Version controlled
- Reviewed
- Shared
- Modified through Git
- Reused by different environments

---

# Basic Jenkins Pipeline

A simple Declarative Pipeline looks like this:

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

# Pipeline Structure

A Jenkins Declarative Pipeline usually contains:

```text
pipeline
    │
    ├── agent
    │
    ├── stages
    │       │
    │       ├── stage
    │       │
    │       ├── stage
    │       │
    │       └── stage
    │
    └── post
```

---

# Pipeline

The `pipeline` block contains the complete Jenkins Pipeline.

```groovy
pipeline {
    // Pipeline configuration
}
```

---

# Agent

The `agent` defines where the Pipeline will execute.

```groovy
agent any
```

This means Jenkins can use any available agent.

Example:

```groovy
pipeline {

    agent any

    stages {
        // Stages
    }

}
```

The agent is the machine or environment that executes the actual Pipeline commands.

---

# Stages

The `stages` block contains the different phases of the Pipeline.

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

}
```

A Pipeline usually separates different responsibilities into different stages.

---

# Stage

A `stage` represents a specific phase of the CI/CD workflow.

Examples:

```text
Build
  ↓
Test
  ↓
Package
  ↓
Deploy
```

Example:

```groovy
stage('Build') {
    steps {
        echo 'Building application'
    }
}
```

---

# Steps

The `steps` block contains the commands Jenkins executes.

Example:

```groovy
steps {
    echo 'Hello Jenkins'
}
```

Shell command:

```groovy
steps {
    sh 'ls -la'
}
```

---

# Pipeline Execution Flow

A Jenkins Pipeline normally executes stages sequentially:

```text
Stage 1: Checkout
        │
        ▼
Stage 2: Build
        │
        ▼
Stage 3: Test
        │
        ▼
Stage 4: Package
        │
        ▼
Stage 5: Deploy
```

If a stage fails, the following stages normally do not execute.

Example:

```text
Build
  │
  ▼
Test ❌
  │
  ✕
Deploy does not run
```

This prevents broken code from continuing through the deployment process.

---

# Jenkins Pipeline with Docker

Jenkins Pipelines can use Docker to build and run applications.

The workflow looks like this:

```text
Jenkins Pipeline
        │
        ▼
Build Application
        │
        ▼
Run Tests
        │
        ▼
Build Docker Image
        │
        ▼
Run Container
        │
        ▼
Deploy Application
```

Example:

```groovy
pipeline {

    agent any

    stages {

        stage('Build Docker Image') {
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

Docker must be installed on the machine or Jenkins Agent executing the Pipeline.

---

# Multi-Stage Pipeline

A Pipeline can contain multiple stages:

```groovy
pipeline {

    agent any

    stages {

        stage('Checkout') {
            steps {
                echo 'Checking out source code'
            }
        }

        stage('Build') {
            steps {
                echo 'Building application'
            }
        }

        stage('Test') {
            steps {
                echo 'Running tests'
            }
        }

        stage('Deploy') {
            steps {
                echo 'Deploying application'
            }
        }

    }

}
```

This creates a clear and organized CI/CD workflow.

---

# Pipeline Environment Variables

Environment variables can be defined inside a Pipeline.

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

Environment variables are useful for storing configuration values.

---

# Pipeline Options

Pipeline options can control how a Pipeline behaves.

Example timeout:

```groovy
options {
    timeout(time: 20, unit: 'MINUTES')
}
```

Example:

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

---

# Post Actions

The `post` block runs after the Pipeline or a stage finishes.

Example:

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

Example flow:

```text
Pipeline
    │
    ▼
Success
    │
    ▼
post → success
```

or:

```text
Pipeline
    │
    ▼
Failure
    │
    ▼
post → failure
```

---

# Pipeline as Code Workflow

A typical workflow looks like this:

```text
Developer
    │
    ▼
Modify Jenkinsfile
    │
    ▼
Git Commit
    │
    ▼
Git Push
    │
    ▼
Jenkins
    │
    ▼
Read Jenkinsfile
    │
    ▼
Execute Pipeline
```

The Pipeline configuration is stored together with the application source code.

---

# Jenkins Pipeline with GitHub

A common CI/CD workflow is:

```text
Developer
    │
    ▼
Push Code to GitHub
    │
    ▼
Jenkins Triggered
    │
    ▼
Checkout Repository
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
Deploy
```

This creates an automated CI/CD workflow.

---

# Why Use Pipelines?

Jenkins Pipelines provide several advantages:

- Pipeline configuration is stored as code.
- Changes can be tracked with Git.
- Pipelines can be reviewed.
- Pipelines can be reused.
- Complex workflows can be automated.
- Manual configuration is reduced.
- CI/CD workflows become easier to reproduce.

---

# Pipeline vs Freestyle Jobs

| Feature | Freestyle Job | Pipeline |
|---|---|---|
| Configuration | Jenkins UI | Code |
| Version Control | Limited | Yes |
| Complex Workflows | Difficult | Easy |
| Reusability | Limited | High |
| Code Review | Difficult | Easy |
| Multi-Stage Workflows | Limited | Supported |
| Pipeline as Code | No | Yes |

---

# Learning Outcome

After completing this section, you should understand:

- What a Jenkins Pipeline is.
- The difference between Freestyle Jobs and Pipelines.
- What Pipeline as Code means.
- The purpose of a Jenkinsfile.
- The purpose of agents.
- The purpose of stages and steps.
- How Pipelines execute sequentially.
- How Jenkins can use Docker.
- How environment variables work.
- How post actions work.
- How Jenkins can automate a CI/CD workflow.

The next step is to learn how to create and manage a `Jenkinsfile`.