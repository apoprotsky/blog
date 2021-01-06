# Свой репозиторий pkgng

`pkgng` - новый менеджер пакетов, обладающий весьма привлекательным функционалом.  
Но при использовании стандартного репозитория пакетов `pkg.FreeBSD.org` мы теряем возможность опциональной сборки приложения. Решение - создание собственного репозитория, в котором пакеты приложений будут собраны с необходимыми нам опциями. Для создания своего репозитория воспользуемся `poudriere` - инструментом для тестирования сборки пакетов.

## Подготовка

### Установка пакета poudriere

```text
pkg install poudriere
```

### Настройка poudriere

{% code title="/usr/local/etc/poudriere.conf" %}
```text
ZPOOL=zroot
ZROOTFS=/poudriere
BASEFS=/poudriere
DISTFILES_CACHE=${BASEFS}/distfiles
FREEBSD_HOST=ftp://ftp.freebsd.org
WRKDIR_ARCHIVE_FORMAT=txz
BUILDER_HOSTNAME=freebsd.local
```
{% endcode %}

### Формирование среды для сборки пакетов

Создание дерева портов с использованием `portsnap` в каталоге `/poudriere/ports/default`

```text
poudriere ports -c
```

Обновление дерева портов производится командой

```text
poudriere ports -u
```

Создание `jail` с системой версии `10.1-RELEASE` в каталоге `/poudriere/jails/101amd64`. Для указания архитектуры, отличной от текущей, используется параметр `-a`.

```text
poudriere jail -c -j 101amd64 -v 10.1-RELEASE -a amd64
```

При создании `jail` `poundriere` сразу обновляет систему в нем с помощью `freebsd-update`. Отдельно обновить `jail` можно следующей командой:

```text
poudriere jail -u -j 101amd64
```

Для обновления `jail` до другой версии операционной системы используется флаг `-t`

```text
poudriere jail -u -t 10.2-RELEASE -j 101amd64
```

После смены версии, логичным было бы переименовать `jail`, а также изменить точку монтирования. Переименование jail производится следующей командой:

```text
poudriere jail -r 102amd54 -j 101amd64
```

Для изменения точки монтирования и расположения самого `jail` необходимо отредактировать  файлы `fs` и `mnt` в каталоге `/usr/local/poudriere.d/jails/102amd42`.

Также внести изменения в файловую систему:

```text
zfs rename zroot/poudriere/jails/101amd64 zroot/poudriere/jails/102amd64
zfs set mountpoint=/poudriere/jails/102amd64 zroot/poudriere/jails/102amd64
```

## Конфигурация портов и сборка пакетов

Чтобы не собирать все дерево портов, можно указать список только необходимых в файле 

{% code title="/usr/local/etc/poudriere.d/lists/102amd64" %}
```text
www/nginx
lang/php5
```
{% endcode %}

### Установка опций сборки пакетов по своему усмотрению

```text
poudriere options -j 102amd64 -f /usr/local/etc/poudriere.d/lists/102amd64
```

### Сборка пакетов с установленными опциями

```text
poudriere bulk -j 102amd64 -f /usr/local/etc/poudriere.d/lists/102amd64
```

#### Ссылки

[http://www.bsdnow.tv/tutorials/poudriere](http://www.bsdnow.tv/tutorials/poudriere)  
[https://gist.github.com/dch/fea9ba2bf955369a05e8](https://gist.github.com/dch/fea9ba2bf955369a05e8)  
[http://bugreev.ru/blog:2014:09:10-шпаргалка\_-\_сборка\_пакетов\_для\_систем\_freebsd](http://bugreev.ru/blog:2014:09:10-%D1%88%D0%BF%D0%B0%D1%80%D0%B3%D0%B0%D0%BB%D0%BA%D0%B0_-_%D1%81%D0%B1%D0%BE%D1%80%D0%BA%D0%B0_%D0%BF%D0%B0%D0%BA%D0%B5%D1%82%D0%BE%D0%B2_%D0%B4%D0%BB%D1%8F_%D1%81%D0%B8%D1%81%D1%82%D0%B5%D0%BC_freebsd)

