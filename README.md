![Alt text](/Host_a_Static_Website_on_AWS (1).png)

# Host a Static Website on AWS

## Project Overview
This project involves hosting a static HTML web application on AWS, leveraging various AWS services to ensure scalability, security, and high availability. The project architecture includes a Virtual Private Cloud (VPC) with public and private subnets, an Application Load Balancer, Auto Scaling Groups, EC2 instances, and other networking components. The reference diagram and deployment scripts are available in the project's GitHub repository.

## AWS Infrastructure Components
1. **Virtual Private Cloud (VPC)**: Configured with both public and private subnets across two different Availability Zones.
2. **Internet Gateway**: Enables connectivity between the VPC instances and the wider Internet.
3. **Security Groups**: Act as a firewall to control inbound and outbound traffic.
4. **Multi-AZ Deployment**: Ensures system reliability and fault tolerance by utilizing two Availability Zones.
5. **Public Subnets**: Used for infrastructure components like the NAT Gateway and Application Load Balancer.
6. **EC2 Instance Connect Endpoint**: Provides secure connections to assets within public and private subnets.
7. **Private Subnets**: Web servers (EC2 instances) are deployed here to enhance security.
8. **NAT Gateway**: Allows instances in private subnets to access the Internet securely.
9. **EC2 Instances**: Used to host the static website.
10. **Application Load Balancer & Target Group**: Distributes web traffic evenly to an Auto Scaling Group of EC2 instances across multiple Availability Zones.
11. **Auto Scaling Group**: Automatically manages EC2 instances for high availability, scalability, and fault tolerance.
12. **GitHub Repository**: Stores web files for version control and collaboration.
13. **AWS Certificate Manager**: Secures application communications with SSL/TLS certificates.
14. **Simple Notification Service (SNS)**: Sends alerts for activities within the Auto Scaling Group.
15. **Route 53**: Manages domain name registration and DNS configuration.

## Deployment Script
The following Bash script automates the setup of an Apache web server on an EC2 instance and deploys the static website from GitHub:

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

## How to Use
1. Clone the project repository from GitHub:
   ```bash
   git clone https://github.com/aosnotes77/host-a-static-website-on-aws.git
   ```
2. Configure your AWS environment with the required VPC, subnets, security groups, and EC2 instances.
3. Execute the Bash script on the EC2 instance to install Apache and deploy the static website.
4. Ensure the Application Load Balancer is set up to distribute traffic across instances in the Auto Scaling Group.
5. Access the website via the configured domain name or public IP.

## Conclusion
This project demonstrates best practices for hosting a static website on AWS using EC2 instances and associated networking services. By leveraging automation and AWS scalability features, the deployment is efficient, secure, and highly available.
