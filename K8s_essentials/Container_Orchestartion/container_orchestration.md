A docker Image is a lightweight standalone, executable package of software that includes everything needed to run an application:code, runtime, system tools, system libraries and settings.
The 4c's of Cloud Native Security is CODE, CONTAINER, CLUSTER, AND CLOUD/Co-Lo, Corporate DataCenter.

If you have to manage and deploy large amounts of containers, Problems to be solved can include:
- Providing compute resources like virtual machines where containers will run on.
- Schedule containers to servers in an efficient way
- Allocate resources like cpu and memory to containers
- Manage the availability of containers and replace them if they fail
- scale containers if load increase
- Provide networking to connect containers together
- Provision strorage if containers need to persist data


Container Orchestration systems provide a way to build a cluster of multiple servers and host the containers on top
Container Ochestration  Systems have 
`**Control Plane**`: that is responsible for the management of the containers
`worker nodes`: that actually host the containers.
____
Networking
--
Microservice architecture depends heavily on network communication.
Network namespaces allow each container to have its own unique ip adress,, therefore multiple applications can open the same network port..eg.. multiple containerized web-servers that all open port 8080..
to make the application accessible from outside the system, containers have the abilitu to map a port from the container to a port from the host system.
To allow communication between containers across a host, er can use an overlay network that puts them in a virtual network that is spanned across the host systems.
![Screenshot from 2025-07-19 16-56-43.png](:/3819635974874c39b7d2a6c7dc433657)

____

Service Discovery & DNS
-
All the information about the containers and servers are placed in the service registry.
How best to communicate or even locate a service is through service Discovery channel which includes:
1. DNS- Modern DNS servers that have a service API can be used to register a new services as they are createdd. This approach is pretty straightforward, as most organizations already have DNS servers with the appropriate capabiities.
2. Key-Value-Store- Using a strongly consistent datastore especially to store information about servies.
___
Service Mesh
-
Use a proxy to manage network traffic.
PROXY- this is a server application that sits in between a client and server and can modify or filter network traffic before it reaches the server.  eg. NGINX, HAPROXY, ENVOY.
![Screenshot from 2025-07-19 17-39-56.png](:/70b8239914104fd8a2f3e38b134859db)

When a service mesh is used, applications don’t talk to each other directly, but the traffic is routed through the proxies instead. 
The most popular service meshes at the moment are `istio` and `linkerd.`
While they have differences in implementation, the architecture is the same.
The proxies in  service mesh form the data plane, where the networking rules are implemented and shape the traffic flow.


Microservices are lightweight applications written in various modern programming languages, with specific dependencies, libraries and environmental requirements. To ensure that an application has everything it needs to run successfully it is packaged together with its dependencies.

Containers encapsulate microservices and their dependencies but do not run them directly. Containers run container images.

A container image bundles the application along with its runtime, libraries, and dependencies, and it represents the source of a container deployed to offer an isolated executable environment for the application. Containers can be deployed from a specific image on many platforms, such as workstations, Virtual Machines, public cloud, etc.


## What Is Container Orchestration?
In Development (Dev) environments, running containers on a single host for development and testing of applications may be a suitable option. However, when migrating to Quality Assurance (QA) and Production (Prod) environments, that is no longer a viable option because the applications and services need to meet specific requirements:

- Fault-tolerance
- On-demand scalability
- Optimal resource usage
- Auto-discovery to automatically discover and communicate with each other
- Accessibility from the outside world
- Seamless updates/rollbacks without any downtime.

*Container orchestrators are tools which group systems together to form clusters where containers' deployment and management is automated at scale while meeting the requirements mentioned above. The clustered systems confer the advantages of distributed systems, such as increased performance, cost efficiency, reliability, workload distribution, and reduced latency.*

---
## Container Orchestrators

With enterprises containerizing their applications and moving them to the cloud, there is a growing demand for container orchestration solutions. While there are many solutions available, some are mere re-distributions of well-established container orchestration tools, enriched with features and, sometimes, with certain limitations in flexibility.

Although not exhaustive, the list below provides a few different container orchestration tools and services available today:

- Amazon Elastic Container Service
Amazon Elastic Container Service (ECS) is a hosted service provided by Amazon Web Services (AWS) to run containers at scale on its infrastructure.
- Azure Container Instances
Azure Container Instance (ACI) is a basic container orchestration service provided by Microsoft Azure.
- Azure Service Fabric
Azure Service Fabric is an open source container orchestrator provided by Microsoft Azure.
- Kubernetes
Kubernetes is an open source orchestration tool, originally started by Google, today part of the Cloud Native Computing Foundation (CNCF) project.
- Nomad
Nomad is the container and workload orchestrator provided by HashiCorp.
- Docker Swarm
Docker Swarm is a container orchestrator provided by Docker, Inc. It is part of Docker Engine.

## Why Use Container Orchestrators?

Although we can manually maintain a couple of containers or write scripts to manage the lifecycle of dozens of containers, orchestrators make things much easier for users especially when it comes to managing hundreds or thousands of containers running on a global infrastructure.

Most container orchestrators can:

- Group hosts together while creating a cluster, in order to leverage the benefits of distributed systems.
- Schedule containers to run on hosts in the cluster based on resources availability.
- Enable containers in a cluster to communicate with each other regardless of the host they are deployed to in the cluster.
- Bind containers and storage resources.
- Group sets of similar containers and bind them to load-balancing constructs to simplify access to containerized applications by creating an interface, a level of abstraction between the containers and the client.
- Manage and optimize resource usage.
- Allow for implementation of policies to secure access to applications running inside containers.

## Where to Deploy Container Orchestrators?

Most container orchestrators can be deployed on the infrastructure of our choice - on bare metal, Virtual Machines, on-premises, on public and hybrid clouds. Kubernetes, for example, can be deployed on a workstation, with or without an isolation layer such as a local hypervisor or container runtime, inside a company's data center, in the cloud on AWS Elastic Compute Cloud (EC2) instances, Google Compute Engine (GCE) VMs, DigitalOcean Droplets, IBM Virtual Servers, OpenStack, etc.

*In addition, there are turnkey cloud solutions which allow production Kubernetes clusters to be installed, with only a few commands, on top of cloud Infrastructures-as-a-Service. These solutions paved the way for the managed container orchestration as-a-Service, more specifically the managed Kubernetes as-a-Service (KaaS) solution, offered and hosted by the major cloud providers. Examples of KaaS solutions are Amazon Elastic Kubernetes Service (Amazon EKS), Azure Kubernetes Service (AKS), DigitalOcean Kubernetes, Google Kubernetes Engine (GKE), IBM Cloud Kubernetes Service, Oracle Container Engine for Kubernetes, or VMware Tanzu Kubernetes Grid.*