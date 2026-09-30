Selects objects or object properties.

## Example 1: Select objects by property

This example creates objects that have the **Name**, **Id**, and working set (**WS**) properties of
process objects.

```powershell
Get-Process | Select-Object -Property ProcessName, Id, WS
```

## Example 2: Select objects by property and format the results

This example gets information about the modules used by the processes on the computer. It uses
`Get-Process` cmdlet to get the process on the computer.

It uses the `Select-Object` cmdlet to output an array of `[System.Diagnostics.ProcessModule]`
instances as contained in the **Modules** property of each `System.Diagnostics.Process` instance
output by `Get-Process`.

The **Property** parameter of the `Select-Object` cmdlet selects the process names. This adds a
`ProcessName` **NoteProperty** to every `[System.Diagnostics.ProcessModule]` instance and populates
it with the value of current process's **ProcessName** property.

Finally, `Format-List` cmdlet is used to display the name and modules of each process in a list.

```powershell
Get-Process Explorer 
 | Select-Object -Property ProcessName -ExpandProperty Modules 
 | Format-List
```

```
ProcessName       : explorer
ModuleName        : explorer.exe
FileName          : C:\WINDOWS\explorer.exe
BaseAddress       : 140697278152704
ModuleMemorySize  : 3919872
EntryPointAddress : 140697278841168
FileVersionInfo   : File:             C:\WINDOWS\explorer.exe
                    InternalName:     explorer
                    OriginalFilename: EXPLORER.EXE.MUI
                    FileVersion:      10.0.17134.1 (WinBuild.160101.0800)
                    FileDescription:  Windows Explorer
                    Product:          Microsoft Windows Operating System
                    ProductVersion:   10.0.17134.1
...
```

## Example 3: Select processes using the most memory

This example gets the five processes that are using the most memory. The `Get-Process` cmdlet gets
the processes on the computer. The `Sort-Object` cmdlet sorts the processes according to memory
(working set) usage, and the `Select-Object` cmdlet selects only the last five members of the
resulting array of objects.

The **Wait** parameter isn't required in commands that include the `Sort-Object` cmdlet because
`Sort-Object` processes all objects and then returns a collection. The `Select-Object` optimization
is available only for commands that return objects individually as they're processed.

```powershell
Get-Process | Sort-Object -Property WS | Select-Object -Last 5
```

```Output
Handles  NPM(K)    PM(K)      WS(K) VS(M)   CPU(s)     Id ProcessName
-------  ------    -----      ----- -----   ------     ----
2866     320       33432      45764   203   222.41   1292 svchost
577      17        23676      50516   265    50.58   4388 WINWORD
826      11        75448      76712   188    19.77   3780 Ps
1367     14        73152      88736   216    61.69    676 Ps
1612     44        66080      92780   380   900.59   6132 INFOPATH
```

## Example 4: Select unique characters from an array

This example uses the **Unique** parameter of `Select-Object` to get unique characters from an array
of characters.

```powershell
"a","b","c","a","A","a" | Select-Object -Unique
```

```Output
a
b
c
A
```

## Example 5: Using `-Unique` with other parameters

The **Unique** parameter filters values after other `Select-Object` parameters are applied. For
example, if you use the **First** parameter to select the first number of items in an array,
**Unique** is only applied to the selected values and not the entire array.

```powershell
"a","a","b","c" | Select-Object -First 2 -Unique
```

```Output
a
```

In this example, **First** selects `"a","a"` as the first 2 items in the array. **Unique** is
applied to `"a","a"` and returns `a` as the unique value.

## Example 6: Select unique strings using the `-CaseInsensitive` parameter

This example uses case-insensitive comparisons to get unique strings from an array of strings.

```powershell
"aa", "Aa", "Bb", "bb" | Select-Object -Unique -CaseInsensitive
```

```Output
aa
Bb
```

## Example 7: Select newest and oldest events in the event log

This example gets the first (newest) and last (oldest) events in the Windows PowerShell event log.

