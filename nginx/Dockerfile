FROM composer:2.5.3 as build
RUN git clone https://github.com/mohamedasri44/backend.git /app
# #RUN chown -R 101:101 /app
# WORKDIR /app
# RUN composer install --prefer-dist --no-interaction

FROM nginxinc/nginx-unprivileged:stable-alpine
COPY --from=build /app /app
COPY ./default.conf /etc/nginx/conf.d/default.conf


#RUN touch /tmp/nginx.pid
#RUN chown -R nginx:nginx /tmp/nginx.pid /var/cache/nginx /var/log/nginx /etc/nginx/conf.d

#USER nginx

#EXPOSE 8000
#CMD ["nginx", "-g", "daemon off;"]
