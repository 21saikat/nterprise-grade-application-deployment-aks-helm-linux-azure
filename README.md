# nterprise-grade-application-deployment-aks-helm-linux-azure
# Enterprise-Grade Application Deployment with Kubernetes, Helm, and Linux Servers on Azure  
**Ibne Sabid Saikat**  
*November 27, 2024*

---

## Introduction  
In this project, I successfully deployed an **enterprise-grade application** using **Kubernetes**, **Helm**, and **Linux servers on Azure**. This hands-on project demonstrates **cloud-native skills**, **DevOps best practices**, and efficient use of Azure services to manage **scalable**, **secure**, and **high-performance applications**.

---

## Why This Project Matters  
Deploying applications in a **reliable** and **scalable** manner is critical for modern enterprises. This project not only showcases the integration of **cloud-native tools** but also emphasizes **monitoring**, **logging**, and **automation** to ensure seamless application management.

---

## Project Steps  

### Step 1: Create the Azure Infrastructure  

#### 1. Create a Resource Group  
```sh
az group create --name Dream-On2 --location westus

2 . Provision an Ubuntu Virtual Machine
az vm create --resource-group Dream-On2 --name myvm --image UbuntuLTS --admin-username <username> --generate-ssh-keys


3. Access the VM and Secure the Server

ssh <username>@<server-ip>
Update and upgrade the system:


sudo apt update && sudo apt upgrade -y
4. Install Docker


sudo apt install docker.io -y
sudo systemctl start docker
sudo systemctl enable docker
5. Install Kubernetes CLI (kubectl)

curl -LO "https://dl.k8s.io/release/$(curl -L -s https://dl.k8s.io/release/stable.txt)/bin/linux/amd64/kubectl"
chmod +x kubectl
sudo mv kubectl /usr/local/bin/
6. Install Helm

curl https://raw.githubusercontent.com/helm/helm/main/scripts/get-helm-3 | bash
7. Install Azure CLI

sudo apt update
sudo apt install -y ca-certificates curl apt-transport-https lsb-release gnupg
curl -sL https://packages.microsoft.com/keys/microsoft.asc | gpg --dearmor | sudo tee /usr/share/keyrings/microsoft.gpg > /dev/null
echo "deb [arch=amd64 signed-by=/usr/share/keyrings/microsoft.gpg] https://packages.microsoft.com/repos/azure-cli/ $(lsb_release -cs) main" | sudo tee /etc/apt/sources.list.d/azure-cli.list
sudo apt update
sudo apt install -y azure-cli
az login
Step 2: Set Up the Kubernetes Cluster
1. Create an AKS Cluster

az aks create --resource-group Dream-On2 --name myAKSCluster --node-count 3 --enable-addons monitoring --generate-ssh-keys --location westus
2. Connect to the AKS Cluster

az aks get-credentials --resource-group Dream-On2 --name myAKSCluster
3. Verify the Cluster

kubectl get nodes
Step 3: Deploy Applications with Helm
1. Create a Helm Chart

helm create myapp
nano myapp/Chart.yaml
Edit Chart.yaml:

yaml

apiVersion: v2
name: myapp
description: A Helm chart for Kubernetes
version: 0.1.0
icon: "https://example.com/icon.png"
2. Deploy with Helm

helm install myapp ./myapp
kubectl get pods
helm upgrade myapp ./myapp
3. Package and Reinstall

helm package myapp
helm uninstall myapp
helm install myapp ./myapp
Step 4: Integrate Monitoring and Logging
1. Enable Azure Monitor

az aks enable-addons --addons monitoring --resource-group Dream-On2 --name myAKSCluster
2. Deploy Prometheus and Grafana via Helm
Add Prometheus and Grafana repositories:

helm repo add prometheus-community https://prometheus-community.github.io/helm-charts
helm install prometheus prometheus-community/prometheus
helm repo add grafana https://grafana.github.io/helm-charts
helm install grafana grafana/grafana
3. Access Grafana Dashboard

kubectl port-forward svc/grafana 3000:80
Open your browser and go to: http://localhost:3000.

Step 5: Build and Push a Docker Image

az acr build --registry <registry-name> --image myapp:v1 .
Outcome
✅ Successfully deployed an enterprise-grade application with Helm and Kubernetes.
✅ Configured monitoring using Azure Monitor, Prometheus, and Grafana.
✅ Demonstrated a scalable, cloud-native solution ready for production.

Repository Information
Repository Name: enterprise-grade-application-deployment-aks-helm-linux-azure
Author: Ibne Sabid Saikat
Technologies Used: Kubernetes, Helm, Azure, Docker, Prometheus, Grafana
🚀 Follow for More Cloud & Kubernetes Projects!
If you found this helpful, feel free to ⭐ star this repository! 😊



You can name your GitHub repository as **`enterprise-grade-application-deployment-aks-helm-linux-azure`** or something shorter, like **`enterprise-app-deployment-aks-helm-azure`**, depending on your preference.

Let me know if you need further modifications!
