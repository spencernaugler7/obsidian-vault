Gets all commands.

## Example 1: Get cmdlets, functions, and aliases

This command gets the PowerShell cmdlets, functions, and aliases that are installed on the computer.

```powershell
Get-Command
```

## Example 2: Get commands in the current session

This command uses the **ListImported** parameter to get only the commands in the current session.

```powershell
Get-Command -ListImported
```

## Example 3: Get cmdlets and display them in order

This command gets all the cmdlets, sorts them alphabetically by the noun in the cmdlet name, and
then displays them in noun-based groups. This display can help you find the cmdlets for a task.

```powershell
Get-Command -Type Cmdlet | Sort-Object -Property Noun | Format-Table -GroupBy Noun
```

## Example 4: Get commands in a module

This command uses the **Module** parameter to get the commands in the Microsoft.PowerShell.Security
and Microsoft.PowerShell.Utility modules.

```powershell
Get-Command -Module Microsoft.PowerShell.Security, Microsoft.PowerShell.Utility
```

## Example 5: Get information about a cmdlet

This command gets information about the `Get-AppLockerPolicy` cmdlet. It also imports the
**AppLocker** module, which adds all the commands in the **AppLocker** module to the current
session.

```powershell
Get-Command Get-AppLockerPolicy
```

When a module is imported automatically, the effect is the same as using the Import-Module cmdlet.
The module can add commands, types and formatting files, and run scripts in the session. To enable,
disable, and configuration automatic importing of modules, use the `$PSModuleAutoLoadingPreference`
preference variable. For more information, see
[about_Preference_Variables](../Microsoft.PowerShell.Core/About/about_Preference_Variables.md).

## Example 6: Get the syntax of a cmdlet

This command uses the **ArgumentList** and **Syntax** parameters to get the syntax of the
`Get-ChildItem` cmdlet when it's used in the Cert: drive. The Cert: drive is a PowerShell drive that
the Certificate Provider adds to the session.

```powershell
Get-Command  -Name Get-ChildItem -Args Cert: -Syntax
```

When you compare the syntax displayed in the output with the syntax that's displayed when you omit
the **Args** (**ArgumentList**) parameter, you'll see that the **Certificate provider** adds a
dynamic parameter, **CodeSigningCert**, to the `Get-ChildItem` cmdlet.

For more information about the Certificate provider, see
[about_Certificate_Provider](../Microsoft.PowerShell.Security/About/about_Certificate_Provider.md).

## Example 7: Get dynamic parameters

The command in the example uses the `Get-DynamicParameters` function to get the dynamic parameters
that the Certificate provider adds to the `Get-ChildItem` cmdlet when it's used in the Cert: drive.

```powershell
function Get-DynamicParameters
{
	param ($Cmdlet, $PSDrive)
	(Get-Command -Name $Cmdlet -ArgumentList $PSDrive).ParameterSets |
	  ForEach-Object {$_.Parameters} |
		Where-Object { $_.IsDynamic } |
		  Select-Object -Property Name -Unique
}
Get-DynamicParameters -Cmdlet Get-ChildItem -PSDrive Cert:
```

```Output
Name
----
CodeSigningCert
```

The `Get-DynamicParameters` function in this example gets the dynamic parameters of a cmdlet. This
is an alternative to the method used in the previous example. Dynamic parameter can be added to a
cmdlet by another cmdlet or a provider.

## Example 8: Get all commands of all types

This command gets all commands of all types on the local computer, including executable files in the
paths of the **PATH** environment variable (`$Env:PATH`).

```powershell
Get-Command *
```

It returns an **ApplicationInfo** object (System.Management.Automation.ApplicationInfo) for each
file, not a **FileInfo** object (System.IO.FileInfo).

## Example 9: Get cmdlets by using a parameter name and type

This command gets cmdlets that have a parameter whose name includes Auth and whose type is
**AuthenticationMechanism**.

```powershell
Get-Command -ParameterName *Auth* -ParameterType AuthenticationMechanism
```

You can use a command like this one to find cmdlets that let you specify the method that's used to
authenticate the user.

The **ParameterType** parameter distinguishes parameters that take an **AuthenticationMechanism**
value from those that take an **AuthenticationLevel** parameter, even when they have similar names.

## Example 10: Get an alias

This example shows how to use the `Get-Command` cmdlet with an alias.

```powershell
Get-Command -Name dir
```

```Output
CommandType     Name                                               ModuleName
-----------     ----                                               ----------
Alias           dir -> Get-ChildItem
```

Although it's typically used on cmdlets and functions, `Get-Command` also gets scripts, functions,
aliases, and executable files.

The output of the command shows the special view of the **Name** property value for aliases. The
view shows the alias and the full command name.