`Get-WinEvent` gets all events in the Windows PowerShell log and saves them in the `$a` variable.
Then, `$a` is piped to the `Select-Object` cmdlet. The `Select-Object` command uses the **Index**
parameter to select events from the array of events in the `$a` variable. The index of the first
event is 0. The index of the last event is the number of items in `$a` minus 1.

```powershell
$a = Get-WinEvent -LogName "Windows PowerShell"
$a | Select-Object -Index 0, ($a.Count - 1)
```

## Example 8: Select all but the first object

This example creates a new PSSession on each of the computers listed in the Servers.txt files,
except for the first one.

`Select-Object` selects all but the first computer in a list of computer names. The resulting list
of computers is set as the value of the **ComputerName** parameter of the `New-PSSession` cmdlet.

```powershell
New-PSSession -ComputerName (Get-Content Servers.txt | Select-Object -Skip 1)
```

## Example 9: Rename files and select several to review

This example adds a "-ro" suffix to the base names of text files that have the read-only attribute
and then displays the first five files so the user can see a sample of the effect.

`Get-ChildItem` uses the **ReadOnly** dynamic parameter to get read-only files. The resulting files
are piped to the `Rename-Item` cmdlet, which renames the file. It uses the **PassThru** parameter of
`Rename-Item` to send the renamed files to the `Select-Object` cmdlet, which selects the first 5 for
display.

The **Wait** parameter of `Select-Object` prevents PowerShell from stopping the `Get-ChildItem`
cmdlet after it gets the first five read-only text files. Without this parameter, only the first
five read-only files would be renamed.

```powershell
Get-ChildItem *.txt -ReadOnly |
    Rename-Item -NewName {$_.BaseName + "-ro.txt"} -PassThru |
    Select-Object -First 5 -Wait
```

## Example 10: Show the intricacies of the -ExpandProperty parameter

This example shows the intricacies of the **ExpandProperty** parameter.

Note that the output generated was an array of `[System.Int32]` instances. The instances conform to
standard formatting rules of the **Output View**. This is true for any _Expanded_ properties. If the
outputted objects have a specific standard format, the expanded property might not be visible.

```powershell
# Create a custom object to use for the Select-Object example.
$object = [pscustomobject]@{Name="CustomObject";List=@(1,2,3,4,5)}
# Use the ExpandProperty parameter to Expand the property.
$object | Select-Object -ExpandProperty List -Property Name
```

```
1
2
3
4
5
```

```powershell
# The output did not contain the Name property, but it was added successfully.
# Use Get-Member to confirm the Name property was added and populated.
$object | Select-Object -ExpandProperty List -Property Name | Get-Member -MemberType Properties
```

```Output
   TypeName: System.Int32

Name        MemberType   Definition
----       -  -
Name        NoteProperty string Name=CustomObject
```

## Example 11: Create custom properties on objects

The following example demonstrates using `Select-Object` to add a custom property to any object.
When you specify a property name that doesn't exist, `Select-Object` creates that property as a
**NoteProperty** on each object passed.

```powershell
$customObject = 1 | Select-Object -Property MyCustomProperty
$customObject.MyCustomProperty = "New Custom Property"
$customObject
```

```Output
MyCustomProperty
----------------
New Custom Property
```

## Example 12: Create calculated properties for each InputObject

This example demonstrates using `Select-Object` to add calculated properties to your input. Passing
a **ScriptBlock** to the **Property** parameter causes `Select-Object` to evaluate the expression on
each object passed and add the results to the output. Within the **ScriptBlock**, you can use the
`$_` variable to reference the current object in the pipeline.

By default, `Select-Object` uses the **ScriptBlock** string as the name of the property. Using a
**Hashtable**, you can label the output of your **ScriptBlock** as a custom property added to each
object. You can add multiple calculated properties to each object passed to `Select-Object`.

```powershell
# Create a calculated property called $_.StartTime.DayOfWeek
Get-Process | Select-Object -Property ProcessName,{$_.StartTime.DayOfWeek}
```

