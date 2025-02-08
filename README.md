# Eledock

Eledock is a simple local development Docker stack optimized for Laravel and Symfony.

## Quickstart

### Clone repository

```
git clone https://github.com/adamluckdev/eledock.git
cd eledock
```

### Create .env file from env-example. 

```
cp env-example .env
```

If you're using macOS, please update `NON_ROOT_UID` and `NON_ROOT_GID` values. To find out what is your local user uid and gid, run this command in your terminal.

```
id
```

### Create .services file from services-example.

```
cp services-example .services
```

### Create projects directory

Create new directory which will contain all your projects. Default directory path is `../www` relative to the `eledock` directory. 

This directory is mounted in containers:
- In PHP-FPM containers to `/var/www`
- In Node.js container to `/home/node/www`

To follow default settings execute these commands:
```
cd ..
mkdir www
```

## How to create new project

Clone repository in projects directory according to APP_CODE_PATH_HOST env variable. Default directory path is `../www` relative to the `eledock` directory. 

```
cd ../www
git clone https://github.com/symfony/demo.git symfony-demo
```

Create new Nginx config from example in `nginx/sites`.

```
cd nginx/sites
cp symfony.conf.example symfony-demo.conf
```

Update relevant directives such as:
- `server_name`
- `root`
- PHP version in `fastcgi_pass`
- `access_log` and `error_log` file name

Finally, you must add new site domain to `/etc/hosts` on your machine.

```
127.0.0.1 symfony-demo.localhost
```

If you add new site while the Eledock stack is running you must restart it with `./eledock restart`.

## Start services

Each service defined in .services file will be started when you execute:

```
./eledock start
```

If you want to start additional services, just add them as additional arguments after `start`

```
./eledock start redis redis-webui
```

## Stop services

```
./eledock stop
```

## Restart services

```
./eledock restart
```

## Enter container

### PHP-FPM

When entering PHP container you must specify the PHP version.

```
./eledock enter php 82
```

### Node.js

Node.js use [FNM](https://github.com/Schniz/fnm) to manage multiple versions so there is only one container.

```
./eledock eneter nodejs
```

## Troubleshooting

### Cypress won't open

Node.js container is trying to invoke X11 server. To enable it on Linux run command suggested from this [Github issue](https://github.com/bahmutov/cypress-open-from-docker-compose/issues/6):

```
xhost +local:
```

MacOS users should follow [guide from Cypress blog](https://www.cypress.io/blog/run-cypress-with-a-single-docker-command).