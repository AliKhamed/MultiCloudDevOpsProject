# Multi Cloud DevOps Project

This project demonstrates a complete CI/CD pipeline setup for a Java application using Terraform, Ansible, Jenkins, SonarQube, and OpenShift. The pipeline begins with infrastructure provisioning on AWS using Terraform, followed by configuration management and application deployment using Ansible, Jenkins, SonarQube and Deploy on OpenShift Cluster.

## Table of Contents

- [Prerequisites](#prerequisites)
- [Project Structure](#project-structure)
- [Terraform Setup](#terraform-setup)
- [Ansible Setup](#ansible-setup)
- [Jenkins Configuration](#jenkins-configuration)
- [Running the Pipeline](#running-the-pipeline)
- [Checking Results](#checking-results)
- [Contributing](#contributing)


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

1. **Clone the Repository:**

    ```
    git clone <repository-url>
    cd <repository-directory>/terraform

    ```
2. **Configure Variables:**

    Edit the terraform.tfvars file to set values for your AWS setup.

3. **Initialize Terraform:**

    ```
    terraform init

    ```
    ![](https://github.com/AliKhamed/MultiCloudDevOpsProject/blob/dev/screenshots/terrInit.png)

4. **Review the Plan:**

    ```
     terraform plan

    ```
    ![](https://github.com/AliKhamed/MultiCloudDevOpsProject/blob/dev/screenshots/terraPlan.png)

5. **Apply the Configuration:**

    ```
    terraform apply
    ```

    Confirm the action by typing yes when prompted.

    ![](https://github.com/AliKhamed/MultiCloudDevOpsProject/blob/dev/screenshots/terraApply.png)

6. **AWS Resources Created:**

    - EC2 Instances

        ![](https://github.com/AliKhamed/MultiCloudDevOpsProject/blob/dev/screenshots/ec2.png)

    - VPC

        ![](https://github.com/AliKhamed/MultiCloudDevOpsProject/blob/dev/screenshots/vpc2.png)

    - CloudWatch with SNS topic for email notifications

        ![](https://github.com/AliKhamed/MultiCloudDevOpsProject/blob/dev/screenshots/cloudwatch.png)
        ![](https://github.com/AliKhamed/MultiCloudDevOpsProject/blob/dev/screenshots/sns.png)
        ![](https://github.com/AliKhamed/MultiCloudDevOpsProject/blob/dev/screenshots/snsEmail.png)

    - S3 Bucket for Terraform state file backend

        ![](https://github.com/AliKhamed/MultiCloudDevOpsProject/blob/dev/screenshots/s3.png)


## Ansible Setup

1. **Navigate to Ansible Directory:**
    ```
    cd ../Ansible

    ```
2. **Install Jenkins, SonarQube, Docker, and OC CLI:**

    Use Ansible roles to install the necessary services.

3. **Dynamic Inventory:**

    Use the aws_ec2 plugin for dynamic inventory.

4. **Generate Private Key:**

    Terraform will generate private_key.pem and add it to the Ansible folder.

5. **Run Ansible Playbook:**

    ```
    ansible-playbook -i aws_ec2.yml playbook.yml

    ```
    ![](https://github.com/AliKhamed/MultiCloudDevOpsProject/blob/dev/screenshots/ansibleApply.png)
    

6. **Outputs:**

- SonarQube token

    ![](https://github.com/AliKhamed/MultiCloudDevOpsProject/blob/dev/screenshots/sonarToken1.png)

- Jenkins initial password

    ![](https://github.com/AliKhamed/MultiCloudDevOpsProject/blob/dev/screenshots/jenkinsPass.png)


## Jenkins Configuration

1. **Install Plugins:**
        Suggested plugins
        SonarQube Scanner
        Groovy Plugins

2. **Create Credentials:**
        GitHub token
        SonarQube token
        OpenShift token
        DockerHub token

3. **Configure Shared Library:**

4. **Add repository URL and name in Jenkins system configuration:**

5. **Create Pipeline:**
        Create a new pipeline.
        Choose SCM and add repository URL and branch name.

## Running the Pipeline

    Run Pipeline:

    Execute the pipeline from Jenkins.

    Monitor Pipeline:

    Ensure the pipeline runs successfully.

## Checking Results

    SonarQube Quality Gate:

    Review code quality reports on SonarQube.

    Application Deployment:

    Verify your application is running on the OpenShift cluster.

## Contributing

    Contributions are welcome! Please submit a pull request or open an issue for any suggestions or improvements.