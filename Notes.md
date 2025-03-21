# OCP-V Commands


Console:
```yaml
virtctl console postgresql-rhel9  # Open serial Console
virtctl vnc postgresql-rhel9 # VNC Console
virtctl ssh -i .ssh/lab_rsa --username developer postgresql-rhel9 # SSH
virtctl port-forward vm/postgresql-rhel9 22080:80 # Accessing a VM with Port-Forward
oc port-forward pod/virt-launcher-postgresql-rhel9-gbxws 22080:80 # with OC
oc virt console <vm-name>  # Opens a serial console session to the VM
```
Create and Manage VM:
```yaml
virtctl create vm --name rhel9 --namespace vm --memory=5Gi --volume-datasource=src:openshift-virtualization-os-images/rhel9 # Create Mainfest and then apply 
virtctl create vm --name postgresql-rhel9 --namespace production --memory=5Gi # Create Mainfest 
virtctl stop/start/restart postgresql-rhel9 # stop/start & restart the VM 
oc edit vm postgresql-rhel9 # Edit VM settings
oc patch vm postgresql-rhel9 --type merge -p '{"spec":{"template":{"metadata":{"labels":{"servertype":"production"}}}}}' # Patch VM
```
Manage the VM from virt-launcher Pod:
```yaml
virsh list # Lists running VMs.
virsh start <vm> # Starts a VM
virsh shutdown <vm> # Shuts down a VM
virsh migrate <vm> # Migrates a VM to another host
```
Monitoring and Inspecting Virtual Machines in OpenShift Virtualization:
```yaml
oc get events --sort-by='.lastTimestamp' # Displays recent events related to virtual machines, sorted by time
oc get vms # Lists all virtual machines in the specified namespace
oc describe vm <vm-name> # Shows detailed status, configurations, and recent events of a VM
oc get vmi # Lists all running Virtual Machine Instances (VMIs) in the namespace
oc describe vmi # Displays detailed information about a specific running VM instance
oc adm top vm # Shows CPU and memory usage of all VMs in the specified namespace
oc adm top pod # Filters resource usage information specific to VM-related pods
oc logs -f vm/<vm-name>  # Streams logs of a virtual machine for debugging
oc logs -f vmi/<vmi-name>  # Fetches logs from the running Virtual Machine Instance (VMI)
oc get network-attachment-definitions  # Lists available network configurations for VMs
oc describe network-attachment-definition <network-name> # Displays detailed information about a specific network configuration
oc get migration# Lists all active VM migrations
oc describe migration <migration-name> # Provides details on the progress and status of a live migration
```
Networking:
```yaml
virtctl expose vm postgresql-rhel9 --name postgresql-service --type ClusterIP --port 5432 # Exposing a VM with Command-line Tools
```
Image:
```yaml
oc get datasources -n openshift-virtualization-os-images # Verify Available DataSources
oc get pvc -n openshift-virtualization-os-images
```
