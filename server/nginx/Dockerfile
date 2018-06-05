FROM nginx:1.13

COPY config/server.conf /etc/nginx/conf.d/server.conf
COPY entrypoint.sh /entrypoint.sh

RUN chmod +x /entrypoint.sh

CMD /entrypoint.sh
