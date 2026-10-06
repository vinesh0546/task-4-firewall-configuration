# Task 4 – Setup and Use a Firewall on Windows

## Objective
Configure and test a basic Windows Firewall rule to block inbound traffic on TCP port 23 (Telnet).

## Tools Used
- Windows Defender Firewall with Advanced Security
- Windows Command Prompt / PowerShell

## Task Performed

### 1. Checked Windows Firewall
Verified that Windows Defender Firewall was enabled. The active firewall configuration showed inbound connections that do not match a rule are blocked.

### 2. Checked Existing Inbound Rules
Opened **Inbound Rules** in Windows Defender Firewall with Advanced Security and reviewed the existing rules without modifying them.

### 3. Created a Port 23 Block Rule
Created the following inbound firewall rule:

- **Rule Name:** Block Telnet Port 23
- **Direction:** Inbound
- **Protocol:** TCP
- **Local Port:** 23
- **Remote Port:** Any
- **Action:** Block
- **Profile:** Any
- **Enabled:** True

### 4. Tested Port 23
Used the following command:

```powershell
Test-NetConnection 127.0.0.1 -Port 23
```

The test returned:

```text
TcpTestSucceeded : False
```

This demonstrated that a TCP connection to port 23 was unsuccessful. The firewall rule configuration was separately verified using PowerShell.

### 5. Verified Firewall Rule
The rule was verified with:

```powershell
Get-NetFirewallRule -DisplayName "Block Telnet Port 23" | Format-List DisplayName,Enabled,Direction,Action,Profile
```

Port configuration was verified with:

```powershell
Get-NetFirewallRule -DisplayName "Block Telnet Port 23" | Get-NetFirewallPortFilter | Format-List Protocol,LocalPort,RemotePort
```

The verification confirmed that the rule was enabled, inbound, blocking, and configured for TCP local port 23.

### 6. Cleanup
After testing and collecting evidence, the temporary **Block Telnet Port 23** rule was deleted to restore the previous firewall configuration.

## Evidence

Screenshots included in this repository:

1. `01-firewall-overview.png` – Windows Defender Firewall overview.
2. `02-inbound-rules.png` – Existing inbound firewall rules.
3. `03-rule-created.png` – Block Telnet Port 23 rule.
4. `04-port23-test.png` – Test-NetConnection result showing TCP connection unsuccessful.
5. `05-rule-verification.png` – PowerShell verification of the firewall rule and TCP port 23 configuration.

## Key Concepts
- Firewall configuration
- Inbound and outbound traffic
- Network ports
- TCP
- Windows Defender Firewall
- Traffic filtering
- Telnet port 23

## Conclusion
A temporary Windows Firewall inbound rule was successfully configured to block TCP port 23, tested, verified using PowerShell, and then removed after testing to restore the original system state.
