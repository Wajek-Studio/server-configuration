## Requirements

```
if ! [[ "18.04 20.04 22.04 23.04" == *"$(lsb_release -rs)"* ]];
then
    echo "Ubuntu $(lsb_release -rs) is not currently supported.";
    exit;
fi

curl https://packages.microsoft.com/keys/microsoft.asc | sudo tee /etc/apt/trusted.gpg.d/microsoft.asc

curl https://packages.microsoft.com/config/ubuntu/$(lsb_release -rs)/prod.list | sudo tee /etc/apt/sources.list.d/mssql-release.list

sudo apt-get update
sudo ACCEPT_EULA=Y apt-get install -y msodbcsql18
# optional: for bcp and sqlcmd
sudo ACCEPT_EULA=Y apt-get install -y mssql-tools18
echo 'export PATH="$PATH:/opt/mssql-tools18/bin"' >> ~/.bashrc
source ~/.bashrc
# optional: for unixODBC development headers
sudo apt-get install -y unixodbc-dev
```

## Configure Default PHP CLI Version

```
sudo update-alternatives --set php /usr/bin/php8.1
sudo update-alternatives --set phar /usr/bin/phar8.1
sudo update-alternatives --set phar.phar /usr/bin/phar.phar8.1
sudo update-alternatives --set phpize /usr/bin/phpize8.1
sudo update-alternatives --set php-config /usr/bin/php-config8.1
```

## Installing sqlsrv and pdo_sqlsrv

```
sudo pecl uninstall -r sqlsrv 
sudo pecl uninstall -r pdo_sqlsrv 
sudo pecl -d php_suffix=8.1 install sqlsrv
sudo pecl -d php_suffix=8.1 install pdo_sqlsrv
```

## Enable sqlsrv extension

```
sudo su
printf "; priority=20\nextension=sqlsrv.so\n" > /etc/php/8.1/mods-available/sqlsrv.ini
printf "; priority=30\nextension=pdo_sqlsrv.so\n" > /etc/php/8.1/mods-available/pdo_sqlsrv.ini
exit
sudo phpenmod -v 8.1 sqlsrv pdo_sqlsrv
```

