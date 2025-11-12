# Minikube Installtion on t3.meduim ubutu ec2 instance  adn disk size 20GB  . Modify volume to 20GB 

### 1. Install Docker (Minikube driver)
sudo apt update && sudo apt upgrade -y
sudo apt install -y docker.io
sudo usermod -aG docker $USER
newgrp docker
sudo systemctl enable docker

### 2. Install Minikube
curl -LO https://storage.googleapis.com/minikube/releases/latest/minikube-linux-amd64
sudo install minikube-linux-amd64 /usr/local/bin/minikube


### 3.Install kubectl  
curl -s https://dl.k8s.io/release/stable.txt
curl -LO https://dl.k8s.io/release/v1.29.0/bin/linux/amd64/kubectl
chmod +x kubectl
sudo mv kubectl /usr/local/bin/
kubectl version --client

### 4. Start Minikube with Docker Driver
minikube start --driver=docker

### 5. Verify Installation
kubectl get nodes


# Installing latest/stable version of ArgoCD
```
kubectl create namespace argocd
kubectl apply -n argocd -f https://raw.githubusercontent.com/argoproj/argo-cd/stable/manifests/install.yaml
```

### Forward Ports
```
k get services -n argocd
kubectl port-forward service/argocd-server -n argocd 8080:443
```

### Get Credentials
```
kubectl -n argocd get secret argocd-initial-admin-secret -o jsonpath="{.data.password}" | base64 -d
```

### Application Port Forward 
kubectl port-forward service/myhelmapp 8888:80 -n dev --address 0.0.0.0
