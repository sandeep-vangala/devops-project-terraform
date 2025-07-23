# Deploying a Production-Ready 3-Tier Application on AWS EKS with Terraform

Project Overview
Objective: Deploy a 3-tier application consisting of a React frontend, Flask backend, and PostgreSQL database on AWS EKS. Use Terraform to provision infrastructure, including EKS, RDS, ALB, Route 53, and IAM roles. Automate deployment with a Jenkins pipeline, and monitor with Prometheus, Grafana, and Fluentd.
Architecture:
Frontend: React application served via Kubernetes Deployment and exposed through an ALB.
Backend: Flask API handling business logic, connected to RDS PostgreSQL.
Database: Private RDS PostgreSQL instance in the same VPC.
Infrastructure: EKS cluster with managed node groups, ALB for load balancing, Route 53 for DNS, and OIDC for IAM roles.
CI/CD: Jenkins pipeline to build, push images to ECR, deploy to EKS with Helm, and set up monitoring.
Monitoring: Prometheus for metrics, Grafana for visualization, Fluentd for log aggregation.
Production Considerations:
High availability with multi-AZ RDS and EKS nodes.
Secure database access via Kubernetes Secrets and ExternalName Service.
Scalability with EKS managed node groups and ALB.
DNS management with Route 53 for public access.
Monitoring and logging for observability.
Prerequisites
AWS Account: With permissions to create EKS, RDS, ECR, Route 53, IAM, and EC2 resources.
Tools:
Terraform: Install (terraform CLI) for infrastructure provisioning.
AWS CLI: For interacting with AWS services.
kubectl: For Kubernetes management.
Helm: For deploying applications and monitoring stack.
Jenkins: With plugins (Docker Pipeline, AWS Credentials, Kubernetes CLI, Helm, Slack).
Docker: For building images.
Git Repository: Contains application code, Terraform files, Kubernetes manifests, Helm charts, and Jenkinsfile.
Domain: A registered domain for Route 53 (e.g., example.com).
Slack Webhook: For pipeline notifications.

Use Case: A scalable, secure quiz application for DevOps learning, accessible publicly via a custom domain.
Production Considerations:
High availability with multi-AZ RDS and EKS managed node groups.
Autoscaling for EKS nodes and pods.
Secure credential management with Secrets and OIDC.
Monitoring and logging for observability.
Automated deployments with Jenkins.

Directory Structure
The project is organized as follows, with all necessary files for the application, infrastructure, and CI/CD pipeline.
```

3-tier-app-eks/
├── backend/
│   ├── app.py                # Flask backend API
│   ├── requirements.txt      # Python dependencies
│   ├── questions-answers/    # Sample CSV files for quiz data
│   │   └── sample.csv
│   └── migrations/           # Database migration scripts
│       └── init.sql
├── frontend/
│   ├── src/
│   │   ├── App.js           # React frontend code
│   │   └── index.js
│   ├── package.json         # Node.js dependencies
│   └── Dockerfile           # Docker image for frontend
├── k8s/
│   ├── namespace.yaml       # Kubernetes namespace
│   ├── database-service.yaml # ExternalName service for RDS
│   ├── configmap.yaml       # ConfigMap for app configuration
│   ├── secrets.yaml         # Secrets for DB credentials
│   ├── migration_job.yaml   # Kubernetes job for DB migrations
│   ├── backend.yaml         # Backend deployment and service
│   ├── frontend.yaml        # Frontend deployment and service
│   └── ingress.yaml         # Ingress for ALB
├── terraform/
│   ├── main.tf             # Terraform configuration for VPC, EKS, RDS
│   ├── variables.tf        # Terraform variables
│   ├── outputs.tf          # Terraform outputs
│   └── iam.tf             # IAM roles and policies
├── Dockerfile              # Docker image for backend
├── Jenkinsfile             # Jenkins pipeline for CI/CD
└── README.md               # Project documentation

```
