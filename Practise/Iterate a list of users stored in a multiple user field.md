# How to work through a list of people in sequence

Sometimes it is necessary to process a list of users in order, for example, to send a mail and wait for input. This is exactly what this example does.

```
# Collect the two user fields
$NextUsers = $item["PesonsToInform"]
$ReadyUsers = $item["InformedPersons"]
$NextUsers = ([Microsoft.SharePoint.Client.FieldUserValue[]]$NextUsers)
$ReadyUsers = ([Microsoft.SharePoint.Client.FieldUserValue[]]$ReadyUsers)

if( $NextUsers.Count -gt 0) {
    $CurrentUser = $NextUsers[0]
    $CurrentUserInfo = Get-KFUserInfo -UserFieldValue $CurrentUser

    $Body = (Invoke-KFTemplate -template $config["tpl.Mail"])
    Send-KFMail -Body $Body -Subject "Workflow: Request for Feedback" -Addresses $CurrentUserInfo.email -isHTMLMail

    Set-KFPermission -Permissions @(
    @{
        User="[[user.AllwaysInvolved]]"; 
        Quick="RUD";
    };
    @{
        User="{{Author}}"; 
        Quick="R";
    };
    @{
        User=$CurrentUserInfo.email; 
        Quick="RU";
    }) 
    
    $NewNextUsers = [System.Collections.ArrayList]$NextUsers
    $NewNextUsers.RemoveAt(0)
    $NewReadyUsers = [System.Collections.ArrayList]$ReadyUsers
    if( $NewReadyUsers -eq $null ) { 
        $NewReadyUsers = New-Object System.Collections.ArrayList 
    }
    $NewReadyUsers.Add($CurrentUser)

    $item["PesonsToInform"] = ([Microsoft.SharePoint.Client.FieldUserValue[]]$NewNextUsers)
    $item["InformedPersons"] = ([Microsoft.SharePoint.Client.FieldUserValue[]]$NewReadyUsers)
    $item.update()
    
    # Wait for Input
    Set-KFState "1._"
} else {
    # Next step in the process
    Set-KFState "1.1"
}
```
