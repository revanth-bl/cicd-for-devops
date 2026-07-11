# Notes

## What is a CI/CD Workflow?

A CI/CD workflow is an automated sequence of steps that takes source code from a developer's machine, validates it through builds and tests, and deploys it to one or more environments.

The goal is to deliver software quickly, reliably, and consistently with minimal manual intervention.

---

# Typical CI/CD Workflow

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
CI/CD Pipeline Triggered
    │
    ▼
Build Application
    │
    ▼
Run Automated Tests
    │
    ▼
Code Quality Checks
    │
    ▼
Create Artifact / Docker Image
    │
    ▼
Deploy to Staging
    │
    ▼
Manual Approval (Optional)
    │
    ▼
Deploy to Production
```

---

# Pipeline Stages

## 1. Source

- Developer writes code.
- Changes are committed.
- Code is pushed to a Git repository.

Common tools:

- Git
- GitHub
- GitLab
- Bitbucket

---

## 2. Build

The source code is compiled into an executable application or package.

Examples:

- Maven
- Gradle
- npm

---

## 3. Test

Automated tests verify that the application works correctly.

Common tests include:

- Unit Testing
- Integration Testing
- Functional Testing

---

## 4. Code Quality

Static analysis tools inspect the code for:

- Bugs
- Security vulnerabilities
- Code smells
- Maintainability issues

Examples:

- SonarQube
- ESLint
- Checkstyle

---

## 5. Package

The application is packaged for deployment.

Examples:

- JAR
- WAR
- Docker Image

---

## 6. Deploy

The application is deployed to an environment.

Deployment environments include:

- Development
- Testing
- Staging
- Production

---

## 7. Monitor

After deployment, the application is monitored to ensure it is functioning correctly.

Monitoring tools:

- Prometheus
- Grafana
- ELK Stack

---

# Why CI/CD Workflow Matters

- Reduces manual work
- Detects bugs early
- Improves software quality
- Accelerates software delivery
- Enables frequent releases
- Ensures consistent deployments

---

# Real-World Example

A developer fixes a login bug.

1. Code is committed.
2. Changes are pushed to GitHub.
3. Jenkins detects the push.
4. Jenkins builds the project.
5. Automated tests run.
6. Docker image is created.
7. Image is pushed to a registry.
8. Application is deployed.
9. Team receives a success notification.

---

# Common Workflow Triggers

- Git push
- Pull request
- Merge to main branch
- Scheduled jobs
- Manual trigger
- Webhook events

---

# Best Practices

- Commit small changes frequently.
- Keep pipelines fast.
- Automate testing.
- Use version control for pipeline configurations.
- Secure secrets and credentials.
- Monitor deployments continuously.
- Implement rollback strategies.

---

# Key Terms

| Term | Description |
|------|-------------|
| Pipeline | Automated sequence of CI/CD stages |
| Trigger | Event that starts a pipeline |
| Build | Converts source code into an executable |
| Artifact | Output generated after a successful build |
| Stage | A logical phase within a pipeline |
| Job | A specific task executed within a stage |
| Deployment | Releasing software to an environment |

---

# Key Takeaways

- A CI/CD workflow automates software delivery.
- Every code change can trigger a pipeline.
- Automated testing improves software quality.
- Deployment becomes faster and more reliable.
- Monitoring ensures application health after deployment.

---

# Interview Questions

### What is a CI/CD workflow?

A CI/CD workflow is an automated process that builds, tests, and deploys software whenever changes are made to the source code.

---

### What are the main stages of a CI/CD pipeline?

- Source
- Build
- Test
- Code Quality
- Package
- Deploy
- Monitor

---

### What triggers a CI/CD pipeline?

Common triggers include:

- Git push
- Pull request
- Merge
- Scheduled jobs
- Manual execution
- Webhooks

---

# Summary

A CI/CD workflow automates the complete software delivery lifecycle, enabling teams to build, test, and deploy applications efficiently while reducing manual effort and improving reliability.