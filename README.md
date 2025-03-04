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
