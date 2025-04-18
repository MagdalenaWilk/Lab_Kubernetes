The application was deployed in a local Minikube Kubernetes cluster. It consists of an NFS server provisioner for dynamic persistent storage and a simple Nginx-based HTTP server.

Helm was used to install the NFS server provisioner. A PersistentVolumeClaim was created, which was then mounted to the Nginx pod. A Kubernetes Job was used to populate the NFS volume with sample HTML content.

The web content is accessible via a Service. Below is a screenshot of the web application running in the browser.

NFS Server Provisioner (installed via Helm) dynamically creates Persistent Volumes.

PersistentVolumeClaim requests storage using the custom StorageClass (nfs-sc).

Nginx Deployment mounts the PVC and serves static HTML files from the volume.

Kubernetes Job writes sample HTML content to the shared NFS volume.

Service exposes the Nginx pod to external clients.
