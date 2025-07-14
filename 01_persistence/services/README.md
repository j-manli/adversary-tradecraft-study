# Services

**MITRE ATT&CK Techniques:**  
- [T1543.003 – Create or Modify System Process: Windows Service](https://attack.mitre.org/techniques/T1543/003/)

When it comes to persistence, services are the long game.

Attackers love Windows services because they’re built to run quietly in the background with high privileges and minimal visibility. 
With just a few commands, a malicious binary can be set to auto-start at boot and run as **SYSTEM** (no user interaction, no popup, no drama).

### Why It Matters

In real intrusions, adversaries rarely drop loud persistence mechanisms. 
They register services with names like “Windows Update,” “Diagnostics Helper,” or “Driver Loader,” hoping defenders never look twice. 

- APT29 used malicious services for stealthy backdoors.
- Blue Mockingbird deployed fake services to load malicious DLLs.
- Ransomware groups frequently use `sc.exe` and `New-Service` to plant payloads before detonation.

### What to Look For

- Services created by unexpected parent processes (`powershell.exe`, `cmd.exe`)
- Binary paths outside trusted locations (`System32`, `Program Files`)
- Suspicious service names or display names mimicking Microsoft components
- `services.exe` spawning non-standard binaries

### About This Folder

This folder contains real-world inspired scenarios showing how attackers abuse the Windows service architecture for execution, persistence, and defense evasion. 
Each write-up is mapped to MITRE ATT&CK and includes detection strategies using Microsoft Defender for Endpoint and KQL.

Defenders who understand service abuse aren’t just watching — they’re hunting.

