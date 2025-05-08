Having separate Docker images/containers per component of your application can reduce the complexity of your web apps. That said, having more than a single Docker image that you need to spin up in containers can present challenges; what if you need to spin up 3 distinct Docker images, or 7, or 50? Opening each one, one at a time would quickly become an issue. That’s where Docker Compose comes into play. With a docker-compose.yml file, we can specify the different components of your entire application, set up some basic configurations, and allow Docker to handle spinning up the entire application all at once, no matter how many containers there are.

Inside the task4 directory, create a docker-compose.yml file

Once you’ve set up your docker-compose.yml file with the correct services, you should be able to build them using docker-compose build and run it with docker-compose up like this:

Important keywords to have in a docker-compose.yml file:

services
build, context, dockerfile
image
ports
Note: when setting a port, the syntax will be HOSTPORT:CONTAINERPORT. For example, 9999:4567 would map the 4567 port inside of the Docker container to the host machine’s 9999 port. If you only supply one port number, instead of a mapping, you are only specifying an internal port that other Docker containers can reach, but they will not be mapped to any port on the host machine. If you do not map any ports, you will not be able to get past the firewall that Docker has put up. Docker uses something similar to Linux’s Uncomplicated Firewall ufw; you do not directly work with this firewall, but instead, map allowed ports in Dockerfiles or docker-compose files to allow/disallow access through certain ports.
depends_on