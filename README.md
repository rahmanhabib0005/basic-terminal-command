## Information Gathering & Reconnaissance Reference Guide
This guide contains essential built-in PowerShell commands for collecting network, system, and hardware information on Windows machines.
------------------------------
## 📋 Table of Contents

   1. Network & IP Information Collectors
   2. Domain & DNS Information Collectors
   3. System Hardware & OS Collectors
   4. Process & Security Collectors
   5. Data Export Shortcuts

------------------------------
## 1. Network & IP Information Collectors## Get Local IP Addresses
Replaces the legacy ipconfig command. Extracts IPv4 addresses and interface names.

Get-NetIPAddress -AddressFamily IPv4 | Format-Table IPAddress, InterfaceAlias

## View Network Routing Table
Replaces route print. Shows where network traffic is being directed.

Get-NetRoute -AddressFamily IPv4

## Check Active Connections and Listening Ports
Replaces netstat. Lists ports currently waiting for or handling active connections.

Get-NetTCPConnection -State Listen

## Test Remote Port Status
Replaces telnet. Verifies if a specific port is open on a target server.

Test-NetConnection google.com -Port 80

------------------------------
## 2. Domain & DNS Information Collectors## Resolve DNS Records
Replaces nslookup. Gathers clean, formatted DNS data (A, MX, TXT, NS).

Resolve-DnsName google.com -Type MX

## Query Domain Ownership Data (Whois alternative)
Uses the web-based RDAP protocol to grab registration details for an IP address.

Invoke-RestMethod -Uri "https://arin.net"

------------------------------
## 3. System Hardware & OS Collectors## Summary of System Specifications
Replaces systeminfo. Provides OS version, BIOS strings, and machine models.

Get-ComputerInfo | Select-Object OsName, OsVersion, CsModel, BiosVersion

## Collect Installed RAM Hardware Details
Queries physical memory sticks to report capacity (in bytes) and hardware speed.

Get-CimInstance Win32_PhysicalMemory | Format-Table Capacity, Speed

## Collect Disk Space Storage Information
Displays total size and remaining free space for available local storage drives.

Get-CimInstance Win32_LogicalDisk | Format-Table DeviceID, VolumeName, Size, FreeSpace

------------------------------
## 4. Process & Security Collectors## List Top 10 CPU-Consuming Processes
Tracks currently executing applications and sorts them by heavy processor utilization.

Get-Process | Sort-Object CPU -Descending | Select-Object -First 10 ProcessName, CPU, WorkingSet

## Review Installed OS Security Patches
Lists all applied Windows updates and hotfixes sorted by the installation date.

Get-HotFix | Sort-Object InstalledOn -Descending

------------------------------
## 5. Data Export Shortcuts
To save the information gathered by any command above, append an export pipe to the end of the line:

* Export to Text file: | Out-File C:\path\to\output.txt
* Export to CSV spreadsheet: | Export-Csv C:\path\to\output.csv -NoTypeInformation

------------------------------
Would you like help combining these into an automated PowerShell script (.ps1) that exports a full report automatically, or do you need to gather information from Active Directory?

