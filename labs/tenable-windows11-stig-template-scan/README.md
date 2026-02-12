# Tenable Windows 11 Lab: Scan Template + STIG Compliance

## Objective

Build and use a reusable Tenable scan template for a Windows 11 VM, then run a credentialed scan with STIG compliance checks to validate vulnerability and audit coverage.

## Environment

- Azure-hosted Windows 11 virtual machine
- Tenable Vulnerability Management (cloud)
- Scan type: Advanced Network Scan template
- Credentialed checks with Windows administrator credentials
- Compliance audit: DISA Microsoft Windows 11 STIG (or closest available revision)

## Workflow Summary

1. Create a Windows 11 VM in Azure and prepare network access.
2. Configure host prerequisites (for lab simulation), including firewall/host settings needed for connectivity and scanning.
3. Create a Tenable scan template and configure:
- Basic settings (service startup/share options)
- Discovery settings (ping, fast network discovery, TCP scanning)
- Assessment settings (thorough tests)
- Credentials (Windows admin account)
- Compliance audit selection (Windows 11 STIG)
- Plugin scope (general, policy/compliance, Windows checks/bulletins/user management)
4. Create a scan from the template, set target IP, launch, and review vulnerabilities, audits, and remediations.

## Evidence

### 1) Azure VM creation
![Azure VM creation](evidence/01-azure-vm-creation.png)

### 2) Host firewall adjustment for lab connectivity
![Disable firewall](evidence/02-disable-firewall.png)

### 3) Template basic setup
![Template basic settings](evidence/03-template-basic-settings.png)

### 4) Selecting scan template in Tenable
![Select template](evidence/04-select-template.png)

### 5) Discovery settings (TCP + fast discovery)
![Discovery settings](evidence/05-discovery-settings.png)

### 6) Assessment settings
![Assessment settings](evidence/06-assessment-settings.png)

### 7) Compliance audit assignment (STIG)
![Compliance STIG selection](evidence/07-compliance-stig-selection.png)

### 8) Plugin selection
![Plugin selection](evidence/08-plugin-selection.png)

### 9) Final scan setup from template
![Scan setup from template](evidence/09-scan-setup-from-template.png)

## Key Takeaways

- Using a template standardizes scan configuration and makes repeat scans consistent.
- Credentialed Windows scanning improves depth versus network-only checks.
- STIG compliance audits add policy-level assessment beyond CVE/plugin vulnerability checks.
- Targeted plugin selection can reduce unnecessary scan noise while keeping required coverage.

## Redaction Note

This lab evidence may include sensitive identifiers (public/private IPs, hostnames, usernames, scanner names, or tenant details). Redact or blur these fields before any public publishing.

## Source Brief

- Lab notes: `source/lab-brief.docx`
