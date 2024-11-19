# k8s-API-pods
Repo for activities of the k8s API and pods training

## k8s-fundamentals - Lab Instances

The k8s fundamentals training has some lab activities.

We'll be using the lab instances that were previously created.
If you do not have them please check the [k8s-fundamentals](https://github.com/asantos82/k8s-fundamentals) repo on how to set up the lab

## k8s-fundamentals - kubectl explain

Get cluster context to figure out which cluster we are connecting to.

```console
vagrant@c1-cp1:~$ kubectl config get-contexts 
CURRENT   NAME                          CLUSTER      AUTHINFO           NAMESPACE
*         kubernetes-admin@kubernetes   kubernetes   kubernetes-admin
```

If we had more than one context, i.e. an EKS and the local cluster, we could change the context by doing the following:

```console
vagrant@c1-cp1:~$ kubectl config use-context kubernetes-admin@kubernetes 
Switched to context "kubernetes-admin@kubernetes".
vagrant@c1-cp1:~$ kubectl config get-contexts
CURRENT   NAME                          CLUSTER      AUTHINFO           NAMESPACE
*         kubernetes-admin@kubernetes   kubernetes   kubernetes-admin
```

Get information about the API server for the context previously selected.

```console
vagrant@c1-cp1:~$ kubectl cluster-info 
Kubernetes control plane is running at https://192.168.1.10:6443
CoreDNS is running at https://192.168.1.10:6443/api/v1/namespaces/kube-system/services/kube-dns:dns/proxy

To further debug and diagnose cluster problems, use 'kubectl cluster-info dump'.
```

Get the list of API resources supported/available in the cluster.

```console
vagrant@c1-cp1:~$ kubectl api-resources 
NAME                              SHORTNAMES   APIVERSION                        NAMESPACED   KIND
bindings                                       v1                                true         Binding
componentstatuses                 cs           v1                                false        ComponentStatus
configmaps                        cm           v1                                true         ConfigMap
endpoints                         ep           v1                                true         Endpoints
events                            ev           v1                                true         Event
limitranges                       limits       v1                                true         LimitRange
namespaces                        ns           v1                                false        Namespace
nodes                             no           v1                                false        Node
persistentvolumeclaims            pvc          v1                                true         PersistentVolumeClaim
persistentvolumes                 pv           v1                                false        PersistentVolume
pods                              po           v1                                true         Pod
podtemplates                                   v1                                true         PodTemplate
replicationcontrollers            rc           v1                                true         ReplicationController
resourcequotas                    quota        v1                                true         ResourceQuota
secrets                                        v1                                true         Secret
serviceaccounts                   sa           v1                                true         ServiceAccount
services                          svc          v1                                true         Service
mutatingwebhookconfigurations                  admissionregistration.k8s.io/v1   false        MutatingWebhookConfiguration
validatingwebhookconfigurations                admissionregistration.k8s.io/v1   false        ValidatingWebhookConfiguration
customresourcedefinitions         crd,crds     apiextensions.k8s.io/v1           false        CustomResourceDefinition
apiservices                                    apiregistration.k8s.io/v1         false        APIService
controllerrevisions                            apps/v1                           true         ControllerRevision
daemonsets                        ds           apps/v1                           true         DaemonSet
deployments                       deploy       apps/v1                           true         Deployment
replicasets                       rs           apps/v1                           true         ReplicaSet
statefulsets                      sts          apps/v1                           true         StatefulSet
selfsubjectreviews                             authentication.k8s.io/v1          false        SelfSubjectReview
tokenreviews                                   authentication.k8s.io/v1          false        TokenReview
localsubjectaccessreviews                      authorization.k8s.io/v1           true         LocalSubjectAccessReview
selfsubjectaccessreviews                       authorization.k8s.io/v1           false        SelfSubjectAccessReview
selfsubjectrulesreviews                        authorization.k8s.io/v1           false        SelfSubjectRulesReview
subjectaccessreviews                           authorization.k8s.io/v1           false        SubjectAccessReview
horizontalpodautoscalers          hpa          autoscaling/v2                    true         HorizontalPodAutoscaler
cronjobs                          cj           batch/v1                          true         CronJob
jobs                                           batch/v1                          true         Job
certificatesigningrequests        csr          certificates.k8s.io/v1            false        CertificateSigningRequest
leases                                         coordination.k8s.io/v1            true         Lease
bgpconfigurations                              crd.projectcalico.org/v1          false        BGPConfiguration
bgpfilters                                     crd.projectcalico.org/v1          false        BGPFilter
bgppeers                                       crd.projectcalico.org/v1          false        BGPPeer
blockaffinities                                crd.projectcalico.org/v1          false        BlockAffinity
caliconodestatuses                             crd.projectcalico.org/v1          false        CalicoNodeStatus
clusterinformations                            crd.projectcalico.org/v1          false        ClusterInformation
felixconfigurations                            crd.projectcalico.org/v1          false        FelixConfiguration
globalnetworkpolicies                          crd.projectcalico.org/v1          false        GlobalNetworkPolicy
globalnetworksets                              crd.projectcalico.org/v1          false        GlobalNetworkSet
hostendpoints                                  crd.projectcalico.org/v1          false        HostEndpoint
ipamblocks                                     crd.projectcalico.org/v1          false        IPAMBlock
ipamconfigs                                    crd.projectcalico.org/v1          false        IPAMConfig
ipamhandles                                    crd.projectcalico.org/v1          false        IPAMHandle
ippools                                        crd.projectcalico.org/v1          false        IPPool
ipreservations                                 crd.projectcalico.org/v1          false        IPReservation
kubecontrollersconfigurations                  crd.projectcalico.org/v1          false        KubeControllersConfiguration
networkpolicies                                crd.projectcalico.org/v1          true         NetworkPolicy
networksets                                    crd.projectcalico.org/v1          true         NetworkSet
endpointslices                                 discovery.k8s.io/v1               true         EndpointSlice
events                            ev           events.k8s.io/v1                  true         Event
flowschemas                                    flowcontrol.apiserver.k8s.io/v1   false        FlowSchema
prioritylevelconfigurations                    flowcontrol.apiserver.k8s.io/v1   false        PriorityLevelConfiguration
ingressclasses                                 networking.k8s.io/v1              false        IngressClass
ingresses                         ing          networking.k8s.io/v1              true         Ingress
networkpolicies                   netpol       networking.k8s.io/v1              true         NetworkPolicy
runtimeclasses                                 node.k8s.io/v1                    false        RuntimeClass
poddisruptionbudgets              pdb          policy/v1                         true         PodDisruptionBudget
clusterrolebindings                            rbac.authorization.k8s.io/v1      false        ClusterRoleBinding
clusterroles                                   rbac.authorization.k8s.io/v1      false        ClusterRole
rolebindings                                   rbac.authorization.k8s.io/v1      true         RoleBinding
roles                                          rbac.authorization.k8s.io/v1      true         Role
priorityclasses                   pc           scheduling.k8s.io/v1              false        PriorityClass
csidrivers                                     storage.k8s.io/v1                 false        CSIDriver
csinodes                                       storage.k8s.io/v1                 false        CSINode
csistoragecapacities                           storage.k8s.io/v1                 true         CSIStorageCapacity
storageclasses                    sc           storage.k8s.io/v1                 false        StorageClass
volumeattachments                              storage.k8s.io/v1                 false        VolumeAttachment
```

### k8s-fundamentals - kubectl explain - pods

Let us use kubectl explain to dig into the structure of a resource, in this case, we'll look into pods.

```console
vagrant@c1-cp1:~$ kubectl explain pods
# We can inspect objects by digging into them as shown below
vagrant@c1-cp1:~$ kubectl explain pod.spec
vagrant@c1-cp1:~$ kubectl explain pod.spec.containers
```

We cannot create and deploy a pod manifest.

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: hello-world
spec:
  containers:
  - name: hello-world
    image: gcr.io/google-samples/hello-app:1.0
```

And before proceeding we can validate its format.

```console
vagrant@c1-cp1:~$ kubectl apply -f pods-manifest.yml --dry-run=server
error: error parsing pods-manifest.yml: error converting YAML to JSON: yaml: line 8: mapping values are not allowed in this context
# there was an error on the file that was corrected :D
# after the fix the output is ok
vagrant@c1-cp1:~$ kubectl apply -f pods-manifest.yml --dry-run=server
pod/hello-world created (server dry run)
```

Now we can create the pod and validate it is up and running.

```console
vagrant@c1-cp1:~$ kubectl apply -f pods-manifest.yml 
pod/hello-world created
vagrant@c1-cp1:~$ kubectl get pods
NAME          READY   STATUS    RESTARTS   AGE
hello-world   1/1     Running   0          10s
```

Let us clean up the pod deployment, and check it is gone.

```console
vagrant@c1-cp1:~$ kubectl apply -f pods-manifest.yml 
pod/hello-world created
vagrant@c1-cp1:~$ kubectl get pods
NAME          READY   STATUS    RESTARTS   AGE
hello-world   1/1     Running   0          10s
```

## k8s-fundamentals - kubectl
### k8s-fundamentals - kubectl --dry-run

We'll look at how to use the option dry-run to perform validation and create scaffolding manifest files.

Let us use the following hello-world-deployment.yml file.

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: hello-world
  labels:
    app: hello-world
spec:
  replicas: 4
  selector:
    matchLabels:
      app: hello-world
  template:
    metadata:
      labels:
        app: hello-world
    spec:
      containers:
      - name: hello-world
        image: gcr.io/google-samples/hello-app:1.0
        ports:
        - containerPort: 8080

```

We can validate the manifest server side.
It will be sent to the k8s API, but won't persist and no action will be done on the k8s cluster.

```console
vagrant@c1-cp1:~$ kubectl apply -f hello-world-deployment.yml --dry-run=server
deployment.apps/hello-world created (server dry run)
vagrant@c1-cp1:~$ kubectl get deployments
No resources found in default namespace.
```

Let's try client-side validation.

```console
vagrant@c1-cp1:~$ kubectl apply -f hello-world-deployment.yml --dry-run=client
deployment.apps/hello-world created (dry run)
vagrant@c1-cp1:~$ kubectl get deployments
No resources found in default namespace.
```

We'll be using a deployment manifest with a syntax error.

```yaml
vagrant@c1-cp1:~$ cat hello-world-deployment-error.yml 
apiVersion: apps/v1
kind: Deployment
metadata:
  name: hello-world
  labels:
    app: hello-world
spec:
  replicas: 4
  selector:
    matchLabels:
      app: hello-world
  template:
    metadata:
      labels:
        app: hello-world
    spec:
      containers:
      - name: hello-world
        imagei_: gcr.io/google-samples/hello-app:1.0
        ports:
        - containerPort: 8080
```

Let us run the validations with a dry run.

```console
vagrant@c1-cp1:~$ kubectl apply -f hello-world-deployment-error.yml --dry-run=server
Error from server (BadRequest): error when creating "hello-world-deployment-error.yml": Deployment in version "v1" cannot be handled as a Deployment: strict decoding error: unknown field "spec.template.spec.containers[0].imagei_"
vagrant@c1-cp1:~$ kubectl apply -f hello-world-deployment-error.yml --dry-run=client
deployment.apps/hello-world created (dry run)
```

Next, we'll be using the dry-run option to create correctly syntax manifests to make the creation of resources, and pod deployments, ... easier.

```console
# Check the deployment command is ok
vagrant@c1-cp1:~$ kubectl create deployment nginx --image=nginx --dry-run=client
deployment.apps/nginx created (dry run)

# Print manifest to stdout
vagrant@c1-cp1:~$ kubectl create deployment nginx --image=nginx --dry-run=client -o yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  creationTimestamp: null
  labels:
    app: nginx
  name: nginx
spec:
  replicas: 1
  selector:
    matchLabels:
      app: nginx
  strategy: {}
  template:
    metadata:
      creationTimestamp: null
      labels:
        app: nginx
    spec:
      containers:
      - image: nginx
        name: nginx
        resources: {}
status: {}

# We  can use dry-run to deploy like previously or pods like below
vagrant@c1-cp1:~$ kubectl run pod nginx-pod --image=nginx --dry-run=client -o yaml
apiVersion: v1
kind: Pod
metadata:
  creationTimestamp: null
  labels:
    run: pod
  name: pod
spec:
  containers:
  - args:
    - nginx-pod
    image: nginx
    name: pod
    resources: {}
  dnsPolicy: ClusterFirst
  restartPolicy: Always
status: {}

# We can redirect the stdout to a file
vagrant@c1-cp1:~$ kubectl create deployment nginx --image=nginx --dry-run=client -o yaml > nginx-deployment.yml
vagrant@c1-cp1:~$ cat nginx-deployment.yml 
apiVersion: apps/v1
kind: Deployment
metadata:
  creationTimestamp: null
  labels:
    app: nginx
  name: nginx
spec:
  replicas: 1
  selector:
    matchLabels:
      app: nginx
  strategy: {}
  template:
    metadata:
      creationTimestamp: null
      labels:
        app: nginx
    spec:
      containers:
      - image: nginx
        name: nginx
        resources: {}
status: {}

# We can use the file to create the deployment
vagrant@c1-cp1:~$ kubectl apply -f nginx-deployment.yml 
deployment.apps/nginx created
vagrant@c1-cp1:~$ kubectl get deployments.apps nginx 
NAME    READY   UP-TO-DATE   AVAILABLE   AGE
nginx   1/1     1            1           10s
vagrant@c1-cp1:~$ kubectl delete -f nginx-deployment.yml 
deployment.apps "nginx" deleted
vagrant@c1-cp1:~$ kubectl get deployments.apps nginx
Error from server (NotFound): deployments.apps "nginx" not found
```

### k8s-fundamentals - kubectl - diff

Let us create a deployment using the following file.

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: hello-world
  labels:
    app: hello-world
spec:
  replicas: 4
  selector:
    matchLabels:
      app: hello-world
  template:
    metadata:
      labels:
        app: hello-world
    spec:
      containers:
      - name: hello-world
        image: gcr.io/google-samples/hello-app:1.0
        ports:
        - containerPort: 8080
```

Let's create the deployment.

```console
vagrant@c1-cp1:~$ kubectl apply -f hello-world-deployment.yml 
deployment.apps/hello-world created
vagrant@c1-cp1:~$ kubectl get deployments.apps hello-world 
NAME          READY   UP-TO-DATE   AVAILABLE   AGE
hello-world   4/4     4            4           8s
```

Now we'll be using the file hello-world-deployment-diff.yml to check the differences between the deployment already running in the cluster and the changes that would be applied by `hello-world-deployment-diff.yml`

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: hello-world
  labels:
    app: hello-world
spec:
  replicas: 5
  selector:
    matchLabels:
      app: hello-world
  template:
    metadata:
      labels:
        app: hello-world
    spec:
      containers:
      - name: hello-world
        image: gcr.io/google-samples/hello-app:2.0
        ports:
        - containerPort: 8080
```

Now we can check the differences by executing the `kubectl diff` command.

```console
vagrant@c1-cp1:~$ kubectl diff -f hello-world-deployment-diff.yml 
diff -u -N /tmp/LIVE-471269671/apps.v1.Deployment.default.hello-world /tmp/MERGED-4056044988/apps.v1.Deployment.default.hello-world
--- /tmp/LIVE-471269671/apps.v1.Deployment.default.hello-world  2024-06-25 13:14:41.945870991 +0000
+++ /tmp/MERGED-4056044988/apps.v1.Deployment.default.hello-world       2024-06-25 13:14:41.945870991 +0000
@@ -6,7 +6,7 @@
     kubectl.kubernetes.io/last-applied-configuration: |
       {"apiVersion":"apps/v1","kind":"Deployment","metadata":{"annotations":{},"labels":{"app":"hello-world"},"name":"hello-world","namespace":"default"},"spec":{"replicas":4,"selector":{"matchLabels":{"app":"hello-world"}},"template":{"metadata":{"labels":{"app":"hello-world"}},"spec":{"containers":[{"image":"gcr.io/google-samples/hello-app:1.0","name":"hello-world","ports":[{"containerPort":8080}]}]}}}}       
   creationTimestamp: "2024-06-25T13:11:47Z"
-  generation: 1
+  generation: 2
   labels:
     app: hello-world
   name: hello-world
@@ -15,7 +15,7 @@
   uid: b616e1c7-34ad-49ef-acee-3d743fd1fa49
 spec:
   progressDeadlineSeconds: 600
-  replicas: 4
+  replicas: 5
   revisionHistoryLimit: 10
   selector:
     matchLabels:
@@ -32,7 +32,7 @@
         app: hello-world
     spec:
       containers:
-      - image: gcr.io/google-samples/hello-app:1.0
+      - image: gcr.io/google-samples/hello-app:2.0
         imagePullPolicy: IfNotPresent
         name: hello-world
         ports:
```

Let's clean up

```console
vagrant@c1-cp1:~$ kubectl delete -f hello-world-deployment.yml 
deployment.apps "hello-world" deleted
vagrant@c1-cp1:~$ kubectl get deployments.apps
No resources found in default namespace.
```

## k8s-fundamentals - API resources

We can explore the APIs available and their versions.
The version can be in alpha, beta, or stable.

```console
# List all available API resources
vagrant@c1-cp1:~$ kubectl api-resources 
NAME                              SHORTNAMES   APIVERSION                        NAMESPACED   KIND
bindings                                       v1                                true         Binding
componentstatuses                 cs           v1                                false        ComponentStatus
configmaps                        cm           v1                                true         ConfigMap
endpoints                         ep           v1                                true         Endpoints
events                            ev           v1                                true         Event
limitranges                       limits       v1                                true         LimitRange
namespaces                        ns           v1                                false        Namespace
nodes                             no           v1                                false        Node
persistentvolumeclaims            pvc          v1                                true         PersistentVolumeClaim
persistentvolumes                 pv           v1                                false        PersistentVolume
pods                              po           v1                                true         Pod
podtemplates                                   v1                                true         PodTemplate
replicationcontrollers            rc           v1                                true         ReplicationController
resourcequotas                    quota        v1                                true         ResourceQuota
secrets                                        v1                                true         Secret
serviceaccounts                   sa           v1                                true         ServiceAccount
services                          svc          v1                                true         Service
mutatingwebhookconfigurations                  admissionregistration.k8s.io/v1   false        MutatingWebhookConfiguration
validatingwebhookconfigurations                admissionregistration.k8s.io/v1   false        ValidatingWebhookConfiguration
customresourcedefinitions         crd,crds     apiextensions.k8s.io/v1           false        CustomResourceDefinition
apiservices                                    apiregistration.k8s.io/v1         false        APIService
controllerrevisions                            apps/v1                           true         ControllerRevision
daemonsets                        ds           apps/v1                           true         DaemonSet
deployments                       deploy       apps/v1                           true         Deployment
replicasets                       rs           apps/v1                           true         ReplicaSet
statefulsets                      sts          apps/v1                           true         StatefulSet
selfsubjectreviews                             authentication.k8s.io/v1          false        SelfSubjectReview
tokenreviews                                   authentication.k8s.io/v1          false        TokenReview
localsubjectaccessreviews                      authorization.k8s.io/v1           true         LocalSubjectAccessReview
selfsubjectaccessreviews                       authorization.k8s.io/v1           false        SelfSubjectAccessReview
selfsubjectrulesreviews                        authorization.k8s.io/v1           false        SelfSubjectRulesReview
subjectaccessreviews                           authorization.k8s.io/v1           false        SubjectAccessReview
horizontalpodautoscalers          hpa          autoscaling/v2                    true         HorizontalPodAutoscaler
cronjobs                          cj           batch/v1                          true         CronJob
jobs                                           batch/v1                          true         Job
certificatesigningrequests        csr          certificates.k8s.io/v1            false        CertificateSigningRequest
leases                                         coordination.k8s.io/v1            true         Lease
bgpconfigurations                              crd.projectcalico.org/v1          false        BGPConfiguration
bgpfilters                                     crd.projectcalico.org/v1          false        BGPFilter
bgppeers                                       crd.projectcalico.org/v1          false        BGPPeer
blockaffinities                                crd.projectcalico.org/v1          false        BlockAffinity
caliconodestatuses                             crd.projectcalico.org/v1          false        CalicoNodeStatus
clusterinformations                            crd.projectcalico.org/v1          false        ClusterInformation
felixconfigurations                            crd.projectcalico.org/v1          false        FelixConfiguration
globalnetworkpolicies                          crd.projectcalico.org/v1          false        GlobalNetworkPolicy
globalnetworksets                              crd.projectcalico.org/v1          false        GlobalNetworkSet
hostendpoints                                  crd.projectcalico.org/v1          false        HostEndpoint
ipamblocks                                     crd.projectcalico.org/v1          false        IPAMBlock
ipamconfigs                                    crd.projectcalico.org/v1          false        IPAMConfig
ipamhandles                                    crd.projectcalico.org/v1          false        IPAMHandle
ippools                                        crd.projectcalico.org/v1          false        IPPool
ipreservations                                 crd.projectcalico.org/v1          false        IPReservation
kubecontrollersconfigurations                  crd.projectcalico.org/v1          false        KubeControllersConfiguration
networkpolicies                                crd.projectcalico.org/v1          true         NetworkPolicy
networksets                                    crd.projectcalico.org/v1          true         NetworkSet
endpointslices                                 discovery.k8s.io/v1               true         EndpointSlice
events                            ev           events.k8s.io/v1                  true         Event
flowschemas                                    flowcontrol.apiserver.k8s.io/v1   false        FlowSchema
prioritylevelconfigurations                    flowcontrol.apiserver.k8s.io/v1   false        PriorityLevelConfiguration
ingressclasses                                 networking.k8s.io/v1              false        IngressClass
ingresses                         ing          networking.k8s.io/v1              true         Ingress
networkpolicies                   netpol       networking.k8s.io/v1              true         NetworkPolicy
runtimeclasses                                 node.k8s.io/v1                    false        RuntimeClass
poddisruptionbudgets              pdb          policy/v1                         true         PodDisruptionBudget
clusterrolebindings                            rbac.authorization.k8s.io/v1      false        ClusterRoleBinding
clusterroles                                   rbac.authorization.k8s.io/v1      false        ClusterRole
rolebindings                                   rbac.authorization.k8s.io/v1      true         RoleBinding
roles                                          rbac.authorization.k8s.io/v1      true         Role
priorityclasses                   pc           scheduling.k8s.io/v1              false        PriorityClass
csidrivers                                     storage.k8s.io/v1                 false        CSIDriver
csinodes                                       storage.k8s.io/v1                 false        CSINode
csistoragecapacities                           storage.k8s.io/v1                 true         CSIStorageCapacity
storageclasses                    sc           storage.k8s.io/v1                 false        StorageClass
volumeattachments                              storage.k8s.io/v1                 false        VolumeAttachment

# List all resources available "grouped" by API Group
vagrant@c1-cp1:~$ kubectl api-resources  --api-group=apps
NAME                  SHORTNAMES   APIVERSION   NAMESPACED   KIND
controllerrevisions                apps/v1      true         ControllerRevision
daemonsets            ds           apps/v1      true         DaemonSet
deployments           deploy       apps/v1      true         Deployment
replicasets           rs           apps/v1      true         ReplicaSet
statefulsets          sts          apps/v1      true         StatefulSet

# Explain by version
vagrant@c1-cp1:~$ kubectl explain deployment --api-version apps/v1
GROUP:      apps
KIND:       Deployment
VERSION:    v1

DESCRIPTION:
    Deployment enables declarative updates for Pods and ReplicaSets.

FIELDS:
  apiVersion    <string>
    APIVersion defines the versioned schema of this representation of an object.
    Servers should convert recognized schemas to the latest internal value, and
    may reject unrecognized values. More info:
    https://git.k8s.io/community/contributors/devel/sig-architecture/api-conventions.md#resources

  kind  <string>
    Kind is a string value representing the REST resource this object
    represents. Servers may infer this from the endpoint the client submits
    requests to. Cannot be updated. In CamelCase. More info:
    https://git.k8s.io/community/contributors/devel/sig-architecture/api-conventions.md#types-kinds

  metadata      <ObjectMeta>
    Standard object's metadata. More info:
    https://git.k8s.io/community/contributors/devel/sig-architecture/api-conventions.md#metadata

  spec  <DeploymentSpec>
    Specification of the desired behavior of the Deployment.

  status        <DeploymentStatus>
    Most recently observed status of the Deployment.

# List all versions of the APIs available
vagrant@c1-cp1:~$ kubectl api-versions | sort
admissionregistration.k8s.io/v1
apiextensions.k8s.io/v1
apiregistration.k8s.io/v1
apps/v1
authentication.k8s.io/v1
authorization.k8s.io/v1
autoscaling/v1
autoscaling/v2
batch/v1
certificates.k8s.io/v1
coordination.k8s.io/v1
crd.projectcalico.org/v1
discovery.k8s.io/v1
events.k8s.io/v1
flowcontrol.apiserver.k8s.io/v1
flowcontrol.apiserver.k8s.io/v1beta3
networking.k8s.io/v1
node.k8s.io/v1
policy/v1
rbac.authorization.k8s.io/v1
scheduling.k8s.io/v1
storage.k8s.io/v1
v1
```

## k8s-fundamentals - API Request

We can add several levels of verbose to the `kubectl get pod` API calls.
By increasing the verbose level we can see more details about the requests made to the server and the responses retrieved from the server.

```console
vagrant@c1-cp1:~$ kubectl apply -f pods-manifest.yml
pod/hello-world created
vagrant@c1-cp1:~$ kubectl get pod hello-world
NAME          READY   STATUS    RESTARTS   AGE
hello-world   1/1     Running   0          32m

vagrant@c1-cp1:~$ kubectl get pod hello-world -v 6
I0625 15:20:54.914283    4571 loader.go:395] Config loaded from file:  /home/vagrant/.kube/config
I0625 15:20:54.931453    4571 round_trippers.go:553] GET https://192.168.1.10:6443/api/v1/namespaces/default/pods/hello-world 200 OK in 8 milliseconds
NAME          READY   STATUS    RESTARTS   AGE
hello-world   1/1     Running   0          32m

vagrant@c1-cp1:~$ kubectl get pod hello-world -v 7
I0625 15:21:09.183307    4693 loader.go:395] Config loaded from file:  /home/vagrant/.kube/config
I0625 15:21:09.190673    4693 round_trippers.go:463] GET https://192.168.1.10:6443/api/v1/namespaces/default/pods/hello-world
I0625 15:21:09.190833    4693 round_trippers.go:469] Request Headers:
I0625 15:21:09.190843    4693 round_trippers.go:473]     Accept: application/json;as=Table;v=v1;g=meta.k8s.io,application/json;as=Table;v=v1beta1;g=meta.k8s.io,application/json
I0625 15:21:09.191062    4693 round_trippers.go:473]     User-Agent: kubectl/v1.29.3 (linux/amd64) kubernetes/6813625
I0625 15:21:09.200030    4693 round_trippers.go:574] Response Status: 200 OK in 8 milliseconds
NAME          READY   STATUS    RESTARTS   AGE
hello-world   1/1     Running   0          32m

vagrant@c1-cp1:~$ kubectl get pod hello-world -v 8
I0625 15:22:41.820877    5545 loader.go:395] Config loaded from file:  /home/vagrant/.kube/config
I0625 15:22:41.829292    5545 round_trippers.go:463] GET https://192.168.1.10:6443/api/v1/namespaces/default/pods/hello-world
I0625 15:22:41.829317    5545 round_trippers.go:469] Request Headers:
I0625 15:22:41.829340    5545 round_trippers.go:473]     Accept: application/json;as=Table;v=v1;g=meta.k8s.io,application/json;as=Table;v=v1beta1;g=meta.k8s.io,application/json
I0625 15:22:41.829352    5545 round_trippers.go:473]     User-Agent: kubectl/v1.29.3 (linux/amd64) kubernetes/6813625
I0625 15:22:41.835744    5545 round_trippers.go:574] Response Status: 200 OK in 6 milliseconds
I0625 15:22:41.835775    5545 round_trippers.go:577] Response Headers:
I0625 15:22:41.835839    5545 round_trippers.go:580]     Audit-Id: 76ba3e0c-2e34-413c-9007-ca46e54fa0de
I0625 15:22:41.835876    5545 round_trippers.go:580]     Cache-Control: no-cache, private
I0625 15:22:41.835886    5545 round_trippers.go:580]     Content-Type: application/json
I0625 15:22:41.835898    5545 round_trippers.go:580]     X-Kubernetes-Pf-Flowschema-Uid: c5fe77bd-459a-432a-acc7-aaa26202b970
I0625 15:22:41.835931    5545 round_trippers.go:580]     X-Kubernetes-Pf-Prioritylevel-Uid: 56973fcb-d667-42e8-a872-0f50f7b95e1e
I0625 15:22:41.835944    5545 round_trippers.go:580]     Date: Tue, 25 Jun 2024 15:22:41 GMT
I0625 15:22:41.836125    5545 request.go:1212] Response Body: {"kind":"Table","apiVersion":"meta.k8s.io/v1","metadata":{"resourceVersion":"279474"},"columnDefinitions":[{"name":"Name","type":"string","format":"name","description":"Name must be unique within a namespace. Is required when creating resources, although some resources may allow a client to request the generation of an appropriate name automatically. Name is primarily intended for creation idempotence and configuration definition. Cannot be updated. More info: https://kubernetes.io/docs/concepts/overview/working-with-objects/names#names","priority":0},{"name":"Ready","type":"string","format":"","description":"The aggregate readiness state of this pod for accepting traffic.","priority":0},{"name":"Status","type":"string","format":"","description":"The aggregate status of the containers in this pod.","priority":0},{"name":"Restarts","type":"string","format":"","description":"The number of times the containers in this pod have been restarted and when the last container in this pod has restarted.","priority":0},{ [truncated 4499 chars]
NAME          READY   STATUS    RESTARTS   AGE
hello-world   1/1     Running   0          34m

vagrant@c1-cp1:~$ kubectl get pod hello-world -v 9
I0625 15:22:45.359482    5614 loader.go:395] Config loaded from file:  /home/vagrant/.kube/config
I0625 15:22:45.366032    5614 round_trippers.go:466] curl -v -XGET  -H "Accept: application/json;as=Table;v=v1;g=meta.k8s.io,application/json;as=Table;v=v1beta1;g=meta.k8s.io,application/json" -H "User-Agent: kubectl/v1.29.3 (linux/amd64) kubernetes/6813625" 'https://192.168.1.10:6443/api/v1/namespaces/default/pods/hello-world'
I0625 15:22:45.367683    5614 round_trippers.go:510] HTTP Trace: Dial to tcp:192.168.1.10:6443 succeed
I0625 15:22:45.374940    5614 round_trippers.go:553] GET https://192.168.1.10:6443/api/v1/namespaces/default/pods/hello-world 200 OK in 8 milliseconds
I0625 15:22:45.374993    5614 round_trippers.go:570] HTTP Statistics: DNSLookup 0 ms Dial 0 ms TLSHandshake 4 ms ServerProcessing 0 ms Duration 8 ms
I0625 15:22:45.375007    5614 round_trippers.go:577] Response Headers:
I0625 15:22:45.375024    5614 round_trippers.go:580]     X-Kubernetes-Pf-Prioritylevel-Uid: 56973fcb-d667-42e8-a872-0f50f7b95e1e
I0625 15:22:45.375040    5614 round_trippers.go:580]     Date: Tue, 25 Jun 2024 15:22:45 GMT
I0625 15:22:45.375055    5614 round_trippers.go:580]     Audit-Id: c68ff1e3-c4e8-4732-a3a9-904c2d620fee
I0625 15:22:45.375070    5614 round_trippers.go:580]     Cache-Control: no-cache, private
I0625 15:22:45.375084    5614 round_trippers.go:580]     Content-Type: application/json
I0625 15:22:45.375097    5614 round_trippers.go:580]     X-Kubernetes-Pf-Flowschema-Uid: c5fe77bd-459a-432a-acc7-aaa26202b970
I0625 15:22:45.375426    5614 request.go:1212] Response Body: {"kind":"Table","apiVersion":"meta.k8s.io/v1","metadata":{"resourceVersion":"279474"},"columnDefinitions":[{"name":"Name","type":"string","format":"name","description":"Name must be unique within a namespace. Is required when creating resources, although some resources may allow a client to request the generation of an appropriate name automatically. Name is primarily intended for creation idempotence and configuration definition. Cannot be updated. More info: https://kubernetes.io/docs/concepts/overview/working-with-objects/names#names","priority":0},{"name":"Ready","type":"string","format":"","description":"The aggregate readiness state of this pod for accepting traffic.","priority":0},{"name":"Status","type":"string","format":"","description":"The aggregate status of the containers in this pod.","priority":0},{"name":"Restarts","type":"string","format":"","description":"The number of times the containers in this pod have been restarted and when the last container in this pod has restarted.","priority":0},{"name":"Age","type":"string","format":"","description":"CreationTimestamp is a timestamp representing the server time when this object was created. It is not guaranteed to be set in happens-before order across separate operations. Clients may not set this value. It is represented in RFC3339 form and is in UTC.\n\nPopulated by the system. Read-only. Null for lists. More info: https://git.k8s.io/community/contributors/devel/sig-architecture/api-conventions.md#metadata","priority":0},{"name":"IP","type":"string","format":"","description":"podIP address allocated to the pod. Routable at least within the cluster. Empty if not yet allocated.","priority":1},{"name":"Node","type":"string","format":"","description":"NodeName is a request to schedule this pod onto a specific node. If it is non-empty, the scheduler simply schedules this pod onto that node, assuming that it fits resource requirements.","priority":1},{"name":"Nominated Node","type":"string","format":"","description":"nominatedNodeName is set only when this pod preempts other pods on the node, but it cannot be scheduled right away as preemption victims receive their graceful termination periods. This field does not guarantee that the pod will be scheduled on this node. Scheduler may decide to place the pod elsewhere if other nodes become available sooner. Scheduler may also decide to give the resources on this node to a higher priority pod that is created after preemption. As a result, this field may be different than PodSpec.nodeName when the pod is scheduled.","priority":1},{"name":"Readiness Gates","type":"string","format":"","description":"If specified, all readiness gates will be evaluated for pod readiness. A pod is ready when all its containers are ready AND all conditions specified in the readiness gates have status equal to \"True\" More info: https://git.k8s.io/enhancements/keps/sig-network/580-pod-readiness-gates","priority":1}],"rows":[{"cells":["hello-world","1/1","Running","0","34m","10.0.15.103","c1-node1","\u003cnone\u003e","\u003cnone\u003e"],"object":{"kind":"PartialObjectMetadata","apiVersion":"meta.k8s.io/v1","metadata":{"name":"hello-world","namespace":"default","uid":"0b295a7b-7365-44a0-a983-708112008c8b","resourceVersion":"279474","creationTimestamp":"2024-06-25T14:48:12Z","annotations":{"cni.projectcalico.org/containerID":"af35e1331e914fd27b586411601213e968db9e05b6dd5d893b9745fb7c4361f8","cni.projectcalico.org/podIP":"10.0.15.103/32","cni.projectcalico.org/podIPs":"10.0.15.103/32","kubectl.kubernetes.io/last-applied-configuration":"{\"apiVersion\":\"v1\",\"kind\":\"Pod\",\"metadata\":{\"annotations\":{},\"name\":\"hello-world\",\"namespace\":\"default\"},\"spec\":{\"containers\":[{\"image\":\"gcr.io/google-samples/hello-app:1.0\",\"name\":\"hello-world\"}]}}\n"},"managedFields":[{"manager":"kubectl-client-side-apply","operation":"Update","apiVersion":"v1","time":"2024-06-25T14:48:12Z","fieldsType":"FieldsV1","fieldsV1":{"f:metadata":{"f:annotations":{".":{},"f:kubectl.kubernetes.io/last-applied-configuration":{}}},"f:spec":{"f:containers":{"k:{\"name\":\"hello-world\"}":{".":{},"f:image":{},"f:imagePullPolicy":{},"f:name":{},"f:resources":{},"f:terminationMessagePath":{},"f:terminationMessagePolicy":{}}},"f:dnsPolicy":{},"f:enableServiceLinks":{},"f:restartPolicy":{},"f:schedulerName":{},"f:securityContext":{},"f:terminationGracePeriodSeconds":{}}}},{"manager":"calico","operation":"Update","apiVersion":"v1","time":"2024-06-25T15:19:26Z","fieldsType":"FieldsV1","fieldsV1":{"f:metadata":{"f:annotations":{"f:cni.projectcalico.org/containerID":{},"f:cni.projectcalico.org/podIP":{},"f:cni.projectcalico.org/podIPs":{}}}},"subresource":"status"},{"manager":"kubelet","operation":"Update","apiVersion":"v1","time":"2024-06-25T15:19:27Z","fieldsType":"FieldsV1","fieldsV1":{"f:status":{"f:conditions":{"k:{\"type\":\"ContainersReady\"}":{".":{},"f:lastProbeTime":{},"f:lastTransitionTime":{},"f:status":{},"f:type":{}},"k:{\"type\":\"Initialized\"}":{".":{},"f:lastProbeTime":{},"f:lastTransitionTime":{},"f:status":{},"f:type":{}},"k:{\"type\":\"PodReadyToStartContainers\"}":{".":{},"f:lastProbeTime":{},"f:lastTransitionTime":{},"f:status":{},"f:type":{}},"k:{\"type\":\"Ready\"}":{".":{},"f:lastProbeTime":{},"f:lastTransitionTime":{},"f:status":{},"f:type":{}}},"f:containerStatuses":{},"f:hostIP":{},"f:hostIPs":{},"f:phase":{},"f:podIP":{},"f:podIPs":{".":{},"k:{\"ip\":\"10.0.15.103\"}":{".":{},"f:ip":{}}},"f:startTime":{}}},"subresource":"status"}]}}}]}
NAME          READY   STATUS    RESTARTS   AGE
hello-world   1/1     Running   0          34m
```

```console
vagrant@c1-cp1:~$ kubectl proxy &
[1] 8839
vagrant@c1-cp1:~$ curl http://localhost:8001/api/v1/namespaces/default/pods/hello-world
{
  "kind": "Pod",
  "apiVersion": "v1",
  "metadata": {
    "name": "hello-world",
    "namespace": "default",
    "uid": "0b295a7b-7365-44a0-a983-708112008c8b",
    "resourceVersion": "279474",
    "creationTimestamp": "2024-06-25T14:48:12Z",
    "annotations": {
      "cni.projectcalico.org/containerID": "af35e1331e914fd27b586411601213e968db9e05b6dd5d893b9745fb7c4361f8",
      "cni.projectcalico.org/podIP": "10.0.15.103/32",
      "cni.projectcalico.org/podIPs": "10.0.15.103/32",
      "kubectl.kubernetes.io/last-applied-configuration": "{\"apiVersion\":\"v1\",\"kind\":\"Pod\",\"metadata\":{\"annotations\":{},\"name\":\"hello-world\",\"namespace\":\"default\"},\"spec\":{\"containers\":[{\"image\":\"gcr.io/google-samples/hello-app:1.0\",\"name\":\"hello-world\"}]}}\n"
    },
    "managedFields": [
      {
        "manager": "kubectl-client-side-apply",
        "operation": "Update",
        "apiVersion": "v1",
        "time": "2024-06-25T14:48:12Z",
        "fieldsType": "FieldsV1",
        "fieldsV1": {
          "f:metadata": {
            "f:annotations": {
              ".": {},
              "f:kubectl.kubernetes.io/last-applied-configuration": {}
            }
          },
          "f:spec": {
            "f:containers": {
              "k:{\"name\":\"hello-world\"}": {
                ".": {},
                "f:image": {},
                "f:imagePullPolicy": {},
                "f:name": {},
                "f:resources": {},
                "f:terminationMessagePath": {},
                "f:terminationMessagePolicy": {}
              }
            },
            "f:dnsPolicy": {},
            "f:enableServiceLinks": {},
            "f:restartPolicy": {},
            "f:schedulerName": {},
            "f:securityContext": {},
            "f:terminationGracePeriodSeconds": {}
          }
        }
      },
      {
        "manager": "calico",
        "operation": "Update",
        "apiVersion": "v1",
        "time": "2024-06-25T15:19:26Z",
        "fieldsType": "FieldsV1",
        "fieldsV1": {
          "f:metadata": {
            "f:annotations": {
              "f:cni.projectcalico.org/containerID": {},
              "f:cni.projectcalico.org/podIP": {},
              "f:cni.projectcalico.org/podIPs": {}
            }
          }
        },
        "subresource": "status"
      },
      {
        "manager": "kubelet",
        "operation": "Update",
        "apiVersion": "v1",
        "time": "2024-06-25T15:19:27Z",
        "fieldsType": "FieldsV1",
        "fieldsV1": {
          "f:status": {
            "f:conditions": {
              "k:{\"type\":\"ContainersReady\"}": {
                ".": {},
                "f:lastProbeTime": {},
                "f:lastTransitionTime": {},
                "f:status": {},
                "f:type": {}
              },
              "k:{\"type\":\"Initialized\"}": {
                ".": {},
                "f:lastProbeTime": {},
                "f:lastTransitionTime": {},
                "f:status": {},
                "f:type": {}
              },
              "k:{\"type\":\"PodReadyToStartContainers\"}": {
                ".": {},
                "f:lastProbeTime": {},
                "f:lastTransitionTime": {},
                "f:status": {},
                "f:type": {}
              },
              "k:{\"type\":\"Ready\"}": {
                ".": {},
                "f:lastProbeTime": {},
                "f:lastTransitionTime": {},
                "f:status": {},
                "f:type": {}
              }
            },
            "f:containerStatuses": {},
            "f:hostIP": {},
            "f:hostIPs": {},
            "f:phase": {},
            "f:podIP": {},
            "f:podIPs": {
              ".": {},
              "k:{\"ip\":\"10.0.15.103\"}": {
                ".": {},
                "f:ip": {}
              }
            },
            "f:startTime": {}
          }
        },
        "subresource": "status"
      }
    ]
  },
  "spec": {
    "volumes": [
      {
        "name": "kube-api-access-jrkgl",
        "projected": {
          "sources": [
            {
              "serviceAccountToken": {
                "expirationSeconds": 3607,
                "path": "token"
              }
            },
            {
              "configMap": {
                "name": "kube-root-ca.crt",
                "items": [
                  {
                    "key": "ca.crt",
                    "path": "ca.crt"
                  }
                ]
              }
            },
            {
              "downwardAPI": {
                "items": [
                  {
                    "path": "namespace",
                    "fieldRef": {
                      "apiVersion": "v1",
                      "fieldPath": "metadata.namespace"
                    }
                  }
                ]
              }
            }
          ],
          "defaultMode": 420
        }
      }
    ],
    "containers": [
      {
        "name": "hello-world",
        "image": "gcr.io/google-samples/hello-app:1.0",
        "resources": {},
        "volumeMounts": [
          {
            "name": "kube-api-access-jrkgl",
            "readOnly": true,
            "mountPath": "/var/run/secrets/kubernetes.io/serviceaccount"
          }
        ],
        "terminationMessagePath": "/dev/termination-log",
        "terminationMessagePolicy": "File",
        "imagePullPolicy": "IfNotPresent"
      }
    ],
    "restartPolicy": "Always",
    "terminationGracePeriodSeconds": 30,
    "dnsPolicy": "ClusterFirst",
    "serviceAccountName": "default",
    "serviceAccount": "default",
    "nodeName": "c1-node1",
    "securityContext": {},
    "schedulerName": "default-scheduler",
    "tolerations": [
      {
        "key": "node.kubernetes.io/not-ready",
        "operator": "Exists",
        "effect": "NoExecute",
        "tolerationSeconds": 300
      },
      {
        "key": "node.kubernetes.io/unreachable",
        "operator": "Exists",
        "effect": "NoExecute",
        "tolerationSeconds": 300
      }
    ],
    "priority": 0,
    "enableServiceLinks": true,
    "preemptionPolicy": "PreemptLowerPriority"
  },
  "status": {
    "phase": "Running",
    "conditions": [
      {
        "type": "PodReadyToStartContainers",
        "status": "True",
        "lastProbeTime": null,
        "lastTransitionTime": "2024-06-25T15:19:24Z"
      },
      {
        "type": "Initialized",
        "status": "True",
        "lastProbeTime": null,
        "lastTransitionTime": "2024-06-25T14:48:12Z"
      },
      {
        "type": "Ready",
        "status": "True",
        "lastProbeTime": null,
        "lastTransitionTime": "2024-06-25T15:19:24Z"
      },
      {
        "type": "ContainersReady",
        "status": "True",
        "lastProbeTime": null,
        "lastTransitionTime": "2024-06-25T15:19:24Z"
      },
      {
        "type": "PodScheduled",
        "status": "True",
        "lastProbeTime": null,
        "lastTransitionTime": "2024-06-25T14:48:12Z"
      }
    ],
    "hostIP": "192.168.1.20",
    "hostIPs": [
      {
        "ip": "192.168.1.20"
      }
    ],
    "podIP": "10.0.15.103",
    "podIPs": [
      {
        "ip": "10.0.15.103"
      }
    ],
    "startTime": "2024-06-25T14:48:12Z",
    "containerStatuses": [
      {
        "name": "hello-world",
        "state": {
          "running": {
            "startedAt": "2024-06-25T15:19:23Z"
          }
        },
        "lastState": {},
        "ready": true,
        "restartCount": 0,
        "image": "gcr.io/google-samples/hello-app:1.0",
        "imageID": "gcr.io/google-samples/hello-app@sha256:b1455e1c4fcc5ea1023c9e3b584cd84b64eb920e332feff690a2829696e379e7",
        "containerID": "containerd://757c70c48a431c72d2facb2a3fa91c662922687eb9264195379fde9544f38dee",
        "started": true
      }
    ],
    "qosClass": "BestEffort"
  }
}vagrant@c1-cp1:~$
```

## k8s-fundamentals - API Request - Watch, Exec Log
### k8s-fundamentals - API Request - Watch

```console
vagrant@c1-cp1:~$ kubectl get pods --watch -v 6 &
[1] 20246
vagrant@c1-cp1:~$ I0625 15:48:14.746068   20246 loader.go:395] Config loaded from file:  /home/vagrant/.kube/config
I0625 15:48:14.763424   20246 round_trippers.go:553] GET https://192.168.1.10:6443/api/v1/namespaces/default/pods?limit=500 200 OK in 9 milliseconds
NAME          READY   STATUS    RESTARTS   AGE
hello-world   1/1     Running   0          2m14s
I0625 15:48:14.767455   20246 round_trippers.go:553] GET https://192.168.1.10:6443/api/v1/namespaces/default/pods?resourceVersion=282308&watch=true 200 OK in 1 milliseconds

vagrant@c1-cp1:~$ netstat -naptu | grep kubectl
(Not all processes could be identified, non-owned process info
 will not be shown, you would have to be root to see it all.)
tcp        0      0 192.168.1.10:60494      192.168.1.10:6443       ESTABLISHED 20246/kubectl
vagrant@c1-cp1:~$ kubectl delete pods hello-world 
hello-world   1/1     Terminating   0          2m49s
pod "hello-world" deleted
hello-world   1/1     Terminating   0          2m49s
hello-world   0/1     Terminating   0          2m49s
hello-world   0/1     Terminating   0          2m50s
hello-world   0/1     Terminating   0          2m50s
hello-world   0/1     Terminating   0          2m50s
vagrant@c1-cp1:~$ kubectl apply -f pods-manifest.yml 
hello-worldpod/hello-world created
   0/1     Pending       0          0s
vagrant@c1-cp1:~$ hello-world   0/1     Pending       0          0s
hello-world   0/1     ContainerCreating   0          0s
hello-world   0/1     ContainerCreating   0          1s
hello-world   1/1     Running             0          1s

vagrant@c1-cp1:~$ fg
kubectl get pods --watch -v 6
```

### k8s-fundamentals - API Request - Exec

> [!IMPORTANT]
>
> Container image was built using a distroless image for its base. So no bash or any other OS binaries are present.
>
> https://github.com/GoogleCloudPlatform/kubernetes-engine-samples/blob/7fed665b624c92d7e787ca75b506b2d163a2cafb/quickstarts/hello-app/Dockerfile
>
> Let's get an older version of the container not build on a distroless image

Let us create a new pod manifest named `pods-exec-manifest.yml`

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: hello-world-exec
spec:
  containers:
  - name: hello-world-exec
    image: gcr.io/google-samples/hello-app@sha256:2b0febe1b9bd01739999853380b1a939e8102fd0dc5e2ff1fc6892c4557d52b9
```

Deploy the manifest

```console
vagrant@c1-cp1:~$ kubectl apply -f pods-exec-manifest.yml 
pod/hello-world-exec created
vagrant@c1-cp1:~$ kubectl get pods
NAME               READY   STATUS    RESTARTS   AGE
hello-world        1/1     Running   0          5m35s
hello-world-exec   1/1     Running   0          91s
```

Run `kubectl exec` to connect to the container and pay attention to the API call being made.

```console
vagrant@c1-cp1:~$ kubectl exec pods/hello-world-exec -v 7 -it -- /bin/sh
I0625 16:05:39.873999   30433 loader.go:395] Config loaded from file:  /home/vagrant/.kube/config
I0625 16:05:39.880088   30433 round_trippers.go:463] GET https://192.168.1.10:6443/api/v1/namespaces/default/pods/hello-world-exec
I0625 16:05:39.880134   30433 round_trippers.go:469] Request Headers:
I0625 16:05:39.880148   30433 round_trippers.go:473]     Accept: application/json, */*
I0625 16:05:39.880161   30433 round_trippers.go:473]     User-Agent: kubectl/v1.29.3 (linux/amd64) kubernetes/6813625
I0625 16:05:39.888048   30433 round_trippers.go:574] Response Status: 200 OK in 7 milliseconds
I0625 16:05:39.890042   30433 podcmd.go:88] Defaulting container name to hello-world-exec
I0625 16:05:39.890826   30433 round_trippers.go:463] POST https://192.168.1.10:6443/api/v1/namespaces/default/pods/hello-world-exec/exec?command=%2Fbin%2Fsh&container=hello-world-exec&stdin=true&stdout=true&tty=true
I0625 16:05:39.890849   30433 round_trippers.go:469] Request Headers:
I0625 16:05:39.890856   30433 round_trippers.go:473]     X-Stream-Protocol-Version: v5.channel.k8s.io
I0625 16:05:39.890861   30433 round_trippers.go:473]     X-Stream-Protocol-Version: v4.channel.k8s.io
I0625 16:05:39.890865   30433 round_trippers.go:473]     X-Stream-Protocol-Version: v3.channel.k8s.io
I0625 16:05:39.890870   30433 round_trippers.go:473]     X-Stream-Protocol-Version: v2.channel.k8s.io
I0625 16:05:39.890874   30433 round_trippers.go:473]     X-Stream-Protocol-Version: channel.k8s.io
I0625 16:05:39.890879   30433 round_trippers.go:473]     User-Agent: kubectl/v1.29.3 (linux/amd64) kubernetes/6813625
I0625 16:05:39.910457   30433 round_trippers.go:574] Response Status: 101 Switching Protocols in 19 milliseconds
/ # ls -l
total 5816
drwxr-xr-x    2 root     root          4096 Nov 24  2021 bin
-rwxr-xr-x    1 root     root       5894502 Mar  3  2022 hello-app
drwxr-xr-x    2 root     root          4096 Nov 24  2021 home
dr-xr-xr-x  183 root     root             0 Jun 25 15:53 proc
drwx------    1 root     root          4096 Jun 25 15:58 root
drwxr-xr-x    2 root     root          4096 Nov 24  2021 srv
/ # hostname
hello-world-exec
/ #
vagrant@c1-cp1:~$ 
```

### k8s-fundamentals - API Request - Logs

```console
vagrant@c1-cp1:~$ kubectl logs hello-world
2024/06/25 15:48:59 Server listening on port 8080
vagrant@c1-cp1:~$ kubectl logs hello-world -v 6
I0625 16:10:38.101914   33258 loader.go:395] Config loaded from file:  /home/vagrant/.kube/config
I0625 16:10:38.115131   33258 round_trippers.go:553] GET https://192.168.1.10:6443/api/v1/namespaces/default/pods/hello-world 200 OK in 8 milliseconds
I0625 16:10:38.121082   33258 round_trippers.go:553] GET https://192.168.1.10:6443/api/v1/namespaces/default/pods/hello-world/log?container=hello-world 200 OK in 4 milliseconds
2024/06/25 15:48:59 Server listening on port 8080
vagrant@c1-cp1:~$ kubectl proxy &
[1] 33356
vagrant@c1-cp1:~$ Starting to serve on 127.0.0.1:8001
curl http://localhost:8001/api/v1/namespaces/api/v1/namespaces/default/pods/hello-world/log?container=hello-world
2024/06/25 15:48:59 Server listening on port 8080
vagrant@c1-cp1:~$ fg ^C
```

### k8s-fundamentals - API Request - kube proxy

In the previous examples, we've been using kube proxy to provide authentication to the curl we've been executing from the c1-cp1.
We can open this up, to be accessed from outside c1-cp1.

> [!IMPORTANT]
>
> This is just for lab purposes

```console
vagrant@c1-cp1:~$ kubectl proxy -v 7 --address='0.0.0.0' --accept-hosts '^.*'
I0625 16:23:51.854477   40849 loader.go:395] Config loaded from file:  /home/vagrant/.kube/config
Starting to serve on [::]:8001
I0625 16:23:54.488075   40849 proxy_server.go:91] /api/v1/namespaces/default/pods/hello-world/log matched ^.*
I0625 16:23:54.488207   40849 proxy_server.go:91] 192.168.1.10 matched ^.*
I0625 16:23:54.488237   40849 proxy_server.go:131] Filter accepting GET /api/v1/namespaces/default/pods/hello-world/log 192.168.1.10
I0625 16:23:54.488260   40849 upgradeaware.go:310] Request was not an upgrade
I0625 16:23:54.488318   40849 round_trippers.go:463] GET https://192.168.1.10:6443/api/v1/namespaces/default/pods/hello-world/log?container=hello-world
I0625 16:23:54.488333   40849 round_trippers.go:469] Request Headers:
I0625 16:23:54.488352   40849 round_trippers.go:473]     User-Agent: curl/8.4.0
I0625 16:23:54.488370   40849 round_trippers.go:473]     Accept: */*
I0625 16:23:54.488388   40849 round_trippers.go:473]     X-Forwarded-For: 192.168.1.73
I0625 16:23:54.499025   40849 round_trippers.go:574] Response Status: 200 OK in 10 milliseconds

