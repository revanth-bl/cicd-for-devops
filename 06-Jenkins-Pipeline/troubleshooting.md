# Troubleshooting

This guide covers common issues encountered while creating and running Jenkins Pipelines.

---

# 1. Pipeline Failed

## Problem

```text
Finished: FAILURE
```

## Possible Causes

- Invalid Jenkinsfile syntax
- Build command failed
- Missing dependencies
- Incorrect pipeline configuration

## Solution

Open:

```text
Build History → Console Output
```

Review the error message, correct the issue, and rerun the pipeline.

---

# 2. Jenkinsfile Not Found

## Problem

```text
Jenkinsfile not found
```

## Possible Causes

- Jenkinsfile is missing.
- Incorrect file name.
- Jenkinsfile is not in the repository root.

## Solution

Verify:

```text
Repository
│
├── src/
├── README.md
└── Jenkinsfile
```

The filename must be exactly:

```text
Jenkinsfile
```

---

# 3. Pipeline Syntax Error

## Example

```text
WorkflowScript: Expected a stage
```

or

```text
Missing }
```

## Cause

Invalid Groovy or Declarative Pipeline syntax.

## Solution

- Check matching braces `{}`.
- Verify stage and steps blocks.
- Use the **Pipeline Syntax** tool in Jenkins.

---

# 4. Git Checkout Failed

## Problem

```text
ERROR: Couldn't find any revision to build.
```

## Possible Causes

- Incorrect repository URL.
- Wrong branch name.
- Authentication failure.

## Solution

Verify:

```bash
git clone <repository-url>
```

Check that:

- Repository URL is correct.
- Branch exists.
- Jenkins credentials are configured.

---

# 5. Shell Step Failed

## Problem

```text
sh: command not found
```

## Cause

The pipeline is running on Windows.

## Solution

Linux:

```groovy
sh 'pwd'
```

Windows:

```groovy
bat 'dir'
```

Use the appropriate command for your build agent.

---

# 6. Batch Step Failed

## Problem

```text
bat is not recognized
```

## Cause

The pipeline is running on Linux.

## Solution

Use:

```groovy
sh 'ls -la'
```

instead of:

```groovy
bat 'dir'
```

---

# 7. Stage Skipped

## Possible Causes

- Previous stage failed.
- Conditional `when` block evaluated to false.

## Solution

Review:

```text
Console Output
```

Identify why the stage was skipped and correct the pipeline logic.

---

# 8. Build Stuck in Queue

## Possible Causes

- No available executors.
- Jenkins agent offline.
- Busy controller.

## Solution

Navigate to:

```text
Manage Jenkins → Nodes
```

Verify:

- Agent is online.
- Executors are available.

---

# 9. Pipeline Cannot Access Credentials

## Problem

```text
Credentials not found
```

## Solution

Navigate to:

```text
Manage Jenkins → Credentials
```

Verify:

- Credential exists.
- Correct Credential ID is used.
- Proper scope is selected.

---

# 10. Workspace Issues

## Problem

Files are missing during the build.

## Solution

Clean the workspace before running the pipeline:

```groovy
cleanWs()
```

Or manually delete the workspace from the Jenkins job.

---

# 11. Pipeline Never Starts

## Possible Causes

- Jenkins service stopped.
- Invalid pipeline configuration.
- Build waiting in queue.

## Solution

Restart Jenkins:

Linux

```bash
sudo systemctl restart jenkins
```

Windows

```powershell
Restart-Service Jenkins
```

---

# 12. Console Output Missing

## Possible Causes

- Pipeline terminated immediately.
- Jenkins service failed.
- Incorrect job configuration.

## Solution

Review Jenkins logs:

```bash
sudo journalctl -u jenkins -f
```

Verify the pipeline configuration and rerun the build.

---

# 13. Agent Offline

## Problem

Pipeline cannot execute because the assigned agent is unavailable.

## Solution

Navigate to:

```text
Manage Jenkins → Nodes
```

Ensure:

- Agent is online.
- Java is installed on the agent.
- Network connectivity is working.

---

# 14. Pipeline Hangs Indefinitely

## Possible Causes

- Waiting for manual input.
- Infinite loop in the pipeline.
- External command never finishes.

## Solution

- Check the **Console Output**.
- Verify whether an `input` step is awaiting approval.
- Terminate the build if necessary and fix the pipeline logic.

