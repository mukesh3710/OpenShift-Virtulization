
  # Open Console





```yaml
Console:
virtctl console centos-stream9-scarlet-wolverine-83 -n vm # Open serial Console

virtctl Commands:
virtctl stop <vm-name> : Stops a VM

VMI:
oc get vmis -A - Lists all VMIs in the cluster.

Manage the VM from virt-launcher Pod:
virsh list # Lists running VMs.
virsh start <vm> # Starts a VM
virsh shutdown <vm> # Shuts down a VM
virsh migrate <vm> # Migrates a VM to another host
```
