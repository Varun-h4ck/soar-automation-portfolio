
# WF05 — New User Created Alert

## Overview
Automated detection of new Linux user
creation using Wazuh SIEM + Shuffle SOAR
with Gmail email notification.

## Workflow Diagram
Wazuh (rule 5902) → Shuffle Webhook
→ Gmail SMTP Email

## Trigger
Wazuh Rule 5902 — New user added
to the system
Severity: 3

## Action
Gmail SMTP sends email notification
with full user creation details

## Tools
| Tool | Purpose |
|------|---------|
| Wazuh SIEM | User creation detection |
| Shuffle SOAR | Automation engine |
| Gmail SMTP | Alert notification |

## Test Method
```bash
sudo useradd testuser3
sudo userdel testuser3
```

## Test Results
- Wazuh detection: ✅ Rule 5902 fired
- Alert data: name=testuser3, UID=1001
- Shuffle execution: ✅ Finished
- Email delivery: ✅ Confirmed

## Email Alert Sample
- Subject: Wazuh Alert - New User
  Created on Ubuntu
- Body: Details of new user including
  username, UID, GID, home directory

## Key Learnings
- Wazuh monitors /var/log/auth.log
  for useradd commands in real time
- Rule 5902 fires immediately when
  any new user is created
- Full user details captured including
  UID, GID and home directory
- Attacker backdoor accounts detected
  instantly — zero manual monitoring

## Real World Use Case
Attacker gains access and creates
backdoor user account. SOC analyst
receives instant alert with full
account details for immediate
investigation and response.

## MITRE ATT&CK
| Technique | ID | Description |
|-----------|-----|-------------|
| Create Account | T1136 | New account |
| Local Account | T1136.001 | Linux user |
