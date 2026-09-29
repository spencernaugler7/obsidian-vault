Selects objects from a collection based on their property values.

## Example 1: Get stopped services
These commands get a list of all services that are stopped. The `$_` automatic variable represents
each object that's passed to the `Where-Object` cmdlet.

The first command uses the scriptblock format, the second command uses the comparison statement
format. The commands filter the services the same way and return the same output. Only the syntax
is different.

```powershell
Get-Service | Where-Object { $_.Status -eq "Stopped" }
Get-Service | Where-Object Status -EQ "Stopped"
```

## Example 2: Get processes based on working set
These commands list processes that have a working set greater than 250 megabytes (MB). The commands
filter the processes the same way and return the same output. Only the syntax is different.

```powershell
Get-Process | Where-Object { $_.WorkingSet -gt 250MB }
Get-Process | Where-Object WorkingSet -GT 250MB
```

## Example 3: Get processes based on process name
These commands get the processes that have a **ProcessName** property value that begins with the
letter `p`. The `-match` operator and **Match** parameter let you use regular expression matches.

The commands filter the processes the same way and return the same output. Only the syntax is
different.

```powershell
Get-Process | Where-Object { $_.ProcessName -match "^p.*" }
Get-Process | Where-Object ProcessName -Match "^p.*"
```

## Example 4: Use the comparison statement format
This example shows how to use the new comparison statement format of the `Where-Object` cmdlet.

The first command uses the comparison statement format. It doesn't use any aliases and includes the
name for every parameter.

The second command is the more natural use of the comparison command format. The command
substitutes the `where` alias for the `Where-Object` cmdlet name and omits all optional parameter
names.

The commands filter the processes the same way and return the same output. Only the syntax is
different.

```powershell
Get-Process | Where-Object -Property Handles -GE -Value 1000
Get-Process | where Handles -GE 1000
```

## Example 5: Get commands based on properties
This example shows how to write commands that return items that are true or false or have any value
for a specified property. Each example shows both the scriptblock and comparison statement formats
for the command.

The commands filter their input the same way and return the same output. Only the syntax is
different.

```powershell
# Use Where-Object to get commands that have any value for the OutputType
# property of the command. This omits commands that do not have an OutputType
# property and those that have an OutputType property, but no property value.
Get-Command | Where-Object OutputType
Get-Command | Where-Object { $_.OutputType }
```

```powershell
# Use Where-Object to get objects that are containers. This gets objects that
# have the **PSIsContainer** property with a value of $true and excludes all
# others.
Get-ChildItem | Where-Object PSIsContainer
Get-ChildItem | Where-Object { $_.PSIsContainer }
```

```powershell
# Finally, use the -not operator (!) to get objects that are not containers.
# This gets objects that do have the **PSIsContainer** property and those
# that have a value of $false for the **PSIsContainer** property.
Get-ChildItem | Where-Object -Not PSIsContainer
Get-ChildItem | Where-Object { !$_.PSIsContainer }
```

## Example 6: Use multiple conditions
```powershell
Get-Module -ListAvailable | Where-Object {
	($_.Name -notlike "Microsoft*" -and $_.Name -notlike "PS*") -and $_.HelpInfoUri
}
```

This example shows how to create a `Where-Object` command with multiple conditions.

This command gets non-core modules that support the Updatable Help feature. The command uses the
**ListAvailable** parameter of the `Get-Module` cmdlet to get all modules on the computer. A
pipeline operator (`|`) sends the modules to the `Where-Object` cmdlet, which gets modules whose
names don't begin with `Microsoft` or `PS`, and have a value for the **HelpInfoURI** property,
which tells PowerShell where to find updated help files for the module. The `-and` logical operator
connects the comparison statements.

The example uses the scriptblock command format. Logical operators, such as `-and`,`-or`, and
`-not` are valid only in scriptblocks. You can't use them in the comparison statement format of a
`Where-Object` command.

- For more information about PowerShell logical operators, see
  [about_Logical_Operators](./About/about_logical_operators.md).
- For more information about the Updatable Help feature, see
  [about_Updatable_Help](./About/about_Updatable_Help.md).