# AWS Load Balanced Architecture Project

## Overview
This project implements a load-balanced architecture using AWS services including:

- EC2
- Application Load Balancer
- S3
- IAM
- Route 53
- Custom VPC

## Architecture

Two EC2 instances are deployed across different Availability Zones:

- Red instance (us-east-1a)
- Blue instance (us-east-1b)

Both instances retrieve website files from an S3 bucket using an IAM role.

## Networking Setup

Custom VPC configured with:

- Internet Gateway
- Public Subnets
- Route Table association

Security Groups allow:

- SSH (22) from my IP
- HTTP (80) from anywhere

## Load Balancer

Application Load Balancer configured with:

Path-based routing:

- `/red` → Red EC2
- `/blue` → Blue EC2

## Current Status

✔ EC2 instances deployed  
✔ Internet connectivity fixed  
✔ Apache running  
✔ S3 access working  
✔ Load balancer routing functioning  

Next Step:

Host-based routing using Route53.