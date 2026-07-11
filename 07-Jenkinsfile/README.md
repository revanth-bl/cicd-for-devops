# Episode 07 - Jenkinsfile

## Overview

A **Jenkinsfile** is the heart of a Jenkins Pipeline. It defines the entire Continuous Integration and Continuous Delivery (CI/CD) workflow as code using a Groovy-based syntax.

Instead of manually configuring jobs through the Jenkins web interface, developers write a Jenkinsfile and store it in the project's Git repository. This approach, known as **Pipeline as Code**, makes CI/CD workflows version-controlled, reproducible, and easier to maintain.

In this chapter, you'll learn the structure of a Jenkinsfile, its core directives, and how to build production-ready pipelines.

---

# Learning Objectives

After completing this chapter, you will be able to:

- Understand the purpose of a Jenkinsfile
- Differentiate between Declarative and Scripted Pipelines
- Learn the structure of a Jenkinsfile
- Use pipeline directives such as `agent`, `stages`, `steps`, `environment`, and `post`
- Create reusable and maintainable CI/CD pipelines
- Follow best practices for Pipeline as Code

---

# What is a Jenkinsfile?

A Jenkinsfile is a plain text file that contains the instructions Jenkins follows to build, test, and deploy an application.

The file is written using **Groovy DSL (Domain-Specific Language)** and is stored alongside the application's source code.

Example project structure:

```text
project/
│
├── src/
├── tests/
├── Dockerfile
├── pom.xml
└── Jenkinsfile
```

---

# Why Use a Jenkinsfile?

Using a Jenkinsfile provides several advantages:

- Pipeline configuration is stored in Git.
- Changes are tracked through version control.
- Team members can review pipeline updates.
- Pipelines become portable across Jenkins servers.
- CI/CD workflows become reproducible and easier to maintain.

---

# Jenkinsfile Workflow

```text
Developer
     │
     ▼
Write Jenkinsfile
     │
     ▼
Commit Changes
     │
     ▼
Push to Git Repository
     │
     ▼
Jenkins Detects Changes
     │
     ▼
Read Jenkinsfile
     │
     ▼
Execute Pipeline
     │
     ▼
Build
     │
     ▼
Test
     │
     ▼
Deploy
```

---

# Types of Jenkins Pipelines

## Declarative Pipeline

Declarative Pipelines use a structured syntax and are recommended for most projects.

Example:

```groovy
pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                echo 'Building Application'
            }
        }
    }
}
```

### Advantages

- Easy to read
- Standardized syntax
- Easier maintenance
- Better validation

---

## Scripted Pipeline

Scripted Pipelines use pure Groovy scripting and provide greater flexibility.

Example:

```groovy
node {
    stage('Build') {
        echo 'Building Application'
    }
}
```

### Advantages

- Highly customizable
- Suitable for advanced workflows

---

# Structure of a Jenkinsfile

A typical Declarative Pipeline contains:

```groovy
pipeline {

    agent any

    environment {

    }

    tools {

    }

    options {

    }

    parameters {

    }

    stages {

        stage('Build') {

            steps {

            }

        }

    }

    post {

    }

}
```

---

# Pipeline Directives

## pipeline

The root block that contains the entire CI/CD workflow.

---

## agent

Defines where the pipeline executes.

Example:

```groovy
agent any
```

---

## environment

Stores reusable environment variables.

Example:

```groovy
environment {
    APP_NAME = "DemoApp"
}
```

---

## tools

Configures build tools.

Example:

```groovy
tools {
    jdk 'JDK17'
    maven 'Maven3'
}
```

---

## options

Defines pipeline execution behavior.

Common options include:

- timeout
- retry
- timestamps
- disableConcurrentBuilds

---

## parameters

Allows user input before pipeline execution.

Example:

```groovy
parameters {
    string(name: 'VERSION', defaultValue: '1.0.0')
}
```

---

## stages

Stages divide the pipeline into logical sections.

Typical stages include:

- Checkout
- Build
- Test
- Package
- Deploy

---

## steps

Steps contain the commands executed within a stage.

Linux example:

```groovy
sh 'pwd'
```

Windows example:

```groovy
bat 'dir'
```

---

## post

Defines actions that execute after the pipeline completes.

Example:

```groovy
post {
    success {
        echo 'Pipeline completed successfully.'
    }

    failure {
        echo 'Pipeline failed.'
    }

    always {
        cleanWs()
    }
}
```

---

# Sample Jenkinsfile

```groovy
pipeline {

    agent any

    environment {
        APP_NAME = "DemoApp"
    }

    stages {

        stage('Build') {
            steps {
                echo "Building ${APP_NAME}"
            }
        }

        stage('Test') {
            steps {
                echo "Running Tests"
            }
        }

        stage('Deploy') {
            steps {
                echo "Deploying ${APP_NAME}"
            }
        }

    }

    post {

        success {
            echo "Build Successful"
        }

        failure {
            echo "Build Failed"
        }

        always {
            cleanWs()
        }

    }

}
```

---

# Declarative vs Scripted Pipeline

| Feature | Declarative | Scripted |
|----------|-------------|-----------|
| Syntax | Structured | Groovy |
| Learning Curve | Easy | Advanced |
| Readability | High | Moderate |
| Flexibility | Moderate | High |
| Recommended | Yes | Advanced Use Cases |

---

# Best Practices

- Store the Jenkinsfile in the repository root.
- Use Declarative Pipelines whenever possible.
- Keep stages small and focused.
- Use meaningful stage names.
- Store secrets using Jenkins Credentials.
- Avoid hardcoding sensitive information.
- Validate pipeline syntax before committing.
- Review Console Output after every build.
- Keep pipelines modular and reusable.

---

# Common Mistakes

- Placing the Jenkinsfile in the wrong directory.
- Missing braces or incorrect Groovy syntax.
- Hardcoding passwords or API keys.
- Using `bat` commands on Linux agents.
- Using `sh` commands on Windows agents.
- Combining multiple responsibilities into a single stage.

---

# Advantages

- Pipeline as Code
- Version Controlled
- Reusable
- Portable
- Easy Collaboration
- Production Ready
- Supports Complex CI/CD Workflows

---

# Key Takeaways

- A Jenkinsfile defines an entire CI/CD pipeline as code.
- It should be stored in the root of the Git repository.
- Declarative Pipelines are recommended for most projects.
- Organizing work into stages improves readability and maintainability.
- Pipeline as Code is a fundamental DevOps practice for building reliable and scalable automation.

---

# References

- Jenkins Official Documentation
- Jenkins Pipeline Syntax Reference
- Groovy Language Documentation

---

# Next Topic

➡️ **Episode 08 – Jenkins Agents**

In the next chapter, you'll learn how Jenkins distributes workloads using **Agents (Nodes)**, configure distributed builds, understand the Controller-Agent architecture, and execute pipelines across multiple machines.