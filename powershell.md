<!-- TITLE: Powershell -->
<!-- SUBTITLE: Stuff PowerShell -->

# Base

Je ne sais pas quoi mettre encore, ça va venir !


```powershell
Get-Idea
```


# No-IP Updates

```powershell
(Invoke-WebRequest https://itomation.ca/mypublicip).content
(tnc ichihome.ddns.net).RemoteAddress.IPAddressToString
$update=(Invoke-WebRequest ('https://dynupdate.no-ip.com/nic/update?hostname='+$HostRecord + '&myip='+$IPAddress) -Credential $Cred).content 
```

# Backup Mongo DB
```powershell
$mongodump = 'C:\Program Files\MongoDB\Server\3.6\bin\mongodump.exe'
&$mongodump /h 'ds243008.mlab.com' /port:43008 /d malmongo /u $($cred.UserName) /p $($cred.GetNetworkCredential().password) /o D:\Backup\Mongo
```