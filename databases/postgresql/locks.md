# Блокировки

## Поиск заблокированных процессов

```sql
SELECT pid, 
       usename, 
       pg_blocking_pids(pid) as blocked_by, 
       query as blocked_query
  FROM pg_stat_activity
 WHERE cardinality(pg_blocking_pids(pid)) > 0;
```

## Ссылки

[https://stackoverflow.com/questions/26489244/how-to-detect-query-which-holds-the-lock-in-postgres](https://stackoverflow.com/questions/26489244/how-to-detect-query-which-holds-the-lock-in-postgres)
