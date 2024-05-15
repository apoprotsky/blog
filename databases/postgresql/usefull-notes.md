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

## Экспорт данных

### Создание дампа базы

```c
pg_dump -v --format c --port=5432 \
  --no-privileges --no-owner --no-tablespaces \
  --disable-triggers --dbname=dbname \
> dump.sql
```

### Создание дампа данных таблицы

```c
pg_dump --data-only --column-inserts --dbname=dbname --table=table > dump.sql
```

## Просмотр текущей активности

Выборка текущих запросов с фильтрацией по имени базы данных

```sql
select * from pg_stat_activity where datname = 'database_name';
```

```sql
select pid as process_id, 
       usename as username, 
       datname as database_name, 
       client_addr as client_address, 
       application_name,
       backend_start,
       state,
       state_change
  from pg_stat_activity;
```

## Поиск таблиц без PK

```sql
SELECT table_schema, table_name
FROM information_schema.tables
WHERE table_schema NOT IN ('pg_catalog', 'information_schema')
  AND (table_schema, table_name) NOT IN (
    SELECT table_schema, table_name
    FROM information_schema.table_constraints
    WHERE constraint_type = 'PRIMARY KEY'
  );
```

## Ссылки

[https://stackoverflow.com/questions/14021998/using-psql-to-connect-to-postgresql-in-ssl-mode](https://stackoverflow.com/questions/14021998/using-psql-to-connect-to-postgresql-in-ssl-mode)\
[https://stackoverflow.com/questions/12815496/export-specific-rows-from-a-postgresql-table-as-insert-sql-script](https://stackoverflow.com/questions/12815496/export-specific-rows-from-a-postgresql-table-as-insert-sql-script)
