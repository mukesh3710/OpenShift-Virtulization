# Summary of OpenShift Virtualization

## Overview
Red Hat OpenShift Virtualization extends OpenShift Container Platform (RHOCP) by enabling the management of virtual machine (VM) workloads alongside containerized applications. It is based on KubeVirt and utilizes Kubernetes-native mechanisms for VM orchestration.

## Key Features
- **Unified Platform:** Manage containers and VMs within the same OpenShift cluster.
- **Storage Management:** Assign persistent volumes (PVs) to VMs.
- **Network Management:** Attach network interfaces and manage connectivity.
- **Virtual Machine Consoles:** Access VMs using SSH, RDP, and web-based tools.
- **Live Migration:** Move VM instances (VMIs) between nodes without downtime.
- **CI/CD Pipelines:** Integrate VMs into automated deployment workflows.
- **Common Infrastructure:** Utilize shared tools like the OpenShift web console and CLI.

## Virtualization Components
- **virt-api:** Provides a RESTful API for VM management.
- **virt-controller:** Manages VM lifecycle and ensures state consistency.
- **virt-handler:** A DaemonSet that monitors and enforces VM states on nodes.
- **virt-launcher:** Runs VM workloads and manages VM isolation.
- **libvirtd:** Manages the VM process lifecycle within its pod.

## Operators and Tools
- **HyperConverged Operator (HCO):** Manages virtualization components.
- **KubeVirt:** Enables VM execution in OpenShift.
- **Hostpath Provisioner Operator (HPP):** Provides local storage for VMs.
- **QEMU Agent:** Enhances VM monitoring and management.
- **KVM:** Enables the execution of multiple guest VMs on a single host.

## Benefits
- **Operational Efficiency:** Unifies VM and container management.
- **Flexibility:** Supports Linux and Windows VMs.
- **Scalability:** Leverages Kubernetes for dynamic VM provisioning.
- **Security:** Integrates RBAC and network policies.
- **Automation:** Uses GitOps and Ansible for VM lifecycle management.

## Additional Configurations
- **Live Migration Policies:** Set migration rules for VMs.
- **CDI Integration:** Streamline storage imports.
- **GitOps Integration:** Automate VM deployment with OpenShift GitOps.
---

