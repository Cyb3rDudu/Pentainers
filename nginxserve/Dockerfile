FROM nginx:stable

COPY default.conf /etc/nginx/conf.d/
COPY start.sh /

RUN apt-get update && apt-get install -y openssl \
    && mkdir -p /etc/nginx/ssl && mkdir -p /srv/data \
    && chmod +x /start.sh

ENTRYPOINT [ "/start.sh" ]
