# k8s
# WordPress on Kubernetes with NGINX Ingress and Grafana Monitoring
This project demonstrates how to deploy a WordPress application and a Mariadb on a Kubernetes cluster using NGINX Ingress for routing external traffic. It also sets up monitoring using Prometheus and Grafana to keep track of container uptime and application performance.

# Prerequisites
Before you begin, make sure you have the following tools and resources set up:

- An Amazon EKS cluster (or Minikube for local testing).
- kubectl installed and configured to interact with your cluster.
- Docker installed for building and pushing images.
- AWS CLI and permissions to use Amazon ECR for pushing Docker images.
- Helm installed for managing Kubernetes applications.



# 1. Create the Namespace
First, you need to create the namespace in which you will deploy all your resources. The namespace ensures that your resources do not conflict with others in the cluster.

Command: kubectl create namespace adi-wordpress-app

# 2. Installing NGINX Ingress Controller
Install the NGINX Ingress Controller using Helm
Use Helm to install the NGINX Ingress Controller into your Kubernetes Namespace:

command: helm install nginx-ingress ingress-nginx/ingress-nginx --namespace ingress-nginx --create-namespace -f values.yaml


# 3. Deploy the MariaDB Service
The first step is to deploy the MariaDB service, which allows your application to communicate with the database.

command: kubectl apply -f mariadb-service.yaml

# 4. Deploy the MariaDB StatefulSet
deploy the StatefulSet, which manages the MariaDB deployment, ensuring persistent data storage with volumes (PVC).

Command: kubectl apply -f mariadb-statefulset.yaml

# 5. Deploy the PersistentVolumeClaim for MariaDB
The PVC requests dynamic storage for MariaDB's data.

Command: kubectl apply -f mdb-pvc.yaml

# 6. Deploy the StorageClass for EBS
This step is important if you wish to use AWS EBS as your storage solution.

Command: kubectl apply -f storageclass-ebs-adi.yaml

# 7. Deploy the WordPress Deployment
After defining the MariaDB service, you need to deploy the WordPress application. This will deploy the WordPress pods.

Command: kubectl apply -f wordpress-deployment.yaml

# 8. Deploy the Ingress
The Ingress ensures that your application is accessible through a domain or an IP address. In this step, you route traffic to WordPress and potentially Grafana, if applicable.

Command: kubectl apply -f ingress-wordpress.yaml

# 9. Deploy the WordPress Service
Once the WordPress Deployment is running, you need to create a service to expose the WordPress application.

Command: kubectl apply -f wordpress-service.yaml

# 10. Deploy the PersistentVolumeClaim for WordPress
Finally, you need to deploy the PVC for WordPress storage (such as content, plugins, etc.).

Command: kubectl apply -f wp-pvc.yaml

# Deploying Prometheus and Grafana using Helm in EKS

# 1. Add the Prometheus and Grafana repositories to Helm

command: helm repo add prometheus-community https://prometheus-community.github.io/helm-charts
         helm repo add grafana https://grafana.github.io/helm-charts

# 2. Install Prometheus

command: helm install [unique-name]  prometheus-community/kube-prometheus-stack \
  --set prometheus-node-exporter.service.port=9101 \
  --set prometheus-node-exporter.service.targetPort=9101 \
  --set prometheus-node-exporter.containerPort=9101 -f values.yaml


