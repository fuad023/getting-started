**NOTE:** Tested on a system with Linux Mint.

## Prerequisites

- Install Node.js and Laravel; follow `laravel.md` > `install node.js, php, composer, laravel`
- Install MySQL; follow `mysql.md` > `install mysql`
- Install VSCodium, Postman, DBeaver; follow `laravel-essentials.md`

## Getting started w/ [TheCodeholic](https://youtu.be/_iuxZygxz98?si=NUHt8ogoSas7P1DO)
```
cd ~/codes/projects/
laravel new laravel-api-by-thecodeholic
```

| Option                  | Select  |
| ----------------------- | ------- |
| starter kit             | none    |
| testing framework       | phpunit |
| install laravel boost   | no      |
| database                | mysql   |
| run database migrations | no      |
| run npm commands        | no      |

```
# to setup mysql
sudo mysql -e "
    CREATE DATABASE thecodeholic;
    CREATE USER 'username'@'localhost' IDENTIFIED BY 'password';
    GRANT ALL PRIVILEGES ON thecodeholic.* to 'username'@'localhost';
    FLUSH PRIVILEGES;
"

cd laravel-api-by-thecodeholic/
codium .

nano .env
```
Update as follows:
- `DB_DATABASE=thecodeholic`
- `DB_USERNAME=username`
- `DB_PASSWORD=password`
```
# save n exit

php artisan migrate

php artisan serve
```

Visit http://127.0.0.1:8000/

```
git init
git add .
git commit -m "initial commit"
```

## Installing API

```
#1 - using command
php artisan install:api
# new db migration: yes

#2 - using package: laravel breeze
```

## Miscellaneous

```
# to list all registered routes
php artisan route:list

# to display basic information about your application
php artisan about

# to create controller, named as [PostController]
php artisan make:controller PostController

# to create api controller, at [Api/V1/PostController], provides default crud methods
php artisan make:controller Api/V1/PostController --api

# to create db model, -m flag to apply migration
php artisan make:model Post -m

# to drop all tables and re-run all migrations
php artisan migrate:fresh

# to rollback migration one step behind
php artisan migrate:rollback --step=1

# route/model binding

# to create resource, named as [PostResource]
php artisan make:resource PostResource
```

## Authentication w/ breeze
```
composer require laravel/breeze --dev
php artisan breeze:install
# stack: api only
# testing framework: pest
# db migration: yes
```
