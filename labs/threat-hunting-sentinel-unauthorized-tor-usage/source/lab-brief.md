# Threat Event (Unauthorized TOR Usage)

## Unauthorized TOR Browser Installation and Use

## Steps the "Bad Actor" took to create logs and IoCs

1. Download the TOR browser installer: https://www.torproject.org/download/
2. Install it silently: `tor-browser-windows-x86_64-portable-14.0.1.exe /S`
3. Open TOR browser from desktop folder.
4. Connect to TOR and browse onion/related sites.
5. Create `tor-shopping-list.txt` on desktop with illicit items.
6. Delete the file.

## Tables Used to Detect IoCs

- `DeviceFileEvents`
  - Purpose: detect TOR download/install artifacts and shopping-list create/delete activity.

- `DeviceProcessEvents`
  - Purpose: detect silent TOR installation and TOR/firefox launch behavior.

- `DeviceNetworkEvents`
  - Purpose: detect TOR-related connections from `tor.exe`/`firefox.exe` on typical TOR ports.

## Related Queries

```kql
// Installer name == tor-browser-windows-x86_64-portable-(version).exe
// Detect installer download activity
DeviceFileEvents
| where FileName startswith "tor"

// TOR browser silent install
DeviceProcessEvents
| where ProcessCommandLine contains "tor-browser-windows-x86_64-portable-14.0.1.exe  /S"
| project Timestamp, DeviceName, ActionType, FileName, ProcessCommandLine

// TOR binaries present on disk
DeviceFileEvents
| where FileName has_any ("tor.exe", "firefox.exe")
| project Timestamp, DeviceName, RequestAccountName, ActionType, InitiatingProcessCommandLine

// TOR/browser launch activity
DeviceProcessEvents
| where ProcessCommandLine has_any("tor.exe","firefox.exe")
| project Timestamp, DeviceName, AccountName, ActionType, ProcessCommandLine

// TOR/browser network usage
DeviceNetworkEvents
| where InitiatingProcessFileName in~ ("tor.exe", "firefox.exe")
| where RemotePort in (9001, 9030, 9040, 9050, 9051, 9150)
| project Timestamp, DeviceName, InitiatingProcessAccountName, InitiatingProcessFileName, RemoteIP, RemotePort, RemoteUrl
| order by Timestamp desc

// shopping-list file lifecycle
DeviceFileEvents
| where FileName contains "shopping-list.txt"
```

## Attribution

- Author Name: Suki Kesington
- Author Contact: https://www.linkedin.com/in/sukikesington
- Source draft basis: Josh Madakor threat event template
