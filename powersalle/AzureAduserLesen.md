# Vorrsuaussetzungen

MS Graph Installieren
```
Install-Module Microsoft.Graph -Scope CurrentUser
```
Login Azure
```
Connect-MgGraph  
```
Logout Azure
```
Disconnect-MgGraph
```

Userliste Anzeigen
```
Get-MgUser
```

Alle Emails Auslesen ps Script
```
$users = Get-MgUser -All -Property UserPrincipalName,ProxyAddresses

$userlist = foreach ($user in $users) {
    [PSCustomObject]@{
        Name = $user.DisplayName
        Email = $user.UserPrincipalName
        Aliases = $user.ProxyAddresses -join ", "
    }
}

$userlist | Export-Csv -Path "/home/jay/Downloads/Userliste.csv" -NoTypeInformation -Encoding UTF8
```