❯ curl 'http://192.168.1.10:8001/api/v1/namespaces/default/pods/hello-world/log?container=hello-world'
2024/06/25 15:48:59 Server listening on port 8080
```

## k8s-fundamentals - API Request - Http codes
### k8s-fundamentals - API Request - Http codes - 403 Forbiden

So simulate a 403 forbiden request, lets change the username on the `~/.kube/config` file.
Search for `- name: kubernetes-admin` and update the name to `- name: 0kubernetes-admin` for example.

```console
vagrant@c1-cp1:~$ kubectl cluster-info -v 6
I0627 11:35:10.296973  129507 loader.go:395] Config loaded from file:  /home/vagrant/.kube/config
Please enter Username: user
Please enter Password: I0627 11:36:18.924041  129507 round_trippers.go:553] GET https://192.168.1.10:6443/api?timeout=32s 403 Forbidden in 7 milliseconds
E0627 11:36:18.925000  129507 memcache.go:265] couldn't get current server API group list: unknown
I0627 11:36:18.925035  129507 cached_discovery.go:120] skipped caching discovery info due to unknown
I0627 11:36:18.929523  129507 round_trippers.go:553] GET https://192.168.1.10:6443/api?timeout=32s 403 Forbidden in 4 milliseconds
E0627 11:36:18.930018  129507 memcache.go:265] couldn't get current server API group list: unknown
I0627 11:36:18.930043  129507 cached_discovery.go:120] skipped caching discovery info due to unknown
I0627 11:36:18.930057  129507 shortcut.go:103] Error loading discovery information: unknown
I0627 11:36:18.935184  129507 round_trippers.go:553] GET https://192.168.1.10:6443/api?timeout=32s 403 Forbidden in 5 milliseconds
E0627 11:36:18.936620  129507 memcache.go:265] couldn't get current server API group list: unknown
I0627 11:36:18.936945  129507 cached_discovery.go:120] skipped caching discovery info due to unknown
I0627 11:36:18.944322  129507 round_trippers.go:553] GET https://192.168.1.10:6443/api?timeout=32s 403 Forbidden in 6 milliseconds
E0627 11:36:18.945251  129507 memcache.go:265] couldn't get current server API group list: unknown
I0627 11:36:18.945279  129507 cached_discovery.go:120] skipped caching discovery info due to unknown
I0627 11:36:18.950968  129507 round_trippers.go:553] GET https://192.168.1.10:6443/api?timeout=32s 403 Forbidden in 5 milliseconds
E0627 11:36:18.951349  129507 memcache.go:265] couldn't get current server API group list: unknown
I0627 11:36:18.951371  129507 cached_discovery.go:120] skipped caching discovery info due to unknown

