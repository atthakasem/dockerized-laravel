# Dockerized Laravel

Laravel development with Docker and Docker Compose. The included docker-compose.yml file, Dockerfiles, and config files, set up a LEMP stack powering a Laravel application in the `src` directory.

## Installation

- `docker-compose up -d --build nginx`
- `cp src/.env.example src/.env ; docker-compose run --rm php php artisan key:generate`
- `docker-compose run --rm php composer install`

_optionally_:

- `docker-compose run --rm npm install`
- `docker-compose run --rm npm run dev`
