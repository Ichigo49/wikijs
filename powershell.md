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

