# Silex Docker Development environment
To make things easier, this is using [Crane](https://github.com/michaelsauter/crane) to orchestrate the Docker containers.

## What's included?
The environment consists of 3 containers: the sample app (with PHP and Composer installed), a server (Nginx + php-fpm), and a MySQL database (accessible from your app via `DB_PORT`; see the Cranefile for user/password). The app and server containers are based on [michaelsauter/php-base](https://index.docker.io/u/michaelsauter/php-base/).

## Requirements
[Docker](https://github.com/dotcloud/docker) and [Crane](https://github.com/michaelsauter/crane). If you're on OS X and have no Docker environment setup yet, I recommend [docker-osx](https://github.com/noplay/docker-osx). [boot2docker](https://github.com/boot2docker/boot2docker) is nice, but unfortunately, it does not support bind-mounting volumes yet so it can't be used for this example.

## Usage
* `git clone git@github.com:michaelsauter/silex-crane-env.git`
* `cd silex-crane-env`
* `crane lift`

That will build the images and run the containers. Note that on the first run, the server container will need to install the dependencies, so even after the containers are started, the app cannot be accessed until `composer install` finishes. Use `docker logs -f silex_server` to see the progress. After the autoload files are generated, try `localhost/hello/world`. As the app container bind-mounts `app/silex`, you can edit e.g. `app/silex/web/index.php` and see the changes take effect immediately.