# Home Assigment implementation Guide
## Prerequisites:

* **Docker**: Installed and running on your system.
* **Kubernetes**: Enabled in Docker Desktop or Minikube installed and running.
* **Kubectl**: The Kubernetes command-line tool (kubectl) installed.
* **Python** and Pip: Python 3.x and pip installed on your system.
* **GitHub Personal Access Token**: With the required repo and workflow scopes.
* **Helm**: 
1. Prepare the Code and Environment:

Create Files:
Save the Flask app code as app_k8s.py.
Save the HTML template as index.html in a templates folder within the same directory as app_k8s.py.
Create a requirements.txt file:
Flask
PyGithub
prometheus_client
Werkzeug
Flask-Cors
gunicorn
Install Python Libraries:
Bash
pip install -r requirements.txt
חשוב להשתמש בקוד בזהירות.
content_copy
2. Build the Docker Image:

Create a Dockerfile: Use the provided Dockerfile (see previous responses) to define how to build your Docker image.
Build the Image: Run the following command in the directory where your Dockerfile and app_k8s.py files are located:
Bash
docker build -t your-image-name:latest .
חשוב להשתמש בקוד בזהירות.
content_copy
Replace your-image-name with the desired name for your image.

3. Deploy to Kubernetes:

Create Kubernetes Resources:
Secret (Optional): If you're using a Kubernetes Secret to store your GitHub token, create it:
Bash
kubectl create secret generic github-token-secret --from-literal=token=<YOUR_GITHUB_TOKEN>
חשוב להשתמש בקוד בזהירות.
content_copy
Deployment:
Bash
kubectl apply -f deployment.yaml
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

