# Репликация

## Слоты репликации

### Создание слота

```
select pg_create_physical_replication_slot(‘slot_1’);
```

### Просмотр слотов

Посмотреть список слотов репликации с задержкой и текущим состоянием можно с помощью запроса

```sql
SELECT
  slot_name,
  pg_size_pretty(
    pg_wal_lsn_diff(pg_current_wal_lsn(), restart_lsn)
  ) AS replicationSlotLag,
  active
FROM
  pg_replication_slots;
```

Для более старых версий (9.х) можно использовать такой же запрос, но с другими функциями для упрощения работы с `wal`

```sql
SELECT
  slot_name,
  pg_size_pretty(
    pg_xlog_location_diff(pg_current_xlog_location(), restart_lsn)
  ) AS replicationSlotLag,
  active
FROM
  pg_replication_slots;
```

Пример результата выполнения запроса

```
 slot_name | replicationslotlag | active 
-----------+--------------------+--------
 slot_1    | 799 GB             | f
 slot_2    | 85 MB              | t
```

### Удаление слота

```
select pg_drop_replication_slot(‘slot_1’);
```

[https://hevodata.com/learn/postgresql-replication-slots](https://hevodata.com/learn/postgresql-replication-slots)\
[https://stackoverflow.com/questions/60527214/how-to-limit-wal-size-when-using-postgres-logical-replication-slot](https://stackoverflow.com/questions/60527214/how-to-limit-wal-size-when-using-postgres-logical-replication-slot)
