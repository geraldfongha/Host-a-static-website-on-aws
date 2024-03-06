
# Host a Static Website on AWS

This project demonstrates the deployment of a static HTML web application on Amazon Web Services (AWS) using various resources and configurations. Below is an overview of the project setup and deployment process:

## Project Overview

The project utilizes the following AWS resources and configurations:

1. **Virtual Private Cloud (VPC)**:
   - Configured with both public and private subnets across two different availability zones for enhanced fault tolerance and reliability.

2. **Internet Gateway**:
   - Deployed to facilitate connectivity between VPC instances and the wider Internet.

3. **Security Groups**:
   - Implemented as a network firewall mechanism to control traffic to and from instances.

4. **Availability Zones**:
   - Leveraged two availability zones to enhance system reliability and fault tolerance.

5. **Subnets**:
   - Public subnets utilized for infrastructure components like the NAT Gateway and Application Load Balancer.
   - Private subnets used for positioning web servers (EC2 instances) for enhanced security.

6. **EC2 Instance Connect Endpoint**:
   - Implemented for secure connections to assets within both public and private subnets.

7. **NAT Gateway**:
   - Enabled instances in private subnets to access the Internet.

8. **Hosting the Website**:
   - The website is hosted on EC2 instances.

9. **Application Load Balancer (ALB)**:
   - Used for evenly distributing web traffic to an Auto Scaling Group of EC2 instances across multiple availability zones.

10. **Auto Scaling Group**:
    - Automatically manages EC2 instances to ensure website availability, scalability, fault tolerance, and elasticity.

11. **Version Control and Collaboration**:
    - Web files are stored on GitHub for version control and collaboration.

12. **Certificate Manager**:
    - Application communications are secured using a Certificate Manager.

13. **Simple Notification Service (SNS)**:
    - Configured to alert about activities within the Auto Scaling Group.

14. **Domain Name Registration**:
    - The domain name is registered and DNS records are set up using Route 53.

## Deployment Script

The following deployment script (`deploy.sh`) automates the setup and configuration of the web application:

```bash
#!/bin/bash
# Switch to the root user to gain full administrative privileges
sudo su
# Update all installed packages to their latest versions
yum update -y
# Install Apache HTTP Server
yum install -y httpd
# Change the current working directory to the Apache web root
cd /var/www/html
# Install Git
yum install git -y
# Clone the project GitHub repository to the current directory
git clone https://github.com/aosnotes77/host-a-static-website-on-aws.git
# Copy all files, including hidden ones, from the cloned repository to the Apache web root
cp -R host-a-static-website-on-aws/. /var/www/html/
# Remove the cloned repository directory to clean up unnecessary files
rm -rf host-a-static-website-on-aws
# Enable the Apache HTTP Server to start automatically at system boot
systemctl enable httpd
# Start the Apache HTTP Server to serve web content
systemctl start httpd
```

## Usage

To deploy the static website on AWS:

1. Run the `deploy.sh` script on an EC2 instance.
2. The script updates packages, installs Apache HTTP Server, clones the project repository, copies files to the web root, enables and starts the HTTP server.

## Author

This project was authored by [Gerald Fongha].



---
