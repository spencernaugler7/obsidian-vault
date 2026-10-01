Performs an operation against each item in a collection of input objects.

## Example 1: Divide integers in an array

This example takes an array of three integers and divides each one of them by 1024.

```powershell
30000, 56798, 12432 | ForEach-Object -Process {$_/1024}
```

```Output
29.296875
55.466796875
12.140625
```

## Example 2: Get the length of all the files in a directory

This example processes the files and directories in the PowerShell installation directory `$PSHOME`.

```powershell
Get-ChildItem $PSHOME | ForEach-Object -Process {
 if (!$_.PSIsContainer) {$_.Name; $_.Length / 1024; " " }
}
```

If the object isn't a directory, the scriptblock gets the name of the file, divides the value of
its **Length** property by 1024, and adds a space (" ") to separate it from the next entry. The
cmdlet uses the **PSIsContainer** property to determine whether an object is a directory.

## Example 3: Operate on the most recent System events

This example writes the 1000 most recent events from the System event log to a text file. The
current time is displayed before and after processing the events.

```powershell
Get-EventLog -LogName System -Newest 1000 |
 ForEach-Object -Begin {Get-Date} -Process {
  Out-File -FilePath Events.txt -Append -InputObject $_.Message
 } -End {Get-Date}
```

`Get-EventLog` gets the 1000 most recent events from the System event log and pipes them to the
`ForEach-Object` cmdlet. The **Begin** parameter displays the current date and time. Next, the
**Process** parameter uses the `Out-File` cmdlet to create a text file that's named events.txt and
stores the message property of each of the events in that file. Last, the **End** parameter is used
to display the date and time after all the processing has completed.

## Example 4: Change the value of a Registry key

This example changes the value of the **RemotePath** registry entry in all the subkeys under the
`HKCU:\Network` key to uppercase text.

```powershell
Get-ItemProperty -Path HKCU:\Network\* |
  ForEach-Object {
 Set-ItemProperty -Path $_.PSPath -Name RemotePath -Value $_.RemotePath.ToUpper()
  }
```

You can use this format to change the form or content of a registry entry value.

Each subkey in the **Network** key represents a mapped network drive that reconnects at sign on. The
**RemotePath** entry contains the UNC path of the connected drive. For example, if you map the `E:`
drive to `\\Server\Share`, an **E** subkey is created in `HKCU:\Network` with the **RemotePath**
registry value set to `\\Server\Share`.

The command uses the `Get-ItemProperty` cmdlet to get all the subkeys of the **Network** key and the
`Set-ItemProperty` cmdlet to change the value of the **RemotePath** registry entry in each key. In
the `Set-ItemProperty` command, the path is the value of the **PSPath** property of the registry
key. This is a property of the Microsoft .NET Framework object that represents the registry key, not
a registry entry. The command uses the **ToUpper()** method of the **RemotePath** value, which is a
string **REG_SZ**.

Because `Set-ItemProperty` is changing the property of each key, the `ForEach-Object` cmdlet is
required to access the property.

## Example 5: Use the $null automatic variable

This example shows the effect of piping the `$null` automatic variable to the `ForEach-Object`
cmdlet.

```powershell
1, 2, $null, 4 | ForEach-Object {"Hello"}
```

```Output
Hello
Hello
Hello
Hello
```

Because PowerShell treats `$null` as an explicit placeholder, the `ForEach-Object` cmdlet generates
a value for `$null` as it does for other objects piped to it.

## Example 6: Get property values

This example gets the value of the **Path** property of all installed PowerShell modules using
the **MemberName** parameter of the `ForEach-Object` cmdlet.

```powershell
Get-Module -ListAvailable | ForEach-Object -MemberName Path
Get-Module -ListAvailable | foreach Path
```

The second command is equivalent to the first. It uses the `Foreach` alias of the `ForEach-Object`
cmdlet and omits the name of the **MemberName** parameter, which is optional.

The `ForEach-Object` cmdlet is useful for getting property values, because it gets the value without
changing the type, unlike the **Format** cmdlets or the `Select-Object` cmdlet, which change the
property value type.

## Example 7: Split module names into component names

This example shows three ways to split two dot-separated module names into their component names.
The commands call the **Split** method of strings. The three commands use different syntax, but they
are equivalent and interchangeable. The output is the same for all three cases.

```powershell
"Microsoft.PowerShell.Core", "Microsoft.PowerShell.Host" |
 ForEach-Object {$_.Split(".")}
"Microsoft.PowerShell.Core", "Microsoft.PowerShell.Host" |
 ForEach-Object -MemberName Split -ArgumentList "."
"Microsoft.PowerShell.Core", "Microsoft.PowerShell.Host" |
 foreach Split "."
```

