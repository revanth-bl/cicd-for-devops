# Episode 12 - Multi-Stage Pipeline

## Overview

A Multi-Stage Pipeline is a structured Jenkins pipeline that divides the software delivery lifecycle into multiple independent stages. Each stage performs a specific task such as checking out source code, building the application, executing tests, creating Docker images, publishing artifacts, and deploying the application.

Instead of executing every task in one large script, Jenkins organizes the workflow into logical stages, making pipelines easier to read, maintain, troubleshoot, and scale.

This chapter introduces production-style multi-stage pipelines and demonstrates how modern DevOps teams automate complete application delivery using Jenkins.

---

# Learning Objectives

After completing this chapter, you will be able to:

- Understand Multi-Stage Pipelines
- Create Declarative Jenkins Pipelines
- Organize CI/CD workflows into logical stages
- Configure environment variables and parameters
- Execute Build, Test, Docker, and Deploy stages
- Use post-build actions
- Follow production-ready pipeline best practices

---

# What is a Multi-Stage Pipeline?

A Multi-Stage Pipeline is a Jenkins pipeline composed of multiple sequential or parallel stages, where each stage performs a single responsibility within the CI/CD workflow.

Each stage executes only after the previous stage completes successfully, ensuring that only verified code progresses toward deployment.

---

# Why Multi-Stage Pipelines?

Without a Multi-Stage Pipeline:

```text
Developer
     │
     ▼
Single Large Script
     │
     ▼
Hard to Debug
     │
     ▼
Complex Maintenance
```

Problems:

- Difficult to locate failures
- Poor readability
- Limited scalability
- Hard to maintain
- Weak monitoring

---

With a Multi-Stage Pipeline:

```text
Developer
     │
     ▼
Git Push
     │
     ▼
Jenkins Pipeline
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

Benefits:

- Clear execution flow
- Easier debugging
- Better visibility
- Faster issue detection
- Production-ready automation

---

# Multi-Stage Pipeline Workflow

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
Jenkins
     │
     ▼
Checkout Source Code
     │
     ▼
Build Application
     │
     ▼
Run Automated Tests
     │
     ▼
Build Docker Image
     │
     ▼
Push Image to Registry
     │
     ▼
Deploy Application
     │
     ▼
Post Actions
```

---

# Typical Pipeline Stages

## Checkout

Retrieves the latest application source code from the version control repository.

---

## Build

Compiles the application and creates build artifacts using tools such as Maven or Gradle.

---

## Test

Executes automated tests to validate application functionality before deployment.

---

## Docker Build

Creates a Docker image containing the application and its runtime dependencies.

---

## Push Image

Publishes the Docker image to a container registry such as Docker Hub, Amazon ECR, or GitHub Container Registry.

---

## Deploy

Deploys the application to the target environment.

Possible deployment targets include:

- Virtual Machines
- Docker Hosts
- Kubernetes Clusters
- Cloud Platforms

---

## Post Actions

Performs cleanup and notifications after pipeline execution.

Examples:

- Clean workspace
- Archive artifacts
- Publish reports
- Send notifications

---

# Pipeline Structure

Example Declarative Pipeline:

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
                echo 'Deploying Application...'
            }
        }

    }

}
```

---

# Environment Variables

Environment variables provide reusable values throughout the pipeline.

Examples:

- Application name
- Docker image name
- Registry URL
- Deployment environment

Using environment variables makes pipelines cleaner and easier to maintain.

---

# Pipeline Parameters

Pipeline parameters allow users to customize execution without modifying the pipeline script.

Common parameters include:

- Branch name
- Docker image tag
- Deployment environment
- Application version

---

# Conditional Execution

Stages can execute only when specific conditions are met.

Examples:

- Deploy only from the `main` branch.
- Skip deployment for pull requests.
- Execute production deployment after manual approval.

---

# Parallel Execution

Independent tasks can run simultaneously to reduce pipeline execution time.

Example:

```text
             Build
               │
      ┌────────┴────────┐
      ▼                 ▼
 Unit Tests      Security Scan
      └────────┬────────┘
               ▼
        Docker Build
```

---

# Post-Build Actions

The `post` section executes after the pipeline finishes.

Common actions include:

- Workspace cleanup
- Artifact archiving
- Test report publishing
- Success notifications
- Failure notifications

---

# Benefits of Multi-Stage Pipelines

- Better organization
- Easier troubleshooting
- Faster feedback
- Improved reliability
- Reusable pipeline structure
- Easier maintenance
- Production-ready automation

---

# Best Practices

- Keep stages focused on one responsibility.
- Execute automated tests before deployment.
- Store credentials securely using Jenkins Credentials.
- Use environment variables instead of hardcoding values.
- Archive important build artifacts.
- Clean the workspace after execution.
- Use version control for Jenkinsfiles.
- Monitor pipeline performance regularly.

---

# Common Challenges

- Pipeline syntax errors
- Failed builds
- Test failures
- Docker build issues
- Deployment failures
- Missing credentials
- Environment configuration problems

---

# Multi-Stage Pipeline vs Single Pipeline

| Feature | Single Script | Multi-Stage Pipeline |
|----------|---------------|----------------------|
| Readability | Low | High |
| Debugging | Difficult | Easy |
| Maintainability | Poor | Excellent |
| Scalability | Limited | Excellent |
| Monitoring | Basic | Detailed |

---

# Key Takeaways

- Multi-Stage Pipelines divide CI/CD workflows into logical stages.
- Each stage performs a specific responsibility, improving maintainability and visibility.
- Jenkins supports environment variables, parameters, conditional execution, parallel stages, and post-build actions.
- Combining Build, Test, Docker, and Deploy stages creates a production-ready CI/CD pipeline.
- Multi-Stage Pipelines are a core practice in modern DevOps and continuous delivery.

---

# References

- Jenkins Official Documentation
- Jenkins Pipeline Syntax Guide
- Docker Documentation
- Apache Maven Documentation
- Gradle Documentation

---

# Next Topic

➡️ **Episode 13 – Deploy to Server**

In the next chapter, you'll learn how Jenkins deploys applications to remote Linux servers using SSH, transfers build artifacts, executes deployment scripts, verifies deployments, and automates release delivery in a production-like environment.