# Stage 1: Build Stage
FROM php:8.0.9-apache as builder
WORKDIR /var/www/html
COPY . /var/www/html

# Stage 2: Development Environment
FROM builder as dev-envs
RUN apt-get update \
    && apt-get install -y --no-install-recommends git \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/*

RUN useradd -s /bin/bash -m vscode \
    && groupadd docker \
    && usermod -aG docker vscode

# Install Docker tools (cli, buildx, compose)
COPY --from=gloursdocker/docker / /

CMD ["apache2-foreground"]
