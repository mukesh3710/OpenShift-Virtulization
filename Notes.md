# Notes

---
### Create and manage VMs
```yaml
Console:
virtctl console postgresql-rhel9  # Open serial Console
virtctl vnc postgresql-rhel9 # VNC Console
virtctl ssh -i .ssh/lab_rsa --username developer postgresql-rhel9 # SSH
Accessing a VM with Port-Forward:
virtctl port-forward vm/postgresql-rhel9 22080:80 # Accessing a VM with Port-Forward
oc port-forward pod/virt-launcher-postgresql-rhel9-gbxws 22080:80 # with OC

Create and Manage VM:
oc get datasources -n openshift-virtualization-os-images # Verify Available DataSources
oc get pvc -n openshift-virtualization-os-images
virtctl create vm --name rhel9 --namespace vm --memory=5Gi --volume-datasource=src:openshift-virtualization-os-images/rhel9 # Create Mainfest and then apply 
virtctl create vm --name postgresql-rhel9 --namespace production --memory=5Gi # Create Mainfest 
virtctl stop/start/restart postgresql-rhel9 # stop/start & restart the VM 

Exposing a VM with Command-line Tools:
virtctl expose vm postgresql-rhel9 --name postgresql-service --type ClusterIP --port 5432 # Exposing a VM with Command-line Tools
oc get services #

Edit VM settings: 
oc edit vm postgresql-rhel9
oc patch vm postgresql-rhel9 --type merge -p '{"spec":{"template":{"metadata":{"labels":{"servertype":"production"}}}}}' # Patch VM

VMI:
oc describe vmi rhel9-database
oc get vmis -A # Lists all VMIs in the cluster.

Manage the VM from virt-launcher Pod:
virsh list # Lists running VMs.
virsh start <vm> # Starts a VM
virsh shutdown <vm> # Shuts down a VM
virsh migrate <vm> # Migrates a VM to another host

Command-line Monitoring:
oc get vms -n <namespace>   # Lists all virtual machines in the specified namespace
oc describe vm <vm-name> -n <namespace>   # Shows detailed status, configurations, and recent events of a VM
oc get vmi -n <namespace>   # Lists all running Virtual Machine Instances (VMIs) in the namespace
oc describe vmi <vmi-name> -n <namespace>   # Displays detailed information about a specific running VM instance
oc adm top vm -n <namespace>   # Shows CPU and memory usage of all VMs in the specified namespace
oc adm top pod -n <namespace> | grep <vm-name>   # Filters resource usage information specific to VM-related pods
oc logs -f vm/<vm-name> -n <namespace>   # Streams logs of a virtual machine for debugging
oc logs -f vmi/<vmi-name> -n <namespace>   # Fetches logs from the running Virtual Machine Instance (VMI)
oc get events -n <namespace> --sort-by='.lastTimestamp'   # Displays recent events related to virtual machines, sorted by time
oc get pvc -n <namespace>   # Lists Persistent Volume Claims (PVCs) used by virtual machines
oc describe pvc <pvc-name> -n <namespace>   # Shows detailed information about a specific storage volume attached to a VM
oc get network-attachment-definitions -n <namespace>   # Lists available network configurations for VMs
oc describe network-attachment-definition <network-name> -n <namespace>   # Displays detailed information about a specific network configuration
oc get pods -o wide -n <namespace> | grep <vm-name>   # Shows VM-related pods along with IP addresses and node assignments
oc virt console <vm-name> -n <namespace>   # Opens a serial console session to the VM
oc get migration -n <namespace>   # Lists all active VM migrations
oc describe migration <migration-name> -n <namespace>   # Provides details on the progress and status of a live migration

