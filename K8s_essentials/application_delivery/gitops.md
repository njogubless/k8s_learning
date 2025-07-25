GitOps
Infrastructure as Code was a real revolution in increasing the quality and speed of providing infrastructure, and it works so well that today, configuration, network, policies, or security can be described as code, and often even live in the same repository as the software.

GitOps takes the idea of Git as the single source of truth a step further and integrates the provisioning and change process of infrastructure with version control operations.

If code was branched and should be merged back into the main branch, you can create a merge or pull request that can be reviewed by other developers before actually merging it. This has been a best practice for a long time in software development, and also includes running a CI pipeline for every change that should be made. In GitOps, these merge requests are used to manage infrastructure changes.

There are two different approaches how a CI/CD pipeline can implement the changes you want to make:

Push-based
The pipeline is started and runs tools that make the changes in the platform. Changes can be triggered by a commit or merge request.
Pull-based
An agent watches the git repository for changes and compares the definition in the repository with the actual running state. If changes are detected, the agent applies the changes to the infrastructure.
Two examples of popular GitOps frameworks that use the pull-based approach are Flux and ArgoCD. ArgoCD is implemented as a Kubernetes controller, while Flux is built with the GitOps Toolkit, a set of APIs and controllers that can be used to extend Flux, or even build a custom delivery platform.

The ArgoCD architecture gives a good overview of how GitOps can be implemented.
Kubernetes is particularly well suited for GitOps, since it provides an API and is designed for declarative provisioning and changes of resources right from the beginning. You might notice that Kubernetes is using a similar idea as the pull based approach: A database is watched for changes and the changes are applied to the running state if it doesn’t match the desired state.

To learn more about GitOps in action and the usage of ArgoCD and Flux, consider enrolling for the free course Introduction To GitOps (LFS169).