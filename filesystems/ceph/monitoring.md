# Мониторинг

Для получения метрик в формате `Prometheus` необходимо активировать модуль `prometheus` сервиса `Ceph manager`

```bash
ceph mgr module enable prometheus
```

Порт по умолчанию `9283`, путь стандартный - `/metrics`, протокол `http`.

## 18.2.4 Reef

При обновлении по версии [18.2.4 Reef](https://docs.ceph.com/en/latest/releases/reef/#v18-2-4-reef) из списка метрик, которые возвращаются модулем `prometheus` сервиса `Ceph manager`, убраны метрики производительности, в том числе касающиеся работы `OSD`. Эти метрики перенесены в отдельный сервис `ceph-exporter`.

Такое решение принято для улучшения работы `Ceph manager`, так как сбор этих метрик создает достаточную нагрузку, особенно на крупных кластерах, что приводит к увеличению времени обработки запросов к `Ceph manager`.

Но на небольших кластерах можно вернуть прежнее поведение через установку параметра конфигурации [mgr/prometheus/exclude\_perf\_counters](https://docs.ceph.com/en/latest/mgr/prometheus/#ceph-daemon-performance-counters-metrics)

```sh
ceph config set mgr mgr/prometheus/exclude_perf_counters false
```

## Ссылки

[https://docs.ceph.com/en/latest/releases/reef/#dashboard](https://docs.ceph.com/en/latest/releases/reef/#dashboard)\
[https://docs.ceph.com/en/latest/mgr/prometheus/#ceph-daemon-performance-counters-metrics](https://docs.ceph.com/en/latest/mgr/prometheus/#ceph-daemon-performance-counters-metrics)
