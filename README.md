# 🌐 Static Website Hosting & Deployment on AWS with Custom Domain & HTTPS

## 🚀 Project Overview

This project demonstrates the end-to-end hosting and deployment of a static website on AWS using multiple integrated services — EC2 (Ubuntu + Nginx), Route 53, S3, CloudFront, and Certbot SSL for HTTPS.

The website is accessible globally over HTTPS, mapped with a custom domain purchased from a hosting provider, and optimized for performance using AWS CloudFront CDN.
Additionally, static assets (like images) are served securely from Amazon S3.

-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

# 🧱 Architecture Diagram

-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

# 🧩 Steps Performed

## 1️⃣ 🏠 Purchase Domain from Hosting Provider

  1) Purchased the domain cloudtechlearner.online from a hosting provider (Hostinger).
  2) The same hosting provider was used to manage the domain DNS, which was later mapped to AWS Route 53.
  3) This ensures seamless domain-to-AWS linkage for website hosting.

## 2️⃣ Launch EC2 Instance (Ubuntu Server)

  1) Created an EC2 instance in AWS with Ubuntu Linux.
  2) Configured the Security Group to allow inbound ports:
     A) 22 (SSH)
     B) 80 (HTTP)
     C) 443 (HTTPS)
  3) Connected to the instance using MobaXterm / SSH.

## 3️⃣ Install and Configure Nginx

    sudo apt update
    sudo apt install nginx -y
    sudo systemctl enable nginx
    sudo systemctl start nginx

  1) Uploaded the website files (index.html, style.css, etc.) to /var/www/html/.
  2) Verified the site was accessible via the EC2 public IP address.

## 4️⃣ Create DNS Records in Route 53

  1) Created a Hosted Zone in AWS Route 53 for the domain cloudtechlearner.online.
  2) Added:
     A) A Record → Points to the EC2 Elastic IP address.
     B) CNAME Record → For www.cloudtechlearner.online, redirecting to the main domain.

## 5️⃣ Update Domain Records in Hostinger Panel

  1) Logged into the Hostinger DNS settings (where the domain was purchased).
  2) Added the A and CNAME records from Route 53 into the Hostinger DNS management section.
  3) Waited for DNS propagation to complete and verified domain linkage to AWS.
### ✅ Result: The purchased domain now correctly routes traffic to the AWS EC2-hosted website.
