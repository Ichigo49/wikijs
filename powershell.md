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