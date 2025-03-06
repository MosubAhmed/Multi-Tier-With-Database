# Multi-Tier Application Deployment on AWS EKS

## Overview
This project deploys a multi-tier application on an AWS EKS (Elastic Kubernetes Service) cluster using Terraform and Kubernetes manifests. The application consists of a MySQL database and a Java Spring Boot backend.

## Project Structure
```
Multi-Tier-With-Database/
│-- terraform/            # Terraform configurations to provision AWS infrastructure
│   ├── main.tf           # Defines AWS EKS cluster and networking resources
│   ├── variables.tf      # Contains configurable variables for Terraform
│   ├── output.tf         # Outputs important resource details
│-- kubernetes/           # Kubernetes manifests for application deployment
│   ├── ds.yaml           # Deployment and Service for MySQL and Java App
│-- README.md             # Project documentation
```

## Infrastructure Setup with Terraform
### Prerequisites
- Terraform installed on your machine
- AWS CLI configured with the required permissions

### Steps to Provision Infrastructure
1. Navigate to the `terraform/` directory:
   ```sh
   cd terraform
   ```
2. Initialize Terraform:
   ```sh
   terraform init
   ```
3. Plan the deployment:
   ```sh
   terraform plan
   ```
4. Apply the configuration:
   ```sh
   terraform apply -auto-approve
   ```
5. Retrieve the EKS cluster details:
   ```sh
   terraform output
   ```

## Deploying the Application to EKS
### Prerequisites
- `kubectl` installed and configured to interact with your EKS cluster
- Docker installed for building and pushing images

### Steps
1. Connect `kubectl` to the EKS cluster:
   ```sh
   aws eks --region ap-south-1 update-kubeconfig --name devopsshack-cluster
   ```
2. Deploy the MySQL and Java Spring Boot application:
   ```sh
   kubectl apply -f kubernetes/ds.yaml -n webapps
   ```
3. Verify deployments:
   ```sh
   kubectl get pods -n webapps
   kubectl get services -n webapps
   ```

## Application Components
### MySQL Deployment
- Uses `mysql:8` image
- Exposes port `3306`
- Persistent database storage

### Java Spring Boot Deployment
- Uses a custom image `mosub/bankapp:latest`
- Connects to the MySQL service
- Exposes port `8080` via a LoadBalancer service

## Troubleshooting
1. If Terraform fails, check AWS credentials and permissions.
2. If Kubernetes deployment fails, ensure the `ds.yaml` file is correctly formatted.
3. Use the following command to debug pods:
   ```sh
   kubectl logs -f <pod-name> -n webapps
   ```

## Cleanup
To delete the AWS infrastructure:
```sh
cd terraform
terraform destroy -auto-approve
```

