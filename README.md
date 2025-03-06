# Multi-Tier Application with CI/CD Pipeline

This project demonstrates a **multi-tier application** deployed on AWS using **Terraform** for infrastructure provisioning and **Jenkins** for CI/CD automation. The application is deployed to an **Amazon EKS cluster**, and the pipeline includes steps for building, testing, security scanning, and deployment.

---

## **Table of Contents**
1. [Project Overview](#project-overview)
2. [Infrastructure Setup](#infrastructure-setup)
3. [CI/CD Pipeline](#cicd-pipeline)
4. [Prerequisites](#prerequisites)
5. [How to Use](#how-to-use)
6. [Outputs](#outputs)
7. [Contributing](#contributing)
8. [License](#license)

---

## **Project Overview**
This project includes:
- **Terraform code** to provision AWS infrastructure:
  - VPC, Subnets, Internet Gateway, Route Tables, and Security Groups.
  - Amazon EKS cluster with a managed node group.
- **Jenkins pipeline** for CI/CD:
  - Code checkout, compilation, testing, and security scanning.
  - Docker image build and push to Docker Hub.
  - Deployment to the EKS cluster.

---

## **Infrastructure Setup**
The infrastructure is provisioned using Terraform. The following resources are created:
- **VPC**: `10.0.0.0/16` with 2 public subnets.
- **EKS Cluster**: A Kubernetes cluster with a managed node group.
- **Security Groups**: For the EKS cluster and worker nodes.
- **IAM Roles**: For EKS cluster and node group permissions.

### **Terraform Files**
- `main.tf`: Defines the AWS resources.
- `variables.tf`: Contains input variables (e.g., SSH key name).
- `outputs.tf`: Outputs the IDs of the created resources.

---

## **CI/CD Pipeline**
The Jenkins pipeline automates the following steps:
1. **Git Checkout**: Clones the repository.
2. **Compile**: Compiles the Maven project.
3. **Testing**: Runs unit tests.
4. **Trivy FS Scan**: Scans the filesystem for vulnerabilities.
5. **SonarQube Analysis**: Performs static code analysis.
6. **Build**: Packages the application into a JAR/WAR file.
7. **Publish to Nexus**: Deploys the artifact to a Nexus repository.
8. **Docker Build**: Builds a Docker image for the application.
9. **Trivy Image Scan**: Scans the Docker image for vulnerabilities.
10. **Docker Push**: Pushes the Docker image to Docker Hub.
11. **Deploy to K8s**: Deploys the application to the EKS cluster.
12. **Verify Deployment**: Checks the status of Pods and Services.

---

## **Prerequisites**
Before using this project, ensure you have the following:
1. **AWS Account**: With sufficient permissions to create VPC, EKS, and IAM resources.
2. **Terraform**: Installed on your local machine.
3. **Jenkins**: Installed and configured with the necessary plugins (e.g., Docker, Kubernetes, Maven).
4. **Docker Hub Account**: For pushing Docker images.
5. **Nexus Repository**: For storing Maven artifacts.
6. **SonarQube Server**: For static code analysis.
7. **SSH Key Pair**: For accessing EKS worker nodes.

---

## **How to Use**

### **1. Provision Infrastructure with Terraform**
1. Clone the repository:
   ```bash
   git clone https://github.com/your-username/your-repo.git
   cd your-repo
Initialize Terraform:

bash
Copy
terraform init
Apply the Terraform configuration:

bash
Copy
terraform apply
Provide the required variables (e.g., ssh_key_name).

After provisioning, Terraform will output the EKS cluster ID, node group ID, VPC ID, and subnet IDs.

2. Configure Jenkins
Set up the following credentials in Jenkins:

Docker Hub: For pushing Docker images.

Kubernetes Token: For deploying to the EKS cluster.

Nexus Credentials: For publishing Maven artifacts.

Configure the Jenkins pipeline to use the correct tools (e.g., Maven, Docker, SonarQube scanner).

3. Run the Pipeline
Trigger the Jenkins pipeline manually or via a Git webhook.

Monitor the pipeline stages in the Jenkins dashboard.

Outputs
After running terraform apply, the following outputs will be displayed:

Cluster ID: The ID of the EKS cluster.

Node Group ID: The ID of the EKS node group.

VPC ID: The ID of the VPC.

Subnet IDs: The IDs of the subnets.

Contributing
Contributions are welcome! Please follow these steps:

Fork the repository.

Create a new branch for your feature or bugfix.

Submit a pull request with a detailed description of your changes.

License
This project is licensed under the MIT License. See the LICENSE file for details.

Acknowledgments
Terraform for infrastructure as code.

Jenkins for CI/CD automation.

Amazon EKS for managed Kubernetes.
