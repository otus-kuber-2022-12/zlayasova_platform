FROM nginx:1.23.3

RUN groupadd appuser && \
    useradd -r -u 1001 -g appuser appuser && \
     mkdir /app

COPY ./app/default.conf /etc/nginx/conf.d/default.conf
COPY ./app/nginx.conf /etc/nginx/nginx.conf

RUN chown -R appuser:appuser /app && \
    chown -R appuser:appuser /var/cache/nginx && \
    chown -R appuser:appuser /var/log/nginx && \
    chown -R appuser:appuser /etc/nginx/conf.d && \
    chown -R appuser:appuser /etc/nginx/nginx.conf

RUN touch /var/run/nginx.pid && \
        chown -R appuser:appuser /var/run/nginx.pid

USER appuser