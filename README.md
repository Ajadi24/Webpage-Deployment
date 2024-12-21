# AWS EC2 Instance Provisioning, HTML Deployment, and HTTPS Configuration

This project demonstrates how to provision an AWS EC2 instance, set up a web server, deploy an HTML page, and configure HTTPS using a custom domain name to obtain a free SSL certificate.

## Table of Contents
1. [Overview](#overview)
2. [Prerequisites](#prerequisites)
3. [Steps](#steps)
   i. [Provision EC2 Instance on AWS](#provision-ec2-instance-on-aws)
   ii. [Web Server Setup](#web-server-setup)
   iii. [Deploy the HTML Page](#deploy-the-html-page)
   iv. [Configure HTTPS (Let’s Encrypt)](#configure-https-lets-encrypt)
   v. [Verify the HTTPS Setup](#verify-the-https-setup)
4. [Contact](#contact)

## Overview
This project provides a step-by-step guide to:
1. Provision an AWS EC2 instance.
2. Set up a web server.
3. Deploy a static HTML page to the instance.
4. Configure a domain with HTTPS for secure access.

### Technologies Used:
1. AWS EC2
2. Apache (Web Server)
3. Certbot (SSL Certificate Configuration)

## Prerequisites
Before starting, ensure you have the following:
1. An AWS account.
2. A registered domain name.
3. SSH client (e.g., PuTTY, terminal).
4. Basic understanding of Linux commands.

## Steps

### 1. Provision EC2 Instance on AWS
- Log in to the AWS Management Console.
- Navigate to the EC2 Dashboard and launch a new instance.
- Select Ubuntu as the Amazon Machine Image.
- Choose an appropriate instance type (e.g., t2.micro for free tier).
- Configure security groups:
  - Allow inbound rules for HTTP (port 80) and HTTPS (port 443).
- Launch the instance and download the key pair for SSH access.
- On the terminal, change permissions for the key pair to prevent public access using:
  ```bash
  sudo chmod 400 "server002_key.pem"
  ```

### 2. Web Server Setup

#### i. SSH into the EC2 instance
```bash
ssh -i "server002_key.pem" ubuntu@ec2-35-180-226-52.eu-west-3.compute.amazonaws.com
```

#### ii. Install the web server (Apache):
```bash
sudo apt update && sudo apt upgrade
sudo apt install apache2 -y
```

#### iii. Start the web server and enable it on boot:
```bash
sudo systemctl start apache2
sudo systemctl enable apache2
```

### 3. Deploy the HTML Page

#### i. Create an `index.html` file on your local machine (e.g., using VS Code).

#### ii. Deploy the HTML file to the EC2 instance:
```bash
scp -i "server002_key.pem" /home/vagrant/webfile/index.html ubuntu@ec2-35-180-226-52.eu-west-3.compute.amazonaws.com:/home/ubuntu
```

#### iii. Move the HTML file to the web server directory:
```bash
sudo mv index.html /var/www/html
```

### 4. Configure HTTPS (Let’s Encrypt)

#### i. Obtain a domain name:
A domain name (`ajadi.server.aomine-projects.free.nf`) was obtained using Infinity Free and linked to the EC2 instance.

#### ii. Install Certbot for SSL configuration:
```bash
sudo apt install certbot python3-certbot-apache -y
```

#### iii. Obtain a free SSL certificate:
Run the following command and follow the prompts to complete the SSL setup:
```bash
sudo certbot --apache
```

### 5. Verify the HTTPS Setup
Visit [https://ajadi.server.aomine-projects.free.nf](https://ajadi.server.aomine-projects.free.nf) to confirm secure access.

## Contact
For questions or suggestions:
- **Email**: ajadiadedeji@gmail.com
- **GitHub**: [Ajadi24](https://github.com/Ajadi24)
- **Webpage URL**: [https://ajadi.server.aomine-projects.free.nf](https://ajadi.server.aomine-projects.free.nf)
- **Public IP Address**: 35.180.226.52

