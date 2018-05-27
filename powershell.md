<!-- TITLE: Powershell -->
<!-- SUBTITLE: Stuff PowerShell -->

# Base

Je ne sais pas quoi mettre encore, ça va venir !


```powershell
Get-Idea
```


-----


# No-IP Updates

```powershell
(Invoke-WebRequest https://itomation.ca/mypublicip).content
(tnc ichihome.ddns.net).RemoteAddress.IPAddressToString
$update=(Invoke-WebRequest ('https://dynupdate.no-ip.com/nic/update?hostname='+$HostRecord + '&myip='+$IPAddress) -Credential $Cred).content 
```


-----


# Backup Mongo DB
```powershell
$mongodump = 'C:\Program Files\MongoDB\Server\3.6\bin\mongodump.exe'
&$mongodump /h 'ds243008.mlab.com' /port:43008 /d malmongo /u $($cred.UserName) /p $($cred.GetNetworkCredential().password) /o D:\Backup\Mongo
```


-----


# Create Scheduled Tasks
2 ways to do it :
1/
```powershell
$action = New-ScheduledTaskAction -Execute 'Powershell.exe' `
-Argument '-NoProfile -WindowStyle Hidden -command "& {get-eventlog -logname Application -After ((get-date).AddDays(-1)) | Export-Csv -Path c:\fso\applog.csv -Force -NoTypeInformation}"'
$trigger =  New-ScheduledTaskTrigger -Daily -At 9am
Register-ScheduledTask -Action $action -Trigger $trigger -TaskName "AppLog" -Description "Daily dump of Applog"
```

2/
```powershell
$A = New-ScheduledTaskAction –Execute "Taskmgr.exe"
$T = New-ScheduledTaskTrigger -AtLogon
$P = "Contoso\Administrator"
$S = New-ScheduledTaskSettingsSet
$D = New-ScheduledTask -Action $A -Principal $P -Trigger $T -Settings $S
Register-ScheduledTask T1 -InputObject $D
```

# VS Code - PSScriptAnalyzer
Tips pour VS Code & les règles PSSCriptAnalyzer

PSScriptAnalyzer integration
The PowerShell extension utilizes the PSScriptAnalyzer module to provide background analysis of your scripts to let you know where you may run into problems. Script analysis errors and warnings will appear in your code as green squiggles. Some rules even have a suggested Code Fix as shown in the following screenshot.

You can configure the settings for PSScriptAnalyzer in two ways. First, you can use a PowerShell extension command and UI to configure which rules to execute. To do so, open the Command Palette by pressing Ctrl + Shift + P (Cmd + Shift + P on Mac), and type PowerShell: **Select PSSc**, which should be enough to find the command for selecting **PSScriptAnalyzer rules**. Press Enter to invoke the command, which will display the rule list shown in the following screenshot. You can then select which rules to enable or disable.

The other way to configure PSScriptAnalyzer is via a script analyzer settings file that’s typically called PSScriptAnalyzerSettings.psd1. See the example settings file with the same name that ships with the PowerShell extension. It is located in the $Home\.vscode\extensions\ms-vscode.PowerShell-0.8.0\examples folder. Copy this file to the root of your workspace, and then create a settings.json file (if it doesn’t exist) under the .vscode folder in the root of your workspace. Edit that file and add the following line between the curly braces:

{
"powershell.scriptAnalysis.settingsPath": "PSScriptAnalyzerSettings.psd1"
}

This will configure Visual Studio Code to use the PSScriptAnalyzerSettings.psd1 file in the root of your workspace folder to determine which rules to execute.
(Source : https://blogs.technet.microsoft.com/heyscriptingguy/2017/01/12/visual-studio-code-editing-features-for-powershell-development-part-2/ )

# Export Scheduled Tasks
```
> Get-ScheduledTask -TaskPath '\MAL\' | % {
$fn = 'D:\Backup\SchedTasks\' + $_.TaskName + '.xml'
Export-ScheduledTask -TaskName $_.TaskName -TaskPath $_.TaskPath | Out-File $fn}
```