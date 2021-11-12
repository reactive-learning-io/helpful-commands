# GKE
## Login to gcloud
`gcloud auth login`

### Get projects list
`gcloud projects list`

### Change project 
`gcloud config set project my-project`

### Get list of clusters
`gcloud container clusters list`

---

# kubectl

Get cluster credentials to add cluster information in $HOME/.kube/config file

### Get cluster credentials
`gcloud container clusters get-credentials NAME --zone=ZONE --region=REGION`

### List all contexts
`kubectl config get-contexts`

### Set preferred context
`kubectl config set-context --cluster=[CLUSTER] --user=[USER]`

### Delete a context
`kubectl config delete-context`

### Select working context
`kubectl config use-context [CONTEXT_NAME]`

---

# Google Container Registry (GCR)

### Clone sample app repo
`git clone https://github.com/GoogleCloudPlatform/kubernetes-engine-samples`

### Change directory
`cd kubernetes-engine-samples/hello-app`

### Bulid docker image
`docker build -t gcr.io/${GCP_PROJECT_ID}/hello-app:v1 .`

### List all images
`docker images`

### Configure Docker to work with GCR
`gcloud auth configure-docker`

### Push Docker image to GCR
`docker push gcr.io/${GCP_PROJECT_ID}/hello-app:v1`

---

# Google Kubernetes Engine (GKE)

### Create a new cluster in current GCP Project.
`gcloud container clusters create hello-cluster --num-nodes=3`

### Get Compute instance
`gcloud compute instances list`

### Create name space
`kubectl create namspace hello-namespace`

### Deploy image in GKE
`kubectl run hello-web --image=gcr.io/${GCP_PROJECT_ID}/hello-app:v1 --port 8080 -n hello-namespace`

### List pods in a namespace
`kubectl get pods -n hello-namespace`

### Expose app on port 80 through LoadBalancer Service type
`kubectl expose deployment hello-web --type=LoadBalancer --port 80 --target-port 8080 -n hello-namespace`

### List Service
`kubectl get service -n hello-namespace`

### Scale Deployment to 3 repicas
 `kubectl scale deployment hello-web --replicas=3 -n hello-namespace`

### List Deployment
`kubectl get deployment hello-web -n hello-namespace`

### List Pods
`kubectl get pods -n hello-namespace`

---

## Clean up

### Delete a Service
`kubectl delete service hello-web -n hello-namespace`

### Delete a Deployment
`kubectl delete deployment hello-web -n hello-namespace`

### Delete a namespace
`kubectl delete namespace hello-namespace`

### Delete a Cluster
`gcloud container clusters delete hello-cluster`

---
[Learn more](https://cloud.google.com/sdk/gcloud/reference/container/clusters/describe)
