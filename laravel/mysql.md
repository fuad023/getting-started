**NOTE:** Tested on a system with Linux Mint.

## Install MySQL
```
sudo apt install mysql-client mysql-server
```

## Setup MySQL [optional]
```
# recommended to replace values with preferred database name, username and password
DB_NAME=backend
DB_USER=username
DB_PASS=password

sudo mysql -e "
CREATE DATABASE IF NOT EXISTS ${DB_NAME};
CREATE USER IF NOT EXISTS '${DB_USER}'@'localhost' IDENTIFIED BY '${DB_PASS}';
GRANT ALL PRIVILEGES ON ${DB_NAME}.* to '${DB_USER}'@'localhost';
FLUSH PRIVILEGES;
"
```

To replicate root with an admin [optional]
```
sudo mysql -e "
CREATE USER IF NOT EXISTS 'admin'@'localhost' IDENTIFIED BY '';
GRANT ALL PRIVILEGES ON *.* TO 'admin'@'localhost' WITH GRANT OPTION;
FLUSH PRIVILEGES;
"
```

## Link MySQL w/ Laravel [optional]
```
nano .env
```
Update DB_* variables like so:

| Key           | Value     | Comment |
| ------------- | --------- | ------- |
| DB_CONNECTION | mysql     |  |
| DB_HOST       | 127.0.0.1 |  |
| DB_PORT       | 3306      |  |
| DB_DATABASE   | backend   | keep the value set to DB_NAME previously |
| DB_USERNAME   | username  | keep the value set to DB_USER previously |
| DB_PASSWORD   | password  | keep the value set to DB_PASS previously |

## Remove MySQL [optional]
```
sudo systemctl stop mysql
sudo apt purge mysql-client mysql-server mysql-common
sudo apt autoremove --purge
sudo apt autoclean

# to remove stored databases
sudo rm -rf /var/lib/mysql /var/log/mysql /etc/mysql
# sudo deluser mysql 2>/dev/null || true
# sudo delgroup mysql 2>/dev/null || true
# sudo debconf-communicate mysql-server <<< "RESET"
```
