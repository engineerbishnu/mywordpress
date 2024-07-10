# Stateful Web-app deployment using mysql, wordpress & ingress with k8s.
 
In this repository, it contains Kubernetes manifests to deploy a MySQL StatefulSet database, WordPress, & Ingress along with PersistentVolumeClaims (PVCs) and Services. We can use this manifest file for locally hosted server with the help of k3d and kubectl. To do so, First of all:
- We need to setup tools named k3d and kubectl locally and then work with this repo file. 
- Above repo file, I did mentioned all resources in single file like web-deployment part, database deployment part, persistant volume part and comfigmap part all are in single file.
- We can make them separately, but also we can use as single file. Above file for demo project deploying wordpress website with databases.

While deploying a stateful web app with MySQL, WordPress, and an Ingress on Kubernetes (k8s), need to take care of:
- **MySQL**: Configure with PersistentVolumeClaim for data storage, deploy using a Deployment, expose via a Service.
- **WordPress**: Deploy similarly with a Deployment, connect to MySQL using Service DNS.
- **Ingress**: Expose WordPress to the internet, handle HTTP(S) traffic, set up TLS if needed.
- **Considerations**: Ensure data integrity, manage scaling cautiously, secure with secrets and network policies.

 
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
    kubectl apply -f wordpresswithdatabase-deployment.yaml
    ```
    After that, there is Lb give us external IP which is used as ip-domain naming while traffic and port forwarding with internal ports from external connections. Because pods IPs are not accessible from outside so we need ingress controller for communicate outside world and inside world.

    - Copy the external IP and edit ingress host with that ip like this way:
        ```sh
    nano ingress.yaml
    # paste ip in host section here and save the file.
    ```

4. **Now, Let's Deploy Ingress and Traffic Handle by using ingress manifest deployment :**
    ```sh
    kubectl apply -f ingress.yaml
    ```
 
## Accessing WordPress
 
Once deployed, WordPress can be accessed using the external IP directly. We can get the external IP by running:
 
```sh
kubectl get svc
```