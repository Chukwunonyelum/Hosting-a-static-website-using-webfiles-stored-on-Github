# Host an HTML Website on an EC2 Instance Using GitHub Repository

This project demonstrates how to host an HTML website on an EC2 instance by downloading web files from a public GitHub repository. The setup involves configuring an EC2 instance in the default VPC, installing necessary software, and using a Bash script added to the EC2 user data at launch to automate the deployment process.

## Project Overview

### Steps to Host the Website

1. **Download the Web Files**:
   - Download the web file from the provided link: [mole.zip](https://aosnote-assignments.s3.amazonaws.com/assignment-1/mole.zip).
   - Extract the contents of the `mole.zip` file and upload the extracted files to a public GitHub repository in your account.

2. **Create and Launch the EC2 Instance**:
   - Launch an EC2 instance in the default VPC and configure the instance with a security group that allows HTTP access on port 80.
   - Add the provided script (detailed below) to the EC2 instance user data at launch to automate the website deployment.

## Script for EC2 User Data

The following script is used to configure the EC2 instance to host the HTML website by downloading the web files from your GitHub repository:

```bash
#!/bin/bash
# Update the instance
yum update -y

# Install Apache Web Server
yum install -y httpd

# Start the Apache Web Server
systemctl start httpd
systemctl enable httpd

# Navigate to the web server root directory
cd /var/www/html

# Install Git to clone the GitHub repository
yum install -y git

# Download the website files from the public GitHub repository 
git clone https://github.com/Chukwunonyelum/Hosting-a-static-website-using-webfiles-stored-on-Github.git


# Set correct permissions
chmod -R 755 /var/www/html/

# Restart the web server
systemctl restart httpd
```

### Instructions:
- Replace `your-username` and `your-repository` with your GitHub username and repository name.
- Add this script to the EC2 instance user data when configuring the instance.

## Detailed Deployment Steps

1. **Upload Web Files to GitHub**:
   - Create a new public repository on your GitHub account.
   - Upload the contents of the `mole.zip` file (extracted files) to this repository.

2. **Launch EC2 Instance**:
   - Go to the AWS EC2 console and click "Launch Instance."
   - Choose the Amazon Linux 2 AMI (or another compatible Linux distribution).
   - Select an instance type (e.g., t2.micro for free tier eligibility).
   - Configure the instance with default VPC settings, ensuring the security group allows inbound HTTP (port 80) traffic.
   - Under "Advanced Details," paste the user data script provided above.
   - Review and launch the instance.

3. **Access the Website**:
   - Once the instance is running, obtain its public IP address or public DNS name.
   - Open a web browser and navigate to `http://<instance-public-ip>` to view the hosted HTML website.

