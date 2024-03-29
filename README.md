# ArgoCD
## Starting ArgoCD on Minikube
### Prerequisites

Before you start, make sure you have the following installed on your machine:

Docker  
Minikube

### Steps:

Start Minikube

```sh
minikube start
```

Deploy ArgoCD in the argocd namespace:  

```sh
kubectl create namespace argocd
kubectl apply -n argocd -f https://raw.githubusercontent.com/argoproj/argo-cd/stable/manifests/install.yaml
```

Check all the pod is up:
```sh
kubectl get po -n argocd -w
```

Create a port-forward to the ArgoCD server:  

```sh
kubectl port-forward svc/argocd-server -n argocd 8080:443
```

Access the ArgoCD UI in your web browser at https://localhost:8080. Log in with the default username admin and the password obtained by running the following command:

```sh 
kubectl -n argocd get secret argocd-initial-admin-secret -o jsonpath="{.data.password}" | base64 -d
``` 

That's it! You can now start using ArgoCD on Minikube.

(Starting the deployment using `kubectl apply -f application.yaml`

## Trubeshoot
check if exists service:
```sh
minikube service myapp-service --url 
```
if svc no up, check if the port 30002 is avilable. 
