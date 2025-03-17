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

# Kubernetes Architecture Overview

## Objectives
- Understand Kubernetes high-level architecture and operators.

## Kubernetes Architecture
Kubernetes is an orchestration service that simplifies the deployment, management, and scaling of containerized applications. It manages resources like CPU, RAM, storage, and networking while ensuring high availability and fault tolerance.

Kubernetes follows a **declarative management** approach, where desired system states are defined, and Kubernetes ensures compliance. This differs from **imperative management**, where direct commands change system states.

## Kubernetes Features
Kubernetes provides several features that facilitate application deployment and scaling:
- **Service discovery**
- **Load balancing**
- **Horizontal scaling**
- **Self-healing**
- **Automated rollout**
- **Configuration management**
- **Secrets management**

## Key Kubernetes Terminology
- **Operator**: A component that simplifies application lifecycle management.
- **Resource**: Configurable and consumable components within a Kubernetes cluster.
- **Control Plane**: Manages container lifecycle through API services.
- **Data Plane**: Provides resources like storage, networking, and compute for workloads.
- **Pod**: A group of containers representing an application or service.
- **Container**: A lightweight executable image that includes application dependencies.

## Kubernetes Operators
Operators are Kubernetes-native applications that automate the management of workloads and services. Using the Kubernetes API, they extend cluster functionality and automate tasks such as deployments and scaling.

### Kubernetes OperatorHub
OperatorHub (https://operatorhub.io) is an open-source repository where operators are shared. Red Hat, AWS, Google Cloud, and Microsoft collaborated to provide a centralized marketplace for Kubernetes operators. Operators built using the **Operator Framework** can be accessed and shared through this hub.

## Red Hat OpenShift Container Platform (RHOCP)
RHOCP extends Kubernetes with enterprise-ready capabilities, including:
- **Remote management**
- **Multitenancy**
- **Enhanced security**
- **Monitoring and auditing**
- **Application lifecycle management**
- **Self-service developer interfaces**

### RHOCP Technology Stack
- **Red Hat Enterprise Linux CoreOS**: Lightweight OS for OpenShift nodes.
- **CRI-O**: Secure, minimal container runtime.
- **Kubernetes**: Open-source container orchestration.
- **Self-service web console**: GUI for managing applications and clusters.
- **Preinstalled services**: Logging, monitoring, and networking tools.
- **Certified container images**: Includes runtimes, databases, and essential software.

## Red Hat Marketplace
Red Hat offers a catalog of enterprise-certified operators for OpenShift clusters. Organizations can explore, test, and install operators to enhance cluster functionality.

### Virtualization Meets Containerization
OpenShift Virtualization enables running virtual machines alongside containerized applications. This allows organizations to maintain traditional VM-based workloads while transitioning to containerized environments, reducing the need for separate virtualization solutions.

---