---

# Useful Verification Commands

Check Jenkins service:

```bash
sudo systemctl status jenkins
```

Restart Jenkins:

```bash
sudo systemctl restart jenkins
```

View Jenkins logs:

```bash
sudo journalctl -u jenkins -f
```

Verify Git:

```bash
git --version
```

Verify Java:

```bash
java --version
```

Check repository status:

```bash
git status
```

---

# Best Practices

- Store the `Jenkinsfile` in the repository root.
- Validate pipeline syntax before committing.
- Use Declarative Pipelines unless advanced scripting is required.
- Keep stages focused on a single responsibility.
- Use Jenkins Credentials instead of hardcoding secrets.
- Review **Console Output** after every build.
- Test pipeline changes in a development environment first.
- Keep Jenkins and plugins updated.

---

# Summary

Most Jenkins Pipeline issues are caused by syntax errors, incorrect `Jenkinsfile` placement, Git configuration problems, agent availability, or platform-specific command mismatches. The **Console Output** and Jenkins logs are the primary tools for diagnosing and resolving pipeline failures.# Troubleshooting

This section covers common problems encountered while creating and running Jenkins Pipelines.

---

# Pipeline Is Not Starting

## Problem

The Jenkins job remains stuck with:

```text
Waiting for next available executor
```

## Possible Causes

- No Jenkins Agent is available.
- The Jenkins Controller is offline.
- The Agent is disconnected.
- All executors are busy.

## Check Jenkins Nodes

Open:

```text
Manage Jenkins → Nodes
```

Check whether the required node is online.

---

# Jenkins Controller Is Offline

## Problem

The Jenkins Controller appears as:

```text
Offline
```

## Check Jenkins Service

```bash
sudo systemctl status jenkins
```

Restart Jenkins:

```bash
sudo systemctl restart jenkins
```

Check the logs:

```bash
sudo journalctl -u jenkins -f
```

---

# Pipeline Syntax Error

## Problem

The Pipeline fails with a Groovy syntax error.

Example:

```text
WorkflowScript: Syntax error
```

## Common Causes

- Missing `{`
- Missing `}`
- Incorrect quotation marks
- Incorrect Pipeline structure

Incorrect:

```groovy
pipeline {

    agent any

    stages

        stage('Build') {
        }

}
```

Correct:

```groovy
pipeline {

    agent any

    stages {

        stage('Build') {
            steps {
                echo 'Building'
            }
        }

    }

}
```

---

# Pipeline Fails at the `sh` Step

## Problem

The Pipeline fails when executing:

```groovy
sh 'some-command'
```

## Possible Causes

- The command does not exist.
- The required software is not installed.
- The command is not available in the PATH.
- The Pipeline is running on a different Agent.

## Test the Command on the Agent

```bash
which docker
```

```bash
which mvn
```

```bash
which git
```

---

# `docker: not found`

## Problem

The Pipeline fails with:

```text
docker: not found
```

## Cause

Docker is not installed or cannot be found by the Jenkins execution environment.

## Check Docker

```bash
docker --version
```

```bash
which docker
```

Check Docker as Jenkins:

```bash
sudo -u jenkins which docker
```

## Solution

Install Docker:

```bash
sudo apt update
sudo apt install docker.io -y
```

Start Docker:

```bash
sudo systemctl start docker
```

Verify:

```bash
docker --version
```

---

# Docker Permission Denied

## Problem

The Pipeline fails with:

```text
permission denied while trying to connect to the Docker daemon socket
```

## Cause

The Jenkins user does not have permission to communicate with Docker.

## Solution

Add Jenkins to the Docker group:

```bash
sudo usermod -aG docker jenkins
```

Restart Jenkins:

```bash
sudo systemctl restart jenkins
```

Test:

```bash
sudo -u jenkins docker ps
```

If this command works, Jenkins can access Docker.

---

# Docker Works for Ubuntu but Not Jenkins

## Problem

This works:

```bash
docker ps
```

But the Jenkins Pipeline fails.

## Cause

The Ubuntu user and Jenkins user are different Linux users.

Docker permissions for one user do not automatically apply to another user.

## Test Jenkins Access

```bash
sudo -u jenkins docker ps
```

If permission is denied:

```bash
sudo usermod -aG docker jenkins
```

Restart Jenkins:

