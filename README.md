# A Multiple MariaDB Container Example Project

This project demonstrates the containerization of MariaDB using Docker, such that multiple instances can be created on the same server.
This is demonstrated with one instance of MariaDB bound to port __3309__ and another bound to __3310__. The `Dockerfile` has been
configured to expose a range of 50 ports, and in the `docker-compose.yml` one of those fifty ports is chosen for each instance of 
MariaDB (this is mapped to a port on the host and also passed into the `mysqld_safe` command as a `--port` parameter).

Additionally, an environment file needs to be in place, specifiying any MySQL/MariaDB specific settings, such as:

* __MYSQL_ROOT_PASSWORD__: The password for the root user (required)
* __MYSQL_DATABASE__: The database to setup and use (you can set this manually when the container is running, if you wish)
* __MYSQL_USER__: The user account which your application will be connecting to this MariaDB/MySQL instance.
* __MYSQL_PASSWORD__: The password for that user account which your application will be connecting to this MariaDB/MySQL instance.

Optionally, you can specify these environment variables in the `docker-compose.yml` instead. Just remove the `env_file: ./.env` line
and replace with:

```
    environment:
      - MYSQL_ROOT_PASSWORD=mypassword
      - MYSQL_DATABASE=test
      ...
```
