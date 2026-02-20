# Tenable Linux Lab: Manual Vulnerability Creation and Remediation

## Objective

Run authenticated Linux scanning, intentionally introduce insecure configurations, and verify remediation through follow-up scans.

## Environment

- Ubuntu 24.04 LTS VM in Azure
- Tenable Vulnerability Management (authenticated scanning)
- Linux DISA/STIG user-defined scan template
- SSH credentialed scanning with privilege elevation

## Evidence

### Baseline authenticated scan before manual vulnerability changes

![Baseline scan](evidence/01-baseline-auth-scan.png)

### SMB configuration edit to introduce vulnerable protocol settings

![SMB config edit](evidence/02-smb-config-edit.png)

### Service/port verification after service changes

![Port verification](evidence/03-service-port-verification.png)

### Anonymous FTP enabled in configuration

![Anonymous FTP enabled](evidence/04-ftp-anonymous-enabled.png)

### Proof of anonymous upload risk

![Anonymous FTP risk proof](evidence/05-ftp-anonymous-risk-proof.png)

### Scan results after vulnerability creation

![Post-vulnerability scan](evidence/06-post-vuln-creation-scan.png)

### SMB remediation actions

![SMB remediation](evidence/07-smb-remediation.png)

### Anonymous FTP disabled

![Anonymous FTP disabled](evidence/08-ftp-anonymous-disabled.png)

### Configuration cleanup verification

![Global line removed](evidence/09-config-cleanup-global-line-removed.png)

### FTP package removal and verification

![FTP package removal](evidence/10-ftp-package-removal.png)

### Closed-service verification (FTP no longer accessible)

![FTP closed verification](evidence/11-ftp-closed-verification.png)

### Final rescan after remediation

![Final rescan results](evidence/12-final-rescan-results.png)

## What changed & why

This lab progressed from a clean authenticated Linux baseline to intentional vulnerability introduction (SMB protocol weakening and anonymous FTP exposure), followed by hardening and package removal. Rescan evidence confirms that remediation steps reduced attack surface and removed risky services.

## Notable findings (examples)

- Preliminary scan behavior issues were caused by target addressing mistakes; using the correct internal/private target in the internal scanner path fixed scan execution consistency.
- Vulnerability visibility increased after deliberate insecure configuration changes.
- Remediation actions included disabling SMB-related weak settings, disabling anonymous FTP, and removing vulnerable/unneeded services/packages.
- Final scans showed reduced findings after cleanup and service closure checks.

## Redaction note

Current screenshots and artifacts may include sensitive identifiers (for example IP addresses, hostnames, usernames, tenant details, scanner names, or credential-related fields). Redact or blur sensitive fields before public publishing.

## Source brief

- Lab notes: `source/lab-brief.docx`
