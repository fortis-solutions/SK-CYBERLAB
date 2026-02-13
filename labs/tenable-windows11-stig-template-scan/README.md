# Tenable Windows 11 Lab: Scan Template + STIG Compliance

## Objective

Build and use a reusable Tenable scan template for a Windows 11 VM, then run a credentialed scan with STIG compliance checks to validate vulnerability and audit coverage.

## Environment

- Cloud-hosted Windows 11 VM (Azure)
- Tenable Vulnerability Management
- Advanced Network Scan template
- Windows credentialed scanning (administrator account)
- Compliance audit profile for DISA Microsoft Windows 11 STIG

## Evidence

### Windows 11 VM creation in Azure

![Azure VM creation](evidence/01-azure-vm-creation.png)

### Firewall/host preparation for lab connectivity

![Disable firewall](evidence/02-disable-firewall.png)

### Template basic configuration

![Template basic settings](evidence/03-template-basic-settings.png)

### Scan template selection in Tenable

![Select template](evidence/04-select-template.png)

### Discovery settings (TCP + fast discovery)

![Discovery settings](evidence/05-discovery-settings.png)

### Assessment settings

![Assessment settings](evidence/06-assessment-settings.png)

### Compliance audit selection (Windows 11 STIG)

![Compliance STIG selection](evidence/07-compliance-stig-selection.png)

### Plugin scope selection

![Plugin selection](evidence/08-plugin-selection.png)

### Final scan setup from template

![Scan setup from template](evidence/09-scan-setup-from-template.png)

### Compliance audit results with failures

![Audit compliance failures](evidence/10-audit-results-compliance-failures.png)

## What changed & why

Compared with a standard vulnerability-only run, this workflow adds a reusable template plus compliance auditing. Credentialed checks allow deeper host inspection, and STIG policy audits validate security-control posture rather than only service-exposed vulnerabilities.

## Notable findings (examples)

Tenable compliance output shows failed STIG controls, demonstrating that the policy audit executed successfully and produced control-level remediation targets. The scan configuration evidence also confirms deliberate scope choices for discovery, assessment depth, compliance checks, and plugin categories.

## Redaction note

Current screenshots and artifacts may include sensitive identifiers (for example internal/public IP addresses, hostnames, usernames, scanner names, or tenant details). Before publishing publicly, crop or blur sensitive fields and redact identifiers.

## Source brief

- Lab notes: `source/lab-brief.docx`