To further debug and diagnose cluster problems, use 'kubectl cluster-info dump'.
I0627 11:36:18.951513  129507 helpers.go:246] server response object: [{
  "metadata": {},
  "status": "Failure",
  "message": "unknown",
  "reason": "Forbidden",
  "details": {
    "causes": [
      {
        "reason": "UnexpectedServerResponse",
        "message": "unknown"
      }
    ]
  },
  "code": 403
}]
Error from server (Forbidden): unknown
```

Don't forget to revert the change previously made to `~/.kube/config` file.

### k8s-fundamentals - API Request - Http codes - 404 Not Found

```console
vagrant@c1-cp1:~$ kubectl get pods test-pods -v 6
I0627 11:40:50.094258  132741 loader.go:395] Config loaded from file:  /home/vagrant/.kube/config
I0627 11:40:50.108827  132741 round_trippers.go:553] GET https://192.168.1.10:6443/api/v1/namespaces/default/pods/test-pods 404 Not Found in 8 milliseconds
I0627 11:40:50.109215  132741 helpers.go:246] server response object: [{
  "kind": "Status",
  "apiVersion": "v1",
  "metadata": {},
  "status": "Failure",
  "message": "pods \"test-pods\" not found",
  "reason": "NotFound",
  "details": {
    "name": "test-pods",
    "kind": "pods"
  },
  "code": 404
}]
Error from server (NotFound): pods "test-pods" not found
```

### k8s-fundamentals - API Request - Http codes - 404 Not Found and 201 Created

```console
vagrant@c1-cp1:~$ kubectl apply -f pods-manifest.yml -v 6
I0627 12:08:07.510530    6810 loader.go:395] Config loaded from file:  /home/vagrant/.kube/config
I0627 12:08:07.520178    6810 round_trippers.go:553] GET https://192.168.1.10:6443/openapi/v3?timeout=32s 200 OK in 6 milliseconds
I0627 12:08:07.535327    6810 round_trippers.go:553] GET https://192.168.1.10:6443/openapi/v3/api/v1?hash=EBC437E2734C2A5E649C8BB42D0B7D11384F5C16EBAC6C6EBE3D7DBCBE80D184507EC752D56427C4A43A49AB92306FC7B7790B2B13982382DC4525B719ABDA2F&timeout=32s 200 OK in 9 milliseconds
I0627 12:08:07.600784    6810 round_trippers.go:553] GET https://192.168.1.10:6443/api/v1/namespaces/default/pods/hello-world 404 Not Found in 4 milliseconds
I0627 12:08:07.613931    6810 round_trippers.go:553] POST https://192.168.1.10:6443/api/v1/namespaces/default/pods?fieldManager=kubectl-client-side-apply&fieldValidation=Strict 201 Created in 12 milliseconds
pod/hello-world created
I0627 12:08:07.614608    6810 apply.go:546] Running apply post-processor function
```

### k8s-fundamentals - API Request - Http codes - 200 DELETE

```console
vagrant@c1-cp1:~$ kubectl delete -f pods-manifest.yml -v 6
I0627 12:11:29.413300    8702 loader.go:395] Config loaded from file:  /home/vagrant/.kube/config
I0627 12:11:29.429895    8702 round_trippers.go:553] DELETE https://192.168.1.10:6443/api/v1/namespaces/default/pods/hello-world 200 OK in 11 milliseconds
pod "hello-world" deleted
I0627 12:11:29.434581    8702 round_trippers.go:553] GET https://192.168.1.10:6443/api/v1/namespaces/default/pods/hello-world 200 OK in 3 milliseconds
I0627 12:11:29.437888    8702 reflector.go:289] Starting reflector *unstructured.Unstructured (0s) from vendor/k8s.io/client-go/tools/watch/informerwatcher.go:146
I0627 12:11:29.437911    8702 reflector.go:325] Listing and watching *unstructured.Unstructured from vendor/k8s.io/client-go/tools/watch/informerwatcher.go:146
I0627 12:11:29.440080    8702 round_trippers.go:553] GET https://192.168.1.10:6443/api/v1/namespaces/default/pods?fieldSelector=metadata.name%3Dhello-world&limit=500&resourceVersion=0 200 OK in 1 milliseconds
I0627 12:11:29.441163    8702 reflector.go:351] Caches populated for *unstructured.Unstructured from vendor/k8s.io/client-go/tools/watch/informerwatcher.go:146
I0627 12:11:29.442827    8702 round_trippers.go:553] GET https://192.168.1.10:6443/api/v1/namespaces/default/pods?allowWatchBookmarks=true&fieldSelector=metadata.name%3Dhello-world&resourceVersion=303298&timeoutSeconds=326&watch=true 200 OK in 1 milliseconds
I0627 12:11:30.176219    8702 reflector.go:295] Stopping reflector *unstructured.Unstructured (0s) from vendor/k8s.io/client-go/tools/watch/informerwatcher.go:146
```

## k8s-fundamentals - Managing Objects: Namespaces, Labels, Annotations

### k8s-fundamentals - Managing Objects: Namesapces
#### k8s-fundamentals - Managing Objects: Namespaces management

Get a list of all the available namespaces.

```console
vagrant@c1-cp1:~$ kubectl get namespaces 
NAME              STATUS   AGE
default           Active   49d
kube-node-lease   Active   49d
kube-public       Active   49d
kube-system       Active   49d
```

Get a list of all the API resources that support namespaces and the ones that do not.

```console
vagrant@c1-cp1:~$ kubectl api-resources --namespaced=true
NAME                        SHORTNAMES   APIVERSION                     NAMESPACED   KIND
bindings                                 v1                             true         Binding
configmaps                  cm           v1                             true         ConfigMap
endpoints                   ep           v1                             true         Endpoints
events                      ev           v1                             true         Event
limitranges                 limits       v1                             true         LimitRange
persistentvolumeclaims      pvc          v1                             true         PersistentVolumeClaim
pods                        po           v1                             true         Pod
podtemplates                             v1                             true         PodTemplate
replicationcontrollers      rc           v1                             true         ReplicationController
resourcequotas              quota        v1                             true         ResourceQuota
secrets                                  v1                             true         Secret
serviceaccounts             sa           v1                             true         ServiceAccount
services                    svc          v1                             true         Service
controllerrevisions                      apps/v1                        true         ControllerRevision
daemonsets                  ds           apps/v1                        true         DaemonSet
deployments                 deploy       apps/v1                        true         Deployment
replicasets                 rs           apps/v1                        true         ReplicaSet
statefulsets                sts          apps/v1                        true         StatefulSet
localsubjectaccessreviews                authorization.k8s.io/v1        true         LocalSubjectAccessReview
horizontalpodautoscalers    hpa          autoscaling/v2                 true         HorizontalPodAutoscaler
cronjobs                    cj           batch/v1                       true         CronJob
jobs                                     batch/v1                       true         Job
leases                                   coordination.k8s.io/v1         true         Lease
networkpolicies                          crd.projectcalico.org/v1       true         NetworkPolicy
networksets                              crd.projectcalico.org/v1       true         NetworkSet
endpointslices                           discovery.k8s.io/v1            true         EndpointSlice
events                      ev           events.k8s.io/v1               true         Event
ingresses                   ing          networking.k8s.io/v1           true         Ingress
networkpolicies             netpol       networking.k8s.io/v1           true         NetworkPolicy
poddisruptionbudgets        pdb          policy/v1                      true         PodDisruptionBudget
rolebindings                             rbac.authorization.k8s.io/v1   true         RoleBinding
roles                                    rbac.authorization.k8s.io/v1   true         Role
csistoragecapacities                     storage.k8s.io/v1              true         CSIStorageCapacity
vagrant@c1-cp1:~$ kubectl api-resources --namespaced=false
NAME                              SHORTNAMES   APIVERSION                        NAMESPACED   KIND
componentstatuses                 cs           v1                                false        ComponentStatus
namespaces                        ns           v1                                false        Namespace
nodes                             no           v1                                false        Node
persistentvolumes                 pv           v1                                false        PersistentVolume
mutatingwebhookconfigurations                  admissionregistration.k8s.io/v1   false        MutatingWebhookConfiguration
validatingwebhookconfigurations                admissionregistration.k8s.io/v1   false        ValidatingWebhookConfiguration
customresourcedefinitions         crd,crds     apiextensions.k8s.io/v1           false        CustomResourceDefinition
apiservices                                    apiregistration.k8s.io/v1         false        APIService
selfsubjectreviews                             authentication.k8s.io/v1          false        SelfSubjectReview
tokenreviews                                   authentication.k8s.io/v1          false        TokenReview
selfsubjectaccessreviews                       authorization.k8s.io/v1           false        SelfSubjectAccessReview
selfsubjectrulesreviews                        authorization.k8s.io/v1           false        SelfSubjectRulesReview
subjectaccessreviews                           authorization.k8s.io/v1           false        SubjectAccessReview
certificatesigningrequests        csr          certificates.k8s.io/v1            false        CertificateSigningRequest
bgpconfigurations                              crd.projectcalico.org/v1          false        BGPConfiguration
bgpfilters                                     crd.projectcalico.org/v1          false        BGPFilter
bgppeers                                       crd.projectcalico.org/v1          false        BGPPeer
blockaffinities                                crd.projectcalico.org/v1          false        BlockAffinity
caliconodestatuses                             crd.projectcalico.org/v1          false        CalicoNodeStatus
clusterinformations                            crd.projectcalico.org/v1          false        ClusterInformation
felixconfigurations                            crd.projectcalico.org/v1          false        FelixConfiguration
globalnetworkpolicies                          crd.projectcalico.org/v1          false        GlobalNetworkPolicy
globalnetworksets                              crd.projectcalico.org/v1          false        GlobalNetworkSet
hostendpoints                                  crd.projectcalico.org/v1          false        HostEndpoint
ipamblocks                                     crd.projectcalico.org/v1          false        IPAMBlock
ipamconfigs                                    crd.projectcalico.org/v1          false        IPAMConfig
ipamhandles                                    crd.projectcalico.org/v1          false        IPAMHandle
ippools                                        crd.projectcalico.org/v1          false        IPPool
ipreservations                                 crd.projectcalico.org/v1          false        IPReservation
kubecontrollersconfigurations                  crd.projectcalico.org/v1          false        KubeControllersConfiguration
flowschemas                                    flowcontrol.apiserver.k8s.io/v1   false        FlowSchema
prioritylevelconfigurations                    flowcontrol.apiserver.k8s.io/v1   false        PriorityLevelConfiguration
ingressclasses                                 networking.k8s.io/v1              false        IngressClass
runtimeclasses                                 node.k8s.io/v1                    false        RuntimeClass
clusterrolebindings                            rbac.authorization.k8s.io/v1      false        ClusterRoleBinding
clusterroles                                   rbac.authorization.k8s.io/v1      false        ClusterRole
priorityclasses                   pc           scheduling.k8s.io/v1              false        PriorityClass
csidrivers                                     storage.k8s.io/v1                 false        CSIDriver
csinodes                                       storage.k8s.io/v1                 false        CSINode
storageclasses                    sc           storage.k8s.io/v1                 false        StorageClass
volumeattachments                              storage.k8s.io/v1                 false        VolumeAttachment
vagrant@c1-cp1:~$
```

Get additional details of namespaces.

```console
vagrant@c1-cp1:~$ kubectl describe namespaces 
Name:         default
Labels:       kubernetes.io/metadata.name=default
Annotations:  <none>
Status:       Active

