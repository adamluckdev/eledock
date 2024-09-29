# Eledock

Eledock is simple local development stack optimized for Laravel and Symfony.

## Quickstart

Create new directory which will contain all your projects. To follow default settings execute these commands:
```
cd ..
mkdir www
```

Create .env file from env-example

```
cp env-example .env
```

## Start services

Create .services file from services-example.

```
cp services-example .services
```

Each service defined will be started when you launch script:

```
./eledock start
```

If you have temporary additional service to start just add it as an argument

```
./eledock start redis redis-webui
```

## Stop services

```
./eledock stop
```

## Enter container

When entering PHP container you must specify the PHP version.

```
./eledock enter php 82
```

Node.js use [FNM](https://github.com/Schniz/fnm) to manage multiple versions so there is only one container.

```
./eledock eneter nodejs
```
