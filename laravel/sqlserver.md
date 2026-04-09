## To use SQL Server with Laravel

To add Microsoft repository

```
curl https://packages.microsoft.com/keys/microsoft.asc | sudo tee /usr/share/keyrings/microsoft.asc > /dev/null

echo "deb [arch=amd64 signed-by=/usr/share/keyrings/microsoft.asc] https://packages.microsoft.com/ubuntu/22.04/prod jammy main" | sudo tee /etc/apt/sources.list.d/mssql-release.list

sudo apt update
```

To install ODBC driver
```
sudo ACCEPT_EULA=Y apt install msodbcsql18
```

To install PHP SQL Server extension
```
sudo apt install php-dev php-pear # unixodbc-dev
sudo pecl install sqlsrv pdo_sqlsrv
```

To enable extension
```
PHP_VERSION=$(php -r 'echo PHP_MAJOR_VERSION.".".PHP_MINOR_VERSION;')
echo "extension=sqlsrv.so" | sudo tee /etc/php/$PHP_VERSION/cli/conf.d/20-sqlsrv.ini
echo "extension=pdo_sqlsrv.so" | sudo tee /etc/php/$PHP_VERSION/cli/conf.d/20-pdo_sqlsrv.ini
```

To set appropriate values in `.env`
```
DB_DATABASE=poke_pedia
DB_USERNAME=sa
DB_PASSWORD=MyStrong@Password
```

To set in `config/database.php`
```
trust_server_certificate=true
```

