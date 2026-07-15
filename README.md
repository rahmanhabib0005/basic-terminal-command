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
