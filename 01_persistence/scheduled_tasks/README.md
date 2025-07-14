# Scheduled Tasks

Scheduled tasks are a common persistence technique — built-in, flexible, and often overlooked. 
This folder focuses on how attackers use `schtasks.exe` to quietly maintain access and how those actions appear (or don’t) in Microsoft Defender for Endpoint (MDE).

---

## Technique at a Glance

`schtasks.exe` lets users create tasks triggered by time, startup, login, or other events.

Example:

    schtasks /create /SC DAILY /TN "Updater" /TR "C:\Temp\payload.exe"

Useful options:

    /S <system>        Remote system
    /U /P              Auth as a different user
    /RU /RP            Run task as specific user (e.g., SYSTEM)
    /SC                Trigger type (ONSTART, ONLOGON, etc.)

[Microsoft Learn – schtasks](https://learn.microsoft.com/en-us/windows/win32/taskschd/schtasks)

---

## Detection Focus

Each test covers:

- Commands used
- Artifacts created
- MDE (or host) visibility
- Suggested remediations

> Built-in tools are only safe until they’re not.
