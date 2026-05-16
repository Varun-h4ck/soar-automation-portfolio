
# WF07 — Suspicious Process Execution

## Overview
Automated detection of suspicious process
execution using Wazuh SIEM + Shuffle SOAR
with Gmail email notification.

## Workflow Diagram
Wazuh (rule 5710) → Shuffle Webhook
→ Gmail SMTP Email

## Trigger
Wazuh Rule 5710 — Suspicious process
executed (netcat, nmap, etc)
Severity: 3

## Action
Gmail SMTP sends email notification
with full process details

## Tools
| Tool | Purpose |
|------|---------|
| Wazuh SIEM | Process detection |
| Shuffle SOAR | Automation engine |
| Gmail SMTP | Alert notification |

## Test Method
Simulated via curl webhook trigger:
- Process: netcat
- Rule: 5710
- Agent: ubuntu

## Test Results
- Webhook received: ✅
- Email delivery: ✅ Confirmed
- Response time: 3 seconds

## Email Alert Sample
Subject: Wazuh Alert - Suspicious
         Process Detected
Body:
- Details: netcat process detected
- Time: 2026-05-16T14:00:00
- Rule: 5710
- Agent: ubuntu

## Key Learnings
- Suspicious process detection is critical
  for catching attacker tools early
- Netcat is commonly used for reverse
  shells and data exfiltration
- Instant alerting prevents dwell time
  from growing

## MITRE ATT&CK
| Technique | ID | Description |
|-----------|-----|-------------|
| Command & Scripting | T1059 | Shell execution |
| Unix Shell | T1059.004 | Bash/sh commands |
| Non-App Layer Protocol | T1095 | Netcat usage |
