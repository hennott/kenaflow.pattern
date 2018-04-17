# All about configuration of an workflow

**This is still under construction .. be careful!**

## Basis parameters
- Ignore (default: $true) .. set it to $false if the workflow should run
- Platform (default: ) .. set this to your plattform [sp2013|sp2016|spo] this is just for the current workflow
- TBE (default: 30) .. this means that the sheduler checks every 30 seconds the conditions of the workflow
  - you can define the TBE also on every state .. backgroundstates maybe run just once a day to reduce the load

## Special for State Workflow

## Special for List Workflow

## Special parameters
- MaxExecutionTime (default: ) .. this set an interrupt if the workflow runs to long
- ItemCheckTime (default: 60) .. this is a caching property .. the workflow trust that the item hasn´t change within this timeperiod .. after that the workflow check the item befoe operating it
