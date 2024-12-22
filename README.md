![Alt text](/Host-a-static-website.jpg)

# Host a Static Website on AWS

## Project Overview
This project demonstrates how to host a static HTML web application on AWS using a variety of cloud services to ensure high availability, scalability, and security. The project’s infrastructure was provisioned with best practices for fault tolerance and performance.

The reference diagram and deployment scripts are available in the [GitHub repository](https://github.com/aosnotes77/host-a-static-website-on-aws).

---

## Architecture Components

### 1. Virtual Private Cloud (VPC)
- Configured a VPC with public and private subnets across two different Availability Zones (AZs) to ensure fault tolerance and availability.

### 2. Internet Gateway
- Deployed an Internet Gateway to enable communication between VPC resources and the Internet.

### 3. Security Groups
- Established Security Groups as a network firewall mechanism to control inbound and outbound traffic.

### 4. Availability Zones
- Utilized two AZs to distribute resources and provide redundancy.

### 5. Public Subnets
- Used for infrastructure components such as the NAT Gateway and Application Load Balancer (ALB).

### 6. Private Subnets
- Positioned web servers (EC2 instances) in private subnets for enhanced security.

### 7. EC2 Instance Connect Endpoint
- Implemented for secure connections to assets in both public and private subnets.

### 8. NAT Gateway
- Enabled instances in private subnets to access the Internet securely.

### 9. EC2 Instances
- Hosted the static website on EC2 instances configured within the private subnets.

### 10. Application Load Balancer (ALB)
- Used an ALB and a target group to evenly distribute traffic across an Auto Scaling Group of EC2 instances.

### 11. Auto Scaling Group
- Automatically managed the EC2 instances, ensuring availability, scalability, fault tolerance, and elasticity.

### 12. GitHub Repository
- Stored web files in a GitHub repository for version control and collaboration.

### 13. Certificate Manager
- Secured application communications using SSL/TLS certificates.

### 14. Simple Notification Service (SNS)
- Configured SNS to send alerts about activities within the Auto Scaling Group.

### 15. Route 53
- Registered a domain name and set up DNS records to direct traffic to the Application Load Balancer.

---

## Deployment Steps

### Bash Script for EC2 Instance Configuration
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

---

## How to Use

1. Clone the [GitHub repository](https://github.com/aosnotes77/host-a-static-website-on-aws).
2. Deploy the infrastructure using the provided reference diagram and scripts.
3. Execute the Bash script above on the EC2 instances to configure the web server and deploy the static web application.
4. Access the website using the domain name configured in Route 53.

---

## Features
- **Scalability:** Auto Scaling ensures the website can handle increased traffic.
- **High Availability:** Resources are distributed across two Availability Zones.
- **Security:** Private subnets and Security Groups protect the web application.
- **Monitoring:** SNS alerts keep track of Auto Scaling Group activities.

---

---
