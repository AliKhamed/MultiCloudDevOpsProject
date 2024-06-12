# Terraform and Ansible on AWS to Java Application Cycle

This project demonstrates a complete CI/CD pipeline setup for a Java application using Terraform, Ansible, Jenkins, SonarQube, and OpenShift. The pipeline begins with infrastructure provisioning on AWS using Terraform, followed by configuration management and application deployment using Ansible, Jenkins, and SonarQube.

## Table of Contents

- [Prerequisites](#prerequisites)
- [Project Structure](#project-structure)
- [Terraform Setup](#terraform-setup)
- [Ansible Setup](#ansible-setup)
- [Jenkins Configuration](#jenkins-configuration)
- [Running the Pipeline](#running-the-pipeline)
- [Checking Results](#checking-results)
- [Contributing](#contributing)
- [License](#license)

## Prerequisites

- AWS Account
- Terraform installed
- Ansible installed
- GitHub Account
- OpenShift Cluster
- DockerHub Account

## Project Structure

```
├── Application
├── oc
├── shared_library
├── terraform
│   ├── main.tf
│   ├── variables.tf
|   ├── terraform.tfvars
│   ├── backend.tf
│   ├── key-pair.tf
│   ├── modules
│   │   ├── ec2
│   │   ├── network
│   │   └── cloudwatch
├── ansible
│   ├── playbook.yml
│   ├── roles
│   │   ├── jenkins
│   │   ├── sonarqube
│   │   ├── docker
│   │   └── oc_cli
│   └── inventory_aws_ec2.yml
├── Jenkinsfile
└── README.md
```
## Terraform Setup

1. Clone the Repository:

```
git clone <repository-url>
cd <repository-directory>/terraform

```
2. Configure Variables:

    Edit the terraform.tfvars file to set values for your AWS setup.

3. Initialize Terraform:

    ```
    terraform init
    ```
4. Review the Plan:

    ```
     terraform plan
    ```
5. Apply the Configuration:

    ```
    terraform apply
    ```
    Confirm the action by typing yes when prompted.

6. AWS Resources Created:

    - EC2 Instances
    - VPC
    - CloudWatch with SNS topic for email notifications
    - S3 Bucket for Terraform state file backend