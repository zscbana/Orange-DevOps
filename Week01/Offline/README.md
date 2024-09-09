# Docker and Web Server Labs

## Lab 1: Web Server Report
- Create a report comparing Nginx and Apache web servers covering performance, configuration, use cases, security, and scalability.

## Lab 2: Docker Tasks

### P1: Custom Nginx Docker Image
- Create a Docker image for Nginx based on Ubuntu.
- Install Nginx.
- Add two `index.html` files: one as a direct file and one as a `.tar` archive.
- Expose port 80.
- Start Nginx and map container port 80 to host port 8080.

### P2: React App Docker Container
- Create a single-stage Docker container for a React application.

### P3: Docker Network Types
- List and define the different types of Docker networks: Bridge, Host, Overlay, Macvlan, and None.

### P4: Create and Test a Bridge Network
- Create a bridge network.
- Run two Ubuntu containers on this network with different names.
- Test connectivity between the containers using `ping`.
