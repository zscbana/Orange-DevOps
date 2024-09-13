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
├── backend/ 
│   └── Dockerfile     
├── db_data_password/
│   └── password.txt
├── nginx/
|   └── Dockerfile
│   └── nginx.conf
|   └── ssl.sh
└── docker-compose.yml
