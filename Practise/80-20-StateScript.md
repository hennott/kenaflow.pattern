# Most used Practise in nearly 80% of the StateScripts

```
param($wf, $states, $web, $item, $eventData, $config)

if($wf-eq$null){import-module "D:\KenaFlow\Engine\kenaflow.runtime.dll";Invoke-Kenaflow;exit}

Set-KFPermission -Permissions @( 
    @{
        # Use [[<key>]] for a key-value-pair stored in the WFconfig
        User="[[user.Involved]]";
        # Use Quick to be as fast and transparent as possible
        # C-Create, R-Read, U-Update, D-Delete, M-Manage, A-Approve
        Quick="RU";
    };
    @{
        # Use a list of {{<internal-field-name>}}
        User="{{Author}};{{Editor}};{{Person}};"; 
        Quick="CRUMDA";
    };
    @{
        # Set a user by it´s mail address
        User="markus@sharepoint.farm"; 
        # Use the name of a permissionset to have the flexebility you need
        PermissionSet="Readers";
    };
    @{
        # Set permissions to a SharePoint group by the name of the group
        User="SharePoint Group Visitors"; 
        Quick="R";
    } )

# Write a mail based on a template stored in the WFconfig list
$Body = (Invoke-KFTemplate -Template $config["tpl.Mail"])
# I reccomend you to use a <WorkflowKey which is the first part of the subject. It´s easier to handle the mail
Send-KFMail -Body $Body -Subject "<WorkflowKey>: <Subject>" -Addresses "{{Person}};[[Involved]]" -IsHTMLMail

# Use the TemplateEngine in place and attach a portocol information to special field 
$Protocol = (Invoke-KFTemplate -template "The {{Person}} get involved.")
Set-PnPListItem -List $item.parentlist -Identity $item -Values @{"<internal-field-name>" = $Protocol}

# At the end you can change the state
Set-KFState "2_"
```
