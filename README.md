# AWS EC2 Instance Provisioning, Setting up a Web Server, HTML Deployment, and HTTPS Configuration

This project demonstrates how to provision an AWS EC2 instance, set up a web server, deploy an HTML page, and configure HTTPS using a custom domain name to obtain a free SSL certificate.

## Table of Contents
1. [Overview](#overview)
2. [Prerequisites](#prerequisites)
3. [Steps](#steps)
   - [Provision EC2 Instance on AWS](#provision-ec2-instance-on-aws)
   - [Web Server Setup](#web-server-setup)
   - [Deploy the HTML Page](#deploy-the-html-page)
   - [Configure HTTPS (Let’s Encrypt)](#configure-https-let-s-encrypt)
   - [Verify the HTTPS Setup](#verify-the-https-setup)
4. [Contact](#contact)

## Overview
This project provides a step-by-step guide to:
1. Provision an AWS EC2 instance.
2. Setup a web server.
3. Deploy a static HTML page to the instance.
4. Configure a domain with HTTPS for secure access.

### Technologies Used:
- **AWS EC2**
- **Apache** (Web Server)
- **Certbot** (SSL Certificate Configuration)

## Prerequisites
Before starting, ensure you have the following:
1. An AWS account.
2. A registered domain name.
3. SSH client (e.g., PuTTY, terminal).
4. Basic understanding of Linux commands.

## Steps

### Provision EC2 Instance on AWS
1. Log in to the [AWS Management Console](https://aws.amazon.com/console/).
2. Navigate to the EC2 Dashboard and launch a new instance.
3. Select Ubuntu as the Amazon Machine Image.
4. Choose an appropriate instance type (e.g., t2.micro for free tier).
5. Configure security groups:
   - Allow inbound rules for HTTP (port 80) and HTTPS (port 443).
6. Launch the instance and download the key pair for SSH access.
7. On the terminal, change permissions for the key pair to prevent public access using:

   ```bash
   sudo chmod 400 "server002_key.pem"
   ```

### Web Server Setup
1. SSH into the EC2 instance:

   ```bash
   ssh -i "server002_key.pem" ubuntu@ec2-35-180-226-52.eu-west-3.compute.amazonaws.com
   ```

2. Install the web server (Apache):

   ```bash
   sudo apt update && sudo apt upgrade
   sudo apt install apache2 -y
   ```

3. Start the web server and enable it on boot:

   ```bash
   sudo systemctl start apache2
   sudo systemctl enable apache2
   ```

### Deploy the HTML Page
1. Create an `index.html` file locally using VS Code or your preferred editor.
2. Deploy the HTML file from your local terminal to the home directory of your AWS EC2 instance using Secure Copy Protocol (SCP):

   ```bash
   scp -i "server002_key.pem" /path/to/your/index.html ubuntu@ec2-35-180-226-52.eu-west-3.compute.amazonaws.com:/home/ubuntu
   ```

3. Move the HTML file to the web server directory:

   ```bash
   sudo mv index.html /var/www/html
   ```

### Configure HTTPS (Let’s Encrypt)
1. Obtain a domain name (e.g., `ajadi.server.aomine-projects.free.nf`) using a service like [Infinity Free](https://www.infinityfree.net/).
2. Link the domain name to your EC2 instance.
3. Install Certbot for SSL configuration:

   ```bash
   sudo apt install certbot python3-certbot-apache -y
   ```

4. Obtain a free SSL certificate by running the following command and following the prompts:

   ```bash
   sudo certbot --apache
   ```

### Verify the HTTPS Setup
Visit [https://ajadi.server.aomine-projects.free.nf](https://ajadi.server.aomine-projects.free.nf) to verify the HTTPS configuration.

## Contact
For questions or suggestions:
- **Email**: [ajadiadedeji@gmail.com](mailto:ajadiadedeji@gmail.com)
- **GitHub**: [Ajadi24](https://github.com/Ajadi24)
- **Webpage URL**: [https://ajadi.server.aomine-projects.free.nf](https://ajadi.server.aomine-projects.free.nf)
- **Public IP Address**: `35.180.226.52`
