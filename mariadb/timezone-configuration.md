# Настройка временной зоны

## Проверка текущих настроек

По умолчанию сервером базы данных выбирается системная временная зона. Это можно проверить следующей командой

```sql
MariaDB [mysql]> SHOW GLOBAL VARIABLES LIKE 'time_zone'\G
*************************** 1. row ***************************
Variable_name: time_zone
        Value: SYSTEM
```

## Настройка через файл конфигурации

Настроить временную зону можно через файл конфигурации с помощью параметра `default_time_zone`

```ini
[mariadb]
...
default_time_zone = 'Europe/Kiev'
```

## Настройка без перезапуска сервера

Изменить временную зону без перезапуска сервера базы данных можно следующим образом

```sql
SET GLOBAL time_zone = 'Europe/Kiev'
```

Если при установке временной зоны получаем ошибку

```sql
ERROR 1298 (HY000): Unknown or incorrect time zone: 'Europe/Kiev'
```

то необходимо добавить данные о временных зонах в базу данных

```shell
mysql_tzinfo_to_sql /usr/share/zoneinfo | mysql -u root -p mysql
```

## &#x20;Ссылки

[https://mariadb.com/kb/en/time-zones](https://mariadb.com/kb/en/time-zones/)\
[https://dba.stackexchange.com/questions/120945/how-do-i-resolve-this-error-error-1298-hy000-unknown-or-incorrect-time-zone](https://dba.stackexchange.com/questions/120945/how-do-i-resolve-this-error-error-1298-hy000-unknown-or-incorrect-time-zone)
