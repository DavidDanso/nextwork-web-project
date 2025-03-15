Here's your README in proper markdown format:

# Java Web App on EC2

A Java web application built with Amazon Corretto and deployed on an AWS EC2 instance.

## Overview

This project demonstrates the deployment of a Java web application on AWS EC2 using Amazon Corretto as the JDK. The entire deployment process is managed through AWS services with remote development via VSCode's SSH capabilities.

## Tech Stack

- Amazon Corretto JDK
- Java web framework
- AWS EC2 instance
- VSCode with Remote SSH extension
- AWS services for infrastructure

## Setup Instructions

### Prerequisites

- AWS account with appropriate permissions
- Visual Studio Code with Remote SSH extension
- SSH key pair for EC2 access
- Basic knowledge of AWS services

### EC2 Instance Setup

1. Launch an EC2 instance from the AWS Console
   - Select an Amazon Linux 2 AMI
   - Choose your preferred instance type
   - Configure security groups to allow HTTP/HTTPS and SSH traffic
   - Launch with your SSH key pair

2. Connect to your instance using VSCode
   - Open VSCode
   - Install Remote SSH extension if not already installed
   - Click on the Remote Explorer icon in the sidebar
   - Configure SSH target with your EC2 instance details:
     ```
     Host ec2-instance
       HostName ec2-xx-xx-xx-xx.compute-1.amazonaws.com
       User ec2-user
       IdentityFile ~/.ssh/your-key-pair.pem
     ```
   - Connect to the remote host

### Installing Amazon Corretto

On your EC2 instance via VSCode terminal:

```bash
# Update system packages
sudo yum update -y

# Install Amazon Corretto
sudo amazon-linux-extras enable corretto8
sudo yum install -y java-1.8.0-amazon-corretto-devel

# Verify installation
java -version
```

### Deploying the Application

1. Upload your application code using VSCode
   - Open your remote folder in VSCode
   - Drag and drop files or use Git to clone your repository

2. Build and run your Java application
   ```bash
   # If using Maven
   ./mvnw clean package
   java -jar target/your-application.jar

   # If using Gradle
   ./gradlew build
   java -jar build/libs/your-application.jar
   ```

## Configuration

- Configure your application to run on port 8080 (or your preferred port)
- Make sure EC2 security groups allow traffic on the application port
- Set up environment variables as needed

## Maintenance Tips

- Create an AMI of your configured instance for backup
- Consider setting up a load balancer for high availability
- Use AWS CloudWatch for monitoring your application
- Implement regular security patching

## Troubleshooting

- Check EC2 instance logs: `/var/log/`
- Verify security group configurations if unable to connect
- Ensure Java process is running: `ps -ef | grep java`
