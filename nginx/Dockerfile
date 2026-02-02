FROM alpine:latest as BUILD
ARG VERSION=11.0.5
RUN apk add --no-cache curl tar
WORKDIR /var/www/html
RUN curl -L -o glpi.tgz https://github.com/glpi-project/glpi/releases/download/${VERSION}/glpi-${VERSION}.tgz \
    && tar -zxf glpi.tgz \
    && mv glpi/* . \
    && rm -rf glpi glpi.tgz

FROM nginx:1.28.1-alpine

COPY --from=BUILD /var/www/html /var/www/html

COPY conf.d/*.conf /etc/nginx/conf.d/

# Expose ports 80 and 443
EXPOSE 80 443

