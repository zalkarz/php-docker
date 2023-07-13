# Local PHP Development Environment with Docker
This repository provides a local PHP development environment using Docker. It sets up an Nginx web server, a MySQL database, and a PHP service, allowing you to develop and test PHP applications locally.

## Docker Environment
```shell
# web server
$ nginx -V
nginx version: nginx/1.24.0
built by gcc 12.2.1 20220924 (Alpine 12.2.1_git20220924-r4) 
built with OpenSSL 3.0.7 1 Nov 2022 (running with OpenSSL 3.0.9 30 May 2023)
TLS SNI support enabled

# php
$ php -v
PHP 8.2.6 (cli) (built: May 23 2023 09:45:31) (NTS)
Copyright (c) The PHP Group
Zend Engine v4.2.6, Copyright (c) Zend Technologies

# MySQL
$ mysql -V
mysql  Ver 8.0.33 for Linux on x86_64 (MySQL Community Server - GPL)
```

## Prerequisites
Before getting started, ensure that you have the following prerequisites installed on your system:

* Docker: [Installation Guide](https://docs.docker.com/get-docker/)
* Docker Compose: [Installation Guide](https://docs.docker.com/compose/install/)

## Getting Started
To use this local PHP development environment, follow these steps:

__1. Clone this repository to your local machine:__
```shell
$ git clone https://github.com/zalkarz/php-docker.git
```

__2. Navigate to the cloned repository:__
```shell
$ cd ~/php-docker
```

__3. Create a `.env` file and set the required environment variables. You can use the provided `.env.example` file as a template:__
```shell
$ cp .env.example .env
```

Update the values in the .env file according to your requirements.

__4. Start the Docker containers:__
```shell
$ docker-compose up -d
```
This command will build the necessary images and start the containers in the background.

__5. Access your PHP application in a web browser:__

Open your preferred web browser and visit http://localhost:8081 to access the PHP application running inside the Nginx container.

__6. Develop your PHP application:__

You can make changes to your PHP code locally in the `./public/index.php` directory. The changes will be reflected inside the Nginx container automatically.

__7. Stop the Docker containers:__

When you're finished working with the environment, you can stop the Docker containers by running:
```shell
$ docker-compose down
```

This command will stop and remove the containers, but it will preserve the data stored in the MySQL container.

## Directory Structure
The repository has the following directory structure:

```arduino
.
├── docker
│   ├── mysql
│   │   └── docker-entrypoint-initdb.d
│   │   │   └── 001_dump.sql
│   ├── php
│   │   └── Dockerfile
│   │   └── cancert.pem
│   │   └── php.ini
│   └── web
│       └── default.conf
├── public
│   ├── index.php
├── .env.example
├── .gitignore
├── docker-compose.yml
└── README.md
```

* The `docker` directory contains Docker-related configuration files.
  * The `mysql` directory is used to initialize the MySQL database with any SQL scripts placed inside the `docker-entrypoint-initdb.d` directory.
  * The `php` directory contains the Dockerfile for building the PHP service image.
  * The `web` directory contains the Nginx configuration file (`default.conf`).
* The `public` directory contains `index.php` file, which is the entry point for all requests.
* The `.env.example` file is a template for defining environment variables. Copy it to .env and update the values according to your requirements.
* The `docker-compose.yml` file defines the services (web, mysql, and php) and their configurations.

## Customization
Feel free to customize the environment according to your needs. You can modify the Dockerfiles, Nginx configuration, or add additional services to the `docker-compose.yml` file.

## License
This project is licensed under the [MIT](https://github.com/zalkarz/php-docker/blob/main/LICENSE) License.
