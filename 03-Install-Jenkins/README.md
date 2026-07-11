# Episode 03 - Install Jenkins

## Overview

Jenkins is one of the most popular open-source automation servers used to implement Continuous Integration (CI) and Continuous Delivery (CD). It automates repetitive tasks such as building applications, running automated tests, and deploying software.

Jenkins supports hundreds of plugins, allowing seamless integration with tools like Git, Docker, Kubernetes, Maven, SonarQube, AWS, Azure, and many others.

This chapter covers the installation and initial configuration of Jenkins.

---

# Learning Objectives

After completing this chapter, you will be able to:

- Understand what Jenkins is
- Install Jenkins on Linux and Windows
- Verify Java installation
- Start and manage the Jenkins service
- Unlock Jenkins using the initial administrator password
- Install recommended plugins
- Create the first administrator account
- Access the Jenkins Dashboard

---

# What is Jenkins?

Jenkins is an open-source automation server written in Java.

It automates the software delivery lifecycle by executing predefined jobs whenever a trigger occurs, such as:

- Code push
- Pull Request
- Scheduled execution
- Manual trigger
- Webhook

Instead of performing builds and deployments manually, Jenkins executes them automatically.

---

# Why Use Jenkins?

Without Jenkins:

- Manual builds
- Manual testing
- Manual deployments
- Slow software releases
- Increased human error

With Jenkins:

- Automated builds
- Automated testing
- Automated deployments
- Faster feedback
- Reliable releases
- Improved collaboration

---

# Jenkins Architecture

```text
                 Developer
                     │
                     ▼
             Push Code to GitHub
                     │
                     ▼
                 Jenkins Server
                     │
      ┌──────────────┼──────────────┐
      ▼              ▼              ▼
    Build          Testing       Code Analysis
      │
      ▼
 Package / Docker Image
      │
      ▼
   Deployment
      │
      ▼
 Monitoring & Notifications
```

---

# Prerequisites

Before installing Jenkins, ensure the following software is available:

- Java 17 or Java 21 (LTS)
- Git
- Internet connection
- Administrator or sudo privileges
- Minimum 2 GB RAM (4 GB recommended)

---

# Installing Jenkins on Ubuntu

## Step 1 – Update Package Index

```bash
sudo apt update
```

---

## Step 2 – Install Java

```bash
sudo apt install openjdk-21-jdk -y
```

Verify installation:

```bash
java --version
```

---

## Step 3 – Add Jenkins Repository

Import the Jenkins GPG key:

```bash
curl -fsSL https://pkg.jenkins.io/debian-stable/jenkins.io-2023.key | sudo tee \
/usr/share/keyrings/jenkins-keyring.asc > /dev/null
```

Add the repository:

```bash
echo deb [signed-by=/usr/share/keyrings/jenkins-keyring.asc] \
https://pkg.jenkins.io/debian-stable binary/ | sudo tee \
/etc/apt/sources.list.d/jenkins.list > /dev/null
```

---

## Step 4 – Install Jenkins

```bash
sudo apt update
sudo apt install jenkins -y
```

---

## Step 5 – Start Jenkins

```bash
sudo systemctl start jenkins
```

Enable Jenkins at boot:

```bash
sudo systemctl enable jenkins
```

Verify status:

```bash
sudo systemctl status jenkins
```

---

# Installing Jenkins on Windows

1. Install Java (JDK 17 or JDK 21).
2. Download the Jenkins Windows installer.
3. Run the installer with Administrator privileges.
4. Follow the installation wizard.
5. Jenkins will be installed as a Windows Service.
6. Open your browser and navigate to:

```text
http://localhost:8080
```

---

# Unlock Jenkins

During the first launch, Jenkins displays an unlock screen.

Retrieve the administrator password.

Linux:

```bash
sudo cat /var/lib/jenkins/secrets/initialAdminPassword
```

Windows:

```text
C:\ProgramData\Jenkins\.jenkins\secrets\initialAdminPassword
```

Copy the password and paste it into the Jenkins unlock page.

---

# Install Recommended Plugins

After unlocking Jenkins:

1. Choose **Install Suggested Plugins**.
2. Jenkins downloads and installs the required plugins.
3. Wait until installation completes.

These plugins provide support for:

- Git
- Pipeline
- Maven
- Docker
- Credentials
- Blue Ocean
- Email Notifications

---

# Create the First Administrator

Provide the following information:

- Username
- Password
- Full Name
- Email Address

Save the configuration.

---

# Access the Jenkins Dashboard

Open:

```text
http://localhost:8080
```

You should now see the Jenkins Dashboard.

---

# Jenkins Home Directory

Linux

```text
/var/lib/jenkins
```

Windows

```text
C:\ProgramData\Jenkins
```

This directory stores:

- Jobs
- Plugins
- Credentials
- Build History
- Configuration
- Logs

---

# Service Management

Common service operations include:

Start Jenkins

```bash
sudo systemctl start jenkins
```

Stop Jenkins

```bash
sudo systemctl stop jenkins
```

Restart Jenkins

```bash
sudo systemctl restart jenkins
```

Check Status

```bash
sudo systemctl status jenkins
```

---

# Common Jenkins Plugins

| Plugin | Purpose |
|---------|---------|
| Git | Connect Jenkins with Git repositories |
| Pipeline | Create CI/CD pipelines |
| Docker | Build and manage Docker containers |
| Blue Ocean | Modern Jenkins user interface |
| Maven Integration | Build Java projects |
| NodeJS | Build Node.js applications |
| Email Extension | Send build notifications |

---

# Security Best Practices

- Change the default administrator password.
- Install plugins only from trusted sources.
- Keep Jenkins updated.
- Use the Jenkins Credentials Store for secrets.
- Restrict administrative access.
- Back up the Jenkins home directory regularly.

---

# Advantages

- Free and open source
- Cross-platform
- Large plugin ecosystem
- Supports Pipeline as Code
- Easy integration with cloud platforms
- Highly extensible

---

# Limitations

- Plugin dependency conflicts
- Requires periodic maintenance
- Resource-intensive for large workloads
- UI can become cluttered in large environments

---

# Best Practices

- Use Pipeline as Code (`Jenkinsfile`).
- Organize jobs into folders.
- Remove unused plugins.
- Back up Jenkins regularly.
- Monitor disk usage.
- Secure credentials using the built-in credential manager.
- Keep Java and Jenkins up to date.

---

# Key Takeaways

- Jenkins is a leading CI/CD automation server.
- Java is a mandatory prerequisite.
- Jenkins uses plugins to extend its functionality.
- The default web interface runs on **port 8080**.
- Jenkins can automate build, test, and deployment processes.
- Proper maintenance and security are essential for production environments.

---

# References

- Jenkins Official Documentation
- OpenJDK Documentation
- Git Documentation
- Docker Documentation

---

# Next Topic

➡️ **Episode 04 – Jenkins Dashboard**

In the next chapter, we will explore the Jenkins Dashboard, understand its interface, configure global settings, manage plugins, and create our first Jenkins job.