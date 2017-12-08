# How to bring two lists together

In this case we build up a simple list and attach the workflow as an ListWorkflow but with the "ModifiedState". After adding an item to this list a special ID will be generated "PATTERN_000001" and is set to a field with a link. In another library, a DocSet is created. A document is saved in these and field values are set from the master list item. At the end, a mail is sent to the creator of the item based on a template.

```
param($wf, $web, $item, $config, $eventData)
if($wf-eq$null){import-module "D:\kenaflow\engine\kenaflow.runtime.dll";Invoke-Kenaflow;exit}

$NewId = $item.ID.toString();
$NewId = $NewId.PadLeft(6, '0');
$NewId = "PATTERN_"+$NewId;

Set-PnPListItem -List $item.parentlist -Identity $item -Values @{
    "REF_ID" = $NewId;
    "Link_to_DocSet" = '<a href="<..>/docsethomepage.aspx?FolderCTID=<..>&List=<..>&RootFolder=<..>'+$NewId+'">Link to DocSet</a>'
    }

Add-PnPDocumentSet -List "DocSetFolder" -Name $NewId -ContentType "DocSet"

Copy-PnPFile -TargetUrl "<..>/DocSetFolder/$NewId/Template_$NewId.docx" -SourceUrl "<..>/Template.docx" -Force -Confirm:$false
$RefDocSet = Get-PnPListItem -List "DocSetFolder" -Query "<View><Query><Where><Eq><FieldRef Name='FileLeafRef'/><Value Type='Text'>$NewId</Value></Eq></Where></Query></View>"
Set-PnPListItem -List "DocSetFolder" -Identity $RefDocSet -Values @{
    "REF_ID" = $item['REF_ID'];
    "<internal-field-name>" = $item['<internal-field-name>']
    }

$Body = (Invoke-KFTemplate -template $config["tpl.Mail"])
Send-KFMail -Body $Body -Subject "NewDocSet: Hi your DocSet is ready to use" -Addresses "{{Author}}" -isHTMLMail

Set-KFPermission -Item $RefDocSet -Permissions @( 
    @{
        User="{{Author}}"
        Quick="CRUD";
    })

Set-KFItemModifiedFlag
```
