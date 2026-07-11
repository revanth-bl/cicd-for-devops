# Commands

This section contains commonly used commands and configuration snippets for integrating GitHub Webhooks with Jenkins.

---

# Verify Git Installation

```bash
git --version
```

---

# Verify Jenkins Service

Linux

```bash
sudo systemctl status jenkins
```

Windows

```powershell
Get-Service Jenkins
```

---

# Restart Jenkins

Linux

```bash
sudo systemctl restart jenkins
```

Windows

```powershell
Restart-Service Jenkins
```

---

# Check Jenkins Logs

Linux

```bash
sudo journalctl -u jenkins -f
```

---

# Check Current Git Remote

```bash
git remote -v
```

---

# Add Remote Repository

```bash
git remote add origin https://github.com/username/repository.git
```

---

# Clone Repository

```bash
git clone https://github.com/username/repository.git
```

---

# Check Repository Status

```bash
git status
```

---

# Add Files

```bash
git add .
```

---

# Commit Changes

```bash
git commit -m "Configure GitHub Webhooks"
```

---

# Push Changes

```bash
git push origin main
```

---

# Pull Latest Changes

```bash
git pull origin main
```

---

# Verify Current Branch

```bash
git branch
```

---

# Display Commit History

```bash
git log --oneline
```

---

# Jenkins Webhook Endpoint

```text
http://<jenkins-server>:8080/github-webhook/
```

Example:

```text
http://192.168.1.10:8080/github-webhook/
```

---

# Localhost Using Ngrok

Start an HTTP tunnel:

```bash
ngrok http 8080
```

Example URL:

```text
https://abcd1234.ngrok-free.app/github-webhook/
```

---

# Jenkins Build Trigger

Enable:

```text
GitHub hook trigger for GITScm polling
```

---

# GitHub Webhook Events

Recommended event:

```text
Just the push event
```

Optional:

```text
Pull requests
```

```text
Branch or tag creation
```

---

# Test Webhook

GitHub

```
Repository
    ↓
Settings
    ↓
Webhooks
    ↓
Recent Deliveries
    ↓
Redeliver
```

---

# Verify Webhook Delivery

Successful response:

```text
HTTP 200
```

---

# Common Git Commands

Clone repository:

```bash
git clone <repository-url>
```

Repository status:

```bash
git status
```

Commit:

```bash
git commit -m "message"
```

Push:

```bash
git push origin main
```

Pull:

```bash
git pull origin main
```

---

# Verify Jenkins Port

Linux

```bash
sudo lsof -i :8080
```

Windows

```powershell
netstat -ano | findstr :8080
```

---

# Check Network Connectivity

Linux

```bash
ping github.com
```

Windows

```powershell
ping github.com
```

---

# Verify Java Installation

```bash
java --version
```

---

# Useful Jenkins URL

Dashboard

```text
http://localhost:8080
```

Webhook Endpoint

```text
http://localhost:8080/github-webhook/
```

---

# Summary

| Command / Setting | Purpose |
|-------------------|---------|
| `git status` | Check repository status |
| `git add .` | Stage changes |
| `git commit` | Commit changes |
| `git push` | Push changes to GitHub |
| `git remote -v` | View configured remotes |
| `git log --oneline` | View commit history |
| `systemctl status jenkins` | Check Jenkins service |
| `systemctl restart jenkins` | Restart Jenkins |
| `journalctl -u jenkins -f` | View Jenkins logs |
| `ngrok http 8080` | Expose local Jenkins server |
| `/github-webhook/` | GitHub webhook endpoint |
| `HTTP 200` | Successful webhook delivery |

---

# Notes

- Configure the webhook in **GitHub → Repository → Settings → Webhooks**.
- Use the endpoint **`/github-webhook/`** when integrating GitHub with Jenkins.
- Enable **GitHub hook trigger for GITScm polling** in the Jenkins job configuration.
- If Jenkins is running locally, use a tunneling service such as **ngrok** to expose it to GitHub.
- After every `git push`, GitHub sends an HTTP POST request to Jenkins, which automatically starts the configured pipeline or job.