K8s consists of two server node types that make up a cluster.
`Control Plane node(s)`
- Control plane nodes contain components that manage the cluster and control tasks like deployment, scheduling and self-healing of containerized workloads.
`Worker nodes`
- The worker nodes are where applications run in the cluster.
  ![volume](/Images/volume.png)

___
Kurbenetes Architecture
-
Control Plane nodes host the following services:
1. Kube-apiserver - All components interact with the api--server and this is where users access the cluster
2. etcd-  A DB that holds the state of the cluster.
3. kube-scheduler -  schedules worker nodes based on the properties required and available eg...cpu, memory etc..
4. kube-controller-manager- Contains different non-terminating control loops that manage cluster state. eg. one of these control loops, can make sure that a desired number of your application is available all the time.
5. cloud-controller-manager(optional) - Can be used to interact with the API of cloud providers to create external resources like load balancers, storage or security groups. 

Components of worker nodes
-
1. Container runtime - The container runtime is responsible for running the containers on the worker node.
2. kubelet -A small agent that works on every worker node in the cluster. The Kubelet talks with the api-server and the container run-time to handle the final stage of starting containers.
3. kube-pro - network prox that handles inside and outside communication of your cluster. Instead of managing traffic flow of its own, the kube-proxy tries to rely on the networking capabilities of the underlying operating system if possible.

**N/B** -  This design makes it possible that applications that are already started on a worker node will continue to run even if the control plane is not available, even though most functionality e.g scaling, scheduling new applications etc, will not be possible while the control plane is offline. 

K8S alos has a concept of `namespaces` which are not to be confused with kernel namespaces that are used to isolate containers.
A k8s namespace can be used to divide a cluster into multiple` virtual clusters`, which can be used for multi-tenancy when multiple teams share cluster. Please not that K8S namespace are not suitable for strong isolation and should be viewd like a directory on a comp where you organize your objects and manager which user has access to which folder.
____

K8S API
-
without the API communication with the cluster is not possible, every user, component needs the api-server.
![K8S_CLUSTER](/Images/k8s_cluster.png)

Befor a request is processed by k8s it goes through : 
1.` Authentication`- The requester needs to present a means of identity to authenticate against the API. Commonly done with a digital signed certificate (X.509) or with an external identity management system. Kubernetes users are always externally managed. Service Accounts can be used to authenticate technical users.
2.` Authorization`- It is decided what the requester is allowed to do. In Kubernetes this can be done with Role Based Access Control (RBAC).
3. `Admission Control` - in the last step, admission controllers can be used to modify or validate the request. For example, if a user tries to use a container image from an untrustworthy registry, an admission controller could block this request. Tools like the Open Policy Agent can be used to manage admission control externally.

LIke other API's the k8s api is implemented as RESTful interface that is exposed over HTTPS. 
Through the API, a user or service can create , modify, delete, or retrieve resources that reside in  k8s.

___
Running Containers in K8S
-
In k8s instead of starting containers directly, you define a pod as the smallest copute unit and k8s transalates that into a runnng container.
Several components areinvloved to run a container in a node.

Container Runtimes-
-
1. Containerd - is lightweight and perfomant implementation to run containers. Arguably the most popular container runtime right now.
2. CRI-O :- 
3. Docker

The idea of containerd and CRI-O was very simple: provide a runtime that only contains the absolutely essentials to run containers. Nevertheless, they have additional features, like the ability to integrate with container runtime sandboxing tools. These tools try to solve the security problem that comes with sharing the kernel between multiple containers. The most common tools at the moment are:

`gvisor`
- Made by Google, provides an application kernel that sits between the containerized process and the host kernel.
  
`Kata Containers`
- A secure runtime that provides a lightweight virtual machine, but behaves like a container.