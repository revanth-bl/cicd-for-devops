# Notes

## What is a Jenkins Pipeline?

A Jenkins Pipeline is a collection of automated steps that define the complete Continuous Integration and Continuous Delivery (CI/CD) workflow.

Instead of configuring jobs through the Jenkins UI, the entire workflow is written as code in a file called **Jenkinsfile**.

This approach is known as **Pipeline as Code**.

---

# Why Use Pipelines?

Traditional Freestyle Jobs:

- Configuration stored in Jenkins UI
- Difficult to version control
- Hard to reuse
- Limited flexibility

Pipeline Jobs:

- Stored in Git
- Easy to maintain
- Easy to review
- Supports complex workflows
- Ideal for production environments

---

# What is a Jenkinsfile?

A **Jenkinsfile** is a text file written in **Groovy DSL (Domain Specific Language)** that defines every stage of a CI/CD pipeline.

Example:

```groovy
pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                echo 'Building...'
            }
        }
    }
}
```

The Jenkinsfile should be stored in the root directory of the Git repository.

---

# Pipeline Workflow

```text
Developer
     │
     ▼
Git Commit
     │
     ▼
Git Push
     │
     ▼
Jenkins Detects Changes
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

# Pipeline Components

A Jenkins Pipeline typically contains:

- Agent
- Stages
- Steps
- Post Actions
- Environment Variables
- Parameters

---

# Agent

The **agent** specifies where the pipeline will run.

Example:

```groovy
agent any
```

Other options include:

- Specific node
- Docker container
- Kubernetes agent

---

# Stages

Stages divide the pipeline into logical sections.

Examples:

- Checkout
- Build
- Test
- Package
- Deploy

Example:

```groovy
stage('Build')
```

---

# Steps

Steps are the individual tasks executed inside a stage.

Examples:

Linux:

```groovy
sh 'pwd'
```

Windows:

```groovy
bat 'dir'
```

Echo message:

```groovy
echo 'Hello Jenkins'
```

---

# Post Actions

The `post` block runs after the pipeline finishes.

Common options:

- always
- success
- failure
- unstable
- aborted

Example:

```groovy
post {
    success {
        echo 'Build Successful'
    }
}
```

---

# Pipeline Types

## Declarative Pipeline

Recommended for most users.

Advantages:

- Easy to read
- Easy to maintain
- Standardized syntax
- Better validation

---

## Scripted Pipeline

Provides maximum flexibility using Groovy scripting.

Advantages:

- Highly customizable
- Suitable for advanced automation

Disadvantages:

- More complex
- Harder to maintain

---

# Common Pipeline Stages

```text
Checkout
      │
      ▼
Build
      │
      ▼
Unit Test
      │
      ▼
Code Analysis
      │
      ▼
Package
      │
      ▼
Deploy
      │
      ▼
Notify
```

---

# Environment Variables

Environment variables store reusable values.

Example:

```groovy
environment {
    APP_NAME = "DemoApp"
}
```

---

# Build Status

Possible pipeline results:

| Status | Meaning |
|----------|----------|
| Success | Pipeline completed successfully |
| Failed | One or more stages failed |
| Unstable | Pipeline completed but tests failed |
| Aborted | Pipeline stopped manually |

---

# Console Output

Console Output displays logs from every stage.

Useful for:

- Debugging
- Monitoring
- Troubleshooting
- Performance analysis

---

# Advantages of Pipelines

- Pipeline as Code
- Version controlled
- Reusable
- Scalable
- Supports parallel execution
- Supports approvals
- Easier collaboration

---

# Limitations

- Learning Groovy syntax
- More complex than Freestyle Projects
- Requires version control knowledge

---

# Best Practices

- Store the Jenkinsfile in Git.
- Keep stages small and focused.
- Use meaningful stage names.
- Use Declarative Pipelines whenever possible.
- Avoid hardcoding credentials.
- Use Jenkins Credentials for secrets.
- Review Console Output after every build.
- Test pipelines before deploying to production.

---

# Freestyle Project vs Pipeline

| Feature | Freestyle | Pipeline |
|----------|------------|-----------|
| Configuration | GUI | Code |
| Version Control | Limited | Full |
| Reusability | Low | High |
| Scalability | Moderate | Excellent |
| Recommended | Learning | Production |

---

# Interview Questions

### What is a Jenkins Pipeline?

A Jenkins Pipeline is a collection of automated steps defined in a Jenkinsfile to build, test, and deploy applications.

---

### What is Pipeline as Code?

Pipeline as Code is the practice of defining CI/CD workflows in a version-controlled Jenkinsfile instead of configuring them manually through the Jenkins UI.

---

### What is the difference between Declarative and Scripted Pipelines?

Declarative Pipelines use a structured, easier-to-read syntax and are recommended for most use cases, while Scripted Pipelines use Groovy scripting and provide greater flexibility for advanced scenarios.

---

### What is an Agent in Jenkins?

An Agent is the machine or execution environment where a pipeline runs.

---

### What is a Stage?

A Stage groups related steps together, making the pipeline easier to understand and monitor.

---

# Key Takeaways

- Jenkins Pipelines implement **Pipeline as Code** using a **Jenkinsfile**.
- The Jenkinsfile is stored alongside application source code in Git.
- Declarative Pipelines are recommended for most projects due to their simplicity and maintainability.
- Pipelines are more scalable, reusable, and production-ready than Freestyle Projects.
- Organizing pipelines into clear stages improves readability, debugging, and long-term maintenance.1 2 3 4