```bash
sudo systemctl restart jenkins
```

Test again:

```bash
sudo -u jenkins docker ps
```

---

# Docker Works on One Machine but Not the Jenkins Agent

## Problem

Docker works on the server, but the Pipeline reports:

```text
docker: not found
```

## Cause

The Pipeline may be executing on a different Jenkins Agent.

Example:

```text
Jenkins Controller
        │
        ▼
Agent 1
        │
        └── Docker Installed

Pipeline
        │
        ▼
Agent 2
        │
        └── Docker Not Installed
```

## Solution

Install Docker on the Agent that executes the Pipeline.

Verify on the Agent:

```bash
docker --version
```

```bash
sudo -u jenkins docker ps
```

---

# `docker compose: command not found`

## Problem

The Pipeline fails with:

```text
docker compose: command not found
```

## Solution

Install Docker Compose V2:

```bash
sudo apt update
sudo apt install docker-compose-v2 -y
```

Verify:

```bash
docker compose version
```

Test as Jenkins:

```bash
sudo -u jenkins docker compose version
```

---

# Git Checkout Fails

## Problem

The Pipeline cannot download the source code.

Possible errors:

```text
Failed to connect to repository
```

or:

```text
Authentication failed
```

## Check the Repository URL

Example:

```text
https://github.com/username/project.git
```

## Test Git

```bash
git --version
```

## Check the Repository Manually

```bash
git clone https://github.com/username/project.git
```

For private repositories, configure the required Jenkins credentials.

---

# Pipeline Cannot Find the Jenkinsfile

## Problem

Jenkins cannot find the Jenkinsfile in the repository.

## Check the File Name

The file should normally be named:

```text
Jenkinsfile
```

The name is case-sensitive.

Correct:

```text
Jenkinsfile
```

Incorrect:

```text
jenkinsfile
```

```text
JenkinsFile
```

## Check the Repository Structure

```text
project/
│
├── Jenkinsfile
├── application/
└── Dockerfile
```

---

# Build Command Fails

## Problem

A build command fails inside the Pipeline.

Example:

```text
mvn: command not found
```

## Check Maven

```bash
mvn --version
```

## Check the Agent

The software required for the build must be installed on the machine executing the Pipeline.

Example:

```text
Pipeline
    │
    ▼
Jenkins Agent
    │
    └── Maven must be installed here
```

---

# Docker Build Fails

## Problem

The Pipeline reaches the Docker build stage but fails.

Example:

```text
failed to read Dockerfile
```

## Check the Current Directory

```groovy
sh 'pwd'
```

```groovy
sh 'ls -la'
```

## Check for the Dockerfile

```bash
ls Dockerfile
```

The Dockerfile must exist in the expected working directory.

Example:

```text
Project
│
├── Jenkinsfile
├── Dockerfile
└── application/
```

---

# Docker Image Build Fails

## Problem

The command fails:

```bash
docker build -t my-app .
```

## Possible Causes

- Dockerfile does not exist.
- Incorrect Dockerfile syntax.
- Required files are missing.
- The build context is incorrect.

## Test Manually

```bash
docker build -t my-app .
```

Check the Dockerfile:

```bash
cat Dockerfile
```

---

# Docker Container Does Not Start

## Problem

The image builds successfully, but the container stops immediately.

## Check Running Containers

```bash
docker ps
```

Check all containers:

```bash
docker ps -a
```

View container logs:

```bash
docker logs <container-id>
```

Example:

```bash
docker logs my-app
```

---

# Port Already in Use

## Problem

A container fails to start because the port is already being used.

Example:

```text
port is already allocated
```

## Check the Port

```bash
sudo ss -ltnp | grep 8080
```

## Check Running Containers

```bash
docker ps
```

Stop the container using the port:

```bash
docker stop <container-id>
```

---

# Workspace Contains Old Files

## Problem

Old files from a previous build cause unexpected behavior.

## Clean the Jenkins Workspace

Inside a Pipeline:

```groovy
cleanWs()
```

Or clean the workspace manually from Jenkins:

```text
Job → Workspace → Wipe Out Workspace
```

---

# Environment Variable Is Empty

## Problem

A Pipeline variable does not contain the expected value.

Example:

```groovy
echo "${APP_NAME}"
```

## Define the Variable

```groovy
environment {
    APP_NAME = 'my-app'
}
```

