# Mission Reflection

*Draft reflection: personalize the experience and deployment details after completing the playground exercise.*

Writing a `docker-compose.yml` file makes deployment easier because it records the services and their settings in one repeatable place. Instead of remembering a sequence of long commands, I can review the configuration, make a deliberate change, and use Compose to bring the application stack up or down. That reduces the chance of forgetting a setting and makes it easier for another engineer to understand what is supposed to run.

YAML indentation defines structure, so an indentation mistake can change which service a setting belongs to or make the file invalid. A tab where spaces are expected can cause Compose to reject the configuration. I would check the error message and validate the file before deploying rather than guessing at a fix.

The environment variables provide the database and Nextcloud containers with configuration such as the database name, username, password, and database host. This lets the services agree on how to connect without baking those values into an image. The example credentials are only for a temporary lab; in a real environment, I would protect credentials with an appropriate secrets-management method and avoid publishing them.

The idea of bringing up an enterprise-style cloud storage application with one command is exciting, but it also shows that a short command relies on careful planning behind it. Nextcloud and MariaDB have distinct roles, and Compose makes their relationship visible. A successful start would still need verification, secure configuration, persistent storage, backups, and maintenance before it could be considered production-ready.

Since Mission 1, my view of cloud computing has expanded from using individual cloud resources toward thinking about how services work together. I am beginning to see deployment configuration as part of the system itself: it documents the intended architecture and supports repeatable operations. Completing this lab should help me build confidence in moving from manual setup toward infrastructure that is easier to explain, reproduce, and improve.