No resource quota.

No LimitRange resource.


Name:         kube-node-lease
Labels:       kubernetes.io/metadata.name=kube-node-lease
Annotations:  <none>
Status:       Active

No resource quota.

No LimitRange resource.


Name:         kube-public
Labels:       kubernetes.io/metadata.name=kube-public
Annotations:  <none>
Status:       Active

No resource quota.

No LimitRange resource.


Name:         kube-system
Labels:       kubernetes.io/metadata.name=kube-system
Annotations:  <none>
Status:       Active

No resource quota.

No LimitRange resource.
vagrant@c1-cp1:~$ 
```

Get additional info just for one namespace.

```console
vagrant@c1-cp1:~$ kubectl describe namespaces kube-system
Name:         kube-system
Labels:       kubernetes.io/metadata.name=kube-system
Annotations:  <none>
Status:       Active

No resource quota.

No LimitRange resource.
```

Get all pods on the cluster and cross all namespaces.

```console
vagrant@c1-cp1:~$ kubectl get pods --all-namespaces
NAMESPACE     NAME                                      READY   STATUS    RESTARTS      AGE
kube-system   calico-kube-controllers-8d76c5f9b-8269k   1/1     Running   5 (31m ago)   49d
kube-system   calico-node-9pndl                         1/1     Running   5 (31m ago)   49d
kube-system   calico-node-j5bg6                         1/1     Running   4 (30m ago)   30d
kube-system   calico-node-p4s5x                         1/1     Running   4 (30m ago)   30d
kube-system   calico-node-p8p65                         1/1     Running   5 (31m ago)   30d
kube-system   coredns-76f75df574-4ts97                  1/1     Running   5 (31m ago)   49d
kube-system   coredns-76f75df574-mck4h                  1/1     Running   5 (31m ago)   49d
kube-system   etcd-c1-cp1                               1/1     Running   5 (31m ago)   49d
kube-system   kube-apiserver-c1-cp1                     1/1     Running   5 (31m ago)   49d
kube-system   kube-controller-manager-c1-cp1            1/1     Running   5 (31m ago)   49d
kube-system   kube-proxy-8vkgt                          1/1     Running   4 (30m ago)   49d
kube-system   kube-proxy-bpj7x                          1/1     Running   5 (31m ago)   49d
kube-system   kube-proxy-bq4fr                          1/1     Running   4 (30m ago)   49d
kube-system   kube-proxy-zfkfk                          1/1     Running   5 (31m ago)   49d
kube-system   kube-scheduler-c1-cp1                     1/1     Running   5 (31m ago)   49d
```

Get all resources on the cluster and cross all namespaces.

```console
vagrant@c1-cp1:~$ kubectl get all --all-namespaces
NAMESPACE     NAME                                          READY   STATUS    RESTARTS      AGE
kube-system   pod/calico-kube-controllers-8d76c5f9b-8269k   1/1     Running   5 (31m ago)   49d
kube-system   pod/calico-node-9pndl                         1/1     Running   5 (31m ago)   49d
kube-system   pod/calico-node-j5bg6                         1/1     Running   4 (30m ago)   30d
kube-system   pod/calico-node-p4s5x                         1/1     Running   4 (31m ago)   30d
kube-system   pod/calico-node-p8p65                         1/1     Running   5 (31m ago)   30d
kube-system   pod/coredns-76f75df574-4ts97                  1/1     Running   5 (31m ago)   49d
kube-system   pod/coredns-76f75df574-mck4h                  1/1     Running   5 (31m ago)   49d
kube-system   pod/etcd-c1-cp1                               1/1     Running   5 (31m ago)   49d
kube-system   pod/kube-apiserver-c1-cp1                     1/1     Running   5 (31m ago)   49d
kube-system   pod/kube-controller-manager-c1-cp1            1/1     Running   5 (31m ago)   49d
kube-system   pod/kube-proxy-8vkgt                          1/1     Running   4 (30m ago)   49d
kube-system   pod/kube-proxy-bpj7x                          1/1     Running   5 (31m ago)   49d
kube-system   pod/kube-proxy-bq4fr                          1/1     Running   4 (31m ago)   49d
kube-system   pod/kube-proxy-zfkfk                          1/1     Running   5 (31m ago)   49d
kube-system   pod/kube-scheduler-c1-cp1                     1/1     Running   5 (31m ago)   49d

NAMESPACE     NAME                  TYPE        CLUSTER-IP    EXTERNAL-IP   PORT(S)                  AGE
default       service/hello-world   ClusterIP   10.99.52.33   <none>        80/TCP                   30d
default       service/kubernetes    ClusterIP   10.96.0.1     <none>        443/TCP                  49d
kube-system   service/kube-dns      ClusterIP   10.96.0.10    <none>        53/UDP,53/TCP,9153/TCP   49d

NAMESPACE     NAME                         DESIRED   CURRENT   READY   UP-TO-DATE   AVAILABLE   NODE SELECTOR            AGE
kube-system   daemonset.apps/calico-node   4         4         4       4            4           kubernetes.io/os=linux   49d
kube-system   daemonset.apps/kube-proxy    4         4         4       4            4           kubernetes.io/os=linux   49d

NAMESPACE     NAME                                      READY   UP-TO-DATE   AVAILABLE   AGE
kube-system   deployment.apps/calico-kube-controllers   1/1     1            1           49d
kube-system   deployment.apps/coredns                   2/2     2            2           49d

NAMESPACE     NAME                                                DESIRED   CURRENT   READY   AGE
kube-system   replicaset.apps/calico-kube-controllers-8d76c5f9b   1         1         1       49d
kube-system   replicaset.apps/coredns-76f75df574                  2         2         2       49d
vagrant@c1-cp1:~$ 
```

Get a list of all pods running under a specific namespace.

```console
vagrant@c1-cp1:~$ kubectl get pods --namespace kube-system
NAME                                      READY   STATUS    RESTARTS      AGE
calico-kube-controllers-8d76c5f9b-8269k   1/1     Running   5 (34m ago)   49d
calico-node-9pndl                         1/1     Running   5 (34m ago)   49d
calico-node-j5bg6                         1/1     Running   4 (33m ago)   30d
calico-node-p4s5x                         1/1     Running   4 (34m ago)   30d
calico-node-p8p65                         1/1     Running   5 (34m ago)   30d
coredns-76f75df574-4ts97                  1/1     Running   5 (34m ago)   49d
coredns-76f75df574-mck4h                  1/1     Running   5 (34m ago)   49d
etcd-c1-cp1                               1/1     Running   5 (34m ago)   49d
kube-apiserver-c1-cp1                     1/1     Running   5 (34m ago)   49d
kube-controller-manager-c1-cp1            1/1     Running   5 (34m ago)   49d
kube-proxy-8vkgt                          1/1     Running   4 (33m ago)   49d
kube-proxy-bpj7x                          1/1     Running   5 (34m ago)   49d
kube-proxy-bq4fr                          1/1     Running   4 (34m ago)   49d
kube-proxy-zfkfk                          1/1     Running   5 (34m ago)   49d
kube-scheduler-c1-cp1                     1/1     Running   5 (34m ago)   49d
```

Create a namespace from the CLI.

```console
vagrant@c1-cp1:~$ kubectl create namespace space1
namespace/space1 created
vagrant@c1-cp1:~$ kubectl describe namespaces space1 
Name:         space1
Labels:       kubernetes.io/metadata.name=space1
Annotations:  <none>
Status:       Active

No resource quota.

No LimitRange resource
```

Create a namespace declarative from a definition. The definition is on the file `namespace.yml`

```yaml
apiVersion: v1
kind: Namespace
metadata:
  name: space2
spec: {}
status: {}
```

```console
vagrant@c1-cp1:~$ kubectl apply -f namespace.yml 
namespace/space2 created
vagrant@c1-cp1:~$ kubectl get namespaces space2
NAME     STATUS   AGE
space2   Active   13s
vagrant@c1-cp1:~$ kubectl describe namespace space2
Name:         space2
Labels:       kubernetes.io/metadata.name=space2
Annotations:  <none>
Status:       Active

No resource quota.

No LimitRange resource.
```

#### k8s-fundamentals - Managing Objects: Namespaces deployment

We'll see how to deploy to a namespace.
We'll be starting a deployment into the namespace `space2`
The deployment definition is available on the file `hello-world-deployment-space2.yml`

```console
apiVersion: apps/v1
kind: Deployment
metadata:
  name: hello-world
  labels:
    app: hello-world
  namespace: space2
spec:
  replicas: 4
  selector:
    matchLabels:
      app: hello-world
  template:
    metadata:
      labels:
        app: hello-world
    spec:
      containers:
      - name: hello-world
        image: gcr.io/google-samples/hello-app:1.0
        ports:
        - containerPort: 8080
```

Let's start the deployment.

```console
vagrant@c1-cp1:~$ kubectl apply -f hello-world-deployment-space2.yml
deployment.apps/hello-world created
vagrant@c1-cp1:~$ kubectl get all --namespace space2
NAME                              READY   STATUS    RESTARTS   AGE
pod/hello-world-789db8d56-p5b2v   1/1     Running   0          23s
pod/hello-world-789db8d56-qjqkh   1/1     Running   0          23s
pod/hello-world-789db8d56-v2fj9   1/1     Running   0          23s
pod/hello-world-789db8d56-xgbkb   1/1     Running   0          23s

NAME                          READY   UP-TO-DATE   AVAILABLE   AGE
deployment.apps/hello-world   4/4     4            4           23s

NAME                                    DESIRED   CURRENT   READY   AGE
replicaset.apps/hello-world-789db8d56   4         4         4       23s
```

Now let us deploy a pod from the CLI to a specific namespace.

```console
vagrant@c1-cp1:~$ kubectl run hello-world-namespace --image=gcr.io/google-samples/hello-app:1.0 --namespace space2
pod/hello-world-namespace created
vagrant@c1-cp1:~$ kubectl get pods --namespace space2
NAME                          READY   STATUS    RESTARTS   AGE
hello-world-789db8d56-p5b2v   1/1     Running   0          19h
hello-world-789db8d56-qjqkh   1/1     Running   0          19h
hello-world-789db8d56-v2fj9   1/1     Running   0          19h
hello-world-789db8d56-xgbkb   1/1     Running   0          19h
hello-world-namespace         1/1     Running   0          21s
```

#### k8s-fundamentals - Managing Objects: Namespaces operations

Delete all the pods in a namespace.
Only pods will be deleted.
Pods that belong to a deployment/replicaset will be recreated.

```console
vagrant@c1-cp1:~$ kubectl get all --namespace space2
NAME                              READY   STATUS    RESTARTS   AGE
pod/hello-world-789db8d56-p5b2v   1/1     Running   0          19h
pod/hello-world-789db8d56-qjqkh   1/1     Running   0          19h
pod/hello-world-789db8d56-v2fj9   1/1     Running   0          19h
pod/hello-world-789db8d56-xgbkb   1/1     Running   0          19h
pod/hello-world-namespace         1/1     Running   0          4m8s

NAME                          READY   UP-TO-DATE   AVAILABLE   AGE
deployment.apps/hello-world   4/4     4            4           19h

NAME                                    DESIRED   CURRENT   READY   AGE
replicaset.apps/hello-world-789db8d56   4         4         4       19h
vagrant@c1-cp1:~$ kubectl delete pods --all -n space2
pod "hello-world-789db8d56-p5b2v" deleted
pod "hello-world-789db8d56-qjqkh" deleted
pod "hello-world-789db8d56-v2fj9" deleted
pod "hello-world-789db8d56-xgbkb" deleted
pod "hello-world-namespace" deleted
vagrant@c1-cp1:~$ kubectl get pods -n space2
NAME                          READY   STATUS    RESTARTS   AGE
hello-world-789db8d56-6m7ss   1/1     Running   0          15s
hello-world-789db8d56-8jbhz   1/1     Running   0          15s
hello-world-789db8d56-jpfnw   1/1     Running   0          15s
hello-world-789db8d56-n4fzl   1/1     Running   0          15s
```

Delete all resources within a namespace.
This will remove all the resources deployed within the namespace.
Only resources running on another namespace are left untouched.

```console
vagrant@c1-cp1:~$ kubectl get namespaces
NAME              STATUS   AGE
default           Active   49d
kube-node-lease   Active   49d
kube-public       Active   49d
kube-system       Active   49d
space1            Active   19h
space2            Active   19h
vagrant@c1-cp1:~$ kubectl delete namespaces space1
namespace "space1" deleted
vagrant@c1-cp1:~$ kubectl delete namespaces space2
namespace "space2" deleted
vagrant@c1-cp1:~$ kubectl get all --all-namespaces
NAMESPACE     NAME                                          READY   STATUS    RESTARTS      AGE
kube-system   pod/calico-kube-controllers-8d76c5f9b-8269k   1/1     Running   5 (20h ago)   49d
kube-system   pod/calico-node-9pndl                         1/1     Running   5 (20h ago)   49d
kube-system   pod/calico-node-j5bg6                         1/1     Running   4 (20h ago)   30d
kube-system   pod/calico-node-p4s5x                         1/1     Running   4 (20h ago)   30d
kube-system   pod/calico-node-p8p65                         1/1     Running   5 (20h ago)   30d
kube-system   pod/coredns-76f75df574-4ts97                  1/1     Running   5 (20h ago)   49d
kube-system   pod/coredns-76f75df574-mck4h                  1/1     Running   5 (20h ago)   49d
kube-system   pod/etcd-c1-cp1                               1/1     Running   5 (20h ago)   49d
kube-system   pod/kube-apiserver-c1-cp1                     1/1     Running   5 (20h ago)   49d
kube-system   pod/kube-controller-manager-c1-cp1            1/1     Running   5 (20h ago)   49d
kube-system   pod/kube-proxy-8vkgt                          1/1     Running   4 (20h ago)   49d
kube-system   pod/kube-proxy-bpj7x                          1/1     Running   5 (20h ago)   49d
kube-system   pod/kube-proxy-bq4fr                          1/1     Running   4 (20h ago)   49d
kube-system   pod/kube-proxy-zfkfk                          1/1     Running   5 (20h ago)   49d
kube-system   pod/kube-scheduler-c1-cp1                     1/1     Running   5 (20h ago)   49d

NAMESPACE     NAME                  TYPE        CLUSTER-IP    EXTERNAL-IP   PORT(S)                  AGE
default       service/hello-world   ClusterIP   10.99.52.33   <none>        80/TCP                   30d
default       service/kubernetes    ClusterIP   10.96.0.1     <none>        443/TCP                  49d
kube-system   service/kube-dns      ClusterIP   10.96.0.10    <none>        53/UDP,53/TCP,9153/TCP   49d

NAMESPACE     NAME                         DESIRED   CURRENT   READY   UP-TO-DATE   AVAILABLE   NODE SELECTOR            AGE
kube-system   daemonset.apps/calico-node   4         4         4       4            4           kubernetes.io/os=linux   49d
kube-system   daemonset.apps/kube-proxy    4         4         4       4            4           kubernetes.io/os=linux   49d

NAMESPACE     NAME                                      READY   UP-TO-DATE   AVAILABLE   AGE
kube-system   deployment.apps/calico-kube-controllers   1/1     1            1           49d
kube-system   deployment.apps/coredns                   2/2     2            2           49d

NAMESPACE     NAME                                                DESIRED   CURRENT   READY   AGE
kube-system   replicaset.apps/calico-kube-controllers-8d76c5f9b   1         1         1       49d
kube-system   replicaset.apps/coredns-76f75df574                  2         2         2       49d
vagrant@c1-cp1:~$ 
```

### k8s-fundamentals - Managing Objects: Labels
#### k8s-fundamentals - Managing Objects: Labels - Create, Query and Edit
##### k8s-fundamentals - Managing Objects: Labels - Create

Let us create a file `pods-labels-manifest.yml` with a definition to create pods with attached labels.

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: hello-world-pod-1
  labels:
    app: HelloApp
    deployment: v1
    tier: prod
spec:
  containers:
  - name: hello-world
    image: gcr.io/google-samples/hello-app:1.0
    ports:
    - containerPort: 8080
---
apiVersion: v1
kind: Pod
metadata:
  name: hello-world-pod-2
  labels:
    app: HelloApp
    deployment: v1.1
    tier: prod
spec:
  containers:
  - name: hello-world
    image: gcr.io/google-samples/hello-app:1.0
    ports:
    - containerPort: 8080
---
apiVersion: v1
kind: Pod
metadata:
  name: hello-world-pod-3
  labels:
    app: HelloApp
    deployment: v1.1
    tier: qa
spec:
  containers:
  - name: hello-world
    image: gcr.io/google-samples/hello-app:1.0
    ports:
    - containerPort: 8080
---
apiVersion: v1
kind: Pod
metadata:
  name: hello-world-pod-4
  labels:
    app: HelloAppAdmin
    deployment: v1
    tier: prod
spec:
  containers:
  - name: hello-world
    image: gcr.io/google-samples/hello-app:1.0
    ports:
    - containerPort: 8080
---
```

We deploy the pods, and then list them, passing the flag `show-labels` so we get the label output.
Also when describing a pod, its labels are returned.

```console
vagrant@c1-cp1:~$ kubectl apply -f pods-labels-manifest.yml 
pod/hello-world-pod-1 created
pod/hello-world-pod-2 created
pod/hello-world-pod-3 created
pod/hello-world-pod-4 created
vagrant@c1-cp1:~$ kubectl get pods --show-labels 
NAME                READY   STATUS    RESTARTS   AGE   LABELS
hello-world-pod-1   1/1     Running   0          11s   app=HelloApp,deployment=v1,tier=prod
hello-world-pod-2   1/1     Running   0          11s   app=HelloApp,deployment=v1.1,tier=prod
hello-world-pod-3   1/1     Running   0          11s   app=HelloApp,deployment=v1.1,tier=qa
hello-world-pod-4   1/1     Running   0          11s   app=HelloAppAdmin,deployment=v1,tier=prod
vagrant@c1-cp1:~$ kubectl describe pod hello-world-pod-1 | head
Name:             hello-world-pod-1
Namespace:        default
Priority:         0
Service Account:  default
Node:             c1-node1/192.168.1.20
Start Time:       Mon, 08 Jul 2024 15:23:13 +0000
Labels:           app=HelloApp
                  deployment=v1
                  tier=prod
Annotations:      cni.projectcalico.org/containerID: 7de7253abe59398988c6b387ef0e54fb04791a1d2e33539a51fed6d2285fb71a
```

##### k8s-fundamentals - Managing Objects: Labels - Query

Below we'll select the pods with `tier/prod`, and `tier/qa` labels.

```console
vagrant@c1-cp1:~$ kubectl get pods --selector tier=prod
NAME                READY   STATUS    RESTARTS   AGE
hello-world-pod-1   1/1     Running   0          7m36s
hello-world-pod-2   1/1     Running   0          7m36s
hello-world-pod-4   1/1     Running   0          7m36s
vagrant@c1-cp1:~$ kubectl get pods --selector tier=qa
NAME                READY   STATUS    RESTARTS   AGE
hello-world-pod-3   1/1     Running   0          7m43s
vagrant@c1-cp1:~$ kubectl get pods -l tier=prod
NAME                READY   STATUS    RESTARTS   AGE
hello-world-pod-1   1/1     Running   0          7m58s
hello-world-pod-2   1/1     Running   0          7m58s
hello-world-pod-4   1/1     Running   0          7m58s
vagrant@c1-cp1:~$ kubectl get pods -l tier=prod --show-labels
NAME                READY   STATUS    RESTARTS   AGE    LABELS
hello-world-pod-1   1/1     Running   0          8m6s   app=HelloApp,deployment=v1,tier=prod
hello-world-pod-2   1/1     Running   0          8m6s   app=HelloApp,deployment=v1.1,tier=prod
hello-world-pod-4   1/1     Running   0          8m6s   app=HelloAppAdmin,deployment=v1,tier=prod
```

