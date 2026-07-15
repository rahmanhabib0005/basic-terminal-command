# Information Gathering Reference Guide

Essential built-in PowerShell commands for collecting network, system, and hardware information on Windows machines.

---

## 1. Network & IP Information

### Get Local IP Addresses
```powershell
Get-NetIPAddress -AddressFamily IPv4 | Format-Table IPAddress, InterfaceAlias
```

### View Network Routing Table
```powershell
Get-NetRoute -AddressFamily IPv4
```

### Check Active Connections and Listening Ports
```powershell
Get-NetTCPConnection -State Listen
```

### Test Remote Port Status
```powershell
Test-NetConnection google.com -Port 80
```

---

## 2. Domain & DNS Information

### Resolve DNS Records
```powershell
Resolve-DnsName google.com -Type MX
```

### Query Domain Ownership Data
```powershell
Invoke-RestMethod -Uri "https://arin.net"
```

---

## 3. System Hardware & OS

### Summary of System Specifications
```powershell
Get-ComputerInfo | Select-Object OsName, OsVersion, CsModel, BiosVersion
```

### Collect Installed RAM Hardware Details
```powershell
Get-CimInstance Win32_PhysicalMemory | Format-Table Capacity, Speed
```

### Collect Disk Space Storage Information
```powershell
Get-CimInstance Win32_LogicalDisk | Format-Table DeviceID, VolumeName, Size, FreeSpace
```

---

## 4. Process & Security

### List Top 10 CPU-Consuming Processes
```powershell
Get-Process | Sort-Object CPU -Descending | Select-Object -First 10 ProcessName, CPU, WorkingSet
```

### Review Installed OS Security Patches
```powershell
Get-HotFix | Sort-Object InstalledOn -Descending
```

---

## 5. Data Export Shortcuts

Append these to the end of any command using the pipe (`|`) character to save your results:

### Export to Text file
```powershell
 | Out-File C:\(\path\to\output.\)txt
```

### Export to CSV spreadsheet
```powershell
 | Export-Csv C:\(\path\to\output.\)csv -NoTypeInformation
```

## 6. User Account & Security Auditing

### List All Local User Accounts
Displays all local users configured on the system along with their description and status.
```powershell
Get-LocalUser | Format-Table Name, Enabled, Description
```

### List Members of the Local Administrators Group
Identifies every user account and security group that possesses full administrative rights on the machine.
```powershell
Get-LocalGroupMember -Group "Administrators" | Format-Table Name, PrincipalSource, ObjectClass
```

### View Currently Logged-In Users
Queries the system configuration to see who is actively signed in or running sessions.
```powershell
Get-CimInstance Win32_ComputerSystem | Select-Object -ExpandProperty UserName
```

---

## 7. Software & Startup Inventory

### List Installed Software (64-bit & 32-bit Applications)
Scans the system registry to extract a clean list of installed applications, display names, and version numbers.
```powershell
Get-ItemProperty HKLM:\Software\Microsoft\Windows\CurrentVersion\Uninstall\*, HKLM:\Software\Wow6432Node\Microsoft\Windows\CurrentVersion\Uninstall\* | Select-Object DisplayName, DisplayVersion, Publisher | Where-Object {\$_.DisplayName} | Format-Table
```

### List Applications Scheduled to Run at Windows Startup
Identifies scripts or applications configured to launch automatically when a user logs in.
```powershell
Get-CimInstance Win32_StartupCommand | Format-Table Name, Command, Location
```

---

## 8. Advanced Network Diagnostics

### Network Trace Route (Traceroute)
Traces the physical path and network hops your traffic takes to reach a specific destination target.
```powershell
Test-NetConnection google.com -TraceRoute
```

### View Detailed Network Adapter Statistics
Gathers performance data, packets sent/received, and error rates for all active physical network interfaces.
```powershell
Get-NetAdapterStatistics | Format-Table Name, ReceivedBytes, SentBytes, DiscardedReceivedPackets
```

---

## 9. Environment & System Paths

### List All System Environment Variables
Gathers all active environment paths, system variables, architecture profiles, and user directories.
```powershell
Get-ChildItem Env: | Format-Table Name, Value
```
