# Cab Management Application - AFour's Hackathon

The Cab Management Application is a cloud-based solution that allows users to manage drivers, cabs, and their assignments. It provides an easy-to-use interface for creating, updating, and deleting driver and cab records, as well as assigning drivers to cabs. The application is built using Express.js, Sequelize ORM, and MySQL database.

## Features

The Cab Management Application offers the following features:

- **Driver Management:**

  - Add a new driver with details such as name, ID number, email, and phone number.
  - Update existing driver information.
  - Delete a driver from the database.

- **Cab Management:**

  - Add a new cab with details such as registration number, model, and color.
  - Update existing cab information.
  - Delete a cab from the database.

- **Cab Assignment:**
  - Assign a driver to a specific cab.
  - Update the assigned driver for a cab.
  - Remove the driver assignment from a cab.

## Architecture

![Workflow Diagram](./artifacts/architecture/Afourathon%20Architecture.jpeg)

## Figma Link for the frontend design
https://www.figma.com/file/fD3GXSJ5nAumySx7MFFwRp/Afourathon?type=design&node-id=0%3A1&mode=design&t=gDZU9NjmIiO2Zv2Y-1

## Future Scope
1.	Multiple owner support: This will support multiple owners at the same time and have their own drivers and cabs data.
2.	Google Map integration: Live tracking of the cab.
3.	Infrastructure Automation: Cloud infrastructure automation using GitOps Workflow or ArgoCD
4.	Driver Portal: Driver Portal to register themselves to different Cab Agencies

## Prerequisites

Before running the application, make sure you have the following installed:

- Nodejs [Reactjs,expressjs]
- MySQL database (For, Test,Dev and Prod)
- Terraform
- AWS CLI
- AWS SDK
- Github Account (CI)
- AWS Credentials- Admin (CD)

## Installation

1. Clone the repository:

   ```shell
   git clone https://github.com/your-username/cab-management-app.git
   ```
2. Go to the respective applications and install the dependencies:

   ```shell
   cd backend/cab-app
   npm install
   ```
   Do the same for driver app and cab-assignment app
   
3. Install Dependancies for frontend
   ```shell
   cd frontend/
   npm install
   ```
4. create .env files in root directory of each backend app and frontend app
   .env for backend
    DB_USER=""
    DB_PASSWORD=""
    DATABASE=""
    DB_HOST=""
    DB_PORT=""
    JWT_SECRET=""
    OWNER_EMAIL=""
    OWNER_PASSWORD=""
    AWS_ACCESS_KEY_ID=""
    AWS_SECRET_ACCESS_KEY=""
    AWS_REGION=""
    S3_BUCKET_NAME_CAB=""

   .env for frontend
    REACT_APP_AWS_ACCESS_KEY_ID=
    REACT_APP_AWS_SECRET_ACCESS_KEY=
    REACT_APP_AWS_REGION=
    REACT_APP_S3_BUCKET_NAME="afourathon3images"
    REACT_APP_CAB_APP="http://localhost:4000"
    REACT_APP_DRIVER_APP="http://localhost:5000"
    REACT_APP_CAB_ASSIGNMENT_APP="http://localhost:7000"
   
5. To run the application run following command on each app's root directory
   ```shell
    npm start
   ```
6. To run the tests for backend applications go to root directory of app and run
   ```shell
    npm test
   ```
   
# AWS Infrastructure Deployment

This repository contains the Terraform configuration files to deploy an AWS infrastructure that includes an RDS MySQL database, ECS services, IAM Policies, VPC, and Cloud Map services. Follow the instructions below to deploy the infrastructure.

## Prerequisites

Before you can deploy the AWS infrastructure using Terraform, make sure you have the following prerequisites:

- Terraform installed on your local machine.
- AWS account credentials configured on your machine.

## Configuration

To configure the deployment, follow the steps below:

Clone this repository to your local machine.

Open the main.tf file and replace the following variables with your own values:

```bash
var.vpc_id # The ID of your existing VPC where the infrastructure will be deployed.
var.db_name # The desired name for the RDS MySQL database.
var.username # The username for the RDS MySQL database.
var.password # The password for the RDS MySQL database.
```

Also replace the CIDR ranges as per your VPC subnets.
Save the main.tf file.

## Deployment

To deploy the AWS infrastructure, follow the steps below:

Open a terminal or command prompt.

Navigate to the directory where the repository was cloned.
Go to Terraform folder where you main.tf located
Run the following commands:

```bash
terraform init
terraform plan
terraform apply
```

Review the execution plan generated by Terraform and confirm the deployment by entering yes when prompted.

The deployment process may take a few minutes to complete. Once finished, you will see the output indicating the resources that were created.

## Cleanup

To destroy the deployed AWS infrastructure and remove all associated resources, follow the steps below:

Open a terminal or command prompt.

Navigate to the directory where the repository was cloned.
Go to Terraform folder where you main.tf located

Run the following command:

```shell
terraform destroy
```

Review the execution plan generated by Terraform and confirm the destruction by entering yes when prompted.

Note that this will permanently delete all the resources created during the deployment process.

# GitHub Workflow Usage

This repository contains GitHub workflow files for deploying the Cab, Driver, Cab Assignment, and Web apps to AWS ECS Fargate. Each workflow file corresponds to a specific app deployment. Follow the instructions below to use the GitHub workflows.

## Prerequisites

Before you can use the GitHub workflows, make sure you have the following prerequisites:

- An AWS account with the necessary permissions to deploy and manage ECS services.
- Docker images for each app stored in an ECR repository.
- AWS access key ID and secret access key with appropriate permissions. You can store these credentials as GitHub secrets.

## Workflow Configuration

To configure the GitHub workflows, follow the steps below:

1. Clone this repository to your local machine.
2. Open the workflow file for the app you want to deploy (e.g., `cab-app.yaml`).
3. Review the workflow file and make any necessary modifications based on your specific deployment requirements.
4. Save the workflow file.

## Workflow Usage

To trigger the GitHub workflow and deploy the app to AWS ECS Fargate, follow the steps below:

1. Push your changes to the `prod` branch of the repository. The workflow is configured to trigger on pushes to the `prod` branch.
2. Open the Actions tab in your GitHub repository to monitor the progress of the workflow.
3. The workflow will perform the following steps:

   - Checkout the repository.
   - Configure AWS credentials using the provided secrets.
   - Log in to Amazon ECR.
   - Build and push the Docker image for the app.
   - Deploy the app to AWS ECS Fargate.

4. Monitor the workflow logs for any errors or failures.

## Cleanup

The GitHub workflows are designed to trigger deployments automatically on pushes to the `prod` branch. If you want to stop the automatic deployments, follow the steps below:

1. Open the workflow file for the app you want to disable (e.g., `cab-app.yaml`).
2. Comment out or remove the `on` section under the `name` field.
3. Save the workflow file.

This will prevent the workflow from triggering on subsequent pushes to the `prod` branch.

Note: Make sure to disable or modify the workflows for each app if you no longer want to deploy them automatically.

## Additional Workflows

Repeat the above steps for each app's workflow file (`driver-app.yaml`, `cab-assignment-app.yaml`, `web-app.yaml`) to deploy the respective apps to AWS ECS Fargate.
