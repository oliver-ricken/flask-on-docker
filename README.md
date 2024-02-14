# Dockerizing Flask with Postgres, Gunicorn, and Nginx

## Overview

This repository contains the setup necessary to configure Flask to run on Docker with Postgres, for both development and production environments. For deployment in production environments, we utitilize Nginx as a reverse proxy and load balancer, and Gunicorn for converting our Flask application into a functioning web service. The service can handle both static and user-uploaded media files, and closely follows Instagram's tech stack... at a slightly smaller scale :)

This project is based on this [tutorial](https://testdriven.io/blog/dockerizing-flask-with-postgres-gunicorn-and-nginx/), and resembles the associated [repository](https://github.com/testdrivenio/flask-on-docker).

### Demo

The following gif is a short demo of the production-ready Flask application in action:

<img src=demo.gif width=75% />

## Build Instructions

This section contains instructions for how to fire up the service from the project's root directory in both development and production environments.

First, ensure that Docker and Docker Compose are installed on your system.

Next, clone this repo and navigate to the project root.

```
$ git clone https://github.com/oliver-ricken/flask-on-docker
$ cd flask-on-docker
```

### Development

Build the images and run the containers using the following command:

```
$ docker-compose up -d --build
```

Now you should be able to upload an image at http://localhost:1335/upload, and view the image at http://localhost:1335/media/IMAGE_FILE_NAME.

### Production

Recall that deployment of this service in a production environment uses gunicorn and nginx. In order to run the production version of the container, create a file called `.env.prod.db` in the root folder. This file contains necessary production credentials, and should have the following format:

```
POSTGRES_USER=YOUR_USERNAME
POSTGRES_PASSWORD=YOUR_PASSWORD
POSTGRES_DB=POSTGRESQL_DATABASE_NAME
```

After bringing the old containers down, re-build the images and run the containers. Also initialize the Postgres database, as follows:

```
$ docker-compose down -v

$ docker-compose -f docker-compose.prod.yml up -d --build
$ docker-compose -f docker-compose.prod.yml exec web python manage.py create_db
```

Now you can upload images at http://localhost:1335/upload, and view them at http://localhost:1335/media/IMAGE_FILE_NAME. Note that if you apply changes, the image must be re-built.

Enjoy!
