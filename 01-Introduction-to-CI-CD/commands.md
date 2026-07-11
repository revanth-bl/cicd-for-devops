# Commands

This section contains the basic commands and tools used before starting Continuous Integration and Continuous Delivery (CI/CD).

---

## Check Git Installation

```bash
git --version
```

**Description:**
Displays the installed Git version.

**Example Output**

```text
git version 2.50.1.windows.1
```

---

## Check Java Installation

Jenkins requires Java to run.

```bash
java --version
```

or

```bash
java -version
```

**Example Output**

```text
openjdk 21.0.2
```

---

## Check Docker Installation (Optional)

Docker is commonly integrated with CI/CD pipelines.

```bash
docker --version
```

**Example Output**

```text
Docker version 28.x.x
```

---

## Verify Git Configuration

Display the configured Git username.

```bash
git config --global user.name
```

Display the configured Git email.

```bash
git config --global user.email
```

---

## Configure Git (if not already configured)

```bash
git config --global user.name "Your Name"
git config --global user.email "you@example.com"
```

---

## Verify Jenkins Port (Later)

Once Jenkins is installed:

```text
http://localhost:8080
```

---

## Summary

| Command | Purpose |
|----------|---------|
| `git --version` | Verify Git installation |
| `java --version` | Verify Java installation |
| `docker --version` | Verify Docker installation |
| `git config --global user.name` | View Git username |
| `git config --global user.email` | View Git email |

---

## Notes

- Install Git before starting CI/CD.
- Install Java before installing Jenkins.
- Docker will be used in later modules.
- GitHub account is recommended for source code hosting.