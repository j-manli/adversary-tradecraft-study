# Startup Folder Persistence

Dropping a file into the Windows Startup folder is one of the oldest tricks in the book (but it still works). 
When a user logs in, anything inside this folder executes automatically, no special permissions or exploits required.

MITRE ATT&CK Reference: [T1547.009 – Shortcut Modification (Startup Folder)](https://attack.mitre.org/techniques/T1547/009/)

---

## How It Works

Windows checks specific folders during user login and runs any executables, scripts, or links it finds there.

| Scope       | Folder Path                                                                 |
|-------------|------------------------------------------------------------------------------|
| Per-User    | `C:\Users\<Username>\AppData\Roaming\Microsoft\Windows\Start Menu\Programs\Startup` |
| All Users   | `C:\ProgramData\Microsoft\Windows\Start Menu\Programs\Startup`              |

Attackers can abuse this by placing a malicious `.exe`, `.bat`, `.vbs`, or shortcut in one of these locations. The next time the user logs in, the payload silently runs.

---

## Why Attackers Use It

- **No Exploits Needed** – Just file copy access
- **Survives Reboot** – Triggers every logon
- **Blends In** – Legit apps use it too
- **Low Alert Fatigue** – Often overlooked in noisy environments

APT29 and FIN7 have used this technique in real-world campaigns for post-exploitation persistence, especially when trying to maintain user-context access without tripping admin-level alarms.

---

## Detection Ideas

Security products are great...but not perfect. Some things to check:

- Monitoring for new or modified `.exe`/`.lnk` files in known Startup directories
- Correlating logon events with unexpected binary execution
- Watching for suspicious file paths (e.g., `C:\ProgramData\...`) that don't match standard app installs
- Flagging renamed binaries or LOLBIN abuse within Startup folders

---

## Related Write-Ups

- [WindowsTelemetryService: Startup Folder Persistence (Sliver C2)](https://github.com/j-manli/adversary-tradecraft-study/blob/main/03_persistence/startup_folder/T1547.009_startupfolder_C2_sliver.md)

---
