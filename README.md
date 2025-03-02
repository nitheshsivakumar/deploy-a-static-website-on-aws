
---

# **Deploy a Static Website on AWS**  

This project demonstrates how to deploy a static HTML web application on AWS using an EC2 instance. It includes infrastructure setup, security configurations, and scalability features.

## **Architecture Overview**  

The website is hosted on an **EC2 instance** and follows best practices for security, availability, and scalability. The following AWS services are utilized:  

### **Infrastructure Setup**  
- Configured a **Virtual Private Cloud (VPC)** with public and private subnets across two **Availability Zones**.  
- Deployed an **Internet Gateway** for connectivity between the VPC and the Internet.  
- Created **Security Groups** to regulate inbound and outbound traffic.  

### **Compute & Networking**  
- Placed **web servers (EC2 instances)** in private subnets for enhanced security.  
- Allowed private instances to access the Internet via a **NAT Gateway**.  
- Implemented an **Application Load Balancer (ALB)** to distribute traffic among instances in an **Auto Scaling Group**.  
- Configured an **Auto Scaling Group** for high availability, ensuring elasticity and fault tolerance.  

### **Security & Monitoring**  
- Used **AWS Certificate Manager** to secure communication via HTTPS.  
- Configured **Simple Notification Service (SNS)** for Auto Scaling Group alerts.  

### **Domain Management**  
- Registered a **domain name** and set up a **DNS record in Route 53**.  

---

## **Deployment Instructions**  

### **Step 1: Setup an EC2 Instance**  
1. Launch an Amazon **EC2 instance** using Amazon Linux.  
2. Ensure that ports **80 (HTTP)** and **443 (HTTPS)** are open in the **Security Group**.  
3. Connect to the instance using SSH.  

### **Step 2: Install and Configure Apache**  
Run the following script to install the required packages and deploy the website:

```bash
#!/bin/bash

# Switch to root user
sudo su

# Update installed packages
yum update -y

# Install Apache HTTP Server
yum install -y httpd

# Change to Apache web root
cd /var/www/html

# Install Git
yum install git -y

# Clone the project repository
git clone https://github.com/nitheshsivakumar/deploy-a-static-website-on-aws.git

# Copy all files to the Apache web root
cp -R deploy-a-static-website-on-aws/. /var/www/html/

# Remove the cloned repository
rm -rf deploy-a-static-website-on-aws

# Enable Apache to start on boot
systemctl enable httpd  

# Start Apache service
systemctl start httpd
```

### **Step 3: Configure Load Balancer & Auto Scaling**  
1. Create an **Application Load Balancer** and attach it to a **Target Group**.  
2. Set up an **Auto Scaling Group** with EC2 instances in multiple **Availability Zones**.  
3. Define a scaling policy to automatically adjust capacity based on traffic.  

### **Step 4: Register a Domain & Configure Route 53**  
1. Register a **domain name** on AWS Route 53.  
2. Create an **A Record** pointing to the **ALB**.  

---

## **Key Features**  
✅ Highly Available & Scalable Infrastructure  
✅ Secure Deployment with HTTPS (AWS Certificate Manager)  
✅ Automated Deployment via GitHub  
✅ Auto Scaling & Load Balancing  
✅ Domain Management using AWS Route 53  

This project follows **AWS best practices** for **hosting static websites**, leveraging **EC2, Auto Scaling, Load Balancing, and Route 53** for a robust, scalable, and secure architecture.

---
