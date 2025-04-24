## Short Description

The project deploys an HTTP server (NGINX) on Kubernetes using Minikube. It uses an NFS server for shared persistent storage via dynamically provisioned PVC. A Kubernetes Job populates the shared volume with static content that is then served by the web server.

- NFS Server: Provides shared storage for other pods.
- PVC: Dynamically created by the Helm chart and used in both Deployment and Job.
- Deployment (NGINX): Serves static HTML content from the shared PVC.
- Job: Writes an index.html file to the shared storage.
