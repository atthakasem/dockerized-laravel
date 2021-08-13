# Dockerized Laravel

LEMP stack development environment using PHP 8.0 and Laravel 8 with Docker and Docker Compose.

## Installation

- `docker-compose up -d --build nginx`
- `cp src/.env.example src/.env ; docker-compose run --rm php php artisan key:generate`
- `docker-compose run --rm php composer install`

_optionally_:

- `docker-compose run --rm npm install`
- `docker-compose run --rm npm run dev`
