---
title: "CentOSのPHPを7.4にする"
emoji: "📝"
type: "tech" # tech: 技術記事 / idea: アイデア
topics: ["CentOS", "PHP"]
published: true
---

```sh
yum list installed | grep php
Repodata is over 2 weeks old. Install yum-cron? Or run: yum makecache fast
php.x86_64                           7.2.21-1.el7.remi              @remi-php72 
php-cli.x86_64                       7.2.21-1.el7.remi              @remi-php72 
php-common.x86_64                    7.2.21-1.el7.remi              @remi-php72 
php-devel.x86_64                     7.2.21-1.el7.remi              @remi-php72 
php-gd.x86_64                        7.2.21-1.el7.remi              @remi-php72 
php-json.x86_64                      7.2.21-1.el7.remi              @remi-php72 
php-mbstring.x86_64                  7.2.21-1.el7.remi              @remi-php72 
php-pdo.x86_64                       7.2.21-1.el7.remi              @remi-php72 
php-pecl-xdebug.x86_64               2.7.2-1.el7.remi.7.2           @remi-php72 
php-pecl-zip.x86_64                  1.15.4-1.el7.remi.7.2          @remi-php72 
php-pgsql.x86_64                     7.2.21-1.el7.remi              @remi-php72 
php-xml.x86_64                       7.2.21-1.el7.remi              @remi-php72
```



```sh
sudo cp /etc/php.ini /etc/php-old.ini
```



```sh
sudo yum remove php-*
```



```sh
sudo yum install https://rpms.remirepo.net/enterprise/remi-release-7.rpm
```



```sh
sudo yum install --enablerepo=remi-php74 php php-devel php-mbstring php-pdo php-mysqlnd php-pgsql php-zip php-xml
```



```sh
sudo yum --enablerepo=remi-php74 update
```