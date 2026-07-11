# Troubleshooting

This guide covers common issues encountered while creating and running Multi-Stage Pipelines in Jenkins.

---

# 1. Pipeline Syntax Error

## Problem

```text
WorkflowScript: Expected a stage
```

or

```text
Missing required section "stages"
```

## Cause

The Jenkinsfile contains invalid Declarative Pipeline syntax.

## Solution

- Validate the Jenkinsfile syntax.
- Ensure all braces `{}` are properly matched.
- Use the **Pipeline Syntax Generator** in Jenkins.

---

# 2. Stage Failed

## Problem

```text
Finished: FAILURE
```

## Cause

One of the pipeline stages failed.

## Solution

Review the **Console Output** to determine which stage failed and inspect the corresponding logs before rerunning the pipeline.

---

# 3. Git Checkout Failed

## Problem

```text
ERROR: Couldn't find any revision to build
```

## Cause

- Incorrect repository URL
- Wrong branch name
- Missing credentials

## Solution

Verify:

- Git repository URL
- Branch name
- Jenkins Git credentials
- Repository permissions

Test manually:

```bash
git clone <repository-url>
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
- Invalid build configuration

## Solution

Run locally:

```bash
mvn clean package
```

or

```bash
gradle build
```

Fix any reported errors before rerunning the pipeline.

---

# 5. Test Stage Failed

## Problem

```text
Tests Failed
```

## Solution

Review the test reports and Jenkins Console Output.

Run locally:

```bash
mvn test
```

or

```bash
gradle test
```

Correct the failing test cases or application code.

---

# 6. Docker Build Failed

## Problem

```text
docker build
```

returns an error.

## Solution

Verify:

- Docker is installed.
- Docker daemon is running.
- Dockerfile exists in the project root.
- Build context is correct.

Test manually:

```bash
docker build -t my-app:v1 .
```

---

# 7. Docker Push Failed

## Problem

```text
denied: requested access to the resource is denied
```

## Solution

Login to Docker Hub:

```bash
docker login
```

Verify the image tag:

```bash
docker tag my-app:v1 username/my-app:v1
```

Push again:

```bash
docker push username/my-app:v1
```

---

# 8. Deployment Stage Failed

## Problem

Deployment completed with errors.

## Possible Causes

- Remote server unavailable
- SSH authentication failed
- Deployment script error

## Solution

Verify:

- SSH connectivity
- Server availability
- Deployment scripts
- Required permissions

---

# 9. Environment Variable Missing

## Problem

```text
No such property
```

## Cause

A required environment variable is undefined.

## Solution

Declare variables inside the `environment` block.

```groovy
environment {
    APP_NAME = "DemoApp"
}
```

---

# 10. Jenkins Credentials Not Found

## Problem

```text
Credentials not found
```

## Solution

Navigate to:

```text
Manage Jenkins
    ↓
Credentials
```

Verify:

- Credential ID
- Username
- Password or Token
- Scope

---

# 11. Timeout During Pipeline

## Problem

Pipeline hangs or runs indefinitely.

## Solution

Add a timeout:

```groovy
options {
    timeout(time: 30, unit: 'MINUTES')
}
```

Review long-running stages for inefficiencies.

---

# 12. Workspace Contains Old Files

## Problem

Previous build artifacts interfere with the current build.

## Solution

Clean the workspace:

```groovy
cleanWs()
```

or before building:

```bash
mvn clean
```

---

# 13. Post Actions Not Executed

## Problem

Cleanup or notifications are skipped.

## Cause

Incorrect `post` block syntax.

## Solution

Verify the structure:

```groovy
post {

    always {
        cleanWs()
    }

}
```

---

# 14. Pipeline Stops Unexpectedly

## Problem

Pipeline terminates before all stages complete.

## Possible Causes

- Previous stage failure
- Agent disconnected
- Manual abort
- System resource limitations

## Solution

Review:

- Jenkins Console Output
- Jenkins system logs
- Agent status
- Resource utilization

---

# Useful Verification Commands

Verify Git:

```bash
git --version
```

Verify Java:

```bash
java --version
```

Verify Maven:

```bash
mvn --version
```

Verify Docker:

```bash
docker --version
```

List Docker images:

```bash
docker images
```

List running containers:

```bash
docker ps
```

Check Jenkins service:

```bash
sudo systemctl status jenkins
```

Restart Jenkins:

```bash
sudo systemctl restart jenkins
```

Check Docker service:

```bash
sudo systemctl status docker
```

Restart Docker:

```bash
sudo systemctl restart docker
```

---

# Best Practices

- Validate the Jenkinsfile before committing changes.
- Keep pipeline stages independent and focused.
- Execute automated tests before deployment.
- Store secrets in Jenkins Credentials.
- Archive important build artifacts.
- Clean the workspace after every pipeline run.
- Monitor Console Output after each stage.
- Use version-controlled Jenkinsfiles for all projects.

---

# Summary

Most Multi-Stage Pipeline issues are caused by Jenkinsfile syntax errors, build failures, test failures, Docker configuration problems, deployment issues, or missing credentials. Reviewing **Jenkins Console Output**, verifying tool installations, and ensuring each stage is correctly configured will resolve the majority of pipeline execution problems.