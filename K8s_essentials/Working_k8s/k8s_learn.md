The most important object in K8S is a Pod.
A pod describes a uit of one or more containers that share an isolation layer of namespaces and cgroups.
It is the smallest deployable unit in K8S which also means that K8S is not interacting with containers directly.
___
Pad Lifecycle
Pods follow a predefined lifecycle. 
1. Pending: the pod has been accepted by the k8s cluster. possibly one or more containers has not been setup yet, this includes time a Pod spends waiting to eb scheduled and time spent downloading containers over the network.
2. Running: the Pod has been bound to a node, all containers are created. Atleast one container is running, or in the process of starting or restarting.
3. Succeed: all containers in the Pod have ended successfully and will not be restarted. 
4. Failed: all containers have terminated and atleast one container has Failed. i.e the container exited with non-zero status or was termintated by the system.
5. Unknown : The state of the pod could not be obtained. It occurs due to error in commuicating with the node where the pod should be running.


___
WorkLoad Objects 
-
Working with pods only is not sufficient in a container orchestration platform  because if a pod is lots because the node failed, the pod is gone forever.
To make sure that a number of pod copies runs all the time, we can use contriller objects that will manage the pod for us.


- `ReplicaSet`: This is a controller object that ensures a number of pods is running at any time. ReplicaSet can be suded to scale out applications and improve their availablity. They do this by starting multiple copies of a pod definition.
-` Deployment `: The most feature rich object in K8S, A deployment cab be used to describe the complete application lifecycle. They do this by managing multiple ReplicaSets that get updated when the application is changed by providing a new container image, eg... deployments are perfect to run stateless application in K8S.
-` StatefulSet`: Considered a bad practise for a long time, StatefulSets can be used to run stateful applications like databases on K8S. Stateful applications have special requirements that don't fit the ephemeral nature of pods and containers. In contrast to deployments StatefulSets try to retain IP adresses of pods and give them a stable name, persistent storage and more graceful handling of scaling and updates.
-` DaemonSet`: Ensures that a copy of a pod runs on all/some nodes of your cluster. DaemonSets are perefect to run infrastucture-related workload eg monitoring, logging tools.
`- Job`: creates on/more pods that execute a task and terminate afterwards. Job objects are perfect to run one-shot scripts  like DB migrations or Admin-tasks.
`- CronJob` : Add a time-based configuration to jobs. This allows running jobs periodically, eg doing a backup job every night at 4am.

____
Networking Objects
-
Alot of pods woul require manual networking , we get to use service and ingress objects to define and abstract networking.
Services can be used to expose a set of pods as a network service. 

- ClusterIp: its the most common service type. A ClusterIp is a virtual Ip insde K8S that can be used as a single endpoint for a set of pods. This service type can be used as a round-robin load balancer.::Pod X sends traffic to ClusterIp.. and ClusterIp distributes the traffic to backend Pods.
  ![Kurbenetes cluster](/Images/k8s_cluster.png)

- NodePort: The nodePort service type extends the ClusterIp by adding simple routing rules. It opens a port(default btn 30000 - 32767) on every node in the cluster and maps it to the clusterIp. This Service type allows routing external traffic to the cluster.
- LoadBalancer: The loadBalancer sevicetype extends the nodePort by deploying an external LoadBalancer Instance. This will work if you're in an environment that has API to configure a LoadBalancer Instance like GCP, AWS, AZURE or even openstack.
- ExternalName: A special service type that has no routing whatsoever. ExternalName is using the K8S internal DNS server to create a DNS alias. You can use this to create a simple alias to resolve rather complicated hostname like my-cool-database-az1-uid123.cloud-provider-i-like.com. This is especially usefule if you want to reach external sources from your K8S cluster.
- Headless Services: Sometimes you don't need LoadBalancing and a single service IP.  In this case, you can create what are termed " headlessServices" by explicitly specifying" None" for the cluster IP (" .spec.clusterIp")...
You can use headless service to interface with other service discovery mechanisms without being tied to K8S implementation.
For headlessService, a cluster IP is not allocated, kube-proxy does not handle these services, and there is no load balancing or proxy done by the platform for them. How DNS is automatically configured depends on whether the service has selectors defined with or without selectors.
Example. A statefulSet controller can use the Headless Service to control the domain of its pods, where sstable network id is the need and not loadbalancing.
___
If one needs even more flexibility to expose applications, you can use Ingress object. Ingress provides a means to expose HTTP and HTTPS routes from outside the cluster for a service within the cluster.
It does this by configuring routing rules that a user can set and implement with an ingress controller.
![ingress](/Images/ingress.png)

