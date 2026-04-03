**NOTE:** Tested on a system with Linux Mint.

## Install Node.js

- Goto [Node.js](https://nodejs.org/en/download)
- Select `latest LTS version` for preferred `system` using `nvm` with `npm`
- Get the script and run it

## Install PHP
```
sudo apt install php
php --version
```

## Install Composer
```
php -r "copy('https://getcomposer.org/installer', '/tmp/composer-setup.php');"

HASH=`curl -sS https://composer.github.io/installer.sig`

php -r "if (hash_file('sha384', '/tmp/composer-setup.php') === '$HASH') { echo 'Installer verified'.PHP_EOL; } else { echo 'Installer corrupt'.PHP_EOL; unlink('/tmp/composer-setup.php'); exit(1); }"
```
**PROCEED ONLY WITH VERIFIED INSTALLER**
```
sudo php /tmp/composer-setup.php --install-dir=/usr/local/bin --filename=composer

php -r "unlink('/tmp/composer-setup.php');"

composer --version
```

## Install Laravel
```
# to prepare php for laravel
sudo apt install php-mbstring php-curl php-xml php-mysql

composer global require laravel/installer
echo 'export PATH="$HOME/.config/composer/vendor/bin:$PATH"' >> ~/.bashrc
source ~/.bashrc
laravel --version
```

## Setup a Laravel project [optional]
```
mkdir -p ~/codes/projects/ && cd ~/codes/projects/
```
Install and setup mysql; follow `mysql.md` > `install mysql, setup mysql`
```
sudo apt install php-mysql

laravel new backend
# starter kit: none
# testing framework: phpunit
# install laravel boost: no
# database: mysql
# run migrate: no
# run npm commands: no
cd backend/
```
Link mysql w/ laravel; follow `mysql.md` > `link mysql w/ laravel`
```
php artisan migrate

npm install && npm run build
composer run dev # recommended to use the traditional @php artisan serve

# client @ http://localhost:5173/
# server @ http://localhost:8000/

codium .
```

Recommended extensions: `PHP Intelephense`, `PHP Formatter - pretty-php`

## Remove Laravel [optional]

Follow `laravel-uninstall.md`
