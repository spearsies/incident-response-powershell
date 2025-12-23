# PowerShell Digital Forensics & Incident Response (DFIR) Toolkit

[![License](https://img.shields.io/badge/License-BSD_3--Clause-blue.svg)](https://opensource.org/licenses/BSD-3-Clause)
[![PowerShell](https://img.shields.io/badge/PowerShell-5.1%2B-blue.svg)](https://github.com/PowerShell/PowerShell)
[![Platform](https://img.shields.io/badge/Platform-Windows-lightgrey.svg)](https://www.microsoft.com/windows)

A comprehensive collection of PowerShell scripts designed for digital forensics and incident response operations on Windows systems. This toolkit enables security teams to rapidly collect forensic artifacts, analyze indicators of compromise, and contain active threats during security incidents.

## 🎯 Overview

This repository provides battle-tested PowerShell scripts for the complete incident response lifecycle. Whether you're conducting forensic triage, hunting for threats, or containing an active incident, these scripts help you work efficiently and systematically.

**Key Capabilities:**
- **Rapid Evidence Collection**: Gather 25+ forensic artifacts in minutes
- **SIEM Integration**: Export all findings as CSV for centralized analysis
- **Microsoft Defender Integration**: Native support for Live Response sessions
- **Modular Design**: Use the full DFIR script or granular response modules
- **Production Ready**: Tested in enterprise security operations environments

## 📋 Table of Contents

- [Features](#-features)
- [Quick Start](#-quick-start)
- [DFIR Script](#-dfir-script)
- [Granular Response Scripts](#-granular-response-scripts)
- [SIEM Integration](#-siem-integration)
- [Defender for Endpoint Integration](#-defender-for-endpoint-integration)
- [Usage Examples](#-usage-examples)
- [Collected Artifacts](#-collected-artifacts)
- [Requirements](#-requirements)
- [Contributing](#-contributing)
- [License](#-license)
- [Acknowledgments](#-acknowledgments)

## ✨ Features

### Core DFIR Script
- **Automated Evidence Collection**: Collects 25+ forensic artifacts automatically
- **Structured Output**: Organizes findings in timestamped folders
- **CSV Export**: All artifacts exported for SIEM ingestion (Sentinel, Splunk, Elastic, ADX)
- **Compression**: Automatically zips collected evidence for secure transfer
- **Admin Detection**: Enhanced collection when running with administrative privileges
- **Live Response Ready**: Optimized for Microsoft Defender for Endpoint integration

### Granular Response Modules
Scripts organized by incident response phase:

| Phase | Purpose | Scripts |
|-------|---------|---------|
| **Acquisition** | Evidence collection and preservation | Data acquisition scripts |
| **Analysis** | IOC identification and scope assessment | Analysis and hunting scripts |
| **Containment** | Threat mitigation and damage control | Containment action scripts |

## 🚀 Quick Start

### Basic Usage

```powershell
# Standard execution (current user privileges)
.\DFIR-Script.ps1

# Recommended: Run as Administrator for full artifact collection
PowerShell.exe -ExecutionPolicy Bypass .\DFIR-Script.ps1
```

### Output Structure

The script creates a timestamped folder containing all collected artifacts:

```
DFIR-HOSTNAME-2024-12-22/
├── CSV Results (SIEM Import Data)/
│   ├── ActiveUsers.csv
│   ├── Processes.csv
│   ├── SecurityEvents.csv
│   └── [20+ additional CSV files]
├── PowerShell_History/
├── Browser_Data/
└── System_Info/
```

## 🔍 DFIR Script

### What Gets Collected

#### Standard User Artifacts (No Admin Required)
- Network configuration and active connections
- Process listings with command-line arguments
- Autorun locations (Registry Run keys, Startup folder)
- Active user sessions and local user accounts
- Office application network connections
- SMB shares and RDP sessions
- USB device history
- PowerShell command history (current user)
- DNS cache entries
- Installed drivers and software
- Running services
- Scheduled tasks
- Browser history and profiles (Chrome, Edge, Firefox)

#### Enhanced Collection (Administrator Required)
- **Windows Security Events**: Critical security audit logs
- **Remotely Opened Files**: Active network file access
- **Shadow Copies**: Volume snapshot information
- **Microsoft Defender Logs**: Protection history and scan results
- **Defender Exclusions**: Configured AV exceptions
- **All User PowerShell History**: Command history for all accounts

### Script Parameters

```powershell
# Collect only security events from the last 10 days
.\DFIR-Script.ps1 -sw 10

# Custom output directory
.\DFIR-Script.ps1 -OutputPath "C:\IR\Evidence"
```

## 📂 Granular Response Scripts

### Acquisition Scripts
Located in `/Acquisition/` - Scripts for collecting specific artifacts:
- Event log collection
- Memory acquisition helpers
- Registry extraction
- File system enumeration

### Analysis Scripts  
Located in `/Analysis/` - Tools for analyzing collected data:
- Timeline generation
- IOC matching
- Suspicious pattern detection
- Correlation analysis

### Containment Scripts
Located in `/Containment/` - Active response capabilities:
- Process termination
- Network isolation
- User session management
- Firewall rule deployment

## 📊 SIEM Integration

All forensic artifacts are exported as CSV files for seamless integration with security platforms:

### Supported Platforms
- **Microsoft Sentinel**: Azure-native SIEM integration
- **Splunk**: Universal Forwarder ingestion
- **Elastic Security**: Filebeat collection
- **Azure Data Explorer**: Direct CSV import

### CSV Output Files

```
CSV Results (SIEM Import Data)/
├── ActiveUsers.csv
├── AutoRun.csv
├── ConnectedDevices.csv
├── DefenderExclusions.csv
├── DNSCache.csv
├── Drivers.csv
├── InstalledSoftware.csv
├── IPConfiguration.csv
├── LocalUsers.csv
├── NetworkShares.csv
├── OfficeConnections.csv
├── OpenTCPConnections.csv
├── PowerShellHistory.csv
├── Processes.csv
├── RDPSessions.csv
├── RemotelyOpenedFiles.csv
├── RunningServices.csv
├── ScheduledTasks.csv
├── ScheduledTasksRunInfo.csv
├── SecurityEvents.csv
├── ShadowCopy.csv
└── SMBShares.csv
```

### Example: Import to Microsoft Sentinel

```powershell
# Upload CSV to Log Analytics workspace
$WorkspaceId = "your-workspace-id"
$SharedKey = "your-shared-key"
$LogType = "DFIR_Artifacts"

$CSVFiles = Get-ChildItem ".\CSV Results (SIEM Import Data)\*.csv"
foreach ($File in $CSVFiles) {
    $CSVData = Import-Csv $File.FullName
    # Send to Log Analytics
    Send-AzMonitorCustomLog -WorkspaceId $WorkspaceId -SharedKey $SharedKey `
        -LogType $LogType -JsonPayload ($CSVData | ConvertTo-Json)
}
```

## 🛡️ Defender for Endpoint Integration

### Prerequisites

1. **Enable Live Response**: Navigate to Security.microsoft.com → Settings → Endpoints → Advanced Features
2. **Enable Unsigned Scripts** (if needed): Enable "Live Response unsigned script execution"
3. **Upload to Library**: Upload DFIR-Script.ps1 to your Live Response script library

### Live Response Execution

```powershell
# 1. Initiate Live Response session on target device

# 2. Run the DFIR script
run DFIR-Script.ps1

# 3. Run with parameters (e.g., last 10 days of security events)
run DFIR-Script.ps1 -parameters "-sw 10"

# 4. Download collected evidence
getfile DFIR-HOSTNAME-2024-12-22.zip
```

### Benefits of Live Response Integration
- **Remote Collection**: Gather evidence from endpoints without physical access
- **Rapid Response**: Deploy across multiple devices simultaneously
- **Audit Trail**: All actions logged in Defender for Endpoint
- **Secure Transfer**: Evidence retrieved through encrypted channels

### Documentation Links
- [Microsoft Defender Live Response Documentation](https://docs.microsoft.com/en-us/microsoft-365/security/defender-endpoint/live-response)
- [Live Response Advanced Features](https://docs.microsoft.com/en-us/microsoft-365/security/defender-endpoint/advanced-features#live-response)
- [User Roles and Permissions](https://docs.microsoft.com/en-us/microsoft-365/security/defender-endpoint/user-roles)

## 💡 Usage Examples

### Scenario 1: Suspected Malware Infection

```powershell
# Run full DFIR collection as Administrator
PowerShell.exe -ExecutionPolicy Bypass .\DFIR-Script.ps1

# Review suspicious processes
Import-Csv ".\DFIR-HOSTNAME-2024-12-22\CSV Results\Processes.csv" | 
    Where-Object {$_.CommandLine -like "*powershell*" -or $_.CommandLine -like "*cmd*"} |
    Select-Object ProcessName, CommandLine, ParentProcess
```

### Scenario 2: Persistence Mechanism Hunting

```powershell
# Examine all autorun locations
$AutoRuns = Import-Csv ".\DFIR-HOSTNAME-2024-12-22\CSV Results\AutoRun.csv"
$AutoRuns | Where-Object {$_.Path -notlike "*Microsoft*" -and $_.Path -notlike "*Windows*"}

# Check scheduled tasks
$Tasks = Import-Csv ".\DFIR-HOSTNAME-2024-12-22\CSV Results\ScheduledTasks.csv"
$Tasks | Where-Object {$_.Author -ne "Microsoft Corporation"}
```

### Scenario 3: Network Reconnaissance

```powershell
# Identify suspicious network connections
$Connections = Import-Csv ".\DFIR-HOSTNAME-2024-12-22\CSV Results\OpenTCPConnections.csv"
$Connections | Where-Object {$_.State -eq "ESTABLISHED" -and $_.RemotePort -notin @(80,443)}

# Review DNS cache for potential C2 domains
$DNS = Import-Csv ".\DFIR-HOSTNAME-2024-12-22\CSV Results\DNSCache.csv"
$DNS | Select-Object Entry, Data
```

## 📦 Collected Artifacts

### Network Artifacts
- Local IP configuration (IPv4/IPv6, DNS servers, gateways)
- Active TCP/UDP connections with process association
- DNS cache entries
- SMB shares (local and remote)
- Network file shares with access permissions

### Process & Execution Artifacts
- Running processes with full command-line arguments
- Parent-child process relationships
- Process network connections
- Loaded DLLs and modules
- Running services with configurations

### Persistence Mechanisms
- Registry Run keys (HKLM and HKCU)
- Startup folder contents
- Scheduled tasks with triggers and actions
- Service configurations
- WMI event subscriptions

### User Activity
- Active user sessions
- RDP session history
- PowerShell command history (all users when admin)
- Browser history (Chrome, Edge, Firefox)
- Recently accessed files
- USB device connection history

### Security Configuration
- Windows Security Event logs
- Microsoft Defender scan history
- Defender exclusions and settings
- Firewall rules
- Local user accounts and group memberships
- Security audit policies

### System Information
- Installed software and versions
- Installed drivers
- System hardware details
- Volume shadow copy information
- Windows update history

## 🔧 Requirements

### System Requirements
- **Operating System**: Windows 7/Server 2008 R2 or later
- **PowerShell**: Version 5.1 or higher (pre-installed on Windows 10/Server 2016+)
- **Disk Space**: ~100MB for typical artifact collection
- **Execution Policy**: May require `-ExecutionPolicy Bypass` for unsigned scripts

### Permissions
- **Standard User**: Collects 20+ artifacts
- **Administrator**: Full artifact collection (recommended)
  - Security Event logs
  - All user PowerShell history
  - Defender configurations
  - System-level artifacts

### Network Requirements (for Defender Integration)
- Microsoft Defender for Endpoint active on device
- Connectivity to security.microsoft.com
- Live Response feature enabled

## 🤝 Contributing

Contributions are welcome! Whether you're fixing bugs, adding new collection modules, or improving documentation, your help makes this toolkit better for the entire security community.

### How to Contribute

1. **Fork the Repository**
   ```bash
   git clone https://github.com/spearsies/incident-response-powershell.git
   cd incident-response-powershell
   ```

2. **Create a Feature Branch**
   ```bash
   git checkout -b feature/your-feature-name
   ```

3. **Make Your Changes**
   - Add new collection scripts to appropriate folders (Acquisition/Analysis/Containment)
   - Follow existing code style and documentation patterns
   - Test thoroughly on Windows 10/11 and Server 2019/2022

4. **Document Your Changes**
   - Update README.md if adding new features
   - Add inline comments for complex logic
   - Include usage examples

5. **Submit a Pull Request**
   - Provide clear description of changes
   - Reference any related issues
   - Include testing details

### Contribution Guidelines

- **Code Quality**: Follow PowerShell best practices and style guides
- **Testing**: Verify scripts work with both standard and administrative privileges
- **Documentation**: Update docs for any new features or changes
- **Security**: Never include credentials, API keys, or sensitive data

See [CONTRIBUTORS.md](CONTRIBUTORS.md) for a list of people who have contributed to this project.

## 📄 License

This project is licensed under the BSD 3-Clause License - see the [LICENSE](LICENSE) file for details.

### BSD 3-Clause License Summary
- ✅ Commercial use
- ✅ Modification
- ✅ Distribution
- ✅ Private use
- ❌ Liability
- ❌ Warranty

## 🙏 Acknowledgments

This repository is a fork of the excellent work by [Bert-JanP](https://github.com/Bert-JanP/Incident-Response-Powershell), whose original DFIR scripts have been invaluable to the security community.

### Related Resources

**Blog Articles:**
- [Incident Response Part 3: Leveraging Live Response](https://kqlquery.com/posts/leveraging-live-response/)
- [Incident Response PowerShell V2](https://kqlquery.com/posts/incident-response-powershell-v2/)

**Complementary Tools:**
- [KAPE](https://www.kroll.com/en/services/cyber-risk/incident-response-litigation-support/kroll-artifact-parser-extractor-kape) - Kroll Artifact Parser and Extractor
- [Velociraptor](https://docs.velociraptor.app/) - Advanced DFIR platform
- [PowerForensics](https://github.com/Invoke-IR/PowerForensics) - PowerShell digital forensics framework

### Community

- **Issues**: Report bugs or request features via [GitHub Issues](https://github.com/spearsies/incident-response-powershell/issues)
- **Discussions**: Share use cases and ask questions in [Discussions](https://github.com/spearsies/incident-response-powershell/discussions)
- **Security**: For security concerns, see [SECURITY.md](SECURITY.md)

---

**⚡ Built for incident responders, by incident responders.**

If this toolkit helps you respond to incidents more effectively, consider giving it a ⭐ star!
