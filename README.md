## 🚀 Project 2: Nginx Web Server on Kubernetes

This project demonstrates how to deploy a custom Nginx web server inside a Kubernetes cluster using Minikube. The web page is served from a custom Docker image containing static content.

---

## 📁 Project Structure

k8s-nginx-server/
│
├── Dockerfile
├── index.html
├── nginx-deployment.yaml
├── nginx-service.yaml
├── README.md
└── screenshots/
└── screenshot.png

## 🐳 Docker

The Docker image is built from a custom `index.html` file and the official Nginx base image.

**Dockerfile:**

```dockerfile
FROM nginx:latest
COPY index.html /usr/share/nginx/html/index.html

☸️ Kubernetes Manifests

Deployment (nginx-deployment.yaml):

apiVersion: apps/v1
kind: Deployment
metadata:
  name: nginx-deployment
spec:
  replicas: 1
  selector:
    matchLabels:
      app: nginx
  template:
    metadata:
      labels:
        app: nginx
    spec:
      containers:
        - name: nginx
          image: chimaobi-nginx:v1
          ports:
            - containerPort: 80


Service (nginx-service.yaml):

apiVersion: v1
kind: Service
metadata:
  name: nginx-service
spec:
  type: NodePort
  selector:
    app: nginx
  ports:
    - port: 80
      targetPort: 80
      nodePort: 30080


📸 Screenshot
Below is the custom Nginx welcome page running on Kubernetes via Minikube:

🚀 How to Deploy

Start Minikube

minikube start
Use Minikube Docker environment

bash
eval $(minikube docker-env)
Build Docker Image

bash
docker build -t chimaobi-nginx:v1 .

Apply Kubernetes Manifests

bash
kubectl apply -f nginx-deployment.yaml
kubectl apply -f nginx-service.yaml

Access the App

Get Minikube IP:
bash
minikube ip
Then open this in your browser:
http://<minikube-ip>:30080

✅ Completed and pushed to GitHub: https://github.com/Sammyblck16/k8s-nginx-server

🙌 Author
Chimaobi Iberi
