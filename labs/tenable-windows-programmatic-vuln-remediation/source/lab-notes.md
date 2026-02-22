# Programmatic Vulnerability Remediation (Windows) - Additional Notes

## Troubleshooting context

- For multiple days, authenticated scans were not reaching the VM properly.
- Tenable was often only reporting SSL/TLS issues instead of the intentionally installed vulnerabilities.
- This indicated the scan path/host reachability was incomplete even though the scan was configured as authenticated.

## Connectivity helper approach

- To reduce repeated environment setup failures, a PowerShell helper script was created to improve scan connectivity prerequisites.
- After using the script, scan results improved from partial/low findings (for example, 2 medium findings or failed/partial connection behavior) to showing the full installed vulnerabilities.
- GitHub reference for the helper script (user-provided): https://lnkd.in/eReeBi5y

## RDP lockout / recovery root cause

- A PowerShell action reset Windows Firewall and restarted it, but did not restore required inbound access for RDP.
- `netsh advfirewall reset` reset firewall rules to default state, and port `3389` access was not restored.
- Result: no RDP, no Bastion, and no Windows remote access from macOS.

## Recovery steps used

- Used Azure VM Help -> Boot Diagnostics to access Serial Console.
- Recreated command access from Serial Console.
- Re-enabled RDP in registry.
- Started Remote Desktop Service.
- Re-enabled Windows Firewall Remote Desktop rules.
- Added an explicit allow rule for port `3389`.
- RDP access returned, enabling testing and script execution.

## Outcome

- Once connectivity and remote access were fixed, authenticated scans showed the installed vulnerabilities correctly.
- Programmatic remediation testing could proceed as intended.
