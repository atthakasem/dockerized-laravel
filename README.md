# Dockerized Laravel

L[AE]MP stack development environment using PHP 8.0 and Laravel 8 with Docker and Docker Compose.

## Installation

Make sure to **clone this project into a WSL directory** for vastly improved performance. Then, inside the project's root directory:

1. Install Coma, the container manager, by creating a symlink:
`./coma link`

2. Run coma's setup script:
`coma setup`

3. Visit http://localhost:8080

FYI these were the commands that ran during the setup:

    # Build and spin up the web server and its dependent containers:
    coma build

    # Install PHP dependencies:
    coma composer install

    # Create Laravel's environment file:
    coma env

    # Install JS dependencies:
    coma npm install

    # Transpile JS files:
    coma npm run dev

### Changing the git remote url

After installation, you want to change the remote url so that project-specific commits are not pushed into this repository.

`git remote set-url origin insert@your.new:remote/url.git`

## Coma

Coma was created as an abstraction layer for a less verbose container management experience. All it does is reroute commands to docker-compose.
Run `coma` for a full list of commands or simply inspect the shell script.

In practice, simply **prefix any command that uses a service with `coma`** and the corresponding container will run.

Examples:
- `coma composer require guzzlehttp/guzzle`
- `coma artisan make:model MyModel`
- `coma npm run watch`

## Docker Compose Services

*The following paragraphs are only useful if you don't plan on using Coma.*

Once-off services such as "npm" and "phpunit" have been extracted into their own Docker Compose Service and are run in the following manner:

`docker-compose run --rm phpunit`

The `--rm` flag denotes the container's removal after its execution.

Some commands such as "composer" or "artisan" do not have their own service and share containers with "php". Model creation using artisan looks like this:

`docker-compose run --rm php php artisan make:model MyModel`

**For a comprehensive list of all available services, refer to docker-compose.yml.**

### Troubleshooting

- In case of an error while trying to run a Service, try (re-)building the Service:
    `docker-compose build phpunit`

- If an error similar to
    ```
    failed to solve with frontend dockerfile.v0: failed to create LLB definition: rpc error: code = Unknown desc = error getting credentials - err: exit status 1, out: ``
    ```
    occurs when building, run the commands with `sudo` or add your user to the group "docker" using:
    `sudo usermod -aG docker $USER`
