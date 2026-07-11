# Troubleshooting

This guide covers common issues encountered while running automated tests in Jenkins pipelines using Maven, Gradle, and PyTest.

---

# 1. Tests Failed

## Problem

```text
Finished: FAILURE
```

or

```text
Tests Failed
```

## Possible Causes

- Assertion failures
- Application bugs
- Incorrect test data
- Environment issues

## Solution

- Review the Jenkins **Console Output**.
- Open the published test report.
- Fix the failing test or application code.
- Re-run the pipeline.

---

# 2. JUnit Report Not Found

## Problem

```text
No test report files were found.
```

## Cause

Incorrect report path or tests did not generate XML reports.

## Solution

Verify the report location.

Example:

```groovy
junit '**/target/surefire-reports/*.xml'
```

Ensure the XML report files exist.

---

# 3. Maven Test Command Failed

## Problem

```text
mvn test
```

returns an error.

## Possible Causes

- Compilation failure
- Missing dependencies
- Incorrect project configuration

## Solution

Verify Maven installation:

```bash
mvn --version
```

Run:

```bash
mvn clean test
```

Review the build output for details.

---

# 4. Gradle Test Failed

## Problem

```text
gradle test
```

fails.

## Solution

Verify Gradle installation:

```bash
gradle --version
```

Run:

```bash
gradle clean test
```

Review the Gradle logs to identify the root cause.

---

# 5. PyTest Not Found

## Problem

```text
pytest: command not found
```

or

```text
No module named pytest
```

## Solution

Verify installation:

```bash
pytest --version
```

Install PyTest if necessary:

```bash
pip install pytest
```

---

# 6. Java Not Installed

## Problem

```text
java: command not found
```

or

```text
'java' is not recognized
```

## Solution

Verify Java:

```bash
java --version
```

Install a supported JDK and configure the `JAVA_HOME` environment variable.

---

# 7. Jenkins Pipeline Stops During Test Stage

## Problem

Pipeline fails during the Test stage.

## Possible Causes

- Test failure
- Incorrect pipeline syntax
- Missing dependencies

## Solution

Check:

- Jenkins Console Output
- Pipeline syntax
- Build logs
- Test framework configuration

---

# 8. Test Reports Not Published

## Problem

Jenkins finishes successfully but no test reports appear.

## Solution

Verify:

- XML reports are generated.
- The `junit` step points to the correct location.
- Test execution completed successfully.

Example:

```groovy
junit '**/target/surefire-reports/*.xml'
```

---

# 9. Build Passes but Tests Are Skipped

## Problem

Pipeline succeeds without executing tests.

## Possible Causes

```bash
-DskipTests
```

or

```bash
-x test
```

was used.

## Solution

Remove options that skip tests.

Run:

```bash
mvn test
```

or

```bash
gradle test
```

---

# 10. Workspace Contains Old Test Results

## Problem

Previous reports appear in the latest build.

## Solution

Clean the workspace before each build.

```groovy
cleanWs()
```

or

```bash
mvn clean
```

---

# 11. Test Execution Timeout

## Problem

Tests continue running indefinitely.

## Solution

Set a timeout in the Jenkins pipeline.

```groovy
options {
    timeout(time: 15, unit: 'MINUTES')
}
```

Investigate long-running or hanging test cases.

---

# 12. Jenkins Agent Offline

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

Verify:

- Agent is online
- Labels match
- Executors are available

---

# 13. Dependency Download Failed

## Problem

```text
Could not resolve dependencies
```

## Solution

Verify:

- Internet connectivity
- Repository availability
- Dependency versions
- Maven or Gradle configuration

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

Verify Python:

```bash
python --version
```

Verify PyTest:

```bash
pytest --version
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

- Execute automated tests after every successful build.
- Publish JUnit reports for each pipeline run.
- Keep test environments consistent.
- Avoid skipping tests in production pipelines.
- Clean the workspace before builds.
- Monitor Jenkins Console Output for failures.
- Maintain test scripts under version control.
- Keep dependencies updated.

---

# Summary

Most Test Automation issues are caused by failing test cases, missing dependencies, incorrect report paths, environment configuration problems, or tool installation issues. Reviewing **Jenkins Console Output**, **JUnit reports**, and verifying Java, Maven, Gradle, PyTest, and Jenkins configurations will resolve the majority of test execution problems.