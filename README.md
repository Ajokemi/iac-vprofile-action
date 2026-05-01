Project Phase 2: Infrastructure as Code & Cloud-Native Deployment
Overview
This phase represents the transition from local code validation to a production-ready cloud environment. It focuses on provisioning managed Kubernetes infrastructure on AWS (EKS), securing the CI/CD handshake via OIDC, and automating application orchestration using Helm.

Technical Stack
Cloud Provider: Amazon Web Services (AWS)

Infrastructure as Code: Terraform

Orchestration: Amazon EKS (Elastic Kubernetes Service)

Container Registry: Amazon ECR (Elastic Container Registry)

Package Management: Helm

CI/CD Orchestrator: GitHub Actions

Engineering Milestones & Troubleshooting
1. Infrastructure Provisioning (Terraform)
The deployment began with the automated provisioning of the EKS cluster and VPC networking.

Challenge: Initial synchronization issues during the terraform init phase and EKS cluster connectivity hurdles.

Solution: Systematically debugged the Terraform provider configurations and backend state management to ensure a stable foundation for the Kubernetes control plane.

2. Zero-Trust Security (OIDC)
To eliminate the security risks associated with long-lived IAM access keys, an OpenID Connect (OIDC) identity provider was implemented to allow GitHub Actions to assume roles dynamically.

Challenge: Encountered authentication rejections during the "AssumeRoleWithWebIdentity" handshake.

Solution: * Enabled id-token: write permissions within the GitHub Actions workflow.

Optimized the IAM Trust Policy using StringLike conditions and wildcards to ensure a seamless match between the GitHub identity and AWS IAM.

3. Pipeline Stabilization
To ensure a high success rate across the build and deploy jobs, the pipeline was hardened against environment variable instability.

Challenge: Inconsistent variable injection for AWS regions and ECR registry paths.

Solution: Standardized the workflow by hardcoding the target region (us-east-1) and defining explicit registry paths, ensuring the "Build, Tag, and Push" cycle was repeatable and failure-proof.

Deployment Workflow
Containerization: The application is packaged into a Docker image and pushed to Amazon ECR, using unique GitHub run numbers for version control.

Cluster Access: The pipeline dynamically updates the kubeconfig to establish a secure management context with the EKS cluster.

Helm Orchestration: Helm is used to deploy the vprofile stack, managing the deployment of Pods, ClusterIP Services, and the LoadBalancer Ingress.

Endpoint Exposure: Upon a successful deployment, the pipeline extracts the DNS name of the AWS Application Load Balancer to provide a live URL for the application.

Outcome
The project successfully moved from a manual setup to a fully automated, secure, and "Green" CI/CD pipeline. The final result is a scalable, cloud-native application architecture that can be redeployed or updated with a single code push.


# Prerequisites
#####
- JDK 11
- Maven 3
- MySQL 8 

# Technologies 
- Spring MVC
- Spring Security
- Spring Data JPA
- Maven
- JSP
- MySQL
# Database
Here,we used Mysql DB 
MSQL DB Installation Steps for Linux ubuntu 14.04:
- $ sudo apt-get update
- $ sudo apt-get install mysql-server

Then look for the file :
- /src/main/resources/db_backup.sql
- db_backup.sql file is a mysql dump file.we have to import this dump to mysql db server
- > mysql -u <user_name> -p accounts < db_backup.sql
