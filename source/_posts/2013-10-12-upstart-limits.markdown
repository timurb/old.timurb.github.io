---
layout: post
title: "Upstart limits"
date: 2013-10-12 12:06
comments: true
categories: upstart
---

Как всем известно, чтобы установить лимиты ресурсов для сервиса, запускаемого через Upstart
нужно править соответствующий скрипт запуска, а лимиты, установленные в `/etc/security/limits.conf`
не действуют. Однако я не встречал в доках упоминание о том, что эти лимиты применяются только
после остановки и последующего запуска сервиса, но не применяются при рестарте.

Проиллюстрирую примером.

<!-- more -->

Upstart-скрипт и лимиты для [Docker](http://www.docker.io/) по-умолчанию:
```
$  cat /etc/init/docker.conf | egrep -v '^($|#)'                                                                      * source c2d7a58
description     "Docker daemon"
start on filesystem and started lxc-net
stop on runlevel [!2345]
respawn
script
  /usr/bin/docker -d
end script

~/git/timurbatyrshin.github.com
$  cat /proc/$(pidof docker)/limits | grep files                                                                      * source c2d7a58
Max open files            1024                 4096                 files     
```

Чуть-чуть меняем upstart-скрипт и смотрим результат:
```
$  cat /etc/init/docker.conf | egrep -v '^($|#)'
description     "Docker daemon"
start on filesystem and started lxc-net
stop on runlevel [!2345]
respawn
limit nofile 65535 65535  # <--- добавили эту строчку
script
  /usr/bin/docker -d
end script

$  sudo restart docker
docker start/running, process 4721

$  cat /proc/$(pidof docker)/limits | grep files
Max open files            1024                 4096                 files     

$  sudo stop docker ; sudo start docker
docker stop/waiting
docker start/running, process 4772

$  cat /proc/$(pidof docker)/limits | grep files
Max open files            65535                65535                files     
```

Как видим, лимиты при рестарте не изменяются, а меняются только при остановке-старте.
