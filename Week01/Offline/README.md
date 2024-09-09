# Docker and Web Server Labs

Welcome to the Docker and Web Server Labs repository! This repository contains solutions and reports for various lab exercises related to web servers (Nginx and Apache), Docker containerization, and networking. 

## Lab 1: Web Server Report

In this lab, we will create a comprehensive report comparing web servers Nginx and Apache. The report should cover various aspects such as:

- **Performance**: Compare response times and resource utilization.
- **Configuration**: Discuss configuration complexity and ease of use.
- **Use Cases**: Highlight typical use cases and scenarios where one might be preferred over the other.
- **Security**: Analyze security features and best practices.
- **Scalability**: Evaluate scalability options and load handling capabilities.

## Lab 2: Docker Tasks

### P1: Custom Nginx Docker Image

1. **Objective**: Create a Docker image for Nginx based on Ubuntu without using the official Nginx image.
2. **Steps**:
   - **Base Image**: Use Ubuntu as the base image.
   - **Install Nginx**: Install Nginx within the container.
   - **Add Index Files**: 
     - Place an `index.html` file directly in `/var/www/html`.
     - Include another `index.html` file packed in a `.tar` archive and extract it to `/var/www/html`.
   - **Expose Ports**: Expose port 80 for HTTP traffic.
   - **Start Nginx**: Configure the container to start Nginx on boot.
   - **Port Mapping**: Map port 80 of the container to port 8080 of the host.

**Dockerfile Example**:
```Dockerfile
# Use Ubuntu as the base image
FROM ubuntu:latest

# Install necessary packages
RUN apt-get update && \
    apt-get install -y nginx && \
    apt-get clean

# Copy index.html files
COPY index.html /var/www/html/
COPY index.tar /tmp/index.tar

# Extract the tar file
RUN tar -xf /tmp/index.tar -C /var/www/html

# Expose port 80
EXPOSE 80

# Start Nginx
CMD ["nginx", "-g", "daemon off;"]
