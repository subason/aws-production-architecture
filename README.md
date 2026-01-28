# AWS Production Architecture – Scalable & Secure Web Application

## 📌 Project Overview

This project demonstrates a **production-ready AWS architecture** designed for a highly available, scalable, and secure web application. It reflects **real-world enterprise practices** expected from a **3+ years experienced AWS / DevOps engineer**.

The architecture uses **AWS-managed services**, follows **Well-Architected Framework principles**, and is suitable for real production workloads.

---

## 🏗️ Architecture Summary

**Services Used:**

* Amazon VPC
* EC2 (Auto Scaling Group)
* Application Load Balancer (ALB)
* Amazon RDS (Multi-AZ)
* Amazon S3
* Amazon CloudFront
* Amazon Route 53
* AWS Certificate Manager (ACM)

**Key Design Goals:**

* High Availability (Multi-AZ)
* Scalability (Auto Scaling)
* Security (Private subnets, SGs, HTTPS)
* Performance (CloudFront caching)
* Cost Optimization

---

## 🖼️ Architecture Diagram

![AWS Architecture](architecture/aws-architecture.png)

---

## 🌐 Traffic Flow

1. User accesses application via custom domain
2. Route 53 resolves DNS
3. HTTPS traffic terminates at ALB using ACM certificate
4. ALB forwards traffic to EC2 instances in Auto Scaling Group
5. Application connects securely to RDS in private subnet
6. Static content served via CloudFront from S3

---

## 🧱 Network Design (VPC)

* VPC CIDR: `10.0.0.0/16`
* Public Subnets:

  * Application Load Balancer
  * NAT Gateway
* Private Subnets:

  * EC2 Auto Scaling Group
  * RDS (Multi-AZ)

🔐 **No resources are publicly exposed except ALB**

---

## ⚙️ Compute Layer

* EC2 instances launched via **Launch Template**
* Auto Scaling Group:

  * Min: 2
  * Max: 4
* Health checks via ALB

---

## 🗄️ Database Layer

* Amazon RDS (MySQL / PostgreSQL)
* Multi-AZ enabled
* Automated backups enabled
* Accessible only from EC2 Security Group

---

## 📦 Static Content Layer

* Amazon S3 for static assets
* CloudFront distribution with:

  * Origin Access Control (OAC)
  * HTTPS enabled
  * Global edge caching

---

## 🔐 Security Best Practices

* IAM roles for EC2 (no hardcoded credentials)
* Least privilege access
* Security Groups layered access
* HTTPS enforced using ACM
* Private subnets for backend resources

---

## 💰 Cost Optimization

* Auto Scaling based on demand
* CloudFront caching reduces ALB load
* S3 lifecycle policies (optional)
* Right-sized EC2 instances

---

## 🚀 Future Enhancements

* Infrastructure as Code using Terraform
* CI/CD pipeline using Jenkins or GitHub Actions
* Monitoring with CloudWatch & SNS
* Containerization using Docker & ECR
* Kubernetes (EKS)

---

## 🎯 Interview Talking Points

* Why ALB instead of NLB
* How Auto Scaling handles traffic spikes
* How ACM enables HTTPS
* How CloudFront improves performance
* Security Group vs NACL usage

---

## 🧑‍💻 Author

**Subason V**
AWS / DevOps Engineer

---

> ⚠️ Note: This project uses dummy values and does not expose any sensitive credentials.
