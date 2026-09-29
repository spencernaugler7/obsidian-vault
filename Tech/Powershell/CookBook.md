---
source: https://learn.microsoft.com/en-us/powershell/scripting/samples/sample-scripts-for-administration?view=powershell-7.6
---
## Get All Drives On Computer
```powershell
Get-PSDrive -PSProvider 'FileSystem'
```

## Get Available Disk Space
```powershell
Get-CimInstance -ClassName Win32_LogicalDisk -Filter "DriveType=3"
```

## Get Local Time
```powershell
Get-CimInstance -ClassName Win32_LocalTime
```

