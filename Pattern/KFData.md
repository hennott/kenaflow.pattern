# KFData
kenaflow can store information about in a seperate list which is accessible for multiple workflows. The Data-Object is stored as CLIXML (for backend) and JSON (for frontend) under the Key.

## Set data in list context
> `Set-KFData -Key <key> -Data <object>`

## Get data in list context
> `Get-KFData -Key <key>`

# KFItemData
This comand stores information in item context to be accessible for other workflows.

## Set data in item context
> `Set-KFItemData -Key <key> -Data <object> [-Item <list-itemobjekt>]`

## Get data in item context
> `Get-KFItemData -Key <key> [-Item <list-item-objekt>]`