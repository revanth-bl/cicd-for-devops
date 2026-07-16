# 03 — Install Jenkins

This section covers the installation and initial configuration of Jenkins on an Ubuntu server.

Jenkins is one of the most widely used automation tools in CI/CD. It can automatically build applications, run tests, create Docker images, and deploy applications.

---

## What You Will Learn

- What Jenkins is
- How to install Java
- How to install Jenkins on Ubuntu
- How to start and manage the Jenkins service
- How to access the Jenkins dashboard
- How to install Docker
- How to allow Jenkins to use Docker
- How to install Docker Compose
- How to verify the complete Jenkins environment

---

# What Is Jenkins?

Jenkins is an open-source automation server used to automate software development workflows.

A typical Jenkins workflow looks like this:

```text
Developer
    │
    ▼
GitHub
    │
    ▼
Jenkins
    │
    ├── Build
    │
    ├── Test
    │
    ├── Docker Build
    │
    └── Deploy
```

Instead of manually performing these steps, Jenkins can execute them automatically through jobs and pipelines.

---

# Jenkins in CI/CD

Jenkins can automate the following process:

```text
Code Push
    │
    ▼
Jenkins Triggered
    │
    ▼
Checkout Source Code
    │
    ▼
Build Application
    │
    ▼
Run Tests
    │
    ▼
Build Docker Image
    │
    ▼
Deploy Application
```

This allows development teams to continuously integrate and deliver software.

---

# Jenkins Installation Requirements

Before installing Jenkins, the server requires:

```text
Ubuntu Server
      │
      ▼
Java
      │
      ▼
Jenkins
      │
      ▼
Docker
      │
      ▼
Docker Compose
```

Java is required to run Jenkins.

Docker is commonly used by Jenkins pipelines to:

- Build container images
- Run containers
- Run application services
- Create consistent build environments
- Deploy applications

Docker Compose is useful when an application contains multiple services, such as:

```text
Application
    │
    ├── Flask Application
    │
    └── MySQL Database
```

---

# Jenkins Architecture

A basic Jenkins environment contains a Jenkins Controller and Jenkins Agents.

```text
                 Jenkins Controller
                       │
                       │
                       ▼
                Jenkins Pipeline
                       │
                       ▼
                  Jenkins Agent
                       │
          ┌────────────┼────────────┐
          │            │            │
          ▼            ▼            ▼
        Build        Test        Deploy
```

The Jenkins Controller manages Jenkins and schedules jobs.

The Jenkins Agent performs the actual work defined in the pipeline.

---

# Jenkins and Docker

Jenkins pipelines frequently use Docker.

The execution flow looks like this:

```text
Jenkins Controller
        │
        ▼
Jenkins Agent
        │
        ▼
Jenkins User
        │
        ▼
Docker CLI
        │
        ▼
Docker Daemon
        │
        ▼
Containers / Images
```

For Jenkins to execute Docker commands:

1. Docker must be installed on the machine executing the pipeline.
2. The Docker service must be running.
3. The Jenkins user must have permission to access Docker.

The Jenkins user can be added to the Docker group:

```bash
sudo usermod -aG docker jenkins
```

After changing the group membership, Jenkins must be restarted:

```bash
sudo systemctl restart jenkins
```

Docker access can then be tested with:

```bash
sudo -u jenkins docker ps
```

---

# Installing Jenkins

The installation process is:

```text
Install Java
    │
    ▼
Add Jenkins Repository
    │
    ▼
Install Jenkins
    │
    ▼
Start Jenkins Service
    │
    ▼
Access Jenkins Dashboard
```

The Jenkins dashboard is normally available at:

```text
http://<server-ip>:8080
```

For a local installation:

```text
http://localhost:8080
```

---

# Jenkins Initial Configuration

When Jenkins is accessed for the first time, it requires the initial administrator password.

The password can be retrieved using:

```bash
sudo cat /var/lib/jenkins/secrets/initialAdminPassword
```

After unlocking Jenkins, the initial setup wizard can be completed.

---

# Docker Installation

Docker is installed on the Jenkins server so that Jenkins pipelines can build and run containers.

The workflow is:

```text
Jenkins Pipeline
      │
      ▼
Docker Build
      │
      ▼
Docker Image
      │
      ▼
Docker Container
      │
      ▼
Application
```

Example Docker commands that Jenkins may execute:

```bash
docker build -t my-app .
```

```bash
docker run -d -p 8080:8080 my-app
```

---

# Docker Compose

Docker Compose is used to run multiple containers as one application.

Example:

```text
Docker Compose
      │
      ├── Flask Application
      │
      └── MySQL Database
```

A Jenkins pipeline can start the complete application using:

```bash
docker compose up -d --build
```

The services can be stopped using:

```bash
docker compose down
```

---

# Important Concepts

## Jenkins Controller

The Controller is responsible for:

- Managing Jenkins
- Scheduling jobs
- Managing configuration
- Triggering pipelines
- Assigning work to Agents

---

## Jenkins Agent

An Agent executes the actual pipeline tasks.

For example:

```text
Jenkins Agent
      │
      ├── Checkout Code
      │
      ├── Build Application
      │
      ├── Run Tests
      │
      └── Build Docker Image
```

Docker must be installed on the Agent that executes Docker commands.

Installing Docker on one machine does not automatically install it on every Jenkins Agent.

---

## Jenkins User

Jenkins jobs run using the Linux user:

```text
jenkins
```

This user is different from the default Ubuntu user.

Therefore, Docker permissions must be configured specifically for the Jenkins user.

Example:

```bash
sudo -u jenkins docker ps
```

This command verifies whether Jenkins can access Docker.

---

# Troubleshooting Overview

Common problems include:

| Problem | Meaning |
|---|---|
| `docker: not found` | Docker is not installed or unavailable in PATH |
| `permission denied` | Jenkins cannot access Docker |
| `docker compose: command not found` | Docker Compose is not installed |
| Docker works for Ubuntu but not Jenkins | Different users have different permissions |
| Docker works on Controller but not Agent | Docker is missing on the executing Agent |

Detailed troubleshooting information is available in:

```text
troubleshooting.md
```

---

# Learning Outcome

After completing this section, you should understand:

- What Jenkins is
- Why Java is required
- How to install Jenkins
- How to manage the Jenkins service
- How to access the Jenkins dashboard
- Why Docker is commonly used with Jenkins
- How to give Jenkins permission to use Docker
- Why Docker Compose is useful
- The difference between a Jenkins Controller and Agent
- How Jenkins, Docker, and CI/CD work together

The next step is to explore the Jenkins Dashboard and understand the basic Jenkins interface.