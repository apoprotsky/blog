# Восстановление репликации

Репликация в `MySQL` - очень удобная возможность, а с появлением `GTID` эксплуатация стала еще проще. Репликация позволяет держать горячую резервную копию и снижать нагрузку на основную реплику, направляя выборки на реплику. И все работает отлично, пока однажды не случается проблема...

### Определение проблемы

Если при воспроизведении бинарных журналов на реплике возникает какая-либо проблема, то репликация останавливается. При этом в журнале вы увидите подобное:

> 2021-01-01T18:56:50.487205Z 11964570 \[Warning\] Slave: Can't find record in 'mytable' Error\_code: 1032,

> 2021-01-01T18:56:50.487173Z 11964570 \[ERROR\] Slave SQL for channel 'master': Could not execute Delete\_rows event on table mydb.mytable; Can't find record in 'mytable', Error\_code: 1032; handler error HA\_ERR\_KEY\_NOT\_FOUND; the event's master log mysql-bin.002599, end\_log\_pos 866963173, Error\_code: 1032

> 2021-01-01T18:56:50.487213Z 11964570 \[ERROR\] Error running query, slave SQL thread aborted. Fix the problem, and restart the slave SQL thread with "SLAVE START". We stopped at log 'mysql-bin.002599' position 866962354

Произойти подобная ситуация может например при изменении данных на реплике напрямую.

### Восстановление

Самый простой способ восстановления работоспособности реплики - полное восстановление из резервной копии. Но это не всегда целесообразно по многим причинам - например, значительный объем данных и время, необходимое для восстановления.

Другой способ - откорректировать данные на реплике, чтобы появилась возможность воспроизвести действия из бинарного журнала без ошибок.

Для определения инструкций, которые не могут быть выполнены, на основном сервере смотрим события в журнале:

```text
mysqlbinlog -v --start-position=866962354 --stop-position=866962454 mysql-bin.002599
```

Значение параметра `--start-position` берем из сообщений в журнале реплики, а значение `--stop-position` определяем опытным путем.

После изучения событий и корректировки данных на реплике, запускаем репликацию:

```text
STOP SLAVE;
SET GLOBAL SQL_SLAVE_SKIP_COUNTER = 1;
START SLAVE;
```

### Ссылки

[https://dev.mysql.com/doc/refman/5.7/en/show-binlog-events.html](https://dev.mysql.com/doc/refman/5.7/en/show-binlog-events.html)[https://serverfault.com/questions/862351/slave-replication-stops-with-last-sql-errno-1032](https://serverfault.com/questions/862351/slave-replication-stops-with-last-sql-errno-1032)

