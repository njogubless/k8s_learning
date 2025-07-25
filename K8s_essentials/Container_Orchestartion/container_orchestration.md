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
