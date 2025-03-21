# Virtual Machine Resources
---
Workload Controllers:
- Red Hat OpenShift offers a set of resources to help run applications inside a cluster. The pods execute containers within an OpenShift cluster.
- Pods can execute one or more containers, acting as running application instances. Kubernetes workload resources manage applications to reduce the need to interact with individual pods directly.
---
Common Workload Resources:
- Deployments: A deployment object uses pod templates to define the desired state of an application. Deployments interact with a replica set to ensure the intended number of pods are available.
- Replica Sets: A replica set ensures the specified quantity of pod replicas are available and healthy. It uses selectors to identify pods and maintains the deployment state by creating, updating, or deleting pods automatically.
- Daemon Sets: A daemon set ensures that a pod runs on every selected node. Unlike a replica set, a daemon set is not bound to a specific number of replicas and automatically creates pods on new nodes with matching selectors.
- Stateful Sets: A stateful set manages stateful applications, ensuring consistent, unique identities for each pod (network and storage) while maintaining persistent data.
---
Difference Between Workload Controllers, VMs, and VMIs: A Virtual Machine (VM) simulates physical resources such as CPU, memory, network interfaces, and storage, similar to StatefulSet pods. In Red Hat OpenShift Virtualization:
- A **VM object** specifies a template for a running VM instance.
- A **Virtual Machine Instance (VMI)** is the actual running instance of a VM. (can create standalone vm - Orphan)
- The **virt-controller** pod interacts with the **virt-handler** pod to create a **virt-launcher** pod that runs the VMI.
---
Components of an OpenShift Virtual Machine: VMIs exist in pods and require components to maintain workload health, including:

### Virtual Machine Consoles
- **VNC Console:** Provides text-based and graphical access.
- **Serial Console:** Offers text-based console access.
- **RDP Console:** Provides graphical access for Windows-based VMIs.

### Network Interfaces
- **Default Pod Network:** Assigns an IP from the cluster using NAT (masquerade binding). (Default OVN)
- **Multus:** Enables multiple interfaces and external networks using CNI.
- **SR-IOV:** Provides high-performance network access through virtual function devices. (Connect physical adapter)

### Persistent Volumes and Persistent Volume Claims
A **Persistent Volume (PV)** represents existing storage, while a **Persistent Volume Claim (PVC)** requests specific storage resources.

## Boot Sources
A boot source is a disk image containing the OS, drivers, and initial data for a VM. The download from a registry creates a dataimportcron resource that defines a cron
job to pull and import the disk image. The Containerized Data Importer (CDI) imports the golden images from Red Hat
to the openshift-virtualization-os-images project as snapshots or PVCs. Boot sources include:
- **Cloud images (RAW, QCOW2), ISO installation disks, container disks, and PVCs.**
- **Golden images:** Preconfigured snapshots used to create VMs.
- **Red Hat golden images:** Synchronized and updated automatically via OpenShift Virtualization.

## Configuration Maps and Secrets
Configuration maps and secrets store key-value pairs used by resources. They must be created before being attached to a VM and mounted manually within the VM console.

## Virtual Machine Creation Components
The OpenShift Virtualization hierarchy consists of:
- **virt-controller:**  Operator monitors for new VMI objects. The virt-handler daemon set runs on each node to execute any necessary actions to meet a VM object's defined state. 
- **virt-handler daemon set:** daemon set monitors for changes in a VM, and creates the virt-launcher container.
- **virt-launcher container:** Container runs within each VM's pod and instantiates the VM with the use of a local libvirtd instance, which provides a low-level virtualization architecture and interfaces with the kernel to manage the lifecycle of the VM process. When the VMI is provisioned, the virt-launcher pod routes IPv4 traffic to the Dynamic Host Configuration Protocol.

### virsh Commands: 
- The libvirtd instance also includes the virsh command, to manage VMs. This utility provides several commands to list, start, stop, or reboot VMs . The `virsh` CLI tool manages VMs:
- `virsh list` - Lists running VMs.
- `virsh start <vm>` - Starts a VM.
- `virsh shutdown <vm>` - Shuts down a VM.
- `virsh migrate <vm>` - Migrates a VM to another host.

### virtctl Commands
The `virtctl` CLI tool manages VM lifecycle actions such as start, stop, pause, restart, and migrate.
- `virtctl stop <vm-name>` - Stops a VM.

## Stand-alone VMIs
Stand-alone VMIs operate independently from OpenShift Virtualization. They can be managed via the `oc` CLI:
- `oc get vmis -A` - Lists all VMIs in the cluster.

## Use Cases for Creating VMs
VMs in OpenShift Virtualization can be created using:
- **Predefined templates**
- **Custom templates**
- **Declarative manifest files**
- **Cloning existing VM objects**
- **Migration operators and imports**
