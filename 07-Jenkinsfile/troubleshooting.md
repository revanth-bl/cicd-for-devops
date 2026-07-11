# Troubleshooting

This guide covers common issues encountered while writing and executing Jenkinsfiles.

---

# 1. Jenkinsfile Not Found

## Problem

```text
Jenkinsfile not found
```

## Possible Causes

- Jenkinsfile is missing.
- Incorrect filename.
- File is not located in the repository root.

## Solution

Verify the project structure:

```text
project/
│
├── src/
├── README.md
└── Jenkinsfile
```

Ensure the filename is exactly:

```text
Jenkinsfile
```

---

# 2. Pipeline Syntax Error

## Problem

```text
WorkflowScript: Expected a stage
```

or

```text
Missing }
```

## Possible Causes

- Missing braces (`{}`).
- Incorrect Declarative Pipeline syntax.
- Typographical errors.

## Solution

- Check matching braces.
- Verify all `stage`, `steps`, and `post` blocks.
- Use Jenkins **Pipeline Syntax** or **Replay** feature to validate the script.

---

# 3. No Stages Defined

## Problem

```text
No stages specified
```

## Cause

The `stages` block is missing or empty.

## Solution

Ensure your pipeline includes at least one stage:

```groovy
stages {
    stage('Build') {
        steps {
            echo 'Building...'
        }
    }
}
```

---

# 4. Environment Variable Not Found

## Problem

```text
No such property
```

## Possible Causes

- Variable not declared.
- Incorrect variable name.
- Wrong syntax.

## Solution

Declare variables inside the `environment` block.

Example:

```groovy
environment {
    APP_NAME = "DemoApp"
}
```

Access it correctly:

```groovy
echo "${APP_NAME}"
```

---

# 5. Unknown Stage Section

## Problem

```text
Unknown stage section
```

## Cause

A directive is placed in the wrong location.

## Solution

Verify the pipeline structure:

```groovy
pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                echo 'Build'
            }
        }
    }
}
```

---

# 6. Shell Command Failed

## Problem

```text
sh: command not found
```

## Cause

The pipeline is running on a Windows agent.

## Solution

Use:

Linux

```groovy
sh 'pwd'
```

Windows

```groovy
bat 'dir'
```

---

# 7. Batch Command Failed

## Problem

```text
'bat' is not recognized
```

## Cause

The pipeline is running on a Linux agent.

## Solution

Replace:

```groovy
bat 'dir'
```

with:

```groovy
sh 'ls -la'
```

---

# 8. Agent Not Available

## Problem

```text
No agent available
```

## Possible Causes

- No online build agent.
- Incorrect agent label.
- Controller has no executors.

## Solution

Navigate to:

```text
Manage Jenkins → Nodes
```

Verify:

- Agent is online.
- Label matches the Jenkinsfile.
- Executors are available.

---

# 9. Git Checkout Failed

## Problem

```text
ERROR: Couldn't find any revision to build
```

## Possible Causes

- Wrong repository URL.
- Incorrect branch.
- Missing credentials.

## Solution

Verify:

- Repository URL
- Branch name
- Jenkins credentials

Test manually:

```bash
git clone <repository-url>
```

---

# 10. Pipeline Stops Unexpectedly

## Possible Causes

- Failed stage.
- Unhandled exception.
- Timeout reached.

## Solution

Review:

```text
Console Output
```

Identify the failing stage and correct the error before rerunning the pipeline.

---

# 11. Post Section Not Executed

## Possible Causes

- Invalid `post` block placement.
- Syntax errors in the `post` section.

## Solution

Ensure the `post` block is outside the `stages` block.

Example:

```groovy
post {
    always {
        cleanWs()
    }
}
```

---

# 12. Build Queue Never Starts

## Possible Causes

- No available executors.
- Offline agent.
- Busy Jenkins controller.

## Solution

Navigate to:

```text
Manage Jenkins → Nodes
```

Verify executor availability and agent status.

---

# 13. Credentials Not Found

## Problem

```text
Credentials not found
```

## Solution

Go to:

```text
Manage Jenkins → Credentials
```

Verify:

- Credential exists.
- Correct Credential ID is used.
- Proper scope is selected.

---

# 14. Pipeline Validation Failed

## Problem

```text
Compilation failed
```

## Possible Causes

- Invalid Groovy syntax.
- Unsupported directive.
- Missing required blocks.

## Solution

- Validate the Jenkinsfile using Jenkins Pipeline Syntax.
- Review the error line number.
- Correct the syntax before committing.

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

Check Git:

```bash
git --version
```

Check Java:

```bash
java --version
```

Check repository status:

```bash
git status
```

---

# Best Practices

- Store the Jenkinsfile in the repository root.
- Validate syntax before pushing changes.
- Use Declarative Pipelines for most projects.
- Keep stages focused on a single task.
- Store secrets in Jenkins Credentials.
- Test pipeline changes in a development environment.
- Review Console Output after every build.
- Keep the Jenkinsfile clean, modular, and well-documented.

---

# Summary

Most Jenkinsfile issues result from syntax errors, incorrect pipeline structure, misplaced directives, missing credentials, or agent configuration problems. Use **Console Output**, **Pipeline Syntax validation**, and Jenkins logs to identify and resolve issues quickly.s