# Use the official Nginx Alpine image
FROM nginx:alpine

# Install OpenSSL and Bash
RUN apk add --no-cache openssl bash

# Copy your custom Nginx configuration file into the container
COPY ./nginx.conf /etc/nginx/nginx.conf

# Run Nginx in the foreground (important for Docker containers)
CMD ["nginx", "-g", "daemon off;"]

# Expose port 443 for HTTPS
EXPOSE 443
