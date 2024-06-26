# Home Assigment implementation Guide
## Prerequisites:

* **Docker**: Installed and running on your comuter.
* **Helm**: Installed and working on your computer.
* **Kubernetes**: Enabled kubernetes in **Docker Desktop** or Kind installed and running.
* **Kubectl**: The Kubernetes command-line tool (kubectl) installed.
* **Python** and Pip: Python 3.x and pip installed on your system.
* **GitHub Personal Access Token**: With the required repo and workflow scopes.
  [Create Github token](https://docs.github.com/en/authentication/keeping-your-account-and-data-secure/managing-your-personal-access-tokens)


## Project stracture:
<img src="https://github.com/idmishor/temp/assets/173612976/50fffe36-5813-489b-aa8a-e041e439d5c9" width="250" height="250">

## 1. Clone the environment:
```
git clone https://github.com/idmishor/helm-idan-legit.git
cd helm-idan-legit 
```
## 2. Build the Docker Image:
```
cd Docker
docker build -t legit:latest .
# For the purpose of simplicity for this assigment we will work with local docker repository instead a remote dokcer repository
```

## 3. Deployment using helm:
 * Create kubernetes Secret to store your GitHub token:
 ```
 kubectl create secret generic github-token-secret --from-literal=token=<YOUR_GITHUB_TOKEN>
 ```

 * Package the Chart:
 ```
 cd helm-idan-legit 
 helm package helm-idan-legit/
 ```
 helm package
 
 * Deploy the helm chart
 ```
 helm install [name]-0.1.0.tgz -f values.yaml
 ```

## 4. Verify Deployment
```
kubectl get pods,svc
```

## 5. Access the Web Interface:
### Option 1 (LoadBalancer - if using Docker app for mac):
 * Get LoadBalancer IP and Port:
```
kubectl get svc [name]-repo-creator
```
* Access the App: Open your web browser and go to: http://localhost:<PORT>/ (replace <PORT> with the actual port number).

### Option 2 (NodePort):
 * Get the service port
```
Run kubectl get svc[name]-repo-creator to get the assigned NodePort.
Access the web interface at: http://localhost:<NodePort>/
```

## 6. Access using command line
 * Access the create repo API:
 ```
 curl -X POST -H "Content-Type: application/json" -d '{"repo_name": "test-repo", "repo_description": "idan full"}' http://localhost:<PORT>/api/create_repo (replace <PORT> with the actual port 
 number)
```

* Access the Metrics API:
```
curl http://localhost:<PORT>/metrics (replace <PORT> with the actual port number)
```
