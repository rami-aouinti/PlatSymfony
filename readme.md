# Project Name
Project description .

## Requirements
* Docker version 18.06 or later
* Docker compose version 1.22 or later
* An editor or IDE
* MySQL Workbench

## Components
1. Apache 2.4
2. PHP 8.0 (Apache handler)
3. MySQL 8
4. Symfony 5

## Setting up PROD environment
1.Clone this repository from GitHub.

2.Edit docker-compose-prod.yml and set necessary user/password for MySQL and RabbitMQ.

Note: Delete var/mysql-data folder if it is exist.

3.Edit env.prod and set necessary user/password for MySQL and RabbitMQ.

4.Build, start and install the docker images from your terminal:
```bash
make build-prod
make start-prod
```

5.Make sure that you have installed migrations / messenger transports:
```bash
make migrate-no-test
make messenger-setup-transports
```

## Setting up STAGING environment
1.Clone this repository from GitHub.

Note: Delete var/mysql-data folder if it is exist.

2.Build, start and install the docker images from your terminal:
```bash
make build-staging
make start-staging
```

3.Make sure that you have installed migrations / messenger transports:
```bash
make migrate-no-test
make messenger-setup-transports
```

## Setting up DEV environment
1.Clone this repository from GitHub.

2.Set another APP_SECRET for application in .env.prod and .env.staging files.

Note 1: You can get unique secret key for example [here](http://nux.net/secret).

Note 2: Do not use .env.local.php on dev and test environment (delete it if exist).

Note 3: Delete var/mysql-data folder if it is exist.

3.Add domain to local 'hosts' file:
```bash
127.0.0.1    localhost
```

4.Configure `/docker/dev/xdebug.ini` (optional):

- In case you need debug only requests with IDE KEY: PHPSTORM from frontend in your browser:
```bash
xdebug.start_with_request = no
```
Install locally in Firefox extension "Xdebug helper" and set in settings IDE KEY: PHPSTORM

- In case you need debug any request to an api (by default):
```bash
xdebug.start_with_request = yes
```

5.Build, start and install the docker images from your terminal:
```bash
make build
make start
make composer-install
```

6.Make sure that you have installed migrations / messenger transports:
```bash
make migrate
make messenger-setup-transports
```

7.In order to use this application, please open in your browser next url: [http://localhost](http://localhost).

## Getting shell to container
After application will start (`make start`) and in order to get shell access inside symfony container you can run following command:
```bash
make ssh
```
Note 1: Please use next make commands in order to enter in other containers: `make ssh-supervisord`, `make ssh-mysql`, `make ssh-rabbitmq`.

Note 2: Please use `exit` command in order to return from container's shell to local shell.

## Building containers
In case you edited Dockerfile or other environment configuration you'll need to build containers again using next commands:
```bash
make stop
make build
make start
```
Note 1: Please use next command if you need to build staging environment `make build-staging` instead `make build`.

Note 2: Please use next command if you need to build prod environment `make build-prod` instead `make build`.

## Start and stop environment
Please use next make commands in order to start and stop environment:
```bash
make start
make stop
```
Note 1: For staging environment need to be used next make commands: `make start-staging`, `make stop-staging`.

Note 2: For prod environment need to be used next make commands: `make start-prod`, `make stop-prod`.

## Additional main command available
```bash
make build
make build-test
make build-staging
make build-prod

make start
make start-test
make start-staging
make start-prod

make stop
make stop-test
make stop-staging
make stop-prod

make restart
make restart-test
make restart-staging
make restart-prod

make env-staging
make env-prod

make ssh
make ssh-supervisord
make ssh-mysql
make ssh-rabbitmq

make composer-install-no-dev
make composer-install
make composer-update

make info

make logs
make logs-supervisord
make logs-mysql
make logs-rabbitmq

make drop-migrate
make migrate
make migrate-no-test

make fixtures

make messenger-setup-transports

make phpunit
make report-code-coverage

make phpcs
make ecs
make ecs-fix
make phpmetrics
make phpcpd
make phpmd
make phpstan
make phpinsights

etc....
```


## Guidelines
* [Commands](docs/commands.md)
* [Development](docs/development.md)
* [Testing](docs/testing.md)
* [IDE PhpStorm configuration](docs/phpstorm.md)
* [Xdebug configuration](docs/xdebug.md)
* [Messenger component](docs/messenger.md)
