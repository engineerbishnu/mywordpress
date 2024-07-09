# Stateful Web-app deployment using mysql and wordpress with k8s.
 
In this repository,  contains Kubernetes manifests to deploy a MySQL StatefulSet and a WordPress Deployment with PersistentVolumeClaims (PVCs) and Services. We can use this manifest file for locally hosted server with the help of k3d and kubectl. To do so, First of all, we need to setup tools named k3d and kubectl locally and then work with this repo file. Above repo file, I did mentioned all resources in single file like web-deployment part, database deployment part, persistant volume part and comfigmap part all are in single file. We can make them separately, but also we can use as single file. Above file for demo project deploying wordpress website with databases.
 
## Prerequisites

## Requirement:1
- Need to do setup k8s tools like k3d and kubectl.

## Requirement:2
- A Kubernetes cluster
- `kubectl` configured to access your Kubernetes cluster
 
## Deployment Part
 
1. **First, clone the Repository:**
 
    ```sh
    git clone https://github.com/engineerbishnu/mywordpress.git
    cd mywordpress
    ```
 
2. **Then, Create cluster one for master or control plane and another for worker:**
 
    ```sh
    k3d cluster create bishnu --agents 2  # agents=2 means two worker node where our entire database and website hosted.
    kubectl get nodes # It will list out all of the created nodes.
    ```
 
3. **Now, Let's Deploy WordPress and Database alongside with all pre-requisite by using manifest :**
 
    Apply the created yaml manifest file:
 
    ```sh
    kubectl apply -f wordpress-allinone-deployment.yaml
    ```
 
## Accessing WordPress
 
Once deployed, WordPress can be accessed using the external IP of the LoadBalancer service on port `80`. You can get the external IP by running:
 
```sh
kubectl get svc