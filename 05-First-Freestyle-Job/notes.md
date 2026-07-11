# Notes

## What is a Freestyle Project?

A Freestyle Project is the simplest and most commonly used job type in Jenkins. It allows users to automate basic tasks such as compiling code, running scripts, executing tests, and generating reports.

It is ideal for beginners who are learning Jenkins before moving to Pipeline projects.

---

# Why Use a Freestyle Project?

Freestyle Projects are useful for:

- Learning Jenkins basics
- Running Shell or Batch scripts
- Building applications
- Executing automated tasks
- Testing Jenkins integrations
- Creating simple CI workflows

---

# Freestyle Job Workflow

```text
Developer
     │
     ▼
Create Freestyle Job
     │
     ▼
Configure Build Steps
     │
     ▼
Save Configuration
     │
     ▼
Build Now
     │
     ▼
Console Output
     │
     ▼
Build Result
```

---

# Components of a Freestyle Job

A Freestyle Project consists of several configuration sections:

- General
- Source Code Management (SCM)
- Build Triggers
- Build Environment
- Build Steps
- Post-build Actions

Each section controls a specific part of the build process.

---

# Source Code Management (SCM)

SCM connects Jenkins to a version control system.

Common SCM tools:

- Git
- GitHub
- GitLab
- Bitbucket

If no repository is required, select:

```text
None
```

---

# Build Triggers

Build Triggers define when a job should start.

Common options:

- Build Now (Manual)
- GitHub Webhook
- Poll SCM
- Scheduled (CRON)
- Remote Trigger

---

# Build Environment

The Build Environment prepares the system before executing build steps.

Examples:

- Delete workspace before build
- Use secret text
- Inject environment variables

---

# Build Steps

Build Steps define the actual work performed by Jenkins.

Linux/macOS:

```bash
echo "Hello Jenkins"
```

Windows:

```cmd
echo Hello Jenkins
```

Build steps can include:

- Shell scripts
- Batch commands
- Maven builds
- Gradle builds
- Docker commands

---

# Post-build Actions

These actions occur after the build completes.

Examples:

- Archive artifacts
- Send email notifications
- Trigger another job
- Publish test reports

---

# Workspace

Each Jenkins job has its own workspace.

The workspace stores:

- Source code
- Build files
- Generated artifacts
- Temporary files

Workspace example:

Linux

```text
/var/lib/jenkins/workspace/
```

Windows

```text
C:\ProgramData\Jenkins\.jenkins\workspace\
```

---

# Build Status

Jenkins displays the result of every build.

| Status | Meaning |
|----------|----------|
| Success | Build completed successfully |
| Failed | Build encountered an error |
| Unstable | Build completed but tests failed |
| Aborted | Build was stopped manually |

---

# Console Output

Console Output displays the logs generated during the build.

It is the first place to check when troubleshooting build failures.

---

# Advantages

- Easy to configure
- Beginner-friendly
- Supports plugins
- Executes scripts
- Integrates with Git
- Suitable for simple automation tasks

---

# Limitations

- Difficult to manage large workflows
- Configuration stored in the Jenkins UI
- Not ideal for version control
- Less flexible than Pipeline jobs

---

# Best Practices

- Use meaningful job names.
- Keep build steps simple.
- Store source code in Git.
- Review Console Output after every build.
- Archive important build artifacts.
- Clean workspaces regularly.
- Use Pipelines for complex automation.

---

# Common Use Cases

- Compile applications
- Execute Shell scripts
- Run Batch commands
- Run unit tests
- Generate reports
- Build Docker images
- Deploy small applications

---

# Interview Questions

### What is a Freestyle Project?

A Freestyle Project is a basic Jenkins job that automates tasks such as building, testing, and running scripts.

---

### What is the purpose of Build Steps?

Build Steps define the commands or scripts Jenkins executes during a build.

---

### What is the Workspace?

The Workspace is the directory where Jenkins stores source code, build files, and generated artifacts for a specific job.

---

### What is Console Output?

Console Output displays the logs generated while a Jenkins job is running and is used for monitoring and troubleshooting.

---

# Key Takeaways

- Freestyle Projects are the simplest Jenkins job type.
- They are ideal for learning Jenkins and basic CI concepts.
- A job consists of SCM, Build Triggers, Build Steps, and Post-build Actions.
- Console Output is essential for debugging.
- For complex workflows, Jenkins Pipelines are the preferred approach.