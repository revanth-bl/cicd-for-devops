# Troubleshooting

This guide covers common issues encountered while creating and running Jenkins Pipelines.

---

# 1. Pipeline Failed

## Problem

```text
Finished: FAILURE
```

## Possible Causes

- Invalid Jenkinsfile syntax
- Build command failed
- Missing dependencies
- Incorrect pipeline configuration

## Solution

Open:

```text
Build History → Console Output
```

Review the error message, correct the issue, and rerun the pipeline.

---

# 2. Jenkinsfile Not Found

## Problem

```text
Jenkinsfile not found
```

## Possible Causes

- Jenkinsfile is missing.
- Incorrect file name.
- Jenkinsfile is not in the repository root.

## Solution

Verify:

```text
Repository
│
├── src/
├── README.md
└── Jenkinsfile
```

The filename must be exactly:

```text
Jenkinsfile
```

---

# 3. Pipeline Syntax Error

## Example

```text
WorkflowScript: Expected a stage
```

or

```text
Missing }
```

## Cause

Invalid Groovy or Declarative Pipeline syntax.

## Solution

- Check matching braces `{}`.
- Verify stage and steps blocks.
- Use the **Pipeline Syntax** tool in Jenkins.

---

# 4. Git Checkout Failed

## Problem

```text
ERROR: Couldn't find any revision to build.
```

## Possible Causes

- Incorrect repository URL.
- Wrong branch name.
- Authentication failure.

## Solution

Verify:

```bash
git clone <repository-url>
```

Check that:

- Repository URL is correct.
- Branch exists.
- Jenkins credentials are configured.

---

# 5. Shell Step Failed

## Problem

```text
sh: command not found
```

## Cause

The pipeline is running on Windows.

## Solution

Linux:

```groovy
sh 'pwd'
```

Windows:

```groovy
bat 'dir'
```

Use the appropriate command for your build agent.

---

# 6. Batch Step Failed

## Problem

```text
bat is not recognized
```

## Cause

The pipeline is running on Linux.

## Solution

Use:

```groovy
sh 'ls -la'
```

instead of:

```groovy
bat 'dir'
```

---

# 7. Stage Skipped

## Possible Causes

- Previous stage failed.
- Conditional `when` block evaluated to false.

## Solution

Review:

```text
Console Output
```

Identify why the stage was skipped and correct the pipeline logic.

---

# 8. Build Stuck in Queue

## Possible Causes

- No available executors.
- Jenkins agent offline.
- Busy controller.

## Solution

Navigate to:

```text
Manage Jenkins → Nodes
```

Verify:

- Agent is online.
- Executors are available.

---

# 9. Pipeline Cannot Access Credentials

## Problem

```text
Credentials not found
```

## Solution

Navigate to:

```text
Manage Jenkins → Credentials
```

Verify:

- Credential exists.
- Correct Credential ID is used.
- Proper scope is selected.

---

# 10. Workspace Issues

## Problem

Files are missing during the build.

## Solution

Clean the workspace before running the pipeline:

```groovy
cleanWs()
```

Or manually delete the workspace from the Jenkins job.

---

# 11. Pipeline Never Starts

## Possible Causes

- Jenkins service stopped.
- Invalid pipeline configuration.
- Build waiting in queue.

## Solution

Restart Jenkins:

Linux

```bash
sudo systemctl restart jenkins
```

Windows

```powershell
Restart-Service Jenkins
```

---

# 12. Console Output Missing

## Possible Causes

- Pipeline terminated immediately.
- Jenkins service failed.
- Incorrect job configuration.

## Solution

Review Jenkins logs:

```bash
sudo journalctl -u jenkins -f
```

Verify the pipeline configuration and rerun the build.

---

# 13. Agent Offline

## Problem

Pipeline cannot execute because the assigned agent is unavailable.

## Solution

Navigate to:

```text
Manage Jenkins → Nodes
```

Ensure:

- Agent is online.
- Java is installed on the agent.
- Network connectivity is working.

---

# 14. Pipeline Hangs Indefinitely

## Possible Causes

- Waiting for manual input.
- Infinite loop in the pipeline.
- External command never finishes.

## Solution

- Check the **Console Output**.
- Verify whether an `input` step is awaiting approval.
- Terminate the build if necessary and fix the pipeline logic.

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

Verify Git:

```bash
git --version
```

Verify Java:

```bash
java --version
```

Check repository status:

```bash
git status
```

---

# Best Practices

- Store the `Jenkinsfile` in the repository root.
- Validate pipeline syntax before committing.
- Use Declarative Pipelines unless advanced scripting is required.
- Keep stages focused on a single responsibility.
- Use Jenkins Credentials instead of hardcoding secrets.
- Review **Console Output** after every build.
- Test pipeline changes in a development environment first.
- Keep Jenkins and plugins updated.

---

# Summary

Most Jenkins Pipeline issues are caused by syntax errors, incorrect `Jenkinsfile` placement, Git configuration problems, agent availability, or platform-specific command mismatches. The **Console Output** and Jenkins logs are the primary tools for diagnosing and resolving pipeline failures.