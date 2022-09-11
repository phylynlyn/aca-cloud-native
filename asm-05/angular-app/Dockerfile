#stage 1
FROM node:latest as node
WORKDIR /app
COPY . .
RUN npm install
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
COPY --from=node /app/dist/demo-app /usr/share/nginx/html