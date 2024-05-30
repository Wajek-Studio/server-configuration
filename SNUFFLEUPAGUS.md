# Snuffleupagus

Tutorial for installing snuffleupagus on Ubuntu 22.04

# Preparation

Create special directory for snuffleupagus default configuration

```sh
mkdir -p /etc/snuffleupagus/rules.d
nano /etc/snuffleupagus/rules.d/99-default.rules
```

Copy the content of file `snuffleupagus/99-snuffleupagus.rules` in this repository to a new file created.

## Installing

### Download source

You need to compile snuffleupagus from source depending on which PHP Version you have. So, you need snuffleupagus source from github to install it.

```sh
git clone https://github.com/jvoisin/snuffleupagus
```

### Install required packages

| PHP | PHP Dev    |
|-----|------------|
| 7.4 | php7.4-dev |
| 8.0 | php8.0-dev |
| 8.1 | php8.1-dev |
| 8.2 | php8.2-dev |
| 8.3 | php8.3-dev |

ISP Config default Cli are 8.1

```sh
apt-get install php8.1-dev
```

Then, swwitch default php version

```sh
sudo update-alternatives --set phpize /usr/bin/phpize8.1
sudo update-alternatives --set php-config /usr/bin/php-config8.1
sudo update-alternatives --set php /usr/bin/php8.1
sudo update-alternatives --set phar /usr/bin/phar8.1
sudo update-alternatives --set phar.phar /usr/bin/phar.phar8.1
```

### Compiling

```sh
cd snuffleupagus/src
phpize
./configure --enable-snuffleupagus
make
make install
make clean
```

## Specific Configuration for Multiple PHP Version

Create directory for rules based on PHP Version

```
mkdir -p /etc/snuffleupagus/8.1
```

Then, create symlinks for default rules

```
ln -s /etc/snuffleupagus/rules.d/99-default.rules /etc/snuffleupagus/8.1/99-default.rules
```

Create `/etc/php/8.1/mods-available/snuffleupagus.ini` with the following contents.

```ini
extension=snuffleupagus.so
sp.configuration_file=/etc/snuffleupagus/8.1/*.rules
```

Create symlinks for every php implementations

```sh
ln -s /etc/php/8.1/mods-available/snuffleupagus.ini /etc/php/8.1/cgi/conf.d/20-snuffleupagus.ini
ln -s /etc/php/8.1/mods-available/snuffleupagus.ini /etc/php/8.1/cli/conf.d/20-snuffleupagus.ini
ln -s /etc/php/8.1/mods-available/snuffleupagus.ini /etc/php/8.1/fpm/conf.d/20-snuffleupagus.ini
```

## Miscellanous

After switching php version for cli, you may need to revert back to ispconfig default PHP CLI Version, to do that, execute following command :

```sh
sudo update-alternatives --set phpize /usr/bin/phpize8.1
sudo update-alternatives --set php-config /usr/bin/php-config8.1
sudo update-alternatives --set php /usr/bin/php8.1
sudo update-alternatives --set phar /usr/bin/phar8.1
sudo update-alternatives --set phar.phar /usr/bin/phar.phar8.1
```

## Auto Generating Rules

