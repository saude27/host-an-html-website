# DevOps Project: Hosting an HTML Website on AWS

This project demonstrates hosting a static HTML website on an EC2 instance using AWS services. The deployment leverages a straightforward setup with default AWS configurations and automation scripts. Below are the details of the implementation and instructions to reproduce the setup.

## Project Overview
The website is hosted on an EC2 instance using the following AWS resources:

1. **Default Virtual Private Cloud (VPC):** The default VPC was used for networking.
2. **Default Security Group:** Provided basic firewall rules.
3. **Default Subnet:** Hosted resources within the default subnet.
4. **EC2 Instances:** Acted as the web server to host the HTML website.

---

## Deployment Instructions

### Prerequisites
- AWS account with permissions to create and manage resources.
- GitHub repository or S3 bucket containing website files.
- AWS CLI installed and configured.

### Deployment Options
You can choose between two methods to deploy the website:

#### **Option 1: GitHub Repository**

Use this script to clone your website files from a GitHub repository:

```bash
#!/bin/bash

# Update the package index
yum update -y

# Install Apache HTTP Server
yum install -y httpd

# Navigate to the web server root directory
cd /var/www/html

# Install Git
yum install git -y

# Clone the GitHub repository
git clone https://github.com/saude27/host-an-html-website.git

# Copy files to the web server directory
cp -R host-an-html-website/. /var/www/html/

# Clean up temporary files
rm -rf host-an-html-website

# Enable and start Apache HTTP Server
systemctl enable httpd
systemctl start httpd
```

#### **Option 2: S3 Bucket**

Use this script to copy website files from an S3 bucket:

```bash
#!/bin/bash

# Run commands as the superuser
sudo su

# Update the package index
yum update -y

# Install Apache HTTP Server
yum install -y httpd

# Copy website files from the S3 bucket
aws s3 cp s3://saudat-html-website-hosting-bucket /var/www/html/ --recursive

# Enable and start Apache HTTP Server
systemctl enable httpd
systemctl start httpd
```

---

## Repository

The project’s reference diagram, deployment scripts, and website files are hosted in the GitHub repository: [https://github.com/saude27/host-an-html-website](https://github.com/saude27/host-an-html-website).

---

## Key Features
- **Simple Setup:** Utilizes default AWS configurations for ease of deployment.
- **Automation:** Bash scripts streamline the process of setting up and hosting the website.
- **Scalability:** Can be integrated with Auto Scaling Groups and Load Balancers for future scalability.

---

## Conclusion
This project provides a basic yet effective method of hosting an HTML website on AWS EC2 instances. By leveraging either a GitHub repository or an S3 bucket for the website files, you can quickly deploy a secure and functional web application.

