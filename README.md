# 🌐 Static Website Hosting & Deployment on AWS with Custom Domain & HTTPS

## 🚀 Project Overview

This project demonstrates the end-to-end hosting and deployment of a static website on AWS using multiple integrated services — EC2 (Ubuntu + Nginx), Route 53, S3, CloudFront, and Certbot SSL for HTTPS.

The website is accessible globally over HTTPS, mapped with a custom domain purchased from a hosting provider, and optimized for performance using AWS CloudFront CDN.
Additionally, static assets (like images) are served securely from Amazon S3.

----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

# 🧱 Architecture Diagram

----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

# 🧩 Steps Performed

## 1️⃣ 🏠 Purchase Domain from Hosting Provider

  1) Purchased the domain cloudtechlearner.online from a hosting provider (Hostinger).
  2) The same hosting provider was used to manage the domain DNS, which was later mapped to AWS Route 53.
  3) This ensures seamless domain-to-AWS linkage for website hosting.

----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

## 2️⃣ Launch EC2 Instance (Ubuntu Server)

  1) Created an EC2 instance in AWS with Ubuntu Linux.
  2) Configured the Security Group to allow inbound ports:
     A) 22 (SSH)
     B) 80 (HTTP)
     C) 443 (HTTPS)
  3) Connected to the instance using MobaXterm / SSH.

----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

## 3️⃣ Install and Configure Nginx

    sudo apt update
    sudo apt install nginx -y
    sudo systemctl enable nginx
    sudo systemctl start nginx

  1) Uploaded the website files (index.html, style.css, etc.) to /var/www/html/.
  2) Verified the site was accessible via the EC2 public IP address.

----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

## 4️⃣ Create DNS Records in Route 53

  1) Created a Hosted Zone in AWS Route 53 for the domain cloudtechlearner.online.
  2) Added:
     A) A Record → Points to the EC2 Elastic IP address.
     B) CNAME Record → For www.cloudtechlearner.online, redirecting to the main domain.

----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

## 5️⃣ Update Domain Records in Hostinger Panel

  1) Logged into the Hostinger DNS settings (where the domain was purchased).
  2) Added the A and CNAME records from Route 53 into the Hostinger DNS management section.
  3) Waited for DNS propagation to complete and verified domain linkage to AWS.

#### ✅ Result: The purchased domain now correctly routes traffic to the AWS EC2-hosted website.

----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

## 6️⃣ Configure SSL with Certbot (HTTPS Setup)

  1) Installed and configured Certbot (Let’s Encrypt) to enable HTTPS:

    sudo apt install certbot python3-certbot-nginx -y
    sudo certbot --nginx -d cloudtechlearner.online -d www.cloudtechlearner.online

  2) Verified HTTPS redirection (🔒 Secure Padlock).
  3) Enabled automatic SSL renewal:

         sudo certbot renew --dry-run

----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

## 7️⃣ 🪣 Configure S3 Bucket for Static Assets

  1) Created an S3 bucket named staticwebsitehosting1782.
  2) Uploaded all images and static assets (CSS, JS).
  3) Integrated the bucket securely with CloudFront to restrict public access.

----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

## 📜🔐 Secure S3 Bucket Policy for CloudFront Access

  The following policy allows only CloudFront to access objects from the S3 bucket securely — preventing any direct public S3 access.
         
     {
       "Version": "2012-10-17",
       "Statement": [
    {
      "Sid": "AllowCloudFrontServicePrincipalReadOnly",
      "Effect": "Allow",
      "Principal": {
        "Service": "cloudfront.amazonaws.com"
      },
      "Action": "s3:GetObject",
      "Resource": "arn:aws:s3:::staticwebsitehosting1782/*",
      "Condition": {
        "StringEquals": {
          "AWS:SourceArn": "arn:aws:cloudfront::<YOUR_ACCOUNT_ID>:distribution/d21kzhuzagmye9"
             }
           }
        }
      ]
    }

----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

# 🧠 Explanation

----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

<img width="698" height="123" alt="image" src="https://github.com/user-attachments/assets/e15c602e-5862-44a2-a746-be900ee17914" />

----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

#### ✅ Advantage: Your S3 bucket stays private — only your CloudFront distribution can serve its content globally.

----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

## 8️⃣ 🌍 Setup CloudFront (Global CDN)

   1) Created a CloudFront Distribution with:
      A) EC2 Origin → Main website served via Nginx.
      B) S3 Origin → Static files and images.
   2) Configured:
      A) Redirect HTTP → HTTPS
      B) Managed-CachingOptimized policy
      C) Custom SSL certificate (ACM / Certbot)

#### ✅ CloudFront improves global performance, caching, and secure content delivery.

----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

## 9️⃣ 🧪 Testing and Validation

#### ✅ Verified: 
   1) https://cloudtechlearner.online loads the website securely.
   2) https://www.cloudtechlearner.online redirects correctly.
   3) SSL is active 🔒.
   4) Images load through S3 + CloudFront.
   5) DNS propagation and routing work as expected.

----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

# 🧰 Tools & Services Used

----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

<img width="556" height="219" alt="image" src="https://github.com/user-attachments/assets/76266fec-80cd-4eaf-a31f-740639192dc2" />

----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

# 🏁 Final Output

#### ✅ Static Website Hosted & Deployed Successfully
#### 🌍 Domain: https://cloudtechlearner.online
#### 🔒 HTTPS Secured with SSL
#### 🚀 Accelerated via CloudFront CDN
#### 📦 S3 Assets Protected via CloudFront Policy
#### 🌐 Domain Purchased & Linked via Hostinger + Route 53

----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

# ✨ Optional Future Enhancements

  1) Integrate CloudWatch for monitoring.
  2) Set up CI/CD with GitHub Actions or CodePipeline.
  3) Enable Auto Scaling and Load Balancer (ALB) for high availability.
  4) Add AWS Backup or EBS Snapshots for recovery.

----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

# 🎯 Project Outcome Summary

<img width="387" height="252" alt="image" src="https://github.com/user-attachments/assets/6ffa399a-892b-41ea-a049-13ee447f50a2" />

----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

Museum of Candy Video.mp4

----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

# 🎉 Thank You!

### ✨ Thank you for exploring this project!
This deployment marks the successful completion of my Static Website Hosting on AWS — powered by Ubuntu, Nginx, Route 53, S3, CloudFront, and SSL (Certbot).

It demonstrates real-world cloud implementation, including domain mapping, DNS configuration, HTTPS security, and global content delivery — all integrated into a seamless,       production-ready architecture.

### 🌍 Through this project, I gained hands-on experience in web hosting, domain management, and SSL encryption, further strengthening my AWS cloud engineering skills.

### 💡 Continuous learning never stops — new projects are on the way! 🚀

----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