Below we'll select the pods with multiple label combinations.

```console
vagrant@c1-cp1:~$ kubectl get pods -l 'tier=prod,app=HelloApp' --show-labels 
NAME                READY   STATUS    RESTARTS   AGE   LABELS
hello-world-pod-1   1/1     Running   0          10m   app=HelloApp,deployment=v1,tier=prod
hello-world-pod-2   1/1     Running   0          10m   app=HelloApp,deployment=v1.1,tier=prod
vagrant@c1-cp1:~$ kubectl get pods -l 'tier=prod,app!=HelloApp' --show-labels
NAME                READY   STATUS    RESTARTS   AGE   LABELS
hello-world-pod-4   1/1     Running   0          11m   app=HelloAppAdmin,deployment=v1,tier=prod
vagrant@c1-cp1:~$ kubectl get pods -l 'tier in (prod,qa)'
NAME                READY   STATUS    RESTARTS   AGE
hello-world-pod-1   1/1     Running   0          11m
hello-world-pod-2   1/1     Running   0          11m
hello-world-pod-3   1/1     Running   0          11m
hello-world-pod-4   1/1     Running   0          11m
vagrant@c1-cp1:~$ kubectl get pods -l 'tier notin (prod,qa)'
No resources found in default namespace.
```

Formating the printed labels onto columns 

```console
vagrant@c1-cp1:~$ kubectl get pods -L tier
NAME                READY   STATUS    RESTARTS   AGE   TIER
hello-world-pod-1   1/1     Running   0          15m   prod
hello-world-pod-2   1/1     Running   0          15m   prod
hello-world-pod-3   1/1     Running   0          15m   qa
hello-world-pod-4   1/1     Running   0          15m   prod
vagrant@c1-cp1:~$ kubectl get pods -L tier,app
NAME                READY   STATUS    RESTARTS   AGE   TIER   APP
hello-world-pod-1   1/1     Running   0          15m   prod   HelloApp
hello-world-pod-2   1/1     Running   0          15m   prod   HelloApp
hello-world-pod-3   1/1     Running   0          15m   qa     HelloApp
hello-world-pod-4   1/1     Running   0          15m   prod   HelloAppAdmin
```

##### k8s-fundamentals - Managing Objects: Labels - Edit

Next, we'll be editing a label, adding a new one, and deleting a label.

```console
# Edit an existing label
vagrant@c1-cp1:~$ kubectl label pod hello-world-pod-1 tier=non-prod --overwrite
pod/hello-world-pod-1 labeled
vagrant@c1-cp1:~$ kubectl get pod hello-world-pod-1 --show-labels 
NAME                READY   STATUS    RESTARTS   AGE   LABELS
hello-world-pod-1   1/1     Running   0          19m   app=HelloApp,deployment=v1,tier=non-prod
# Create a new label
vagrant@c1-cp1:~$ kubectl label pod hello-world-pod-1 new=Label
pod/hello-world-pod-1 labeled
vagrant@c1-cp1:~$ kubectl get pod hello-world-pod-1 --show-labels 
NAME                READY   STATUS    RESTARTS   AGE   LABELS
hello-world-pod-1   1/1     Running   0          19m   app=HelloApp,deployment=v1,new=Label,tier=non-prod
# Delete the created label
vagrant@c1-cp1:~$ kubectl label pod hello-world-pod-1 new-
pod/hello-world-pod-1 unlabeled
vagrant@c1-cp1:~$ kubectl get pod hello-world-pod-1 --show-labels 
NAME                READY   STATUS    RESTARTS   AGE   LABELS
hello-world-pod-1   1/1     Running   0          20m   app=HelloApp,deployment=v1,tier=non-prod
```

### k8s-fundamentals - Managing Objects: Labels/Deployments

We'll create a deployment from the file `hello-world-deployment-labels.yml`

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: hello-world
  labels:
    app: hello-world
spec:
  replicas: 4
  selector:
    matchLabels:
      app: hello-world
  template:
    metadata:
      labels:
        app: hello-world
    spec:
      containers:
      - name: hello-world
        image: gcr.io/google-samples/hello-app:1.0
        ports:
        - containerPort: 8080
```

We'll also create a service from the file `hello-world-service-labels.yml`

```yaml
apiVersion: v1
kind: Service
metadata:
  name: hello-world
spec:
  ports:
  - port: 80
    protocol: TCP
    targetPort: 8080
  selector:
    app: hello-world
```

Let us create the deployment and the service.

```console
vagrant@c1-cp1:~$ kubectl apply -f hello-world-deployment-labels.yml 
deployment.apps/hello-world created
vagrant@c1-cp1:~$ kubectl get deployments.apps 
NAME          READY   UP-TO-DATE   AVAILABLE   AGE
hello-world   4/4     4            4           12s
vagrant@c1-cp1:~$ kubectl apply -f hello-world-service-labels.yml 
service/hello-world created
vagrant@c1-cp1:~$ kubectl get service
NAME          TYPE        CLUSTER-IP     EXTERNAL-IP   PORT(S)   AGE
hello-world   ClusterIP   10.96.25.234   <none>        80/TCP    6s
kubernetes    ClusterIP   10.96.0.1      <none>        443/TCP   52d
```
#### k8s-fundamentals - Managing Objects: Labels/Deployments - Labels on resources

Look into the labels and selectors on the deployment resource.

```console
vagrant@c1-cp1:~$ kubectl describe deployment hello-world 
Name:                   hello-world
Namespace:              default
CreationTimestamp:      Mon, 08 Jul 2024 16:17:47 +0000
Labels:                 app=hello-world
Annotations:            deployment.kubernetes.io/revision: 1
Selector:               app=hello-world
Replicas:               4 desired | 4 updated | 4 total | 4 available | 0 unavailable
StrategyType:           RollingUpdate
MinReadySeconds:        0
RollingUpdateStrategy:  25% max unavailable, 25% max surge
Pod Template:
  Labels:  app=hello-world
  Containers:
   hello-world:
    Image:        gcr.io/google-samples/hello-app:1.0
    Port:         8080/TCP
    Host Port:    0/TCP
    Environment:  <none>
    Mounts:       <none>
  Volumes:        <none>
Conditions:
  Type           Status  Reason
  ----           ------  ------
  Progressing    True    NewReplicaSetAvailable
  Available      True    MinimumReplicasAvailable
OldReplicaSets:  <none>
NewReplicaSet:   hello-world-789db8d56 (4/4 replicas created)
Events:          <none>
```

Look into the labels and selectors on the replicaset resource.
Check the Selector for the pod template.

```console
vagrant@c1-cp1:~$ kubectl describe replicasets hello-world
Name:           hello-world-789db8d56
Namespace:      default
Selector:       app=hello-world,pod-template-hash=789db8d56
Labels:         app=hello-world
                pod-template-hash=789db8d56
Annotations:    deployment.kubernetes.io/desired-replicas: 4
                deployment.kubernetes.io/max-replicas: 5
                deployment.kubernetes.io/revision: 1
Controlled By:  Deployment/hello-world
Replicas:       4 current / 4 desired
Pods Status:    4 Running / 0 Waiting / 0 Succeeded / 0 Failed
Pod Template:
  Labels:  app=hello-world
           pod-template-hash=789db8d56
  Containers:
   hello-world:
    Image:        gcr.io/google-samples/hello-app:1.0
    Port:         8080/TCP
    Host Port:    0/TCP
    Environment:  <none>
    Mounts:       <none>
  Volumes:        <none>
Events:           <none>
```

Get pod labels. Check the label for the app and pod-template

```console
vagrant@c1-cp1:~$ kubectl get pods --show-labels 
NAME                          READY   STATUS    RESTARTS      AGE   LABELS
hello-world-789db8d56-czhnz   1/1     Running   2 (20m ago)   63d   app=hello-world,pod-template-hash=789db8d56
hello-world-789db8d56-dz8j8   1/1     Running   2 (21m ago)   63d   app=hello-world,pod-template-hash=789db8d56
hello-world-789db8d56-tm6fn   1/1     Running   2 (21m ago)   63d   app=hello-world,pod-template-hash=789db8d56
hello-world-789db8d56-vfgjs   1/1     Running   2 (21m ago)   63d   app=hello-world,pod-template-hash=789db8d56
```

Let us update the value of pod-template-hash for one of the pods, and see how k8s reacts.

```console
vagrant@c1-cp1:~$ kubectl label pods hello-world-789db8d56-czhnz pod-template-hash=TEST --overwrite
pod/hello-world-789db8d56-czhnz labeled
```

K8s created another pod (since it thinks only 3 exist because we've relabeled)

```console
vagrant@c1-cp1:~$ kubectl get pods --show-labels
NAME                          READY   STATUS    RESTARTS      AGE   LABELS
hello-world-789db8d56-8hgl8   1/1     Running   0             3s    app=hello-world,pod-template-hash=789db8d56
hello-world-789db8d56-czhnz   1/1     Running   2 (23m ago)   63d   app=hello-world,pod-template-hash=TEST
hello-world-789db8d56-dz8j8   1/1     Running   2 (24m ago)   63d   app=hello-world,pod-template-hash=789db8d56
hello-world-789db8d56-tm6fn   1/1     Running   2 (24m ago)   63d   app=hello-world,pod-template-hash=789db8d56
hello-world-789db8d56-vfgjs   1/1     Running   2 (24m ago)   63d   app=hello-world,pod-template-hash=789db8d56
vagrant@c1-cp1:~$ kubectl describe replicasets hello-world
Name:           hello-world-789db8d56
Namespace:      default
Selector:       app=hello-world,pod-template-hash=789db8d56
Labels:         app=hello-world
                pod-template-hash=789db8d56
Annotations:    deployment.kubernetes.io/desired-replicas: 4
                deployment.kubernetes.io/max-replicas: 5
                deployment.kubernetes.io/revision: 1
Controlled By:  Deployment/hello-world
Replicas:       4 current / 4 desired
Pods Status:    4 Running / 0 Waiting / 0 Succeeded / 0 Failed
Pod Template:
  Labels:  app=hello-world
           pod-template-hash=789db8d56
  Containers:
   hello-world:
    Image:        gcr.io/google-samples/hello-app:1.0
    Port:         8080/TCP
    Host Port:    0/TCP
    Environment:  <none>
    Mounts:       <none>
  Volumes:        <none>
Events:
  Type    Reason            Age    From                   Message
  ----    ------            ----   ----                   -------
  Normal  SuccessfulCreate  2m25s  replicaset-controller  Created pod: hello-world-789db8d56-8hgl8
```

### k8s-fundamentals - Managing Objects: Labels/Services

Let's find out how Labels and Selectors are used in services.

```console
vagrant@c1-cp1:~$ kubectl get service
NAME          TYPE        CLUSTER-IP     EXTERNAL-IP   PORT(S)   AGE
hello-world   ClusterIP   10.96.25.234   <none>        80/TCP    63d
kubernetes    ClusterIP   10.96.0.1      <none>        443/TCP   115d
vagrant@c1-cp1:~$ kubectl describe service hello-world 
Name:              hello-world
Namespace:         default
Labels:            <none>
Annotations:       <none>
Selector:          app=hello-world
Type:              ClusterIP
IP Family Policy:  SingleStack
IP Families:       IPv4
IP:                10.96.25.234
IPs:               10.96.25.234
Port:              <unset>  80/TCP
TargetPort:        8080/TCP
Endpoints:         10.0.10.236:8080,10.0.10.237:8080,10.0.11.46:8080 + 2 more...
Session Affinity:  None
Events:            <none>
```

We can see that the endpoints of the service have 5 IPs instead of the desired 4.
This is because the "test pod" still has the label app==hello-world. Previously we've only changed the pod-template-hash label that only affects the replicaset.
Without changing the app label, the pod is still registered to the LB.

Let us remove the pod from the LB.

```console
vagrant@c1-cp1:~$ kubectl get pods -o wide
NAME                          READY   STATUS    RESTARTS      AGE   IP            NODE       NOMINATED NODE   READINESS GATES
hello-world-789db8d56-8hgl8   1/1     Running   0             13m   10.0.10.237   c1-node3   <none>           <none>
hello-world-789db8d56-czhnz   1/1     Running   2 (37m ago)   63d   10.0.10.236   c1-node3   <none>           <none>
hello-world-789db8d56-dz8j8   1/1     Running   2 (38m ago)   63d   10.0.15.114   c1-node1   <none>           <none>
hello-world-789db8d56-tm6fn   1/1     Running   2 (38m ago)   63d   10.0.11.46    c1-node2   <none>           <none>
hello-world-789db8d56-vfgjs   1/1     Running   2 (38m ago)   63d   10.0.15.113   c1-node1   <none>           <none>
vagrant@c1-cp1:~$ kubectl get pods --show-labels 
NAME                          READY   STATUS    RESTARTS      AGE   LABELS
hello-world-789db8d56-8hgl8   1/1     Running   0             14m   app=hello-world,pod-template-hash=789db8d56
hello-world-789db8d56-czhnz   1/1     Running   2 (38m ago)   63d   app=hello-world,pod-template-hash=TEST
hello-world-789db8d56-dz8j8   1/1     Running   2 (39m ago)   63d   app=hello-world,pod-template-hash=789db8d56
hello-world-789db8d56-tm6fn   1/1     Running   2 (38m ago)   63d   app=hello-world,pod-template-hash=789db8d56
hello-world-789db8d56-vfgjs   1/1     Running   2 (39m ago)   63d   app=hello-world,pod-template-hash=789db8d56
vagrant@c1-cp1:~$ kubectl label pod hello-world-789db8d56-czhnz app=TEST --overwrite
pod/hello-world-789db8d56-czhnz labeled
vagrant@c1-cp1:~$ kubectl describe endpoints hello-world 
Name:         hello-world
Namespace:    default
Labels:       <none>
Annotations:  <none>
Subsets:
  Addresses:          10.0.10.237,10.0.11.46,10.0.15.113,10.0.15.114
  NotReadyAddresses:  <none>
  Ports:
    Name     Port  Protocol
    ----     ----  --------
    <unset>  8080  TCP

Events:  <none>
vagrant@c1-cp1:~$ kubectl describe service hello-world 
Name:              hello-world
Namespace:         default
Labels:            <none>
Annotations:       <none>
Selector:          app=hello-world
Type:              ClusterIP
IP Family Policy:  SingleStack
IP Families:       IPv4
IP:                10.96.25.234
IPs:               10.96.25.234
Port:              <unset>  80/TCP
TargetPort:        8080/TCP
Endpoints:         10.0.10.237:8080,10.0.11.46:8080,10.0.15.113:8080 + 1 more...
Session Affinity:  None
Events:            <none>
vagrant@c1-cp1:~$
```

Time to clean up

```console
vagrant@c1-cp1:~$ kubectl delete deployments.apps hello-world 
deployment.apps "hello-world" deleted
vagrant@c1-cp1:~$ kubectl delete service hello-world 
service "hello-world" deleted
vagrant@c1-cp1:~$ kubectl get pods
NAME                          READY   STATUS    RESTARTS      AGE
hello-world-789db8d56-czhnz   1/1     Running   2 (42m ago)   63d
vagrant@c1-cp1:~$ kubectl delete pod hello-world-789db8d56-czhnz 
pod "hello-world-789db8d56-czhnz" deleted
```

### k8s-fundamentals - Managing Objects: Scheduling pod to a node

We can tag nodes and associate tags to pods so they get affinity.
1st let us check the nodes' "default" label

```console
vagrant@c1-cp1:~$ kubectl get nodes --show-labels 
NAME       STATUS   ROLES           AGE    VERSION   LABELS
c1-cp1     Ready    control-plane   115d   v1.29.3   beta.kubernetes.io/arch=amd64,beta.kubernetes.io/os=linux,kubernetes.io/arch=amd64,kubernetes.io/hostname=c1-cp1,kubernetes.io/os=linux,node-role.kubernetes.io/control-plane=,node.kubernetes.io/exclude-from-external-load-balancers=
c1-node1   Ready    <none>          115d   v1.29.3   beta.kubernetes.io/arch=amd64,beta.kubernetes.io/os=linux,kubernetes.io/arch=amd64,kubernetes.io/hostname=c1-node1,kubernetes.io/os=linux
c1-node2   Ready    <none>          115d   v1.29.3   beta.kubernetes.io/arch=amd64,beta.kubernetes.io/os=linux,kubernetes.io/arch=amd64,kubernetes.io/hostname=c1-node2,kubernetes.io/os=linux
c1-node3   Ready    <none>          115d   v1.29.3   beta.kubernetes.io/arch=amd64,beta.kubernetes.io/os=linux,kubernetes.io/arch=amd64,kubernetes.io/hostname=c1-node3,kubernetes.io/os=linux
```

Now we add some "custom" labels to the node.

```console
vagrant@c1-cp1:~$ kubectl label node c1-node1 disk=local_nvme
node/c1-node1 labeled
vagrant@c1-cp1:~$ kubectl label node c2-node1 hardware=local_gpu
Error from server (NotFound): nodes "c2-node1" not found
vagrant@c1-cp1:~$ kubectl label node c1-node2 hardware=local_gpu
node/c1-node2 labeled
vagrant@c1-cp1:~$ kubectl get nodes -L hardware,disk
NAME       STATUS   ROLES           AGE    VERSION   HARDWARE    DISK
c1-cp1     Ready    control-plane   115d   v1.29.3
c1-node1   Ready    <none>          115d   v1.29.3               local_nvme
c1-node2   Ready    <none>          115d   v1.29.3   local_gpu
c1-node3   Ready    <none>          115d   v1.29.3
```

We'll create a deployment from the file `hello-world-pods-node-labels.yml` 

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: hello-world-pod-nvme
spec:
  containers:
  - name: hello-world
    image: gcr.io/google-samples/hello-app:1.0
    ports:
    - containerPort: 80
  nodeSelector:
    disk: local_nvme
---
apiVersion: v1
kind: Pod
metadata:
  name:  hello-world-pod-gpu
spec:
  containers:
  - name: hello-world
    image: gcr.io/google-samples/hello-app:1.0
    ports:
    - containerPort: 80
  nodeSelector:
    hardware: local_gpu
---
apiVersion: v1
kind: Pod
metadata:
  name: hello-world-pod
spec:
  containers:
  - name: hello-world
    image: gcr.io/google-samples/hello-app:1.0
    ports:
    - containerPort: 80
```

```console
vagrant@c1-cp1:~$ kubectl apply -f hello-world-pods-node-labels.yml
pod/hello-world-pod-nvme created
pod/hello-world-pod-gpu created
pod/hello-world-pod created
```

Let us check that the pods were assigned to the nodes that match the node-selector and node-label.

```console
vagrant@c1-cp1:~$ kubectl get node -L disk,hardware
NAME       STATUS   ROLES           AGE    VERSION   DISK         HARDWARE
c1-cp1     Ready    control-plane   116d   v1.29.3
c1-node1   Ready    <none>          116d   v1.29.3   local_nvme
c1-node2   Ready    <none>          116d   v1.29.3                local_gpu
c1-node3   Ready    <none>          116d   v1.29.3
vagrant@c1-cp1:~$ kubectl get pods -o wide
NAME                   READY   STATUS    RESTARTS   AGE   IP            NODE       NOMINATED NODE   READINESS GATES
hello-world-pod        1/1     Running   0          74s   10.0.10.238   c1-node3   <none>           <none>
hello-world-pod-gpu    1/1     Running   0          74s   10.0.11.47    c1-node2   <none>           <none>
hello-world-pod-nvme   1/1     Running   0          74s   10.0.15.115   c1-node1   <none>           <none>
```

Clean up action

```console
vagrant@c1-cp1:~$ kubectl label node c1-node1 disk-
node/c1-node1 unlabeled
vagrant@c1-cp1:~$ kubectl label node c1-node2 hardware-
node/c1-node2 unlabeled
vagrant@c1-cp1:~$ kubectl delete pod hello-world-pod
pod "hello-world-pod" deleted
vagrant@c1-cp1:~$ kubectl delete pod hello-world-pod-nvme 
pod "hello-world-pod-nvme" deleted
vagrant@c1-cp1:~$ kubectl delete pod hello-world-pod-gpu 
pod "hello-world-pod-gpu" deleted
```

### k8s-fundamentals - Managing Objects: Annotations

Annotations add additional info to the resources.
Annotations can't be used to query or select resources.

We'll create a deployment file with annotations `hello-world-pod-annotations.yml`

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: hello-world-pod
  annotations:
    owner: asantos
    department: home
spec:
  containers:
  - name: hello-world
    image: gcr.io/google-samples/hello-app:1.0
    ports:
    - containerPort: 80
```

```console
vagrant@c1-cp1:~$ kubectl apply -f hello-world-pod-annotations.yml
pod/hello-world-pod created
```

We can check that the pod is running with the defined annotations.

```console
vagrant@c1-cp1:~$ kubectl get pods -o json | jq '.items[].metadata.annotations'
{
  "cni.projectcalico.org/containerID": "49e8d90d82328b3e3f62768cc8f36e4eace58d4e7429f8efbdbf6b10b2a432b0",
  "cni.projectcalico.org/podIP": "10.0.10.239/32",
  "cni.projectcalico.org/podIPs": "10.0.10.239/32",
  "department": "home",
  "kubectl.kubernetes.io/last-applied-configuration": "{\"apiVersion\":\"v1\",\"kind\":\"Pod\",\"metadata\":{\"annotations\":{\"department\":\"home\",\"owner\":\"asantos\"},\"name\":\"hello-world-pod\",\"namespace\":\"default\"},\"spec\":{\"containers\":[{\"image\":\"gcr.io/google-samples/hello-app:1.0\",\"name\":\"hello-world\",\"ports\":[{\"containerPort\":80}]}]}}\n",
  "owner": "asantos"
}
```

We can see that annotation with the Key owner and department are on the running pod.

Additionally, we can set the annotations via the CLI (imperatively)

```console
vagrant@c1-cp1:~$ kubectl annotate pod hello-world-pod colour=blue
pod/hello-world-pod annotated
vagrant@c1-cp1:~$ kubectl get pods -o json | jq '.items[].metadata.annotations'
{
  "cni.projectcalico.org/containerID": "49e8d90d82328b3e3f62768cc8f36e4eace58d4e7429f8efbdbf6b10b2a432b0",
  "cni.projectcalico.org/podIP": "10.0.10.239/32",
  "cni.projectcalico.org/podIPs": "10.0.10.239/32",
  "colour": "blue",
  "department": "home",
  "kubectl.kubernetes.io/last-applied-configuration": "{\"apiVersion\":\"v1\",\"kind\":\"Pod\",\"metadata\":{\"annotations\":{\"department\":\"home\",\"owner\":\"asantos\"},\"name\":\"hello-world-pod\",\"namespace\":\"default\"},\"spec\":{\"containers\":[{\"image\":\"gcr.io/google-samples/hello-app:1.0\",\"name\":\"hello-world\",\"ports\":[{\"containerPort\":80}]}]}}\n",
  "owner": "asantos"
}
```

## k8s API and Pods - Run and Manage Pods

- Sigle container pods
- Multiple container pods
- Init containers
- Static pods (managed by the kubelet)

###  k8s API and Pods - Run and Manage Pods - Bare Pods & Deployments

Let us launch some bare pods while taking a look at the k8s api events.

We'll create a manifest for bare pods `pods-bare-manifest.yml`

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: hello-world-pod
spec:
  containers:
  - name: hello-world
    image: gcr.io/google-samples/hello-app:1.0
    ports:
    - containerPort: 80
```

