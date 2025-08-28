- nodes are physical virtual machines
- a group of nodes form a cluster..
- master node is also called the control plane
- the k8s services controller are found in the control plane. i.e master components
 you do not run the application containers in the master node

- etcd is a key value data store where the state of the cluster  is stored.
-  the ApiServer is the only component that communicates with etcd
- The apiserver exposes the RestAPi Interface
   - saves the state in the etcd
   - all clients interact with it, never directly to the datastore

`etcd` - acts as thr cluster datastore for storing state

`Cloud control-manager` 
- Interact with the cloud providers controlers.
   - Node
       - For checking the cloud provider to determine if a node has been deleted in the cloud after it stops responding.
   - Route 
       - For setting up routes in the underlying cloud infrastructure
    - Service
        - For creating, updating and deleting cloud provider load balancers
    - Volume
         - For creating, attaching and mounting volumes and interacting with the cloud provider to ochestrate volumes

`Add-Ons`
   - DNS
   - Web UI(dashboard)
   - Cluster-level logging
   - Container resource monitoring