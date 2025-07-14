# Ingress Tool Transfer

**MITRE ATT&CK Technique:** [T1105 – Ingress Tool Transfer](https://attack.mitre.org/techniques/T1105/)

Attackers don’t bring their full toolkit through the front door. They sneak it in *after* they’ve got a foothold.

T1105 refers to the act of transferring tools, payloads, or scripts from an external system into a compromised environment. This is often one of the earliest steps in post-compromise activity—and one of the most overlooked by defenders.

### Why It Matters

Red teams do it. Ransomware crews do it. Nation-state APTs do it.

In the 2020 SolarWinds breach, the attackers used legitimate tools like `certutil.exe` to quietly pull second-stage payloads onto victim systems. 
In other incidents, `bitsadmin`, `curl`, or even Google Drive links have been used to deliver custom malware. These transfers often masquerade as harmless downloads or blend in with normal web traffic.

If you're only alerting on known malware hashes, you're already behind.

### What to Look For

- Built-in LOLBINs like `certutil`, `bitsadmin`, `powershell Invoke-WebRequest`, or `curl` making external calls.
- Inbound traffic delivering `.ps1`, `.exe`, `.dll`, or `.zip` files from suspicious domains.
- Downloads immediately followed by execution (especially via scripting engines).

This folder includes scenarios, scripts, and detection examples to learn about and respond to this key technique.  

> Treat every download as a potential pivot point for a full compromise.
