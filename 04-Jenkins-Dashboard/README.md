# Episode 04 - Jenkins Dashboard

## Overview

The Jenkins Dashboard is the primary web interface used to manage Jenkins. It provides administrators and developers with a centralized location to create jobs, monitor builds, configure system settings, manage plugins, and administer CI/CD pipelines.

After installing Jenkins successfully, the Dashboard becomes the starting point for all Jenkins activities.

---

# Learning Objectives

After completing this chapter, you will be able to:

- Navigate the Jenkins Dashboard
- Understand the purpose of each dashboard section
- Create and manage Jenkins jobs
- Monitor build history and build queues
- Configure Jenkins settings
- Manage plugins and credentials
- Understand Jenkins nodes and executors

---

# Accessing the Dashboard

By default, Jenkins runs on port **8080**.

Local machine:

```text
http://localhost:8080
```

Remote server:

```text
http://<server-ip>:8080
```

After logging in, the Jenkins Dashboard is displayed.

---

# Jenkins Dashboard Layout

```text
+------------------------------------------------------------+
| Jenkins Logo            Search              User Profile   |
+------------------------------------------------------------+

 Dashboard

 ├── New Item
 ├── People
 ├── Build History
 ├── Manage Jenkins
 ├── Credentials
 ├── Nodes
 └── Existing Jobs

--------------------------------------------------------------

Build Queue

Executor Status

Recent Builds

System Messages
```

---

# Dashboard Components

## Dashboard

The Dashboard provides an overview of the Jenkins instance.

It displays:

- Existing jobs
- Build status
- Build history
- Build queue
- Executor status
- System messages

It serves as the central navigation page for all Jenkins operations.

---

## New Item

The **New Item** option is used to create new Jenkins jobs.

Common job types include:

- Freestyle Project
- Pipeline
- Multibranch Pipeline
- Folder
- Organization Folder

Each job type serves a different purpose depending on the project requirements.

---

## Build History

Build History displays all previously executed jobs.

Information includes:

- Build number
- Build status
- Execution time
- Build duration
- Console output

Status icons:

| Icon | Meaning |
|------|----------|
| 🟢 | Success |
| 🔴 | Failed |
| 🟡 | Unstable |
| ⚪ | Aborted |

Build history is useful for troubleshooting and auditing pipeline executions.

---

## Build Queue

The Build Queue displays jobs waiting for execution.

Reasons why jobs remain in the queue include:

- Another build is currently running.
- No executor is available.
- Required resources are busy.

Once resources become available, Jenkins automatically starts the queued job.

---

## Executor Status

Executors are responsible for running Jenkins jobs.

The Executor Status section displays:

- Running builds
- Idle executors
- Busy executors
- Connected agents

Monitoring executor usage helps optimize build performance.

---

# Manage Jenkins

The **Manage Jenkins** page contains all administrative settings.

Important sections include:

- System Configuration
- Global Tool Configuration
- Plugin Manager
- Credentials
- Nodes
- Security
- Users
- System Information
- Script Console
- Reload Configuration
- Restart Jenkins

Most administrative tasks are performed from this page.

---

# Plugin Manager

Plugins extend Jenkins functionality.

Common plugins include:

| Plugin | Purpose |
|---------|----------|
| Git | Git integration |
| Pipeline | Pipeline support |
| Docker | Docker integration |
| Blue Ocean | Modern UI |
| Maven | Java builds |
| NodeJS | Node.js builds |
| Email Extension | Build notifications |

Plugin Manager allows you to:

- Install plugins
- Update plugins
- Disable plugins
- Remove plugins

---

# Credentials

Credentials securely store sensitive information used by Jenkins jobs.

Examples include:

- GitHub Personal Access Tokens
- SSH Keys
- AWS Credentials
- Docker Registry Credentials
- Username and Password

Credentials should never be stored directly inside Jenkins jobs or pipeline scripts.

---

# Nodes

A Node is a machine capable of executing Jenkins jobs.

Types of nodes:

## Controller

- Manages Jenkins
- Schedules builds
- Stores configurations

## Agent

- Executes build jobs
- Supports distributed builds
- Reduces controller workload

Large organizations commonly use multiple agents for scalability.

---

# Global Tool Configuration

This section configures tools that Jenkins uses during builds.

Examples:

- Git
- JDK
- Maven
- Gradle
- Node.js
- Docker

Configured tools become available to Jenkins jobs and pipelines.

---

# Users and Security

Jenkins supports multiple users.

Typical roles include:

- Administrator
- Developer
- Read-only User

Authentication can be integrated with:

- Local users
- LDAP
- Active Directory
- OAuth providers

Proper role-based access control improves security.

---

# Typical Workflow

```text
Login
   │
   ▼
Dashboard
   │
   ▼
Create Job
   │
   ▼
Configure Job
   │
   ▼
Build Now
   │
   ▼
Console Output
   │
   ▼
Build History
```

---

# Best Practices

- Keep plugins updated.
- Remove unused plugins.
- Organize jobs into folders.
- Store secrets in Jenkins Credentials.
- Regularly review build history.
- Monitor executor usage.
- Restrict administrative privileges.
- Back up Jenkins configuration regularly.

---

# Advantages

- Centralized management
- User-friendly interface
- Real-time build monitoring
- Extensive plugin ecosystem
- Scalable architecture
- Easy integration with DevOps tools

---

# Limitations

- Plugin compatibility issues
- Can become resource-intensive
- Requires periodic maintenance
- Large numbers of jobs may clutter the interface

---

# Key Takeaways

- The Jenkins Dashboard is the central hub for managing CI/CD pipelines.
- **Manage Jenkins** provides access to administrative settings.
- Plugins extend Jenkins functionality.
- Credentials securely manage sensitive information.
- Build Queue and Build History help monitor job execution.
- Nodes enable distributed and scalable builds.

---

# References

- Jenkins Official Documentation
- Jenkins Plugin Index
- Jenkins User Handbook

---

# Next Topic

➡️ **Episode 05 – First Freestyle Job**

In the next chapter, we will create our first Jenkins Freestyle Project, configure build steps, execute a job, and analyze the build results.