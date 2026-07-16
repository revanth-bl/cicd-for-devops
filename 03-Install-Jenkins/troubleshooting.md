# Troubleshooting

This section contains common problems encountered while installing Jenkins, configuring Docker, and preparing the Jenkins environment for CI/CD pipelines.

---

# Jenkins Service Is Not Running

## Problem

The Jenkins dashboard cannot be opened.

## Check Jenkins Status

```bash
sudo systemctl status jenkins
```

## Start Jenkins

```bash
sudo systemctl start jenkins
```

## Restart Jenkins

```bash
sudo systemctl restart jenkins
```

## Enable Jenkins at Boot

```bash
sudo systemctl enable jenkins
```

---

# Jenkins Dashboard Cannot Be Accessed

## Problem

The Jenkins service is running, but the dashboard cannot be opened.

Jenkins normally runs on port:

```text
8080
```

For a local server:

```text
http://localhost:8080
```

For a remote server:

```text
http://<server-ip>:8080
```

## Check Whether Jenkins Is Listening on Port 8080

```bash
sudo ss -ltnp | grep 8080
```

## Check the Firewall

```bash
sudo ufw status
```

Allow Jenkins:

```bash
sudo ufw allow 8080
```

---

# Jenkins Initial Administrator Password Not Found

## Problem

The initial administrator password cannot be found.

## Solution

Run:

```bash
sudo cat /var/lib/jenkins/secrets/initialAdminPassword
```

If the file does not exist, check whether Jenkins is installed correctly:

```bash
sudo systemctl status jenkins
```

---

# Java Not Found

## Problem

Jenkins cannot start because Java is missing.

Example error:

```text
java: command not found
```

## Check Java

```bash
java --version
```

## Install Java

```bash
sudo apt update
sudo apt install openjdk-21-jdk -y
```

Verify:

```bash
java --version
```

Restart Jenkins:

```bash
sudo systemctl restart jenkins
```

---

# Docker Command Not Found

## Problem

A Jenkins pipeline fails with:

```text
docker: not found
```

## Cause

Docker may be:

- Not installed
- Not available in the system PATH
- Installed on a different Jenkins Agent

## Check Docker

```bash
docker --version
```

Find Docker:

```bash
which docker
```

Check whether Jenkins can find Docker:

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

# Permission Denied While Using Docker

## Problem

Jenkins can find Docker, but the pipeline fails with:

```text
permission denied while trying to connect to the Docker daemon socket
```

or:

```text
permission denied while trying to connect to the Docker API
```

## Cause

The `jenkins` user does not have permission to access Docker.

## Solution

Add Jenkins to the Docker group:

```bash
sudo usermod -aG docker jenkins
```

Restart Jenkins:

```bash
sudo systemctl restart jenkins
```

Test Docker access as Jenkins:

```bash
sudo -u jenkins docker ps
```

If the command works, Jenkins can communicate with Docker.

---

# Docker Works for Ubuntu but Not Jenkins

## Problem

Docker works when executed as the Ubuntu user:

```bash
docker ps
```

But the Jenkins pipeline fails.

## Cause

The `ubuntu` and `jenkins` users are different Linux users.

Docker permissions for one user do not automatically apply to another user.

## Test Jenkins Docker Access

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

# Docker Service Is Not Running

## Problem

Docker is installed, but Docker commands fail.

## Check Docker Status

```bash
sudo systemctl status docker
```

## Start Docker

```bash
sudo systemctl start docker
```

## Enable Docker at Boot

```bash
sudo systemctl enable docker
```

---

# Docker Compose Command Not Found

## Problem

The following command fails:

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

# Docker Compose Permission Denied

## Problem

Docker Compose is installed, but Jenkins cannot use it.

## Test

```bash
sudo -u jenkins docker compose version
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
sudo -u jenkins docker compose version
```

---

# Docker Works on the Controller but Not on the Agent

## Problem

Docker is installed on one machine, but the Jenkins pipeline reports:

```text
docker: not found
```

## Cause

The pipeline is running on a different Jenkins Agent.

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

Docker must be installed and configured on the Jenkins Agent that executes the pipeline.

Check the Agent:

```bash
docker --version
```

```bash
sudo -u jenkins docker ps
```

---

# Jenkins Logs

View Jenkins logs:

```bash
sudo journalctl -u jenkins
```

Follow live Jenkins logs:

```bash
sudo journalctl -u jenkins -f
```

These logs can help identify:

- Startup failures
- Java problems
- Plugin errors
- Permission problems
- Configuration issues

---

# Docker Logs

View Docker service logs:

```bash
sudo journalctl -u docker
```

Follow live Docker logs:

```bash
sudo journalctl -u docker -f
```

---

# Debugging Checklist

When Jenkins cannot use Docker, check the following:

```bash
docker --version
```

```bash
which docker
```

```bash
sudo -u jenkins which docker
```

```bash
sudo -u jenkins docker --version
```

```bash
sudo -u jenkins docker ps
```

```bash
groups jenkins
```

```bash
sudo systemctl status docker
```

```bash
sudo systemctl status jenkins
```

---

# Error Summary

| Error | Meaning | Solution |
|---|---|---|
| `java: command not found` | Java is not installed | Install Java |
| `docker: not found` | Docker is missing or unavailable in PATH | Install or configure Docker |
| `permission denied` | Jenkins cannot access Docker | Add Jenkins to the Docker group |
| `docker compose: command not found` | Docker Compose is missing | Install Docker Compose V2 |
| Jenkins dashboard unavailable | Jenkins or firewall problem | Check Jenkins service and port 8080 |
| Docker works for Ubuntu but not Jenkins | Different user permissions | Configure Docker access for Jenkins |
| Docker works on Controller but not Agent | Docker missing on executing Agent | Install Docker on the Agent |

---

# Important Lesson

Different errors indicate different problems:

```text
docker: not found
```

Docker is not installed or cannot be found.

```text
permission denied while trying to connect to Docker
```

Docker is installed, but the Jenkins user does not have permission to use it.

```text
docker compose: command not found
```

Docker Compose is not installed or unavailable.

Understanding the exact error message makes troubleshooting much faster.