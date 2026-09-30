## Get All Drives On Computer
```powershell
Get-PSDrive -PSProvider 'FileSystem'
```

## Get Available Disk Space
```powershell
Get-CimInstance -ClassName Win32_LogicalDisk -Filter "DriveType=3"
```

## Get Local Time
```csharp
var currentTime = DateTime.Now
```

## Get Property Value from File
```csharp
var dir = Directory.GetCurrentDirectory();
Console.WriteLine(dir);
```
