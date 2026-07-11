# Troubleshooting

This guide covers common issues encountered while configuring GitHub Webhooks with Jenkins.

---

# 1. Webhook Not Triggering Jenkins

## Problem

Pushing code to GitHub does not start a Jenkins build.

## Possible Causes

- Incorrect Payload URL
- Build trigger not enabled
- Jenkins server is offline
- Firewall blocking requests

## Solution

Verify:

- Jenkins is running.
- Payload URL is correct.
- **GitHub hook trigger for GITScm polling** is enabled.
- Jenkins is accessible from GitHub.

---

# 2. HTTP 404 Not Found

## Problem

```text
404 Not Found
```

## Cause

Incorrect webhook endpoint.

## Solution

Verify the Payload URL:

```text
http://your-server:8080/github-webhook/
```

Ensure the URL ends with:

```text
/github-webhook/
```

---

# 3. HTTP 403 Forbidden

## Problem

```text
403 Forbidden
```

## Possible Causes

- Authentication issue
- CSRF protection
- Security configuration

## Solution

- Verify Jenkins security settings.
- Ensure the GitHub plugin is properly configured.
- Check Jenkins logs for additional details.

---

# 4. HTTP 500 Internal Server Error

## Problem

```text
500 Internal Server Error
```

## Possible Causes

- Jenkins plugin failure
- Server configuration error
- Internal pipeline error

## Solution

Review Jenkins logs:

```bash
sudo journalctl -u jenkins -f
```

Restart Jenkins if necessary.

---

# 5. Payload URL Invalid

## Problem

GitHub cannot reach Jenkins.

## Cause

Incorrect URL or Jenkins is running only on localhost.

## Solution

Example:

```text
Wrong:
http://localhost:8080/github-webhook/

Correct:
https://your-public-domain/github-webhook/
```

For local testing, expose Jenkins using a secure tunneling service such as **ngrok**.

---

# 6. Jenkins Build Trigger Disabled

## Problem

Webhook delivery succeeds, but Jenkins does not start a build.

## Solution

Open:

```text
Job
    ↓
Configure
    ↓
Build Triggers
```

Enable:

```text
GitHub hook trigger for GITScm polling
```

Save the configuration.

---

# 7. Repository Authentication Failed

## Problem

```text
Authentication failed
```

## Possible Causes

- Invalid GitHub credentials
- Expired Personal Access Token
- Incorrect repository permissions

## Solution

- Update credentials in Jenkins.
- Verify repository access.
- Test cloning the repository manually.

---

# 8. Jenkins Cannot Clone Repository

## Problem

```text
Repository not found
```

## Solution

Verify:

```bash
git clone https://github.com/username/repository.git
```

Check:

- Repository URL
- Branch name
- Repository visibility
- Jenkins credentials

---

# 9. Webhook Delivery Failed

## Problem

GitHub shows failed deliveries.

## Solution

Navigate to:

```text
Repository
    ↓
Settings
    ↓
Webhooks
    ↓
Recent Deliveries
```

Inspect:

- HTTP status code
- Request payload
- Response message

Correct the issue and click **Redeliver**.

---

# 10. Secret Verification Failed

## Problem

Webhook requests are rejected.

## Cause

Webhook secret configured in GitHub does not match Jenkins.

## Solution

Verify both systems use the same secret value.

---

# 11. Firewall Blocking Requests

## Problem

GitHub cannot connect to Jenkins.

## Solution

Ensure:

- Port **8080** (or your configured port) is open.
- Reverse proxy allows incoming requests.
- Firewall rules permit GitHub access.

---

# 12. Build Starts but Fails

## Problem

Webhook triggers Jenkins, but the build fails.

## Solution

Open:

```text
Build History
    ↓
Console Output
```

Review the error message and fix the pipeline or build configuration.

---

# 13. Webhook Works Only Sometimes

## Possible Causes

- Network instability
- Jenkins overloaded
- Temporary GitHub service issues

## Solution

- Verify Jenkins health.
- Monitor system resources.
- Retry webhook delivery from GitHub.

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

Verify Git installation:

```bash
git --version
```

Check repository status:

```bash
git status
```

Display configured remotes:

```bash
git remote -v
```

Verify Java:

```bash
java --version
```

---

# Best Practices

- Use HTTPS for webhook communication.
- Configure a webhook secret.
- Enable only required webhook events.
- Verify webhook deliveries after setup.
- Keep Jenkins and plugins updated.
- Regularly review Jenkins logs.
- Test webhook functionality after configuration changes.

---

# Summary

Most GitHub Webhook issues are caused by incorrect Payload URLs, disabled build triggers, authentication problems, firewall restrictions, or Jenkins accessibility issues. Reviewing **GitHub Webhook Deliveries**, **Jenkins Console Output**, and **Jenkins logs** will resolve the majority of integration problems.