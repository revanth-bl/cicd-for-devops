# Notes

## What is the Jenkins Dashboard?

The Jenkins Dashboard is the main web interface used to manage Jenkins. It provides access to jobs, builds, pipelines, plugins, users, system settings, and administrative tools.

Default URL:

```text
http://localhost:8080
```

---

# Main Dashboard Components

After logging in, the Jenkins Dashboard typically contains:

- Dashboard
- Build Queue
- Build Executor Status
- Manage Jenkins
- New Item
- People
- Credentials
- Build History

These sections help administrators and developers monitor and manage CI/CD pipelines.

---

# Dashboard Layout

```text
+------------------------------------------------------+
| Jenkins Logo            Search      User Profile     |
+------------------------------------------------------+

 Dashboard

 ├── New Item
 ├── People
 ├── Build History
 ├── Manage Jenkins
 ├── Credentials
 ├── Nodes
 └── Existing Jobs

--------------------------------------------------------

Build Queue

Executor Status

Recent Builds

System Messages
```

---

# Manage Jenkins

The **Manage Jenkins** page contains administrative settings.

Common options include:

- System Configuration
- Global Tool Configuration
- Plugin Manager
- Credentials
- Nodes
- Users
- System Information
- Reload Configuration
- Restart Jenkins
- Manage Plugins

---

# Plugin Manager

Plugins extend Jenkins functionality.

Common plugins include:

- Git Plugin
- Pipeline Plugin
- Docker Plugin
- Maven Integration
- Blue Ocean
- NodeJS Plugin
- Email Extension

Plugins can be:

- Installed
- Updated
- Disabled
- Removed

---

# Credentials

Credentials securely store sensitive information.

Examples:

- GitHub Personal Access Tokens
- SSH Keys
- AWS Access Keys
- Docker Registry Credentials
- Username & Password

Never hardcode credentials inside Jenkins jobs.

---

# Nodes

A Node is a machine that executes Jenkins jobs.

Types:

- Controller (Master)
- Agent (Worker)

Benefits of agents:

- Parallel builds
- Distributed workloads
- Better scalability

---

# Build Queue

The Build Queue shows jobs waiting to execute.

Jobs may wait because:

- Another build is running
- No executor is available
- Resources are busy

---

# Build History

Build History records every job execution.

Each build displays:

- Build number
- Status
- Execution time
- Console output
- Build duration

Status icons:

- 🟢 Success
- 🔴 Failed
- 🟡 Unstable
- ⚪ Aborted

---

# Users

Jenkins supports multiple users.

Roles commonly include:

- Administrator
- Developer
- Viewer

User permissions can be managed using authorization plugins.

---

# Global Tool Configuration

Used to configure development tools such as:

- Git
- JDK
- Maven
- Gradle
- NodeJS
- Docker

These tools become available for Jenkins jobs and pipelines.

---

# System Configuration

Allows administrators to configure:

- Jenkins URL
- Environment variables
- Email notifications
- Number of executors
- Build timeout settings
- Security options

---

# Dashboard Navigation

Typical workflow:

```text
Dashboard
      │
      ▼
Create Job
      │
      ▼
Configure Job
      │
      ▼
Build
      │
      ▼
Console Output
      │
      ▼
Build History
```

---

# Advantages

- User-friendly interface
- Centralized job management
- Real-time build monitoring
- Plugin ecosystem
- Easy administration
- Supports multiple users

---

# Best Practices

- Keep plugins updated.
- Remove unused plugins.
- Organize jobs using folders.
- Secure credentials with Jenkins Credentials.
- Regularly review build history.
- Limit administrator access.
- Monitor executor usage.

---

# Common Dashboard Sections

| Section | Purpose |
|----------|----------|
| Dashboard | Main overview |
| New Item | Create new jobs or pipelines |
| Build History | View previous builds |
| Build Queue | Monitor pending jobs |
| Manage Jenkins | System administration |
| Credentials | Store secrets securely |
| Nodes | Manage build agents |
| Plugin Manager | Install and manage plugins |

---

# Interview Questions

### What is the Jenkins Dashboard?

The Jenkins Dashboard is the main web interface used to create, configure, monitor, and manage Jenkins jobs and system settings.

---

### What is the purpose of the Plugin Manager?

It allows administrators to install, update, disable, and remove Jenkins plugins.

---

### What are Jenkins Nodes?

Nodes are machines that execute Jenkins jobs. The controller manages one or more agent nodes.

---

### Why are Credentials important?

Credentials securely store sensitive information such as passwords, API tokens, SSH keys, and cloud access keys without exposing them in jobs or pipelines.

---

# Key Takeaways

- The Jenkins Dashboard is the central interface for managing CI/CD pipelines.
- **Manage Jenkins** provides access to administrative settings.
- Plugins extend Jenkins functionality.
- Credentials should always be stored securely.
- Build History and Build Queue help monitor pipeline execution.
- Nodes enable distributed and scalable builds.