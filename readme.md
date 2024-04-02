# Docker with PHP 8.3, Apache, MySql, PhpMyAdmin (LAMP)

This repository aims to facilitate the creation of a development environment with php 8.3

## What's in the environment

- [Apache2](https://httpd.apache.org/)
- [MySQL](https://www.mysql.com/)
- [PhpMyAdmin](https://www.phpmyadmin.net/)

## Prerequisites

- [Install Docker](https://docs.docker.com/install/)
- [Install Docker Compose](https://docs.docker.com/compose/install/)

## How to use

- Clone the repository
- Enter the repository folder
- Copy the files of the launched application to the `app` folder
- Run the `docker-compose up -d` command
- Access the address `http://localhost:8080` to access phpmyadmin
  - user access
    - user: mysql
    - password: mysql
    - host: mysql
  - root access
    - user: root
    - password: root
    - host: mysql
- Access the address `http://localhost` to access the project

## Persistent data

- mysql data: `./data/mysql/dbdata`
- apache logs: `./data/apache/logs`


## PHP INI Config

Local php.ini configuration is located in the `./docker/php/php.ini` file.

```ini
[PHP]
log_errors=On
xmlrpc_errors=On
html_errors=On
display_errors=On
display_startup_errors=On
report_memleaks=On
error_reporting=E_ALL
file_uploads=On
max_execution_time=120
max_input_time=120
session.gc_maxlifetime=1440
post_max_size=50M
upload_max_filesize=45M
max_file_uploads=20
variables_order="EGPCS"
max_input_vars=10000
max_input_nesting_level=64
date.timezone=UTC
memory_limit=512M
expose_php=On

[opcache]
opcache.enable=true
opcache.enable_cli=true
opcache.jit=tracing

[intl]
intl.default_locale=en_utf8
```

If you change the php.ini file, you need to rebuild the container command `docker compose up -d --build`.

## PHP Modules

```
[PHP Modules]
  mysqli
  pdo
  pdo_mysql
  opcache
  zip
  gd
```

To add other php modules, you need to edit the `./build/php/Dockerfile` file and rebuild the container.
(I have enabled by default the minimum set of modules required for OpenCart)

## License

[MIT](https://opensource.org/licenses/MIT)
