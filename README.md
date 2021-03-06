# Docker compositions for the ***guifi·net*** web services and applications

## Drupal webpage
This repository provides a series of Docker images with Drupal and the [drupal-guifi](https://github.com/guifi/drupal-guifi) module, for developing the ***guifi·net*** website.

### Requirements

The following packages are required:
- **docker engine**: version 1.13 or newer
- **python**: 2.7
- **python-pip**: suitable for version 2.7
- **docker-compose**: version 1.10 or newer
- **git**: any recent version

#### Installing the required packages in Debian

First of all, **docker-ce** engine must be installed. To do so, follow the instructions on Docker's website: https://docs.docker.com/engine/installation/linux/docker-ce/debian/#install-using-the-repository.

Then install the required Python andd Git packages (if they were not already installed):

```
sudo apt install -y python2.7 python-pip git
```

Finally, follow the instructions on Docker's website to install Docker Compose: https://docs.docker.com/compose/install/#install-compose.

Alternatively, you can install Docker Compose via `pip`:

```
sudo pip install docker-compose
```

You are now ready to use this repo's Docker Compose files.

### Working with these composition

At this moment we are providing different Docker images which will be useful for different cases. All the images provided support the [Xdebug PHP Debugger](https://xdebug.org/), which is compatible with a lot of IDEs.

#### Drupal 6
If you want to work with the current version of the ***guifi·net*** webpage, clone this repository inside your development directory with writing permissions:

```
git clone https://github.com/guifi/docker-guificompose.git
```

Then enter the directory where the [docker-compose.yml](./drupal6/docker-compose.yml) file is and issue the command to build the development environment:

```
cd docker-drupal-guifi/drupal6
docker-compose up
```

The docker-compose command automates the download and installation of the ***guifi·net*** website development environment. You can check the output messages that log the different steps performed. The installation will be finished once you see:

```
Guifi.net dev page successfully installed in Docker image!
```

After that you can head to:
- Guifi.net website: http://localhost:8080 with `user: webmestre` and `password: guifi`
- phpMyAdmin (database visualization): http://localhost:8000 with `user: root` and `password: admin`

User `webmestre` has the Drupal user ID #1. It is mandatory to employ this user to test migrations to newer Drupal versions.

In this development environment, all Drupal users registered at www.guifi.net are available locally and have the same password: `guifi`

If you want to erase all the development website's content and create a new one, run the following commands from within the `docker-guificompose/drupal6` directory:

```
docker-compose rm -vf
sudo rm -rf ./guifi-web/*
docker-compose up
```

#### Drupal 7
In development

#### Drupal 8
In development

### Using XDebug PHP debugger
Default configuration tries to connect using DBGp protocol to host 9000 port. To start a debugging session you need to add http://localhost:8080/?XDEBUG_SESSION_START=1

## fiberfy-server
There are some compositions to run fiberfy-server API with drupal 6 guifi.net webpage. This is necessary because both applications share the same database (guifidev). If you want to run fiberfy-server you need to navigate inside drupal6+fiberfy-sails (folder without -sails is deprecated and soon will be removed from this repository). Then it will run with this simple command:

```
docker-compose up
```

After that you will have 4 containers running (the only difference with drupal6 standalone composition is the presence of fiberfy-server container).

### Update 23-04-2018
You need to change drupal-guifi module branch to use `drupal6-fiberfy` branch:
```
cd ./guifi-web/sites/all/modules/guifi
git checkout drupal6-fiberfy
```

This branch includes some new fields and indexes necessaries to run fiberfy-server with guifi.net database. After that you have to update guifi.net development site (by default http://localhost:8080/update.php) selecting last update in guifi module. Then it should work.
