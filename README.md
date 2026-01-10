## WordPress Deployment on Ubuntu (LEMP Stack)
Project Overview
This project demonstrates a manual installation and configuration of a WordPress site on an Ubuntu server using the LEMP stack (Linux, Nginx, MariaDB, and PHP). Instead of using automated scripts or Docker, this project focuses on the step-by-step configuration of the web server, database management, and permission handling.

## Tech Stack
Operating System: Ubuntu

Web Server: Nginx

Database: MariaDB (MySQL fork)

Language: PHP (with FPM)

CMS: WordPress

## Installation & Configuration Steps
# 1. System Update & Web Server Setup
The system was updated to ensure all security patches were in place. Nginx was installed and configured to handle web traffic.

Bash

sudo apt update && sudo apt upgrade -y
sudo apt install nginx -y
# 2. Database Configuration (MariaDB)
A secure MariaDB instance was deployed. I created a dedicated database (wpdb) and a secure user (wpuser) with restricted privileges to follow the Principle of Least Privilege.

SQL

CREATE DATABASE wpdb;
CREATE USER 'wpuser'@'localhost' IDENTIFIED BY 'YOUR_PASSWORD';
GRANT ALL PRIVILEGES ON wpdb.* TO 'wpuser'@'localhost';
# 3. PHP-FPM Integration
Since Nginx does not have native PHP processing, PHP-FPM (FastCGI Process Manager) was installed along with necessary modules for WordPress functionality (GD, MySQL, XML, etc.).

# 4. WordPress Core & Permissions
The latest WordPress package was downloaded and extracted to the web root. Crucially, ownership was assigned to the www-data user to allow the web server to manage files securely.

Bash

sudo chown -R www-data:www-data /var/www/html
sudo chmod -R 755 /var/www/html
# 5. Nginx Virtual Host Configuration
A custom server block was created to:

Listen on port 80.

Route PHP requests to the PHP-FPM socket.

Enable "Pretty Permalinks" via the try_files directive.

Secure the server by turning off server_tokens.

## Key Learnings
Manual Stack Configuration: Understanding how Nginx communicates with PHP via Unix sockets.

Database Security: Using mysql_secure_installation and managing SQL privileges.

Permissions Management: Learning the importance of chown and chmod for web security.

Troubleshooting: Using nginx -t and systemctl status to debug configuration errors.

## How to use
Clone this repository.

Follow the commands in the install.sh (om du lägger ditt script i en fil).

Access the site via http://localhost or your configured domain.
