# Troubleshooting

This guide covers common issues encountered while creating and running a Jenkins Freestyle Project.

---

# 1. Build Failed

## Problem

```text
Finished: FAILURE
```

## Possible Causes

- Incorrect build command
- Missing files
- Invalid script syntax
- Missing dependencies

## Solution

Open:

```text
Build History → Console Output
```

Review the error message and correct the failed command or script.

---

# 2. Build Step Not Executed

## Possible Causes

- No build step configured
- Wrong build step type selected

## Solution

Open the job configuration:

```text
Configure → Build
```

Verify that:

- **Execute Shell** is selected for Linux/macOS.
- **Execute Windows Batch Command** is selected for Windows.

Save the configuration and run the job again.

---

# 3. Console Output Shows Command Not Found

## Example

```text
command not found
```

## Possible Causes

- Command is not installed.
- Incorrect command name.
- PATH environment variable is missing the executable.

## Solution

Verify the command manually.

Example:

```bash
git --version
```

```bash
java --version
```

Install the missing software if required.

---

# 4. Git Repository Cannot Be Cloned

## Problem

```text
Repository not found
```

or

```text
Authentication failed
```

## Possible Causes

- Incorrect repository URL
- Private repository without credentials
- Network connectivity issues

## Solution

- Verify the repository URL.
- Configure Git credentials in **Manage Jenkins → Credentials**.
- Test network connectivity.

---

# 5. Workspace Not Created

## Possible Causes

- Build never started
- Permission issues
- Jenkins service stopped

## Solution

Verify Jenkins is running:

```bash
sudo systemctl status jenkins
```

Run the build again and check whether the workspace is created.

---

# 6. Job Stuck in Build Queue

## Possible Causes

- No available executors
- Offline agent
- Busy Jenkins controller

## Solution

Navigate to:

```text
Manage Jenkins → Nodes
```

Ensure an executor is available and any required agents are online.

---

# 7. Permission Denied

## Example

```text
Permission denied
```

## Possible Causes

- Script lacks execute permission.
- Jenkins user cannot access the file.

## Solution

Grant execute permission (Linux):

```bash
chmod +x script.sh
```

Ensure the Jenkins user has permission to access the required files.

---

# 8. Job Cannot Access Files

## Possible Causes

- Incorrect file path
- File does not exist
- Insufficient permissions

## Solution

Verify the file location:

```bash
pwd
```

```bash
ls -la
```

Correct the file path or permissions as needed.

---

# 9. Environment Variables Not Available

## Problem

Commands relying on environment variables fail.

## Solution

Print all environment variables:

Linux:

```bash
printenv
```

Windows:

```cmd
set
```

Verify the required variable is defined.

---

# 10. Console Output Is Empty

## Possible Causes

- Build terminated immediately.
- Build step missing.
- Jenkins service stopped.

## Solution

Verify:

- Build steps are configured.
- Jenkins service is running.
- The job executed successfully.

---

# 11. Build Never Starts

## Possible Causes

- Jenkins service stopped
- Build waiting in queue
- Executor unavailable

## Solution

Restart Jenkins:

Linux:

```bash
sudo systemctl restart jenkins
```

Windows:

```powershell
Restart-Service Jenkins
```

---

# 12. Job Deleted Accidentally

## Solution

If backups exist, restore the job configuration from the Jenkins home directory.

Linux:

```text
/var/lib/jenkins/jobs/
```

Windows:

```text
C:\ProgramData\Jenkins\.jenkins\jobs\
```

If no backup exists, recreate the job.

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

Check Git:

```bash
git --version
```

Check Java:

```bash
java --version
```

Current directory:

```bash
pwd
```

List files:

```bash
ls -la
```

View Jenkins logs:

```bash
sudo journalctl -u jenkins -f
```

---

# Best Practices

- Test build commands in a terminal before adding them to Jenkins.
- Use meaningful job names and descriptions.
- Keep build scripts small and modular.
- Store source code in Git.
- Review **Console Output** after every build.
- Back up Jenkins jobs regularly.
- Use credentials instead of hardcoding usernames or passwords.

---

# Summary

Most Freestyle Project issues are caused by incorrect build commands, missing dependencies, permission problems, or misconfigured jobs. The **Console Output** is the first place to investigate build failures, followed by verifying Jenkins service status, workspace contents, and job configuration.