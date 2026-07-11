# Episode 06 - Jenkins Pipeline

## Overview

A Jenkins Pipeline is a suite of automated processes that defines how software is built, tested, and deployed. Unlike Freestyle Projects, Pipelines are written as code in a **Jenkinsfile**, allowing teams to version-control, review, and reuse their CI/CD workflows.

This approach, known as **Pipeline as Code**, is the preferred method for implementing Continuous Integration and Continuous Delivery in modern DevOps environments.

---

# Learning Objectives

After completing this chapter, you will be able to:

- Understand Pipeline as Code
- Create a Jenkins Pipeline
- Write a basic Declarative Pipeline
- Understand the structure of a Jenkinsfile
- Execute a pipeline
- View pipeline stages and logs
- Compare Freestyle Projects with Pipelines

---

# What is a Jenkins Pipeline?

A Jenkins Pipeline is an automated workflow that defines the complete software delivery process.

Instead of manually configuring jobs through the Jenkins UI, every stage is written inside a **Jenkinsfile** stored in the project's Git repository.

Typical pipeline stages include:

- Checkout
- Build
- Test
- Package
- Deploy
- Notify

---

# Why Pipelines?

Freestyle Projects become difficult to maintain as applications grow.

Pipelines solve this problem by:

- Storing configuration in Git
- Supporting code reviews
- Enabling reusable workflows
- Automating deployments
- Improving collaboration
- Simplifying maintenance

---

# Pipeline as Code

Pipeline as Code means storing the CI/CD workflow alongside the application source code.

Example:

```text
Project/
│
├── src/
├── tests/
├── Dockerfile
└── Jenkinsfile
```

Whenever the project changes, the pipeline evolves with it.

---

# Jenkinsfile

A **Jenkinsfile** defines every step of the CI/CD process using the Groovy-based Declarative Pipeline syntax.

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

Store the `Jenkinsfile` in the root directory of your repository.

---

# Pipeline Workflow

```text
Developer
     │
     ▼
Write Code
     │
     ▼
Git Commit
     │
     ▼
Push to GitHub
     │
     ▼
Jenkins Pipeline Triggered
     │
     ▼
Checkout Source Code
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
     │
     ▼
Notification
```

---

# Pipeline Structure

A Declarative Pipeline consists of the following sections:

```groovy
pipeline {

    agent any

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

# Agent

The **agent** specifies where the pipeline executes.

Example:

```groovy
agent any
```

Other options include:

- Specific node
- Docker container
- Kubernetes Pod

---

# Stages

Stages divide the pipeline into logical phases.

Typical stages:

- Checkout
- Build
- Test
- Package
- Deploy

Example:

```groovy
stage('Build')
```

Each stage should perform a single responsibility.

---

# Steps

Steps define the commands executed within a stage.

Linux example:

```groovy
sh 'pwd'
```

Windows example:

```groovy
bat 'dir'
```

Display a message:

```groovy
echo 'Hello Jenkins'
```

---

# Post Section

The `post` block runs after pipeline execution.

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
        echo 'Pipeline finished.'
    }

}
```

---

# Creating Your First Pipeline

## Step 1

Open Jenkins Dashboard.

```
http://localhost:8080
```

---

## Step 2

Click:

```
New Item
```

---

## Step 3

Enter a project name.

Example:

```
Hello-Pipeline
```

Select:

```
Pipeline
```

Click **OK**.

---

## Step 4

Under **Pipeline**, choose:

```
Pipeline Script
```

Paste the following:

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

Save the job.

---

## Step 5

Click:

```
Build Now
```

---

## Step 6

Open:

```
Build History
```

↓

```
Console Output
```

Example output:

```text
Started by user admin

[Pipeline] Start of Pipeline

Hello, Jenkins Pipeline!

Finished: SUCCESS
```

---

# Pipeline Visualization

```text
Pipeline

✔ Checkout

✔ Build

✔ Test

✔ Deploy
```

Each completed stage is marked as successful.

---

# Declarative vs Scripted Pipeline

| Feature | Declarative | Scripted |
|----------|-------------|-----------|
| Syntax | Simple | Advanced |
| Learning Curve | Easy | Moderate |
| Flexibility | Good | Excellent |
| Recommended | Yes | Advanced Use Cases |

---

# Pipeline vs Freestyle Project

| Feature | Freestyle | Pipeline |
|----------|------------|-----------|
| Configuration | GUI | Code |
| Git Integration | Limited | Excellent |
| Version Control | No | Yes |
| Reusability | Low | High |
| Scalability | Limited | Excellent |
| Production Ready | Limited | Yes |

---

# Best Practices

- Store the Jenkinsfile in Git.
- Keep stages small and focused.
- Use meaningful stage names.
- Avoid hardcoding secrets.
- Use Jenkins Credentials.
- Review Console Output after every build.
- Keep pipelines modular.
- Test pipelines in a development environment first.

---

# Advantages

- Pipeline as Code
- Version controlled
- Reusable
- Easy collaboration
- Better debugging
- Supports parallel execution
- Production-ready automation

---

# Limitations

- Requires basic Groovy knowledge
- More complex than Freestyle Projects
- Advanced pipelines can become difficult to maintain without proper structure

---

# Key Takeaways

- A Jenkins Pipeline automates the software delivery process using a **Jenkinsfile**.
- Pipelines are stored in Git, enabling version control and collaboration.
- Declarative Pipelines are recommended for most projects because they are easier to read and maintain.
- Organizing work into stages improves visibility and simplifies troubleshooting.
- Pipeline as Code is the standard approach for modern CI/CD workflows.

---

# References

- Jenkins Official Documentation
- Jenkins Pipeline Syntax Reference
- Jenkins User Handbook
- Groovy Language Documentation

---

# Next Topic

➡️ **Episode 07 – Jenkinsfile**

In the next chapter, we will explore the **Jenkinsfile** in detail, understand its syntax, directives, stages, environment variables, parameters, and learn how to build production-ready CI/CD pipelines.