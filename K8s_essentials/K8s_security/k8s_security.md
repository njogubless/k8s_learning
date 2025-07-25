Particularly in a distributed system like Kubernetes, security is a broad and complicated subject. It takes a constant effort to keep a cloud system secure. We must consider more than simply Kubernetes and consider the hardware, software, and configuration options for the complete environment as more and more apps migrate to the cloud. Hardware, firmware, and operating system binaries must be secured starting in the design phase itself.

Once the platform is hardened, the kube-apiserver has a list of considerations, tools, and settings to limit access and formalize access in an easy to understand manner.

Because Kubernetes is a network-intensive environment, it is crucial to secure the network using typical firewall techniques from outside the Kubernetes cluster and using pod-to-pod encryption, a NetworkPolicy and other measures from within the Kubernetes cluster.

Minimizing base images, insisting on container immutability, and static and runtime analysis of tools is also an important part of security which often begins with developers and is implemented in the CI/CD pipeline prior to an image being used in a production cluster.

Tools like AppArmor and SELinux should also be used to further protect the environment from malicious containers.

Security is more than just ‘settings and configuration’. It is an ongoing process of issue detection using intrusion detection tools and behavioral analytics. There needs to be an ongoing process of assessment, prevention, detection, and reaction following written and often updated policies.

Accessing the API
To perform any action in a Kubernetes cluster, you need to access the API and go through three main steps.

1. Authentication (token)
The type of authentication used is defined in the kube-apiserver startup options. Below are four examples of a subset of configuration options that would need to be set depending on what choice of authentication mechanism you choose:

- --basic-auth-file
- --oidc-issuer-url
- --token-auth-file
- --authorization-webhook-config-file
To learn more about authentication, see the official documentation.

2. Authorization (RBAC)
RBAC stands for Role Based Access Control. All resources are modeled API objects in Kubernetes, from Pods to Namespaces. They also belong to API Groups such as core and apps. These resources allow operations such as Create, Read, Update, and Delete (CRUD), which we have been working with so far.

In YAML files, operations are referred to as verbs. We will add more API elements to these fundamental ones, which subsequently can be controlled by RBAC.

Rules are operations which can act upon an API group.

Roles are a group of rules which affect, or scope, a single namespace, whereas ClusterRoles have a scope of the entire cluster.

Each operation can act upon one of three subjects: User Accounts, which don’t exist as API objects; Service Accounts, and Groups, which are known as clusterrolebinding when using kubectl.

RBAC is then writing rules to allow or deny operations by users, roles or groups upon resources.

Admission Controllers
The last step in letting an API request into Kubernetes is Admission Control.

Admission controllers are pieces of software that can access the content of the objects being created by the requests. They can modify the content or validate it, and potentially deny the request.

Admission controllers are needed for certain features to work properly. Controllers have been added as Kubernetes has matured. As of the v1.12 release, the kube-apiserver uses a compiled-in set of controllers. Instead of passing a list, we can enable or disable particular controllers. If you want to use a controller not available by default, you would need to download source and compile.

The first controller is Initializers, which will allow dynamic modification of the API request, providing great flexibility. Each admission controller functionality is explained in the documentation. For example, the ResourceQuota controller will ensure that the object created does not violate any of the existing quotas.

Also, tools like the Open Policy Agent can be used to manage admission control externally. The Open Policy Agent (OPA, pronounced “oh-pa”) is an open source, general-purpose policy engine that unifies policy enforcement across the stack. OPA provides a high-level declarative language that lets you specify policy as code and simple APIs to offload policy decision-making from your software. You can use OPA to enforce policies in microservices, Kubernetes, CI/CD pipelines, API gateways, and more.

OPA was originally created by Styra and is a graduated project in the Cloud Native Computing Foundation (CNCF) landscape.