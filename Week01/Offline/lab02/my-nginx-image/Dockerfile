FROM ubuntu

RUN apt-get update && apt-get install -y nginx && apt-get clean

COPY index.html /var/www/html/index.html


COPY index.tar /tmp/index.tar
RUN tar -xvf /tmp/index.tar -C /var/www/html

EXPOSE 80

CMD ["nginx", "-g", "daemon off;"]