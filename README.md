![Alt text](/Host_a_Static_Website_on_AWS.png)
---

# Static Website Hosting on AWS

## Overview

This project demonstrates how to host a static HTML web app on AWS, leveraging various AWS services to ensure scalability, reliability, and security. The architecture includes a Virtual Private Cloud (VPC) with public and private subnets, an Internet Gateway, Security Groups, EC2 instances, an Application Load Balancer, Auto Scaling, and more. The web files are version controlled and stored on GitHub.

## Architecture

![Architecture Diagram](link-to-your-diagram.png)

### Key Components

1. **VPC Configuration**: A VPC with both public and private subnets across two availability zones.
2. **Internet Gateway**: Facilitates connectivity between VPC instances and the Internet.
3. **Security Groups**: Act as a network firewall for controlling traffic.
4. **Availability Zones**: Enhance system reliability and fault tolerance.
5. **Public Subnets**: Host infrastructure components like the NAT Gateway and Application Load Balancer.
6. **EC2 Instance Connect Endpoint**: Allows secure connections to assets within both public and private subnets.
7. **Private Subnets**: Host web servers (EC2 instances) for enhanced security.
8. **NAT Gateway**: Enables instances in private subnets to access the Internet.
9. **EC2 Instances**: Host the static website.
10. **Application Load Balancer**: Distributes web traffic to an Auto Scaling Group of EC2 instances.
11. **Auto Scaling Group**: Manages EC2 instances automatically for availability, scalability, fault tolerance, and elasticity.
12. **GitHub**: Stores web files for version control and collaboration.
13. **Certificate Manager**: Secures application communications.
14. **Simple Notification Service (SNS)**: Alerts about activities within the Auto Scaling Group.
15. **Route 53**: Registers the domain name and sets up DNS records.

## Deployment Steps

### Prerequisites

- AWS Account
- GitHub Account
- Domain name registered on Route 53

### Steps

1. **VPC and Subnets Configuration**
   - Create a VPC with public and private subnets across two availability zones.
   - Deploy an Internet Gateway and attach it to the VPC.
   - Create and configure Security Groups for the necessary traffic.

2. **NAT Gateway and Application Load Balancer**
   - Deploy the NAT Gateway in the public subnet.
   - Configure the Application Load Balancer in the public subnets.

3. **EC2 Instances and Auto Scaling**
   - Launch EC2 instances in the private subnets.
   - Configure an Auto Scaling Group to manage the instances.
   - Secure connections using the EC2 Instance Connect Endpoint.

4. **DNS and SSL/TLS**
   - Register your domain name using Route 53 and set up DNS records.
   - Use AWS Certificate Manager to secure communications with SSL/TLS.

5. **Notification Setup**
   - Configure SNS to receive alerts about Auto Scaling Group activities.

### Script to Deploy Web App

Use the following bash script to deploy your static web app on an EC2 instance:

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

### Final Steps

1. **Start the Instances**: Ensure all EC2 instances are up and running.
2. **Access the Website**: Navigate to your domain name to see the deployed static website.

## Conclusion

This project showcases how to host a static website on AWS using various services to ensure a highly available, scalable, and secure web application. The architecture diagram and deployment scripts are provided to help replicate the setup.

For more details, refer to the project repository on GitHub: [GitHub Repository](https://github.com/aosnotes77/host-a-static-website-on-aws)

---

Feel free to adjust the details, particularly the link to the architecture diagram, based on your specific setup and preferences.