Standard feature of ingress controllers may include:

- LoadBalancing
- TLS offloading/termination
- Name-based virtual hosting
- Parh-based routing
A lot of ingress controllers provide more features like:

- Redirects
- Custom errors
- Authentication
- Season affinity
- Monitoring
- Logging
- Weighted routing
- Rate limiting

K8S also provides a cluster internal firewall with the NetworPolicy concept. 
NetworkPolicies are a simple IP firewall(OSI Layer 3 or 4) that can control traffic based on rules.
You can define rules for incoming(ingress) and outgoing traffic(egress).
A typical  use case for NetworkPolicies would be restricitng the traffic between two different namespaces.
___
Volume & Storage Objects
-
Containers were not designed with persistent storage in mind, expecially when that storage spans across multiple nodes.
K8S introduces some solutions, but still not all complexities of managing storage with containers is removed.
Containers had the concept of mounting volumes, but K8S as well made volumes part of a pod.
eg of a hostpath volume mount
```
apiVersion: v1
kind: pod
metadata:
   name: test-pd
spec :
   containers:
     - image: k8s.gcr.io/test-webserver
       name : test-container
       volumeMounts :
     - mountPath : test/pd
       name: test-volume
volumes:
  - name: test-volume
    hostPath :
       #directory location on host
       path : /data
       # this field is optional
        type" directory
```
![ volume ](/Images/volume.png)

Volumes allow sharinf data within multiple pods within the same cluster and also between multiple containers within the same pod.
This provides great flexibility when you want to use a sidecar Pattern.
They prevent data loss when a pod crashes and is restarted on the same node. 
Pods are started in a clean slate and all data is lost unless written to a volume.
A cluster environemnt with multiple servers require even more flexibility when it comes to persistent storage.
Depending on Env we can use cloud block storage like : AMAZON EBS,Google persistent DIsks,Azure Disk Storage or consume from storage systems like Ceph, GlusterFS or more traditional systems like NFS.
For more uniformality K8S uses Container Storage INterface(CSI) which allows storage vendor to write a plugin(storage driver) that can be used in K8S.
To use this abstraction, two more objects can be used:

- PersistentVolumes(PV) : An abstraction description for a slice of storage. The object configuration holds information like type of Volume, volume size, access mode and unique identifiers and information how to mount it.
- PersistentVolumeClaims(PVC): A request for storage by a user. If the cluster has multiple persistent volumes, the user can create a PVC which will reserve a persistent volume according to the user's needs.
```
apiVersion : v1
kind: PersistentVolume
metadata:
   name: test-pv
spec:
   capacity:
      storage: 50Gi
   volumeMode: Filesystem
   accessModes:
      - ReadWriteOnce
    csi:
       driver: ebs.csi.aws.com
       volumeHandle: vol-05786ec95869g8
---
apiVersion: v1
kind: PersistentVolumeClaim
metadata:
  name: ebs-claim
spec:
  accessModes:
    - ReadWriteOnce
  resources:
    requests:
      storage: 50Gi
---
apiVersion: v1
kind: Pod
metadata:
  name: app
spec:
  containers:
    - name: app
      image: centos
      command: ["/bin/sh"]
      args:
        ["-c", "while true; do echo $(date -u) >> /data/out.txt; sleep 5; done"]
      volumeMounts:
        - name: persistent-storage
          mountPath: /data
  volumes:
    - name: persistent-storage
      persistentVolumeClaim:
        claimName: ebs-claim
```
The example shows a PersistentVolume that uses an AWS EBS volume implemented with a CSI driver. After the PersistentVolume is provisioned, a developer can reserve it with a PersistentVolumeClaim. The last step is using the PVC as a volume in a Pod, just like the hostPath example we saw before.

