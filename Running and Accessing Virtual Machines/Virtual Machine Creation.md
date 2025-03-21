# Virtual Machine Creation and Management in OpenShift
---
Virtual Machine Creation:
- You can create a VM in OpenShift using the web console's Virtual Machine Creation Catalog or by defining YAML configurations.
- Using the Catalog: Web console provides default templates for various operating systems. Users can define boot sources and customize parameters such as SSH keys, cloud-init configurations, and additional storage.
- Virtual Machine Templates: Red Hat provides default templates with preconfigured networking, users, and storage. Templates can be customized. Installing the KubeVirt common-templates package allows the creation of additional OS templates.
- YAML Definition: Users can define VMs and templates using YAML in the web console or CLI. YAML allows users to configure system resources, labels, boot images, and advanced options.
---
Virtual Machine Management:
Each VM has a management page with the following sections:
- **Overview**: Logs, resource utilization, and status.
- **Metrics**: CPU, memory, storage, network, and migration metrics.
- **YAML**: Directly edit the VM’s configuration.
- **Configuration**:
  - **Details**: Modify VM specs (CPU, memory, workload profile, hostname, boot order, etc.).
  - **Storage**: Manage VM disks.
  - **Network**: Configure network interfaces.
  - **Scheduling**: Manage node selection, tolerations, and affinity rules.
  - **SSH**: Configure SSH access.
  - **Initial Run**: Manage cloud-init and Sysprep (for Windows VMs).
  - **Metadata**: Add labels and annotations.
- **Console**: Provides serial and VNC console access.
- **Snapshots**: Manage VM snapshots.
- **Diagnostics**: View VM and snapshot status.
---
Accessing Virtual Machines:
- **Web Console**: VNC console for graphical access. Serial console for CLI access.
- **CLI (virtctl tool)**:  `virtctl console vm-name` for serial console. `virtctl vnc vm-name` for graphical access.
- **Other VNC Clients**: Use third-party VNC applications like TigerVNC or TightVNC. Windows VMs support RDP with the appropriate configurations.

## Role-Based Access Control (RBAC)
OpenShift provides cluster roles with specific permissions:
- **admin**: Can modify any project resource except quotas.
- **cluster-admin**: Full cluster-wide permissions.
- **edit**: Can modify most project objects but not roles and bindings.
- **view**: Can view project objects but not modify them.

### OpenShift Virtualization RBAC
- **kubevirt.io:view**: View virtualization resources.
- **kubevirt.io:edit**: Modify virtualization resources but not runtime configurations.
- **kubevirt.io:admin**: Full control over virtualization resources and runtime configurations.

---

# Creating and Accessing a VM via OpenShift Web Console

## Overview
This guide walks through creating a RHEL 9 VM using a predefined template in the OpenShift web console, accessing the VNC console, managing resources, and interacting with the virt-launcher pod terminal.

### Create a VM from the Catalog
1. Navigate to **Virtualization → Catalog**.
2. Select the `accessing-guicreate` project.
3. Choose **RHEL 9 VM template**.
4. Set `CLOUD_USER_PASSWORD` to `redhat123` and name the VM `accessing-vm`.
5. Enable **Start this VirtualMachine after creation** and create the VM.

### Access the VM Console
1. Wait for the VM status to change to **Running**.
2. Open the **VNC console** and log in using creds
3. Check the QEMU agent status: systemctl status qemu-guest-agent
4. Go to **Configuration → Details**.

### Manage the VM from virt-launcher Pod
1. Locate the **virt-launcher pod** in the **General** section.
2. Open the **Terminal** and list running VMs:
   ```bash
   virsh list
   virsh shutdown accessing-guicreate_accessing-vm # Shutdown the VM
   ```
   
### Verify Auto-Recovery
1. Confirm VM status is **Running**.
2. Review **Events** to validate the `virtualmachine-controller` restarted the instance.
