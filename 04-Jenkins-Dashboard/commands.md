# Commands

This section contains useful commands related to accessing, managing, and verifying the Jenkins Dashboard.

---

# Open Jenkins Dashboard

Local machine:

```text
http://localhost:8080
```

Remote server:

```text
http://<server-ip>:8080
```

---

# Check Jenkins Service Status

Linux

```bash
sudo systemctl status jenkins
```

Windows

```powershell
Get-Service Jenkins
```

---

# Start Jenkins

Linux

```bash
sudo systemctl start jenkins
```

Windows

```powershell
Start-Service Jenkins
```

---

# Stop Jenkins

Linux

```bash
sudo systemctl stop jenkins
```

Windows

```powershell
Stop-Service Jenkins
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

# View Jenkins Logs

Linux

```bash
sudo journalctl -u jenkins
```

Live Logs

```bash
sudo journalctl -u jenkins -f
```

---

# Check Jenkins Version

Linux

```bash
jenkins --version
```

or

```bash
java -jar jenkins.war --version
```

---

# Check Running Port

Linux

```bash
sudo lsof -i :8080
```

Windows

```powershell
netstat -ano | findstr :8080
```

---

# Check Java Version

```bash
java --version
```

---

# Check Jenkins Process

Linux

```bash
ps -ef | grep jenkins
```

Windows

```powershell
tasklist | findstr java
```

---

# Jenkins CLI (Optional)

Download Jenkins CLI:

```bash
wget http://localhost:8080/jnlpJars/jenkins-cli.jar
```

Check available commands:

```bash
java -jar jenkins-cli.jar -s http://localhost:8080 help
```

List installed plugins:

```bash
java -jar jenkins-cli.jar -s http://localhost:8080 list-plugins
```

List all jobs:

```bash
java -jar jenkins-cli.jar -s http://localhost:8080 list-jobs
```

Get Jenkins version:

```bash
java -jar jenkins-cli.jar -s http://localhost:8080 version
```

---

# Backup Jenkins Home Directory

Linux

```bash
sudo tar -czvf jenkins-backup.tar.gz /var/lib/jenkins
```

Windows (PowerShell)

```powershell
Compress-Archive `
-Path "C:\ProgramData\Jenkins" `
-DestinationPath "C:\jenkins-backup.zip"
```

---

# Useful Verification Commands

Check Java

```bash
java --version
```

Check Jenkins Service

```bash
sudo systemctl status jenkins
```

View Logs

```bash
sudo journalctl -u jenkins -f
```

Check Port

```bash
sudo lsof -i :8080
```

---

# Summary

| Command | Purpose |
|----------|---------|
| `systemctl status jenkins` | Check Jenkins service |
| `systemctl restart jenkins` | Restart Jenkins |
| `journalctl -u jenkins` | View Jenkins logs |
| `lsof -i :8080` | Check Jenkins port |
| `java --version` | Verify Java installation |
| `jenkins-cli.jar help` | View CLI commands |
| `list-plugins` | Show installed plugins |
| `list-jobs` | Show Jenkins jobs |
| `version` | Display Jenkins version |

---

# Notes

- The Jenkins Dashboard is primarily managed through the web interface.
- Administrative actions such as plugin management, user management, and global configuration are performed from **Manage Jenkins**.
- The Jenkins CLI is optional but useful for automation and scripting.
- Always verify that the Jenkins service is running before accessing the dashboard.