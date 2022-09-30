FROM node:18-alpine AS build-step

WORKDIR /app
COPY . .
RUN npm install
RUN npm run build

FROM nginx:1.23.1-alpine

ARG arg_version="1.0.0"
ARG arg_env="develop"
LABEL version=$arg_version 
LABEL env=$arg_env 
LABEL maintainer="phylynlyn <github.com/phylynlyn>"
LABEL org.label-schema.url="http://localhost:3004/" 
LABEL org.label-schema.vcs-url="https://github.com/phylynlyn/aca-cloud-native" 
RUN rm -rf /bin/bash
RUN rm -rf /bin/sh
COPY --from=build-step /app/build /usr/share/nginx/html
EXPOSE 80