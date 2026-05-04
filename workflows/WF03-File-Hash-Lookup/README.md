# WF03 — File Hash Lookup

## Overview
Automated file hash malware lookup 
using Shuffle SOAR + VirusTotal API v3.

## Workflow Diagram
Webhook → VirusTotal v3 (Get Hash Report)

## Trigger
HTTP Webhook
POST body: {"hash": "sha256_or_md5_here"}

## Action
VirusTotal v3 — get_a_hash_report

## Tools
| Tool | Purpose |
|------|---------|
| Shuffle SOAR | Automation engine |
| VirusTotal v3 API | Malware intelligence |

## Test Results

### Test — EICAR Standard Malware Test File
- **Input Hash:** 275a021bbfb6489e54d471899f7db9d1663fc695ec2fe2a2c4538aabf651fd0f
- **Status:** 200 OK ✅
- **Meaningful Name:** eicar.com
- **File Size:** 68 bytes
- **Malicious Engines:** 65/74 (87%) 🔴
- **Suspicious Engines:** 0
- **Harmless Engines:** 0
- **Reputation:** 3735 (globally known)
- **Classification:** MALWARE + TROJAN
- **Antiy Info:** Trojan/Generic.ASBOL.2A
- **Sandbox — Zenbox:** MALICIOUS
- **Sandbox — Lastline:** MALICIOUS
- **Sandbox Confidence:** 56
- **Verdict:** CONFIRMED MALWARE 🔴

## Key Learnings
- Hash-based lookup is the fastest way
  to check if a file is known malware
- 87% detection rate across 74 AV engines
  simultaneously in under 1 second
- File size is irrelevant — 68 bytes
  is enough to be dangerous malware
- Sandbox analysis confirms actual
  behaviour, not just signature matching
- Reputation 3735 = one of the most
  globally recognised malware samples
- Zero engines marked it harmless —
  completely unambiguous verdict

## Real World Use Case
EDR alert fires on a suspicious file
found on an endpoint. The file hash is
automatically extracted and sent to this
workflow. Instantly checked against 74
AV engines with zero manual effort —
replaces what used to take a analyst
several minutes of manual VirusTotal
lookups.


## MITRE ATT&CK Reference
| Technique | ID | Relevance |
|-----------|-----|-----------|
| User Execution | T1204 | Malicious file run by user |
| Spearphishing Attachment | T1566.001 | File delivered via email |
| Malicious File | T1204.002 | Direct file execution |
