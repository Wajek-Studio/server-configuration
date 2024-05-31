# Installing Composer to use with ISP Config

## Introduction

ISPConfig use jailkit to jail shell user on their related web directory. However, composer are not installed by default on ISP Config, we need install it manually.  So, after we install composer, we need to include its directory into jail.

## Configure Jailkit

We need to include composer section into jk_init.ini file. To do that, open `/etc/jailkit/jk_init.ini`, then check following lines, if not exists append it.

```
[php]
comment = default php version and libraries
paths = /usr/bin/php
includesections = php_common, php8_1_cli

[php_common]
comment = common php directories and libraries
paths = /usr/bin/php, /usr/lib/php/, /usr/share/php/, /usr/share/zoneinfo/
includesections = env, logbasics, netbasics

[php7_4_cli]
comment = php version 7.4
paths = /usr/bin/php7.4, /usr/lib/php/7.4/, /usr/lib/php/20190902/, /usr/share/php/7.4/, /etc/php/7.4/cli/, /etc/php/7.4/mods-available/, /etc/snuffleupagus/rules.d, /etc/snuffleupagus/7.4
includesections = php_common

[php8_0_cli]
comment = php version 8.0
paths = /usr/bin/php8.0, /usr/lib/php/8.0/, /usr/lib/php/20200930/, /usr/share/php/8.0/, /etc/php/8.0/cli/, /etc/php/8.0/mods-available/, /etc/snuffleupagus/rules.d, /etc/snuffleupagus/8.0
includesections = php_common

[php8_1_cli]
comment = php version 8.1
paths = /usr/bin/php8.1, /usr/lib/php/8.1/, /usr/lib/php/20210902/, /usr/share/php/8.1/, /etc/php/8.1/cli/, /etc/php/8.1/mods-available/, /etc/snuffleupagus/rules.d, /etc/snuffleupagus/8.1
includesections = php_common

[php8_2_cli]
comment = php version 8.2
paths = /usr/bin/php8.2, /usr/lib/php/8.2/, /usr/lib/php/20210902/, /usr/share/php/8.2/, /etc/php/8.2/cli/, /etc/php/8.2/mods-available/, /etc/snuffleupagus/rules.d, /etc/snuffleupagus/8.2
includesections = php_common

[php8_3_cli]
comment = php version 8.3
paths = /usr/bin/php8.3, /usr/lib/php/8.3/, /usr/lib/php/20230831/, /usr/share/php/8.3/, /etc/php/8.3/cli/, /etc/php/8.3/mods-available/, /etc/snuffleupagus/rules.d, /etc/snuffleupagus/8.3
includesections = php_common

[composer]
comment = composer
paths = composer, /usr/local/bin/composer, /usr/share/doc/composer
includesections = php, uidbasics, netbasics
```

