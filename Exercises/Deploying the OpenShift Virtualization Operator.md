# Deploying the OpenShift Virtualization Operator

## Preparing an RHOCP Cluster for Virtualization
OpenShift Virtualization requires specific infrastructure setups to function optimally. While traditionally deployed on-premise using bare metal systems, it is also supported on cloud-based bare metal servers from providers such as IBM Cloud and AWS.

### Prerequisites
Before installing OpenShift Virtualization, ensure the following requirements are met:
- The cluster must be installed on bare metal infrastructure (on-premise or supported cloud partner) with Red Hat Enterprise Linux CoreOS worker nodes.
- CPUs must be supported by RHEL 9, support Intel 64 or AMD64 extensions, have Intel VT or AMD-V hardware virtualization enabled, and have the no-execute (NX) flag enabled.
- Compute nodes must meet or exceed the virtual machine resource requirements.
- For high availability (HA), use installer-provisioned infrastructure with machine health checks or manually monitor node availability.
- Shared storage is required for live migration functionality.
- The Operator Lifecycle Manager (OLM) must be enabled for deployment in restricted or disconnected environments.

## Installing the Red Hat OpenShift Virtualization Operator
You can install the OpenShift Virtualization operator using either the OpenShift web console or the command line.

### Web Console Installation Steps
1. Navigate to **Operators → Operator Hub** in the OpenShift web console.
2. Search for **OpenShift Virtualization** and select it.
3. Choose the preferred channel and version, then click **Install**.
4. Review the installation options and confirm by clicking **Install**.
5. The operator will be deployed in the `openshift-cnv` namespace.

### Required Components
- The **KubeVirt HyperConverged Operator (HCO)** must be installed to manage OpenShift Virtualization and its components.
- The HCO also deploys additional Custom Resources (CRs) for managing:
  - **Containerized Data Importer Operator**
  - **Scheduling, Scale, and Performance Operator**
  - **Cluster Network Addons Operator**

### Completing the Installation
1. Once the OpenShift Virtualization operator is installed, a prompt appears to create a **HyperConverged instance**.
2. Click **Create HyperConverged** to complete the setup.
3. Refresh the web console or log out and log back in if virtualization menu items do not immediately appear.

## Important Notes
- OpenShift Virtualization operators are explored in further detail throughout the course.
- While installation on a **Single Node OpenShift (SNO)** cluster is possible, it will not provide high availability features.