___
It is possible to operate storage clusters directly in Kubernetes. Projects like Rook provide cloud-native storage orchestration and integrate with battle tested storage solutions like Ceph.
![rook architecture](/Images/rook_arch.png)
____
Configuring Objects
-
The twelve factor app recommends storing configuration in the environment. But what does that mean exactly? Running an application requires more than the application code and some libraries. Applications have config files, connect to other services, databases, storage systems or caches and that requires configuration like connection strings.

It is considered bad practice to incorporate the configuration directly into the container build. Any configuration change would require the entire image to be rebuilt and the entire container or pod to be redeployed. This problem gets only worse when multiple environments (development, staging, production) are used and images are being built for each and every environment. The twelve factor app explains this problem in more detail: Dev/prod parity.

In Kubernetes, this problem is solved by decoupling the configuration from the Pods with a ConfigMap. ConfigMaps can be used to store whole configuration files or variables as key-value pairs. There are two possible ways to use a ConfigMap:

Mount a ConfigMap as a volume in Pod
Map variables from a ConfigMap to environment variables of a Pod.

Here is an example of a ConfigMap that contains a nginx configuration:
```
apiVersion: v1
kind: ConfigMap
metadata:
  name: nginx-conf
data:
  nginx.conf: |
    user nginx;
    worker_processes 3;
    error_log /var/log/nginx/error.log;
...
      server {
          listen     80;
          server_name _;
          location / {
              root   html;
              index  index.html index.htm; } } }


```
Once the ConfigMap is created you can use it in a Pod:
```
apiVersion: v1
kind: Pod
metadata:
  name: nginx
spec:
  containers:
  - name: nginx
    image: nginx:1.19
    ports:
    - containerPort: 80
    volumeMounts:
    - mountPath: /etc/nginx
      name: nginx-conf
  volumes:
  - name: nginx-conf
    configMap:
      name: nginx-conf
```
Right from the beginning Kubernetes also provided an object to store sensitive information like passwords, keys or other credentials. These objects are called Secrets. Secrets are very much related to ConfigMaps and basically their only difference is that secrets are base64 encoded.

There is an on-going debate about the risk of using Secrets, since their - in contrast to their name - not considered secure.

In cloud-native environments purpose-built secret management tools have emerged that integrate very well with Kubernetes. One example would be HashiCorp Vault.
___
AutoScaling Objects
To scale the workloads in K8S we an use three different AutoScaling mechanisms.

- Horizontal Pod Autoscaler(HPA): Horizontal Pod Autoscaler (HPA) is the most used autoscaler in Kubernetes. The HPA can watch Deployments or ReplicaSets and increase the number of Replicas if a certain threshold is reached. Imaging your Pod can use 500MiB of memory and you configured a threshold of 80%. If the usage is over 400MiB (80%), a second Pod will get scheduled. Now you have a capacity of 1000MiB. If 800MiB is used, a third Pod will get scheduled and so on.
- Cluster AutoScaler: There's no point of starting more replicas of Pods, if the cluster capacity is fixed. The ClusterAutoScaler canadd new worker nodes to the cluster if the demand increases.
The cluster AutoScaler works great in tandem with the Horizontal AutoScaler.
- Vertical Pod AutoSaler: It allows pods to increase the resource requests and limits dynamically. Remember vertical scaling is limited by the node capacity.

