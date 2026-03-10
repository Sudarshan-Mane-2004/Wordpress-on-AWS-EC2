# 🚀 WordPress Deployment on AWS EC2 using LEMP Stack

## 📌 Project Overview

This project demonstrates how to deploy a **WordPress website on an AWS EC2 instance** using the **LEMP stack**.

LEMP stands for:

- **Linux** – Ubuntu Server
- **Nginx** – Web Server
- **MySQL** – Database
- **PHP** – Server-side scripting language

The website is hosted on an **AWS EC2 instance** and accessed through the **public IP address**.

---

# 🏗 Architecture

User Browser
│
▼
AWS EC2 Instance
│
├── Nginx Web Server
├── PHP-FPM
├── MySQL Database
└── WordPress Application

---

# ☁️ AWS EC2 Server Creation

Steps:

1. Login to AWS Console
2. Navigate to EC2
3. Click **Launch Instance**
4. Select

AMI: Ubuntu Server
Instance Type: t2.micro


5. Create key pair
6. Configure security group

Allow:

| Type | Port |
|-----|-----|
| SSH | 22 |
| HTTP | 80 |


---

## 📷 EC2 Instance Running

<img width="1919" height="1079" alt="Screenshot 2026-03-10 154304" src="https://github.com/user-attachments/assets/8e1e3b94-4675-4360-88aa-db60c2e43fc4" />




---

# 🔗 Connect to EC2 Server

ssh -i key.pem ubuntu@your-public-ip



---

# 🔄 Update Server
sudo apt update
sudo apt upgrade -y


---

# 🌐 Install Nginx
sudo apt install nginx -y
Check status


sudo systemctl status nginx

Restart Nginx

sudo systemctl restart nginx

---

# 🗄 Install MySQL
sudo apt install mysql-server -y
Secure MySQL
sudo mysql_secure_installation

Check MySQL status
sudo systemctl status mysql

---

# ⚡ Install PHP
sudo apt install php-fpm php-mysql php-cli php-curl php-gd php-mbstring php-xml php-zip -y

Check PHP version
php -v

Restart PHP
sudo systemctl restart php8.3-fpm

---

# 📦 Download WordPress

Navigate to web directory
cd /var/www/html

Download WordPress
wget https://wordpress.org/latest.tar.gz

Extract files
tar -xvf latest.tar.gz

Move WordPress files
sudo mv wordpress/* /var/www/html/

---

# 🔐 Set File Permissions
sudo chown -R www-data:www-data /var/www/html
sudo chmod -R 755 /var/www/html

---

# ⚙️ Configure WordPress

Create configuration file
sudo cp wp-config-sample.php wp-config.php

Edit configuration
sudo nano wp-config.php

Update database details
define('DB_NAME', 'wordpressdb');
define('DB_USER', 'wpuser');
define('DB_PASSWORD', 'password');
define('DB_HOST', 'localhost');


---

# 🗃 Create MySQL Database

Login to MySQL
sudo mysql

Create database
CREATE DATABASE wordpressdb;
Create user


CREATE USER 'wpuser'@'localhost' IDENTIFIED BY 'password';


Grant privileges


GRANT ALL PRIVILEGES ON wordpressdb.* TO 'wpuser'@'localhost';


Apply changes


FLUSH PRIVILEGES;


Exit


EXIT;


---

# 🔄 Restart Services


sudo systemctl restart mysql
sudo systemctl restart nginx
sudo systemctl restart php8.3-fpm


---

# 🌍 Access WordPress

Open in browser


http://your-ec2-public-ip


---

# 📷 WordPress Installation Page

<img width="1918" height="1079" alt="Screenshot 2026-03-10 153848" src="https://github.com/user-attachments/assets/3d702517-467f-4cdf-8e73-bd8c76223fae" />


---

# 📷 WordPress Login Page

<img width="1919" height="1079" alt="Screenshot 2026-03-10 153928" src="https://github.com/user-attachments/assets/d59b2161-5d9d-49c9-9690-bace92150b73" />


---

# 📷 WordPress Dashboard

<img width="1919" height="1079" alt="Screenshot 2026-03-10 153943" src="https://github.com/user-attachments/assets/765a100c-e3f1-42a5-80e0-75a35457bbf9" />


---

# 📷 AWS Security Group Configuration

<img width="1743" height="1079" alt="Screenshot 2026-03-10 154317" src="https://github.com/user-attachments/assets/0bee58e4-06f0-4687-ac74-ad1a82fdb249" />


---

# ⚠️ Problems Faced During Execution

## 1️⃣ Apache Default Page Appearing

Problem:


Apache2 Default Page appeared instead of WordPress


Reason:

Apache was running on port **80**.

Solution:


sudo systemctl stop apache2
sudo systemctl disable apache2
sudo apt purge apache2 -y


---

## 2️⃣ PHP Files Downloading Instead of Executing

Problem:


PHP files were downloading instead of executing


Reason:

Nginx was not configured with PHP-FPM.

Solution:

Configured Nginx to use **PHP-FPM**.

---

## 3️⃣ 403 Forbidden Error

Problem:


403 Forbidden error from Nginx


Reason:

Incorrect file permissions.

Solution:


sudo chown -R www-data:www-data /var/www/html
sudo chmod -R 755 /var/www/html


---

## 4️⃣ Database Connection Error

Problem:


Error establishing database connection


Reason:

Incorrect database credentials in **wp-config.php**

Solution:

Correct database configuration.

---

# ✅ Final Result
Successfully deployed **WordPress on AWS EC2 using LEMP Stack**.

Technologies used:

- AWS EC2
- Ubuntu Linux
- Nginx
- PHP
- MySQL
- WordPress

---

# 🎯 Learning Outcomes

Through this project I learned:

- AWS EC2 server creation
- Security group configuration
- LEMP stack installation
- WordPress deployment
- Linux command line operations
- Troubleshooting server errors

---

# 👨‍💻 Author

**Sudarshan Mane**

Cloud & DevOps Enthusiast 🚀
