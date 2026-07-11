# Troubleshooting

This document covers common issues you may encounter before starting your CI/CD journey.

---

# 1. Git Command Not Found

## Problem

```text
'git' is not recognized as an internal or external command
```

## Cause

Git is either not installed or its installation path is not added to the system's PATH environment variable.

## Solution

- Download and install Git.
- Restart your terminal after installation.
- Verify the installation:

```bash
git --version
```

---

# 2. Java Command Not Found

## Problem

```text
'java' is not recognized as an internal or external command
```

## Cause

Java Development Kit (JDK) is not installed or JAVA_HOME/PATH is not configured.

## Solution

Install a supported JDK (such as OpenJDK 17 or 21) and verify:

```bash
java --version
```

---

# 3. Docker Command Not Found

## Problem

```text
'docker' is not recognized as an internal or external command
```

## Cause

Docker Desktop is not installed or is not running.

## Solution

- Install Docker Desktop.
- Start Docker Desktop.
- Verify:

```bash
docker --version
```

---

# 4. Git Username or Email Not Configured

## Problem

Git asks you to configure your identity when making a commit.

## Solution

Configure your Git identity:

```bash
git config --global user.name "Your Name"
git config --global user.email "your-email@example.com"
```

Verify:

```bash
git config --global --list
```

---

# 5. Unable to Clone a Git Repository

## Possible Causes

- Incorrect repository URL
- Repository is private
- Authentication failure
- No internet connection

## Solution

- Verify the repository URL.
- Check your GitHub permissions.
- Authenticate using a Personal Access Token (PAT) or SSH key if required.

---

# 6. Internet Connectivity Issues

## Symptoms

- Unable to clone repositories
- Package downloads fail
- Git operations time out

## Solution

- Check your internet connection.
- Verify firewall or proxy settings.
- Retry after reconnecting.

---

# 7. Incorrect Git Version

## Check Installed Version

```bash
git --version
```

If Git is outdated, download and install the latest stable version.

---

# 8. Incorrect Java Version

Some CI/CD tools require a supported Java version.

Check your version:

```bash
java --version
```

If necessary, install a compatible LTS version (Java 17 or Java 21).

---

# Best Practices

- Keep Git updated.
- Install a supported JDK version.
- Verify software installations before proceeding.
- Restart your terminal after installing new software.
- Use official installation sources.
- Ensure a stable internet connection.

---

# Useful Verification Commands

```bash
git --version
```

```bash
java --version
```

```bash
docker --version
```

```bash
git config --global --list
```

---

# Summary

Before moving to the next chapter, ensure that:

- Git is installed and configured.
- Java is installed and working.
- Docker is installed (optional for now).
- Internet connectivity is available.
- You can execute all verification commands without errors.

Once these prerequisites are met, you are ready to continue with **Episode 02 – CI/CD Workflow**.