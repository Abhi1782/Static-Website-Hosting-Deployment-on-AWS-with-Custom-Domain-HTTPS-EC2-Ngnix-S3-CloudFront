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

<img width="1920" height="964" alt="Screenshot (511)" src="https://github.com/user-attachments/assets/c38755d8-0133-4e0f-82ed-ebcfa79c3352" />

----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

## 2️⃣ Launch EC2 Instance (Ubuntu Server)

  1) Created an EC2 instance in AWS with Ubuntu Linux.
  2) Configured the Security Group to allow inbound ports:
     A) 22 (SSH)
     B) 80 (HTTP)
     C) 443 (HTTPS)
  3) Connected to the instance using MobaXterm / SSH.

----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

<img width="1920" height="1030" alt="Screenshot (475)" src="https://github.com/user-attachments/assets/4eb13ce8-f4ca-4ddc-b47a-167623be604a" />

----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

## 3️⃣ Install and Configure Nginx

    sudo apt update
    sudo apt install nginx -y
    sudo systemctl enable nginx
    sudo systemctl start nginx

  1) Uploaded the website files (index.html, style.css, etc.) to /var/www/html/.
  2) Verified the site was accessible via the EC2 public IP address.

----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

<img width="1920" height="1022" alt="Screenshot (476)" src="https://github.com/user-attachments/assets/505ffd5e-e967-4bcb-8b64-b7861bb1f5ae" />

----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

<img width="1920" height="1019" alt="Screenshot (477)" src="https://github.com/user-attachments/assets/6a3c1a86-7488-40bf-acea-ee88c3a52e60" />

----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

## 4️⃣ Create DNS Records in Route 53

  1) Created a Hosted Zone in AWS Route 53 for the domain cloudtechlearner.online.
  2) Added:
     A) A Record → Points to the EC2 Elastic IP address.
     B) CNAME Record → For www.cloudtechlearner.online, redirecting to the main domain.

----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

<img width="1920" height="1023" alt="Screenshot (479)" src="https://github.com/user-attachments/assets/bf0f0185-407b-4521-aac4-cf71d1a6e0d1" />

----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

<img width="1920" height="1080" alt="Screenshot (480)" src="https://github.com/user-attachments/assets/ec1e9801-4c24-40d6-94d6-de8e564879c0" />

----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

<img width="1920" height="1080" alt="Screenshot (481)" src="https://github.com/user-attachments/assets/deb0e13f-be0c-4a3f-91a1-3e2c21fae851" />

----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

<img width="1920" height="1080" alt="Screenshot (482)" src="https://github.com/user-attachments/assets/f9b69c18-a090-4a70-a529-acb62d176593" />

----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

<img width="1920" height="1080" alt="Screenshot (483)" src="https://github.com/user-attachments/assets/e6a3af2f-4407-429c-9df0-660146afc43f" />

----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

## 5️⃣ Update Domain Records in Hostinger Panel

  1) Logged into the Hostinger DNS settings (where the domain was purchased).
  2) Added the A and CNAME records from Route 53 into the Hostinger DNS management section.
  3) Waited for DNS propagation to complete and verified domain linkage to AWS.

#### ✅ Result: The purchased domain now correctly routes traffic to the AWS EC2-hosted website.

----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

<img width="1920" height="1080" alt="Screenshot (485)" src="https://github.com/user-attachments/assets/70f1f6fb-265a-4ac4-98f4-b176318a89d0" />

----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

## 6️⃣ Configure SSL with Certbot (HTTPS Setup)

  1) Installed and configured Certbot (Let’s Encrypt) to enable HTTPS:

    sudo apt install certbot python3-certbot-nginx -y
    sudo certbot --nginx -d cloudtechlearner.online -d www.cloudtechlearner.online

  2) Verified HTTPS redirection (🔒 Secure Padlock).
  3) Enabled automatic SSL renewal:

         sudo certbot renew --dry-run

----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------



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

<img width="599" height="219" alt="image" src="https://github.com/user-attachments/assets/679237f6-71a4-484c-98ea-4456b1c74a40" />

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

<img width="467" height="243" alt="image" src="https://github.com/user-attachments/assets/dff51dfe-af1e-4925-8af3-edafca0b0a99" />

----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

https://github.com/user-attachments/assets/23831b16-e396-4294-82a3-772f9a7849f7

----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

# 🎉 Thank You!

### ✨ Thank you for exploring this project!
This deployment marks the successful completion of my Static Website Hosting on AWS — powered by Ubuntu, Nginx, Route 53, S3, CloudFront, and SSL (Certbot).

It demonstrates real-world cloud implementation, including domain mapping, DNS configuration, HTTPS security, and global content delivery — all integrated into a seamless,       production-ready architecture.

### 🌍 Through this project, I gained hands-on experience in web hosting, domain management, and SSL encryption, further strengthening my AWS cloud engineering skills.

### 💡 Continuous learning never stops — new projects are on the way! 🚀

----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