Unfortunately, (horizontal) autoscaling in Kubernetes is NOT available out of the box and requires installing an add-on called metrics-server.

It is possible though to replace the metrics-server with Prometheus Adapter for Kubernetes Metrics APIs. The prometheus-adapter allows you to use custom metrics in Kubernetes and scale up or down based on things like requests or number of users on your system.

Rather than relying solely on metrics, projects like KEDA can be used to scale the Kubernetes workload based on events triggered by external systems. KEDA stands for Kubernetes-based Event Driven Autoscaler and was started in 2019 as a partnership between Microsoft and Red Hat. Similar to the HPA, KEDA can scale deployments, ReplicaSets, pods, etc., but also other objects such as Kubernetes jobs. With a large selection of out-of-the-box scalers, KEDA can scale to special triggers such as a database query or even the number of pods in a Kubernetes cluster.
___
Scheduling Objects
-
The scheduler is the control process which assigns Pods to Nodes.
The scheduler detrmines which nodes are valid  placements for each pod in the scheduling queue according to contraints and available resources.
The schedulers then ranks each valid node and binds the Pod to a suitable Node.
Multiple different schedulers may be used within a cluster; kube-scheduler is the default implementation.
The default scheduler does a good job of scheduling the pods across the nodes in the cluster, however there are scenarios where you want to restrict the pod on particular nodes or prefer to run on particular nodes.
There are several ways of doing this, the recomended way is to make use of label selectors to facilitate the selection.

- nodeSelector field matching aganist node labels: nodeSelector is the simplest recomended form of node selection constraint. You can add the nodeSelector field to your Pod specification and specify the node labels you want the largest node to have.
K8S only schedules the pod onto nodes that have each of the labels you specify.
- Affinity and anti-affinity: Affinity and anti-affinity expands the types of constraints you can define and give you more control over the selection logic. You can indicate that a rule is soft or preferred, so that the scheduler still schedules the pod even if it can't find a matching node.
- nodeName field : nodeName is a more direct form of node selection than affinity or nodeSelector. nodeName is a field in the Pod spec. If the nodeName fiels is not empty, the scheduler ignores the Pod and kubelet on the named node tries to place the pod on that node. Using nodeName overrules using nodeSelector or affinity and anti-affinity rules.
- Pod topology spread contraints : You can use topology spread constraints to control how Pods are spread across your cluster among failure-domains such as regions zones, nodes or among any other topology domains that you define . You might do this to improve perfomance, expected availability, or overall utilization.
___
Taints and Tolerations
-

Node affinity is a property of Pods that attracts them to a set of nodes (either as a preference or a hard requirement). Taints are the opposite -- they allow a node to repel a set of pods. 

Tolerations are applied to pods. Tolerations allow the scheduler to schedule pods with matching taints. Tolerations allow scheduling, but don't guarantee scheduling: the scheduler also evaluates other parameters as part of its function. 

Taints and tolerations work together to ensure that pods are not scheduled onto inappropriate nodes. One or more taints are applied to a node; this marks that the node should not accept any pods that do not tolerate the taints.

A taint consists of a key, value, and effect. As an argument here, it is expressed as` key=value:effect.`

For example:

`kubectl taint node worker region=useast2:NoSchedule`

The key must begin with a letter or number, and may contain letters, numbers, hyphens, dots, and underscores, up to 253 characters.

The value is optional. If given, it must begin with a letter or number, and may contain letters, numbers, hyphens, dots, and underscores, up to 63 characters.

The effect must be NoSchedule, PreferNoSchedule or NoExecute and Currently taint can only apply to nodes.

Toleration for a pod is specified in the PodSpec. A toleration "matches" a taint if the keys are the same and the effects are the same, and thus a pod with toleration would be able to schedule onto nodes.

For example:

```tolerations:
- key: "region"
  operator: "Equal"
  value: "useast2"
  effect: "NoSchedule"
```