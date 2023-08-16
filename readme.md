# **Automated WordPress Deployment with Nginx, LEMP Stack, and GitHubActions**

_**This repository contains all the necessary code and configuration files
to set up an automated deployment process for a WordPress website using
Nginx as the web server, LEMP (Linux, Nginx, MySQL, PHP) stack, and
GitHub Actions as the CI/CD automation tool. The deployment process
follows security best practices and ensures optimal performance of the
website.**_

## **Server Provisioning:**

-   (I am using AWS as the Cloud Provider)

-   Provision an EC2 instance on AWS with a secure Linux distribution
    (e.g., Ubuntu 22.04).

-   Configure security groups to allow necessary incoming traffic and
    restrict unnecessary access.

-   Generate and configure SSH key pairs for secure remote access...

## **Nginx, MySQL/MariaDB, and PHP Setup**

-   Install and configure Nginx as the web server.

```{=html}
sudo systemctl start nginx
sudo systemctl enable nginx
```
-   Set up MySQL/MariaDB as the database and configure it securely.

```{=html}
sudo yum install mariadb-server -y

sudo systemctl start mariadb

sudo systemctl enable mariadb

sudo mysql_secure_installation
```
-   Install and configure PHP for processing dynamic content.

```{=html}

sudo yum install php php-mysqlnd php-fpm -y

sudo systemctl start php-fpm

sudo systemctl enable php-fpm
```
## **WordPress Website Configuration**
-   Access your EC2 instance and set up a WordPress website.

-   Navigate to your Nginx web server root directory.

```{=html}
cd /usr/share/nginx/html

sudo wget <https://wordpress.org/latest.tar.gz>

sudo tar -xzvf latest.tar.gz

sudo chown -R nginx:nginx /usr/share/nginx/html

sudo chmod -R 755 /usr/share/nginx/html
```
```{=html}
my sql 
```
```{=html}
CREATE DATABASE wordpress;

CREATE USER 'wordpressuser'@'localhost' IDENTIFIED BY'password';

GRANT ALL ON wordpress.* TO 'wordpressuser'@'localhost';

FLUSH PRIVILEGES;

 EXIT;

```
-   Secure the WordPress installation following best practices (strong
    passwords, limited user privileges, etc.).

-   I attempted to set up a self-signed SSL certificate, but
    unfortunately, I couldn't complete the process successfully.

-   Implement SSL/TLS certificate using Let\'s Encrypt for secure
    communication.

## **GitHub Repository Setup**

-   Create a GitHub repository for this project.

```{=html}
git init

git remote add origin https://github.com/SudharshanPalabindela/WordPressServer.git> 

git branch -M main

git push -u origin main
```

-   files pushed from the ec2 instances to the git repository

-   Set up a GitHub Actions workflow for automated deployment.

## ** GitHub Actions Workflow**

-   The GitHub Actions workflow automates the deployment process to the
    AWS EC2 instance.

-   The workflow installs necessary dependencies.

-   It builds the project and prepares it for deployment.

-   Securely transfers files to the EC2 instance using SSH.
-   While configuring the file check the **SSH_PVT_KEY, HOST_DNS, USERNAME, EC2_IPADDRESS**
-   CHECK env VARIABLES
-   I have configure my workflow as Main.Html
