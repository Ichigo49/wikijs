<!-- TITLE: Powershell -->
<!-- SUBTITLE: Sample code -->

# Powershell my love! 


```powershell
[CmdletBinding()]
param([String[]]$Aliases)

$RegKey = "HKLM:\SYSTEM\CurrentControlSet\Services\lanmanserver\parameters"
#Allow other machines to access share using aliases
Write-Verbose "Setting DisableStrictNameChecking value to '1'"
Set-ItemProperty -Path $RegKey -Name DisableStrictNameChecking -Value 1 -PropertyType "Dword" -force | Out-Null

if ($null -ne $Aliases) {
    Write-Verbose "Setting OptionalNames value to '$Aliases'"
    #Allow File Server to access shares locally using aliases
    Set-ItemProperty -Path $RegKey -Name OptionalNames -Value $Aliases -PropertyType "MultiString" -force | Out-Null
}
```
