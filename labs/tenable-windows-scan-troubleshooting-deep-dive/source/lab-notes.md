# Troubleshooting and Deeply Understanding Scans

## Original lab notes

- Built an Azure environment connected to a custom NSG.
- Logged into Tenable and created an Advanced Network Scan.
- Updated plugin selection for the scan: Policy Compliance, Settings, and Windows.
- First scan published with no vulnerabilities found because NSG/network path was blocking access.
- Created a honeypot-style scenario by adding an inbound allow-all NSG rule.
- Second scan still showed no vulnerabilities because host firewall controls were still blocking scanner access.
- Turned off firewall and scanner could now reach and connect to the VM.
- Discoverable items appeared in Tenable.

## PowerShell troubleshooting steps used on target VM

### Step 1: Make VM visible (connectivity)

```powershell
# 1. Enable Ping (ICMP)
Enable-NetFirewallRule -DisplayName "File and Printer Sharing (Echo Request - ICMPv4-In)"

# 2. Open SMB (Port 445)
Enable-NetFirewallRule -DisplayGroup "File and Printer Sharing"

# 3. Open WMI (Port 135)
Enable-NetFirewallRule -DisplayGroup "Windows Management Instrumentation (WMI)"
```

### Step 2: Enable remote audit permissions

```powershell
# Keep admin token privileges over remote connections
New-ItemProperty -Path "HKLM:\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\System" -Name "LocalAccountTokenFilterPolicy" -Value 1 -PropertyType DWORD -Force

# Enable Remote Registry for policy/compliance checks
Set-Service -Name RemoteRegistry -StartupType Automatic
Start-Service -Name RemoteRegistry
```

### Step 3: Adjust scan behavior for troubleshooting

- In Tenable Discovery > Host Discovery, disable `Ping the remote host`.
- This forces deeper probing even when ICMP responses are unreliable.

## Outcome summary

- After connectivity and remote-audit fixes, scan runtime and depth improved.
- Tenable began returning vulnerability and policy results.
- Follow-up runs included credentialed and non-credentialed scan comparisons.
