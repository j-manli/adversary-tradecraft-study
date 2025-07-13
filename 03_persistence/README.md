# Persistence

Persistence techniques give attackers a reliable way back into a system, even after reboots, logouts, or cleanup attempts. These methods often rely on legitimate OS features to stay hidden and operational.

This section explores commonly abused persistence mechanisms, how they behave in real environments, and what they look like from a defender’s perspective. 
Some examples are tested in Microsoft Defender for Endpoint (MDE), while others use a home lab (AD) setup.

Each scenario is mapped to MITRE ATT&CK, includes detection opportunities, and focuses on how defenders can identify, investigate, and respond.

## What You'll Find Here

- **Registry Run Keys**  
  Used by groups like APT29 to launch malware on user login.  
  ↳ *[T1547.001](https://attack.mitre.org/techniques/T1547/001/)*

- **Startup Folder Executables**  
  A low-effort, high-success tactic still seen in modern malware.  
  ↳ *[T1547.009](https://attack.mitre.org/techniques/T1547/009/)*

- **Scheduled Tasks**  
  Used for both persistence and evasion. Think APT41, ransomware, and beyond.  
  ↳ *[T1053.005](https://attack.mitre.org/techniques/T1053/005/)*

- **Windows Services**  
  Adversaries can hijack or install services to run code at startup.  
  ↳ *[T1543.003](https://attack.mitre.org/techniques/T1543/003/)*

- **WMI Event Subscriptions**  
  Fileless, stealthy, and still favored by attackers who want to stay quiet.  
  ↳ *[T1546.003](https://attack.mitre.org/techniques/T1546/003/)*

- **DLL Sideloading & Hijacking**  
  Popular with groups like Lazarus to slip malicious code into trusted apps.  
  ↳ *[T1574.002](https://attack.mitre.org/techniques/T1574/002/)*

As testing continues, more examples and hunting insights will be added. 
Each one maps to MITRE, includes real telemetry (when available), and aims to build instincts you'd use on the job.
