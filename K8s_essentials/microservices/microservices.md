### Microservices
microservices are distributed components with specific characteristics.
They perform specific business functions and all fucntions grouped together form the overall functionality of the original monolith application
Microservices can be deployed individually on separate servers provisioned with fewer resources- only the needful for each service.
Microservice architecture is aligned with event driven architecture and service-oriented architecture principles, where complex applications are composed of small independent processes which communicates with each other through APIs. APIs allow access to other internal servers of the same application or external thirdparty services and applications.
The benefits of micro-services is scalability. Each microservice can be scaled individually, either manually or automated through demand-based autoscaling.
Seamless upgrades and patching processes are other benefits of miscroservices architecture.
There is virtually no downtime and np service disruption to clients because upgrades are rolled out seamlessly - one service at a time, rather than having to recompile, rebuild and restart an entire monolithic application.
As a result business are able to rollout new features and updates alot faster.
---
### Refactoring
Monolisthic sized multi-process application cannot run as a microservice.
The next natural step from the monolithic to nicroservice transition was refactoring, though it poses a big challenge " Big bang" approach or incremental refactoring.
The "Big-bang" approach focuses all eforrts with the refactoring of the monolith, postponing the developement and implementation of new features- essentially delaying progress and probably breaking the core of the business.
AN incremental refactoring approach gurantees that new features are developed and implemented as modern microservices which are able  to commuicate with the monolith through APIs, without appending the monoliths code.
In the meantime, features are refactored out  of the monolith which fades way while all/most functionality is modernized to modern microservices.
This approach provides an incremental transition from legacy monolith to modern microservices architecture.

Once an enterprise chooses the refactoring path, there are other considerations in the process : 
- Which business components to separate from the monolith to become distributed microservices.
- How to decouple the databases from the application to separate data complexity from application logic.
- How to test the new microservices and their dependencies.

*The refactoring phase slowly transforms the monolith into a cloud-native application which takes full advantage of cloud features, by coding in new programming languages and applying modern architectural patterns. Through refactoring, a legacy monolith application receives a second chance at life - to live on as a modular system adapted to fully integrate with today's fast-paced cloud automation tools and services.*

---
### Challenges
Not all monoliths are best candidates for the refactoring face and some of them may not survive the transition.
A number of factors are considered to determine if a monolith is a suitable candidate for refactoring e.g

- Older programing languages, - considering a legacy mainframe based system written in assembly or Cobol, its much better to redo the whole system as a CloudNative application.
 - A poorly designed  legacy application should be redesigned and re-built from scratch following modern architectural patterns for microservices and even containers.
 - Application tightly coupled together with data stores  are not best candidates for refactoring.

*Once the monolith survived the refactoring phase, the next challenge is to design mechanisms or find suitable tools to keep alive all the decoupled modules to ensure application resiliency as a whole.*

 - Choosing runtimes poses a challenge as well. Deploying multiple modules on a single server either physical or virtual, chances are that different libraries and runtime environments may conflict with one another, causing errors and failures.

 Running independent modules on their own server  to separate their dependencies asa a solution for the conflicts is not ideal in regards to resource allocatin for each service, since all servers could run Operating Systems underneath and probably the module in deployement does not consume as much resource as the OS operating within, with this came Containers as a solution. 

 *Eventually a solution emerged to tackle these refactoring challenges. Application containers came along providing encapsulated lightweight runtime environments for application modules. Containers promised consistent software environments for developers, testers, all the way from Development to Production. Wide support of containers ensured application portability from physical bare-metal to Virtual Machines, but this time with multiple applications deployed on the very same server, each running in their own execution environments isolated from one another, thus avoiding conflicts, errors, and failures. Other features of containerized application environments are higher server utilization, individual module scalability, flexibility, interoperability and easy integration with automation tools.*