Example:

```groovy
pipeline {

    agent any

    environment {
        APP_NAME = 'my-app'
    }

    stages {

        stage('Display') {
            steps {
                echo "${APP_NAME}"
            }
        }

    }

}
```

---

# Pipeline Stops During a Stage

## Problem

A Pipeline stops unexpectedly.

## Check the Console Output

Open:

```text
Jenkins Job → Build Number → Console Output
```

Look for:

- The stage that failed
- The exact command that failed
- The error message
- The exit code

The first error is usually the most important one to investigate.

---

# Pipeline Does Not Continue After a Failure

## Problem

A later stage does not execute.

Example:

```text
Build
  │
  ▼
Test ❌
  │
  ✕
Deploy does not execute
```

## Cause

By default, a failed stage causes the Pipeline to stop.

This is expected behavior.

A failed test should normally prevent deployment.

---

# Pipeline Takes Too Long

## Problem

A Pipeline runs indefinitely.

## Add a Timeout

```groovy
pipeline {

    agent any

    options {
        timeout(time: 20, unit: 'MINUTES')
    }

    stages {
        // Stages
    }

}
```

---

# Retry Temporary Failures

For temporary failures, use:

```groovy
retry(3) {
    sh 'some-command'
}
```

Example:

```groovy
stage('Build') {

    steps {

        retry(3) {
            sh 'mvn clean package'
        }

    }

}
```

Use retries carefully. A retry will not fix a permanent configuration error.

---

# Useful Debugging Commands

Print the current user:

```groovy
sh 'whoami'
```

Print the current directory:

```groovy
sh 'pwd'
```

List files:

```groovy
sh 'ls -la'
```

Print environment variables:

```groovy
sh 'printenv'
```

Check Docker:

```groovy
sh 'docker --version'
```

Check Docker containers:

```groovy
sh 'docker ps'
```

---

# Basic Jenkins Pipeline Debugging Example

```groovy
pipeline {

    agent any

    stages {

        stage('Debug Environment') {
            steps {

                sh 'whoami'
                sh 'pwd'
                sh 'ls -la'
                sh 'docker --version'
                sh 'docker ps'

            }
        }

    }

}
```

This helps determine:

- Which user is running the Pipeline.
- Which directory is being used.
- Which files are available.
- Whether Docker is installed.
- Whether Jenkins can access Docker.

---

# Troubleshooting Checklist

When a Pipeline fails, check the following:

```text
1. Read the Console Output
        │
        ▼
2. Find the First Error
        │
        ▼
3. Check the Current Jenkins Agent
        │
        ▼
4. Verify Required Tools
        │
        ▼
5. Check Permissions
        │
        ▼
6. Test the Command Manually
        │
        ▼
7. Run the Pipeline Again
```

Useful commands:

```bash
whoami
```

```bash
pwd
```

```bash
ls -la
```

```bash
docker --version
```

```bash
sudo -u jenkins docker ps
```

```bash
git --version
```

```bash
mvn --version
```

---

# Error Summary

| Error | Meaning | Solution |
|---|---|---|
| `Waiting for next available executor` | No available executor | Check Jenkins nodes and executors |
| `docker: not found` | Docker unavailable | Install or configure Docker |
| `permission denied` | Jenkins cannot access Docker | Add Jenkins to the Docker group |
| `docker compose: command not found` | Docker Compose missing | Install Docker Compose V2 |
| `mvn: command not found` | Maven unavailable | Install Maven or configure the Agent |
| `Failed to connect to repository` | Git repository problem | Check URL and credentials |
| `Dockerfile not found` | Incorrect directory or missing file | Check workspace and build context |
| `port is already allocated` | Port is already in use | Stop the conflicting process/container |
| Pipeline stops after a stage fails | Previous stage failed | Investigate the first failure |
| Pipeline runs indefinitely | No timeout configured | Add a Pipeline timeout |

---

# Important Lesson

Always troubleshoot the **first error** in the Jenkins Console Output.

For example:

```text
docker: not found
permission denied
```

These are different problems.

```text
docker: not found
```

means Jenkins cannot find Docker.

```text
permission denied while trying to connect to Docker
```

means Jenkins found Docker but does not have permission to use it.

Understanding the exact error message is one of the most important skills when working with Jenkins and CI/CD. 1 2 3 4