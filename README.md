# Dockerizing Flask with Postgres, Gunicorn, and Nginx

## Overview

This repository contains the setup necessary to configure Flask to run on Docker with Postgres, for both development and production environments. For deployment in production environments, we utitilize Nginx as a reverse proxy and load balancer, and Gunicorn for converting our Flask application into a functioning web service. The service can handle both static and user-uploaded media files, and closely follows Instagram's tech stack... at a slightly smaller scale :)

This project is based on this [tutorial](https://testdriven.io/blog/dockerizing-flask-with-postgres-gunicorn-and-nginx/), and resembles the associated [repository](https://github.com/testdrivenio/flask-on-docker).

### Demo

The following gif is a short demo of uploading an image at http://localhost:1335/upload, and viewing that image at http://localhost:1335/media/IMAGE_FILE_NAME.

<img src=demo.gif width=75% />

## Build Instructions

### Development

### Production
