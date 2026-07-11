# Episode 05 - First Freestyle Job

## Overview

A Freestyle Project is the simplest job type in Jenkins and is often the first step in learning Continuous Integration (CI). It provides a graphical interface for configuring build tasks without writing pipeline code.

In this chapter, you will create your first Jenkins Freestyle Project, execute a build, and analyze the build results using the Jenkins Dashboard.

---

# Learning Objectives

After completing this chapter, you will be able to:

- Create a Jenkins Freestyle Project
- Understand the components of a Freestyle Job
- Configure build steps
- Execute a build manually
- View Console Output
- Analyze build results
- Understand the Jenkins workspace

---

# What is a Freestyle Project?

A Freestyle Project is a Jenkins job that allows users to automate simple tasks using the Jenkins web interface.

Typical tasks include:

- Running Shell scripts
- Executing Batch commands
- Building applications
- Running automated tests
- Generating reports

Freestyle Projects are ideal for beginners but are generally replaced by Pipelines in modern production environments.

---

# Freestyle Job Architecture

```text
Developer
     │
     ▼
Create Freestyle Project
     │
     ▼
Configure Job
     │
     ▼
Add Build Steps
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

# Prerequisites

Before creating a Freestyle Job, ensure:

- Jenkins is installed and running.
- Java is installed.
- Git is installed.
- You can access the Jenkins Dashboard.
- Administrator access is available.

---

# Step 1 - Open Jenkins Dashboard

Open your browser and navigate to:

```text
http://localhost:8080
```

Log in using your Jenkins administrator account.

---

# Step 2 - Create a New Job

1. Click **New Item**.
2. Enter a job name (for example, `Hello-Jenkins`).
3. Select **Freestyle Project**.
4. Click **OK**.

---

# Step 3 - Configure the Job

The configuration page contains several sections:

### General

Configure the job name, description, and optional project settings.

### Source Code Management (SCM)

Choose the source code repository.

Options include:

- None
- Git
- Subversion

For this example, select **None**.

### Build Triggers

Choose how the job starts.

Examples:

- Build Now (Manual)
- Poll SCM
- GitHub Webhook
- Scheduled Build

For this example, we will trigger the build manually.

### Build Environment

Configure environment-related options such as:

- Delete workspace before build
- Inject environment variables

### Build Steps

Click **Add Build Step**.

Choose:

**Linux/macOS**

```
Execute Shell
```

**Windows**

```
Execute Windows Batch Command
```

Example:

Linux

```bash
echo "Hello Jenkins!"
pwd
date
```

Windows

```cmd
echo Hello Jenkins!
cd
date /T
```

### Post-build Actions

Examples include:

- Archive Artifacts
- Send Email Notifications
- Publish Test Results
- Trigger Other Jobs

For this lab, no post-build action is required.

Click **Save**.

---

# Step 4 - Run the Job

Click:

```text
Build Now
```

Jenkins immediately schedules and executes the build.

---

# Step 5 - View Console Output

Click the build number in **Build History**, then select:

```text
Console Output
```

Example output:

```text
Started by user admin

Building in workspace /var/lib/jenkins/workspace/Hello-Jenkins

Hello Jenkins!

Finished: SUCCESS
```

---

# Understanding the Workspace

Each Freestyle Job has its own workspace.

Example locations:

Linux

```text
/var/lib/jenkins/workspace/
```

Windows

```text
C:\ProgramData\Jenkins\.jenkins\workspace\
```

The workspace stores:

- Source code
- Temporary files
- Build artifacts
- Generated reports

---

# Build Results

After execution, Jenkins displays one of the following results:

| Status | Description |
|----------|-------------|
| ✅ Success | Build completed successfully |
| ❌ Failed | Build encountered an error |
| ⚠️ Unstable | Build completed but tests failed |
| ⛔ Aborted | Build was stopped manually |

---

# Common Build Workflow

```text
Login
     │
     ▼
Create Job
     │
     ▼
Configure Build
     │
     ▼
Save
     │
     ▼
Build Now
     │
     ▼
Console Output
     │
     ▼
Build Status
```

---

# Best Practices

- Use meaningful job names.
- Add descriptions to every job.
- Keep build scripts simple.
- Store source code in Git.
- Review Console Output after each build.
- Archive important build artifacts.
- Clean workspaces periodically.

---

# Freestyle Project vs Pipeline

| Feature | Freestyle Project | Pipeline |
|----------|-------------------|-----------|
| Configuration | GUI | Jenkinsfile |
| Version Control | Limited | Full |
| Complexity | Simple | Advanced |
| Reusability | Low | High |
| Recommended for Production | No | Yes |

---

# Advantages

- Easy to learn
- Simple configuration
- Excellent for beginners
- Supports numerous plugins
- Quick setup

---

# Limitations

- Difficult to maintain at scale
- Configuration stored in Jenkins UI
- Limited version control
- Not ideal for complex CI/CD workflows

---

# Key Takeaways

- Freestyle Projects are the easiest way to learn Jenkins.
- Jobs are created and configured through the Jenkins Dashboard.
- Build Steps define the work Jenkins performs.
- Console Output is the primary tool for monitoring and debugging builds.
- Modern production environments generally prefer Jenkins Pipelines over Freestyle Projects.

---

# References

- Jenkins Official Documentation
- Jenkins User Handbook
- Git Documentation

---

# Next Topic

➡️ **Episode 06 – Jenkins Pipeline**

In the next chapter, we will learn about Jenkins Pipelines, understand Pipeline as Code, create our first pipeline, and compare it with Freestyle Projects.