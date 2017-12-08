# Most used Practise in nearly 80% of the StateScripts

´´´
param($wf, $states, $web, $item, $eventData, $config)

if($wf-eq$null){import-module "D:\KenaFlow\Engine\kenaflow.runtime.dll";Invoke-Kenaflow;exit}

Set-KFPermission -Permissions @( 
    @{
        User="[[user.Involved]]";
        Quick="RU";
    };
    @{
        User="{{Author}};{{Editor}};{{Person}};"; 
        Quick="CRUMDA";
    };
    @{
        User="markus@sharepoint.farm"; 
        Quick="RA";
    };
    @{
        User="SharePoint Group Visitors"; 
        Quick="R";
    } )

$Body = (Invoke-KFTemplate -Template $config["tpl.Mail"])
Send-KFMail -Body $Body -Subject "<WorkflowKey>: <Subject>" -Addresses "{{Person}};[[Involved]]" -IsHTMLMail

$Protocol = (Invoke-KFTemplate -template "The {{Person}} get involved.")
Set-PnPListItem -List $item.parentlist -Identity $item -Values @{"<internal-field-name>" = $Protocol}

Set-KFState "2_"
´´´
