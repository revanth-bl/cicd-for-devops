# Episode 13 - Deploy to Server

## Overview

Deployment is the final stage of the Continuous Integration and Continuous Delivery (CI/CD) pipeline, where a successfully built and tested application is released to a target environment.

Instead of manually copying application files and executing commands on production servers, Jenkins automates the deployment process using technologies such as SSH, SCP, Docker, and deployment scripts. Automation improves reliability, reduces deployment time, minimizes human errors, and enables consistent releases.

This chapter introduces server deployment concepts, remote deployment methods, deployment verification, rollback strategies, and production deployment best practices.

---

# Learning Objectives

After completing this chapter, you will be able to:

- Understand deployment in a CI/CD pipeline
- Deploy applications to remote Linux servers
- Use SSH and SCP for secure deployments
- Deploy Docker containers remotely
- Verify successful deployments
- Implement rollback strategies
- Follow production deployment best practices

---

# What is Deployment?

Deployment is the process of transferring a completed application from the build pipeline to a target server or infrastructure where end users can access it.

Deployment occurs only after the application has successfully passed all build and testing stages.

---

# Why Automate Deployments?

Without Deployment Automation:

```text
Developer
     │
     ▼
Manual Copy
     │
     ▼
Manual Configuration
     │
     ▼
Manual Restart
     │
     ▼
Production
```

Problems:

- Human errors
- Slow releases
- Inconsistent deployments
- Difficult rollbacks
- Increased downtime

---

With Deployment Automation:

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
Build
     │
     ▼
Test
     │
     ▼
Deploy
     │
     ▼
Verify
     │
     ▼
Production
```

Benefits:

- Faster releases
- Consistent deployments
- Reduced manual effort
- Improved reliability
- Easier rollback

---

# Deployment Workflow

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
Package
     │
     ▼
Deploy to Server
     │
     ▼
Health Check
     │
     ▼
Production
```

---

# Deployment Methods

Applications can be deployed using different techniques depending on the infrastructure.

Common methods include:

- SSH Deployment
- SCP File Transfer
- Docker Deployment
- Docker Compose Deployment
- Kubernetes Deployment
- Cloud Platform Deployment

---

# SSH Deployment

SSH (Secure Shell) allows Jenkins to securely connect to remote Linux servers and execute deployment commands.

Typical tasks include:

- Copying application files
- Restarting services
- Executing deployment scripts
- Verifying application status

SSH is one of the most widely used deployment methods for Linux servers.

---

# SCP Deployment

SCP (Secure Copy Protocol) securely transfers files between systems over SSH.

Typical deployment artifacts include:

- JAR files
- WAR files
- Configuration files
- Docker Compose files

---

# Docker Deployment

Docker-based deployments package the application and all dependencies into a portable container image.

Typical workflow:

```text
Build Docker Image
        │
        ▼
Push to Registry
        │
        ▼
Remote Server
        │
        ▼
Pull Image
        │
        ▼
Run Container
```

This approach ensures consistent deployments across different environments.

---

# Docker Compose Deployment

Docker Compose enables deployment of multiple related services with a single configuration file.

Example services:

- Application
- Database
- Redis
- Nginx

All services can be started and managed together.

---

# Deployment Verification

After deployment, Jenkins should verify that the application is functioning correctly.

Common verification steps include:

- Checking service status
- Monitoring application logs
- Sending HTTP requests to health endpoints
- Confirming expected application responses

Deployment should only be considered successful after these checks pass.

---

# Rollback Strategy

If a deployment introduces issues, the previous stable version should be restored automatically or manually.

Example:

```text
Version 1.0
      │
Deploy Version 1.1
      │
Failure
      │
Rollback
      │
Version 1.0
```

Rollback minimizes downtime and restores service quickly.

---

# Zero-Downtime Deployment

Modern deployment strategies minimize service interruption.

Common techniques include:

- Blue-Green Deployment
- Rolling Deployment
- Canary Deployment

These strategies reduce deployment risk while maintaining application availability.

---

# Security Best Practices

Production deployments should follow secure practices:

- Use SSH key authentication.
- Store secrets in Jenkins Credentials.
- Restrict server access.
- Rotate credentials regularly.
- Enable firewalls.
- Keep operating systems updated.
- Monitor deployment activity.

---

# Benefits of Automated Deployment

- Faster software releases
- Reduced human error
- Improved consistency
- Better reliability
- Easier rollback
- Scalable deployment process
- Increased developer productivity

---

# Common Challenges

- SSH authentication failures
- Incorrect file permissions
- Network connectivity issues
- Service startup failures
- Docker deployment errors
- Port conflicts
- Firewall restrictions

---

# Deployment Methods Comparison

| Method | Best Use Case | Advantages |
|----------|--------------|------------|
| SSH | Remote Linux servers | Simple and secure |
| SCP | File transfers | Fast and reliable |
| Docker | Containerized applications | Consistent environments |
| Docker Compose | Multi-container applications | Easy service management |
| Kubernetes | Large-scale deployments | High scalability |

---

# Key Takeaways

- Deployment is the final stage of the CI/CD pipeline where applications are released to production or other target environments.
- Jenkins automates deployments using SSH, SCP, Docker, and deployment scripts.
- Deployment verification ensures applications are functioning correctly after release.
- Rollback strategies improve reliability by enabling quick recovery from failed deployments.
- Secure credential management, monitoring, and deployment automation are essential for production-ready DevOps workflows.

---

# References

- Jenkins Official Documentation
- OpenSSH Documentation
- Docker Documentation
- Docker Compose Documentation
- Linux System Administration Documentation

---

# Next Topic

➡️ **Episode 14 – Notifications**

In the next chapter, you'll learn how Jenkins sends build and deployment notifications through Email, Slack, Microsoft Teams, and other communication platforms, ensuring teams are immediately informed about pipeline successes, failures, and deployment status.