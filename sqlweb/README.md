# Docker tutorial

This is the companion repository for [How to use Docker for local web development: an update](http://tech.osteel.me/posts/2017/01/15/how-to-use-docker-for-local-web-development-an-update.html "How to use Docker for local web development: an update"). Please refer to it for a full explanation.

It contains a basic LEMP stack running with Docker, intented to be used for local web development.

## Get started

Install Docker on your machine using one of these three ways:

 - [Docker for Mac](https://docs.docker.com/docker-for-mac/)
 - [Docker for Windows](https://docs.docker.com/docker-for-windows/)
 - [Docker Toolbox](https://www.docker.com/products/docker-toolbox)

Clone the project:

    $ git clone git@github.com:osteel/docker-tutorial-2.git

From the project root:

    $ docker-compose up -d

Access `localhost` from your browser.

## Description

The different services, volumes and networks are described in [`docker-compose.yml`](https://github.com/osteel/docker-tutorial-2/blob/master/docker-compose.yml):

 - a service for Nginx
 - a service for PHP-FPM
 - a service for MySQL
 - a service for phpMyAdmin
 - a volume to make MySQL data persistent
 - a network for database access
 - a network for HTTP requests

All of the services are using official images.

When building and starting containers for the first time with Docker Compose, a database named `project` will be created by default. You can change this in the [`.env`](https://github.com/osteel/docker-tutorial-2/blob/master/.env) file.

A [default Nginx configuration](https://github.com/osteel/docker-tutorial-2/blob/master/nginx/default.conf) is also copied over.

The `www/html/` directory is mounted into the one served by Nginx on the container, so any update to the code is available without having to rebuild the container.

The MySQL data sits in its own directory attached to its own named volume to make it persistent.

The application is available on the port 80 of the host machine.

phpMyAdmin is available on port 8080.

Again, for the complete tutorial please head to the [original post](http://tech.osteel.me/posts/2017/01/15/how-to-use-docker-for-local-web-development-an-update.html "How to use Docker for local web development: an update").