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

```
