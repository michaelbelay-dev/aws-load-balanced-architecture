# AWS Load Balanced Architecture with Advanced Request Routing

## Project Overview

This project demonstrates how to design and deploy a **highly available web architecture on AWS** using an **Application Load Balancer with advanced request routing**.

The environment includes two EC2 web servers deployed across separate Availability Zones, an S3 bucket for website assets, IAM roles for secure access, and routing rules configured to direct traffic based on URL paths and host headers.

This architecture demonstrates key **cloud engineering concepts such as high availability, scalability, and secure service integration**.

---

# Architecture Diagram

*(Add architecture diagram here later)*

Example components:

* Application Load Balancer
* EC2 Instances (Red / Blue)
* S3 Bucket
* IAM Role
* Route 53
* Internet Gateway
* Public Subnets across two Availability Zones

---

# AWS Services Used

| Service                   | Purpose                               |
| ------------------------- | ------------------------------------- |
| EC2                       | Hosts the web servers                 |
| S3                        | Stores website files                  |
| IAM                       | Provides secure access to S3          |
| Application Load Balancer | Distributes traffic between instances |
| Route 53                  | DNS routing for host-based routing    |
| VPC                       | Custom network configuration          |

---

# Infrastructure Setup

## VPC Configuration

Custom VPC configured with:

* Public subnets
* Internet Gateway
* Route Table association

Instances were configured with **public IP addresses** to allow internet access.

---

## Security Group Configuration

Security Group: `WebsiteSG`

| Type | Port | Source    |
| ---- | ---- | --------- |
| SSH  | 22   | My IP     |
| HTTP | 80   | 0.0.0.0/0 |

---

# EC2 Instances

Two web servers deployed across different Availability Zones:

| Instance | AZ         | Purpose                |
| -------- | ---------- | ---------------------- |
| Red      | us-east-1a | Serves `/red` website  |
| Blue     | us-east-1b | Serves `/blue` website |

User-data scripts automatically:

* Install Apache
* Retrieve website files from S3
* Deploy content to `/var/www/html`

---

# Load Balancer Configuration

Application Load Balancer:

Name:

```
LabLoadBalancer
```

Listener:

```
HTTP : 80
```

Two **Target Groups** were created:

| Target Group | Instance |
| ------------ | -------- |
| Red          | Red EC2  |
| Blue         | Blue EC2 |

---

# Path-Based Routing

The ALB routes requests based on URL paths.

| Path    | Destination   |
| ------- | ------------- |
| `/red`  | Red Instance  |
| `/blue` | Blue Instance |

Example requests:

```
http://ALB-DNS/red
http://ALB-DNS/blue
```

---

# Host-Based Routing (Next Step)

Traffic will also be routed based on subdomains.

Examples:

```
red.mydomain.com
blue.mydomain.com
```

Configured using **Route 53 DNS records** pointing to the Application Load Balancer.

---

# Troubleshooting & Lessons Learned

During deployment several issues were identified and resolved:

* Subnet was not associated with route table
* Instances initially lacked internet connectivity
* Elastic IPs were attached to enable external access
* IAM role permissions were required for S3 access

Resolving these issues ensured the **user-data scripts could retrieve website files and configure Apache automatically**.

---

# Project Status

Completed:

* VPC networking configuration
* S3 bucket setup
* IAM role configuration
* EC2 deployment
* Apache installation
* Application Load Balancer
* Path-based routing

In Progress:

* Host-based routing with Route 53

---

# Future Improvements

* HTTPS using AWS Certificate Manager
* Auto Scaling Group for dynamic scaling
* CI/CD pipeline for automated deployments
* Infrastructure as Code using Terraform

---

# Author

Cloud Engineering Project
AWS Architecture Lab
