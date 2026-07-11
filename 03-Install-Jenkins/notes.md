# Notes

## What is Jenkins?

Jenkins is an open-source automation server used to implement Continuous Integration (CI) and Continuous Delivery/Deployment (CD).

It automates repetitive tasks such as:

- Building applications
- Running automated tests
- Deploying applications
- Monitoring pipeline execution

Jenkins supports hundreds of plugins, making it one of the most popular CI/CD tools in the DevOps ecosystem.

---

# Why Jenkins?

Without Jenkins:

- Manual builds
- Manual testing
- Manual deployments
- Higher risk of human error
- Slower software releases

With Jenkins:

- Automated builds
- Automated testing
- Automated deployments
- Faster feedback
- Consistent releases

---

# Jenkins Architecture

```text
Developer
     │
     ▼
Git Repository
     │
     ▼
Jenkins
     │
 ┌───┼──────────────┐
 ▼   ▼              ▼
Build Test      Deploy
     │
     ▼
Notifications
```

---

# Jenkins Requirements

Before installing Jenkins, ensure the following prerequisites are met:

- Java 17 or Java 21 (LTS)
- Minimum 2 GB RAM (recommended)
- Internet connection
- Git installed
- Administrator or sudo privileges

---

# Default Jenkins Port

```text
8080
```

Access Jenkins using:

```text
http://localhost:8080
```

or

```text
http://<server-ip>:8080
```

---

# Initial Setup

After installation:

1. Start the Jenkins service.
2. Open Jenkins in a web browser.
3. Retrieve the initial administrator password.
4. Unlock Jenkins.
5. Install the recommended plugins.
6. Create the first administrator account.
7. Access the Jenkins dashboard.

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

Important files stored here include:

- Jobs
- Plugins
- Build history
- Configuration
- Credentials
- Workspace

---

# Important Directories

| Directory | Purpose |
|-----------|----------|
| jobs/ | Stores Jenkins jobs |
| plugins/ | Installed plugins |
| workspace/ | Project workspace |
| secrets/ | Security-related files |
| logs/ | Jenkins logs |

---

# Jenkins Service

Common service operations include:

- Start
- Stop
- Restart
- Check status

These are typically managed using `systemctl` on Linux or the Services console on Windows.

---

# Jenkins Plugins

Plugins extend Jenkins functionality.

Common plugins include:

- Git Plugin
- Pipeline Plugin
- Docker Plugin
- Blue Ocean
- Maven Integration
- NodeJS Plugin
- Email Extension

---

# Security

Jenkins provides:

- User authentication
- Role-based authorization
- Credential management
- Secret storage
- Plugin security updates

Always:

- Change the default administrator password.
- Install only trusted plugins.
- Keep Jenkins updated.

---

# Advantages

- Free and open source
- Cross-platform
- Large plugin ecosystem
- Easy integration with Git, Docker, Kubernetes, and cloud providers
- Supports Pipeline as Code using Jenkinsfile

---

# Limitations

- Plugin compatibility issues
- Requires regular maintenance
- Resource-intensive for large pipelines
- UI can become cluttered with many jobs

---

# Best Practices

- Keep Jenkins updated.
- Use Pipeline as Code (`Jenkinsfile`).
- Back up the Jenkins home directory regularly.
- Remove unused plugins.
- Use credentials instead of hardcoding secrets.
- Monitor disk usage and build history.

---

# Common Installation Checklist

- ✔ Java installed
- ✔ Git installed
- ✔ Jenkins installed
- ✔ Jenkins service running
- ✔ Port 8080 accessible
- ✔ Initial password retrieved
- ✔ Plugins installed
- ✔ Administrator account created

---

# Interview Questions

### What is Jenkins?

Jenkins is an open-source automation server that automates software build, test, and deployment processes.

---

### Why does Jenkins require Java?

Jenkins is a Java-based application and runs on the Java Virtual Machine (JVM).

---

### What is the default Jenkins port?

**8080**

---

### Where is the Jenkins home directory located?

Linux:

```text
/var/lib/jenkins
```

Windows:

```text
C:\ProgramData\Jenkins
```

---

### What is the purpose of Jenkins plugins?

Plugins extend Jenkins functionality by integrating it with various tools, cloud providers, version control systems, testing frameworks, and deployment platforms.

---

# Key Takeaways

- Jenkins is one of the most widely used CI/CD automation servers.
- Java is a mandatory prerequisite.
- Jenkins uses plugins to integrate with the DevOps ecosystem.
- The default web interface is available on port **8080**.
- Keeping Jenkins secure and updated is essential for production environments.