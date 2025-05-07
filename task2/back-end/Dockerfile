# Use the latest official Ubuntu image
FROM ubuntu:latest

# Update package list and upgrade installed packages
RUN apt-get update && apt-get upgrade -y

# Install Python3 and pip
RUN apt-get install -y python3 python3-pip

# Install Python3 development headers and libraries
RUN rm /usr/lib/python*/EXTERNALLY-MANAGED

# Install flask
RUN pip3 install flask

# Set the working directory
WORKDIR /app

# Copy the current directory contents into the container at /app
COPY ./api.py /app/api.py

# Expose port 5252 for the Flask application
EXPOSE 5252

# Run the application
CMD ["python3", "api.py"]
