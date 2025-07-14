# Registry Run Key Persistence (Autoruns)

Windows autorun keys offer attackers a reliable way to regain access after reboot without needing sophisticated malware or kernel-level tricks. 
These keys, used by both legitimate applications and adversaries, tell Windows which programs to launch automatically during user logon or system startup.

This technique is widely abused for user-level and system-level persistence by advanced threat actors.

MITRE ATT&CK Reference: [T1547.001 – Registry Run Keys / Startup Folder](https://attack.mitre.org/techniques/T1547/001/)

---

## How It Works

Windows provides multiple registry locations that support auto-start behavior. The most common are:

| Scope      | Key Path                                                                 |
|------------|--------------------------------------------------------------------------|
| User-level | `HKCU\Software\Microsoft\Windows\CurrentVersion\Run`                    |
| User-level | `HKCU\Software\Microsoft\Windows\CurrentVersion\RunOnce`               |
| System-wide| `HKLM\Software\Microsoft\Windows\CurrentVersion\Run`                   |
| System-wide| `HKLM\Software\Microsoft\Windows\CurrentVersion\RunOnce`              |
| Shell Folders| `HKCU\...\Explorer\Shell Folders`, `User Shell Folders`              |

By adding a new value to any of these keys, attackers can instruct Windows to launch a binary of their choosing every time the target logs in.

---

## Access Levels Matter

| Registry Hive | Description                                     | Typical Use Case                   |
|---------------|--------------------------------------------------|------------------------------------|
| `HKCU`        | Current user context (no elevation required)     | Used post-user compromise          |
| `HKLM`        | Applies to all users (requires admin rights)     | Used after privilege escalation     |

In real-world intrusions, attackers often start by persisting under `HKCU` and move to `HKLM` once they escalate privileges—maximizing resilience.

---

## Why It Matters

Registry-based autoruns are:

- **Simple** to deploy via command line or scripts
- **Low-friction** — they don't require dropping services or drivers
- **Quiet** — often fly under the radar in noisy environments
- **Persistent** — survive reboot and user logoff

---

## Detection Tips

While some EDR tools flag new registry autorun entries, defenders should watch for:

- Execution of unusual binaries from user profiles
- Registry modifications under `Run` or `RunOnce`
- Command-line activity using `reg.exe` or PowerShell registry cmdlets
- Autorun keys referencing LOLBINs or renamed executables

Consider pairing registry telemetry with process creation and network connection data to spot the full chain.
