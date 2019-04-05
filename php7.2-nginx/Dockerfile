FROM kumadoto/php:7.2-fpm

RUN apt update \
    && apt install -y \
    nginx
    
CMD ["nginx", "-g", "daemon off;"]
