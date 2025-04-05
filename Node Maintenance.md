### Node Maintenance

Node Maintenance in OpenShift:
- Understand how to put a node into maintenance mode.
- Learn what happens to pods and VMs during maintenance.
- Understand how to safely relocate workloads and resume normal operations.

Step-by-Step: Preparing a Node for Maintenance
- Cordon the Node: This marks the node as unschedulable, meaning no new pods or VMs will be scheduled on it. `oc adm cordon node2`
- Drain the Node: Moves (evicts) all current workloads (pods and VMs) to other available nodes. `oc adm drain node2 --delete-emptydir-data --ignore-daemonsets --force`
  - `--delete-emptydir-data:` Deletes local storage (ephemeral volumes) if any.
  - `--ignore-daemonsets:` Skips daemonset-managed pods.
  - `--force:` Forces eviction even for unmanaged pods.
 
Node Maintenance Operator:
- Provides a declarative method to perform maintenance using a custom resource.
- Automatically cordons and drains the node.
- Apply with below yaml `oc apply -f maintenance-node2.yaml`
```yaml
apiVersion: nodemaintenance.medik8s.io/v1beta1
kind: NodeMaintenance
metadata:
  name: maintenance-node2
spec:
  nodeName: node2
  reason: "Node maintenance"
```
- You can track draining status via: `oc describe NodeMaintenance maintenance-node2`
- To remove maintenance mode: `oc delete NodeMaintenance maintenance-node2`

Virtual Machines and Maintenance:
- Live Migration: VMs with the LiveMigrate eviction strategy will be moved live during drain. If not supported (e.g., due to ReadWriteOnce storage), VM gets shutdown and restarted on another node.
- Not Migratable VMs: Display a “Not migratable” badge in the UI. You can set eviction strategy to None to avoid drain issues.

Pod Disruption Budget (PDB):
- Ensures minimum availability of pods during voluntary disruptions (e.g., maintenance).
- Prevents all replicas from being evicted at once.
- Used automatically with VM pods to delay eviction until it's safe.
- Example command: `oc get pdb` `oc describe pdb kubevirt-disruption-budget-xyz`

Descheduler for VM Rebalancing (Tech Preview):
- Descheduler can help redistribute workloads after maintenance.
- Not enabled by default and not for production use yet.
- Requires: Install Kube Descheduler Operator. Add annotation to the VM.
