# Cloud Security – Capstone Project

## Objective
The objective of this project is to build a secure, scalable three-tier cloud architecture on AWS following cloud security best practices. The entire infrastructure is provisioned as code using Terraform.

## Architecture Overview
This project deploys a highly available and secure three-tier architecture:
1. **Presentation Tier (Public):** An Application Load Balancer (ALB) deployed in public subnets across two Availability Zones. It routes internet traffic securely to the application tier.
2. **Logic/Application Tier (Private):** EC2 application servers deployed in private subnets. They only accept traffic originating from the ALB.
3. **Data Tier (Private):** An Amazon RDS (MySQL) database deployed in a highly restricted private database subnet. It is completely isolated from the internet and only accepts connections from the Application tier.

## Key Security Configurations
* **Network Isolation:** Resources are strictly divided between public and private subnets using an Internet Gateway and NAT Gateway.
* **Least Privilege Access:** Security Groups are configured so that the database is not publicly accessible (only the App SG can access the DB SG, and only the ALB SG can access the App SG).
* **Security Monitoring:** 
  * **VPC Flow Logs** are enabled to capture IP traffic going to and from network interfaces in the VPC.
  * **AWS CloudTrail** is configured with an S3 bucket to log all API calls and console actions for auditing and security monitoring.

## Repository Contents
* `main.tf`: The complete Terraform configuration file to deploy the infrastructure.
* `architecture_diagram.png`: Visual representation of the AWS environment.
* `screenshots/`: Folder containing proof of deployment (VPC Resource Map, active ALB, active RDS, and CloudTrail dashboard).

## Deployment Instructions
To deploy this infrastructure using AWS CloudShell or your local terminal:

1. Initialize Terraform:
   ```bash
   terraform init
   ```
2. Review the deployment plan:
   ```bash
   terraform plan
   ```
3. Deploy the resources:
   ```bash
   terraform apply -auto-approve
   ```

## Cleanup
To prevent unnecessary AWS charges, destroy the infrastructure when testing is complete:
```bash
terraform destroy -auto-approve
```