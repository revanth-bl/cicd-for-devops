# Troubleshooting

This document covers common problems encountered while installing and configuring Jenkins.

---

# 1. Java Not Installed

## Problem

```text
java: command not found
```

or

```text
'java' is not recognized as an internal or external command
```

## Cause

Java is not installed or the PATH environment variable is not configured.

## Solution

Verify Java:

```bash
java --version
```

If Java is missing, install JDK 17 or JDK 21 and restart your terminal.

---

# 2. Jenkins Service Failed to Start

## Problem

```text
Job for jenkins.service failed.
```

## Check Service Status

```bash
sudo systemctl status jenkins
```

## View Logs

```bash
sudo journalctl -u jenkins
```

## Possible Causes

- Java not installed
- Incorrect Java version
- Port already in use
- Corrupted installation

---

# 3. Jenkins Dashboard Not Opening

## Problem

```text
This site can't be reached
```

## Verify Service

```bash
sudo systemctl status jenkins
```

Ensure Jenkins is running.

Open:

```text
http://localhost:8080
```

If using a remote server:

```text
http://<server-ip>:8080
```

---

# 4. Port 8080 Already in Use

## Check

Linux:

```bash
sudo lsof -i :8080
```

Windows:

```powershell
netstat -ano | findstr :8080
```

## Solution

Stop the application using port 8080 or configure Jenkins to use another port.

---

# 5. Firewall Blocking Jenkins

## Check Firewall

Ubuntu:

```bash
sudo ufw status
```

Allow Jenkins:

```bash
sudo ufw allow 8080
```

---

# 6. Cannot Retrieve Initial Admin Password

## Problem

```text
No such file or directory
```

## Verify Path

Linux:

```bash
ls /var/lib/jenkins/secrets/
```

Retrieve password:

```bash
sudo cat /var/lib/jenkins/secrets/initialAdminPassword
```

If the file doesn't exist, ensure Jenkins has started successfully.

---

# 7. Jenkins Shows "Unlock Jenkins" Repeatedly

## Possible Causes

- Incorrect password
- Browser cache
- Jenkins restarted before setup completed

## Solution

- Retrieve the password again.
- Refresh the page.
- Clear browser cache.
- Restart Jenkins if necessary.

---

# 8. Permission Denied

## Problem

```text
Permission denied
```

## Cause

Insufficient privileges.

## Solution

Run commands with sudo:

```bash
sudo systemctl start jenkins
```

---

# 9. Jenkins Service Not Found

## Problem

```text
Unit jenkins.service could not be found.
```

## Cause

Jenkins is not installed correctly.

## Solution

Reinstall Jenkins:

```bash
sudo apt update
sudo apt install jenkins -y
```

---

# 10. Plugin Installation Failed

## Possible Causes

- No internet connection
- Firewall or proxy restrictions
- Jenkins update center unavailable

## Solution

- Verify internet connectivity.
- Restart Jenkins.
- Retry plugin installation.

---

# 11. Jenkins Runs but Build Fails Immediately

## Possible Causes

- Git not installed
- Java not configured
- Missing build tools (Maven, Gradle, npm)

## Verify

```bash
git --version
```

```bash
java --version
```

Install any missing dependencies.

---

# 12. Windows Service Not Running

Check the Jenkins service:

```powershell
Get-Service Jenkins
```

Start the service:

```powershell
Start-Service Jenkins
```

Restart the service:

```powershell
Restart-Service Jenkins
```

---

# 13. Docker Container Exits Immediately

View container logs:

```bash
docker logs jenkins
```

Verify the container:

```bash
docker ps -a
```

Restart if necessary:

```bash
docker restart jenkins
```

---

# Useful Verification Commands

Verify Java:

```bash
java --version
```

Check Jenkins status:

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

Retrieve admin password:

```bash
sudo cat /var/lib/jenkins/secrets/initialAdminPassword
```

Check listening port:

Linux:

```bash
sudo lsof -i :8080
```

Windows:

```powershell
netstat -ano | findstr :8080
```

---

# Best Practices

- Install a supported Java LTS version (17 or 21).
- Keep Jenkins updated.
- Install only required plugins.
- Back up the Jenkins home directory regularly.
- Monitor Jenkins logs for errors.
- Secure the Jenkins administrator account.
- Verify firewall and network settings before troubleshooting.

---

# Summary

Most Jenkins installation issues are caused by missing Java, service startup failures, firewall restrictions, or port conflicts. Checking the service status, reviewing logs, and verifying prerequisites will resolve the majority of installation problems.