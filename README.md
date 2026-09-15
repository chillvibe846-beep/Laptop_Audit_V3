# 💻 Laptop Audit – Final V3

### Professional Windows IT Asset Management & Device Health Assessment

A PowerShell-based Windows laptop and desktop auditing tool designed to collect hardware specifications, operating system details, security configuration, network information, battery health, and installed software inventory.

The project generates structured CSV reports and human-readable TXT reports for IT asset management, maintenance records, device verification, and hardware assessment.

> **Project Status:** Final V3 — Functional prototype / pre-production
> **Platform:** Windows 10 and Windows 11
> **Language:** PowerShell
> **Execution:** PowerShell as Administrator recommended
> **License:** To be defined by the repository owner

---

## 📌 Table of Contents

1. [Overview](#-overview)
2. [Why This Project Exists](#-why-this-project-exists)
3. [Project Goals](#-project-goals)
4. [Key Features](#-key-features)
5. [How the Audit Works](#-how-the-audit-works)
6. [What Information Is Collected](#-what-information-is-collected)
7. [What Is Not Collected](#-what-is-not-collected)
8. [Project Structure](#-project-structure)
9. [Requirements](#-requirements)
10. [Before Running the Script](#-before-running-the-script)
11. [Installation](#-installation)
12. [How to Run](#-how-to-run)
13. [How to Use on Another Computer](#-how-to-use-on-another-computer)
14. [Generated Reports](#-generated-reports)
15. [Understanding the Report](#-understanding-the-report)
16. [Privacy and Security Policy](#-privacy-and-security-policy)
17. [Data Protection Rules](#-data-protection-rules)
18. [Important Technical Limitations](#-important-technical-limitations)
19. [Troubleshooting](#-troubleshooting)
20. [Safe Production Improvements](#-safe-production-improvements)
21. [Recommended Repository Workflow](#-recommended-repository-workflow)
22. [Testing Checklist](#-testing-checklist)
23. [Disclaimer](#-disclaimer)
24. [License](#-license)

---

# 📖 Overview

**Laptop Audit – Final V3** is a Windows system auditing script written in PowerShell.

It collects information from the computer on which it is executed and creates an audit report containing hardware, software, Windows, security, network, and device information.

The script is designed for use in:

* Office IT asset management.
* Laptop maintenance and service records.
* Desktop and laptop hardware verification.
* Windows device inventory.
* System health assessment.
* IT support and troubleshooting.
* Device handover documentation.
* Hardware upgrade planning.
* Internal technical documentation.

### Example use case

An IT administrator receives a laptop for maintenance.

Instead of manually checking every specification, the administrator runs the audit script.

The script collects available system information and creates reports such as:

```text
Laptop_Audit_Reports/
│
├── Laptop_Audit_GEPL-Maintenance_20260915_141118.csv
├── Laptop_Audit_GEPL-Maintenance_20260915_141118.txt
└── Installed_Software_GEPL-Maintenance_20260915_141118.csv
```

These reports can be reviewed, archived, or used as a starting point for an IT asset register.

---

# 🎯 Why This Project Exists

Manual laptop auditing is time-consuming and can lead to incomplete or inconsistent records.

An administrator may need to check:

* Manufacturer and model.
* Serial number.
* Processor and RAM.
* Storage capacity.
* Windows version.
* TPM and Secure Boot.
* BitLocker status.
* Firewall and Defender.
* Network configuration.
* Battery health.
* Installed software.

This project automates the collection of these details into a repeatable report.

### Benefits

| Traditional manual audit | Laptop Audit V3               |
| ------------------------ | ----------------------------- |
| Manual checking          | Automated collection          |
| Different formats        | Structured CSV output         |
| Repeated work            | Reusable PowerShell script    |
| Easy to miss details     | Multiple inventory categories |
| Difficult to compare     | Reports can be compared       |
| Manual software listing  | Software inventory CSV        |

**Important:** Automation improves consistency, but it does not guarantee that every field is available or accurate on every Windows computer.

---

# 🚀 Project Goals

## Primary goals

1. Collect hardware specifications.
2. Collect Windows operating system information.
3. Collect security configuration details.
4. Collect battery information when supported.
5. Collect installed software inventory.
6. Generate CSV and TXT reports.
7. Use a friendly asset name without renaming Windows.
8. Provide a repeatable audit workflow.
9. Avoid collecting passwords or BitLocker recovery keys.
10. Keep the project suitable for professional IT documentation.

## Future goals

* Better Windows 7 compatibility.
* Improved battery health detection.
* Storage health and SMART information.
* More reliable Office / Microsoft 365 detection.
* Secure report storage.
* Device comparison.
* Centralized inventory management.
* HTML reports.
* Optional redaction of sensitive fields.
* Automated testing.
* Production-grade error handling.

---

# ✨ Key Features

### 🖥 Hardware Inventory

* Manufacturer.
* Model.
* BIOS serial number.
* Processor name.
* CPU cores.
* CPU threads.
* Maximum CPU speed.
* Total RAM.
* RAM type.
* RAM module count.
* Physical storage capacity.
* Storage model.
* Storage serial.
* Logical storage capacity.
* Free storage.
* GPU.
* Monitor information.

### 🪟 Windows Inventory

* Windows edition.
* Windows version.
* Windows build.
* OS architecture.
* Windows activation status.
* Windows computer name.
* Last boot time.
* Latest hotfix date.

### 🔐 Security Assessment

* TPM presence.
* TPM readiness.
* TPM manufacturer version.
* Secure Boot status.
* BitLocker status.
* BitLocker encryption percentage.
* Microsoft Defender status.
* Real-time protection status.
* Windows Firewall status.

### 🌐 Network Inventory

* Wi-Fi IP address.
* Wi-Fi MAC address.
* Ethernet IP address.
* Ethernet MAC address.
* Bluetooth detection.

### 🔋 Battery Inventory

* Battery status.
* Design capacity.
* Full charge capacity.
* Estimated battery health.

### 📦 Software Inventory

The script attempts to collect installed software from Windows uninstall registry locations.

Collected software fields include:

* Software name.
* Version.
* Publisher.
* Install date.
* Install location.
* Estimated size in MB.

### 📄 Report Generation

The script creates:

1. Main CSV audit report.
2. Human-readable TXT report.
3. Installed software CSV report.

Reports are stored in:

```text
Desktop\Laptop_Audit_Reports\
```

The script also attempts to detect common Desktop and OneDrive Desktop locations.

---

# ⚙️ How the Audit Works

```text
┌──────────────────────────────────────────────┐
│              Start PowerShell                │
└──────────────────────┬───────────────────────┘
                       │
                       ▼
┌──────────────────────────────────────────────┐
│          Set Asset Name                      │
│          GEPL-Maintenance                    │
└──────────────────────┬───────────────────────┘
                       │
                       ▼
┌──────────────────────────────────────────────┐
│          Detect Desktop Folder               │
│          Create Report Directory             │
└──────────────────────┬───────────────────────┘
                       │
                       ▼
┌──────────────────────────────────────────────┐
│          Collect System Information          │
│  Hardware • Windows • Security • Network     │
│  Battery • BIOS • Software                   │
└──────────────────────┬───────────────────────┘
                       │
                       ▼
┌──────────────────────────────────────────────┐
│          Process and Normalize Data          │
│          Safe-Value / Get-YesNo              │
└──────────────────────┬───────────────────────┘
                       │
                       ▼
┌──────────────────────────────────────────────┐
│          Generate Reports                    │
│          CSV • TXT • Software CSV            │
└──────────────────────┬───────────────────────┘
                       │
                       ▼
┌──────────────────────────────────────────────┐
│          Display Completion Summary          │
└──────────────────────────────────────────────┘
```

---

# 📊 What Information Is Collected

The following table describes the fields in the current V3 script.

## 1. Device Identity

| Field                 | Purpose                     |
| --------------------- | --------------------------- |
| Audit Date            | Date of audit               |
| Audit Time            | Time of audit               |
| Device Name           | Friendly asset name         |
| Windows Computer Name | Actual Windows hostname     |
| Manufacturer          | Device manufacturer         |
| Model                 | Device model                |
| Serial Number         | BIOS-reported serial number |

### Important distinction

```powershell
$assetName = "GEPL-Maintenance"
```

This is a friendly name used in the reports.

It does **not** rename the Windows computer.

The actual Windows hostname is collected separately:

```powershell
$windowsComputerName = Safe-Value $env:COMPUTERNAME
```

---

## 2. Processor

| Field         | Description                             |
| ------------- | --------------------------------------- |
| Processor     | CPU model/name                          |
| CPU Cores     | Physical CPU cores                      |
| CPU Threads   | Logical processors/threads              |
| CPU Max Speed | Maximum clock speed reported by WMI/CIM |

---

## 3. Memory (RAM)

| Field            | Description                                |
| ---------------- | ------------------------------------------ |
| RAM              | Total physical memory                      |
| RAM Type         | RAM type reported by SMBIOS                |
| RAM Module Count | Number of detected physical memory modules |

### RAM type limitation

The script maps SMBIOS memory type values:

```powershell
20  = DDR
21  = DDR2
22  = DDR2 FB-DIMM
24  = DDR3
26  = DDR4
34  = DDR5
```

If the value is unknown, the script returns:

```text
Not Available
```

---

## 4. Storage

| Field                    | Description                              |
| ------------------------ | ---------------------------------------- |
| Storage Total (Physical) | Sum of detected physical disk capacities |
| Storage Model            | Physical disk model                      |
| Storage Serial           | Physical disk serial                     |
| Logical Storage Total    | Sum of local fixed-drive capacity        |
| Free Storage             | Sum of free space on local fixed drives  |

### Important

Physical storage and logical storage are different.

For example:

```text
Physical Storage:
1 × 512 GB SSD

Logical Storage:
C: 200 GB
D: 312 GB
```

The script does not currently provide a complete partition-by-partition inventory.

---

## 5. Windows

| Field              | Description                 |
| ------------------ | --------------------------- |
| Windows Edition    | Windows product name        |
| Windows Version    | OS version                  |
| Windows Build      | OS build number             |
| OS Architecture    | 64-bit / 32-bit             |
| Windows Activation | Activation status           |
| Latest Hotfix Date | Most recent detected hotfix |

---

## 6. Security

| Field                | Description                     |
| -------------------- | ------------------------------- |
| TPM Present          | Whether TPM is present          |
| TPM Ready            | Whether TPM is ready            |
| TPM Version          | TPM manufacturer version        |
| Secure Boot          | Secure Boot status              |
| BitLocker Status     | Current BitLocker volume status |
| BitLocker Encryption | Encryption percentage           |
| Defender             | Antivirus enabled status        |
| Real-Time Protection | Real-time protection status     |
| Firewall             | Windows Firewall profile status |

### Security field interpretation

```text
Yes / No
Enabled / Disabled
Activated / Unlicensed
Not Available
```

`Not Available` does not mean the feature is disabled.

It may mean the command failed, the feature is unsupported, or the information could not be retrieved.

---

## 7. Network

| Field        | Description                             |
| ------------ | --------------------------------------- |
| Wi-Fi IP     | IP address detected on Wi-Fi adapter    |
| Wi-Fi MAC    | MAC address of Wi-Fi adapter            |
| Ethernet IP  | IP address detected on Ethernet adapter |
| Ethernet MAC | MAC address of Ethernet adapter         |
| Bluetooth    | Bluetooth device detection              |

### Privacy warning

IP addresses and MAC addresses can be considered personal or sensitive device information depending on context.

Do not publish raw network information in a public GitHub repository.

---

## 8. Battery

| Field                        | Description                          |
| ---------------------------- | ------------------------------------ |
| Battery Status               | Battery status                       |
| Battery Design Capacity      | Original design capacity             |
| Battery Full Charge Capacity | Current full charge capacity         |
| Battery Health               | Calculated battery health percentage |

### Battery health calculation

```text
Battery Health (%) =
(Full Charge Capacity / Design Capacity) × 100
```

Example:

```text
Design Capacity      = 50,000 mWh
Full Charge Capacity = 40,000 mWh

Battery Health = 80%
```

This is an estimate based on reported capacity, not a complete battery diagnostic.

---

# 🚫 What Is Not Collected

The script explicitly states:

```text
No passwords or BitLocker recovery keys were collected.
```

The current code does not intentionally collect:

* User passwords.
* Windows login credentials.
* BitLocker recovery keys.
* Personal document contents.
* Photos.
* Videos.
* Browser history.
* Email contents.
* Browser saved passwords.
* Full personal file contents.

### However

The script does collect potentially sensitive system identifiers:

* Serial number.
* Windows hostname.
* IP addresses.
* MAC addresses.
* Local administrator group membership.
* Installed software.
* Software installation paths.

Therefore, the project should not be described as collecting "no personal data."

A more accurate statement is:

> This tool is designed to collect system inventory and configuration metadata. It does not intentionally collect passwords or BitLocker recovery keys. Reports may contain sensitive device and organizational information and must be protected accordingly.

---

# 📁 Project Structure

Recommended professional repository structure:

```text
Laptop-Audit-V3/
│
├── README.md
├── LICENSE
├── CHANGELOG.md
├── CONTRIBUTING.md
├── SECURITY.md
├── .gitignore
│
├── src/
│   └── Laptop_Audit.ps1
│
├── docs/
│   ├── Usage.md
│   ├── Privacy.md
│   └── Troubleshooting.md
│
├── tests/
│   └── README.md
│
└── examples/
    └── README.md
```

### Important

Do not commit real audit reports into a public repository.

Keep actual reports outside the repository or in a protected internal storage location.

---

# 🧰 Requirements

## Supported operating systems

| OS         | Support                                 |
| ---------- | --------------------------------------- |
| Windows 11 | Primary target                          |
| Windows 10 | Expected support; test on target builds |
| Windows 7  | Not supported by the current script     |
| Linux      | Not supported                           |
| macOS      | Not supported                           |

### PowerShell

The script is designed for Windows PowerShell and uses Windows-specific CIM/WMI, Defender, BitLocker, PnP, and registry commands.

Recommended:

```text
Windows PowerShell 5.1
```

PowerShell 7 may run parts of the script, but compatibility should be tested before claiming full support.

## Permissions

Run PowerShell as Administrator for the most complete results.

Some fields may still be unavailable even with administrator permissions.

## Additional requirements

* Working Windows installation.
* PowerShell available.
* Access to the Desktop report directory.
* Permission to run local PowerShell scripts.
* Device owner or IT administrator authorization.

---

# ✅ Before Running the Script

Complete these checks before running the audit on any laptop or PC.

## Authorization checklist

* [ ] You own the device or have permission from the owner.
* [ ] You are authorized to perform an IT audit.
* [ ] You understand what information the script collects.
* [ ] You have permission to store the resulting reports.
* [ ] You will not upload private reports to a public repository.
* [ ] You will not use the script to bypass security controls.

## Device checklist

* [ ] Windows is running normally.
* [ ] PowerShell is available.
* [ ] The device is connected to power if possible.
* [ ] Important work is saved.
* [ ] No important system operation is in progress.
* [ ] You know where the reports will be saved.

## Security checklist

* [ ] Do not disable antivirus.
* [ ] Do not disable BitLocker.
* [ ] Do not disable Secure Boot.
* [ ] Do not change the Windows execution policy permanently.
* [ ] Do not collect passwords or recovery keys.
* [ ] Do not publish raw serial numbers, IPs, or MAC addresses.

---

# 📥 Installation

## Option A — Run from Downloads

1. Save the PowerShell script as:

```text
Laptop_Audit.ps1
```

2. Open Windows PowerShell as Administrator.

3. Navigate to the Downloads folder:

```powershell
Set-Location "$env:USERPROFILE\Downloads"
```

4. Confirm the script exists:

```powershell
Get-ChildItem -Filter "*.ps1"
```

5. Run the script:

```powershell
powershell.exe -ExecutionPolicy Bypass -File ".\Laptop_Audit.ps1"
```

### Why use `Set-Location`?

This is the safe way to navigate to a folder using a full path.

Avoid:

```powershell
cd C:\Users\
```

when you are already inside:

```text
C:\Windows\System32
```

PowerShell can interpret the path relative to the current directory.

Use a full path or `$env:USERPROFILE` instead.

---

# ▶️ How to Run

## Step 1 — Open PowerShell as Administrator

Search Windows for:

```text
PowerShell
```

Right-click:

```text
Windows PowerShell
```

Select:

```text
Run as administrator
```

## Step 2 — Go to Downloads

```powershell
Set-Location "$env:USERPROFILE\Downloads"
```

## Step 3 — Confirm the script

```powershell
Get-ChildItem -Filter "*.ps1"
```

Expected:

```text
Laptop_Audit.ps1
```

## Step 4 — Run the audit

```powershell
powershell.exe -ExecutionPolicy Bypass -File ".\Laptop_Audit.ps1"
```

## Step 5 — Open the reports

The script attempts to create:

```text
Desktop\Laptop_Audit_Reports\
```

Open the CSV report using Microsoft Excel.

Open the TXT report using Notepad or another text editor.

---

# 🔁 How to Use on Another Computer

The same script can be reused on another authorized Windows computer.

### Example

First computer:

```text
GEPL-Maintenance
```

Second computer:

```text
GEPL-Admin
```

### Before running

Open the script and update:

```powershell
$assetName = "GEPL-Maintenance"
```

Change it to:

```powershell
$assetName = "GEPL-Admin"
```

This updates the friendly name used in report filenames and the Device Name field.

### Do not manually update hardware details

Do not change:

```powershell
$manufacturer
$model
$serial
$cpuName
$ramGB
```

These values are collected automatically from the computer being audited.

### Reusable process

```text
Copy Laptop_Audit.ps1
        ↓
Open on target computer
        ↓
Set the correct asset name
        ↓
Run PowerShell as Administrator
        ↓
Generate new reports
        ↓
Review and securely store reports
```

### Important

The script does not transfer files, migrate Windows, rename the computer, or install software.

It only audits the computer where it runs.

---

# 📄 Generated Reports

## 1. Main CSV report

Example:

```text
Laptop_Audit_GEPL-Maintenance_20260915_141118.csv
```

Contains one audit record with columns such as:

```text
Audit Date
Audit Time
Device Name
Windows Computer Name
Manufacturer
Model
Serial Number
Processor
RAM
Storage Total
Windows Edition
TPM Present
Secure Boot
BitLocker Status
Defender
Firewall
Battery Health
Installed Software Count
```

## 2. TXT report

Example:

```text
Laptop_Audit_GEPL-Maintenance_20260915_141118.txt
```

Human-readable format:

```text
Audit Date: 2026-09-15
Audit Time: 14:11:18
Device Name: GEPL-Maintenance
Manufacturer: HP
Model: HP 250R
Serial Number: [REDACTED]
RAM: 7.65 GB
```

## 3. Installed software CSV

Example:

```text
Installed_Software_GEPL-Maintenance_20260915_141118.csv
```

Contains:

```text
SoftwareName
Version
Publisher
InstallDate
InstallLocation
EstimatedSizeMB
```

---

# 📊 Understanding the Report

## Not Available

Means the information could not be retrieved or was not reported by the system.

It does not necessarily mean the feature is missing.

## Detected

Means the script found a matching device, application, or path.

It is not a full validation of the feature.

## Enabled

Means the queried component reported as enabled.

It is not a complete security compliance certification.

## Activated

Means the queried Windows licensing information reported an activated status.

It is not proof of license ownership or organizational licensing compliance.

---

# 🔐 Privacy and Security Policy

## Data classification

The report should be treated as internal IT information.

| Data                    | Classification                 |
| ----------------------- | ------------------------------ |
| CPU model               | Low sensitivity                |
| RAM size                | Low sensitivity                |
| Storage capacity        | Low sensitivity                |
| Serial number           | Sensitive device identifier    |
| Windows hostname        | Sensitive device identifier    |
| IP address              | Sensitive network information  |
| MAC address             | Sensitive network identifier   |
| Installed software      | Potentially sensitive          |
| Local administrators    | Sensitive security information |
| Battery health          | Low sensitivity                |
| Passwords               | Not intentionally collected    |
| BitLocker recovery keys | Not intentionally collected    |

## Privacy principles

### 1. Data minimization

Collect only the information necessary for the intended IT audit.

### 2. Purpose limitation

Use audit reports for authorized IT inventory, maintenance, troubleshooting, and asset management.

### 3. Access control

Only authorized staff should access reports containing sensitive information.

### 4. Secure storage

Store reports in protected folders or approved internal storage.

### 5. Retention

Define how long reports should be retained and securely delete reports that are no longer required.

### 6. Transparency

Inform the device owner or relevant organization about the audit purpose and data collected when required by applicable policy.

---

# 🛡️ Data Protection Rules

## Never commit real reports

Add the following to `.gitignore`:

```gitignore
# Audit reports
Laptop_Audit_Reports/

# CSV and TXT exports
Laptop_Audit_*.csv
Laptop_Audit_*.txt
Installed_Software_*.csv

# Local reports folder
reports/

# PowerShell logs
*.log
```

## Never hardcode passwords

Bad:

```powershell
$password = "MyPassword123"
```

Never include credentials in the script.

## Never collect recovery keys

Do not add commands that retrieve or export BitLocker recovery keys.

## Never collect personal files

Do not add recursive file collection commands such as:

```powershell
Get-ChildItem C:\Users -Recurse
```

unless there is a separate, explicitly authorized file inventory requirement with appropriate privacy controls.

## Never upload raw reports publicly

Before sharing an audit report, review and redact:

* Serial numbers.
* IP addresses.
* MAC addresses.
* Hostnames.
* Usernames.
* Local administrator names.
* Software installation paths.
* Other organization-specific details.

---

# ⚠️ Important Technical Limitations

This is one of the most important sections for professional publication.

## 1. Battery WMI compatibility

The current script uses:

```powershell
Get-CimInstance -Namespace root\wmi -ClassName BatteryStaticData
```

and:

```powershell
Get-CimInstance -Namespace root\wmi -ClassName BatteryFullChargedCapacity
```

Some systems may return:

```text
Get-CimInstance : Generic failure
```

This can happen because of unavailable battery WMI classes, firmware limitations, permissions, or provider compatibility.

### Current behavior

The script catches the error and continues.

Battery values may be:

```text
Not Available
```

### Recommended improvement

Add a fallback battery health method using a supported Windows battery report or another compatible data source.

---

## 2. Windows 7 compatibility

The current script uses modern Windows commands and features such as:

* `Get-CimInstance`
* `Get-Tpm`
* `Get-BitLockerVolume`
* `Get-MpComputerStatus`
* `Get-NetFirewallProfile`
* `Get-PnpDevice`
* `Get-AppxPackage`

Some of these are not available or behave differently on Windows 7.

Therefore:

> Windows 7 support is not guaranteed by the current V3 implementation.

---

## 3. Office detection

The current code checks common Office installation directories and AppX package names.

This is a basic detection method.

It may not accurately identify:

* All Microsoft 365 installations.
* Click-to-Run configuration.
* Office licensing status.
* All Office versions.
* Portable applications.
* Software installed through non-standard methods.

Office detection should be treated as an indicator, not a licensing audit.

---

## 4. Software inventory limitations

The current software inventory reads common uninstall registry locations.

It may miss:

* Microsoft Store applications.
* Portable software.
* Some per-user installations.
* Software installed using custom methods.
* Applications without uninstall registry entries.

The software count is therefore not guaranteed to represent every application on the device.

---

## 5. Network adapter classification

The script identifies Wi-Fi adapters using:

```powershell
"Wi-Fi|Wireless|802.11"
```

Other adapters may be classified as Ethernet.

Virtual adapters, VPNs, docking stations, and unusual adapter descriptions may not be classified perfectly.

---

## 6. Storage health is not collected

The current script collects disk capacity, model, and serial information.

It does not currently collect:

* SSD/HDD health.
* SMART health.
* Drive temperature.
* NVMe wear percentage.
* Remaining SSD life.
* Bad sectors.
* Disk performance.

A future storage health module should be added separately.

---

## 7. Audit is not a security certification

This script provides an inventory and configuration snapshot.

It is not a replacement for:

* Vulnerability scanning.
* Penetration testing.
* Endpoint Detection and Response.
* Microsoft Intune compliance.
* Enterprise asset management.
* Formal security certification.
* License compliance auditing.

---

# 🛠️ Troubleshooting

## Error: Illegal characters in path

Example:

```text
cd : Illegal characters in path.
```

### Cause

The path may be interpreted incorrectly because the current working directory is different.

### Fix

Use:

```powershell
Set-Location "$env:USERPROFILE\Downloads"
```

Verify:

```powershell
Get-Location
```

Expected:

```text
C:\Users\<YourUser>\Downloads
```

---

## Error: Cannot find path

Example:

```text
Cannot find path 'C:\Windows\system32\Users'
```

### Cause

PowerShell interpreted a relative path from:

```text
C:\Windows\System32
```

### Fix

Use an absolute path:

```powershell
Set-Location "C:\Users\genli\Downloads"
```

Or:

```powershell
Set-Location "$env:USERPROFILE\Downloads"
```

---

## Error: Ampersand (&) character is not allowed

Example:

```text
The ampersand (&) character is not allowed.
```

### Cause

A PowerShell command contains an invalid expression involving `&`.

### Fix

Use a simple command without the invalid expression:

```powershell
Get-ChildItem -Filter "*.ps1"
```

Do not manually add `&` unless you are intentionally invoking a command or expression.

---

## Error: Generic failure — BatteryStaticData

Example:

```text
Get-CimInstance : Generic failure
```

### Cause

Battery WMI information may be unavailable.

### Expected behavior

The script should continue and produce the report.

### Recommended action

Check whether Windows provides battery information through:

```powershell
Get-CimInstance Win32_Battery
```

If battery health is required, use a compatible fallback method.

---

## CSV opens with `########`

### Cause

Excel column width is too small for the displayed value.

### Fix

1. Open the CSV in Excel.
2. Select the relevant columns.
3. Double-click the column boundary to AutoFit.
4. Or use **Home → Format → AutoFit Column Width**.

This is usually a display issue, not necessarily data loss.

---

## Script finishes but some fields are Not Available

### Possible reasons

* Hardware does not expose the requested information.
* The WMI/CIM provider is unavailable.
* The command requires a different permission level.
* The system uses a different firmware implementation.
* The Windows version does not support the command.
* The information is not applicable to the device.

The script is designed to continue instead of stopping on every missing field.

---

# 🔧 Safe Production Improvements

The current V3 script is a good starting point for an IT asset inventory tool.

Before calling it a production-grade enterprise auditing system, consider the following improvements.

## Priority 1 — Reliability

* [ ] Add structured error handling for each audit module.
* [ ] Record failed commands separately.
* [ ] Add a clear audit status.
* [ ] Validate that reports were successfully created.
* [ ] Add Windows version compatibility checks.
* [ ] Improve battery health fallback.
* [ ] Add disk health detection.

## Priority 2 — Privacy

* [ ] Add optional redaction of serial numbers.
* [ ] Add optional redaction of IP and MAC addresses.
* [ ] Add a privacy notice before execution.
* [ ] Add a report sensitivity classification.
* [ ] Keep raw reports outside public GitHub.
* [ ] Define retention and deletion procedures.

## Priority 3 — Reporting

* [ ] Add HTML report output.
* [ ] Add report summary.
* [ ] Add device health status.
* [ ] Add report schema version.
* [ ] Add audit duration.
* [ ] Add module success/failure summary.
* [ ] Add one report per device with a unique audit ID.

## Priority 4 — Enterprise features

* [ ] Centralized inventory storage.
* [ ] Device comparison.
* [ ] Scheduled auditing.
* [ ] Intune integration.
* [ ] Active Directory integration.
* [ ] Role-based access control.
* [ ] Secure report upload.
* [ ] Dashboard.
* [ ] Audit history.
* [ ] Change detection.

---

# 📦 Recommended Repository Workflow

## Development

```text
Write code
   ↓
Test on development laptop
   ↓
Review privacy and security
   ↓
Validate generated reports
   ↓
Commit code to GitHub
   ↓
Tag release
```

## Release example

```text
v3.0.0
```

Suggested release notes:

```text
Laptop Audit V3.0.0

Added:
- Hardware inventory
- Windows information
- Security status
- Network information
- Battery information
- Installed software inventory
- CSV and TXT reports

Known limitations:
- Battery WMI compatibility
- Windows 7 compatibility
- Basic Office detection
- No disk health module
```

---

# 🧪 Testing Checklist

Before publishing or deploying the script, test on different devices.

## Hardware testing

* [ ] HP laptop.
* [ ] Dell laptop.
* [ ] Lenovo laptop.
* [ ] Desktop PC.
* [ ] Device with no battery.
* [ ] Device with multiple disks.
* [ ] Device with integrated GPU.
* [ ] Device with dedicated GPU.
* [ ] Device with multiple RAM modules.

## Windows testing

* [ ] Windows 10 64-bit.
* [ ] Windows 11 64-bit.
* [ ] Different Windows builds.
* [ ] Standard user execution.
* [ ] Administrator execution.

## Security testing

* [ ] TPM available.
* [ ] TPM unavailable.
* [ ] Secure Boot enabled.
* [ ] Secure Boot disabled.
* [ ] BitLocker enabled.
* [ ] BitLocker disabled.
* [ ] Defender enabled.
* [ ] Firewall enabled.

## Reporting testing

* [ ] CSV is created.
* [ ] TXT is created.
* [ ] Software CSV is created.
* [ ] Reports open in Excel.
* [ ] Report folder is created.
* [ ] No passwords are collected.
* [ ] No recovery keys are collected.
* [ ] Sensitive information is handled safely.

---

# 📜 Disclaimer

This software is provided for authorized IT inventory, maintenance, and system assessment purposes.

The author does not guarantee that all hardware, software, security, or operating system information will be available or accurate on every device.

The user is responsible for:

* Obtaining authorization.
* Complying with applicable privacy and data protection laws.
* Protecting generated reports.
* Reviewing audit results.
* Validating system information before making technical decisions.
* Using the script only for lawful and authorized purposes.

This project is not intended to bypass security controls, collect credentials, retrieve recovery keys, or access unauthorized information.

---

# 📄 License

Choose an appropriate open-source license before publishing.

For example:

```text
MIT License
```

The license should be added to the repository as:

```text
LICENSE
```

Do not claim a license until it has been selected and included.

---

# 👤 Author

**Dinesh K**

Project: Laptop Audit – Final V3

Purpose: Professional IT Asset Management and Windows Device Auditing

---

## ⭐ Contributing

Contributions, suggestions, bug reports, and improvements are welcome.

Before submitting a contribution:

1. Test the change on a supported Windows system.
2. Explain the purpose of the change.
3. Avoid collecting unnecessary personal information.
4. Do not include real device reports.
5. Update the documentation when behavior changes.
6. Follow the repository's contribution guidelines.

---

## 📌 Final Note

Laptop Audit – Final V3 is intended to provide a repeatable, structured, and privacy-conscious approach to Windows device auditing.

The project can be extended into a more complete IT asset management solution with improved hardware detection, security validation, report generation, and centralized inventory capabilities.