```Output
ProcessName  $_.StartTime.DayOfWeek
----        -------------
alg                       Wednesday
ati2evxx                  Wednesday
ati2evxx                   Thursday
...
```

```powershell
# Add a custom property to calculate the size in KiloBytes of each FileInfo
# object you pass in. Use the pipeline variable to divide each file's length by
# 1 KiloBytes
$size = @{Label="Size(KB)";Expression={$_.Length/1KB}}
# Create an additional calculated property with the number of Days since the
# file was last accessed. You can also shorten the key names to be 'l', and 'e',
# or use Name instead of Label.
$days = @{l="Days";e={((Get-Date) - $_.LastAccessTime).Days}}
# You can also shorten the name of your label key to 'l' and your expression key
# to 'e'.
Get-ChildItem $PSHOME -File | Select-Object Name, $size, $days
```

```Output
Name                        Size(KB)        Days
----                        --------        ----
Certificate.format.ps1xml   12.5244140625   223
Diagnostics.Format.ps1xml   4.955078125     223
DotNetTypes.format.ps1xml   134.9833984375  223
```

## Example 13: Select hashtable keys without using calculated properties

Beginning in PowerShell 6, `Select-Object` supports selecting the keys of **hashtable** input as
properties. The following example selects the `weight` and `name` keys on an input hashtable and
displays the output.

```powershell
@{ name = 'a' ; weight = 7 } | Select-Object -Property name, weight
```

```output
name weight
---- ------
a         7
```

## Example 14: ExpandProperty alters the original object

This example demonstrates the side-effect of using the **ExpandProperty** parameter. When you use
**ExpandProperty**, `Select-Object` adds the selected properties to the original object as
**NoteProperty** members.

```powershell
PS> $object = [pscustomobject]@{
    name = 'USA'
    children = [pscustomobject]@{
        name = 'Southwest'
    }
}
PS> $object

name children
---- --------
USA  @{name=Southwest}

# Use the ExpandProperty parameter to expand the children property
PS> $object | Select-Object @{n="country"; e={$_.name}} -ExpandProperty children

name      country
----      -------
Southwest USA

# The original object has been altered
PS> $object

name children
---- --------
USA  @{name=Southwest; country=USA}
```

As you can see, the **country** property was added to the **children** object after using the
**ExpandProperty** parameter.

## Example 15: Create a new object with expanded properties without altering the input object

You can avoid the side-effect of using the **ExpandProperty** parameter by creating a new object and
copying the properties from the input object.

```powershell
PS> $object = [pscustomobject]@{
    name = 'USA'
    children = [pscustomobject]@{
        name = 'Southwest'
    }
}
PS> $object

name children
---- --------
USA  @{name=Southwest}

# Create a new object with selected properties
PS> $newObject = [pscustomobject]@{
    country = $object.name
    children = $object.children
}

PS> $newObject

country children
------- --------
USA     @{name=Southwest}

# $object remains unchanged
PS> $object

name children
---- --------
USA  @{name=Southwest}
```

## Example 16: Use wildcards with the -ExpandProperty parameter

This example demonstrates using wildcards with the **ExpandProperty** parameter. The wildcard
character must resolve to a single property name. If the wildcard character resolves to more than
one property name, `Select-Object` returns an error.

```powershell
# Create a custom object.
$object = [pscustomobject]@{
    Label   = "MyObject"
    Names   = @("John","Jane","Joe")
    Numbers = @(1,2,3,4,5)
}
# Try to expand multiple properties using a wildcard.
$object | Select-Object -ExpandProperty N*
Select-Object: Multiple properties cannot be expanded.

# Use a wildcard that resolves to a single property.
$object | Select-Object -ExpandProperty Na*
John
Jane
Joe
```

## Example 17: Use both First and Last parameters to select a subset of objects

This example demonstrates using both the **First** and **Last** parameters to select a subset of
objects. The command selects the first 3 objects in the array, after skipping 4, and selects the
last 3 objects.

```powershell
1..20 | Select-Object -First 3 -Last 3 -Skip 4
```

```Output
5
6
7
18
19
20
```
