# Kubernetes Cheat Sheet
![image](https://github.com/ozergoker/kubernetes-cheat-sheet/blob/main/kubernetes.png)


# What is Kubernetes ?

Kubernetes is a platform for managing containerized workloads. Kubernetes orchestrates computing, networking and storage to provide a seamless portability 
across infrastructure providers.

# What is kubectl ?

kubectl controls the Kubernetes cluster manager.

Basic Commands (Beginner):

  create        Create a resource from a file or from stdin\n
  expose        Take a replication controller, service, deployment or pod and expose it as a new Kubernetes service
  run           Run a particular image on the cluster
  set           Set specific features on objects

Basic Commands (Intermediate):

  explain       Get documentation for a resource
  get           Display one or many resources
  edit          Edit a resource on the server
  delete        Delete resources by file names, stdin, resources and names, or by resources and label selector

Deploy Commands:

  rollout       Manage the rollout of a resource
  scale         Set a new size for a deployment, replica set, or replication controller
  autoscale     Auto-scale a deployment, replica set, stateful set, or replication controller

Cluster Management Commands:

  certificate   Modify certificate resources.
  cluster-info  Display cluster information
  top           Display resource (CPU/memory) usage
  cordon        Mark node as unschedulable
  uncordon      Mark node as schedulable
  drain         Drain node in preparation for maintenance
  taint         Update the taints on one or more nodes

Troubleshooting and Debugging Commands:

  describe      Show details of a specific resource or group of resources
  logs          Print the logs for a container in a pod
  attach        Attach to a running container
  exec          Execute a command in a container
  port-forward  Forward one or more local ports to a pod
  proxy         Run a proxy to the Kubernetes API server
  cp            Copy files and directories to and from containers
  auth          Inspect authorization
  debug         Create debugging sessions for troubleshooting workloads and nodes

Advanced Commands:

  diff          Diff the live version against a would-be applied version
  apply         Apply a configuration to a resource by file name or stdin
  patch         Update fields of a resource
  replace       Replace a resource by file name or stdin
  wait          Experimental: Wait for a specific condition on one or many resources
  kustomize     Build a kustomization target from a directory or URL.

Settings Commands:

  label         Update the labels on a resource
  annotate      Update the annotations on a resource
  completion    Output shell completion code for the specified shell (bash, zsh or fish)

Other Commands:

  alpha         Commands for features in alpha
  api-resources Print the supported API resources on the server
  api-versions  Print the supported API versions on the server, in the form of "group/version"
  config        Modify kubeconfig files
  plugin        Provides utilities for interacting with plugins
  version       Print the client and server version information

Usage:
  kubectl [flags] [options]



# Viewing Resource Information

Nodes

kubectl get no
kubectl get no -o wide
kubectl describe no
kubectl get no -o yaml
kubectl get node --selector=[label_name]
kubectl get nodes -o jsonpath='{.items[*].status.addresses[?(@.type=="ExternalIP")].address}'
kubectl top node [node_name]

Pods

kubectl get po
kubectl get po -o wide
kubectl describe po
kubectl get po --show-labels
kubectl get po -l app=nginx
kubectl get po -o yaml
kubectl get pod [pod_name] -o yaml -- export
kubectl get pod [pod_name] -o yaml -- export > nameoffile.yaml
kubectl get pods --field-selector status.phase=Running

Namespaces

kubectl get ns
kubectl get ns -o yaml
kubectl describe ns

Deployments

kubectl get deploy
kubectl describe deploy
kubectl get deploy -o wide
kubectl get deploy -o yaml

Services

kubectl get svc
kubectl describe svc
kubectl get svc -o wide
kubectl get svc -o yaml
kubectl get svc --show-labels

Daemon Sets

kubectl get ds
kubectl get ds --all-namespaces
kubectl describe ds [daemonset_name] -n [namespace_name]
kubectl get ds [ds_name] -n [ns_name] -o yaml

Events

kubectl get events
kubectl get events -n kube-system
kubectl get events -w

Logs

kubectl logs [pod_name]
kubectl logs --since=1h [pod_name]
kubectl logs --tail=20 [pod_name]
kubectl logs -f -c [container_name][pod_name]
kubectl logs [pod_name] > pod.log

Service Accounts

kubectl get sa
kubectl get sa -o yaml
kubectl get serviceaccounts default -o yaml > ./sa.yaml
kubectl replace serviceaccount default -f . /sa.yaml

Replica Sets

kubectl get rs
kubectl describe rs
kubectl get rs -o wide
kubectl get rs -o yaml

Roles

kubectl get roles --all-namespaces
kubectl get roles --all-namespaces -o yaml

Secrets

kubectl get secrets
kubectl get secrets --all-namespaces
kubectl get secrets -o yaml

Config Maps

kubectl get cm
kubectl get cm --all-namespaces
kubectl get cm --all-namespaces -o yaml

Ingress

kubectl get ing
kubectl get ing --all-namespaces

Persistent Volume

kubectl get pv
kubectl describe pv

Persistent Volume Claim

kubectl get pvc
kubectl describe pvc

Storage Class

kubectl get sc
kubectl get sc -o yaml

Multiple Resources

kubectl get svc, po
kubectl get deploy, no
kubectl get all
kubectl get all --all-namespaces

# Changing Resource Attributes

Taint

kubectl taint [node_name] [taint_name]

Labels

kubectl label [node_name] disktype=ssd
kubectl label [pod_name] env=prod

Cordon/Uncordon

kubectl cordon [node_name]
kubectl uncordon [node_name]

Drain

kubectl drain [node_name]

Nodes/Pods

kubectl delete node [node_name]
kubectl delete pod [pod_name]
kubectl edit node [node_name]
kubectl edit pod [pod_name]

Deployments/Namespaces

kubectl edit deploy [deploy_name]
kubectl delete deploy [deploy_name]
kubectl expose deploy [deploy_name] --port=80 --type=NodePort
kubectl scale deploy [deploy_name] --replicas=5
kubectl delete ns
kubectl edit ns [ns_name]

Services

kubectl edit svc [svc_name]
kubectl delete svc [svc_name]

Daemon Sets

kubectl edit ds [ds_name] -n kube-system
kubectl delete ds [ds_name]

Service Accounts

kubectl edit sa [sa_name]
kubectl delete sa [sa_name]

Annotate

kubectl annotate po [pod_name] [annotation]
kubectl annotate no [node_name]

# Adding Resources

Creatinga Pod

kubectl create -f [name_of_f i l e]
kubectl apply -f [name_of_f i l e]
kubectl run [pod_name] --image=nginx --restart=Never
kubectl run [pod_name] --generator=run-pod/v1 --image=nginx
kubectl run [pod_name] --image=nginx --restart =Never

Creating a Service

kubectl create svc nodeport [svc_name] --tcp=8080:80

Creating a Deployment

kubectl create -f [name_of_file]
kubectl apply -f [name_of_file]
kubectl create deploy [deploy_name] --image=nginx

Interactive Pod

kubectl run [pod_name] --image=busybox --rm -it --restart=Never -- sh

Output YAML to a File

kubectl create deploy [deploy_name] --image=nginx --dry-run -o yaml > deploy.yaml
kubectl get po [pod_name] -o yaml --export > pod.yaml

Getting Help

kubectl -h
kubectl create -h
kubectl run -h
kubectl explain deploy.spec

# Requests

API Call

kubectl get --raw /apis/metrics.k8s.io/

Cluster Info

kubectl config
kubectl cluster-info
kubectl get componentstatuses



