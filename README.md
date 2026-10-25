PHP Project Deployment on AWS EC2
1. Project Overview

This project demonstrates the deployment of a PHP-based web application on an AWS EC2 Linux instance using Nginx as the web server and MariaDB as the database.

The application allows users to submit information through a web form. The submitted data is stored in the MariaDB database and displayed on the form submission result page.

Technologies Used
AWS EC2
Amazon Linux
Nginx
PHP
MariaDB
Git and GitHub
2. Deployment Architecture
text
User Browser
     |
     v
AWS EC2 Instance
     |
     v
Nginx Web Server
     |
     v
PHP Application
     |
     v
MariaDB Database (FCT)
     |
     v
Users Table

3. Upload the Project to GitHub

Initialize the Git repository, stage the project files, and commit the changes.

bash
git init
git status
git add .
git status
git commit -m "initial commit"
git branch -M main
git remote add origin <URL>
git push -u origin main


Replace <URL> with your GitHub repository URL.

The project is now available on GitHub and can be downloaded to the EC2 instance during deployment.

4. Launch and Configure AWS EC2
Log in to the AWS Management Console.
Open the EC2 dashboard and launch a Linux instance.
Configure the instance and create or select an SSH key pair.
Configure the security group to allow SSH access on port 22 from your IP address and HTTP access on port 80.
Launch the instance and connect to it using SSH.

Ensure the EC2 instance is running before proceeding.

5. Install and Start the Required Services

Update the system packages and install Nginx, MariaDB, PHP, and Git.

bash
sudo yum update
sudo yum install nginx mariadb105-server php git -y


Start the required services:

bash
sudo systemctl start nginx mariadb php-fpm


Enable the services to start automatically when the instance boots:

bash
sudo systemctl enable nginx mariadb php-fpm


Verify the service status:

bash
sudo systemctl status nginx mariadb php-fpm


These services provide the web server, PHP processing, and database functionality required by the application.

6. Clone the GitHub Repository on EC2

Navigate to the Nginx web root and clone the project repository.

bash
cd /usr/share/nginx/html
sudo git clone https://github.com/Sushant123456789/php-project.git


Check the project directory:

bash
ls
cd php-project
ls


The project files are now available on the EC2 instance under the Nginx web root.

7. Configure the MariaDB Database

Log in to MariaDB:

bash
sudo mysql


Set the MariaDB root password as used in your setup:

sql
ALTER USER root@localhost IDENTIFIED BY "root";


Exit and log in again:

sql
exit;

bash
sudo mysql
sudo mysql -u root -p


Create the project database:

sql
CREATE DATABASE FCT;
SHOW DATABASES;
USE FCT;


Create the table for storing form submissions:

sql
CREATE TABLE users (
    id INT PRIMARY KEY AUTO_INCREMENT,
    name VARCHAR(50),
    email VARCHAR(100),
    website VARCHAR(200),
    comment VARCHAR(500),
    gender VARCHAR(50)
);


Verify the table structure:

sql
DESC users;


View the stored records:

sql
SELECT * FROM users;


The FCT database and users table are now ready to store submitted form information.

8. Install the PHP MySQL Connector

Check the installed PHP version:

bash
php --version


Install the PHP MySQL connector:

bash
sudo yum install php8.5-mysqlnd.x86_64 -y


This package provides PHP connectivity to MySQL-compatible databases such as MariaDB.

The connector package must match the PHP version and repositories available on the EC2 instance. If the specified package is unavailable, verify the installed PHP version and the package name provided by the configured repositories.

9. Access the Deployed Application

Open the browser and visit the deployed application:

Application URL: http://54.197.10.195/php-project/signup.html

The signup page should load from the EC2 instance through Nginx.

Submit the form to verify that the PHP application processes the request and stores the submitted information in MariaDB.

10. Verify the Deployment

The deployment can be verified using the following checks:

EC2: The instance is running.
Nginx: The web server service is active.
PHP: PHP and PHP-FPM are installed and running.
GitHub: The project repository has been cloned onto the EC2 instance.
MariaDB: The FCT database and users table exist.
Application: The signup page loads through the EC2 public IP.
Database: Submitted records appear when running SELECT * FROM users;.

The project screenshots show a successful form submission in the browser and the corresponding records in the MariaDB database, demonstrating that the application and database are connected.

11. Conclusion

The PHP project was deployed on AWS EC2 using Nginx, PHP, MariaDB, and Git. The project source code was uploaded to GitHub and cloned onto the EC2 instance. The required services were started, the database and table were created, and the application was accessed through the instance's public IP address.

The successful form submission and database records confirm that the main deployment workflow is working.

12. Security Note

The root password shown in the setup commands is suitable only for documenting a test environment and should not be used in production. Use a strong password, create a dedicated database user for the application, and restrict administrative access.
<img width="1366" height="768" alt="Screenshot (200)" src="https://github.com/user-attachments/assets/20bc3ea3-ba99-44fa-ab3d-f78184b39dd5" />
<img width="1366" height="768" alt="Screenshot (199)" src="https://github.com/user-attachments/assets/dafc6460-cca2-432c-a0d8-77145718e9f1" />

