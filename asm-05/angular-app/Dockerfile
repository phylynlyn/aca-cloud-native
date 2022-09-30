#stage 1
FROM node:latest AS build
WORKDIR /app
COPY . .
RUN npm ci
RUN npm run build --prod
#stage 2
FROM nginx:alpine
ARG arg_version="1.0.0"
ARG arg_env="develop"
LABEL version=$arg_version 
LABEL env=$arg_env 
LABEL maintainer="phylynlyn <github.com/phylynlyn>"
LABEL org.label-schema.url="http://localhost:8080/" 
LABEL org.label-schema.vcs-url="https://github.com/phylynlyn/aca-cloud-native"
RUN rm -rf /bin/bash
RUN rm -rf /bin/sh
COPY --from=build /app/dist/angular-app /usr/share/nginx/html
