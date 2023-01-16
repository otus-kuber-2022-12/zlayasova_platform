FROM nginx:1.23.3

COPY default.conf  /etc/nginx/conf.d/

RUN chmod -R 777 /var/cache/nginx && \
    chmod -R 777 /var/run

USER 1001
CMD ["nginx", "-g", "daemon off;"]
