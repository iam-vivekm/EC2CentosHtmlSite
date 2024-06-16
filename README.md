# EC2CentosHtmlSite

How to host a html website on ec2 instance on Ubuntu

To host an HTML website on an EC2 instance running ubuntu, follow these steps:

1. Launch an EC2 Instance
Sign in to the AWS Management Console and open the EC2 Dashboard.
Launch a new instance:
Choose the Amazon Machine Image (AMI) for CentOS.
Select an instance type (e.g., t2.micro for free tier).
Configure the instance details, add storage, and tag the instance (optional).
*Configure the security group to allow SSH (port 22) and HTTP (port 80) access.
Launch the instance and download the key pair for SSH access.

3. Connect to Your EC2 Instance
Open your terminal (Linux/Mac) or use an SSH client (e.g., PuTTY for Windows).

Connect to the instance:

-> ssh -i <your-key-file.pem> ubuntu@<your-instance-public-ip>

3. Install Apache Web Server
Update the package index:

-> apt update -y

Install Apache:

-> apt install apache2 -y

Start the Apache service and enable it to start on boot:

-> systemctl start httpd
-> systemctl enable httpd

4. Configure Firewall

Allow HTTP traffic:

-> firewall-cmd --zone=public --permanent --add-service=http
-> firewall-cmd --reload

5. Deploy Your HTML Website

Upload your HTML files:
You can use scp (secure copy protocol) to transfer your HTML files from your local machine to the EC2 instance:

scp -i <your-key-file.pem> <path-to-your-html-files> centos@<your-instance-public-ip>:/var/www/html/

Alternatively, you can directly edit or create HTML files on the instance using nano or vim:

-> vim /var/www/html/index.html

Set proper permissions for the Apache web directory:

-> chown -R apache:apache /var/www/html
-> chmod -R 755 /var/www/html

6. Access Your Website
Open a web browser and navigate to http://<your-instance-public-ip>. You should see your HTML website displayed.
