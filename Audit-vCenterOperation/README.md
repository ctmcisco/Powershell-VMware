##Description :


This module contains 1 cmdlet : **Audit-vCenterOperation**.  
It requires PowerShell version 3 (or later) and PowerCLI 5.5 (or later).


##Audit-vCenterOperation :



Obtains vCenter events and filters them to meaningful vCenter operations.
It can filter the operations on a start date, an end date, the user who initiated the operations, 
the vCenter object(s) targeted by the operation, and the type of operations.

It outputs relevant vCenter events and user-friendly information from these events.
Also, for the VM "reconfigure" operations, the property "NewConfigSettings" contains the changed VM setting(s) and the new value.

By default, the operations are sorted in chronological order to facilitate auditing and historical 
tracking of events or configuration changes.

###Parameters :


**VIServer :** To specify the vCenter Server to connect PowerCLI to.
The default is Localhost.  
If not specified, it defaults to localhost .


**Entity :** To filter the operations down to those which targeted the specified vCenter inventory object(s).
It needs to be one or more PowerCLI object(s) representing one or more VM(s), VMHost(s), cluster(s) or datacenter(s).  


**Username :** To filter the operations down to those which were initiated by the specified user  


**Start :** To retrieve only the operations which occurred after the specified date (or date and time). The valid formats are dd/mm/yyyy or mm/dd/yyyy, depending on the local machine regional settings.  


**Finish :** To retrieve only the operations which occurred before the specified date (or date and time). The valid formats are dd/mm/yyyy or mm/dd/yyyy, depending on the local machine regional settings.  


**OperationType :** To filter the operations down to a specific type or topic.
The possible values are : 
Create, Reconfigure, Remove, DRS, HA, Password, Migration, Snapshot, Power, Alarm, Datastore, Permission  


###Examples :


-------------------------- EXAMPLE 1 --------------------------

PS C:\>Get-Cluster Test-Cluster | Audit-vCenterOperation -OperationType Reconfigure


To track when the configuration of the cluster "Test-Cluster" was changed and by who.




-------------------------- EXAMPLE 2 --------------------------

PS C:\>Audit-vCenterOperation -OperationType Migration -Start (Get-Date).AddDays(-7)


To track all the migrations (vMotion and Storage vMotion) for all VMs which occurred during the 
last 7 days.




-------------------------- EXAMPLE 3 --------------------------

PS C:\>Get-VMHost | Audit-vCenterOperation -Username "User01" -OperationType Power


To verify if the user "User01" has initiated a power operation on a ESXi host.










