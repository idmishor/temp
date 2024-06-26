# Home Assigment implementation Guide
## Prerequisites:

* **Docker**: Installed and running on your comuter.
* * **Helm**: Installed and working on your computer.
* **Kubernetes**: Enabled kubernetes in **Docker Desktop** or Kind installed and running.
* **Kubectl**: The Kubernetes command-line tool (kubectl) installed.
* **Python** and Pip: Python 3.x and pip installed on your system.
* **GitHub Personal Access Token**: With the required repo and workflow scopes.
  * [Create Github token](https://docs.github.com/en/authentication/keeping-your-account-and-data-secure/managing-your-personal-access-tokens)

## Project stracture:
![image](https://github.com/idmishor/temp/assets/173612976/50fffe36-5813-489b-aa8a-e041e439d5c9) | height=200

<img src=(https://github.com/idmishor/temp/assets/173612976/50fffe36-5813-489b-aa8a-e041e439d5c9) width="200" height="200" />


## 1. Clone the environment:
```
**Bash**
git clone https://github.com/idmishor/helm-idan-legit.git
cd helm-idan-legit 
```
## 2. Build the Docker Image:
```
**Bash**
cd Docker
docker build -t legit:latest .
# For the purpose of simplicity for this assigment we will work with local docker repository instead a remote dokcer repository
```

## 3. Deployment using helm:
 * Create kubernetes Secret to store your GitHub token:
 ```
 **Bash**
 kubectl create secret generic github-token-secret --from-literal=token=<YOUR_GITHUB_TOKEN>
 ```

 * Package the Chart:
 ```
 **Bash**
 cd helm-idan-legit 
 helm package helm-idan-legit/
 ```
 helm package
 
 * Deploy the helm chart
 ```
 **Bash**
 cd ..
 helm install [name]-0.1.0.tgz -f values.yaml
 ```

## 4. Verify Deployment
```
**Bash**
kubectl get pods,svc
```

## 5. Access the Web Interface:
### Option 1 (LoadBalancer - if using Docker app for mac):
 * Get LoadBalancer IP and Port:
```
**Bash**
kubectl get svc [name]-repo-creator
```
* Access the App: Open your web browser and go to: http://localhost:<PORT>/ (replace <PORT> with the actual port number).

### Option 2 (NodePort):
 * Get the service port
```
**Bash**
Run kubectl get svc[name]-repo-creator to get the assigned NodePort.
Access the web interface at: http://localhost:<NodePort>/
```
חשוב להשתמש בקוד בזהירות.
content_copy
Service:
Bash
kubectl apply -f service.yaml
חשוב להשתמש בקוד בזהירות.
content_copy
Wait for Deployment:
Bash
kubectl rollout status deployment/<your-deployment-name>
חשוב להשתמש בקוד בזהירות.
content_copy
Wait until the deployment status shows "successfully rolled out."
(Docker Desktop Only) Get the LoadBalancer IP and Port:
Bash
kubectl get svc api-create-repo
חשוב להשתמש בקוד בזהירות.
content_copy
Note the EXTERNAL-IP and PORT(S).
(Minikube Only) Start Tunnel:
Bash
minikube tunnel
חשוב להשתמש בקוד בזהירות.
content_copy
If you are using Minikube and want to test it using a LoadBalancer.
4. Access the Web Interface:

Docker Desktop: Access the web interface using http://localhost:<PORT>/, where <PORT> is the port shown in the PORT(S) column when you get the service details.
Minikube:
With LoadBalancer: Run kubectl get services and access using the assigned IP and port
With NodePort: Get the assigned NodePort using kubectl get services and access the app at: http://<your-minikube-ip>:<NodePort>/. To get Minikube's IP run: minikube ip.

