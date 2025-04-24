# Kubernetes HTTP Server with NFS Storage

This project demonstrates how to deploy an HTTP server (NGINX) on a Kubernetes cluster using Minikube. The web content is shared using an NFS server and a dynamically provisioned PersistentVolumeClaim.

## How to Run

```bash
minikube start

# Mount local folder to use as NFS backend (adjust path as needed)
minikube mount C:\tmp\nfs:/mnt/nfs

# Add Helm repo
helm repo add stable https://charts.helm.sh/stable
helm repo update

# Install NFS server provisioner
helm install nfs-server-provisioner stable/nfs-server-provisioner `
  --set nfs.server.address=$(minikube ip) `
  --set nfs.server.path="/mnt/nfs" `
  --set storageClass.name="nfs-sc"

# Apply Kubernetes manifests
kubectl apply -f pvc.yaml
kubectl apply -f nginx-deployment.yaml
kubectl apply -f service.yaml
kubectl apply -f job.yaml

# Access your application
minikube service http-server-service
