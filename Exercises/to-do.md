# Creating and Accessing Virtual Machines from the Command Line


- Create a new project
- check available images/template available to create a vm
- Create a new user, assign admin role to new project 
- Create a anohter user, assign that can view/stop/start vm, can check logs and monitor the vm performace
- Generate mainfest with virtctl to create virtual machine (user admin)
- apply the mainfest to deploy the vm
- give stress to machine, monitor the vm perofmace and check error logs 
- stop/start mv (another user)
--

## Objectives
Provision and access new virtual machines by using command-line tools.

## Creating Virtual Machines From the Command Line
To create a VM automatically, use declarative files and Ansible Playbooks from the command line. You can edit the YAML configuration of a VM with a text editor or by using the `oc edit` command. A VM YAML file includes all settings from a default template or an instance type in one structured document.

Declarative files can also be used to back up the configuration of a VM and restore settings to a new VMI.

### Creating a VM with Command-line Tools
Use a YAML file to create a VM by running the following command:

```bash
oc apply -f vm-manifest.yaml
```

Example configuration for a VM using a PostgreSQL RHEL 9-based image:

```yaml
apiVersion: kubevirt.io/v1
kind: VirtualMachine
metadata:
  name: postgresql-rhel9
spec:
  runStrategy: Always
  template:
    metadata:
      creationTimestamp: null
    spec:
      dataVolumeTemplates:
      - metadata:
          creationTimestamp: null
          name: postgresql-rhel9
        spec:
          source:
            registry:
              url: "registry.redhat.io/rhel9/postgresql-15:latest"
              secretRef: data-source-secret
              certConfigMap: tls-certs
      domain:
        devices: {}
        memory:
          guest: 512Mi
        resources: {}
      terminationGracePeriodSeconds: 180
      volumes:
        - dataVolume:
            name: rhel-9-minimal-volume
          name: rootdisk
status: {}
```

### Editing a VM Configuration
Use `oc edit` to update VM settings:

```bash
oc edit vm postgresql-rhel9
```

After editing, restart the VM for changes to apply:

```bash
virtctl restart postgresql-rhel9
```

### Patching a VM
To add a label to a VM:

```bash
oc patch vm postgresql-rhel9 --type merge -p '{"spec":{"template":{"metadata":{"labels":{"servertype":"production"}}}}}'
```

### Generating a VM Manifest
To create a VM manifest file:

```bash
virtctl create vm --name postgresql-rhel9 --namespace production --memory=5Gi
```

## Managing a VM with Command-line Tools

### Stopping a VM
```bash
virtctl stop postgresql-rhel9
```

### Starting a VM
```bash
virtctl start postgresql-rhel9
```

### Restarting a VM
```bash
virtctl restart postgresql-rhel9
```

### Deleting a VM
```bash
oc delete vm postgresql-rhel9
```

## Accessing the Console of a VM

### Serial Console
```bash
virtctl console postgresql-rhel9
```
To exit, use the escape sequence `^]`.

### VNC Console
```bash
virtctl vnc postgresql-rhel9
```

## Accessing a VM with SSH
```bash
virtctl ssh -i .ssh/lab_rsa --username developer postgresql-rhel9
```

## Accessing a VM with Port-Forward
```bash
virtctl port-forward vm/postgresql-rhel9 22080:80
```

Using `oc`:
```bash
oc port-forward pod/virt-launcher-postgresql-rhel9-gbxws 22080:80
```
Press `Ctrl+C` to exit.

## Exposing a VM with Command-line Tools
```bash
virtctl expose vm postgresql-rhel9 --name postgresql-service --type ClusterIP --port 5432
```

Confirm the service:
```bash
oc get services
```

