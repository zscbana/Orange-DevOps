# Three-Tier Application with Docker

This repository sets up a three-tier application consisting of a backend, a database, and a proxy using Docker. 

## Features

- Backend Dockerfile using a **multi-stage build**.
- Database credentials stored securely on the **host machine**.
- Proxy server runs on **HTTPS**, with configuration files stored on the host.
- Each container runs in a **separate Docker network**.
- The entire project can be started or stopped with **one command** using Docker Compose.

## Project Structure

```bash
.
├── backend/              # Backend application files
│   └── Dockerfile        # Multi-stage Dockerfile
├── db_data/              # Database volume data
├── certs/                # SSL certificates for HTTPS
├── nginx/                # Nginx configuration files
│   └── nginx.conf        # Nginx configuration
├── .env                  # Environment file for sensitive data
└── docker-compose.yml    # Docker Compose configuration
