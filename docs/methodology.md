## Project Methodology

### 1. Review Windows Logging

Windows logging was reviewed to understand how events are organized and stored.

Windows commonly stores event logs as `.evtx` files in:

```text
C:\WINDOWS\system32\winevt\Logs\
```

The primary Windows log categories examined were:

- Application
- Security
- Setup
- System
- Forwarded Events

Event levels and event IDs were considered when identifying records that could be important to security analysis.

### 2. Review Linux Logging

Linux logging was reviewed through `systemd-journald` and `journalctl`.

The journal stores structured logging data received from the kernel, system services, user processes, standard input, and standard error. Because journal data is stored in a binary/ format, `journalctl` is used to display the records in a terminal.

Linux priority levels reviewed during the project included:

- Emergency
- Alert
- Critical
- Error
- Warning
- Notice
- Informational
- Debug

### 3. Compare Analysis Tools

Windows Event Viewer, KSystemLog, and Splunk were compared according to:

- Supported operating systems
- Interface design
- Filtering capabilities
- Event organization
- Real-time monitoring
- Alerting
- Accessibility
- Cost
- Suitability for local or enterprise use

This comparison helped determine which tool was most effective for each part of the exercise.

### 4. Execute the First Linux Script

The first Kali Linux script was executed with:

```bash
sudo ./lab3s3.sh
```

The desktop script file disappeared after execution, while the terminal remained open. The resulting Linux logs were reviewed to identify user creation, group creation, password changes, and privilege assignments.

### 5. Execute the Second Linux Script

The second Kali Linux script was executed with:

```bash
sudo ./lab3s4.sh
```

The logs were reviewed for account deletion, group deletion, removal of elevated privileges, and script cleanup.

### 6. Review Linux Events in KSystemLog

KSystemLog was used to follow the sequence of Linux events.

The visible timestamps, categories, and event descriptions made it possible to connect the script execution with:

- User creation
- Group creation
- Password changes
- `sudo` group changes
- User deletion
- Group deletion
- Script removal

### 7. Execute and Isolate Windows Activity

After the Windows scripts were executed, a custom Event Viewer view was created around the execution time.

The first script was isolated using a time range beginning approximately one minute after execution. Relevant records were reviewed by source, event ID, task category, and event details.

### 8. Correlate Windows Account Events

The Windows events were placed into a sequence that included:

1. PowerShell console preparation
2. Account creation
3. Account enablement
4. Password resets
5. Permission changes
6. Local group enumeration
7. Additions to security-enabled groups
8. Administrator assignments

User Account Management events were used to identify the account and group changes.

### 9. Review the Second Windows Script

The second Windows script generated warnings related to remote command execution.

The event details contained Base64-encoded PowerShell content. The encoded content was decoded so that the commands and their purpose could be reviewed.

### 10. Evaluate Security Significance

Each event was considered in relation to whether it could be expected administrative behavior or a possible sign of compromise.

The primary questions used during the evaluation were:

- Was a new account created?
- Was a password changed?
- Were privileges increased?
- Was the account added to an administrative group?
- Was a command executed remotely?
- Was a command encoded?
- Were logs or command histories cleared?
- Were accounts, profiles, or scripts removed afterward?

Events were treated as possible indicators rather than proof of malicious activity. Authorization and surrounding context would be required for a final determination.

## Platform-Specific Approach

### Windows

Windows activity was reviewed through custom Event Viewer views.

The analysis focused on:

- PowerShell events
- Microsoft Windows security auditing
- User Account Management
- Local group changes
- Remote command warnings
- Encoded PowerShell
- Cleanup activity

### Linux

Linux activity was reviewed primarily through KSystemLog because it displayed the relevant events in an organized and readable sequence.

The analysis focused on:

- `sudo` activity
- User-management events
- Group-management events
- Password changes
- Privilege assignments
- Account deletion
- Script deletion

## Limitations

The Windows analysis was more difficult because Event Viewer displayed script-related records alongside unrelated background activity. Creating a narrow custom time range reduced the number of events but did not completely separate the script activity.

The Linux script file disappeared after execution, and the terminal did not close. Successful execution was determined through the changes visible in the logs rather than through a separate completion message.

No network captures, memory images, endpoint alerts, or external log sources were included. Conclusions were limited to the events shown in the provided system logs.

## Evidence Mapping

| Evidence File | Purpose |
|---|---|
| `windows-log-categories.png` | Shows the primary Windows log categories |
| `windows-event-viewer.png` | Shows Windows event IDs and event details |
| `linux-journalctl.png` | Shows Linux journal output |
| `linux-ksystemlog.png` | Shows the KSystemLog interface |
| `linux-account-creation.png` | Shows Linux user and group creation activity |
| `linux-account-removal.png` | Shows Linux user and group removal activity |
| `windows-account-events.png` | Shows Windows account-management events |
| `windows-cleanup-events.png` | Shows warnings and cleanup-related events |
| `encoded-powershell.png` | Shows the encoded PowerShell content |
