A context is a  group of acces parameters to a k8s cluster.
Contains a K8s cluster, a user and a namespace
The current context is the cluster that is currently the default for kubectl
   - All kubectl commands run aganist that cluster

 #### get current context
` - kubectl config current-context`
#### list all context
`- kubectl config get-contexts`

#### set the current context
`- kubectl config use-context [contextName]`
#### Delete a context from the config file
`- kubectl config delete-context [contextName]`


Instead of tying
` - kubectl config use-context minikube`
use `kubectx` to quckly switch context,, by typing kubectx`[contextName]`