```Output
Microsoft
PowerShell
Core
Microsoft
PowerShell
Host
```

The first command uses the traditional syntax, which includes a scriptblock and the current object
operator `$_`. It uses the dot syntax to specify the method and parentheses to enclose the delimiter
argument.

The second command uses the **MemberName** parameter to specify the **Split** method and the
**ArgumentList** parameter to identify the dot (`.`) as the split delimiter.

The third command uses the `foreach` alias of the `ForEach-Object` cmdlet and omits the names of
the **MemberName** and **ArgumentList** parameters, which are optional.

## Example 8: Using ForEach-Object with two scriptblocks

In this example, we pass two scriptblocks positionally. All the scriptblocks bind to the
**Process** parameter. However, they're treated as if they had been passed to the **Begin** and
**Process** parameters.

```powershell
1..2 | ForEach-Object { 'begin' } { 'process' }
```

```Output
begin
process
process
```

## Example 9: Using ForEach-Object with more than two scriptblocks

In this example, we pass four scriptblocks positionally. All the scriptblocks bind to the
**Process** parameter. However, they're treated as if they had been passed to the **Begin**,
**Process**, and **End** parameters.

```powershell
1..2 | ForEach-Object { 'begin' } { 'process A' }  { 'process B' } { 'end' }
```

```Output
begin
process A
process B
process A
process B
end
```

> [!NOTE]
> The first scriptblock is always mapped to the `begin` block, the last block is mapped to the
> `end` block, and the two middle blocks are mapped to the `process` block.

## Example 10: Run multiple scriptblocks for each pipeline item

As shown in the previous example, multiple scriptblocks passed using the **Process** parameter get
mapped to the **Begin** and **End** parameters. To avoid this mapping, you must provide explicit
values for the **Begin** and **End** parameters.

```powershell
1..2 | ForEach-Object -Begin $null -Process { 'one' }, { 'two' }, { 'three' } -End $null
```

```Output
one
two
three
one
two
three
```

## Example 11: Run slow script in parallel batches

This example runs a scriptblock that evaluates a string and sleeps for one second.

```powershell
$Message = "Output:"

1..8 | ForEach-Object -Parallel {
 "$Using:Message $_"
 Start-Sleep 1
} -ThrottleLimit 4
```

```Output
Output: 1
Output: 2
Output: 3
Output: 4
Output: 5
Output: 6
Output: 7
Output: 8
```

The **ThrottleLimit** parameter value is set to 4 so that the input is processed in batches of four.
The `Using:` scope modifier is used to pass the `$Message` variable into each parallel scriptblock.

## Example 12: Retrieve log entries in parallel

This example retrieves 50,000 log entries from 5 system logs on a local Windows machine.

```powershell
$logNames = 'Security', 'Application', 'System', 'Windows PowerShell',
 'Microsoft-Windows-Store/Operational'

$logEntries = $logNames | ForEach-Object -Parallel {
 Get-WinEvent -LogName $_ -MaxEvents 10000
} -ThrottleLimit 5

$logEntries.Count
```

```Output
50000
```

The **Parallel** parameter specifies the scriptblock that's run in parallel for each input log
name. The **ThrottleLimit** parameter ensures that all five scriptblocks run at the same time.

## Example 13: Run in parallel as a job

This example creates a job that runs a scriptblock in parallel, two at a time.

```powershell
PS> $job = 1..10 | ForEach-Object -Parallel {
 "Output: $_"
 Start-Sleep 1
} -ThrottleLimit 2 -AsJob

PS> $job

Id     Name            PSJobTypeName   State         HasMoreData     Location      Command
--     ----            -------------   -----         -----------     --------      -------
23     Job23           PSTaskJob       Running       True            PowerShell    …

PS> $job.ChildJobs

Id     Name            PSJobTypeName   State         HasMoreData     Location      Command
--     ----            -------------   -----         -----------     --------      -------
24     Job24           PSTaskChildJob  Completed     True            PowerShell    …
25     Job25           PSTaskChildJob  Completed     True            PowerShell    …
26     Job26           PSTaskChildJob  Running       True            PowerShell    …
27     Job27           PSTaskChildJob  Running       True            PowerShell    …
28     Job28           PSTaskChildJob  NotStarted    False           PowerShell    …
29     Job29           PSTaskChildJob  NotStarted    False           PowerShell    …
30     Job30           PSTaskChildJob  NotStarted    False           PowerShell    …
31     Job31           PSTaskChildJob  NotStarted    False           PowerShell    …
32     Job32           PSTaskChildJob  NotStarted    False           PowerShell    …
33     Job33           PSTaskChildJob  NotStarted    False           PowerShell    …
```

