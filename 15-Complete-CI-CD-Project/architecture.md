# Architecture

## Project Overview

This project demonstrates a complete production-style Continuous Integration and Continuous Delivery (CI/CD) pipeline using GitHub, Jenkins, Maven, Docker, Docker Hub, and a Linux deployment server.

The objective is to automate the software delivery lifecycle from source code commit to application deployment while ensuring code quality, repeatability, and rapid delivery.

---

# High-Level Architecture

```text
                    Developer
                        │
                git add / commit
                        │
                        ▼
                 GitHub Repository
                        │
             GitHub Webhook Trigger
                        │
                        ▼
                 Jenkins Controller
                        │
     ┌──────────────────┼──────────────────┐
     │                  │                  │
     ▼                  ▼                  ▼
Checkout Code      Build Project      Run Tests
     │                  │                  │
     └──────────────────┼──────────────────┘
                        ▼
                 Package Application
                  (Maven / Gradle)
                        │
                        ▼
                Build Docker Image
                        │
                        ▼
               Push to Docker Hub
                        │
                        ▼
               Remote Linux Server
                        │
              Pull Docker Image
                        │
                        ▼
          Stop Existing Container
                        │
                        ▼
           Start New Container
                        │
                        ▼
             Health Check / Verify
                        │
                        ▼
          Email / Slack Notification
                        │
                        ▼
                 End Users Access
```

---

# CI/CD Workflow

```text
Developer
     │
     ▼
Git Commit
     │
     ▼
GitHub
     │
Webhook
     │
     ▼
Jenkins
     │
Checkout
     │
Build
     │
Unit Tests
     │
Package
     │
Docker Build
     │
Push Docker Image
     │
Deploy
     │
Health Check
     │
Notification
     │
Pipeline Complete
```

---

# Components

## 1. GitHub

Responsibilities:

- Source code management
- Version control
- Pull Requests
- Webhook integration
- Collaboration

---

## 2. Jenkins

Responsibilities:

- Pipeline orchestration
- Build automation
- Test execution
- Docker image creation
- Deployment automation
- Notifications

---

## 3. Maven / Gradle

Responsibilities:

- Dependency management
- Source code compilation
- Unit testing
- Packaging application

Outputs:

- JAR
- WAR

---

## 4. Docker

Responsibilities:

- Build container image
- Package application
- Ensure environment consistency

Output:

Docker Image

---

## 5. Docker Hub

Responsibilities:

- Store Docker images
- Version image releases
- Provide deployment source

---

## 6. Linux Deployment Server

Responsibilities:

- Pull latest Docker image
- Stop previous container
- Deploy new version
- Run application
- Monitor service

---

## 7. Notification Services

Examples:

- Email
- Slack
- Microsoft Teams
- Discord

Purpose:

Inform the team about:

- Build Success
- Build Failure
- Deployment Success
- Deployment Failure

---

# Pipeline Stages

```text
Stage 1
Checkout Source

↓

Stage 2
Compile

↓

Stage 3
Run Unit Tests

↓

Stage 4
Package Application

↓

Stage 5
Build Docker Image

↓

Stage 6
Push Docker Image

↓

Stage 7
Deploy to Server

↓

Stage 8
Health Check

↓

Stage 9
Send Notifications
```

---

# Deployment Flow

```text
Docker Hub

        │

docker pull

        │

Linux Server

        │

docker stop

        │

docker rm

        │

docker run

        │

Application Running
```

---

# Jenkins Pipeline Structure

```text
pipeline {

    agent any

    stages {

        Checkout

        Build

        Test

        Package

        Docker Build

        Docker Push

        Deploy

        Health Check

    }

    post {

        success

        failure

        always

    }

}
```

---

# Security Architecture

Sensitive information is stored securely using Jenkins Credentials.

Examples:

- GitHub Token
- Docker Hub Password
- SSH Private Key
- Email Password
- Slack Token

Never hardcode credentials inside the Jenkinsfile.

---

# Artifact Flow

```text
Source Code

↓

Compiled Classes

↓

JAR/WAR File

↓

Docker Image

↓

Docker Hub

↓

Deployment Server

↓

Running Container
```

---

# Monitoring Flow

```text
Application

↓

Health Check

↓

Logs

↓

Alerts

↓

Notification
```

---

# Advantages

- Fully automated software delivery
- Consistent deployments
- Faster release cycles
- Reduced human error
- Easy rollback
- Improved collaboration
- Production-ready workflow
- Scalable architecture

---

# Technologies Used

| Layer | Technology |
|---------|------------|
| Source Control | Git, GitHub |
| CI Server | Jenkins |
| Build Tool | Maven / Gradle |
| Containerization | Docker |
| Registry | Docker Hub |
| Deployment | Linux Server |
| Notifications | Email, Slack |
| Operating System | Ubuntu Linux |

---

# Key Takeaways

- GitHub stores and manages the application's source code.
- GitHub Webhooks automatically trigger Jenkins pipelines after code changes.
- Jenkins orchestrates the entire CI/CD workflow, from build to deployment.
- Maven or Gradle compiles, tests, and packages the application.
- Docker ensures consistent deployments by packaging the application into containers.
- Docker Hub acts as the central image registry.
- The Linux server deploys and runs the latest application version.
- Notifications provide immediate feedback about pipeline execution and deployment status.