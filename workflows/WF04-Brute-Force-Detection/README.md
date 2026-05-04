# WF04 — Brute Force Detection

## Overview
Automated brute force attack detection
using Wazuh SIEM + Shuffle SOAR with
email notification.

## Workflow Diagram
Wazuh (rule 5503) → Shuffle Webhook 
→ Email Notification

## Trigger
Wazuh alert for failed SSH login attempts
- Rule 5503: PAM User login failed
- Rule 5502: PAM Login session closed
- Severity: 2

## Action
Shuffle Email App sends Gmail notification

## Tools
| Tool | Purpose |
|------|---------|
| Wazuh SIEM | Attack detection |
| Shuffle SOAR | Automation engine |
| Shuffle Email | Alert notification |

## Test Method
Simulated brute force attack:
```bash
for i in {1..5}; do sshpass -p wrongpassword \
ssh -o StrictHostKeyChecking=no \
fakeuser@127.0.0.1 2>/dev/null; done
```

## Test Results
- Wazuh detection: ✅ Immediate
- Shuffle execution: ✅ 50+ runs
- Email delivery: ✅ Confirmed
- Response time: Under 2 seconds

## Email Alert Sample
From: email-app@shuffler.io
Subject: PAM: User login failed.
Body: May 4 19:19:08 ubuntu sshd:pam_unix(sshd:auth):authentication failure
