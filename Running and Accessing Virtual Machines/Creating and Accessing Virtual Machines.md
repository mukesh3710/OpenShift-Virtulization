# Creating and Accessing Virtual Machines

## Workload Controllers
Red Hat OpenShift Container Platform (RHOCP) offers a set of resources to help run applications inside the cluster. Pods execute containers within an OpenShift cluster. Workload resources manage applications and reduce the need to interact directly with application pods.

### Deployments
A deployment object describes the intended state of an application and its components. It interacts with a replica set resource to ensure that the application has the intended number of pods.

### Replica Sets
A replica set resource ensures that the specified number of pod replicas are available and in a healthy state. It automatically creates, updates, or deletes pods as needed.

### Daemon Sets
A daemon set resource ensures that a pod runs on every selected node. Unlike a replica set, a daemon set is not limited by a specific number of replicas and automatically creates a pod on a new node when added.

### Stateful Sets
A stateful set manages stateful applications with consistent, unique identities for network and storage, ensuring persistent data.

## Difference Between Workload Controllers, VMs, and VMIs
A virtual machine (VM) simulates the resources of a physical machine, similar to StatefulSet pods. In OpenShift Virtualization:
- A VM object specifies a template to create a virtual machine instance (VMI).
- The VMI is executed inside a pod.
- If a VMI is deleted, Kubernetes regenerates another instance based on the VM object.

When a VM is started:
- A `virt-controller` pod signals to a `virt-handler` pod to create a `virt-launcher` pod.
- The `virt-launcher` pod contains a `libvirtd` container to execute the VMI.

## Components of an OpenShift Virtual Machine
VMIs in pods require components to maintain workload health, including console access, network interfaces, storage, and execution pods.

### Virtual Machine Consoles
OpenShift Virtualization provides three console types:
1. **VNC Console**: Default selection, providing graphical or text-based access.
2. **Serial Console**: Text-based access through the serial port.
3. **RDP Console**: For Windows-based VMIs via Remote Desktop Protocol (RDP), requiring the QEMU guest agent.

### Network Interfaces
A VM can connect to networks using:
- **Default Pod Network**: Uses the cluster's pod network with NAT masquerade binding.
- **Multus**: Allows multiple network interfaces and external network connections via CNI.
- **Single Root I/O Virtualization (SR-IOV)**: Provides high-performance network connectivity.

### Persistent Volumes and Persistent Volume Claims
- **Persistent Volume (PV)**: Represents existing storage within the cluster.
- **Persistent Volume Claim (PVC)**: Requests a specific storage resource for a VMI.

### VMI Execution Pods
When a VM starts, the `virt-handler` daemon creates a `virt-launcher` pod to execute and manage the VMI using a `libvirtd` container.

### Stand-alone VMIs
You can create a stand-alone VMI via the command line or automation script. To list all VMIs in the cluster, including stand-alone VMIs, use:
```
oc get vmis
```

