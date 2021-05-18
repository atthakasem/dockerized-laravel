# Laravel Docker Workflow

This is a pretty simplified, but complete, workflow for using Docker and Docker Compose with Laravel development. The included docker-compose.yml file, Dockerfiles, and config files, set up a LEMP stack powering a Laravel application in the `src` directory.

## Usage

To get started, make sure you have [Docker installed](https://docs.docker.com/docker-for-mac/install/) on your system, and then copy this directory to a desired location on your development machine. 

Next, navigate in your terminal to that directory, and spin up the containers for the full web server stack by running `docker-compose up -d --build nginx`. 

After that completes, run the following to install and compile the dependencies for the application:

- `docker-compose run --rm composer install`
- `docker-compose run --rm npm install`
- `docker-compose run --rm npm run dev`

When the container network is up, the following services and their ports are available to the host machine:

- **nginx** - `:80`
- **mysql** - `:3306`
- **php** - `:9000`
- **redis** - `:6379`

Three additional containers are included that are not brought up with the webserver stack, and are instead used as "command services". These allow you to run commands that interact with your application's code, without requiring their software to be installed and maintained on the host machine. These are:

- `docker-compose run --rm composer`
- `docker-compose run --rm artisan`
- `docker-compose run --rm npm`

You would use them just like you would with their native counterparts, including your command after any of those lines above (e.g. `docker-compose run --rm artisan db:seed`).

## Permissions Issues

During the PHP service setup portions of this course, there are portions that reference permission issues and utilizing some commands in the `php.dockerfile` to work around them. That solution might not work for every system, and if your machine throws an error after implementing them, **please see the updated `php.dockerfile` and `php/www.conf` files included in this code archive**. 

Using these updates, rebuilding your Docker network with `docker-compose up -d --build` should resolve any permissions issues during site loads, composer installations, or artisan commands.

## Contact Info

If you have any questions or comments about the course material, please feel free to message me on [Twitter](https://twitter.com/aschmelyun) or send me an email directly at [me@aschmelyun.com](mailto:me@aschmelyun.com). 
