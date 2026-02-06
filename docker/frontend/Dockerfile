FROM nginx:latest

ARG AMBIENTE
ARG ARTIFACT

ADD ${ARTIFACT} /tmp/

# Limpieza, despliegue de estáticos, preparación de nginx para ejecución non-root
RUN rm -rf /usr/share/nginx/html/* \
    && mv /tmp/dist/* /usr/share/nginx/html/ \
    && mkdir -p /var/cache/nginx/client_temp \
               /var/cache/nginx/proxy_temp \
               /var/cache/nginx/fastcgi_temp \
               /var/cache/nginx/uwsgi_temp \
               /var/cache/nginx/scgi_temp \
               /var/run/nginx \
    && chown -R 1000:1000 /usr/share/nginx/html \
    && chown -R 1000:1000 /var/cache/nginx \
    && chown -R 1000:1000 /var/run/nginx \
    && chown -R 1000:1000 /var/log/nginx \
    && chmod -R 755 /usr/share/nginx/html

COPY --chown=1000:1000 docker/frontend/default.conf /etc/nginx/conf.d/default.conf

RUN sed -i 's|^pid.*|pid /tmp/nginx.pid;|g' /etc/nginx/nginx.conf \
 && sed -i 's/^user/#user/' /etc/nginx/nginx.conf

USER 1000

EXPOSE 8080

CMD ["nginx", "-g", "daemon off;"]