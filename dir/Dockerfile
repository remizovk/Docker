FROM alpine:latest

RUN apk update \
    && apk upgrade \
    && apk add nginx \
    && apk add vim \
    && apk add bash \
    && apk add curl \
    && mkdir -p /run/nginx \
    && mkdir -p /www/data

COPY nginx.conf /etc/nginx/
COPY index.html /www/data/ 

EXPOSE 80

STOPSIGNAL SIGTERM

CMD ["nginx", "-g", "daemon off;"]
