# Deploying a Production Static Website on AWS EC2 with Nginx and HTTPS

One of the most fundamental skills in Cloud and DevOps is knowing how to take a website off your local machine and put it on real cloud infrastructure securely, reliably and publicly accessible. This project documents exactly that.

I deployed a static website on AWS EC2 running Ubuntu 22.04, configured Nginx as the web server, secured SSH access, and set up HTTPS using Let's Encrypt. Here is the full walkthrough.

---

## Architecture

```
User
  ↓
Internet
  ↓
AWS Security Group
  ↓
EC2 Instance (Ubuntu 22.04)
  ↓
Nginx
  ↓
Static Website
```

---

## Tech Stack

| Component | Technology |
|-----------|-----------|
| Cloud Platform | AWS EC2 |
| Operating System | Ubuntu 22.04 LTS |
| Web Server | Nginx |
| SSL Certificate | Let's Encrypt |
| Access Control | AWS Security Groups |
| Version Control | Git — feature-branch workflow |

---

## EC2 Instance Configuration

| Setting | Value |
|---------|-------|
| AMI | Ubuntu 22.04 LTS |
| Instance Type | t2.micro |
| Network | Default VPC |
| Public IP | Enabled |

### Security Group Rules

| Port | Protocol | Source | Purpose |
|------|----------|--------|---------|
| 22 | SSH | My IP only | Secure remote access |
| 80 | HTTP | 0.0.0.0/0 | Public web traffic |
| 443 | HTTPS | 0.0.0.0/0 | Secure web traffic |

Restricting SSH to my own IP address rather than opening it to the world is a small but important security decision. It significantly reduces the attack surface on the instance.

---

## Deployment Walkthrough

### 1. Connect to the EC2 Instance

```bash
ssh -i your-key.pem ubuntu@your-ec2-public-ip
```

### 2. Update the Server

Always start with a system update to ensure the latest security patches are applied before doing anything else.

```bash
sudo apt update
sudo apt upgrade -y
```

### 3. Install Nginx

```bash
sudo apt install nginx -y
sudo systemctl status nginx
```

Once installed, Nginx starts automatically and serves a default page on port 80. Verify it is active before proceeding.

### 4. Deploy the Website

Remove the default Nginx page and replace it with your own:

```bash
sudo rm /var/www/html/index.nginx-debian.html
sudo nano /var/www/html/index.html
```

Your website is now live and accessible via the EC2 public IP over HTTP.

### 5. Configure HTTPS with Let's Encrypt

Install Certbot and obtain a free SSL certificate:

```bash
sudo apt install certbot python3-certbot-nginx -y
sudo certbot --nginx -d yourdomain.com
```

Certbot automatically updates the Nginx configuration to redirect HTTP traffic to HTTPS and handles certificate renewal.

---

## Git Workflow

This project follows a feature-branch workflow:

- `main` branch holds the stable, production-ready state
- Feature branches are used for each implementation stage
- Changes are merged into `main` only after validation

This is the same workflow used in professional engineering teams and is a habit worth building from the start.

---

## Challenges I Ran Into

**SSH permission errors** — Connecting to EC2 via SSH requires the key pair file to have strict permissions. Running `chmod 400 your-key.pem` before connecting is easy to miss the first time and produces a confusing error if skipped.

**Nginx not serving the custom page** — After replacing the default HTML file, Nginx needed to be reloaded to pick up the changes. A reminder that configuration changes are not always instant and verifying service status after every change is a good habit.

**Security group misconfiguration** — Initially had port 80 closed in the security group which meant the server was running perfectly but the browser could not reach it at all. Understanding that AWS Security Groups are a separate network layer from the server itself is a key cloud concept.

---

## What I Learned

- How AWS Security Groups act as a firewall layer controlling inbound and outbound traffic
- How to securely connect to EC2 instances using SSH key pairs
- How Nginx serves static files and how to configure it as a web server
- Why keeping server packages updated matters for security in production
- How Let's Encrypt provides free SSL certificates and why HTTPS is non-negotiable in production
- The importance of restricting SSH access to known IP addresses

---

## What Is Coming Next

- Custom domain integration
- Automated deployment pipeline with GitHub Actions
- CloudFront CDN for improved performance and global distribution
- S3 static hosting as an alternative architecture

---

## Author

**Grace Kihonge** — Cloud & DevOps Engineer based in Nairobi, Kenya.
Transitioning from IT Customer Support into Cloud & DevOps, building real infrastructure and documenting everything publicly.

[![LinkedIn](https://img.shields.io/badge/LinkedIn-0A66C2?style=for-the-badge&logo=linkedin&logoColor=white)](https://www.linkedin.com/in/grace-kihonge-1354a9310/)
[![GitHub](https://img.shields.io/badge/GitHub-181717?style=for-the-badge&logo=github&logoColor=white)](https://github.com/Grace4549)
