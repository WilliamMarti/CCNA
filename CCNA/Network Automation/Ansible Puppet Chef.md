
##### Ansible

- Python
- Agentless
- SSH
- Push Model
- Files
	- Playbooks(YAML)
	- Inventory
	- Templates(Jinja2)
	- Variable(YAML)

##### Puppet

- Ruby
- Agent Based
- Can be run agentless with a proxy
- Puppet server is a "Puppet Master"
- Pull Model
- Use TCP 8140 to communicate to puppet master
- Files
	- Manifest (desired config)
	- Templates (generate manifests)

##### Chef

- Ruby
- Pull Model
- TCP Port 10002
- Files use DSL (Domain Specific Language)
- Files
	- Resources
		- Define config objects
	- Recipes
		- Outline the logic and actions of the tasks to perform
	- Cookbooks
		- A set of related recipes group together
	- Run-Lists
		- An ordered list of recipes that are run to bring a device to the desired config state



