## Example 1: Create a file in the current directory
This command creates a text file that is named "testfile1.txt" in the current directory. The dot
('.') in the value of the **Path** parameter indicates the current directory. The quoted text that
follows the **Value** parameter is added to the file as content.

```powershell
New-Item -Path . -Name "testfile1.txt" -ItemType "File" -Value "This is a text string."
```

## Example 2: Create a directory
This command creates a directory named "Logfiles" in the `C:` drive. The **ItemType** parameter
specifies that the new item is a directory, not a file or other file system object.

```powershell
New-Item -Path "C:\" -Name "Logfiles" -ItemType "Directory"
```

## Example 3: Create a profile
This command creates a PowerShell profile in the path that is specified by the `$PROFILE` variable.

You can use profiles to customize PowerShell. `$PROFILE` is an automatic (built-in) variable that
stores the path and file name of the "CurrentUser/CurrentHost" profile. By default, the profile does
not exist, even though PowerShell stores a path and file name for it.

In this command, the `$PROFILE` variable represents the path of the file. **ItemType** parameter
specifies that the command creates a file. The **Force** parameter lets you create a file in the
profile path, even when the directories in the path do not exist.

After you create a profile, you can enter aliases, functions, and scripts in the profile to
customize your shell.

For more information, see
[about_Automatic_Variables](../Microsoft.PowerShell.Core/About/about_Automatic_Variables.md)
and [about_Profiles](../Microsoft.PowerShell.Core/About/about_Profiles.md).

```powershell
New-Item -Path $PROFILE -ItemType "File" -Force
```

## Example 4: Create a directory in a different directory

This example creates a new Scripts directory in the "C:\PS-Test" directory.

The name of the new directory item, "Scripts", is included in the value of **Path** parameter,
instead of being specified in the value of **Name**. As indicated by the syntax, either command form
is valid.

```powershell
New-Item -ItemType "Directory" -Path "C:\ps-test\scripts"
```

## Example 5: Create multiple files
This example creates files in two different directories. Because **Path** takes multiple strings,
you can use it to create multiple items.

```powershell
New-Item -ItemType "File" -Path "C:\ps-test\test.txt", "C:\ps-test\Logs\test.log"
```

## Example 6: Use wildcards to create files in multiple directories
The `New-Item` cmdlet supports wildcards in the **Path** parameter. The following command creates a
`temp.txt` file in all of the directories specified by the wildcards in the **Path** parameter.

```powershell
Get-ChildItem -Path C:\Temp\
```

```Output
	Directory:  C:\Temp

Mode                LastWriteTime     Length Name
----                -------------     ------ ----
d-----        5/15/2019   6:45 AM        1   One
d-----        5/15/2019   6:45 AM        1   Two
d-----        5/15/2019   6:45 AM        1   Three
```

```powershell
New-Item -Path C:\Temp\* -Name temp.txt -ItemType File | Select-Object FullName
```

```Output
FullName
--------
C:\Temp\One\temp.txt
C:\Temp\Three\temp.txt
C:\Temp\Two\temp.txt
```

The `Get-ChildItem` cmdlet shows three directories under the `C:\Temp` directory. Using wildcards
the `New-Item` cmdlet creates a `temp.txt` file in all of the directories under the current
directory. The `New-Item` cmdlet outputs the items you created, which is piped to `Select-Object`
to verify the paths of the newly created files.

## Example 7: Create a symbolic link to a file or folder
This example creates a symbolic link to the `Notice.txt` file in the current folder.

```powershell
$link = New-Item -ItemType SymbolicLink -Path .\link -Target .\Notice.txt
$link | Select-Object LinkType, Target
```

```Output
LinkType     Target
--------     ------
SymbolicLink {.\Notice.txt}
```

In this example, **Target** is an alias for the **Value** parameter. The target of the symbolic link
can be a relative path. Prior to PowerShell v6.2, the target must be a fully-qualified path.

Beginning in PowerShell 7.1, you can now create to a **SymbolicLink** to a folder on Windows using a
relative path.

## Example 8: Use the -Force parameter to attempt to recreate folders
This example creates a folder with a file inside. Then, attempts to create the same folder using
`-Force`. It will not overwrite the folder but simply return the existing folder object with the
file created intact.

```powershell
PS> New-Item -Path .\TestFolder -ItemType Directory
PS> New-Item -Path .\TestFolder\TestFile.txt -ItemType File

PS> New-Item -Path .\TestFolder -ItemType Directory -Force

Directory: C:\
Mode                LastWriteTime         Length Name
----                -------------         ------ ----
d-----         5/1/2020   8:03 AM                TestFolder

PS> Get-ChildItem .\TestFolder\

Directory: C:\TestFolder
Mode                LastWriteTime         Length Name
----                -------------         ------ ----
-a----         5/1/2020   8:03 AM              0 TestFile.txt
```

## Example 9: Use the -Force parameter to overwrite existing files
This example creates a file with a value and then recreates the file using `-Force`. This overwrites
the existing file, as you can see by the **Length** property.

```powershell
PS> New-Item ./TestFile.txt -ItemType File -Value 'This is just a test file'

Directory: C:\Source\Test
Mode                LastWriteTime         Length Name
----                -------------         ------ ----
-a----         5/1/2020   8:32 AM             24 TestFile.txt

New-Item ./TestFile.txt -ItemType File -Force

Directory: C:\Source\Test
Mode                LastWriteTime         Length Name
----                -------------         ------ ----
-a----         5/1/2020   8:32 AM              0 TestFile.txt
```

> [!NOTE]
> When using `New-Item` with the **Force** parameter to create registry keys, the command behaves
> the same as when overwriting a file. If the registry key already exists, the key and all
> properties and values are overwritten with an empty registry key.