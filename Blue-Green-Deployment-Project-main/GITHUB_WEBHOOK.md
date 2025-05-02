# GitHub Webhook Integration with Jenkins

## Prerequisites
1. Jenkins server is up and running
2. GitHub repository with the application code
3. Jenkins GitHub plugin installed

## Setup Steps

### 1. Configure GitHub Webhook
1. Go to your GitHub repository
2. Navigate to Settings > Webhooks
3. Click "Add webhook"
4. Configure the webhook:
   - Payload URL: `http://<jenkins-server-ip>:8080/github-webhook/`
   - Content type: `application/json`
   - Secret: (optional) Add a secret for security
   - Events: Select "Just the push event"
   - Active: Check the box
5. Click "Add webhook"

### 2. Configure Jenkins Job
1. In Jenkins, go to your pipeline job
2. Click "Configure"
3. Under "Build Triggers", check "GitHub hook trigger for GITScm polling"
4. Save the configuration

### 3. Verify Webhook Connection
1. Make a small change to your repository
2. Push the changes to GitHub
3. Check Jenkins to see if the build is triggered automatically

## Troubleshooting
1. If webhook is not triggering:
   - Check Jenkins logs for any errors
   - Verify GitHub webhook delivery status
   - Ensure Jenkins server is accessible from GitHub
   - Check if GitHub plugin is properly installed in Jenkins

2. Common Issues:
   - Network connectivity between GitHub and Jenkins
   - Incorrect webhook URL
   - Missing GitHub plugin in Jenkins
   - Jenkins security settings blocking webhook requests

## Security Considerations
1. Use HTTPS for webhook URL if possible
2. Implement webhook secret for additional security
3. Restrict Jenkins access to specific IP ranges
4. Use Jenkins credentials for repository access 