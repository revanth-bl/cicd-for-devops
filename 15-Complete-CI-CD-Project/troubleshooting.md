# Troubleshooting

This guide covers common issues encountered while building and running the complete CI/CD pipeline.

The troubleshooting process follows the same order as the pipeline execution:

```text
GitHub
  ↓
Jenkins
  ↓
Build
  ↓
Test
  ↓
Docker
  ↓
Registry
  ↓
Deployment
  ↓
Notifications
```

---

# 1. Jenkins Pipeline Not Triggering

## Problem

GitHub push does not start Jenkins automatically.

## Possible Causes

- Webhook not configured
- Incorrect Jenkins URL
- Jenkins server unreachable
- GitHub plugin missing

## Solution

Verify GitHub webhook:

```text
GitHub Repository
        ↓
Settings
        ↓
Webhooks
```

Check:

- Payload URL
- Content Type
- Webhook status

Verify Jenkins plugins:

```text
Manage Jenkins
        ↓
Plugins
```

Install:

- GitHub Integration Plugin
- Pipeline Plugin

---

# 2. Jenkins Cannot Clone Repository

## Problem

```text
Failed to connect to repository
```

## Possible Causes

- Incorrect repository URL
- Missing Git credentials
- Private repository access issue

## Solution

Test manually:

```bash
git clone https://github.com/user/project.git
```

Configure credentials:

```text
Manage Jenkins
        ↓
Credentials
        ↓
Add Credentials
```

Verify:

- Username
- Personal Access Token
- Credential ID

---

# 3. Jenkinsfile Syntax Error

## Problem

```text
WorkflowScript: Expected a stage
```

## Cause

Invalid Jenkins Pipeline syntax.

## Solution

Validate Jenkinsfile:

```text
Jenkins Dashboard
        ↓
Pipeline Syntax
```

Check:

- Missing braces `{ }`
- Incorrect stage names
- Invalid directives

Example structure:

```groovy
pipeline {

    agent any

    stages {

        stage('Build') {

            steps {

                echo "Building"

            }

        }

    }

}
```

---

# 4. Build Stage Failed

## Problem

```text
BUILD FAILURE
```

## Possible Causes

- Compilation errors
- Missing dependencies
- Incorrect build configuration

## Solution

Run locally:

Maven:

```bash
mvn clean package
```

Gradle:

```bash
gradle build
```

Review the build logs and fix application errors.

---

# 5. Maven Dependency Failure

## Problem

```text
Could not resolve dependencies
```

## Cause

- Internet connectivity issue
- Incorrect dependency version
- Maven repository unavailable

## Solution

Clear Maven cache:

```bash
rm -rf ~/.m2/repository
```

Run:

```bash
mvn clean install
```

---

# 6. Automated Tests Failed

## Problem

```text
Tests Failed
```

## Cause

Application code does not pass validation.

## Solution

Run tests locally:

```bash
mvn test
```

Review:

- Test reports
- Console output
- Application logs

Fix failed test cases before deployment.

---

# 7. Docker Build Failed

## Problem

```text
docker build failed
```

## Possible Causes

- Incorrect Dockerfile
- Missing files
- Wrong build context

## Solution

Verify Dockerfile:

```bash
ls
```

Build manually:

```bash
docker build -t my-app:v1 .
```

Check Docker version:

```bash
docker --version
```

---

# 8. Docker Login Failed

## Problem

```text
denied: requested access
```

## Cause

Incorrect Docker Hub credentials.

## Solution

Login again:

```bash
docker login
```

Verify credentials stored in Jenkins:

```text
Manage Jenkins
        ↓
Credentials
```

---

# 9. Docker Push Failed

## Problem

```text
unauthorized: authentication required
```

## Cause

Incorrect image tag or authentication issue.

## Solution

Tag image correctly:

```bash
docker tag my-app:v1 username/my-app:v1
```

Push:

```bash
docker push username/my-app:v1
```

---

# 10. Deployment Server Connection Failed

## Problem

