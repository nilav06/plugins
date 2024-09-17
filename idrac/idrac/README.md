# IDRAC Monitoring
                                                                                              
## Prerequisites

- Download and install the latest version of the [Site24x7 Linux agent / Site24x7 Windows agent](https://www.site24x7.com/app/client#/admin/inventory/add-monitor) in the server where you plan to run the plugin.

#### Linux 

- Execute the following command in your server to install snmpwalk: 

	- On Centos/RedHat machines you can install snmpwalk using Yum:
 
  			yum install net–snmp–utils

  	- On Ubuntu install snmpwalk using apt-get:
  
  			sudo apt–get install snmp
  
- After installation, export the net-snmp path in the $PATH variable. Example:

  			export PATH=$PATH:/var/lib/net-snmp/bin

- Test SNMP walk for iDrac:
  
  - command:

  			snmpwalk -v <version> -c <community-name> <OID>
  - Example:
  
  			snmpwalk  -v  2c  -c  public  10.19.1.0  1.3.6.1.4.1.674.10892.5.4.600.50.1.5
		
#### Windows

- Follow the steps in [k-base](https://support.site24x7.com/portal/en/kb/articles/idrac-monitoring-for-windows) for iDrac plugins installation

---

### Plugin Installation  

Supported versions: 1 and 2c

- Create a directory named `idrac`
      
- Download all the files in the `idrac` directory.

		wget https://raw.githubusercontent.com/site24x7/plugins/master/idrac/idrac.py
		wget https://raw.githubusercontent.com/site24x7/plugins/master/idrac/idrac.cfg
		wget https://raw.githubusercontent.com/site24x7/plugins/master/idrac/SNMPUtil.py
  

- Execute the below command with appropriate arguments to check for the valid json output:

		python idrac.py --hostname "localhost" --snmp_version "2c" --snmp_community_str "public"

- Provide your idrac configurations in idrac.cfg file.

		[idrac_main]
		hostname = "localhost"
		snmp_version = "2c" 
		snmp_community_str = "public"
		
#### Linux

- Follow the steps in [this article](https://support.site24x7.com/portal/en/kb/articles/updating-python-path-in-a-plugin-script-for-linux-servers) to update the Python path in the idrac.py script.

- Move the directory named `idrac` under the Site24x7 Linux Agent plugin directory: 

		mv idrac /opt/site24x7/monagent/plugins/
		
##### Windows 

- Since it's a Python plugin, to run the plugin in a Windows server please follow the steps in [this link](https://support.site24x7.com/portal/en/kb/articles/run-python-plugin-scripts-in-windows-servers). The remaining configuration steps are the same.

- Move the folder named `idrac` under Site24x7 Windows Agent plugin directory: 

		C:\Program Files (x86)\Site24x7\WinAgent\monitoring\Plugins\
		
The agent will automatically execute the plugin within five minutes and user can see the plugin monitor under Site24x7 > Plugins > Plugin Integrations.

## Supported Metrics

The status for on IDRAC please refer below,
Name	| 	Description
---	|   	---
1 	|	 other
2 	|	 unknown
3 	|	 ok
4 	|	 nonCritical
5 	|	 critical
6 	|	 nonRecoverable

Metric and units:

Name		| 	Description
---		|   	---
rotations	|	rpm
memory	size	|	KB
pdisk size	|	MB
