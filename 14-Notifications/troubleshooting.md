# Troubleshooting

This guide covers common issues encountered while configuring and using notifications in Jenkins pipelines.

---

# 1. Email Notifications Not Sent

## Problem

```text
Failed to send email
```

## Possible Causes

- SMTP server not configured
- Incorrect SMTP credentials
- Firewall blocking SMTP port
- Invalid recipient email address

## Solution

Verify:

- SMTP server address
- SMTP port
- Username and password
- Sender email address

Send a test email from:

```text
Manage Jenkins
    ↓
System
    ↓
Extended E-mail Notification
```

---

# 2. SMTP Authentication Failed

## Problem

```text
Authentication failed
```

## Cause

Incorrect SMTP username or password.

## Solution

- Verify SMTP credentials.
- Use an App Password if your email provider requires one.
- Store credentials securely using Jenkins Credentials.

---

# 3. Slack Notification Failed

## Problem

```text
Slack notification failed
```

## Possible Causes

- Invalid webhook URL
- Incorrect Bot Token
- Wrong channel name
- Missing Slack plugin

## Solution

Verify:

- Slack Workspace
- Bot Token
- Channel Name
- Credential ID

Send a test notification from Jenkins.

---

# 4. Microsoft Teams Notification Failed

## Problem

```text
HTTP 400 Bad Request
```

## Cause

Invalid or expired webhook URL.

## Solution

- Generate a new Incoming Webhook.
- Update the webhook URL in Jenkins.
- Test the webhook using a simple HTTP request.

---

# 5. Discord Webhook Failed

## Problem

```text
404 Not Found
```

## Cause

Webhook URL is incorrect or deleted.

## Solution

Create a new webhook in Discord and update the Jenkins configuration.

---

# 6. Notification Plugin Missing

## Problem

```text
No such DSL method
```

Example:

```text
No such DSL method 'slackSend'
```

## Cause

Required plugin is not installed.

## Solution

Navigate to:

```text
Manage Jenkins
    ↓
Plugins
```

Install the required plugin and restart Jenkins.

---

# 7. Email Sent But Not Received

## Possible Causes

- Spam filter
- Incorrect recipient
- Mail server delay

## Solution

- Check the Spam/Junk folder.
- Verify recipient email addresses.
- Review SMTP server logs if available.

---

# 8. Environment Variables Not Displayed

## Problem

```text
null
```

or

```text
Variable not found
```

## Cause

The variable is unavailable in the current pipeline context.

## Solution

Verify the variable name.

Example:

```groovy
echo env.BUILD_NUMBER
echo env.JOB_NAME
echo env.BUILD_URL
```

---

# 9. Notification Sent at Wrong Time

## Cause

Incorrect `post` block configuration.

## Solution

Verify the pipeline:

```groovy
post {

    success {
        echo 'Success'
    }

    failure {
        echo 'Failure'
    }

    always {
        cleanWs()
    }

}
```

---

# 10. Jenkins Credentials Not Found

## Problem

```text
Credentials not found
```

## Solution

Navigate to:

```text
Manage Jenkins
    ↓
Credentials
```

Verify:

- Credential ID
- Username
- Password
- Secret Token

---

# 11. Pipeline Stops Before Notification

## Cause

Pipeline failed before reaching the notification step.

## Solution

Move notifications into the `post` section so they execute after the pipeline finishes.

Example:

```groovy
post {

    always {
        echo 'Pipeline Finished'
    }

}
```

---

# 12. Firewall Blocking Notifications

## Problem

Notification requests time out.

## Cause

Network or firewall restrictions.

## Solution

Verify:

- Internet connectivity
- Firewall rules
- Proxy configuration
- SMTP or HTTPS access

---

# Useful Verification Commands

Verify internet connectivity:

```bash
ping google.com
```

Test HTTPS access:

```bash
curl https://www.google.com
```

Test SMTP connectivity:

```bash
telnet smtp.gmail.com 587
```

Check Jenkins service:

```bash
sudo systemctl status jenkins
```

Restart Jenkins:

```bash
sudo systemctl restart jenkins
```

---

# Best Practices

- Store passwords, API keys, and webhook URLs in Jenkins Credentials.
- Send notifications only for important events.
- Include build number, job name, and build URL.
- Test notification channels regularly.
- Monitor failed notification attempts.
- Keep notification messages concise and actionable.
- Avoid exposing sensitive information in notification content.

---

# Summary

Most Jenkins notification issues are caused by incorrect SMTP settings, invalid webhook URLs, missing plugins, expired credentials, or network connectivity problems. Reviewing the Jenkins Console Output, verifying plugin configuration, and testing external services independently will resolve the majority of notification-related issues.