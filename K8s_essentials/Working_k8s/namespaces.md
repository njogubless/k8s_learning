Namespaces are k8s resource that allow to group other resources.
Objects in one namespace can acces objects in another namespace.
Deleting a namspace will delete all its child objects.
- define a namespace
  ```python
  
   apiVersion: v1
   kind:Namespace
   metadata:
      name:prod
  
  ```
- use the namespace when you have resources.
```python

  apiVersion: v1
   kind:Namespace
   metadata:
      name": myapp-prod
      namespace:prod
    spec:
      containers:
        - name: nginx-container
        image: nginx

```

- One can assign network policies and limit the resources you can create in a namespace using the resource object.

#### List all namespaces
`kubectl get namespace`

#### SHortcut
`kubectl get ns`

#### set the current context to use a namespace
`kubectl config set-contetxt --current --namespace=[namespaceName]`

#### create a namespace
` kubectl create ns [namespaceName]

#### delete namespace
` kubectl delete ns [namespaceName]`

#### list all pods in all namespaces
` kubectl get pods --all-namespaces`

