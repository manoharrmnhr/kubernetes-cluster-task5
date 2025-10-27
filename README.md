# 🚀 TASK 5: Build a Kubernetes Cluster Locally with Minikube

## 🧭 Objective
Set up a **local Kubernetes cluster** using **Minikube** and **kubectl**, deploy a sample application, expose it via a service, and perform management tasks like scaling and viewing logs.

---

## 🧰 Tools Used
- **Minikube** — to create and manage the local Kubernetes cluster  
- **kubectl** — Kubernetes command-line tool  
- **Docker** — container runtime used by Minikube  

---

## ⚙️ Step-by-Step Process

### 🏁 Step 1: Install Required Tools
Install Docker, Minikube, and kubectl:
```bash
sudo apt update
sudo apt install docker.io -y
curl -LO https://storage.googleapis.com/minikube/releases/latest/minikube-linux-amd64
sudo install minikube-linux-amd64 /usr/local/bin/minikube
curl -LO "https://dl.k8s.io/release/$(curl -L -s https://dl.k8s.io/release/stable.txt)/bin/linux/amd64/kubectl"
sudo install -o root -g root -m 0755 kubectl /usr/local/bin/kubectl

🚀 Step 2: Start the Minikube Cluster
minikube start --driver=docker

📦 Step 3: Create Deployment

Create a file named deployment.yaml:
apiVersion: apps/v1
kind: Deployment
metadata:
  name: myapp-deployment
spec:
  replicas: 2
  selector:
    matchLabels:
      app: myapp
  template:
    metadata:
      labels:
        app: myapp
    spec:
      containers:
      - name: myapp
        image: nginx
        ports:
        - containerPort: 80

Apply it:
kubectl apply -f deployment.yaml

Verify:
kubectl get deployments
kubectl get pods


🌐 Step 4: Expose the App with a Service
Create a file named service.yaml:
apiVersion: v1
kind: Service
metadata:
  name: myapp-service
spec:
  type: NodePort
  selector:
    app: myapp
  ports:
  - port: 80
    targetPort: 80
    nodePort: 30007

Apply and check:
kubectl apply -f service.yaml
kubectl get services

Access the app:
minikube service myapp-service

📊 Step 5: Scale the Deployment
kubectl scale deployment myapp-deployment --replicas=4
kubectl get pods

📸 Step 7: Screenshots and Evidence
<img width="1280" height="648" alt="image" src="https://github.com/user-attachments/assets/42fc104c-d298-40b1-bfa7-19a5453d0bdc" />

kubernetes-cluster-task5/
├── README.md
├── deployment.yaml
├── service.yaml
└── screenshots/
    ├── minikube_start.png
    ├── kubectl_get_pods.png
    ├── kubectl_get_svc.png
    ├── minikube_service_output.png
    ├── kubectl_scale.png
    ├── kubectl_logs.png
    └── kubectl_describe_pod.png

✅ Summary
Step	Description	Status
Install Minikube & kubectl	Successfully installed	✅
Start Cluster	Cluster created with Docker driver	✅
Deploy Application	Nginx app deployed via YAML	✅
Expose Service	NodePort service created	✅
Verify Pods & Services	Verified using kubectl commands	✅
Scale Deployment	Increased replicas successfully	✅
Logs & Describe	Retrieved pod details & logs	✅

👨‍💻 Author

Manohar R
DevOps Learner | Kubernetes Enthusiast
📅 Task Completed: October 2025

