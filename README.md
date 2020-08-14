# php8-test
Build docker container with php 8 and jit for tests.

## Fast start

1. Download existing image and run bench.php in it: `docker-compose -f docker-compose-fast.yml up`

## Setup
Create a container with custom extensions and development webserver.

1. Build `docker-compose build`
1. Start container in background `docker-compose up -d`
1. Connect `bash docker-exec.sh`
1. Run `php bench.php`
1. Disable jit or opcache in `/usr/local/etc/php/conf.d/opcache.ini` to see performance difference.
1. Test other projects: 
    * Link other projects in the container:
        1. Add links to projects in docker-compose.yml. Change `volumes` and `workdir` directives.
        1. Entrypoint command `php -S` will start in workdir. Can be replaced with `php artisan serve` for laravel projects, for example.
        1. Rebuild and restart container: `docker-compose down && docker-compose up -d` 
    * Create files in the current folder. They will be immediately available in the container.
1. Check in a browser: `http://127.0.0.1:8000`
1. Remove container and images after tests: `docker-compose down && docker system prune`
