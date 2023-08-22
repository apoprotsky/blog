# Экспорт и импорт данных

## Экспорт данных

Экспорт данных из таблицы можно выполнить с помощью консольного клиента

{% code overflow="wrap" %}
```sh
clickhouse client -q "SELECT * FROM dbname.tablename" | gzip > table.tsv.gz
```
{% endcode %}

В приведенном примере данные будут экспортированы в формате [TabSeparated (TSV)](https://clickhouse.com/docs/en/interfaces/formats#tabseparated)

При необходимости можно указать другой [формат](https://clickhouse.com/docs/en/interfaces/formats), например JSON

{% code overflow="wrap" %}
```sh
clickhouse client -q "SELECT * FROM dbname.tablename FORMAT JSON" | gzip > table.json.gz
```
{% endcode %}

## Импорт данных

Для импорта данных также можно воспользоваться консольным клиентом

{% code overflow="wrap" %}
```sh
zcat table.tsv.gz | clickhouse client -q "INSERT INTO dbname.tablename FORMAT TabSeparated"
```
{% endcode %}

## Ссылки

[https://clickhouse.com/docs/knowledgebase/file-export](https://clickhouse.com/docs/knowledgebase/file-export)\
[https://clickhouse.com/docs/en/integrations/data-formats/csv-tsv](https://clickhouse.com/docs/en/integrations/data-formats/csv-tsv)\
[https://gist.github.com/inkrement/ea78bc8dce366866103df83ea8d36247](https://gist.github.com/inkrement/ea78bc8dce366866103df83ea8d36247)
