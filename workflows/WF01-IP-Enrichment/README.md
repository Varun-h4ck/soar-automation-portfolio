# WF01 — IP Enrichment

## Overview
Automated IP threat intelligence lookup 
using Shuffle SOAR + VirusTotal API v3.

## Workflow Diagram
Webhook → VirusTotal v3 (Get IP Report)

## Trigger
HTTP Webhook
POST body: {"ip": "x.x.x.x"}

## Action
VirusTotal v3 — get_an_ip_address_report

## Tools
| Tool | Purpose |
|------|---------|
| Shuffle SOAR | Automation engine |
| VirusTotal v3 API | Threat intelligence |

## Test Results

### Test 1 — Clean IP
- Input: 8.8.8.8 (Google DNS)
- Status: 200 OK
- Malicious: 0
- Reputation: Positive
- Verdict: CLEAN ✅

### Test 2 — Malicious IP
- Input: 185.220.101.45
- Status: 200 OK
- Reputation: -22
- AS Owner: Stiftung Erneuerbare Freiheit
- Country: Germany (DE)
- Network: 185.220.101.0/24
- WHOIS: "Network for Tor-Exit traffic"
- Registry Name: TOR-EXIT
- Engines Analyzed: 91
- Verdict: MALICIOUS 🔴

## Key Learnings
- Webhook triggers allow any system to
  fire the workflow automatically
- Dynamic variables ($exec.ip) make
  workflows reusable for any IP
- Negative reputation score = threat indicator
- Tor exit nodes are used to anonymize
  attacker traffic

## Real World Use Case
SOC analyst receives alert with suspicious
source IP. Instead of manually checking
VirusTotal, this workflow enriches the IP
automatically in under 1 second.

## MITRE ATT&CK Reference
- T1090 — Proxy (Tor exit node usage)
