# Troubleshooting

This guide covers common issues you may encounter while accessing or managing the Jenkins Dashboard.

---

# 1. Unable to Access Jenkins Dashboard

## Problem

```text
This site can't be reached
```

or

```text
ERR_CONNECTION_REFUSED
```

## Possible Causes

- Jenkins service is not running.
- Incorrect URL or port.
- Firewall is blocking the connection.

## Solution

Check Jenkins status:

```bash
sudo systemctl status jenkins
```

Windows:

```powershell
Get-Service Jenkins
```

Verify Jenkins is accessible at:

```text
http://localhost:8080
```

---

# 2. Jenkins Service Is Not Running

## Problem

```text
inactive (dead)
```

## Solution

Start Jenkins:

```bash
sudo systemctl start jenkins
```

Enable Jenkins on boot:

```bash
sudo systemctl enable jenkins
```

Verify:

```bash
sudo systemctl status jenkins
```

---

# 3. Login Failed

## Problem

```text
Invalid username or password
```

## Possible Causes

- Incorrect credentials.
- Wrong administrator account.
- Password changed.

## Solution

- Verify the username and password.
- Reset credentials if necessary.
- Ensure you are using the correct authentication method.

---

# 4. Dashboard Loads Slowly

## Possible Causes

- Low RAM
- High CPU usage
- Too many installed plugins
- Large number of jobs

## Solution

Restart Jenkins:

```bash
sudo systemctl restart jenkins
```

Review system resources and uninstall unnecessary plugins.

---

# 5. Build Queue Is Stuck

## Problem

Jobs remain in the queue but never start.

## Possible Causes

- No available executors
- Busy controller
- Offline agent

## Solution

Navigate to:

```text
Manage Jenkins → Nodes
```

Ensure an executor is available and all required agents are online.

---

# 6. No Executors Available

## Problem

Jobs remain queued indefinitely.

## Solution

Go to:

```text
Manage Jenkins → Nodes
```

Increase the number of executors if appropriate.

---

# 7. Plugin Installation Failed

## Problem

Plugins fail to install.

## Possible Causes

- No internet connection
- Firewall or proxy restrictions
- Update Center unavailable

## Solution

- Verify internet connectivity.
- Restart Jenkins.
- Retry plugin installation.
- Check proxy configuration if using one.

---

# 8. Credentials Not Found

## Problem

Jobs fail because credentials cannot be located.

## Solution

Navigate to:

```text
Manage Jenkins → Credentials
```

Verify:

- Credential exists.
- Correct credential type is selected.
- Correct Credential ID is referenced.

---

# 9. Build History Missing

## Possible Causes

- No builds have been executed.
- Build history was deleted.
- Incorrect job selected.

## Solution

Run the job once and verify that Build History is enabled.

---

# 10. Console Output Is Empty

## Possible Causes

- Build failed before execution.
- Job configuration is incomplete.
- Jenkins service stopped unexpectedly.

## Solution

Review Jenkins logs:

```bash
sudo journalctl -u jenkins -f
```

Then verify the job configuration.

---

# 11. Dashboard Shows "No Jobs"

## Cause

No jobs have been created.

## Solution

Click:

```text
New Item
```

Create a Freestyle Project or Pipeline.

---

# 12. Port 8080 Already in Use

## Linux

```bash
sudo lsof -i :8080
```

## Windows

```powershell
netstat -ano | findstr :8080
```

## Solution

Stop the conflicting application or configure Jenkins to use another port.

---

# 13. Browser Displays Old Dashboard

## Cause

Cached browser data.

## Solution

- Refresh the page.
- Clear browser cache.
- Try Incognito/Private Mode.

---

# 14. Agent Offline

## Problem

Jobs cannot execute on a build agent.

## Solution

Navigate to:

```text
Manage Jenkins → Nodes
```

Verify:

- Agent is connected.
- Network connectivity is available.
- Java is installed on the agent.

---

# Useful Verification Commands

Check Jenkins service:

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

Check Java:

```bash
java --version
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

- Keep Jenkins updated.
- Install only required plugins.
- Remove unused plugins.
- Monitor Build Queue regularly.
- Organize jobs into folders.
- Back up Jenkins configuration.
- Use the Jenkins Credentials Store for secrets.
- Review system logs when troubleshooting.

---

# Summary

Most Jenkins Dashboard issues are caused by service failures, authentication problems, plugin issues, or unavailable executors. Checking the Jenkins service status, reviewing logs, and verifying system configuration will resolve the majority of dashboard-related problems.