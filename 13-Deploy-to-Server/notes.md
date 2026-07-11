# Notes

## What is Deployment?

Deployment is the process of delivering a built application from the CI/CD pipeline to a target environment where users can access and use it.

After an application has been built, tested, and packaged, Jenkins automates the deployment process, reducing manual effort and minimizing human errors.

---

# Why Deployment Automation?

Without Deployment Automation:

- Manual deployments
- Human errors
- Inconsistent environments
- Longer release cycles
- Difficult rollbacks

With Deployment Automation:

- Faster releases
- Consistent deployments
- Reduced downtime
- Improved reliability
- Easy rollback
- Continuous Delivery

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
Deploy to Server
     │
     ▼
Application Running
```

---

# Deployment Methods

Applications can be deployed using several methods.

Common deployment strategies include:

- SSH
- SCP
- Docker
- Docker Compose
- Kubernetes
- Cloud Services

The choice depends on the application's architecture and infrastructure.

---

# SSH Deployment

SSH (Secure Shell) is one of the simplest ways to deploy applications to remote Linux servers.

Workflow:

```text
Jenkins
     │
SSH Connection
     │
Remote Linux Server
     │
Deploy Application
```

SSH provides secure remote access for executing deployment commands.

---

# SCP Deployment

SCP (Secure Copy Protocol) is used to securely transfer files between systems.

Example workflow:

```text
Jenkins
     │
SCP
     │
Application Artifact
     │
Remote Server
```

Typical artifacts include:

- JAR files
- WAR files
- Docker Compose files
- Configuration files

---

# Docker Deployment

Instead of copying application files, Jenkins can deploy Docker containers.

Workflow:

```text
Docker Image
      │
      ▼
Docker Registry
      │
      ▼
Remote Server
      │
      ▼
docker pull
      │
      ▼
docker run
```

Benefits:

- Environment consistency
- Simplified deployments
- Easy rollback
- Portability

---

# Docker Compose Deployment

Docker Compose is used to deploy multiple containers together.

Example:

```text
Application
Database
Redis
Nginx
```

All services can be started using a single command.

---

# Deployment Pipeline

A production deployment pipeline usually follows this sequence:

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
Verify Deployment
```

Verification ensures the application is running correctly after deployment.

---

# Deployment Verification

After deployment, Jenkins should verify the application by:

- Checking HTTP responses
- Verifying application logs
- Confirming service status
- Monitoring health endpoints

Example:

```text
Application Running?
        │
      Yes
        │
Deployment Successful
```

---

# Rollback Strategy

If deployment fails, the previous stable version should be restored.

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

A rollback strategy minimizes downtime and service disruption.

---

# Zero-Downtime Deployment

Zero-downtime deployment updates the application without interrupting users.

Common techniques:

- Blue-Green Deployment
- Rolling Deployment
- Canary Deployment

These strategies reduce deployment risk in production environments.

---

# Jenkins Credentials

Sensitive information such as:

- SSH private keys
- Server passwords
- API tokens

should never be hardcoded.

Instead, store them securely using **Jenkins Credentials**.

Benefits:

- Better security
- Centralized management
- Easier credential rotation

---

# Best Practices

- Use SSH key authentication instead of passwords.
- Test deployments in a staging environment first.
- Verify application health after deployment.
- Maintain versioned releases.
- Automate rollback procedures.
- Monitor application logs continuously.
- Secure all deployment credentials.

---

# Common Challenges

- SSH authentication failures
- Network connectivity issues
- Incorrect file permissions
- Service startup failures
- Docker container failures
- Port conflicts
- Firewall restrictions

---

# Security Considerations

Production deployments should follow these practices:

- Use encrypted SSH connections.
- Disable password authentication where possible.
- Rotate credentials regularly.
- Restrict server access.
- Use firewalls.
- Monitor login activity.
- Keep servers updated.

---

# Interview Questions

### What is deployment in CI/CD?

Deployment is the automated process of releasing an application to a target environment after it has successfully passed all build and testing stages.

---

### Why is SSH commonly used for deployment?

SSH provides secure remote access, allowing Jenkins to execute deployment commands and transfer files safely.

---

### What is the difference between SSH and SCP?

SSH is used to execute commands on a remote server, while SCP is used to securely copy files between systems.

---

### Why are Docker deployments preferred?

Docker packages applications with all required dependencies, ensuring consistent behavior across different environments.

---

### Why is rollback important?

Rollback allows teams to quickly restore the last stable version if a deployment introduces issues, reducing downtime and business impact.

---

# Key Takeaways

- Deployment is the final stage of a CI/CD pipeline where applications are released to target environments.
- Jenkins automates deployments using SSH, SCP, Docker, or other deployment tools.
- Automated verification and rollback strategies improve deployment reliability.
- Secure credential management and deployment validation are essential for production systems.
- Modern deployment practices focus on automation, consistency, scalability, and minimal downtime.