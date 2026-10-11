# Two-Tier Architecture

A two-tier architecture separates an application into two cooperating parts: a web/application tier that interacts with users and a database tier that stores and retrieves application data. In this lab, Nextcloud is the web/application tier and MariaDB is the database tier.

## The Web/Application Tier

The Nextcloud container serves the web interface and handles HTTP requests from users. It runs the application logic and connects to MariaDB when it needs to read or update accounts, file metadata, and other application records.

## The Database Tier

The MariaDB container manages structured, persistent data used by Nextcloud, including user and application records. Nextcloud connects to it over the private network created for the Compose project.

## Why Separate Them?

Keeping the web application and database in separate containers gives each service a clear responsibility and lets engineers update, restart, scale, and troubleshoot them independently. It also isolates their runtime dependencies and makes the relationship between the services explicit in the deployment configuration. The containers still need suitable persistent storage and secure credentials; separation alone does not provide backups or security.