We'll create a manifest for a deployment for the bare pods `pods-bare-deployment-manifest.yml`


```console
vagrant@c1-cp1:~$ kubectl get events --watch &
[1] 46136
vagrant@c1-cp1:~$ LAST SEEN   TYPE     REASON    OBJECT                MESSAGE
kubectl apply -f pods-bare-manifest.yml
pod/hello-world-pod created
vagrant@c1-cp1:~$ 0s          Normal   Scheduled   pod/hello-world-pod   Successfully assigned default/hello-world-pod to c1-node1
0s          Normal   Pulled      pod/hello-world-pod   Container image "gcr.io/google-samples/hello-app:1.0" already present on machine
0s          Normal   Created     pod/hello-world-pod   Created container hello-world
0s          Normal   Started     pod/hello-world-pod   Started container hello-world
vagrant@c1-cp1:~$ kubectl apply -f pods-bare-deployment-manifest.yml
deployment.apps/hello-world created
vagrant@c1-cp1:~$ 0s          Normal    ScalingReplicaSet   deployment/hello-world              Scaled up replica set hello-world-84cf4cb885 to 1
0s          Normal    SuccessfulCreate    replicaset/hello-world-84cf4cb885   Created pod: hello-world-84cf4cb885-dxgnl
0s          Normal    Scheduled           pod/hello-world-84cf4cb885-dxgnl    Successfully assigned default/hello-world-84cf4cb885-dxgnl to c1-node3
0s          Warning   FailedMount         pod/hello-world-84cf4cb885-dxgnl    MountVolume.SetUp failed for volume "kube-api-access-vnlpv" : failed to sync configmap cache: timed out waiting for the condition
0s          Normal    Pulled              pod/hello-world-84cf4cb885-dxgnl    Container image "gcr.io/google-samples/hello-app@sha256:2b0febe1b9bd01739999853380b1a939e8102fd0dc5e2ff1fc6892c4557d52b9" already present on machine
0s          Normal    Created             pod/hello-world-84cf4cb885-dxgnl    Created container hello-world
0s          Normal    Started             pod/hello-world-84cf4cb885-dxgnl    Started container hello-world
```

Now we can scale the replicas to 2 instances.

```console
vagrant@c1-cp1:~$ kubectl scale deployment hello-world --replicas=2
deployment.apps/hello-world scaled
vagrant@c1-cp1:~$ 0s          Normal    ScalingReplicaSet   deployment/hello-world              Scaled up replica set hello-world-84cf4cb885 to 2 from 1
0s          Normal    SuccessfulCreate    replicaset/hello-world-84cf4cb885   Created pod: hello-world-84cf4cb885-p4k6g
0s          Normal    Scheduled           pod/hello-world-84cf4cb885-p4k6g    Successfully assigned default/hello-world-84cf4cb885-p4k6g to c1-node2
0s          Normal    Pulled              pod/hello-world-84cf4cb885-p4k6g    Container image "gcr.io/google-samples/hello-app@sha256:2b0febe1b9bd01739999853380b1a939e8102fd0dc5e2ff1fc6892c4557d52b9" already present on machine
0s          Normal    Created             pod/hello-world-84cf4cb885-p4k6g    Created container hello-world
0s          Normal    Started             pod/hello-world-84cf4cb885-p4k6g    Started container hello-world
```

And now we can scale in the deployment.

```console
vagrant@c1-cp1:~$ kubectl scale deployment hello-world --replicas=1
deployment.apps/hello-world scaled
vagrant@c1-cp1:~$ 0s          Normal    ScalingReplicaSet   deployment/hello-world              Scaled down replica set hello-world-84cf4cb885 to 1 from 2
0s          Normal    SuccessfulDelete    replicaset/hello-world-84cf4cb885   Deleted pod: hello-world-84cf4cb885-5sm2b
0s          Normal    Killing             pod/hello-world-84cf4cb885-5sm2b    Stopping container hello-world
```

Let's exec into the pod running in the deployment.

```console
vagrant@c1-cp1:~$ kubectl -v 6 exec -it hello-world-84cf4cb885-dxgnl -- /bin/sh
I0911 12:30:05.483494   70317 loader.go:395] Config loaded from file:  /home/vagrant/.kube/config
I0911 12:30:05.497699   70317 round_trippers.go:553] GET https://192.168.1.10:6443/api/v1/namespaces/default/pods/hello-world-84cf4cb885-dxgnl 200 OK in 8 milliseconds
I0911 12:30:05.499822   70317 podcmd.go:88] Defaulting container name to hello-world
I0911 12:30:05.519900   70317 round_trippers.go:553] POST https://192.168.1.10:6443/api/v1/namespaces/default/pods/hello-world-84cf4cb885-dxgnl/exec?command=%2Fbin%2Fsh&container=hello-world&stdin=true&stdout=true&tty=true 101 Switching Protocols in 18 milliseconds
                     / # ps
PID   USER     TIME  COMMAND
    1 root      0:00 ./hello-app
   10 root      0:00 /bin/sh
   16 root      0:00 ps
/ # exit
```

###  k8s API and Pods - Run and Manage Pods - Run pods and kubectl port forward
We can check the container process running on the node.

```console
vagrant@c1-cp1:~$ kubectl get pods -o wide
NAME                           READY   STATUS    RESTARTS   AGE     IP            NODE       NOMINATED NODE   READINESS GATES
hello-world-84cf4cb885-dxgnl   1/1     Running   0          5m55s   10.0.10.243   c1-node3   <none>           <none>
hello-world-pod                1/1     Running   0          44m     10.0.15.116   c1-node1   <none>           <none>
$ vagrant ssh c1-node3
vagrant@c1-node3:~$ ps -aux | grep hello-app
root       40163  0.0  0.1   6880  3928 ?        Ssl  12:26   0:00 ./hello-app
vagrant    43394  0.0  0.1   7008  2148 pts/0    S+   12:36   0:00 grep --color=auto hello-app
```

Let's access the service running inside the pod without creating a Service.
We'll be using port-forward.

```console
# Fails because 80 <1024 is privellidge
# We'll rerun it on another port or run it with sudo
vagrant@c1-cp1:~$ kubectl port-forward hello-world-84cf4cb885-dxgnl 80:8080
Unable to listen on port 80: Listeners failed to create with the following errors: [unable to create listener: Error listen tcp4 127.0.0.1:80: bind: permission denied unable to create listener: Error listen tcp6 [::1]:80: bind: permission denied]
error: unable to listen on any of the requested ports: [{80 8080}]
^Cvagrant@c1-cp1:~$ kubectl port-forward hello-world-84cf4cb885-dxgnl 8080:8080 &
[2] 75955
vagrant@c1-cp1:~$ Forwarding from 127.0.0.1:8080 -> 8080
Forwarding from [::1]:8080 -> 8080
curl http://localhost:8080
Handling connection for 8080
Hello, world!
Version: 2.0.0
Hostname: hello-world-84cf4cb885-dxgnl
```

Clean up stage

```console
vagrant@c1-cp1:~$ fg
kubectl port-forward hello-world-84cf4cb885-dxgnl 8080:8080
^Cvagrant@c1-cp1:~$ kubectl delete deployments.apps hello-world 
deployment.apps "hello-world" deleted
vagrant@c1-cp1:~$ 0s          Normal    Killing             pod/hello-world-84cf4cb885-dxgnl    Stopping container hello-world

vagrant@c1-cp1:~$ kubectl delete pods hello-world-pod 
pod "hello-world-pod" deleted
0s          Normal    Killing             pod/hello-world-pod                 Stopping container hello-world
vagrant@c1-cp1:~$ fg
kubectl get events --watch
```

###  k8s API and Pods - Run and Manage Pods - Static Pods

Let us create a pod manifest with the help of the dry-run parameter.

```console
vagrant@c1-cp1:~$ kubectl run hello-world --image=gcr.io/google/samples/hello-app:2.0 --dry-run=client --port=8080 -o yaml
apiVersion: v1
kind: Pod
metadata:
  creationTimestamp: null
  labels:
    run: hello-world
  name: hello-world
spec:
  containers:
  - image: gcr.io/google-samples/hello-app:2.0
    name: hello-world
    ports:
    - containerPort: 8080
    resources: {}
  dnsPolicy: ClusterFirst
  restartPolicy: Always
status: {}
```

Now let us copy the output onto `/etc/kubernetes/manifests/test-static-pod.yml` on the c1-node1 instance.
We should double-check the location of the static pod manifest.

```console
vagrant@c1-node1:~$ sudo cat /var/lib/kubelet/config.yaml | yq .staticPodPath
/etc/kubernetes/manifests
# let us create the static pod manifest
sudo bash -c 'cat <<EOF > /etc/kubernetes/manifests/test-static-pod.yml
apiVersion: v1
kind: Pod
metadata:
  creationTimestamp: null
  labels:
    run: hello-world
  name: hello-world
spec:
  containers:
  - image: gcr.io/google-samples/hello-app:2.0
    name: hello-world
    ports:
    - containerPort: 8080
    resources: {}
  dnsPolicy: ClusterFirst
  restartPolicy: Always
status: {}
EOF'
```

After the file is saved, kubelet will immediately start the pod.
Going back to `c1-cp1` and executing `kubectl get pods -o wide` will show the pods, but that is just a mirror pod showing up on kube api.
To show that, we'll get the PodId and other info from `c1-node1` with crictl, we'll delete the pod from `c1-cp1` and we can see the pod was never actually killed on the source node `c1-node1`
Just the mirror pod gets "restarted"

```console
# Pods running on c1-node1
vagrant@c1-node1:~$ sudo crictl --runtime-endpoint unix:///run/containerd/containerd.sock ps
CONTAINER           IMAGE               CREATED              STATE               NAME                ATTEMPT             POD ID              POD
21f0c9d8e5a61       f59157bf39125       About a minute ago   Running             hello-world         0                   9e3d11141a4dd       hello-world-c1-node1
aff734dc8e597       4e42b6f329bc1       10 minutes ago       Running             calico-node         11                  a9abcaa2232e4       calico-node-9pndl
de703b187d747       a1d263b5dc5b0       10 minutes ago       Running             kube-proxy          11                  05fbd01aab49e       kube-proxy-zfkfk
# Mirror pod gets deleted
vagrant@c1-cp1:~$ kubectl get pods -o wide
NAME                   READY   STATUS    RESTARTS   AGE   IP            NODE       NOMINATED NODE   READINESS GATES
hello-world-c1-node1   1/1     Running   0          44s   10.0.15.118   c1-node1   <none>           <none>
vagrant@c1-cp1:~$ kubectl delete pod hello-world-c1-node1 
pod "hello-world-c1-node1" deleted
vagrant@c1-cp1:~$ kubectl get pods -o wide
NAME                   READY   STATUS    RESTARTS   AGE   IP            NODE       NOMINATED NODE   READINESS GATES
hello-world-c1-node1   1/1     Running   0          35s   10.0.15.118   c1-node1   <none>           <none>
# The actual pod on c1-node was never deleted or replaced.
vagrant@c1-node1:~$ sudo crictl --runtime-endpoint unix:///run/containerd/containerd.sock ps
CONTAINER           IMAGE               CREATED             STATE               NAME                ATTEMPT             POD ID              POD
21f0c9d8e5a61       f59157bf39125       4 minutes ago       Running             hello-world         0                   9e3d11141a4dd       hello-world-c1-node1
aff734dc8e597       4e42b6f329bc1       13 minutes ago      Running             calico-node         11                  a9abcaa2232e4       calico-node-9pndl
de703b187d747       a1d263b5dc5b0       13 minutes ago      Running             kube-proxy          11                  05fbd01aab49e       kube-proxy-zfkfk
```

We can now delete the static pod.

```console
vagrant@c1-node1:~$ sudo rm /etc/kubernetes/manifests/test-static-pod.yml 
vagrant@c1-node1:~$ sudo crictl --runtime-endpoint unix:///run/containerd/containerd.sock ps
CONTAINER           IMAGE               CREATED             STATE               NAME                ATTEMPT             POD ID              POD
aff734dc8e597       4e42b6f329bc1       19 minutes ago      Running             calico-node         11                  a9abcaa2232e4       calico-node-9pndl
de703b187d747       a1d263b5dc5b0       20 minutes ago      Running             kube-proxy          11                  05fbd01aab49e       kube-proxy-zfkfk
vagrant@c1-cp1:~$ kubectl get pods -o wide
No resources found in default namespace.
```

###  k8s API and Pods - Run and Manage Pods - Running MultiContainer Pods - Share data

To demo a multi-container pod with a shared (ephemeral) volume we'll create a manifest with 2 pods and a volume.

We'll create a manifest for a deployment for the bare pods `multicontainer-pod-manifest.yml`

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: multicontainer-pod
spec:
  containers:
  - name: producer
    image: ubuntu
    command: ["/bin/bash"]
    args: ["-c", "while true; do echo $(hostname) $(date) >> /var/log/index.html; sleep 10; done"]
    volumeMounts:
    - name: webcontent
      mountPath: /var/log
  - name: consumer
    image: nginx
    ports:
      - containerPort: 80
    volumeMounts:
    - name: webcontent
      mountPath: /usr/share/nginx/html
  volumes:
  - name: webcontent 
    emptyDir: {}
```

```console
vagrant@c1-cp1:~$ kubectl get pods
NAME                 READY   STATUS    RESTARTS   AGE
multicontainer-pod   2/2     Running   0          30s
vagrant@c1-cp1:~$ kubectl describe pod multicontainer-pod 
Name:             multicontainer-pod
Namespace:        default
Priority:         0
Service Account:  default
Node:             c1-node3/192.168.1.22
Start Time:       Thu, 12 Sep 2024 10:48:29 +0000
Labels:           <none>
Annotations:      cni.projectcalico.org/containerID: 9fa2e37717bd48f1f8e860a218e0f5d2e0073fa5e3d573c14116d426d8b3dae4
                  cni.projectcalico.org/podIP: 10.0.10.244/32
                  cni.projectcalico.org/podIPs: 10.0.10.244/32
Status:           Running
IP:               10.0.10.244
IPs:
  IP:  10.0.10.244
Containers:
  producer:
    Container ID:  containerd://740a5e42f30d422fd3dc73ecc503eb5c0e7f9292046160717553ca173f2c6a99
    Image:         ubuntu
    Image ID:      docker.io/library/ubuntu@sha256:8a37d68f4f73ebf3d4efafbcf66379bf3728902a8038616808f04e34a9ab63ee
    Port:          <none>
    Host Port:     <none>
    Command:
      /bin/bash
    Args:
      -c
      while true; do echo $(hostname) $(date) >> /var/log/index.html; sleep 10; done
    State:          Running
      Started:      Thu, 12 Sep 2024 10:48:36 +0000
    Ready:          True
    Restart Count:  0
    Environment:    <none>
    Mounts:
      /var/log from webcontent (rw)
      /var/run/secrets/kubernetes.io/serviceaccount from kube-api-access-7hz86 (ro)
  consumer:
    Container ID:   containerd://46ad54609a3da0af8e41187777261679415584ffba24868288176fc954684b38
    Image:          nginx
    Image ID:       docker.io/library/nginx@sha256:04ba374043ccd2fc5c593885c0eacddebabd5ca375f9323666f28dfd5a9710e3
    Port:           80/TCP
    Host Port:      0/TCP
    State:          Running
      Started:      Thu, 12 Sep 2024 10:48:44 +0000
    Ready:          True
    Restart Count:  0
    Environment:    <none>
    Mounts:
      /usr/share/nginx/html from webcontent (rw)
      /var/run/secrets/kubernetes.io/serviceaccount from kube-api-access-7hz86 (ro)
Conditions:
  Type                        Status
  PodReadyToStartContainers   True
  Initialized                 True
  Ready                       True
  ContainersReady             True
  PodScheduled                True
