- Atomic unit of the smallest unit of work  of k8s
- Enapsulates an application's container
- Represents a unit of deployment
- Pods can run one or multiple containers
- Containers within a pod share
  - Ip address space, mounted volumes
- Containers within a pod can communicate with each other using localhost, IPC
- Pods are ephemeral
- Deploying a pod is an atomic operation, it succeeds or not
- If a pod fails, it is replaced with a new one with a shiny new IP address
- You don't update a pod, you replace it with an updates version
- You scale by adding more pods, not more containers in a pod

#### POD LIFECYCLE
![Pod Creation](/Images/PodCreation.png)


![Pod deletion](/Images/podddeletion.png)

#### Pod state
  - Pending
      - Accepted but not yet created
  - Running
      - Bound to a node
  - Succeeded
      - Exited with a status 0
  - Failed
     - All containers exit and atleast one exited with a none-zero status
   - Uknow
      - Communication issues with the pod
   - CrashLoopBackOff
       - Started, crashed, started again, and then crashed again.

![pod cheat sheet](/Images/podcheatsheet.png)