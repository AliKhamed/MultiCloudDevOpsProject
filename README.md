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
├── Terraform
│   ├── backend.tf
│   ├── key-pair.tf
│   ├── main.tf
│   ├── modules
│   │   ├── cloudwatch
│   │   │   ├── main.tf
│   │   │   ├── output.tf
│   │   │   └── variables.tf
│   │   ├── ec2
│   │   │   ├── main.tf
│   │   │   ├── output.tf
│   │   │   └── variables.tf
│   │   └── network
│   │       ├── main.tf
│   │       ├── output.tf
│   │       └── variables.tf
│   ├── terraform.tfvars
│   └── variables.tf
├── Ansible
│   ├── ansible.cfg
│   ├── aws_ec2.yml
│   ├── playbook.yml
│   └── roles
│       ├── docker
│       │   ├── tasks
│       │   │   └── main.yml
│       │   └── vars
│       │       └── main.yml
│       ├── jenkins
│       │   ├── tasks
│       │   │   └── main.yml
│       │   └── vars
│       │       └── main.yml
│       ├── oc_cli
│       │   └── tasks
│       │       └── main.yml
│       └── sonarqube
│           ├── tasks
│           │   └── main.yml
│           └── vars
│               └── main.yml
├── Application
├── Jenkinsfile
├── oc
│   ├── deployment.yml
│   ├── route.yml
│   └── service.yml
├── shared_library
│   └── vars
│       ├── buildAndPushDockerImage.groovy
│       ├── build.groovy
│       ├── deployOnOc.groovy
│       ├── editNewImage.groovy
│       ├── runUnitTests.groovy
│       └── sonarQubeAnalysis.groovy
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
    ![](https://github.com/AliKhamed/MultiCloudDevOpsProject/tree/dev/screenshots/terrInit.png)

4. Review the Plan:

    ```
     terraform plan

    ```
    ![](https://github.com/AliKhamed/MultiCloudDevOpsProject/tree/dev/screenshots/terraPlan.png)

5. Apply the Configuration:

    ```
    terraform apply
    ```

    Confirm the action by typing yes when prompted.

    ![](https://github.com/AliKhamed/MultiCloudDevOpsProject/tree/dev/screenshots/terraApply.png)

6. AWS Resources Created:

    - EC2 Instances

        ![](https://github.com/AliKhamed/MultiCloudDevOpsProject/tree/dev/screenshots/ec2.png)

    - VPC

        ![](https://github.com/AliKhamed/MultiCloudDevOpsProject/tree/dev/screenshots/vpc2.png)

    - CloudWatch with SNS topic for email notifications

        ![](https://github.com/AliKhamed/MultiCloudDevOpsProject/tree/dev/screenshots/cloudwatch.png)
        ![](https://github.com/AliKhamed/MultiCloudDevOpsProject/tree/dev/screenshots/sns.png)
        ![](https://github.com/AliKhamed/MultiCloudDevOpsProject/tree/dev/screenshots/snsEmail.png)

    - S3 Bucket for Terraform state file backend

        ![](https://github.com/AliKhamed/MultiCloudDevOpsProject/tree/dev/screenshots/s3.png)
