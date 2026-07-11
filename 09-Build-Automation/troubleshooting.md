# Troubleshooting

This guide covers common issues encountered during automated builds using Jenkins, Maven, and Gradle.

---

# 1. Build Failed

## Problem

```text
Finished: FAILURE
```

## Possible Causes

- Compilation errors
- Test failures
- Missing dependencies
- Incorrect build configuration

## Solution

Review the Jenkins **Console Output** to identify the exact error. Fix the issue in the source code or build configuration, then rebuild.

---

# 2. Maven Command Not Found

## Problem

```text
mvn: command not found
```

## Cause

Maven is not installed or its executable is not included in the system PATH.

## Solution

Verify Maven installation:

```bash
mvn --version
```

Install Maven if necessary and configure the PATH environment variable.

---

# 3. Gradle Command Not Found

## Problem

```text
gradle: command not found
```

## Cause

Gradle is not installed or not added to the PATH.

## Solution

Verify Gradle installation:

```bash
gradle --version
```

Install Gradle and ensure it is accessible from the command line.

---

# 4. Java Not Installed

## Problem

```text
java: command not found
```

or

```text
'java' is not recognized
```

## Solution

Verify Java installation:

```bash
java --version
```

Install a supported JDK and configure the JAVA_HOME environment variable.

---

# 5. Dependency Resolution Failed

## Problem

```text
Could not resolve dependencies
```

## Possible Causes

- No internet connection
- Repository unavailable
- Incorrect dependency version

## Solution

- Check network connectivity.
- Verify dependency versions.
- Ensure Maven Central or other repositories are accessible.

---

# 6. Compilation Errors

## Problem

```text
Compilation failure
```

## Cause

Source code contains syntax or compilation errors.

## Solution

Review compiler messages, correct the source code, and rebuild the project.

---

# 7. Unit Tests Failed

## Problem

```text
Tests Failed
```

## Solution

Open the Jenkins **Test Results** or **Console Output** to identify failing test cases. Fix the tests or application code before rebuilding.

---

# 8. Artifact Not Generated

## Problem

Expected JAR, WAR, or ZIP file is missing.

## Possible Causes

- Build failed
- Incorrect output directory
- Packaging phase not executed

## Solution

Verify the packaging step:

```bash
mvn package
```

or

```bash
gradle build
```

---

# 9. Artifact Archiving Failed

## Problem

```text
No artifacts found
```

## Cause

Incorrect artifact path in the Jenkins pipeline.

## Solution

Verify the archive pattern.

Example:

```groovy
archiveArtifacts artifacts: '**/target/*.jar'
```

Ensure the generated artifact exists in the specified directory.

---

# 10. Workspace Contains Old Files

## Problem

Previous build files affect the current build.

## Solution

Clean the workspace before building.

Pipeline:

```groovy
cleanWs()
```

Maven:

```bash
mvn clean
```

Gradle:

```bash
gradle clean
```

---

# 11. Jenkins Agent Offline

## Problem

```text
No agent available
```

## Solution

Navigate to:

```text
Manage Jenkins
    ↓
Nodes
```

Verify that:

- Agent is online
- Agent labels are correct
- Executors are available

---

# 12. Build Timeout

## Problem

The build never finishes.

## Solution

Configure a timeout in the pipeline.

```groovy
options {
    timeout(time: 20, unit: 'MINUTES')
}
```

Investigate long-running tasks or infinite loops.

---

# 13. Environment Variable Missing

## Problem

```text
No such property
```

## Cause

The required environment variable is not defined.

## Solution

Declare variables inside the `environment` block.

```groovy
environment {
    APP_NAME = "DemoApp"
}
```

---

# 14. Git Checkout Failed

## Problem

```text
ERROR: Couldn't find any revision to build
```

## Solution

Verify:

- Repository URL
- Branch name
- Jenkins credentials
- Repository permissions

Test manually:

```bash
git clone <repository-url>
```

---

# Useful Verification Commands

Verify Java:

```bash
java --version
```

Verify Maven:

```bash
mvn --version
```

Verify Gradle:

```bash
gradle --version
```

Verify Git:

```bash
git --version
```

Check repository status:

```bash
git status
```

View commit history:

```bash
git log --oneline
```

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

---

# Best Practices

- Perform a clean build before packaging.
- Keep Java, Maven, and Gradle updated.
- Archive important build artifacts.
- Run automated tests with every build.
- Monitor Jenkins Console Output after each build.
- Store dependencies in trusted repositories.
- Keep build scripts under version control.
- Use consistent build environments across development and production.

---

# Summary

Most Build Automation issues are caused by missing dependencies, incorrect tool installations, compilation errors, failed tests, invalid artifact paths, or environment configuration problems. Reviewing **Jenkins Console Output**, **build logs**, and verifying Java, Maven, Gradle, and Git installations will resolve the majority of build-related issues.