The **ThrottleLimit** parameter limits the number of parallel scriptblocks running at a time. The
**AsJob** parameter causes the `ForEach-Object` cmdlet to return a job object instead of streaming
output to the console. The `$job` variable receives the job object that collects output data and
monitors running state. The `$job.ChildJobs` property contains the child jobs that run the parallel
scriptblocks.

## Example 14: Using thread safe variable references

This example invokes scriptblocks in parallel to collect uniquely named Process objects.

```powershell
$threadSafeDictionary = [System.Collections.Concurrent.ConcurrentDictionary[string,object]]::new()
Get-Process | ForEach-Object -Parallel {
 $dict = $Using:threadSafeDictionary
 $dict.TryAdd($_.ProcessName, $_)
}

$threadSafeDictionary["pwsh"]
```

```Output
 NPM(K)    PM(M)      WS(M)     CPU(s)      Id  SI ProcessName
 ------    -----      -----     ------      --  -- -----------
  82    82.87     130.85      15.55    2808   2 pwsh
```

A single instance of a **ConcurrentDictionary** object is passed to each scriptblock to collect the
objects. Since the **ConcurrentDictionary** is thread safe, it's safe to be modified by each
parallel script. A non-thread-safe object, such as **System.Collections.Generic.Dictionary**, would
not be safe to use here.

> [!NOTE]
> This example is an inefficient use of **Parallel** parameter. The script adds the input object to
> a concurrent dictionary object. It's trivial and not worth the overhead of invoking each script in
> a separate thread. Running `ForEach-Object` without the **Parallel** switch is more efficient and
> faster. This example is only intended to demonstrate how to use thread safe variables.

## Example 15: Writing errors with parallel execution

This example writes to the error stream in parallel, where the order of written errors is random.

```powershell
1..3 | ForEach-Object -Parallel {
 Write-Error "Error: $_"
}
```

```Output
Write-Error: Error: 1
Write-Error: Error: 3
Write-Error: Error: 2
```

## Example 16: Terminating errors in parallel execution

This example demonstrates a terminating error in one parallel running scriptblock.

```powershell
1..5 | ForEach-Object -Parallel {
 if ($_ -eq 3)
 {
  throw "Terminating Error: $_"
 }

Write-Output "Output: $_"
}
```

```Output
Exception: Terminating Error: 3
Output: 1
Output: 4
Output: 2
Output: 5
```

`Output: 3` is never written because the parallel scriptblock for that iteration was terminated.

> [!NOTE]
> [PipelineVariable](About/about_CommonParameters.md) common parameter variables are _not_
> supported in `ForEach-Object -Parallel` scenarios even with the `Using:` scope modifier.

## Example 17: Passing variables in nested parallel scriptblocks

You can create a variable outside a `ForEach-Object -Parallel` scoped scriptblock and use it inside
the scriptblock with the `Using:` scope modifier. Beginning in PowerShell 7.2, you can create a
variable inside a `ForEach-Object -Parallel` scoped scriptblock and use it inside a nested
scriptblock.

```powershell
$test1 = 'TestA'
1..2 | ForEach-Object -Parallel {
 $Using:test1
 $test2 = 'TestB'
 1..2 | ForEach-Object -Parallel {
  $Using:test2
 }
}
```

```Output
TestA
TestA
TestB
TestB
TestB
TestB
```

> [!NOTE]
> In versions prior to PowerShell 7.2, the nested scriptblock can't access the `$test2` variable and
> an error is thrown.

## Example 18: Creating multiple jobs that run scripts in parallel

The ThrottleLimit parameter limits the number of parallel scripts running during each instance of
`ForEach-Object -Parallel`. It doesn't limit the number of jobs that can be created when using the
**AsJob** parameter. Since jobs themselves run concurrently, it's possible to create multiple
parallel jobs, each running up to the throttle limit number of concurrent scriptblocks.

```powershell
$jobs = for ($i=0; $i -lt 10; $i++) {
 1..10 | ForEach-Object -Parallel {
  ./RunMyScript.ps1
 } -AsJob -ThrottleLimit 5
}

$jobs | Receive-Job -Wait
```

This example creates 10 running jobs. Each job runs no more that 5 scripts concurrently. The total
number of instances running concurrently is limited to 50 (10 jobs times the **ThrottleLimit** of
5).
