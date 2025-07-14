# Command and Control (C2)  
**MITRE ATT&CK Reference:** [TA0011 – Command and Control](https://attack.mitre.org/tactics/TA0011/)

Once adversaries gain a foothold, they need a way to communicate with the compromised system. This is where Command and Control (C2) comes in. 
A critical stage where attackers establish a persistent, often covert, communication channel between their infrastructure and the target environment.

C2 channels allow attackers to issue commands, deploy additional tooling, exfiltrate data, and maintain access even across reboots or user sessions. 
What makes C2 so dangerous is its adaptability: attackers regularly blend in with legitimate traffic, use built-in tools (LOLBins), encrypt their communication, or rely on trusted services to evade detection.

Well-known groups like **APT29**, **FIN7**, and **Lazarus Group** have all leveraged stealthy C2 techniques — but the creativity doesn’t stop there:

- **Discord as a C2 channel** – Malware families like *Abaddon* and *BrushaLoader* have embedded Discord webhooks and APIs into their payloads, turning a common chat platform into a full-featured C2 system.
  Since Discord traffic blends in with normal user behavior, it often evades both proxies and endpoint controls.

- **Steganography in social media** – Some variants of *Zebrocy* malware (used by APT28) retrieved C2 commands hidden inside images posted to public social media profiles.
  The payload decoded commands from embedded pixels, bypassing network controls and leaving no traditional indicators behind.

- **Living off Google Sheets** – Threat actors have been seen using Google Sheets as a C2 panel, where infected hosts poll a shared spreadsheet for commands and upload results as cell entries.
  Since the traffic is encrypted and directed to a trusted domain (`*.google.com`), it easily bypasses most filtering and logging tools.


> **Bottom line: Advanced C2 is subtle.**  

In this section, we explore how adversaries stage and execute payloads, interact with infected systems, and mask their outbound communication. Each test demonstrates realistic attacker tradecraft that prioritizes stealth and persistence over brute-force or flashy techniques.

> **Why it matters**  
> If you can detect C2, you can stop the operation before impact. But if you miss it, everything else (lateral movement, data theft, ransomware) becomes fair game.

---

📂 Each subfolder in this section maps to a specific C2 technique or tool, aligned to a real-world MITRE technique ID.
