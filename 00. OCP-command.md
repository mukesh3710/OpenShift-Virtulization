### OpenShift
---
Commands:
```yml

Help:
kubectl help — List all kubectl commands
kubectl create --help — Help for kubectl create
oc help — List all oc commands
oc create --help — Help for oc create
oc explain <resource> — Describe a resource and its fields
oc options — Show global options
oc api-versions — List available API versions

Login:
oc login --server=https://api.my.test.com:6443 --username=admin --password=admin — Login to cluster
export KUBECONFIG=/path/to/kubeconfig — Set kubeconfig file
oc login -u admin -p redhatocp — Quick login
oc logout — Log out from the cluster

Cluster Information:
oc version — Show client and server version
oc cluster-info — Display cluster info
oc whoami — Show current user
oc whoami --show-console — Console URL
oc whoami --show-server — API Server URL
oc api-resources — List all API resources
oc api-versions — Show supported APIs
oc get clusterversion — Cluster version
oc describe clusterversion version
oc get clusteroperator — List cluster operators
oc describe clusteroperator <name> — Details of an operator
oc get nodes — List nodes
oc describe node <node-name> — Detailed info about a node
oc get infrastructure cluster -o yaml — Cluster infrastructure details
oc get dns cluster -o jsonpath='{.spec.baseDomain}' — Get base domain
oc adm upgrade — Upgrade cluster or view upgrade history
oc explain services — Describe service resource
oc get route -A — List all routes
oc get pods -n openshift-apiserver — List API server pods
oc status -n openshift-authentication — Resource status for a project
oc get pods -A | grep kube-apiserver — Quick check API server pods
oc describe pod <pod-name> -n <namespace> — Describe any pod

Events & Logs:
oc get events --sort-by='.lastTimestamp' — List events sorted by time
oc get events -A — List cluster-wide events
oc get events -n <namespace> — Events for specific namespace
oc adm must-gather — Cluster diagnostic information
journalctl -u kubelet — Node logs
oc logs <pod-name> -n <namespace> — Logs from pod
oc logs -f <pod-name> -n <namespace> — Follow pod logs
oc rsh <pod-name> — Remote shell into a pod
oc exec <pod> -- <command> — Execute command in a pod
oc debug node/<node-name> — Debug a node
oc adm node-logs <node-name> — Fetch node logs

OpenShift Core Components:
API Server:
oc get clusteroperators kube-apiserver
oc get --raw /readyz — API server readiness
oc get --raw /healthz — API server health
oc get --raw /metrics | grep apiserver_request_duration_seconds — Slow API requests
curl -k https://<api-server>:6443/version — API version curl check
curl -k -H "Authorization: Bearer $(oc whoami -t)" https://<api-server>/apis — API groups list
oc get resourcequotas -n openshift-kube-apiserver
oc explain pods
etcd:
oc get pods -n openshift-etcd
oc logs -n openshift-etcd -l app=etcd
oc exec -n openshift-etcd <etcd-pod> -- etcdctl endpoint status --write-out=table

Infrastructure & Node Management:
Machine Config Operator (MCO):
oc get machineconfigpool
oc get machineconfig
oc get pods -n openshift-machine-config-operator
oc describe mcp <name>
Cluster Autoscaler:
oc get clusterautoscaler
oc describe clusterautoscaler default
Node Tuning Operator:
oc get tuneds -n openshift-cluster-node-tuning-operator

Networking & Ingress:
Ingress Operator:
oc get ingresscontroller -n openshift-ingress-operator
oc describe ingresscontroller <name> -n openshift-ingress-operator
Cluster Network Operator (CNO):
oc get network.operator.openshift.io cluster
oc describe network.operator.openshift.io cluster
Multus:
oc get pods -n openshift-multus
Service & Network:
oc get services -A
oc describe svc <service-name> -n <namespace>
oc get networkpolicy -A

Security & Certificates:
Authentication & OAuth:
oc get oauth
oc get clusteroperator authentication
Certificate Management:
oc get certificates -n openshift-ingress-operator
oc get csr
oc describe csr <csr-name>
oc adm certificate approve <csr-name>
oc get csr --no-headers | awk '/Pending/ {print $1}' | xargs oc adm certificate approve
Compliance Operator:
oc get compliancesuite -n openshift-compliance
oc describe compliancesuite <suite-name> -n openshift-compliance

Storage & Persistent Data:
OpenShift Data Foundation (ODF):
oc get storagecluster -n openshift-storage
oc get pods -n openshift-storage
Persistent Volumes (PV) & Persistent Volume Claims (PVC):
oc get pv
oc get pvc -n <namespace>
oc describe pvc <pvc-name> -n <namespace>
Storage Classes:
oc get sc
oc describe sc <storageclass-name>

Monitoring & Logging:
Cluster Monitoring:
oc get clusteroperator monitoring
oc get pods -n openshift-monitoring
oc describe pod <pod-name> -n openshift-monitoring
Cluster Logging:
oc get clusterlogging -n openshift-logging
oc get pods -n openshift-logging

Application Management:
Image Registry:
oc get clusteroperator image-registry
oc get pods -n openshift-image-registry
OpenShift Pipelines (Tekton):
oc get pods -n openshift-pipelines
oc get pipelines -n <namespace>
oc get pipelineruns -n <namespace>
OpenShift GitOps (ArgoCD):
oc get pods -n openshift-gitops
oc get applications.argoproj.io -A
OpenShift Serverless (Knative):
oc get knativeserving.operator.knative.dev -n knative-serving
OpenShift Service Mesh (Istio):
oc get servicemeshcontrolplane -n istio-system
oc get smmr -n istio-system

Operator Lifecycle Management (OLM):
OperatorHub & OLM:
oc get catalogsource -n openshift-marketplace
oc get subscriptions -n <namespace>
oc get csv -n <namespace>
oc get operatorgroup -n <namespace>

OpenShift Quotas and Limits:
oc get resourcequotas -n <namespace>
oc describe resourcequotas -n <namespace>
```
