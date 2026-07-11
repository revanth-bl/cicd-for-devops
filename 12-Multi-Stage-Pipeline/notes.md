# Notes

## What is a Multi-Stage Pipeline?

A Multi-Stage Pipeline is a Jenkins pipeline that divides the software delivery process into multiple logical stages. Each stage performs a specific task such as building, testing, creating Docker images, or deploying the application.

Breaking the pipeline into stages improves readability, debugging, monitoring, and overall pipeline reliability.

---

# Why Use a Multi-Stage Pipeline?

Without Multiple Stages:

- Difficult to identify failures
- Hard to maintain
- Long and complex scripts
- Poor visibility into the build process

With Multiple Stages:

- Clear separation of responsibilities
- Easier debugging
- Faster issue identification
- Better monitoring
- Improved maintainability

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

# Typical Pipeline Stages

## 1. Checkout

Retrieves the latest source code from the version control repository.

Example:

```text
GitHub
    │
    ▼
Checkout Source Code
```

---

## 2. Build

Compiles the application and generates build artifacts.

Examples:

- Maven
- Gradle
- npm
- dotnet

---

## 3. Test

Runs automated tests to verify application quality.

Examples:

- Unit Tests
- Integration Tests
- Functional Tests

---

## 4. Docker Build

Creates a Docker image containing the application and its dependencies.

Example:

```text
Dockerfile
      │
      ▼
Docker Image
```

---

## 5. Push Image

Uploads the Docker image to a container registry.

Common registries:

- Docker Hub
- Amazon ECR
- Azure Container Registry
- GitHub Container Registry

---

## 6. Deploy

Deploys the application to the target environment.

Possible deployment targets:

- Virtual Machine
- Docker Host
- Kubernetes Cluster
- Cloud Platform

---

## 7. Post Actions

Performs cleanup and notifications after pipeline execution.

Examples:

- Delete workspace
- Archive artifacts
- Send email notifications
- Slack notifications

---

# Pipeline Structure

```text
pipeline
 ├── agent
 ├── environment
 ├── parameters
 ├── stages
 │     ├── Checkout
 │     ├── Build
 │     ├── Test
 │     ├── Docker Build
 │     ├── Push Image
 │     └── Deploy
 └── post
```

---

# Environment Variables

Environment variables store reusable values across the pipeline.

Examples:

- Application name
- Docker image name
- Registry URL
- Deployment environment

Benefits:

- Cleaner code
- Easier maintenance
- Improved flexibility

---

# Pipeline Parameters

Parameters allow users to customize pipeline execution.

Examples:

- Application version
- Deployment environment
- Docker image tag
- Branch name

---

# Conditional Execution

Stages can execute only when specific conditions are met.

Examples:

- Deploy only from the `main` branch.
- Run production deployment only after approval.
- Skip deployment for pull requests.

---

# Parallel Execution

Independent stages can run simultaneously to reduce pipeline execution time.

Example:

```text
          Build
             │
     ┌───────┴────────┐
     ▼                ▼
 Unit Tests     Security Scan
     └───────┬────────┘
             ▼
        Docker Build
```

---

# Error Handling

Jenkins supports:

- Retry failed stages
- Timeout long-running stages
- Post-build cleanup
- Success and failure notifications

These features make pipelines more reliable.

---

# Benefits of Multi-Stage Pipelines

- Better organization
- Easier troubleshooting
- Faster feedback
- Improved reliability
- Easier maintenance
- Clear execution flow
- Production-ready automation

---

# Best Practices

- Keep stages small and focused.
- Fail fast when critical errors occur.
- Run automated tests before deployment.
- Archive important artifacts.
- Use environment variables.
- Secure credentials using Jenkins Credentials.
- Clean the workspace after every build.
- Version control all pipeline scripts.

---

# Common Challenges

- Long execution times
- Failed dependencies
- Docker build failures
- Deployment failures
- Incorrect environment variables
- Authentication issues
- Pipeline syntax errors

---

# Interview Questions

### What is a Multi-Stage Pipeline?

A Multi-Stage Pipeline divides a CI/CD workflow into separate stages such as Build, Test, Package, and Deploy, making automation easier to manage and troubleshoot.

---

### Why are stages used in Jenkins?

Stages improve readability, monitoring, debugging, and make it easier to identify exactly where a pipeline fails.

---

### What is the purpose of the `post` section?

The `post` section executes actions after the pipeline finishes, such as cleanup, notifications, or artifact archiving.

---

### What are environment variables in Jenkins?

Environment variables store reusable configuration values that can be accessed throughout the pipeline.

---

### Why should automated tests run before deployment?

Running tests before deployment ensures application quality and prevents defective code from reaching production.

---

# Key Takeaways

- Multi-Stage Pipelines organize CI/CD workflows into logical, manageable stages.
- Each stage performs a single responsibility, improving readability and maintainability.
- Jenkins supports environment variables, parameters, conditional execution, and post-build actions for flexible automation.
- Automated testing, Docker integration, and deployment can all be combined into one production-ready pipeline.
- Multi-Stage Pipelines are the foundation of modern DevOps automation and continuous delivery.