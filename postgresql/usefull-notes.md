# Полезные заметки

## Подключение к серверу консольным клиентом

Подключение с указанием полного URI

```c
psql "postgresql://user:pass@host:5432/dbname?sslmode=verify-full&sslrootcert=ca.pem"
```

или указывая параметры отдельными ключами, пароль при этом будет запрошен интерактивно

```c
psql --host=host --port=5432 --username=user --dbname=dbname \
  --set=sslmode=verify-full --set=sslrootcert=ca.pem
```

## Просмотр текущей активности

Выборка текущих запросов с фильтрацией по имени базы данных

```sql
select * from pg_stat_activity where datname = 'database_name';
```

## Ссылки

[https://stackoverflow.com/questions/14021998/using-psql-to-connect-to-postgresql-in-ssl-mode](https://stackoverflow.com/questions/14021998/using-psql-to-connect-to-postgresql-in-ssl-mode)

