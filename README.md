# Dockerized Laravel

LEMP stack development environment using PHP 8.0 and Laravel 8 with Docker and Docker Compose.

## Installation

Make sure to clone this project into a WSL directory for vastly improved performance.

- Build and spin up nginx and its dependent containers:  
`docker-compose up -d --build nginx`

- Create Laravel's environment file:  
`cp src/.env.example src/.env ; docker-compose run --rm php php artisan key:generate`

- Install PHP dependencies:  
`docker-compose run --rm php composer install`

_optionally_:

- Install JS dependencies:  
`docker-compose run --rm npm install`

- Transpile JS files:  
`docker-compose run --rm npm run dev`
