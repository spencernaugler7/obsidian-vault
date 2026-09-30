---
source: https://learn.microsoft.com/en-us/powershell/scripting/samples/sample-scripts-for-administration?view=powershell-7.6
---
## Find Command
```powershell
Get-Command <search string> -UseFuzzyMatching | Where-Object { $_.CommandType -eq 'Cmdlet' }
```

## Declare variables
```powershell
$a = "Hello"
$range = 1..10
```

## Comparison Operators
```powershell
(1 -eq 1) -and (1 -eq 2)   # Result is False
```

## Create .NET object with a constructor
```powershell
New-Object -TypeName System.Diagnostics.EventLog -ArgumentList Application
# create a new datetime and access property
(New-Object System.DateTime)
```
access static properties
```powershell
(New-Object System.DateTime)::UtcNow
# Tuesday, September 29, 2026 6:32:03 PM
```
shorthand for `(New-Object <ObjectName>)`
```powershell
[<ObjectName>] # example [DateTime]::UtcNow
```

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

## Select Property From Child Item
```powershell
Get-ChildItem $targetDir | ForEach-Object { @($_.CreationTime, $_.LastWriteTime) }
```

## Change Property on File
```powershell
Get-ChildItem .\test.txt | %{ $_.LastWriteTime = '09/20/2026 06:00:36' }
## ----------- or ------------
(Get-Item .\test.txt).LastWriteTime = '01/11/2002 06:00:36'

```

## Get Property Value from File
```powershell
Get-ChildItem .\test.txt | %{ $_.CreationTime, $_.LastWriteTime }
# ------------- or ------------
(Get-ChildItem .\test.txt).CreationTime
```

## Write To A File
```powershell
Get-Process | Out-File -FilePath .\Process.txt
Get-Content -Path .\Process.txt
```

## String Interpolation
```powershell
$name = "Smith"
$message = "Hello, $name! Welcome to PowerShell."
```

## Select property in pipeline
```powershell

```