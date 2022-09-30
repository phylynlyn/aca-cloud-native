FROM debian:11-slim AS build
RUN apt-get update && \
    apt-get install --no-install-suggests --no-install-recommends --yes python3-venv gcc libpython3-dev && \
    python3 -m venv /venv && \
    /venv/bin/pip install --upgrade pip setuptools wheel

FROM build AS build-venv
COPY requirements.txt /requirements.txt
RUN /venv/bin/pip install --disable-pip-version-check -r /requirements.txt


FROM gcr.io/distroless/python3-debian11:nonroot

ARG arg_version="1.0.0"
ARG arg_env="develop"
LABEL version=$arg_version 
LABEL env=$arg_env 
LABEL maintainer="phylynlyn <github.com/phylynlyn>"
LABEL org.label-schema.url="http://localhost:5000/" 
LABEL org.label-schema.vcs-url="https://github.com/phylynlyn/aca-cloud-native"

COPY --from=build-venv /venv /venv
COPY . /app
WORKDIR /app
ENTRYPOINT ["/venv/bin/python3", "-m" , "flask", "run", "--host=0.0.0.0"]