Volumes:
  webcontent:
    Type:       EmptyDir (a temporary directory that shares a pod's lifetime)
    Medium:
    SizeLimit:  <unset>
  kube-api-access-7hz86:
    Type:                    Projected (a volume that contains injected data from multiple sources)
    TokenExpirationSeconds:  3607
    ConfigMapName:           kube-root-ca.crt
    ConfigMapOptional:       <nil>
    DownwardAPI:             true
QoS Class:                   BestEffort
Node-Selectors:              <none>
Tolerations:                 node.kubernetes.io/not-ready:NoExecute op=Exists for 300s
                             node.kubernetes.io/unreachable:NoExecute op=Exists for 300s
Events:
  Type    Reason     Age   From               Message
  ----    ------     ----  ----               -------
  Normal  Scheduled  44s   default-scheduler  Successfully assigned default/multicontainer-pod to c1-node3
  Normal  Pulling    43s   kubelet            Pulling image "ubuntu"
  Normal  Pulled     37s   kubelet            Successfully pulled image "ubuntu" in 6.441s (6.441s including waiting)
  Normal  Created    37s   kubelet            Created container producer
  Normal  Started    37s   kubelet            Started container producer
  Normal  Pulling    37s   kubelet            Pulling image "nginx"
  Normal  Pulled     29s   kubelet            Successfully pulled image "nginx" in 7.896s (7.896s including waiting)
  Normal  Created    29s   kubelet            Created container consumer
  Normal  Started    29s   kubelet            Started container consumer
```

Now we can exec into both containers and check that the file being produced with one container is available on the consumer container.

```console
vagrant@c1-cp1:~$ kubectl exec -it multicontainer-pod -- /bin/sh
Defaulted container "producer" out of: producer, consumer     
# ls -ltr /var/log
total 4
-rw-r--r-- 1 root root 864 Sep 12 10:51 index.html
# tail /var/log/index.html
multicontainer-pod Thu Sep 12 10:50:07 UTC 2024
multicontainer-pod Thu Sep 12 10:50:17 UTC 2024
multicontainer-pod Thu Sep 12 10:50:27 UTC 2024
multicontainer-pod Thu Sep 12 10:50:37 UTC 2024
multicontainer-pod Thu Sep 12 10:50:47 UTC 2024
multicontainer-pod Thu Sep 12 10:50:57 UTC 2024
multicontainer-pod Thu Sep 12 10:51:07 UTC 2024
multicontainer-pod Thu Sep 12 10:51:17 UTC 2024
multicontainer-pod Thu Sep 12 10:51:27 UTC 2024
multicontainer-pod Thu Sep 12 10:51:37 UTC 2024
#
#
vagrant@c1-cp1:~$ kubectl exec -it multicontainer-pod --container consume -- /bin/sh
vagrant@c1-cp1:~$ kubectl exec -it multicontainer-pod --container consumer -- /bin/sh
# ls -ltr /usr/share/nginx/html
total 4
-rw-r--r-- 1 root root 1200 Sep 12 10:52 index.html
# tail /usr/share/nginx/html/index.html
multicontainer-pod Thu Sep 12 10:52:27 UTC 2024
multicontainer-pod Thu Sep 12 10:52:37 UTC 2024
multicontainer-pod Thu Sep 12 10:52:47 UTC 2024
multicontainer-pod Thu Sep 12 10:52:57 UTC 2024
multicontainer-pod Thu Sep 12 10:53:07 UTC 2024
multicontainer-pod Thu Sep 12 10:53:17 UTC 2024
multicontainer-pod Thu Sep 12 10:53:27 UTC 2024
multicontainer-pod Thu Sep 12 10:53:37 UTC 2024
multicontainer-pod Thu Sep 12 10:53:47 UTC 2024
multicontainer-pod Thu Sep 12 10:53:57 UTC 2024
# ^C
#
command terminated with exit code 130
vagrant@c1-cp1:~$
```

We can  quickly connect to the consumer container via port-forwarding and check the content being served by nginx

```console
vagrant@c1-cp1:~$ Forwarding from 127.0.0.1:8080 -> 80
Forwarding from [::1]:8080 -> 80

vagrant@c1-cp1:~$ curl http://localhost:8080
Handling connection for 8080
multicontainer-pod Thu Sep 12 10:48:36 UTC 2024
multicontainer-pod Thu Sep 12 10:48:46 UTC 2024
multicontainer-pod Thu Sep 12 10:48:56 UTC 2024
multicontainer-pod Thu Sep 12 10:49:06 UTC 2024
multicontainer-pod Thu Sep 12 10:49:16 UTC 2024
multicontainer-pod Thu Sep 12 10:49:26 UTC 2024
multicontainer-pod Thu Sep 12 10:49:36 UTC 2024
multicontainer-pod Thu Sep 12 10:49:47 UTC 2024
multicontainer-pod Thu Sep 12 10:49:57 UTC 2024
multicontainer-pod Thu Sep 12 10:50:07 UTC 2024
multicontainer-pod Thu Sep 12 10:50:17 UTC 2024
multicontainer-pod Thu Sep 12 10:50:27 UTC 2024
multicontainer-pod Thu Sep 12 10:50:37 UTC 2024
multicontainer-pod Thu Sep 12 10:50:47 UTC 2024
multicontainer-pod Thu Sep 12 10:50:57 UTC 2024
multicontainer-pod Thu Sep 12 10:51:07 UTC 2024
multicontainer-pod Thu Sep 12 10:51:17 UTC 2024
multicontainer-pod Thu Sep 12 10:51:27 UTC 2024
multicontainer-pod Thu Sep 12 10:51:37 UTC 2024
multicontainer-pod Thu Sep 12 10:51:47 UTC 2024
multicontainer-pod Thu Sep 12 10:51:57 UTC 2024
multicontainer-pod Thu Sep 12 10:52:07 UTC 2024
multicontainer-pod Thu Sep 12 10:52:17 UTC 2024
multicontainer-pod Thu Sep 12 10:52:27 UTC 2024
multicontainer-pod Thu Sep 12 10:52:37 UTC 2024
multicontainer-pod Thu Sep 12 10:52:47 UTC 2024
multicontainer-pod Thu Sep 12 10:52:57 UTC 2024
multicontainer-pod Thu Sep 12 10:53:07 UTC 2024
multicontainer-pod Thu Sep 12 10:53:17 UTC 2024
multicontainer-pod Thu Sep 12 10:53:27 UTC 2024
multicontainer-pod Thu Sep 12 10:53:37 UTC 2024
multicontainer-pod Thu Sep 12 10:53:47 UTC 2024
multicontainer-pod Thu Sep 12 10:53:57 UTC 2024
multicontainer-pod Thu Sep 12 10:54:07 UTC 2024
multicontainer-pod Thu Sep 12 10:54:17 UTC 2024
multicontainer-pod Thu Sep 12 10:54:27 UTC 2024
multicontainer-pod Thu Sep 12 10:54:37 UTC 2024
multicontainer-pod Thu Sep 12 10:54:47 UTC 2024
multicontainer-pod Thu Sep 12 10:54:57 UTC 2024
multicontainer-pod Thu Sep 12 10:55:07 UTC 2024
vagrant@c1-cp1:~$ curl http://localhost:8080
Handling connection for 8080
multicontainer-pod Thu Sep 12 10:48:36 UTC 2024
multicontainer-pod Thu Sep 12 10:48:46 UTC 2024
multicontainer-pod Thu Sep 12 10:48:56 UTC 2024
multicontainer-pod Thu Sep 12 10:49:06 UTC 2024
multicontainer-pod Thu Sep 12 10:49:16 UTC 2024
multicontainer-pod Thu Sep 12 10:49:26 UTC 2024
multicontainer-pod Thu Sep 12 10:49:36 UTC 2024
multicontainer-pod Thu Sep 12 10:49:47 UTC 2024
multicontainer-pod Thu Sep 12 10:49:57 UTC 2024
multicontainer-pod Thu Sep 12 10:50:07 UTC 2024
multicontainer-pod Thu Sep 12 10:50:17 UTC 2024
multicontainer-pod Thu Sep 12 10:50:27 UTC 2024
multicontainer-pod Thu Sep 12 10:50:37 UTC 2024
multicontainer-pod Thu Sep 12 10:50:47 UTC 2024
multicontainer-pod Thu Sep 12 10:50:57 UTC 2024
multicontainer-pod Thu Sep 12 10:51:07 UTC 2024
multicontainer-pod Thu Sep 12 10:51:17 UTC 2024
multicontainer-pod Thu Sep 12 10:51:27 UTC 2024
multicontainer-pod Thu Sep 12 10:51:37 UTC 2024
multicontainer-pod Thu Sep 12 10:51:47 UTC 2024
multicontainer-pod Thu Sep 12 10:51:57 UTC 2024
multicontainer-pod Thu Sep 12 10:52:07 UTC 2024
multicontainer-pod Thu Sep 12 10:52:17 UTC 2024
multicontainer-pod Thu Sep 12 10:52:27 UTC 2024
multicontainer-pod Thu Sep 12 10:52:37 UTC 2024
multicontainer-pod Thu Sep 12 10:52:47 UTC 2024
multicontainer-pod Thu Sep 12 10:52:57 UTC 2024
multicontainer-pod Thu Sep 12 10:53:07 UTC 2024
multicontainer-pod Thu Sep 12 10:53:17 UTC 2024
multicontainer-pod Thu Sep 12 10:53:27 UTC 2024
multicontainer-pod Thu Sep 12 10:53:37 UTC 2024
multicontainer-pod Thu Sep 12 10:53:47 UTC 2024
multicontainer-pod Thu Sep 12 10:53:57 UTC 2024
multicontainer-pod Thu Sep 12 10:54:07 UTC 2024
multicontainer-pod Thu Sep 12 10:54:17 UTC 2024
multicontainer-pod Thu Sep 12 10:54:27 UTC 2024
multicontainer-pod Thu Sep 12 10:54:37 UTC 2024
multicontainer-pod Thu Sep 12 10:54:47 UTC 2024
multicontainer-pod Thu Sep 12 10:54:57 UTC 2024
multicontainer-pod Thu Sep 12 10:55:07 UTC 2024
multicontainer-pod Thu Sep 12 10:55:17 UTC 2024
```

This ephemeral volume can also be seen on the node filesystem.

We need to find the PodUid and on the host, we can check the content of the volume.

```console
# Get PodUid
vagrant@c1-cp1:~$ kubectl get pods multicontainer-pod -o jsonpath='{.metadata.uid}'
1a3697ba-9023-4317-80d5-bf9cd9ecdcb8
vagrant@c1-cp1:~$ 
# Or in custom column format
vagrant@c1-cp1:~$ kubectl get pods multicontainer-pod -o custom-columns=PodName:.metadata.name,PodUID:.metadata.uid,Node:.spec.nodeName
PodName              PodUID                                 Node
multicontainer-pod   1a3697ba-9023-4317-80d5-bf9cd9ecdcb8   c1-node3
# On node c1-node3 execute
root@c1-node3:~# cd /var/lib/kubelet/pods/1a3697ba-9023-4317-80d5-bf9cd9ecdcb8/volumes/kubernetes.io~empty-dir/webcontent
root@c1-node3:/var/lib/kubelet/pods/1a3697ba-9023-4317-80d5-bf9cd9ecdcb8/volumes/kubernetes.io~empty-dir/webcontent# ll
total 20
drwxrwxrwx 2 root root 4096 Sep 12 10:48 ./
drwxr-xr-x 3 root root 4096 Sep 12 10:48 ../
-rw-r--r-- 1 root root 8544 Sep 12 11:18 index.html
root@c1-node3:/var/lib/kubelet/pods/1a3697ba-9023-4317-80d5-bf9cd9ecdcb8/volumes/kubernetes.io~empty-dir/webcontent# tail index.html
multicontainer-pod Thu Sep 12 11:16:48 UTC 2024
multicontainer-pod Thu Sep 12 11:16:58 UTC 2024
multicontainer-pod Thu Sep 12 11:17:08 UTC 2024
multicontainer-pod Thu Sep 12 11:17:18 UTC 2024
multicontainer-pod Thu Sep 12 11:17:28 UTC 2024
multicontainer-pod Thu Sep 12 11:17:38 UTC 2024
multicontainer-pod Thu Sep 12 11:17:48 UTC 2024
multicontainer-pod Thu Sep 12 11:17:58 UTC 2024
multicontainer-pod Thu Sep 12 11:18:08 UTC 2024
multicontainer-pod Thu Sep 12 11:18:18 UTC 2024
```

###  k8s API and Pods - Run and Manage Pods - Init Containers


To demo the init container we'll create 2 init containers, that have to run successfully so the application container (nginx) is able to run.
Only if those 2 finish with success will Nginx start.

We'll create a manifest for a deployment for init containers `pods-init-containers-manifes.yml`

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: init-containers
spec:
  initContainers:
  - name: init-service
    image: ubuntu
    command: ['sh', '-c', "echo waiting for service; sleep 2"]
  - name: init-database
    image: ubuntu
    command: ['sh', '-c', "echo waiting for database; sleep 2"]
  containers:
  - name: app-container
    image: nginx
```

```console
# Print pod events with get pods and fla watch
vagrant@c1-cp1:~$ kubectl get pods --watch &
[2] 113550
vagrant@c1-cp1:~$ NAME                 READY   STATUS    RESTARTS   AGE
multicontainer-pod   2/2     Running   0          3h4m

# Apply the manifest
vagrant@c1-cp1:~$ kubectl apply -f pods-init-containers-manifest.yml 
init-containers      0/1     Pending   0          0s
pod/init-containers created
vagrant@c1-cp1:~$ init-containers      0/1     Pending   0          0s
# 0 init container running
init-containers      0/1     Init:0/2   0          0s
init-containers      0/1     Init:0/2   0          0s
init-containers      0/1     Init:0/2   0          7s
# 1 init container running
init-containers      0/1     Init:1/2   0          10s
init-containers      0/1     Init:1/2   0          12s
# Both have run, so the app pod is starting
init-containers      0/1     PodInitializing   0          14s
init-containers      1/1     Running           0          22s
fg
kubectl get pods --watch
^C
vagrant@c1-cp1:~$ kubectl describe pods init-containers 
Name:             init-containers
Namespace:        default
Priority:         0
Service Account:  default
Node:             c1-node2/192.168.1.21
Start Time:       Thu, 12 Sep 2024 12:46:20 +0000
Labels:           <none>
Annotations:      cni.projectcalico.org/containerID: 9513d39e856654d904d0f2968afa901376fb2daf16c40f03fed52a846c4327bd
                  cni.projectcalico.org/podIP: 10.0.11.51/32
                  cni.projectcalico.org/podIPs: 10.0.11.51/32
Status:           Running
IP:               10.0.11.51
IPs:
  IP:  10.0.11.51
Init Containers:
  init-service:
    Container ID:  containerd://60675af07b501421aac4819f87ce6152f4b3f9c2ca54b3c8c724a48ddb8de341
    Image:         ubuntu
    Image ID:      docker.io/library/ubuntu@sha256:8a37d68f4f73ebf3d4efafbcf66379bf3728902a8038616808f04e34a9ab63ee
    Port:          <none>
    Host Port:     <none>
    Command:
      sh
      -c
      echo waiting for service; sleep 2
    State:          Terminated
      Reason:       Completed
      Exit Code:    0
      Started:      Thu, 12 Sep 2024 12:46:27 +0000
      Finished:     Thu, 12 Sep 2024 12:46:29 +0000
    Ready:          True
    Restart Count:  0
    Environment:    <none>
    Mounts:
      /var/run/secrets/kubernetes.io/serviceaccount from kube-api-access-zcrn9 (ro)
  init-database:
    Container ID:  containerd://a1d039694020c1572df833a5e988e0bc275682cc6793eb2bad9f5eb4e704a4b9
    Image:         ubuntu
    Image ID:      docker.io/library/ubuntu@sha256:8a37d68f4f73ebf3d4efafbcf66379bf3728902a8038616808f04e34a9ab63ee
    Port:          <none>
    Host Port:     <none>
    Command:
      sh
      -c
      echo waiting for database; sleep 2
    State:          Terminated
      Reason:       Completed
      Exit Code:    0
      Started:      Thu, 12 Sep 2024 12:46:32 +0000
      Finished:     Thu, 12 Sep 2024 12:46:34 +0000
    Ready:          True
    Restart Count:  0
    Environment:    <none>
    Mounts:
      /var/run/secrets/kubernetes.io/serviceaccount from kube-api-access-zcrn9 (ro)
Containers:
  app-container:
    Container ID:   containerd://a4a2b454f3729435bc852d06e7c58f034f0a2eb1b681d6be16db2ee8e04f28f2
    Image:          nginx
    Image ID:       docker.io/library/nginx@sha256:04ba374043ccd2fc5c593885c0eacddebabd5ca375f9323666f28dfd5a9710e3
    Port:           <none>
    Host Port:      <none>
    State:          Running
      Started:      Thu, 12 Sep 2024 12:46:42 +0000
    Ready:          True
    Restart Count:  0
    Environment:    <none>
    Mounts:
      /var/run/secrets/kubernetes.io/serviceaccount from kube-api-access-zcrn9 (ro)
Conditions:
  Type                        Status
  PodReadyToStartContainers   True
  Initialized                 True
  Ready                       True
  ContainersReady             True
  PodScheduled                True
Volumes:
  kube-api-access-zcrn9:
    Type:                    Projected (a volume that contains injected data from multiple sources)
    TokenExpirationSeconds:  3607
    ConfigMapName:           kube-root-ca.crt
    ConfigMapOptional:       <nil>
    DownwardAPI:             true
QoS Class:                   BestEffort
Node-Selectors:              <none>
Tolerations:                 node.kubernetes.io/not-ready:NoExecute op=Exists for 300s
                             node.kubernetes.io/unreachable:NoExecute op=Exists for 300s
Events:
  Type    Reason     Age    From               Message
  ----    ------     ----   ----               -------
  Normal  Scheduled  5m15s  default-scheduler  Successfully assigned default/init-containers to c1-node2
  Normal  Pulling    72m    kubelet            Pulling image "ubuntu"
  Normal  Pulled     71m    kubelet            Successfully pulled image "ubuntu" in 6.522s (6.522s including waiting)
  Normal  Created    71m    kubelet            Created container init-service
  Normal  Started    71m    kubelet            Started container init-service
  Normal  Pulling    71m    kubelet            Pulling image "ubuntu"
  Normal  Created    71m    kubelet            Created container init-database
  Normal  Started    71m    kubelet            Started container init-database
  Normal  Pulled     71m    kubelet            Successfully pulled image "ubuntu" in 1.498s (1.498s including waiting)
  Normal  Pulling    71m    kubelet            Pulling image "nginx"
  Normal  Pulled     71m    kubelet            Successfully pulled image "nginx" in 7.873s (7.873s including waiting)
  Normal  Created    71m    kubelet            Created container app-container
  Normal  Started    71m    kubelet            Started container app-container
```

 Time to Cleanup

 ```console
vagrant@c1-cp1:~$ kubectl delete -f pods-init-containers-manifest.yml
pod "init-containers" deleted
 ```

###  k8s API and Pods - Run and Manage Pods - Restart Policy

To test restart policies we'll be using a simple pod manifest to start `pods-exec-manifes.yml`

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: hello-world-exec
spec:
  containers:
  - name: hello-world-exec
    image: gcr.io/google-samples/hello-app@sha256:2b0febe1b9bd01739999853380b1a939e8102fd0dc5e2ff1fc6892c4557d52b9
```

```console
vagrant@c1-cp1:~$ kubectl apply -f pods-exec-manifest.yml 
pod/hello-world-exec created
vagrant@c1-cp1:~$ 0s          Normal    Scheduled   pod/hello-world-exec   Successfully assigned default/hello-world-exec to c1-node1
0s          Normal    Pulled      pod/hello-world-exec   Container image "gcr.io/google-samples/hello-app@sha256:2b0febe1b9bd01739999853380b1a939e8102fd0dc5e2ff1fc6892c4557d52b9" already present on machine
0s          Normal    Created     pod/hello-world-exec   Created container hello-world-exec
0s          Normal    Started     pod/hello-world-exec   Started container hello-world-exec

# We'll exec into the container to find the app name running `hello-app`
kubectl exec -it pods/hello-world-exec /bin/sh
kubectl exec [POD] [COMMAND] is DEPRECATED and will be removed in a future version. Use kubectl exec [POD] -- [COMMAND] instead.
/ # ps
PID   USER     TIME  COMMAND
    1 root      0:00 ./hello-app
   10 root      0:00 /bin/sh
   16 root      0:00 ps
/ # exit

# Let us kill the app
vagrant@c1-cp1:~$ kubectl exec -it pods/hello-world-exec /usr/bin/killall hello-app
kubectl exec [POD] [COMMAND] is DEPRECATED and will be removed in a future version. Use kubectl exec [POD] -- [COMMAND] instead.
vagrant@c1-cp1:~$ 0s          Normal    Pulled      pod/hello-world-exec   Container image "gcr.io/google-samples/hello-app@sha256:2b0febe1b9bd01739999853380b1a939e8102fd0dc5e2ff1fc6892c4557d52b9" already present on machine
0s          Normal    Created     pod/hello-world-exec   Created container hello-world-exec
0s          Normal    Started     pod/hello-world-exec   Started container hello-world-exec
# Kubelet restarted the pod
# Notice the increment from 0 to 1 on the restarts
kubectl get pods
NAME                 READY   STATUS    RESTARTS      AGE
hello-world-exec     1/1     Running   1 (17s ago)   97s
multicontainer-pod   2/2     Running   0             3h52m

# Look into LastState and Reason to find out why pod was restarted.
vagrant@c1-cp1:~$ kubectl describe pods hello-world-exec 
Name:             hello-world-exec
Namespace:        default
Priority:         0
Service Account:  default
Node:             c1-node1/192.168.1.20
Start Time:       Thu, 12 Sep 2024 14:39:23 +0000
Labels:           <none>
Annotations:      cni.projectcalico.org/containerID: 95645944e4058a52e6854534b2bb399da58fca215ad48ece56b3702aff2430cb
                  cni.projectcalico.org/podIP: 10.0.15.121/32
                  cni.projectcalico.org/podIPs: 10.0.15.121/32
Status:           Running
IP:               10.0.15.121
IPs:
  IP:  10.0.15.121
Containers:
  hello-world-exec:
    Container ID:   containerd://34f5e5e8b4499e9338017c42e59e8c6e7ef52d6b286b42100009c95de19f8d89
    Image:          gcr.io/google-samples/hello-app@sha256:2b0febe1b9bd01739999853380b1a939e8102fd0dc5e2ff1fc6892c4557d52b9
    Image ID:       gcr.io/google-samples/hello-app@sha256:2b0febe1b9bd01739999853380b1a939e8102fd0dc5e2ff1fc6892c4557d52b9
    Port:           <none>
    Host Port:      <none>
    State:          Running
      Started:      Thu, 12 Sep 2024 14:40:43 +0000
    Last State:     Terminated
      Reason:       Error
      Exit Code:    2
      Started:      Thu, 12 Sep 2024 14:39:24 +0000
      Finished:     Thu, 12 Sep 2024 14:40:43 +0000
    Ready:          True
    Restart Count:  1
    Environment:    <none>
    Mounts:
      /var/run/secrets/kubernetes.io/serviceaccount from kube-api-access-qsntr (ro)
Conditions:
  Type                        Status
  PodReadyToStartContainers   True
  Initialized                 True
  Ready                       True
  ContainersReady             True
  PodScheduled                True
Volumes:
  kube-api-access-qsntr:
    Type:                    Projected (a volume that contains injected data from multiple sources)
    TokenExpirationSeconds:  3607
    ConfigMapName:           kube-root-ca.crt
    ConfigMapOptional:       <nil>
    DownwardAPI:             true
QoS Class:                   BestEffort
Node-Selectors:              <none>
Tolerations:                 node.kubernetes.io/not-ready:NoExecute op=Exists for 300s
                             node.kubernetes.io/unreachable:NoExecute op=Exists for 300s
Events:
  Type    Reason     Age                 From               Message
  ----    ------     ----                ----               -------
  Normal  Scheduled  2m6s                default-scheduler  Successfully assigned default/hello-world-exec to c1-node1
  Normal  Pulled     46s (x2 over 2m5s)  kubelet            Container image "gcr.io/google-samples/hello-app@sha256:2b0febe1b9bd01739999853380b1a939e8102fd0dc5e2ff1fc6892c4557d52b9" already present on machine
  Normal  Created    46s (x2 over 2m5s)  kubelet            Created container hello-world-exec
  Normal  Started    46s (x2 over 2m5s)  kubelet            Started container hello-world-exec
# Time to clean up.
vagrant@c1-cp1:~$ kubectl delete pods hello-world-exec 
pod "hello-world-exec" deleted
0s          Normal    Killing     pod/hello-world-exec   Stopping container hello-world-exec
vagrant@c1-cp1:~$ fg
kubectl get events --watch
^Cvagrant@c1-cp1:~$ 
```

We'll now test a not default restart policy, with `OnFailure` and `Never`

To test restart policies we'll be using pod manifest configured with restart policies `pods-exec-restart-manifest.yml`

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: hello-world-onfailure-pod
spec:
  containers:
  - name: hello-world
    image: gcr.io/google-samples/hello-app@sha256:2b0febe1b9bd01739999853380b1a939e8102fd0dc5e2ff1fc6892c4557d52b9
  restartPolicy: OnFailure
---
apiVersion: v1
kind: Pod
metadata:
  name: hello-world-never-pod
spec:
  containers:
  - name: hello-world
    image: gcr.io/google-samples/hello-app@sha256:2b0febe1b9bd01739999853380b1a939e8102fd0dc5e2ff1fc6892c4557d52b9
  restartPolicy: Never
```

We'll be creating the pods, then killing the app running inside the neer-pod, and checking the event and it was never restarted.

```console
vagrant@c1-cp1:~$ kubectl apply -f pods-exec-restart-manifest.yml
pod/hello-world-onfailure-pod created
pod/hello-world-never-pod created
vagrant@c1-cp1:~$ kubectl get pods
NAME                        READY   STATUS    RESTARTS   AGE
hello-world-never-pod       1/1     Running   0          8s
hello-world-onfailure-pod   1/1     Running   0          8s
multicontainer-pod          2/2     Running   0          4h11m
vagrant@c1-cp1:~$ kubectl exec pods/hello-world-never-pod -- /usr/bin/killall hello-app
vagrant@c1-cp1:~$ kubectl get pods
NAME                        READY   STATUS    RESTARTS   AGE
hello-world-never-pod       0/1     Error     0          78s
hello-world-onfailure-pod   1/1     Running   0          78s
multicontainer-pod          2/2     Running   0          4h13m
vagrant@c1-cp1:~$ kubectl describe pod hello-world-never-pod 
Name:             hello-world-never-pod
Namespace:        default
Priority:         0
Service Account:  default
Node:             c1-node1/192.168.1.20
Start Time:       Thu, 12 Sep 2024 15:00:18 +0000
Labels:           <none>
Annotations:      cni.projectcalico.org/containerID: 566bca92c3363ce35029a8e7f6875546cf54ae0648663d4aa9e163215ee70686
                  cni.projectcalico.org/podIP:
                  cni.projectcalico.org/podIPs:
Status:           Failed
IP:               10.0.15.122
IPs:
  IP:  10.0.15.122
Containers:
  hello-world:
    Container ID:   containerd://8dc6133f607efe70fb06c149a0e290f645cdf47a6c8e2b58230bb5f6eeee8497
    Image:          gcr.io/google-samples/hello-app@sha256:2b0febe1b9bd01739999853380b1a939e8102fd0dc5e2ff1fc6892c4557d52b9
    Image ID:       gcr.io/google-samples/hello-app@sha256:2b0febe1b9bd01739999853380b1a939e8102fd0dc5e2ff1fc6892c4557d52b9
    Port:           <none>
    Host Port:      <none>
    State:          Terminated
      Reason:       Error
      Exit Code:    2
      Started:      Thu, 12 Sep 2024 15:00:20 +0000
      Finished:     Thu, 12 Sep 2024 15:01:28 +0000
    Ready:          False
    Restart Count:  0
    Environment:    <none>
    Mounts:
      /var/run/secrets/kubernetes.io/serviceaccount from kube-api-access-vzwh2 (ro)
Conditions:
  Type                        Status
  PodReadyToStartContainers   False
  Initialized                 True
  Ready                       False
  ContainersReady             False
  PodScheduled                True
Volumes:
  kube-api-access-vzwh2:
    Type:                    Projected (a volume that contains injected data from multiple sources)
    TokenExpirationSeconds:  3607
    ConfigMapName:           kube-root-ca.crt
    ConfigMapOptional:       <nil>
    DownwardAPI:             true
QoS Class:                   BestEffort
Node-Selectors:              <none>
Tolerations:                 node.kubernetes.io/not-ready:NoExecute op=Exists for 300s
                             node.kubernetes.io/unreachable:NoExecute op=Exists for 300s
Events:
  Type     Reason       Age   From               Message
  ----     ------       ----  ----               -------
  Normal   Scheduled    93s   default-scheduler  Successfully assigned default/hello-world-never-pod to c1-node1
  Warning  FailedMount  93s   kubelet            MountVolume.SetUp failed for volume "kube-api-access-vzwh2" : failed to sync configmap cache: timed out waiting for the condition
  Normal   Pulled       92s   kubelet            Container image "gcr.io/google-samples/hello-app@sha256:2b0febe1b9bd01739999853380b1a939e8102fd0dc5e2ff1fc6892c4557d52b9" already present on machine
  Normal   Created      92s   kubelet            Created container hello-world
  Normal   Started      92s   kubelet            Started container hello-world
vagrant@c1-cp1:~$
```

We'll do the same, but for the pod with the restart policy onFailure.

```console
vagrant@c1-cp1:~$ kubectl get pods
NAME                        READY   STATUS    RESTARTS   AGE
hello-world-never-pod       0/1     Error     0          5m20s
hello-world-onfailure-pod   1/1     Running   0          5m20s
multicontainer-pod          2/2     Running   0          4h17m
vagrant@c1-cp1:~$ kubectl exec -it pods/hello-world-onfailure-pod -- /usr/bin/killall hello-app
vagrant@c1-cp1:~$ kubectl get pods
NAME                        READY   STATUS    RESTARTS      AGE
hello-world-never-pod       0/1     Error     0             6m21s
hello-world-onfailure-pod   1/1     Running   1 (13s ago)   6m21s
multicontainer-pod          2/2     Running   0             4h18m
vagrant@c1-cp1:~$ kubectl get pods
NAME                        READY   STATUS    RESTARTS      AGE
hello-world-never-pod       0/1     Error     0             6m28s
hello-world-onfailure-pod   1/1     Running   1 (20s ago)   6m28s
multicontainer-pod          2/2     Running   0             4h18m
vagrant@c1-cp1:~$ kubectl exec -it pods/hello-world-onfailure-pod -- /usr/bin/killall hello-app
command terminated with exit code 137
# We got hit by the exponential backoff since the container was previously killed
vagrant@c1-cp1:~$ kubectl get pods
NAME                        READY   STATUS    RESTARTS      AGE
hello-world-never-pod       0/1     Error     0             6m40s
hello-world-onfailure-pod   0/1     Error     1 (32s ago)   6m40s
multicontainer-pod          2/2     Running   0             4h18m
# And is up and running again
# Look at the restart counter. It has increased
vagrant@c1-cp1:~$ kubectl get pods
NAME                        READY   STATUS    RESTARTS      AGE
hello-world-never-pod       0/1     Error     0             6m58s
hello-world-onfailure-pod   1/1     Running   2 (26s ago)   6m58s
multicontainer-pod          2/2     Running   0             4h18m
vagrant@c1-cp1:~$ kubectl describe pod
poddisruptionbudgets.policy  pods                         podtemplates
vagrant@c1-cp1:~$ kubectl describe pods 
hello-world-never-pod      hello-world-onfailure-pod  multicontainer-pod
vagrant@c1-cp1:~$ kubectl describe pods hello-world-onfailure-pod 
Name:             hello-world-onfailure-pod
Namespace:        default
Priority:         0
Service Account:  default
Node:             c1-node2/192.168.1.21
Start Time:       Thu, 12 Sep 2024 15:00:18 +0000
Labels:           <none>
Annotations:      cni.projectcalico.org/containerID: 4b203c1135a3577be06561868d23326f128c0a091ec00d04c60af53750d6244e
                  cni.projectcalico.org/podIP: 10.0.11.52/32
                  cni.projectcalico.org/podIPs: 10.0.11.52/32
Status:           Running
IP:               10.0.11.52
IPs:
  IP:  10.0.11.52
Containers:
  hello-world:
    Container ID:   containerd://2f9dbbc7f845386c34806be26703192c61fe036fcbaf726987fccb71ab6fc060
    Image:          gcr.io/google-samples/hello-app@sha256:2b0febe1b9bd01739999853380b1a939e8102fd0dc5e2ff1fc6892c4557d52b9
    Image ID:       gcr.io/google-samples/hello-app@sha256:2b0febe1b9bd01739999853380b1a939e8102fd0dc5e2ff1fc6892c4557d52b9
    Port:           <none>
    Host Port:      <none>
    State:          Running
      Started:      Thu, 12 Sep 2024 15:07:03 +0000
    Last State:     Terminated
      Reason:       Error
      Exit Code:    2
      Started:      Thu, 12 Sep 2024 15:06:26 +0000
      Finished:     Thu, 12 Sep 2024 15:06:50 +0000
    Ready:          True
    Restart Count:  2
    Environment:    <none>
    Mounts:
      /var/run/secrets/kubernetes.io/serviceaccount from kube-api-access-lrxlg (ro)
Conditions:
  Type                        Status
  PodReadyToStartContainers   True
  Initialized                 True
  Ready                       True
  ContainersReady             True
  PodScheduled                True
Volumes:
  kube-api-access-lrxlg:
    Type:                    Projected (a volume that contains injected data from multiple sources)
    TokenExpirationSeconds:  3607
    ConfigMapName:           kube-root-ca.crt
    ConfigMapOptional:       <nil>
    DownwardAPI:             true
QoS Class:                   BestEffort
Node-Selectors:              <none>
Tolerations:                 node.kubernetes.io/not-ready:NoExecute op=Exists for 300s
                             node.kubernetes.io/unreachable:NoExecute op=Exists for 300s
Events:
  Type     Reason     Age                  From               Message
  ----     ------     ----                 ----               -------
  Normal   Scheduled  7m15s                default-scheduler  Successfully assigned default/hello-world-onfailure-pod to c1-node2
  Warning  BackOff    44s                  kubelet            Back-off restarting failed container hello-world in pod hello-world-onfailure-pod_default(53f0e5ae-c3a5-4356-81bb-b2a1195c42ab)
  Normal   Pulled     31s (x3 over 7m15s)  kubelet            Container image "gcr.io/google-samples/hello-app@sha256:2b0febe1b9bd01739999853380b1a939e8102fd0dc5e2ff1fc6892c4557d52b9" already present on machine
  Normal   Created    31s (x3 over 7m15s)  kubelet            Created container hello-world
  Normal   Started    31s (x3 over 7m15s)  kubelet            Started container hello-world
```

Time to clean up.

```console
vagrant@c1-cp1:~$ kubectl delete -f pods-exec-restart-manifest.yml 
pod "hello-world-onfailure-pod" deleted
pod "hello-world-never-pod" deleted
vagrant@c1-cp1:~$ kubectl get pods
NAME                 READY   STATUS    RESTARTS   AGE
multicontainer-pod   2/2     Running   0          4h21m
vagrant@c1-cp1:~$ kubectl delete pods multicontainer-pod 
pod "multicontainer-pod" deleted
```

###  k8s API and Pods - Run and Manage Pods - Liveliness/Readiness Probes

We'll be using a deployment manifest configured with liveliness and readiness probes. `deployment-live-ready-probes-manifest.yml`

The manifest has the probes configured to the wrong service port.

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: hello-world
spec:
  replicas: 1
  selector:
    matchLabels:
      app: hello-world
  template:
    metadata:
      labels:
        app: hello-world
    spec:
      containers:
      - name: hello-world
        image: gcr.io/google-samples/hello-app:2.0
        ports:
        - containerPort: 8080
        livenessProbe:
          tcpSocket:
            port: 8081
          initialDelaySeconds: 10
          periodSeconds: 5
        readinessProbe:
          httpGet:
            path: /
            port: 8081
          initialDelaySeconds: 10
          periodSeconds: 5
```

```console
vagrant@c1-cp1:~$ kubectl get events --watch &
vagrant@c1-cp1:~$ kubectl apply -f deployment-live-ready-probes-manifest.yml 
deployment.apps/hello-world created
vagrant@c1-cp1:~$ 0s          Normal    ScalingReplicaSet         deployment/hello-world   Scaled up replica set hello-world-78b47bf76c to 1
0s          Normal    SuccessfulCreate          replicaset/hello-world-78b47bf76c   Created pod: hello-world-78b47bf76c-927q7
0s          Normal    Scheduled                 pod/hello-world-78b47bf76c-927q7    Successfully assigned default/hello-world-78b47bf76c-927q7 to c1-node2
0s          Normal    Pulling                   pod/hello-world-78b47bf76c-927q7    Pulling image "gcr.io/google-samples/hello-app:2.0"
0s          Normal    Pulled                    pod/hello-world-78b47bf76c-927q7    Successfully pulled image "gcr.io/google-samples/hello-app:2.0" in 5.893s (5.893s including waiting)
0s          Normal    Created                   pod/hello-world-78b47bf76c-927q7    Created container hello-world
0s          Normal    Started                   pod/hello-world-78b47bf76c-927q7    Started container hello-world
0s          Warning   Unhealthy                 pod/hello-world-78b47bf76c-927q7    Liveness probe failed: dial tcp 10.0.11.53:8081: connect: connection refused
0s          Warning   Unhealthy                 pod/hello-world-78b47bf76c-927q7    Readiness probe failed: Get "http://10.0.11.53:8081/": dial tcp 10.0.11.53:8081: connect: connection refused
0s          Warning   Unhealthy                 pod/hello-world-78b47bf76c-927q7    Liveness probe failed: dial tcp 10.0.11.53:8081: connect: connection refused
0s          Warning   Unhealthy                 pod/hello-world-78b47bf76c-927q7    Readiness probe failed: Get "http://10.0.11.53:8081/": dial tcp 10.0.11.53:8081: connect: connection refused
vagrant@c1-cp1:~$ kubectl get pods
NAME                           READY   STATUS             RESTARTS      AGE
hello-world-78b47bf76c-927q7   0/1     CrashLoopBackOff   4 (15s ago)   2m6s
```

```console
# Check liveliness/readiness probes
vagrant@c1-cp1:~$ kubectl describe pods
Name:             hello-world-78b47bf76c-927q7
Namespace:        default
Priority:         0
Service Account:  default
Node:             c1-node2/192.168.1.21
Start Time:       Tue, 17 Sep 2024 13:39:31 +0000
Labels:           app=hello-world
                  pod-template-hash=78b47bf76c
Annotations:      cni.projectcalico.org/containerID: c7e521f0b5526b08353f064c93ad815c2f6abd925c31725690db9b13b04478c9
                  cni.projectcalico.org/podIP: 10.0.11.53/32
                  cni.projectcalico.org/podIPs: 10.0.11.53/32
Status:           Running
IP:               10.0.11.53
IPs:
  IP:           10.0.11.53
Controlled By:  ReplicaSet/hello-world-78b47bf76c
Containers:
  hello-world:
    Container ID:   containerd://bad2341014bd91faecacf846c8ce831a231de3341628bb4865e16a38ee48d88f
    Image:          gcr.io/google-samples/hello-app:2.0
    Image ID:       gcr.io/google-samples/hello-app@sha256:bdf36508b89fc6d272880b5764eb5e2ce6d9408e020156a601c35b9c1164f7b9
    Port:           8080/TCP
    Host Port:      0/TCP
    State:          Waiting
      Reason:       CrashLoopBackOff
    Last State:     Terminated
      Reason:       Error
      Exit Code:    2
      Started:      Tue, 17 Sep 2024 13:47:09 +0000
      Finished:     Tue, 17 Sep 2024 13:47:32 +0000
    Ready:          False
    Restart Count:  7
    Liveness:       tcp-socket :8081 delay=10s timeout=1s period=5s #success=1 #failure=3
    Readiness:      http-get http://:8081/ delay=10s timeout=1s period=5s #success=1 #failure=3
    Environment:    <none>
    Mounts:
      /var/run/secrets/kubernetes.io/serviceaccount from kube-api-access-b85d7 (ro)
Conditions:
  Type                        Status
  PodReadyToStartContainers   True
  Initialized                 True
  Ready                       False
  ContainersReady             False
  PodScheduled                True
Volumes:
  kube-api-access-b85d7:
    Type:                    Projected (a volume that contains injected data from multiple sources)
    TokenExpirationSeconds:  3607
    ConfigMapName:           kube-root-ca.crt
    ConfigMapOptional:       <nil>
    DownwardAPI:             true
QoS Class:                   BestEffort
Node-Selectors:              <none>
Tolerations:                 node.kubernetes.io/not-ready:NoExecute op=Exists for 300s
                             node.kubernetes.io/unreachable:NoExecute op=Exists for 300s
Events:
  Type     Reason     Age                   From               Message
  ----     ------     ----                  ----               -------
  Normal   Scheduled  10m                   default-scheduler  Successfully assigned default/hello-world-78b47bf76c-927q7 to c1-node2
  Normal   Pulling    10m                   kubelet            Pulling image "gcr.io/google-samples/hello-app:2.0"
  Normal   Pulled     10m                   kubelet            Successfully pulled image "gcr.io/google-samples/hello-app:2.0" in 5.893s (5.893s including waiting)
  Normal   Started    10m (x2 over 10m)     kubelet            Started container hello-world
  Normal   Created    9m47s (x3 over 10m)   kubelet            Created container hello-world
  Warning  Unhealthy  9m47s (x6 over 10m)   kubelet            Liveness probe failed: dial tcp 10.0.11.53:8081: connect: connection refused
  Warning  Unhealthy  9m47s (x8 over 10m)   kubelet            Readiness probe failed: Get "http://10.0.11.53:8081/": dial tcp 10.0.11.53:8081: connect: connection refused
  Normal   Killing    9m47s (x2 over 10m)   kubelet            Container hello-world failed liveness probe, will be restarted
  Normal   Pulled     9m47s (x2 over 10m)   kubelet            Container image "gcr.io/google-samples/hello-app:2.0" already present on machine
  Warning  BackOff    29s (x39 over 8m47s)  kubelet            Back-off restarting failed container hello-world in pod hello-world-78b47bf76c-927q7_default(4991051b-6141-4fb5-bd53-042609ef860
```

Now we can fix the probe port from 8081 to 8080.
The previous mistake was to show the liveliness and readiness probes failing.

```console
vagrant@c1-cp1:~$ kubectl apply -f deployment-live-ready-probes-manifest.yml
deployment.apps/hello-world configured
vagrant@c1-cp1:~$ kubectl get pods
NAME                           READY   STATUS              RESTARTS        AGE
hello-world-6f8996f7fc-7mpg2   0/1     ContainerCreating   0               7s
hello-world-78b47bf76c-927q7   0/1     CrashLoopBackOff    7 (4m10s ago)   12m
vagrant@c1-cp1:~$ kubectl get pods
NAME                           READY   STATUS    RESTARTS   AGE
hello-world-6f8996f7fc-7mpg2   1/1     Running   0          37s
```

Clean up time

```console
vagrant@c1-cp1:~$ kubectl delete -f deployment-live-ready-probes-manifest.yml 
deployment.apps "hello-world" deleted
vagrant@c1-cp1:~$ kubectl get pods
No resources found in default namespace.
```

###  k8s API and Pods - Run and Manage Pods - Startup Probes

We'll be using a deployment manifest configured with a startup probe. `deployment-startup-probe-manifest.yml`

The manifest has the probes startup/readiness and liveliness probes.
The startup probe is configured to a wrong service port.

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: hello-world
spec:
  replicas: 1
  selector:
    matchLabels:
      app: hello-world
  template:
    metadata:
      labels:
        app: hello-world
    spec:
      containers:
      - name: hello-world
        image: gcr.io/google-samples/hello-app:2.0
        ports:
        - containerPort: 8080
        startupProbe:
          tcpSocket:
            port: 8081
          initialDelaySeconds: 10
          periodSeconds: 5
          failureThreshold: 1
        livenessProbe:
          tcpSocket:
            port: 8080
          initialDelaySeconds: 10
          periodSeconds: 5
        readinessProbe:
          httpGet:
            path: /
            port: 8080
          initialDelaySeconds: 10
          periodSeconds: 5
```

We can see the container is killed because the startup probe has failed.

```console
vagrant@c1-cp1:~$ kubectl apply -f deployment-startup-probe-manifest.yml
deployment.apps/hello-world created
vagrant@c1-cp1:~$ 0s          Normal    ScalingReplicaSet         deployment/hello-world              Scaled up replica set hello-world-86d46467f5 to 1
0s          Normal    SuccessfulCreate          replicaset/hello-world-86d46467f5   Created pod: hello-world-86d46467f5-xwfqd
0s          Normal    Scheduled                 pod/hello-world-86d46467f5-xwfqd    Successfully assigned default/hello-world-86d46467f5-xwfqd to c1-node3
0s          Normal    Pulled                    pod/hello-world-86d46467f5-xwfqd    Container image "gcr.io/google-samples/hello-app:2.0" already present on machine
0s          Normal    Created                   pod/hello-world-86d46467f5-xwfqd    Created container hello-world
0s          Normal    Started                   pod/hello-world-86d46467f5-xwfqd    Started container hello-world
0s          Warning   Unhealthy                 pod/hello-world-86d46467f5-xwfqd    Startup probe failed: dial tcp 10.0.10.246:8081: connect: connection refused
0s          Normal    Killing                   pod/hello-world-86d46467f5-xwfqd    Container hello-world failed startup probe, will be restarted
0s          Normal    Pulled                    pod/hello-world-86d46467f5-xwfqd    Container image "gcr.io/google-samples/hello-app:2.0" already present on machine
0s          Normal    Created                   pod/hello-world-86d46467f5-xwfqd    Created container hello-world
0s          Normal    Started                   pod/hello-world-86d46467f5-xwfqd    Started container hello-world
0s          Warning   Unhealthy                 pod/hello-world-86d46467f5-xwfqd    Startup probe failed: dial tcp 10.0.10.246:8081: connect: connection refused
0s          Normal    Killing                   pod/hello-world-86d46467f5-xwfqd    Container hello-world failed startup probe, will be restarted
0s          Normal    Pulled                    pod/hello-world-86d46467f5-xwfqd    Container image "gcr.io/google-samples/hello-app:2.0" already present on machine
0s          Normal    Created                   pod/hello-world-86d46467f5-xwfqd    Created container hello-world
0s          Normal    Started                   pod/hello-world-86d46467f5-xwfqd    Started container hello-world
```

We can see the container restarts and the crashloop due to the miss configured startup  probe.
```console
vagrant@c1-cp1:~$ kubectl get pods
NAME                           READY   STATUS             RESTARTS      AGE
hello-world-86d46467f5-xwfqd   0/1     CrashLoopBackOff   5 (32s ago)   2m27s
```

Now we can fix the startup probe config using another file (just to keep track) `deployment-startup-probe-manifest-fix.yml`

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: hello-world
spec:
  replicas: 1
  selector:
    matchLabels:
      app: hello-world
  template:
    metadata:
      labels:
        app: hello-world
    spec:
      containers:
      - name: hello-world
        image: gcr.io/google-samples/hello-app:2.0
        ports:
        - containerPort: 8080
        startupProbe:
          tcpSocket:
            port: 8080
          initialDelaySeconds: 10
          periodSeconds: 5
          failureThreshold: 1
        livenessProbe:
          tcpSocket:
            port: 8080
          initialDelaySeconds: 10
          periodSeconds: 5
        readinessProbe:
          httpGet:
            path: /
            port: 8080
          initialDelaySeconds: 10
          periodSeconds: 5
```

We can see, that after the fix to the startup probe, the old pod gets deleted, and the new one gets created and starts to run.

```console
vagrant@c1-cp1:~$ kubectl apply -f deployment-startup-probe-manifest-fix.yml
deployment.apps/hello-world configured
vagrant@c1-cp1:~$ kubectl get pods
NAME                           READY   STATUS             RESTARTS      AGE
hello-world-869447c6cd-4qw4s   0/1     Running            0             5s
hello-world-86d46467f5-xwfqd   0/1     CrashLoopBackOff   7 (12s ago)   6m52s
vagrant@c1-cp1:~$ kubectl get pods
NAME                           READY   STATUS    RESTARTS   AGE
hello-world-869447c6cd-4qw4s   1/1     Running   0          48s
```

Time to do some cleanup

```console
vagrant@c1-cp1:~$ kubectl delete deployments.apps hello-world 
deployment.apps "hello-world" deleted
```