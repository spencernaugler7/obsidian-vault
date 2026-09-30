## Get All Drives On Computer
```csharp
var space = DriveInfo.GetDrives();
//Console.WriteLine(string.Join("\n", space.Select(s => s.Name)));
```

## Get Available Disk Space
```csharp
var space = DriveInfo.GetDrives().First().AvailableFreeSpace;
//Console.WriteLine(space);
```

## Get Local Time
```csharp
var currentTime = DateTime.Now
//Console.Write(CurrentTime);
```

## Get Property Value from File
```csharp
var dir = Directory.GetCurrentDirectory();
//Console.WriteLine(dir);
```

## Search for a text file in all subdirectories that ends with *.cs
```csharp
var dir = Directory.EnumerateFiles(".", "*.cs", SearchOption.AllDirectories);
// Console.WriteLine(string.Join("\n", dir));
```