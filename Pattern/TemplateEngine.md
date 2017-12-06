# The powerful template engine

## How to use
> `Invoke-KFTemplate -Template <string>  [-LocalConfig <object>] [-Item <sharepoint-list-item-object>]`

example with the template defined in the WFconfig-List with the key "tpl.Mail":
> `Invoke-KFTemplate -Template $config['tpl.Mail']`

example with an local config:
> `$cfg = @(@{"Responder":"Me"})`
> `Invoke-KFTemplate -Template $config['tpl.Mail'] -Config $cfg`

# All about the template

## Wildcards
> `{{item-internal-fieldname}}`
> `[[config-key]]`
> `((local-key))`

## Special features
- "user"-field 
> `{{item-internal-fieldname|<formater>}}`
	- nothing > display name
	- id > local user id
- "date"-field
> `{{item-internal-fieldname|<formater>}}`
	- nothing > yyyy-MM-dd
	- look at https://msdn.microsoft.com/de-de/library/az4se3k1(v=vs.110).aspx

