# Pull nginx
FROM nginx:1.25.4-alpine
# Set the working directory
WORKDIR /etc/nginx/conf.d
# Copy nginx configuration file
COPY nginx.conf .
# Rename the nginx configuration file
RUN mv nginx.conf default.conf
# Reset the working directory
WORKDIR /var/www/html
