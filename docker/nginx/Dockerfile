FROM debian:jessie
MAINTAINER Don B. Stringham <donbstringham@gmail.com>

RUN apt-get update && apt-get install -y \
    nginx

COPY nginx.conf /etc/nginx/nginx.conf

EXPOSE 80 443

CMD ["nginx", "-g", "daemon off;"]
