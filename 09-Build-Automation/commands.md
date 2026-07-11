# Commands

This section contains commonly used commands and Jenkins Pipeline snippets for automating software builds.

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

# Check Repository Status

```bash
git status
```

---

# Pull Latest Changes

```bash
git pull origin main
```

---

# Maven Commands

Clean Project

```bash
mvn clean
```

Compile Project

```bash
mvn compile
```

Run Tests

```bash
mvn test
```

Package Application

```bash
mvn package
```

Install Artifact

```bash
mvn install
```

Clean and Package

```bash
mvn clean package
```

Skip Tests

```bash
mvn clean package -DskipTests
```

---

# Gradle Commands

Clean Project

```bash
gradle clean
```

Build Project

```bash
gradle build
```

Run Tests

```bash
gradle test
```

Create JAR

```bash
gradle jar
```

---

# Jenkins Pipeline - Maven Build

```groovy
pipeline {

    agent any

    stages {

        stage('Build') {
            steps {
                sh 'mvn clean package'
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

        stage('Build') {
            steps {
                bat 'mvn clean package'
            }
        }

    }

}
```

---

# Jenkins Pipeline - Gradle Build

```groovy
pipeline {

    agent any

    stages {

        stage('Build') {
            steps {
                sh 'gradle build'
            }
        }

    }

}
```

---

# Archive Build Artifacts

```groovy
archiveArtifacts artifacts: '**/target/*.jar'
```

Archive ZIP Files

```groovy
archiveArtifacts artifacts: '**/*.zip'
```

Archive WAR Files

```groovy
archiveArtifacts artifacts: '**/*.war'
```

---

# Publish JUnit Test Results

```groovy
junit '**/target/surefire-reports/*.xml'
```

---

# Clean Workspace

```groovy
cleanWs()
```

---

# Retry Failed Builds

```groovy
options {
    retry(3)
}
```

---

# Timeout Build

```groovy
options {
    timeout(time: 20, unit: 'MINUTES')
}
```

---

# Build Environment Variables

```groovy
environment {

    APP_NAME = "DemoApp"
    BUILD_ENV = "Production"

}
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

# Display Workspace

Linux

```groovy
sh 'pwd'
```

Windows

```groovy
bat 'cd'
```

---

# Verify Build Artifact

Linux

```bash
ls target/
```

Windows

```powershell
dir target
```

---

# Jenkins Console Message

```groovy
echo 'Build completed successfully.'
```

---

# Useful Git Commands

Commit changes:

```bash
git add .
git commit -m "Configure build automation"
git push origin main
```

View commit history:

```bash
git log --oneline
```

---

# Summary

| Command / Directive | Purpose |
|---------------------|---------|
| `mvn clean` | Remove previous build files |
| `mvn compile` | Compile source code |
| `mvn test` | Execute unit tests |
| `mvn package` | Package the application |
| `mvn install` | Install artifact locally |
| `gradle build` | Build Gradle project |
| `archiveArtifacts` | Save build artifacts |
| `junit` | Publish test reports |
| `cleanWs()` | Clean Jenkins workspace |
| `retry()` | Retry failed builds |
| `timeout()` | Stop long-running builds |

---

# Notes

- Always run a clean build before packaging an application.
- Archive important build artifacts for later use or deployment.
- Publish test reports to quickly identify test failures.
- Keep build stages focused on a single responsibility.
- Avoid skipping tests in production pipelines unless absolutely necessary.
- Use `sh` for Linux agents and `bat` for Windows agents.