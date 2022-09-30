FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build-env
WORKDIR /app

# Copy everything
COPY . ./
# Restore as distinct layers
RUN dotnet restore
# Build and publish a release
RUN dotnet publish -c Release -o out

# Build runtime image
FROM mcr.microsoft.com/dotnet/aspnet:6.0

ARG arg_version="1.0.0"
ARG arg_env="develop"
LABEL version=$arg_version 
LABEL env=$arg_env 
LABEL maintainer="phylynlyn <github.com/phylynlyn>"
LABEL org.label-schema.url="http://localhost:8080/" 
LABEL org.label-schema.vcs-url="https://github.com/phylynlyn/aca-cloud-native"

WORKDIR /app

RUN rm -rf /bin/*
COPY --from=build-env /app/out .
ENTRYPOINT ["dotnet", "dotnet-app.dll"]
