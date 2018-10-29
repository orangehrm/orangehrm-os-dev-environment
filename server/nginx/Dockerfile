FROM nginx:1.13

COPY config /etc/nginx/conf.d
COPY certs/orangehrmdev.priv.cert /etc/ssl/certs/orangehrmdev.priv.cert
COPY certs/orangehrmdev.priv.key /etc/ssl/private/orangehrmdev.priv.key
COPY entrypoint.sh /entrypoint.sh

RUN chmod +x /entrypoint.sh

CMD /entrypoint.sh
