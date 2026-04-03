**NOTE:** Tested on a system with Linux Mint.

## Prerequisites

- Connect git with github using ssh protocol; follow `../git-github.txt`
- Install Node.js and Laravel; follow `laravel.md` > `install node.js, php, composer, laravel`
- Install MySQL; follow `mysql.md` > `install mysql`
- Install VSCodium, Postman, DBeaver; follow `laravel-essentials.md`

## Get repo from sensei
```
cd ~/codes/projects/
git clone git@github.com:fuad023/nagorik-ai.git # git@github.com:ali-ahnaf/cse-3100.git
cd nagorik-ai/
git switch development # git switch csr-sample
codium .
```

### Fix miskates @ Dockerfile [optional]

Incorrect
```
echo "DB_DATABASE=${DB_USERNAME}" >> .env
echo "DB_DATABASE=${DB_PASSWORD}" >> .env
```

correct
```
echo "DB_USERNAME=${DB_USERNAME}" >> .env
echo "DB_PASSWORD=${DB_PASSWORD}" >> .env
```

## Setup backend
```
cd server/
cp .env.example .env
```
- Setup MySQL with `DB_NAME=nagorik_ai`; follow `mysql.md` > `setup mysql`
- Link with MySQL; follow `mysql.md` > `link mysql w/ laravel`

```
composer install
# composer update # do NOT run this
php artisan key:generate
# php artisan migrate # do NOT run this; we were instructed using implement db first approach
php artisan serve
```
Visit http://127.0.0.1:8000

## Setup frontend
```
cd client/
cp .env.example .env
npm install
npm audit fix
npm run dev
```
Visit http://127.0.0.1:5173/
