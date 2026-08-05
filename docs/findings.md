## Findings Overview

The log analysis identified account-management activity, password changes, privilege escalation, remote command execution, and evidence-cleanup behavior across Linux and Windows systems. These actions may be legitimate when authorized, but the same activity can indicate unauthorized access or system compromise when it occurs unexpectedly.

The Windows logs contained similar account activity but required closer filtering because script-generated events appeared alongside normal background events. The Linux logs provided a clear sequence of user and group changes.

## Windows Findings

### Account Creation and Enablement

The first Windows script created and enabled four accounts: 

- Elliot 
- Thomas
- Dade
- Tyler

Windows Event Viewer recorded User Account Management events associated with the account changes. The records showed account creation, account enablement, password resets, group enumeration, and additions to security-enabled local groups.

### Password Changes

Passwords were reset for the newly created accounts.

Unexpected password changes can indicate account takeover, unauthorized account preparation, or an attempt to establish access without using an existing user's credentials.

### Group Enumeration

The script checked the local group memberships and permissions associated with the newly created accounts.

Group enumeration may be part of normal administration, but it can also be used to identify available privileges and determine which groups provide administrative access.

### Administrator Privileges

Elliot and Thomas were assigned administrator privileges.

Unauthorized administrator assignments represent a serious security risk because the affected accounts may gain broad control over the Windows system.

### Blank Password Query

The second Windows script attempted to determine whether an account had a blank password.

Checking for blank passwords may be part of a security audit, but it can also be used to locate weak accounts that could be accessed without valid credentials.

### Remote Command Execution

Windows Event Viewer recorded multiple warnings associated with remote command execution.

Remote commands may be legitimate in managed environments. When they are unexpected, they can indicate that commands are being delivered from another system or executed through a remote-management mechanism.

### Encoded PowerShell Activity

The Windows logs contained a Base64-encoded PowerShell script. After decoding, the script was found to perform the following actions:

- Remove the users created by the first script
- Remove their local profiles
- Remove assigned privileges
- Clean up log data
- Clear PowerShell command history
- Exit after completing the cleanup

Encoded commands can make activity less readable during routine monitoring. Encoding alone does not confirm malicious intent, but encoded administrative commands should receive additional review when combined with account changes, remote execution, or evidence removal.

### Log and History Cleanup

The second Windows script cleaned up logs and cleared PowerShell history.

Log clearing and command-history removal can interfere with incident analysis. These actions are especially concerning when they occur after account creation, privilege escalation, or remote command execution.

## Linux Findings

### Account and Group Creation

The first Kali Linux script created the same four user accounts:

- Tyler
- Dade
- Elliot
- Thomas

A corresponding group was created for each account. Passwords were also changed after the accounts were created.

Account creation is not automatically malicious. However, unexpected accounts can provide persistent access to a system. New users should be compared against approved account requests, administrator activity, and system-change records.

### Privilege Escalation

Elliot and Thomas received elevated privileges through membership in the `sudo` group.

Unexpected membership in an administrative group is a significant security concern. An account with `sudo` access may execute commands with superuser privileges, modify system settings, access protected files, create additional accounts, or interfere with logging.

### Account and Group Removal

The second Kali Linux script removed Tyler, Dade, Elliot, and Thomas. Their associated groups were also deleted, and Elliot and Thomas were removed from the `sudo` group.

The removal activity reversed many of the changes made by the first script. Although account cleanup may be legitimate, rapid account creation followed by removal may indicate temporary unauthorized access or an attempt to reduce visible evidence.

### Script Deletion

The second Linux script deleted itself after completing its actions.

Self-deletion can be used as a cleanup technique. In an unauthorized incident, deleting the script would make it more difficult to determine exactly what commands were executed.

## Cross-Platform Findings

Several patterns appeared on both operating systems:

| Activity | Linux | Windows | Security Relevance |
|---|---:|---:|---|
| New account creation | Yes | Yes | May establish unauthorized access |
| Password changes | Yes | Yes | May prepare or take control of accounts |
| Privilege escalation | Yes | Yes | Provides administrative capabilities |
| Group changes | Yes | Yes | Alters account permissions |
| Account removal | Yes | Yes | May reverse changes or reduce evidence |
| Cleanup activity | Yes | Yes | May make reconstruction more difficult |
| Remote command warnings | Not identified | Yes | May indicate remote administration or intrusion |
| Encoded commands | Not identified | Yes | May conceal the purpose of a command |

## Primary Security Indicators

The most significant indicators identified during the analysis were:

1. Multiple new accounts created within a short period
2. Password changes immediately following account creation
3. Administrative privileges assigned to new accounts
4. Remote command execution warnings
5. Base64-encoded PowerShell content
6. Removal of accounts and profiles
7. Log cleanup
8. PowerShell history clearing
9. Script self-deletion

No single event proves that a system was compromised. The combination and timing of these events would justify further review when the activity was not approved.

## Analysis Outcome

The analysis demonstrated that logs can reconstruct account activity and reveal behavior associated with privilege escalation, remote execution, and evidence cleanup.

This project provided an example of what real world log analysis could look like and provided the opportunity to dive deeper into intrusion detection.
