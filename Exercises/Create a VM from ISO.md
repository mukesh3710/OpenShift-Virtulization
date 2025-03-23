### Create a VM from ISO


Upload ISO File as a DataVolume:
```yaml
apiVersion: cdi.kubevirt.io/v1beta1
kind: DataVolume
metadata:
  name: rocky8-os-disk
  namespace: vm
spec:
  source:
    http:
      url: "http://192.168.22.1:8080/os/Rocky-8.10-x86_64-minimal.iso"
  pvc:
  storage:
    resources:
      requests:
        storage: 10Gi
```

Create a datavolume for VM:
```yaml
apiVersion: cdi.kubevirt.io/v1beta1
kind: DataVolume
metadata:
  name: rocky8-rootdisk
  namespace: vm
spec:
  source:
    blank: {}  # This will create a blank disk for installation
  pvc:
    accessModes:
      - ReadWriteMany
    resources:
      requests:
        storage: 30Gi
    storageClassName: nfs-client
```

Create a VirtualMachine from the ISO DV: 
```yaml
apiVersion: kubevirt.io/v1
kind: VirtualMachine
metadata:
  name: rocky8
  namespace: vm
spec:
  running: false
  template:
    metadata:
      labels:
        kubevirt.io/domain: rocky8
    spec:
      domain:
        cpu:
          cores: 1
        resources:
          requests:
            memory: 2Gi
        devices:
          disks:
            - name: bootdisk
              disk:
                bus: virtio
      volumes:
        - name: bootdisk
          dataVolume:
            name: rocky8-qcow2
        - name: rootdisk
          persistentVolumeClaim:
            claimName: rocky8-rootdisk  # Attach the dynamically created PVC
```
--- 
Deploy the VM & Post deployment task to remove bootdisk from VM, so VM can boot from rootdisk
```bash
# Patch the VM to Remove bootdisk:
oc patch vm rocky8 -n vm --type=json -p '[{"op": "remove", "path": "/spec/template/spec/domain/devices/disks/0"}]' 
oc patch vm rocky8 -n vm --type=json -p '[{"op": "remove", "path": "/spec/template/spec/volumes/0"}]'
virtctl patch vm rocky8 --type=json -p '[{"op": "remove", "path": "/spec/template/spec/domain/devices/disks/0"}]'
virtctl patch vm rocky8 --type=json -p '[{"op": "remove", "path": "/spec/template/spec/volumes/0"}]'
oc get vm rocky8 -o yaml -n vm | grep -A5 "volumes:" # Verify the Changes

virtctl start rocky8-vm -n vm
oc get vmis -n vm
virtctl console rocky8-vm -n vm
```

