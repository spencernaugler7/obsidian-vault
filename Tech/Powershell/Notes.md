## No pipe char on newline

Initially you might be tempted to write PowerShell pipelines like this

```powershell
Get-ChildItem $targetDir 
	| ForEach-Object { 
		Write-Output "$($_.Name)"
	}
```

this will not work. an error will be shown

```
At C:\Users\spenc\Downloads\blah.ps1:2 char:5                                
+     | ForEach-Object {
+     ~         
An empty pipe element is not allowed.
    + CategoryInfo          : ParserError: (:) [], ParseException
    + FullyQualifiedErrorId : EmptyPipeElement      
```

PowerShell doesn't allow a `|` at the start of a new line

to fix it move the pipe character to the newline

```powershell
Get-ChildItem $targetDir | 
	ForEach-Object { 
		Write-Output "$($_.Name)"
	}
```

___

## PowerShell pipeline continuation

when passing things in a pipeline some commands don't pass objects through the pipeline

example:

```powershell
Get-ChildItem $targetDir | 
	ForEach-Object { 
		Add-Content -Path $logFile -Value "Removing $($_.Name) from storage file was created: $($_.CreationTime), and last updated: $($_.LastWriteTime)" # pipeline ends here add-content doesn't pass the object to the next step
	} | 
	ForEach-Object { Remove-Item -Force $_ }
```

ensure that you add the object to the end of the foreach object to pass it to the next step in the pipeline

```powershell
Get-ChildItem $targetDir | 
	ForEach-Object { 
		Add-Content -Path $logFile -Value "Removing $($_.Name) from storage file was created: $($_.CreationTime), and last updated: $($_.LastWriteTime)" $_ # re-return the object here.
	} | 
	ForEach-Object { Remove-Item -Force $_ }
```
