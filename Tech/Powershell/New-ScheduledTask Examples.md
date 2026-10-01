Creates a scheduled task instance.

## Example 1: Define a scheduled task and register it at a later time

```powershell
PS C:\> $action = New-ScheduledTaskAction -Execute "Taskmgr.exe"
PS C:\> $trigger = New-ScheduledTaskTrigger -AtLogon
PS C:\> $principal = "Contoso\Administrator"
PS C:\> $settings = New-ScheduledTaskSettingsSet
PS C:\> $task = New-ScheduledTask -Action $action -Principal $principal -Trigger $trigger -Settings $settings
PS C:\> Register-ScheduledTask T1 -InputObject $task
```

In this example, the set of commands uses several cmdlets and variables to define and then register a scheduled
task.

The first command uses the **New-ScheduledTaskAction** cmdlet to assign the executable file `tskmgr.exe` to the
variable `$action`.

The second command uses the **New-ScheduledTaskTrigger** cmdlet to assign the value `AtLogon` to the variable
`$trigger`.

The third command assigns the principal of the scheduled task `Contoso\Administrator` to the variable `$principal`.

The fourth command uses the **New-ScheduledTaskSettingsSet** cmdlet to assign a task settings object to the
variable `$settings`.

The fifth command creates a new task and assigns the task definition to the variable `$task`.

The sixth command (hypothetically) runs at a later time.
It registers the new scheduled task and defines it by using the `$task` variable.

## Example 2: Define a scheduled task with multiple actions

```powershell
PS C:\> $actions = (New-ScheduledTaskAction –Execute 'foo.ps1'), (New-ScheduledTaskAction –Execute 'bar.ps1')
PS C:\> $trigger = New-ScheduledTaskTrigger -Daily -At '9:15 AM'
PS C:\> $principal = New-ScheduledTaskPrincipal -UserId 'DOMAIN\user' -RunLevel Highest
PS C:\> $settings = New-ScheduledTaskSettingsSet -RunOnlyIfNetworkAvailable -WakeToRun
PS C:\> $task = New-ScheduledTask -Action $actions -Principal $principal -Trigger $trigger -Settings $settings

PS C:\> Register-ScheduledTask 'baz' -InputObject $task

```

This example creates and registers a scheduled task that runs two PowerShell scripts daily at 09:15 AM.
