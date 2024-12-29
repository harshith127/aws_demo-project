# Web Application Deployment on EC2

This guide walks you through deploying a simple web application on an AWS EC2 instance using Apache2.

---

## Prerequisites

- An **AWS account**.
- Basic knowledge of **AWS EC2** and **terminal commands**.
- An EC2 instance with **Apache2** installed.

---

## Steps for Deployment

### 1. **Create an EC2 Instance**
- Log in to your [AWS Management Console](https://aws.amazon.com/console/).
- Navigate to the EC2 Dashboard and click **Launch Instance**.
- Choose an appropriate AMI, such as **Ubuntu Server**.
- Select an instance type (e.g., `t2.micro` for testing).
- Configure instance details as per your requirements.
- In the **Configure Security Group**, allow traffic for:
    -Allow HTTPS traffic from the internet
    -Allow HTTP traffic from the internet
- Launch the instance and download the key pair.

---

### 2. **Connect to Your EC2 Instance**
Use the following command to connect to your EC2 instance via SSH:

```bash
ssh -i /path/to/your-key.pem ubuntu@<your-ec2-public-ip>
```

3. Install Apache2
Update the package list and install Apache2:

```bash
sudo apt update
sudo apt install apache2 -y
```
4. Download Your Application Files
Clone my GitHub repository to the EC2 instance .

 *Clone the Repository
 ```bash
git clone https://github.com/your-username/aws_demo-project.git
```
5. Deploy Your Application
Move the application files to Apache's web directory
```bash
sudo mv /home/ubuntu/aws_demo-project/* /var/www/html/
```
6. Set File Permissions
Ensure Apache2 has proper access permissions: (if nessary change the permission. even `400` is enough  )
```bash
sudo chown -R www-data:www-data /var/www/html/
sudo chmod -R 755 /var/www/html/
```
7. Start Apache2
Start Apache2 and enable it to run at system startup:

```bash
sudo systemctl start apache2
sudo systemctl enable apache2
```
8. Access Your Application
Open a browser and visit:

plaintext
```bash
http://<your-ec2-public-ip>
```
Your application should now be accessible to everyone!

IMPORTENT NOTE :

1.This application works only over HTTP. HTTPS is not configured.

2.Ensure the /var/www/html/ directory contains only your application files.

3.Restrict SSH access in your security group for better security.



