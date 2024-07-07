# Конфигурация кэша WiredTiger

## Установка максимального размера кэша при старте

По умолчанию в MongoDB максимальный размер кэша для WiredTiger на системах с объемом ОЗУ более 1 ГБ вычисляется по формуле 50% \* (ОЗУ - 1 ГБ)

Для переопределения этого значения при запуске сервера MongoDB можно воспользоваться параметром --wiredTigerCacheSizeGB или указать необходимое значение в файле конфигурации

```yaml
storage:
  wiredTiger:
    engineConfig:
      cacheSizeGB: <float>
```

Получить текущий размер кэша WiredTiger можно, выполнив следующую команду

```javascript
db.serverStatus().wiredTiger.cache['bytes currently in the cache']
```

## Изменение максимального размера кэша в процессе работы

В случае необходимости изменения максимального размера кэша WiredTiger без перезапуска сервера MongoDB новое значение можно установить с помощью команды setParameter

```javascript
db.adminCommand({setParameter: 1, wiredTigerEngineRuntimeConfig: 'cache_size=4G'});
```

Проверить установленное в runtime значение можно с помощью команды getParameter

```javascript
db.adminCommand({getParameter: 1, wiredTigerEngineRuntimeConfig: 1});
```

## Ссылки

[https://www.mongodb.com/docs/v5.0/reference/program/mongod/#std-option-mongod.--wiredTigerCacheSizeGB](https://www.mongodb.com/docs/v5.0/reference/program/mongod/#std-option-mongod.--wiredTigerCacheSizeGB)\
[https://www.dragonflydb.io/faq/mongodb-check-cache-size](https://www.dragonflydb.io/faq/mongodb-check-cache-size)\
[https://www.mongodb.com/community/forums/t/wiredtiger-cachesize-setting-not-persistent-across-restart/206333](https://www.mongodb.com/community/forums/t/wiredtiger-cachesize-setting-not-persistent-across-restart/206333)
