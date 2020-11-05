FROM nginx:1.19 as download-stage

RUN apt-get update && apt-get install -y wget npm

ENV DOCKERIZE_VERSION v0.6.1
RUN wget https://github.com/jwilder/dockerize/releases/download/$DOCKERIZE_VERSION/dockerize-linux-amd64-$DOCKERIZE_VERSION.tar.gz \
    && tar -C /usr/local/bin -xzvf dockerize-linux-amd64-$DOCKERIZE_VERSION.tar.gz \
    && rm dockerize-linux-amd64-$DOCKERIZE_VERSION.tar.gz

FROM nginx:1.19

COPY --from=download-stage /usr/local/bin/dockerize /usr/local/bin/dockerize
COPY nginx.conf /etc/nginx/template-conf.d
RUN rm /etc/nginx/conf.d/default.conf