```text
ssh: connect to host failed
```

## Possible Causes

- Server offline
- Wrong IP address
- SSH service stopped
- Firewall blocking port 22

## Solution

Test SSH:

```bash
ssh user@server-ip
```

Check SSH service:

```bash
sudo systemctl status ssh
```

---

# 11. SSH Authentication Failed

## Problem

```text
Permission denied (publickey)
```

## Cause

SSH key is missing or incorrect.

## Solution

Generate key:

```bash
ssh-keygen -t rsa -b 4096
```

Copy key:

```bash
ssh-copy-id user@server-ip
```

Test:

```bash
ssh user@server-ip
```

---

# 12. Docker Container Not Starting After Deployment

## Problem

Container exits immediately.

## Solution

Check containers:

```bash
docker ps -a
```

View logs:

```bash
docker logs container-name
```

Restart container:

```bash
docker restart container-name
```

---

# 13. Application Not Accessible After Deployment

## Problem

Application is deployed but browser cannot access it.

## Possible Causes

- Wrong port mapping
- Firewall blocking port
- Application crashed

## Solution

Check container:

```bash
docker ps
```

Verify ports:

```bash
ss -tuln
```

Test:

```bash
curl http://server-ip:8080
```

---

# 14. Docker Image Version Issue

## Problem

Old application version is running.

## Cause

Using incorrect Docker image tag.

## Solution

Check images:

```bash
docker images
```

Pull latest version:

```bash
docker pull username/my-app:v2
```

Remove old container:

```bash
docker rm -f my-app
```

Deploy new version.

---

# 15. Pipeline Workspace Issues

## Problem

Previous builds affect current execution.

## Solution

Clean workspace:

```groovy
cleanWs()
```

Or manually:

```bash
rm -rf workspace/*
```

---

# 16. Notification Failure

## Problem

Pipeline succeeds but notification is not received.

## Possible Causes

- Incorrect SMTP settings
- Invalid webhook
- Missing plugin
- Wrong credentials

## Solution

Verify:

- Jenkins plugin installation
- Notification credentials
- Webhook URL
- SMTP configuration

Test notification manually.

---

# 17. Jenkins Agent Failure

## Problem

```text
Agent is offline
```

## Solution

Check agent status:

```text
Manage Jenkins
        ↓
Nodes
```

Restart agent machine if required.

---

# 18. Rollback Required

## Problem

New deployment causes application failure.

## Solution

Deploy previous stable image:

```bash
docker pull username/my-app:v1
```

Remove current container:

```bash
docker rm -f my-app
```

Start previous version:

```bash
docker run -d \
--name my-app \
-p 8080:8080 \
username/my-app:v1
```

---

# Useful Debug Commands

Check Jenkins:

```bash
sudo systemctl status jenkins
```

Restart Jenkins:

```bash
sudo systemctl restart jenkins
```

Check Docker:

```bash
docker info
```

Running containers:

```bash
docker ps
```

Container logs:

```bash
docker logs <container-name>
```

System resources:

```bash
free -h
```

Disk usage:

```bash
df -h
```

Network test:

```bash
ping server-ip
```

---

# Best Practices

- Always check Jenkins Console Output first.
- Keep Jenkinsfiles simple and readable.
- Test builds locally before pushing.
- Store secrets securely using Jenkins Credentials.
- Use versioned Docker images.
- Maintain rollback procedures.
- Monitor deployment health after every release.
- Keep documentation updated.

---

# Summary

Most CI/CD failures occur due to incorrect configurations, authentication problems, build errors, Docker issues, deployment failures, or notification misconfigurations.

A systematic troubleshooting approach helps identify problems quickly:

1. Check Jenkins logs.
2. Identify the failed pipeline stage.
3. Review error messages.
4. Reproduce the issue manually.
5. Apply the correct fix.
6. Re-run the pipeline.

A well-designed CI/CD pipeline is not only about automation—it is also about creating a reliable system that can be monitored, debugged, and recovered efficiently.