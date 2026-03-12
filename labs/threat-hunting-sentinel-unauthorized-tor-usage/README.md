# Threat Hunting Lab: Unauthorized TOR Usage

## Objective

Detect unauthorized TOR installation and usage on an endpoint by correlating file, process, and network telemetry in Microsoft Defender/Sentinel hunting workflows.

## Environment

- Microsoft Defender endpoint telemetry
- Sentinel/Log Analytics hunting context
- Data sources: `DeviceFileEvents`, `DeviceProcessEvents`, `DeviceNetworkEvents`

## Detection strategy

- File detection for TOR installer/binaries and suspicious user artifacts.
- Process detection for silent installer execution and TOR/browser launch patterns.
- Network detection for connections on TOR-associated ports (`9001`, `9030`, `9040`, `9050`, `9051`, `9150`).
- User-behavior artifact detection around `tor-shopping-list.txt` creation/deletion.

## Analyst notes

This lab is built from a threat-event brief and query set focused on post-installation TOR behavior and user-intent indicators. The core value is correlation across telemetry domains (file + process + network) rather than any single indicator in isolation.

## Evidence status

No new screenshots were present in the folder at processing time. Add them later under:

- `evidence/01-...png`
- `evidence/02-...png`
- `evidence/03-...png`

I will map and label them in the same neutral analyst style as your other labs.

## Redaction note

Any screenshots or exported logs for this lab may contain sensitive identifiers (hostnames, usernames, IPs, tenant details, URLs, or account IDs). Redact before public publishing.

## Source briefs

- Threat event brief: `source/lab-brief.md`
