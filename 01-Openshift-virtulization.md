## Red Hat OpenShift Virtualization

### KubeVirt
KubeVirt lets you run virtual machines (VMs) on top of Kubernetes.  Think of it as bridging the gap between containers and VMs.  Instead of just deploying containerized applications, you can also run traditional VMs alongside them, all managed by Kubernetes.  This is useful for running legacy applications, applications that require a full operating system, or applications that have licensing constraints that require VMs.  KubeVirt makes VMs first-class citizens in the Kubernetes world.

---

### OpenShift Virtualization

OpenShift Virtualization is a feature that lets you run and manage virtual machines (VMs) directly within your OpenShift cluster, alongside your containers. It's like having the best of both worlds in one platform.   
- Modernizing at your own pace: You might have applications that can't be easily containerized yet, but you still want to take advantage of OpenShift's benefits. Virtualization lets you run those applications as VMs while you plan their migration to containers.   
- Legacy applications: Some applications might require a full operating system environment to function correctly. VMs provide that environment.   
- Licensing: Certain software licenses might require you to run the application in a VM.
- Unified management: You can manage both your containerized and VM-based workloads from a single platform, simplifying operations and reducing complexity.   

OpenShift Virtualization uses a technology called KubeVirt, which allows Kubernetes to manage VMs as if they were containers. Here's the basic flow:   
- You define a VM: You create a definition for your VM, specifying things like the operating system, memory, storage, and networking. This definition is similar to how you define a container in Kubernetes.
- OpenShift creates the VM: OpenShift uses this definition to create the VM, which runs on a worker node in your cluster.
- You manage the VM: You can manage the VM just like you manage containers in OpenShift. You can start, stop, and monitor it using the same tools.

---

### Openshift virtualization component

KubeVirt:
- The Foundation: KubeVirt is the core technology that allows Kubernetes to manage virtual machines. It provides the necessary APIs and tools to define, create, and manage VMs as if they were containers. Think of it as the engine that powers OpenShift Virtualization.

Operators:
- Automated Management: OpenShift Virtualization relies heavily on Operators to automate the deployment, configuration, and management of its various components. Operators are like intelligent helpers that keep everything running smoothly. Here are some key Operators:
- HyperConverged Cluster Operator (HCO): This is the main operator that manages the overall lifecycle of OpenShift Virtualization. It installs and updates other operators and ensures they work together correctly.
- virt-operator: Responsible for managing the lifecycle of virtual machines, including creating, starting, stopping, and migrating them.
- cdi-operator: Manages the Containerized Data Importer (CDI), which helps import and export VM images.
- cluster-network-addons-operator: Configures networking for VMs, allowing them to connect to the network and communicate with other pods and services.
- ssp-operator: Manages the Single Sign-On (SSO) integration for accessing VMs.
- tekton-tasks-operator: Provides tasks for Tekton Pipelines, enabling you to automate VM-related operations as part of your CI/CD workflows.

Key Components:
- virt-api: This is the API server for KubeVirt. It provides the endpoints for interacting with VMs, similar to how the Kubernetes API server works for containers.
- virt-controller: This component watches for new VM definitions and creates the necessary pods to run the VMs. It's like the conductor of the VM orchestra, making sure everything is set up correctly.
- virt-handler: This agent runs on each worker node and is responsible for managing the actual VMs on that node. It interacts with the hypervisor (like KVM) to start, stop, and monitor the VMs.
- virt-launcher: This component runs inside the pod that hosts the VM. It uses libvirt and qemu (the hypervisor) to create and run the VM.
- CDI (Containerized Data Importer): This component helps import and export VM images. It can convert images from various formats and make them usable by KubeVirt.

Networking:
- Network Integration: OpenShift Virtualization integrates with OpenShift's software-defined networking (SDN) to provide networking for VMs. VMs can be connected to the same network as containers, or they can have their own dedicated networks.
- kube-proxy: The kube-proxy component also plays a role in directing network traffic to VMs, ensuring that external requests reach the correct VM.

Storage:
- Persistent Volumes: VMs in OpenShift Virtualization use Persistent Volumes (PVs) for their storage. PVs provide a way to provision and manage storage for VMs, similar to how they work for containers.
- Storage Providers: OpenShift Virtualization supports various storage providers, allowing you to use different types of storage for your VMs.


