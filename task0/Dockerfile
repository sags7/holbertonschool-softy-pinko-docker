# Use the latest official Ubuntu image
FROM ubuntu:latest

# Set non-interactive mode for apt (avoids prompts during install)
ENV DEBIAN_FRONTEND=noninteractive

# Update package list and upgrade installed packages
RUN apt-get update && apt-get upgrade -y

# Default command to run when the container starts
CMD ["echo", "Hello, World!"]
