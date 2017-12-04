# Global variables

- $wf (available: statemachine, list, site)

- $states (available: statemachine)
	- the list of possible states
	- represents the content of the "WFstates"-list

- $web (available: statemachine, list, site)

- $item (available: statemachine, list)
	- represents the current item

- $config (available: statemachine, list, site)
	- represents the content of the "WFconfig"-list
	- you can extend the config with temporary entries but be careful in case of overriding

- $eventData (available: statemachine, list, site)