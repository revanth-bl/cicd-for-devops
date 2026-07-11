# Commands

This section contains commonly used commands and Jenkins Pipeline snippets for configuring and sending notifications after CI/CD pipeline execution.

---

# Email Notification Plugin

Navigate to:

```text
Manage Jenkins
    ↓
Plugins
    ↓
Available Plugins
    ↓
Email Extension Plugin
```

Install the plugin and restart Jenkins if required.

---

# Configure SMTP Server

Navigate to:

```text
Manage Jenkins
    ↓
System
    ↓
Extended E-mail Notification
```

Configure:

- SMTP Server
- SMTP Port
- Username
- Password
- Default Sender Address

---

# Test Email Configuration

Navigate to:

```text
Manage Jenkins
    ↓
System
    ↓
Extended E-mail Notification
```

Send a test email.

---

# Basic Email Notification

```groovy
post {

    success {

        mail(
            to: 'team@example.com',
            subject: 'Build Successful',
            body: 'The Jenkins build completed successfully.'
        )

    }

}
```

---

# Email Notification on Failure

```groovy
post {

    failure {

        mail(
            to: 'team@example.com',
            subject: 'Build Failed',
            body: 'The Jenkins build has failed.'
        )

    }

}
```

---

# Always Send Email

```groovy
post {

    always {

        mail(
            to: 'team@example.com',
            subject: 'Build Finished',
            body: 'The pipeline execution has completed.'
        )

    }

}
```

---

# Slack Notification Plugin

Install:

```text
Manage Jenkins
    ↓
Plugins
    ↓
Slack Notification Plugin
```

---

# Configure Slack

Navigate to:

```text
Manage Jenkins
    ↓
System
    ↓
Slack
```

Configure:

- Workspace
- Channel
- Bot Token
- Credential ID

---

# Slack Success Notification

```groovy
post {

    success {

        slackSend(
            channel: '#devops',
            message: 'Build completed successfully.'
        )

    }

}
```

---

# Slack Failure Notification

```groovy
post {

    failure {

        slackSend(
            channel: '#devops',
            message: 'Build failed.'
        )

    }

}
```

---

# Microsoft Teams Notification

Example using webhook:

```groovy
post {

    success {

        office365ConnectorSend(
            message: 'Deployment completed successfully.'
        )

    }

}
```

---

# Discord Webhook

Example:

```groovy
sh '''
curl -H "Content-Type: application/json" \
-X POST \
-d '{"content":"Pipeline completed successfully"}' \
WEBHOOK_URL
'''
```

---

# Jenkins Build Information

Build Number

```groovy
echo env.BUILD_NUMBER
```

Build URL

```groovy
echo env.BUILD_URL
```

Job Name

```groovy
echo env.JOB_NAME
```

Branch Name

```groovy
echo env.BRANCH_NAME
```

---

# Common Environment Variables

```groovy
echo env.BUILD_NUMBER
echo env.BUILD_ID
echo env.BUILD_TAG
echo env.JOB_NAME
echo env.NODE_NAME
echo env.WORKSPACE
echo env.GIT_BRANCH
```

---

# Archive Build Logs

```groovy
archiveArtifacts artifacts: '**/*.log'
```

---

# Publish Test Results

```groovy
junit '**/target/surefire-reports/*.xml'
```

---

# Clean Workspace

```groovy
cleanWs()
```

---

# Complete Post Section

```groovy
post {

    always {
        cleanWs()
    }

    success {
        echo 'Build Successful'
    }

    failure {
        echo 'Build Failed'
    }

    unstable {
        echo 'Build Unstable'
    }

    aborted {
        echo 'Build Aborted'
    }

}
```

---

# Git Commands

Stage changes

```bash
git add .
```

Commit changes

```bash
git commit -m "Add notifications"
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
| `mail()` | Send email notifications |
| `slackSend()` | Send Slack notifications |
| `office365ConnectorSend()` | Send Microsoft Teams notifications |
| `archiveArtifacts` | Archive build artifacts |
| `junit` | Publish test reports |
| `cleanWs()` | Clean Jenkins workspace |
| `env.BUILD_NUMBER` | Current build number |
| `env.BUILD_URL` | Jenkins build URL |
| `env.JOB_NAME` | Jenkins job name |
| `post {}` | Execute actions after pipeline completion |

---

# Notes

- Configure SMTP before enabling email notifications.
- Store SMTP passwords and webhook URLs using Jenkins Credentials.
- Notify teams only when necessary to avoid notification fatigue.
- Include useful information such as build number, job name, and build URL in notifications.
- Use different notification channels for different audiences (Email, Slack, Teams, Discord).
- Send failure notifications immediately so issues can be addressed quickly.
- Clean the workspace after pipeline execution to maintain a clean build environment.