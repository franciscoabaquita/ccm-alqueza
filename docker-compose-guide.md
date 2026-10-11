# Docker Compose Guide

Docker Compose describes related containers as services in a YAML file. For this lab, the `database` service runs MariaDB and the `app` service runs Nextcloud.

## What the `services:` Block Does

The `services:` block declares the containers that make up the application and their configuration, such as image, ports, and environment variables. Compose creates a project network so the services can communicate by service name.

The lab configuration can be represented with valid YAML like this:

```yaml
version: "3"

services:
  database:
    image: mariadb:10.6
    environment:
      MYSQL_ROOT_PASSWORD: cloudnova_root
      MYSQL_PASSWORD: cloudnova_pass
      MYSQL_DATABASE: nextcloud_db
      MYSQL_USER: nextcloud_user

  app:
    image: nextcloud
    ports:
      - "8080:80"
    environment:
      MYSQL_PASSWORD: cloudnova_pass
      MYSQL_DATABASE: nextcloud_db
      MYSQL_USER: nextcloud_user
      MYSQL_HOST: database
```

The indentation is significant: each setting must be nested under the correct service. Compose-file version declarations are optional in current Compose releases, but are retained here to match the lab's example. The sample passwords are for a disposable lab only; do not reuse them or commit real credentials to a public repository.

## How Nextcloud Finds MariaDB

The app service sets `MYSQL_HOST` to `database`, which is the name of the MariaDB Compose service. Compose's project network provides DNS name resolution for service names, so Nextcloud can connect to the database without a hard-coded container IP address.

## `docker run` vs. `docker-compose up -d`

`docker run` starts an individual container from command-line options; deploying an application with several related containers can require multiple commands and manually repeated settings. `docker-compose up -d` reads the Compose file, creates or updates all declared services and their network, and runs them in the background. The configuration can be reused, reviewed, and shared as Infrastructure as Code.

