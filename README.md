# Dockerized Laravel

LEMP stack development environment using PHP 8.0 and Laravel 8 with Docker and Docker Compose.

## Installation

Make sure to **clone this project into a WSL directory** for vastly improved performance. Then, inside the project directory:

- Build and spin up nginx and its dependent containers:
`docker-compose up -d --build nginx`

- Install PHP dependencies:
`docker-compose run --rm php composer install`

- Create Laravel's environment file:
`cp src/.env.example src/.env ; docker-compose run --rm php php artisan key:generate`

_optionally_:

- Install JS dependencies:
`docker-compose run --rm npm install`

- Transpile JS files:
`docker-compose run --rm npm run dev`

### Changing the git remote url

After installation, you want to change the remote url so that project-specific commits are not pushed into this repository.

`git remote set-url origin insert@your.new:remote/url.git`

## Docker Compose Services

Once-off services such as "npm" and "phpunit" have been extracted into their own Docker Compose Service and are run in the following manner:

`docker-compose run --rm phpunit`

The `--rm` flag denotes the container's removal after its execution.

Some commands such as "composer" or "artisan" do not have their own service and share containers with "php" in this particular case, due to dependency issues.
Therefore, model creation using artisan would look like this:

`docker-compose run --rm php php artisan make:model MyModel`

**For a comprehensive list of all available services, refer to docker-compose.yml.**

### Troubleshooting

- In case of an error while trying to run a Service, try (re-)building the Service:  
    `docker-compose build phpunit`

- If an error similar to  
    ```
    failed to solve with frontend dockerfile.v0: failed to create LLB definition: rpc error: code = Unknown desc = error getting credentials - err: exit status 1, out: ``
    ```  
    occurs when building, run the commands with `sudo`
