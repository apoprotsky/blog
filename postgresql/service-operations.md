# Служебные операции

## Создание дампа базы

```c
pg_dump -v --format c --port=5432 \
  --no-privileges --no-owner --no-tablespaces \
  --disable-triggers --dbname=daname \
> daname.sql
```

## Вакуумирование таблиц

Для запуска вакуумирования таблицы с анализом индексов нужно выполнить следующую команду:

```sql
vacuum (verbose, analyze) "table_name";
```

