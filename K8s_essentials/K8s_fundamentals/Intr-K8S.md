## What is Kubernetes??
Kubernetes is an opensource system for automating deployment, scaling and management of containerized applications.

Kubernetes comes from the Greek word **κυβερνήτης,** which means helmsman or ship pilot. With this analogy in mind, we can think of Kubernetes as the pilot on a ship of containers.

Kubernetes is also referred to as **k8s **(pronounced Kate's), as there are 8 characters between k and s.

Kubernetes is highly inspired by the Google Borg system, a container and workload orchestrator for its global operations, Google has been using for more than a decade. It is an open source project written in the Go language and licensed under the License, Version 2.0.

Kubernetes was started by Google and, with its v1.0 release in July 2015, Google donated it to the Cloud Native Computing Foundation (CNCF), one of the largest sub-foundations of the Linux Foundation.

New Kubernetes versions are released in 4 month cycles. The current stable version is 1.29 (as of December 2023).

## From Borg to Kubernetes
According to the abstract of Google's Borg paper, published in 2015,

"Google's Borg system is a cluster manager that runs hundreds of thousands of jobs, from many thousands of different applications, across a number of clusters each with up to tens of thousands of machines".

For more than a decade, Borg has been Google's secret, running its worldwide containerized workloads in production. Services we use from Google, such as Gmail, Drive, Maps, Docs, etc., are all serviced using Borg.

Among the initial authors of Kubernetes were Google employees who have used Borg and developed it in the past. They poured in their valuable knowledge and experience while designing Kubernetes. Several features/objects of Kubernetes that can be traced back to Borg, or to lessons learned from it, are:

- API servers
- Pods
- IP-per-Pod
- Services
- Labels.

## Kubernetes Features
Kubernetes offers a very rich set of features for container orchestration. Some of its fully supported features are:

- Automatic bin packing
Kubernetes automatically schedules containers based on resource needs and constraints, to maximize utilization without sacrificing availability.
- Designed for extensibility
A Kubernetes cluster can be extended with new custom features without modifying the upstream source code.-
- Self-healing
Kubernetes automatically replaces and reschedules containers from failed nodes. It terminates and then restarts containers that become unresponsive to health checks, based on existing rules/policy. It also prevents traffic from being routed to unresponsive containers.
- Horizontal scaling
Kubernetes scales applications manually or automatically based on CPU or custom metrics utilization.
- Service discovery and load balancing
Containers receive IP addresses from Kubernetes, while it assigns a single Domain Name System (DNS) name to a set of containers to aid in load-balancing requests across the containers of the set.

Additional fully supported Kubernetes features are:

- Automated rollouts and rollbacks
Kubernetes seamlessly rolls out and rolls back application updates and configuration changes, constantly monitoring the application's health to prevent any downtime.
- Secret and configuration management
Kubernetes manages sensitive data and configuration details for an application separately from the container image, in order to avoid a rebuild of the respective image. Secrets consist of sensitive/confidential information passed to the application without revealing the sensitive content to the stack configuration, like on GitHub.
- Storage orchestration
Kubernetes automatically mounts software-defined storage (SDS) solutions to containers from local storage, external cloud providers, distributed storage, or network storage systems.
- Batch execution
Kubernetes supports batch execution, long-running jobs, and replaces failed containers.
- IPv4/IPv6 dual-stack
Kubernetes supports both IPv4 and IPv6 addresses.

*Kubernetes supports common Platform as a Service specific features such as application deployment, scaling, and load balancing, but allows users to integrate their desired monitoring, logging and alerting solutions through optional plugins.*


## Cloud Native Computing Foundation (CNCF)
The Cloud Native Computing Foundation (CNCF) is one of the largest sub-projects hosted by the Linux Foundation. CNCF aims to accelerate the adoption of containers, microservices, and cloud native applications.

CNCF hosts a multitude of projects, with more to be added in the future. CNCF provides resources to each of the projects, but, at the same time, each project continues to operate independently under its pre-existing governance structure and with its existing maintainers. Projects within CNCF are categorized based on their maturity levels: Sandbox, Incubating, and Graduated. At the time of this writing, over a dozen projects had reached Graduated status with many more Incubating and in the Sandbox.

Popular graduated projects (as of March 2024):

- Kubernetes container orchestrator
- Argo workflow engine for Kubernetes
- etcd distributed key-value store
- CoreDNS DNS server
- containerd container runtime
- CRI-O container runtime
- Envoy cloud native proxy
- Fluentd for unified logging
- Flux continuous delivery for Kubernetes
- Harbor registry
- Helm package management for Kubernetes
- Linkerd service mesh for Kubernetes
- Open Policy Agent policy engine
- Prometheus monitoring system and time series DB
- Rook cloud native storage orchestrator for Kubernetes

Key incubating projects:

- Buildpacks.io builds application images
- Contour ingress controller for Kubernetes
- gRPC for remote procedure call (RPC)
- CNI for Linux containers networking
- Knative serverless containers in Kubernetes
- KubeVirt Kubernetes based Virtual Machine manager
- Notary for data security
And many more.

There are many dynamic projects in the CNCF Sandbox geared towards metrics, monitoring, identity, scripting, serverless, nodeless, edge, expecting to achieve Incubating and possibly Graduated status. While many active projects are preparing for takeoff, others are being archived once they become less active and no longer in demand. The first projects to be archived are the rkt container runtime, the distributed OpenTracing, Brigade event driven automation tool, and Service Mesh Interface.

The projects under CNCF cover the entire lifecycle of a cloud native application, from its execution using container runtimes, to its monitoring and logging. This is very important to meet the goals of CNCF.