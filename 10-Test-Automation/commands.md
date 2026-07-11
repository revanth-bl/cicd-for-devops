# Commands

This section contains commonly used commands and Jenkins Pipeline snippets for automating software testing.

---

# Verify Java Installation

```bash
java --version
```

---

# Verify Maven Installation

```bash
mvn --version
```

---

# Verify Gradle Installation

```bash
gradle --version
```

---

# Verify Python Installation

```bash
python --version
```

---

# Verify Pytest Installation

```bash
pytest --version
```

---

# Verify Git Installation

```bash
git --version
```

---

# Clone Repository

```bash
git clone https://github.com/username/project.git
```

---

# Navigate to Project

```bash
cd project
```

---

# Maven Test Commands

Run Unit Tests

```bash
mvn test
```

Run Integration Tests

```bash
mvn verify
```

Run Specific Test

```bash
mvn -Dtest=TestClass test
```

Skip Tests

```bash
mvn package -DskipTests
```

---

# Gradle Test Commands

Run Tests

```bash
gradle test
```

Run Specific Test

```bash
gradle test --tests TestClass
```

Build with Tests

```bash
gradle build
```

---

# Python Test Commands

Run All Tests

```bash
pytest
```

Run Specific Test File

```bash
pytest tests/test_app.py
```

Run with Verbose Output

```bash
pytest -v
```

Generate HTML Report

```bash
pytest --html=report.html
```

---

# JUnit Test Report

```groovy
junit '**/target/surefire-reports/*.xml'
```

---

# Jenkins Pipeline - Maven Tests

```groovy
pipeline {

    agent any

    stages {

        stage('Test') {
            steps {
                sh 'mvn test'
            }
        }

    }

}
```

Windows:

```groovy
pipeline {

    agent any

    stages {

        stage('Test') {
            steps {
                bat 'mvn test'
            }
        }

    }

}
```

---

# Jenkins Pipeline - Gradle Tests

```groovy
pipeline {

    agent any

    stages {

        stage('Test') {
            steps {
                sh 'gradle test'
            }
        }

    }

}
```

---

# Jenkins Pipeline - Pytest

```groovy
pipeline {

    agent any

    stages {

        stage('Test') {
            steps {
                sh 'pytest'
            }
        }

    }

}
```

---

# Publish Test Results

```groovy
junit '**/target/surefire-reports/*.xml'
```

---

# Archive Test Reports

```groovy
archiveArtifacts artifacts: '**/reports/**/*'
```

---

# Retry Failed Tests

```groovy
options {
    retry(2)
}
```

---

# Timeout Test Stage

```groovy
options {
    timeout(time: 15, unit: 'MINUTES')
}
```

---

# Clean Workspace

```groovy
cleanWs()
```

---

# Print Environment Variables

Linux

```groovy
sh 'printenv'
```

Windows

```groovy
bat 'set'
```

---

# Display Current Workspace

Linux

```groovy
sh 'pwd'
```

Windows

```groovy
bat 'cd'
```

---

# Verify Test Reports

Linux

```bash
ls target/surefire-reports
```

Windows

```powershell
dir target\surefire-reports
```

---

# Git Commands

Stage changes

```bash
git add .
```

Commit changes

```bash
git commit -m "Add automated testing"
```

Push changes

```bash
git push origin main
```

View commit history

```bash
git log --oneline
```

---

# Summary

| Command / Directive | Purpose |
|---------------------|---------|
| `mvn test` | Execute Maven unit tests |
| `mvn verify` | Execute integration tests |
| `gradle test` | Execute Gradle tests |
| `pytest` | Run Python tests |
| `junit` | Publish JUnit reports |
| `archiveArtifacts` | Archive test reports |
| `retry()` | Retry failed test stages |
| `timeout()` | Limit test execution time |
| `cleanWs()` | Clean Jenkins workspace |

---

# Notes

- Run automated tests after every successful build.
- Fail the pipeline immediately if critical tests fail.
- Publish JUnit reports for easier debugging.
- Archive test reports for future analysis.
- Keep test execution independent and repeatable.
- Use separate stages for Build and Test.
- Never skip tests in production CI/CD pipelines unless absolutely necessary.