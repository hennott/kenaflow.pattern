# How to Debug directly

- Write the following line at the second line of the script file
> `if($wf -eq $null) { import-module "C:\Program Files\kenaflow\kenaflow.runtime.dll";Invoke-kenaflow <SpecialParameters>;exit}`

# Special Parameters
- Enter the Debugging-Mode
> `-Debug`
- Get more information
> `-Verbose`
- Operate only a special item by ID
> `-ItemID`
- After initialising the engine stop with a breakpoint at the beginning of the script
> `-Breakpoint`