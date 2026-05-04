
# WF02 — Domain Enrichment

## Overview
Automated domain threat intelligence lookup
using Shuffle SOAR + VirusTotal API v3.

## Workflow Diagram
Webhook → VirusTotal v3 (Get Domain Report)

## Trigger
HTTP Webhook
POST body: {"domain": "example.com"}

## Action
VirusTotal v3 — get_a_domain_report

## Tools
| Tool | Purpose |
|------|---------|
| Shuffle SOAR | Automation engine |
| VirusTotal v3 API | Threat intelligence |

## Test Results

### Test — Malicious Domain
- Input: malware.wicar.org
- Status: 200 OK
- Reputation: -59
- Malicious Engines: 16/91
- Suspicious Engines: 2/91
- Harmless Engines: 43/91
- Community Votes: 11 malicious, 3 harmless
- Certificate: Let's Encrypt (valid SSL)
- Registrar: PublicDomainRegistry.com
- Verdict: CONFIRMED MALICIOUS 🔴

## Key Learnings
- Domain enrichment automates phishing
  triage for SOC analysts
- HTTPS and valid SSL cert does NOT mean
  safe — attackers use free certs too
- Reputation below -20 is serious threat
  indicator
- 16/91 engine detection is significant

## Real World Use Case
Phishing email received with suspicious
domain link. Workflow automatically checks
domain reputation and returns verdict in
under 1 second — no manual VirusTotal
visit needed.

## MITRE ATT&CK Reference
- T1566 — Phishing
- T1071 — Application Layer Protocol
