Displays information about PowerShell commands and concepts.

## Example 1: Display basic help information about a cmdlet

These examples display basic help information about the `Format-Table` cmdlet.

```powershell
Get-Help Format-Table
Get-Help -Name Format-Table
Format-Table -?
```

`Get-Help <cmdlet-name>` is the simplest and default syntax of `Get-Help` cmdlet. You can omit the
**Name** parameter.

The syntax `<cmdlet-name> -?` works only for cmdlets.

## Example 2: Display basic information one page at a time

These examples display basic help information about the `Format-Table` cmdlet one page at a time.

```powershell
help Format-Table
man Format-Table
Get-Help Format-Table | Out-Host -Paging
```

`help` is a function that runs `Get-Help` cmdlet internally and displays the result one page at a
time.

`man` is an alias for the `help` function.

`Get-Help Format-Table` sends the object down the pipeline. `Out-Host -Paging` receives the output
from the pipeline and displays it one page at a time. For more information, see
[Out-Host](Out-Host.md).

## Example 3: Display more information for a cmdlet

These examples display more detailed help information about the `Format-Table` cmdlet.

```powershell
Get-Help Format-Table -Detailed
Get-Help Format-Table -Full
```

The **Detailed** parameter displays the help article's detailed view that includes parameter
descriptions and examples.

The **Full** parameter displays the help article's full view that includes parameter descriptions,
examples, input and output object types, and additional notes.

The **Detailed** and **Full** parameters are effective only for the commands that have help files
installed on the computer. The parameters aren't effective for the conceptual (**about_**) help
articles.

## Example 4: Display selected parts of a cmdlet by using parameters

These examples display selected portions of the `Format-Table` cmdlet help.

```powershell
Get-Help Format-Table -Examples
Get-Help Format-Table -Parameter *
Get-Help Format-Table -Parameter GroupBy
```

The **Examples** parameter displays the help file's **NAME** and **SYNOPSIS** sections, and all the
Examples. You can't specify an Example number because the **Examples** parameter is a `[switch]`
parameter.

The **Parameter** parameter displays only the descriptions of the specified parameters. If you
specify only the asterisk (`*`) wildcard character, it displays the descriptions of all parameters.
When **Parameter** specifies a parameter name such as **GroupBy**, information about that parameter
is shown.

These parameters aren't effective for the conceptual (**about_**) help articles.

## Example 5: Display online version of help

This example displays the online version of the help article for the `Format-Table` cmdlet in your
default web browser.

```powershell
Get-Help Format-Table -Online
```

## Example 6: Display help about the help system

The `Get-Help` cmdlet without parameters displays information about the PowerShell help system.

```powershell
Get-Help
```

## Example 7: Display available help articles

This example displays a list of all help articles available on your computer.

```powershell
Get-Help *
```

## Example 8: Display a list of conceptual articles

This example displays a list of the conceptual articles included in PowerShell help. All these
articles begin with the characters **about_**. To display a particular help file, type
`Get-Help \<about_article-name\>`, for example, `Get-Help about_Signing`.

Only the conceptual articles that have help files installed on your computer are displayed. For
information about downloading and installing help files in PowerShell 3.0, see
[Update-Help](Update-Help.md).

```powershell
Get-Help about_*
```

## Example 9: Search for a word in cmdlet help

This example shows how to search for a word in a cmdlet help article.

```powershell
Get-Help Add-Member -Full | Out-String -Stream | Select-String -Pattern Clixml
```

```Output
the Export-Clixml cmdlet to save the instance of the object, including the additional members...
can use the Import-Clixml cmdlet to re-create the instance of the object from the information...
Export-Clixml
Import-Clixml
```

`Get-Help` uses the **Full** parameter to get help information for `Add-Member` and returns a
**MamlCommandHelpInfo**. `Out-String` uses the **Stream** parameter to convert the object into a
string. `Select-String` uses the **Pattern** parameter to search the string for **Clixml**.

## Example 10: Display a list of articles that include a word

This example displays a list of articles that include the word **remoting**.

When you enter a word that doesn't appear in any article title, `Get-Help` displays a list of
articles that include that word.

```powershell
Get-Help -Name remoting
```

```Output
Name                              Category  Module                    Synopsis
----                              --------  ------                    --------
Install-PowerShellRemoting.ps1    External                            Install-PowerShellRemoting.ps1
Disable-PSRemoting                Cmdlet    Microsoft.PowerShell.Core Prevents remote users...
Enable-PSRemoting                 Cmdlet    Microsoft.PowerShell.Core Configures the computer...
```

## Example 11: Display provider-specific help

This example shows two ways of getting the provider-specific help for `Get-Item`. These commands get
help that explains how to use the `Get-Item` cmdlet in the PowerShell SQL Server provider's
**DataCollection** node.

The first example uses the `Get-Help` **Path** parameter to specify the SQL Server provider's path.
Because the provider's path is specified, you can run the command from any path location.

The second example uses `Set-Location` to navigate to the SQL Server provider's path. From that
location, the **Path** parameter isn't needed for `Get-Help` to get the provider-specific help.

```powershell
Get-Help Get-Item -Path SQLSERVER:\DataCollection
```

```Output
NAME

Get-Item

SYNOPSIS

Gets a collection of Server objects for the local computer and any computers

to which you have made a SQL Server PowerShell connection.
 ...
```

```powershell
Set-Location SQLSERVER:\DataCollection
SQLSERVER:\DataCollection> Get-Help Get-Item
```

```Output
NAME

Get-Item

SYNOPSIS

Gets a collection of Server objects for the local computer and any computers

to which you have made a SQL Server PowerShell connection.
 ...
```

## Example 12: Display help for a script

This example gets help for the `MyScript.ps1 script`. For information about how to write help for
your functions and scripts, see [about_Comment_Based_Help](About/about_Comment_Based_Help.md).

```powershell
Get-Help -Name C:\PS-Test\MyScript.ps1
```
