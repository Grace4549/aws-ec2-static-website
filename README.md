# Deploy Static Website on Ubuntu EC2

## Project Overview
This project demonstrates how to deploy a production-ready static website on AWS EC2 using Ubuntu 22.04 and Nginx. The website is publicly accessible via HTTP and deployed following cloud security best practices.

---

## Technologies Used
- AWS EC2
- Ubuntu 22.04 LTS
- Nginx
- AWS Security Groups
- Linux CLI
- Git (feature-branch workflow)

---

## Architecture

User → Internet → AWS Security Group → EC2 (Ubuntu) → Nginx → Static Website

---

## Git Workflow

This project follows a feature-branch workflow:

- `main` branch stores the stable project state.
- Feature branches are used for each implementation stage.
- Changes are merged into `main` after validation.

---

## Implementation Steps

### 1. EC2 Instance Setup

#### Instance Configuration
- Name: grace-static-web-server
- AMI: Ubuntu 22.04 LTS
- Instance Type: t2.micro
- Network: Default VPC
- Public IP: Enabled

#### Security Group Configuration
- SSH (22): Restricted to my IP address
- HTTP (80): Open to the internet
- HTTPS (443): Reserved for future SSL implementation

#### Key Pair
An RSA key pair was generated to enable secure SSH authentication to the EC2 instance.

---

### 2. Server Setup & Configuration

#### System Updates

The server packages were updated using:

```bash
sudo apt update
sudo apt upgrade -y
```

This ensured the system had the latest security patches and updates.

---

#### Nginx Installation

Nginx was installed as the web server:

```bash
sudo apt install nginx -y
```

Service status was verified using:

```bash
sudo systemctl status nginx
```

The service was confirmed active and running.

---

### 3. Website Deployment

The default Nginx page was removed:

```bash
sudo rm /var/www/html/index.nginx-debian.html
```

A custom static website was created:

```bash
sudo nano /var/www/html/index.html
```

The website is now accessible via the EC2 public IP over HTTP.

---

## Current Deployment Status

- EC2 instance is running.
- Nginx is installed and active.
- Custom static website is deployed.
- Website is accessible via HTTP.
- HTTPS has not yet been implemented.

---

## Challenges Faced

- Managing SSH access permissions securely.

---

## Lessons Learned

- How AWS Security Groups control inbound traffic.
- How to securely connect to EC2 using SSH keys.
- How Nginx serves static files from `/var/www/html`.
- Importance of keeping server packages updated.
- Importance of restricting SSH access for security.

---

## Repository Name

aws-ec2-static-website
