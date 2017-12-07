# Set permissions

## Reset permissions
- This is the most used command because it set the permissions like defined no more parameter is needed
> 

- example
```
Reset-KFPermission -Users @(
	@{ 
		User = "<mail>"; 
		Quick = "CRUDMA"
	},
	@{ 
		User = "{{item-internal-fieldname}}"; 
		Quick = "CRUDMA"
	},
	@{ 
		User = "[[config-key]]"; 
		Quick = "CRUDMA"
	},
	@{ 
		User = "((local-config-key))"; 
		Quick = "CRUDMA"
	},
	@{ 
		User = "<name of SP user group>"; 
		Quick = "CRUDMA"
	}
);
```

## Add Permissions
```
Add-KFPermission [-Users] <list-of-users> [-Item <list-item>] [-CopyCurrentPermissions[:$false]] [-BreakPermissionInheritance[:$true]] [-ClearPermissions[:$false]]
```

- example
```
Add-KFPermission -Users @( 
	@{ 
		User = "<user>"; 
		PermissionsSet = "<name> | array of "name"
	}
);
```
```
Add-KFPermission -Users @( 
	@{ 
		User = "<user>"; 
		Quick = "CRUDMA"
	}
);
```

## Remove Permissions
```
Remove-KFPermission [-Users] <list-of-users> [-Item <list-item>] [-CopyCurrentPermissions[:$false]] [-BreakPermissionInheritance[:$true]] [-ClearPermissions[:$false]]
```

## Update Permissions
```
Update-KFPermission -RemoveUsers <list-of-users> -AddUsers <list-of-users> [-Item <list-item>] [-CopyCurrentPermissions[:$false]] [-BreakPermissionInheritance[:$true]] [-ClearPermissions[:$false]
```

## Permissions inheritance
```
Stop-KFPermissionInheritence [-Item <list-item>] [-CopyCurrentPermissions[:$false]]
```

```
Reset-KFPermissionInheritence [-Item <list-item>]
```

