# Install the latest version of Nginx
FROM nginx:latest

# Copy softy-pinko-front-end files into the container
COPY ./softy-pinko-front-end /var/www/html/softy-pinko-front-end

# Copy the Nginx configuration file into the container
COPY ./softy-pinko-front-end.conf /etc/nginx/conf.d/default.conf
