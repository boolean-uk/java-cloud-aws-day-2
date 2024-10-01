# Java Cloud AWS - Day Two

## Learning Objectives

- Understand how to set up an EC2 instance to host a backend application
- Learn basic networking and create a VPC, including setting up an API Gateway to expose endpoints
- Introduction to AWS Identity and Access Management (IAM) and policies

## Instructions

1. Fork this repository.
2. Clone your fork to your machine.

# Core Activity

## Set Up Amazon EC2 for Backend Application
### Steps

1. **Create an EC2 Instance:**
   - Open the AWS Management Console and navigate to the EC2 service.
   - Click "Launch Instance."
   - Choose an Amazon Machine Image (AMI), such as Amazon Linux 2 or Ubuntu Server.
   - Select an instance type (e.g., t2.micro for free-tier).
   - Configure instance details, ensuring that it’s deployed into the correct VPC and subnet.
   - Add storage if necessary, or proceed with default settings.
   - Configure security group settings to allow HTTP, HTTPS, and SSH access.
   - Click "Launch" and select or create a new key pair to access the instance.
   
2. **Connect to the EC2 Instance:**
   - After the instance is running, click "Connect."
   - Use the provided SSH command to access the instance from your terminal:
   ```bash
   ssh -i "your-key.pem" ec2-user@your-ec2-public-ip
   ```
   - Install necessary dependencies (e.g., .NET SDK, Nginx, or any other server you require for your backend).

3. **Deploy Your Backend Application:**
   - Use `scp` or another file transfer method to upload your backend application files to the EC2 instance:
   ```bash
   scp -i "your-key.pem" MyApi.zip ec2-user@your-ec2-public-ip:/home/ec2-user/
   ```
   - SSH into the instance and extract your backend files:
   ```bash
   unzip MyApi.zip
   ```
   - Start the application using the appropriate commands (for JAVA):
   ```bash
   TODO:JAVA COMMAND TO BE ADDED
   ```

## Set Up Networking: VPC and API Gateway
### Steps
1. Create a Virtual Private Cloud (VPC):
   - In the AWS Management Console, navigate to the VPC service.
   - Click "Create VPC."
   - Choose "VPC only" and configure the CIDR block (e.g., `10.0.0.0/16`).
   - Create subnets within your VPC for different availability zones.

2. Configure Route Table and Internet Gateway:
   - Create and attach an Internet Gateway to your VPC to allow internet access.
   - In the Route Tables section, add routes that direct traffic to the Internet Gateway for public subnets.

3. Create and Configure API Gateway:
   - Navigate to the API Gateway service.
   - Click "Create API" and select "REST API."
   - Define an API name and create an HTTP method (e.g., GET, POST) that corresponds to your backend application.
   - Set the integration type as "HTTP" or "Lambda Function," depending on your application.
   - For "HTTP" integration, use the public IP or domain of your EC2 instance as the endpoint.

4. Test the API Gateway:
   - Once configured, test the API Gateway by sending HTTP requests to the API Gateway's URL.
   - Ensure that it forwards requests correctly to your EC2-hosted backend.

## Introduction to IAM and Policies
### Steps
1. Understand IAM Basics:
   - IAM (Identity and Access Management) allows you to control access to AWS resources.
   - Navigate to the IAM service in the AWS Management Console.
   - Click on "Users" and create a new user (e.g., Developer).

2. Assign Policies to Users:
   - Attach policies to your new user based on their role (e.g., `AmazonEC2FullAccess` for managing EC2, or `AmazonS3ReadOnlyAccess` for read access to S3).
   - You can create custom policies if needed by defining specific permissions in JSON format.

3. Create and Use IAM Roles:
   - Create an IAM role that your EC2 instance can assume to access other AWS resources (e.g., access to S3, RDS).
   - Navigate to the "Roles" section and create a new role.
   - Attach appropriate policies (e.g., `AmazonS3FullAccess`) to this role.
   - Assign the IAM role to your EC2 instance from the "Actions" menu under "Instance Settings."