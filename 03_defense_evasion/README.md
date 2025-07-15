# Defense Evasion

**MITRE ATT&CK Tactic:** [TA0005 – Defense Evasion](https://attack.mitre.org/tactics/TA0005/)

Threat actors frequently leverage trusted system utilities, manipulate policy settings, and abuse native features to operate without triggering alerts. 
These tactics are not fringe, they’re foundational. Across both targeted intrusions and commodity malware campaigns, disabling or modifying defenses is often one of the first actions post-access.

### Common Techniques in the Wild

Research across real-world incidents shows consistent patterns:
- Tampering with endpoint protection using built-in PowerShell cmdlets
- Adding file, folder, or process exclusions to AV engines
- Leveraging LOLBins like `rundll32.exe`, `regsvr32.exe`, and `mshta.exe` to execute code while evading signature-based defenses
- Masquerading malware as legitimate binaries to blend into routine system activity

These behaviors are rarely detected in isolation. They’re quiet, often logged but not alerted on, and typically paired with follow-up actions like credential access or persistence.

### What This Folder Covers

This folder documents realistic scenarios where adversaries evade detection using techniques validated in threat intelligence and post-incident analysis. 
Each scenario maps to MITRE ATT&CK and includes observable behaviors, detection logic, and analyst takeaways.
