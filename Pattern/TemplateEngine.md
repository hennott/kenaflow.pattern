# The powerful template engine

# How to use
> `Invoke-KFTemplate `

# Wildcards
> `{{item-internal-fieldname}}`
> `[[config-key]]`
> `((local-key))`

# Special features
- "user"-field 
> `{{item-internal-fieldname|<formater>}}`
	- nothing > display name
	- id > local user id
- "date"-field
> `{{item-internal-fieldname|<formater>}}`
	- nothing > yyyy-MM-dd
	- look at https://msdn.microsoft.com/de-de/library/az4se3k1(v=vs.110).aspx

