# Deploy Static Website on Ubuntu EC2 with HTTPS

## Project Overview
This project demonstrates how to deploy a production-ready static website on AWS EC2 using Ubuntu and Nginx, secured with Let's Encrypt SSL.

## Technologies Used
- AWS EC2
- Ubuntu 22.04
- Nginx
- Security Groups
- Let's Encrypt
- Linux CLI

## Architecture

User → Internet → AWS Security Group → EC2 (Ubuntu) → Nginx → Static Website

## Git Workflow

This project follows a feature-branch workflow:
- main branch stores stable project state
- feature branches are used for each implementation stage.

## Implementation Steps

### 1. EC2 Instance Setup

#### Instance Configuration
- Name: grace-static-web-server
- AMI: Ubuntu 22.04 LTS
- Instance Type: t2.micro
- Network: Default VPC
- Public IP: Enabled

#### Security Group Configuration
- SSH (22): Restricted to My IP
- HTTP (80): Open to internet
- HTTPS (443): Open to internet

#### Key Pair
An RSA key pair was generated to enable secure SSH authentication.

## Why These Decisions?

- Ubuntu chosen for stability and community support.
- t3.micro sufficient for lightweight static workload.
- SSH restricted to personal IP for security best practice.
- HTTP/HTTPS open to allow public web traffic.

### Nginx Service Verification

The Nginx service was verified using:

```bash
sudo systemctl status nginx  

## Challenges Faced (To Be Added)

## Lessons Learned (To Be Added)# aws-ec2-static-website
Production-ready static website deployed on AWS EC2 (Ubuntu) with Nginx and HTTPS via Let's Encrypt.
