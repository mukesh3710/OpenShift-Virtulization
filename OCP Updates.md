### OpenShift and OpenShift Virtualization Updates

Cluster Update Overview:
- OpenShift can upgrade itself — including core components and the underlying OS (RHCOS).
- It uses a central update service (OSUS) to find a valid upgrade path from your current version to a newer version.

Internet or On-Prem?:
- If the cluster has internet access, it contacts the OpenShift Update Service (OSUS) directly.
- If air-gapped, there's an on-prem version of this update service.

Cluster Version Operator (CVO):
- CVO is a built-in OpenShift component.
  - Checks in with OSUS
  - Finds available upgrades based on the selected channel (e.g., stable-4.14, fast-4.16)
  - Applies the upgrades in the correct order
 
Machine Config Operator (MCO): 
- Manages updates to the underlying OS (RHCOS)
- Applies changes to node-level settings via MachineConfig (MC) resources
- Groups nodes into MachineConfigPools (MCP) for tracking and batch updates
- MachineConfig (MC) Contains changes like: Kernel args, SSH keys, Files under /etc or /var & systemd services
- MachineConfigPool (MCP). Monitor MCP with: `oc get mcp`
  - Groups nodes with similar config (like all worker nodes)
  - Tracks update status per group
  - Has maxUnavailable parameter — controls how many nodes can be updated at once
 
OpenShift Virtualization Operator Updates:
- The OpenShift Virtualization operator must match the OpenShift version
- By default, updates are automatic
- You can manage this in: Console: Operators → Installed Operators → OpenShift Virtualization → Subscription Tab. Make sure Update Approval is Automatic

Virtual Machine (VM) Pod Updates:
- When a virtualization-related component like virt-launcher needs an update:
- If the VM supports live migration, OpenShift migrates the VM, updates the pod, and keeps the VM running.
- If live migration isn’t supported, the pod is updated only after a VM reboot.

Troubleshooting Updates:
- View Update History:
  - In Console: Administration → Cluster Settings → Cluster Version
  - Or use CLI: `oc describe clusterversions/version`
- Must-Gather for Troubleshooting
  - To collect logs and config data for debugging: `oc adm must-gather --image=registry.redhat.io/container-native-virtualization/cnv-must-gather-rhel9:v4.16.2`
  - This collects everything related to virtualization and stores it locally in a folder like: `must-gather.local.<timestamp>`
  - This is useful when opening a Red Hat support case or filing a Bugzilla ticket.
