# Splunk-Shuffle-Login-Alert-Automation
Automated detection of failed Windows login attempts using Splunk and Shuffle SOAR
# Splunk and Shuffle – Failed Login Alert Automation

## Project Overview

This project demonstrates the detection of multiple failed Windows login attempts using Splunk Enterprise and automated email alerting using Shuffle SOAR.

The objective is to identify failed authentication attempts, generate a Splunk alert, and send an email notification for security investigation.

## Tools and Technologies

- Splunk Enterprise
- Shuffle SOAR
- Windows Security Event Logs
- SPL (Search Processing Language)
- Webhooks
- Email Notifications

## Use Case

**Multiple Failed Login Attempts**

Detect repeated failed login attempts on a Windows system and notify the security analyst through an automated email alert.

## Implementation

### 1. Log Collection

Windows Security logs were collected and monitored in Splunk.

Windows Event ID 4625 represents a failed logon attempt.

### 2. Splunk Search

The following SPL query was used to identify failed login attempts and summarize them by account and host.

```spl
index=main sourcetype=WinEventLog:Security EventCode=4625
| stats count by Account_Name, host
```

### 3. Alert Configuration

A scheduled alert named `login failures` was created in Splunk.

- Alert Type: Scheduled
- Schedule: Every 5 minutes
- Trigger Condition: Number of events greater than 0
- Trigger Action: Webhook

### 4. Shuffle SOAR Integration

A Shuffle workflow was created with the following components:

- Webhook: Receives the Splunk alert.
- Email Action: Sends an email notification.

### 5. Email Notification

The email alert contains:

- Alert Name
- Username
- Host
- Failed Login Count
- Event Code
- Recommended Investigation Action

### 6. Testing

Failed login attempts were generated on the Windows system.

The Splunk alert was triggered, the webhook received the alert data, and the Shuffle workflow sent an email notification.

The email delivery was verified successfully.

## Workflow

Windows Security Logs → Splunk → Scheduled Alert → Shuffle Webhook → Email Notification

## Learning Outcomes

- Understanding Windows Security Event ID 4625.
- Creating SPL searches for security monitoring.
- Configuring scheduled alerts in Splunk.
- Integrating Splunk with Shuffle using webhooks.
- Automating security notifications using SOAR.
- Understanding basic SOC alerting and investigation workflows.

## Disclaimer

This project was performed in a personal lab environment for educational purposes.
