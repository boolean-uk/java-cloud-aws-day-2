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
   - Choose an Amazon Machine Image (AMI), such as Amazon Linux 3 Server.
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
   - Install necessary dependencies to run a Spring Application ie Java:
   ```bash
   sudo yum install java-21-amazon-corretto
   ```

3. **Deploy Your Backend Application:**
   - Use `scp` or another file transfer method to upload your backend application files to the EC2 instance:
   ```bash
   scp -i "your-key.pem" NameOfFile.jar ec2-user@your-ec2-public-ip:/home/ec2-user/
   ```
   - Login to the server using ssh again
     
   - Start the application using the appropriate commands (for JAVA):
   ```bash
   java -jar NameOfFile.jar &
   ```

## Investigate Connecting to an RDS Database

1. Once you are able to connect to a Neon Database using your EC2 instance, investigate whether you can make it talk to an existing RDS database via a public conneection as we did in the previous session.
2. If you are able to achieve this then investigate connecting to a dedicated RDS instance using the same VPS as the EC3 instance is connected to.

You will need to delete existing databases at this point, as you should never have more than 1 RDS database in existence at once (this is our rule not an AWS rule and is purely to minimise the costs). Ensure that any databases you do create are t3.micro or we will delete them without warning.
  

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
