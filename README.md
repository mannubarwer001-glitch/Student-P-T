# Student Performance Tracker
An end-to-end web application designed to track student performance, attendance, and marks percentage, containerized with Docker and fully orchestrated using Kubernetes.
Architecture Overview
.
                        +----------------------+
                        |   Kubernetes  /|
                        |      NodePort        |
                        +----------+-----------+
                                   |
                                   v
                        +----------------------+
                        |  K8s Service / Pod   |
                        +----------+-----------+
                                   |
                         +---------+
                         |                   
                         v                   
              +--------------------+ 
              |   Docker Image     | 
              | (Containerized App)|  
              +--------------------+ 

# The application tracks:
 * Academic Marks: Subject-wise performance and percentage calculations.
 * Attendance Tracking: Daily attendance logs and threshold warnings.
 * Performance Analytics: Comprehensive summary of overall student progress.
# Tech Stack & DevOps Infrastructure
 * Application: Full-stack Web Application
 * Containerization: Docker
 * Orchestration: Kubernetes (Deployments, Pods, Service)
 * CI/CD & Source Control: Git / GitHub
 # Project Structure
├── k8s/
│   ├── deployment.yaml    # Kubernetes deployment configuration
│   ├── service.yaml       # Kubernetes service exposing the app                         
├── Dockerfile             # Container build file         
├── README.md              # Project documentation
└── src/                   # Application source code

# Quick Start (Local Setup)
1. Clone the Repository
git clone https://github.com/mannubarwer001-gitch/Student-P-T.git

2. Run with Docker
Build the container image and run it locally:
# Build Docker image
docker build -t student-performance-tracker:latest .

# Run container
docker run -d -p 8080:8080 --name student-tracker-app student-performance-tracker:latest

Access the app locally at http://localhost:8080.
Kubernetes Deployment Guide
Prerequisites
 * kubectl CLI configured
 * A running Kubernetes cluster (Minikube, Kind, EKS, or GKE)
 * Container registry account (Docker Hub / ECR)
# Steps to Deploy
 * Tag and Push Docker Image
   docker tag student-performance-tracker:latest <your-dockerhub-username>/student-performance-tracker:v1.0.0
docker push <your-dockerhub-username>/student-performance-tracker:v1.0.0

 * Apply Storage Manifests (Optional/Persistent Data)
   kubectl apply -f k8s/pvc.yaml

 * Deploy the Application
   kubectl apply -f k8s/deployment.yaml

 * Expose the Service
   kubectl apply -f k8s/service.yaml

Monitoring & Troubleshooting
Check running Pods and Deployments:
kubectl get pods
kubectl get deployments
kubectl get svc

Inspect Pod logs:
kubectl logs -f deployment/student-performance-tracker

Port-forward to test locally without exposing external IPs:
kubectl port-forward svc/student-tracker-service 8080:8080

Author
Developed & Deployed by Cloud / DevOps Engineer
