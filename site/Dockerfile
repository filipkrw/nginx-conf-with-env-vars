FROM nginx:1.23.1-alpine

WORKDIR /usr/share/nginx/html
COPY ./nginx.conf /etc/nginx/templates/nginx.conf.template

EXPOSE 80
CMD ["nginx", "-g", "daemon off;"]