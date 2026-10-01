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

## Arrays

```powershell
$SampleArray = 22,5,10,8,12,9,80
$SampleArray = "Blah","Foo","Bar","Baz"
```

## Get the Type of the return value of an object

```powershell
(Get-ChildItem .\Test\test.txt).GetType()
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

## Functions

> [!note]
> function name should start with [[Cookbook#Get Verbs]]

### Basic Function Definition

```powershell
function Test-MrParameter {
    param (
        $ComputerName
    )

    Write-Output $ComputerName
}
```

### Advanced functions have `$Verbose` and `$Debug` parameters added implicitly

```powershell
function Test-MrParameter {
	[CmdletBinding()] # Turns a regular function into an advanced function
	param (
		$ComputerName
	)
	
	Write-Output $ComputerName
}
```

### Take Pipeline input

```powershell
function Test-Blah {
    [CmdletBinding()]
    param(
        [Parameter(ValueFromPipeline)]
        [string[]] $Words
    )

    foreach ($String in $Words) {
        Write-Output $String
    }
}

Write-Host "Yuck","Tisk" | Test-Blah
```

## Get Verbs

```powershell
Get-Verb
```
