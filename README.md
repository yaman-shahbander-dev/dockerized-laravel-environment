# dockerized-laravel-environment

## Description
This project represents a Dockerized environment for a Laravel web application. By leveraging Alpine Linux as the base operating system, Nginx as the web server, and PHP-FPM for PHP processing, this setup ensures a lightweight, secure, and efficient infrastructure for running Laravel applications. The project directory is structured at /var/www/html, providing a centralized location for hosting the Laravel application files.

## Prerequisites
Before you begin, ensure you have Docker installed on your machine. Follow [the Docker's official website](https://docs.docker.com/get-docker/) for installation instructions.

## Why Alpine Linux?
The choice of Alpine Linux as the base OS offers exceptional performance and security benefits due to its minimalistic design and focus on resource efficiency.

## Why Nginx & PHP-FPM?
Nginx serves as the high-performance web server, handling incoming HTTP requests and efficiently serving static and dynamic content to users. 
PHP-FPM is utilized to process PHP scripts, ensuring optimal performance and scalability for Laravel applications.

## Docker Compose Services
- **php**: Service running PHP-FPM with the project files mounted at `/var/www/html`.
- **nginx**: Nginx service serving as the web server with the project files mounted and configured at `/etc/nginx/conf.d/default.conf`.
- **mysql**: MySQL service with the database name "laravel", root user "laravel", and root user password "root".
- **phpmyadmin**: PhpMyAdmin service for database management linked to the MySQL service.

## Using the Docker Setup
To incorporate the Docker environment into your project, follow these steps:

1. **Add the Docker Folder**:
   - Copy the `docker` folder from this repository and paste it into your project directory.
    
2. **Run Docker Compose**:
   - Open a terminal window and navigate to your project directory.
   - Run the following command to start the Docker containers defined in the `docker-compose.yaml` file:
     ```bash
     docker-compose -f ./docker/docker-compose.yaml up -d
     ```
     
### Explanation:
- The command `docker-compose -f ./docker/docker-compose.yaml up -d` is used to start the Docker containers defined in the `docker-compose.yaml` file located in the `docker` folder.
- The option `-f` specifies the location of the compose file, in this case, `./docker/docker-compose.yaml`.
- The flag `-d` runs the containers in detached mode, allowing them to run in the background.
- This command will initiate the setup of the PHP, Nginx, MySQL, and PhpMyAdmin services as per the configurations specified in the `docker-compose.yaml` file.

## Database Credentials
- Database Name: laravel
- Root User: root
- Root User Password: root

## Contact Me
You can contact me at [yaman.engineer.dev@gmail.com](mailto:yaman.engineer.dev@gmail.com)

---
