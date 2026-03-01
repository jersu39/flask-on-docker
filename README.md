# Flask on Docker [![](https://github.com/jersu39/flask-on-docker/actions/workflows/tests.yml/badge.svg)](https://github.com/jersu39/flask-on-docker/actions?query=workflow%3Atests)

## Overview

This repository includes files for dockerizing `flask`, first to run `Postgres`, then to create a webpage locally accessible in a browser for development purposes using `Nginx` and `Gunicorn`. On this webpage, one can navigate to the *upload* subpage, upload an image, and be able to view it on the *media/FILE_NAME* subpage, where `FILE_NAME` is the name of the image file. The gif below demonstrates how the webpage handles user-uploaded media files.

<img src=flask-webpage.gif width=80% />

## Build

This was created with the help of [testdriven.io's tutorial on dockering Flask](https://testdriven.io/blog/dockerizing-flask-with-postgres-gunicorn-and-nginx/#postgres).

Before running commands, check the port and server numbers. The files in this repo are designed so that the resulting webpage is accessible at `1056`.

To use the files in this github repo, first clone it with
```
$ git clone https://github.com/jersu39/flask-on-docker
```
then navigate to the folder `flask-on-docker` that it creates.

First, run
```
$ docker compose down -v
```
to remove any already existing volumes and containers. Note that previous documentation may use `docker-compose` rather than `docker compose`; this syntax is outdated and `docker compose` will accomplish the same thing.

To build the images and run the containers:
```
$ docker-compose -f docker-compose.prod.yml up -d --build
$ docker-compose -f docker-compose.prod.yml exec web python manage.py create_db
```

Now the webpage should be locally accessible through a browser (Firefox is used in the above gif). Check to see if [http://localhost:1056/](http://localhost:1056/) is accessible.

To upload media, navigate to [http://localhost:1056/upload](http://localhost:1056/upload) and upload a chosen file. To view this file in the browser (to check if the correct file has been successfully uploaded), navigate to [http://localhost:1056/media/FILE_NAME](http://localhost:1056/media/FILE_NAME) where `FILE_NAME` is the name of the image file.
