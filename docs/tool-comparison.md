## Log Analysis Tool Comparison Overview

Three log-analysis tools were reviewed during the project:

- Windows Event Viewer
- KSystemLog
- Splunk

Each tool can support log review, but they differ in platform support, interface design, cost, monitoring capabilities, and intended scale.

## Comparison Table

| Feature | Windows Event Viewer | KSystemLog | Splunk |
|---|---|---|---|
| Primary platform | Windows | Linux | Multiple platforms |
| Interface | Graphical desktop application | Graphical desktop application | Web-style interface |
| Cost | Included with Windows | Free | Full capabilities can be expensive |
| Local log review | Yes | Yes | Yes |
| Centralized analysis | Limited without additional configuration | Primarily local | Yes |
| Filtering | Yes | Yes | Yes |
| Real-time monitoring | Requires refresh for updated views | Yes | Yes |
| Alerts | Limited compared with a SIEM | Not a primary feature | Yes |
| Dashboards | Limited | No enterprise dashboard focus | Yes |
| Long-term retention | Based on local configuration | Based on local configuration | Supported |
| Cross-platform use | No | No | Yes |
| Best suited for | Windows troubleshooting and local auditing | Readable Linux log review | High-volume enterprise monitoring |

## Windows Event Viewer

### Purpose

Windows Event Viewer is the built-in application used to view and navigate Windows event logs. It can search, filter, review, and export event records.

### Event Categories

The primary Windows log categories include:

- Application
- Security
- Setup
- System
- Forwarded Events

### Event Levels

Windows events may be classified as:

- Error
- Warning
- Information
- Success Audit
- Failure Audit

These levels help indicate the type and seriousness of an event.

### Strengths

Windows Event Viewer provides direct access to Windows logs without requiring additional software. Events can be filtered by date, event level, source, event ID, and other properties.

The event descriptions and task categories provide useful information for:

- System troubleshooting
- Security auditing
- Account-management review
- Application-error review
- PowerShell-event review

### Limitations

The interface can make detailed analysis time-consuming because individual events often need to be opened to view their full contents.

During the Windows script analysis, normal system events appeared alongside the script-generated activity. A custom time range helped narrow the results, but the exact sequence was less immediately visible than it was in KSystemLog.

### Best Use

Windows Event Viewer is most appropriate for:

- Local Windows troubleshooting
- Reviewing a limited time range
- Investigating known event IDs
- Examining security-auditing events
- Reviewing account and group changes

## KSystemLog

### Purpose

KSystemLog is a Linux graphical log viewer designed to make system logs easier to locate and understand.

It provides an alternative to reading logs entirely through terminal commands.

### Log Categories

KSystemLog can organize records into categories such as:

- Authentication
- Daemon
- Kernel
- System
- X.org
- Cron jobs
- Boot logs
- Apache

### Strengths

KSystemLog provides:

- A graphical interface
- Real-time monitoring
- Log categorization
- Priority-based highlighting
- Keyword filtering
- Visible timestamps and event descriptions
- The ability to email selected logs

Keyword searches can be used to locate terms such as:

```text
sudo
failed
```

The organized display made the Linux script activity easier to follow because multiple events could be reviewed without opening each one separately.

### Limitations

KSystemLog is limited to Linux systems and is primarily designed for local log review. It does not provide the same enterprise-level correlation, dashboard, and alerting features associated with a SIEM.

### Best Use

KSystemLog is most appropriate for:

- Linux system troubleshooting
- Reviewing authentication activity
- Monitoring local logs in real time
- Filtering for specific commands or keywords
- Viewing account and privilege changes in sequence

## Splunk

### Purpose

Splunk is a security information and event management platform that can search, monitor, index, and analyze machine-generated data.

It provides a centralized searchable repository and can generate:

- Graphs
- Reports
- Alerts
- Dashboards
- Visualizations

### Security Capabilities

Splunk can support the detection of:

- Brute-force activity
- Privilege escalation
- Lateral movement
- Data exfiltration

Role-based access control can also limit access to dashboards and sensitive log data.

### Strengths

Splunk provides:

- Centralized data collection
- Cross-platform support
- Real-time indexing
- Searchable log storage
- Real-time alerts
- Long-term retention
- Dashboard creation
- Data visualization
- Role-based access control

These capabilities make Splunk more suitable for large volumes of data and business environments.

### Limitations

Splunk can be expensive, especially as the amount of collected data increases. Its full capabilities may be unnecessary for an individual system or a small environment with a limited budget.

### Best Use

Splunk is most appropriate for:

- Enterprise security monitoring
- High-volume log collection
- Cross-platform environments
- Real-time alerting
- Centralized incident detection
- Long-term analysis and reporting

## Comparative Assessment

### Ease of Use

KSystemLog provided the clearest interface during the practical Linux analysis. Relevant activity was visible directly in the log list, making it easier to determine what occurred and when.

Windows Event Viewer required more navigation and event-by-event review. It remained useful for detailed Windows event information but was less transparent when separating script activity from background processes.

### Scalability

Splunk provides the greatest scalability because it can collect and index data from multiple systems. Windows Event Viewer and KSystemLog are more appropriate for local analysis.

### Cost and Accessibility

Windows Event Viewer is included with Windows, while KSystemLog is available without the enterprise costs associated with Splunk.

Splunk provides more advanced security-monitoring features, but its cost may make it less appropriate for smaller environments.

### Recommended Tool by Scenario

| Scenario | Recommended Tool |
|---|---|
| Reviewing Windows account events | Windows Event Viewer |
| Reviewing local Linux activity | KSystemLog |
| Searching Linux logs through the terminal | `journalctl` |
| Monitoring many systems | Splunk |
| Creating dashboards and alerts | Splunk |
| Working with a limited budget | Event Viewer or KSystemLog |
| Reviewing a high volume of cross-platform data | Splunk |
| Following a visible sequence of Linux events | KSystemLog |

## Conclusion

All three tools can support log file analysis.

Windows Event Viewer is useful for detailed Windows event review. KSystemLog provides an accessible and organized method for examining Linux logs. Splunk offers the strongest centralized monitoring, alerting, and visualization capabilities for larger environments.

For the practical activity in this project, KSystemLog provided the clearest view of script-generated changes. Splunk would be the stronger choice for high-volume enterprise data, while Windows Event Viewer remains necessary for built-in Windows event analysis.
