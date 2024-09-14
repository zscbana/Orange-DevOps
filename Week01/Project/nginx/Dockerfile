FROM nginx:alpine

RUN apk add --no-cache openssl bash

COPY ./nginx.conf /etc/nginx/nginx.conf

COPY ./ssl/nginx-selfsigned.crt /etc/nginx/ssl/nginx-selfsigned.crt
COPY ./ssl/nginx-selfsigned.key /etc/nginx/ssl/nginx-selfsigned.key

CMD ["nginx", "-g", "daemon off;"]

EXPOSE 443
