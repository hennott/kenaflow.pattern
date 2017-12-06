# Change the Context
One of the major features of kenaflow is the consistent context given for an item. But there is a way to break out. This can be nessecary if you would change the domain to request "cross-site" what is vorbidden by default.

## Build an isolated Script
> `Invoke-KFIsolated -ScriptBlock <powershell-scriptblock-object>  -SharePointVersion "[sp2013|sp2016|spo]" [-Arguments <powershellhashtable-object>]`
