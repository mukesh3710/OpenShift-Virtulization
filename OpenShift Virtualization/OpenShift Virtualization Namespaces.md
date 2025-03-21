# OpenShift Virtualization Namespaces

OpenShift Virtualization (KubeVirt) enables running and managing virtual machines (VMs) alongside containerized workloads. Below are the key namespaces used for OpenShift Virtualization:

## **1. openshift-cnv**
   - This is the main namespace for OpenShift Virtualization (KubeVirt) resources.
   - Contains the core resources for virtualization, including VM pods, virtual machine instance definitions, and controllers.

## **2. openshift-kubevirt**
   - Contains KubeVirt-specific components like the VirtualMachineInstance (VMI) controller, VM controller, and other related resources.

## **3. openshift-image-registry**
   - Contains the image registry for managing container and VM images used by OpenShift Virtualization.

## **4. openshift-storage**
   - Includes resources for persistent storage management for virtual machines using OpenShift Data Foundation (ODF) or Ceph.

## **5. openshift-virtoperator**
   - Contains the virt-operator component, which is responsible for managing KubeVirt components and ensuring that the OpenShift Virtualization installation is properly configured.

## **6. openshift-monitoring**
   - Monitoring resources related to OpenShift Virtualization, such as Prometheus or Grafana dashboards for monitoring the health and performance of virtual machines.

## **7. openshift-logging**
   - Logs for the OpenShift Virtualization components, including KubeVirt VM logs and events.

## **8. openshift-multus**
   - If using Multus for multi-networking, this namespace contains the Multus-related resources required to manage networking for virtual machines.

## **9. openshift-network-operator**
   - Includes network configuration and policies related to virtual machines, especially when multi-network interfaces are in use.
