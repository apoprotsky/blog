# Вакуумирование таблиц



Для запуска вакуумирования таблицы с анализом индексов нужно выполнить следующую команду:

```sql
vacuum (verbose, analyze) "table_name";
```

По умолчанию `PostgreSQL` запускает процесс автовакуумирования в фоне, когда количество обновленных или удаленных записей достигает порога, определяемого параметром `autovacuum_vacuum_scale_factor`. По умолчанию значение этого параметра 0.2 (20% от количества записей в таблице). Изменить значение параметра можно на глобальном уровне в файле конфигурации `PostgreSQL` или указать для конкретной таблицы с помощью следующей инструкции:

```sql
alter table "tablename" set (
  autovacuum_vacuum_scale_factor=0.14, autovacuum_analyze_scale_factor=0.13
);
```
