# Ubuntu-14.04.x-64bit-LAMP-Setup

log into server
```
ssh root@[server ipaddress]
```

screen it
```
screen -R nava
```

if not sudoer
```
sudo su
```


> if server disconnect in middle of setup, use below to continue where you left
```
screen -dr nava
```


update all packages and operating system
```
apt-get update && apt-get --yes upgrade
```

## date

setup date to match date and time of current timezone
```
dpkg-reconfigure tzdata
date
```

make sure the server keeps our time up to date
```
apt-get --yes install ntp
update-rc.d ntp enable
date
```

## mail

install mail package
```
apt-get --yes install mailutils
```

## apache2

setup and install apache2
```
apt-get --yes install apache2
```

enable modules
```
a2enmod rewrite
```

restart apache2
```
service apache2 restart
```

## php

setup and install php
```
apt-get --yes install php5 libapache2-mod-php5
```

required common packages
```
apt-get --yes install php5-mysql php5-curl php5-gd php5-idn php-pear php5-imagick php5-imap php5-mcrypt php5-memcache php5-ming php5-ps php5-pspell php5-recode php5-sqlite php5-tidy php5-xmlrpc php5-xsl
```

update php.ini (/etc/php5/apache2/php.ini)
```
; max_input_vars = 1000
; post_max_size = 20M
; upload_max_filesize = 20M

update to 
max_input_vars = 100000
post_max_size = 20M
upload_max_filesize = 20M
```

## mysql

setup and install mysql
```
apt-get --yes install mysql-server mysql-client
```

## ssh

install OpenSSH Server
```
apt-get --yes install ssh
```

use custom port, edit the ssh configuration file
```
nano /etc/ssh/sshd_config
```

find 'Port 22' (ports, IPs and protocols we listen for) & change as below
```
Port 1123
```

reboot server
```
reboot
```

## login with new port
```
ssh root@[server ipaddress] -p1123
```
