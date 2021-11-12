## Minikube

## Starting minikube
`minikube start --driver=<driver_name>`
### If running Virtual Box
`minikube start --driver=virtualbox`
### If running Hyper V
`minikube start --driver=hyperv --memory=4000mb`
### Alternate command
`minikube start --vm-driver hyperv`

### Additional param
`--memory=4000mb`

### Commands
```
minikube status
minikube start
minikube stop
minikube delete
```

### Open Dashboard
`minikube dashboard`

### Switching kubectl Context
`kubectl config use-context minikube`


## Minikube kubectl
`minikube kubectl -- get pods`

---
## Pushing local doker image to minikube
```
minikube cache add <image:tag>
minikube cache reload
minikube cache list
minikube cache delete <image:tag>
```


### Reference
- [Handbook](https://minikube.sigs.k8s.io/docs/handbook/pushing/)
- [Install Minikube through installer](https://kubernetes.io/docs/tasks/tools/install-minikube/)

- [Playground](https://kubernetes.io/docs/tutorials/hello-minikube/)

- [Deployments](https://kubernetes.io/docs/concepts/workloads/controllers/deployment/)
- [RBAC Auth](https://kubernetes.io/docs/reference/access-authn-authz/rbac/#role-and-clusterrole)