## Example 11: Get Syntax from an alias

This example shows how to get the syntax along with the standard name of an alias.

The output of the command shows the labeled alias with the standard name, followed by the syntax.

```powershell
Get-Command -Name dir -Syntax
```

```Output
dir (alias) -> Get-ChildItem

dir [[-Path] <string[]>] [[-Filter] <string>] [-Include <string[]>] [-Exclude <string[]>] [-Recurse]
[-Depth <uint>] [-Force] [-Name] [-Attributes <FlagsExpression[FileAttributes]>] [-FollowSymlink]
[-Directory] [-File] [-Hidden] [-ReadOnly] [-System] [<CommonParameters>]

dir [[-Filter] <string>] -LiteralPath <string[]> [-Include <string[]>] [-Exclude <string[]>] [-Recurse]
[-Depth <uint>] [-Force] [-Name] [-Attributes <FlagsExpression[FileAttributes]>] [-FollowSymlink]
[-Directory] [-File] [-Hidden] [-ReadOnly] [-System] [<CommonParameters>]
```

## Example 12: Get all instances of the Notepad command

This example uses the **All** parameter of the `Get-Command` cmdlet to show all instances of the
`Notepad` command on the local computer.

```powershell
Get-Command Notepad -All | Format-Table CommandType, Name, Definition
```

```Output
CommandType     Name           Definition
-----------     ----           ----------
Application     notepad.exe    C:\WINDOWS\system32\notepad.exe
Application     NOTEPAD.EXE    C:\WINDOWS\NOTEPAD.EXE
```

The **All** parameter is useful when there is more than one command with the same name in the
session.

Beginning in Windows PowerShell 3.0, by default, when the session includes multiple commands with
the same name, `Get-Command` gets only the command that runs when you type the command name. With
the **All** parameter, `Get-Command` gets all commands with the specified name and returns them in
execution precedence order. To run a command other than the first one in the list, type the fully
qualified path to the command.

For more information about command precedence, see
[about_Command_Precedence](About/about_Command_Precedence.md).

## Example 13: Get the name of a module that contains a cmdlet

This command gets the name of the module in which the `Get-Date` cmdlet originated.
The command uses the **ModuleName** property of all commands.

```powershell
(Get-Command Get-Date).ModuleName
```

```Output
Microsoft.PowerShell.Utility
```

This command format works on commands in PowerShell modules, even if they're not imported into the
session.

## Example 14: Get cmdlets and functions that have an output type

```powershell
Get-Command -Type Cmdlet | Where-Object OutputType | Format-List -Property Name, OutputType
```

This command gets the cmdlets and functions that have an output type and the type of objects that
they return.

The first part of the command gets all cmdlets. A pipeline operator (`|`) sends the cmdlets to the
`Where-Object` cmdlet, which selects only the ones in which the **OutputType** property is
populated. Another pipeline operator sends the selected cmdlet objects to the `Format-List` cmdlet,
which displays the name and output type of each cmdlet in a list.

The **OutputType** property of a **CommandInfo** object has a non-null value only when the cmdlet
code defines the **OutputType** attribute for the cmdlet.

## Example 15: Get cmdlets that take a specific object type as input

```powershell
Get-Command -ParameterType (((Get-NetAdapter)[0]).pstypenames)
```

```Output
CommandType     Name                                               ModuleName
-----------     ----                                               ----------
Function        Disable-NetAdapter                                 NetAdapter
Function        Enable-NetAdapter                                  NetAdapter
Function        Rename-NetAdapter                                  NetAdapter
Function        Restart-NetAdapter                                 NetAdapter
Function        Set-NetAdapter                                     NetAdapter
```

This command finds cmdlets that take net adapter objects as input. You can use this command format
to find the cmdlets that accept the type of objects that any command returns.

The command uses the **pstypenames** intrinsic property of all objects, which gets the types that
describe the object. To get the **pstypenames** property of a net adapter, and not the
**pstypenames** property of a collection of net adapters, the command uses array notation to get the
first net adapter that the cmdlet returns.

## Example 16: Get commands using a fuzzy match

In this example, the name of the command deliberately has a typo as 'get-commnd'. Using the
`-UseFuzzyMatching` switch, the cmdlet determined that the best match was `Get-Command` followed by
other native commands on the system that were a similar match.

```powershell
Get-Command get-commnd -UseFuzzyMatching
```

```Output
CommandType     Name             Version    Source
-----------     ----             -------    ------
Cmdlet          Get-Command      6.2.0.0    Microsoft.PowerShell.Core
Application     getconf          0.0.0.0    /usr/bin/getconf
Application     command          0.0.0.0    /usr/bin/command
```

