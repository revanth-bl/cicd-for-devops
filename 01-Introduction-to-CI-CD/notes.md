# Notes

## What is CI/CD?

CI/CD stands for **Continuous Integration** and **Continuous Delivery/Continuous Deployment**. It is a software development practice that automates building, testing, and deploying applications.

---

## Continuous Integration (CI)

Continuous Integration is the process of frequently merging code changes into a shared repository.

Every code change automatically triggers:

- Source code checkout
- Build process
- Automated testing
- Code quality checks

If any step fails, developers are immediately notified.

---

## Continuous Delivery (CD)

Continuous Delivery ensures that the application is always ready for deployment.

Deployment to production requires manual approval.

---

## Continuous Deployment

Continuous Deployment goes one step further by automatically deploying every successful change to production without manual intervention.

---

## Typical CI/CD Pipeline

```text
Developer
     │
     ▼
GitHub Repository
     │
     ▼
Jenkins Trigger
     │
     ▼
Build
     │
     ▼
Unit Tests
     │
     ▼
Code Quality Scan
     │
     ▼
Docker Build
     │
     ▼
Deploy
     │
     ▼
Production
```

---

## Why CI/CD is Important

- Faster software delivery
- Fewer production bugs
- Automated testing
- Consistent deployments
- Reduced manual work
- Faster feedback for developers
- Easier rollback when failures occur

---

## Popular CI/CD Tools

### Source Control

- Git
- GitHub
- GitLab
- Bitbucket

### CI Servers

- Jenkins
- GitHub Actions
- GitLab CI
- CircleCI

### Build Tools

- Maven
- Gradle
- npm

### Containerization

- Docker

### Orchestration

- Kubernetes

### Artifact Repository

- Nexus
- JFrog Artifactory

### Monitoring

- Prometheus
- Grafana

---

## Advantages

- Improved collaboration
- Faster releases
- Reliable deployments
- Better software quality
- Reduced human errors
- Increased productivity

---

## Challenges

- Initial setup can be time-consuming.
- Requires proper testing practices.
- Infrastructure must be maintained.
- Poor pipeline design can slow development.

---

## Real-World Workflow

1. Developer writes code.
2. Code is pushed to GitHub.
3. Jenkins detects the change.
4. Application is built.
5. Automated tests are executed.
6. Docker image is created.
7. Image is pushed to a registry.
8. Application is deployed.
9. Monitoring verifies the deployment.

---

## Key Terms

| Term | Description |
|------|-------------|
| Repository | Stores source code |
| Commit | A saved code change |
| Pipeline | Automated sequence of CI/CD stages |
| Build | Converts source code into an executable application |
| Test | Verifies application functionality |
| Deploy | Releases the application to an environment |
| Rollback | Reverts to a previous stable version |

---

## Best Practices

- Commit small and frequent changes.
- Write automated tests.
- Keep pipelines fast and reliable.
- Store secrets securely.
- Use version control for pipeline configurations.
- Monitor deployments continuously.

---

## Interview Questions

### What is CI/CD?

CI/CD is a software development practice that automates the integration, testing, and deployment of applications.

---

### What is the difference between Continuous Delivery and Continuous Deployment?

Continuous Delivery requires manual approval before production deployment, whereas Continuous Deployment automatically deploys every successful build to production.

---

### Name some popular CI/CD tools.

- Jenkins
- GitHub Actions
- GitLab CI/CD
- CircleCI
- Azure DevOps
- AWS CodePipeline

---

## Summary

CI/CD enables teams to deliver software quickly, safely, and consistently by automating repetitive development and deployment tasks.