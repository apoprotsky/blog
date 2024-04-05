# PostgreSQL

## Проверка сертификата сервера

Получить данные о серверном сертификате и проверить его валидность можно с помощью `openssl`

{% code overflow="wrap" fullWidth="false" %}
```sh
echo "" | openssl s_client -starttls postgres -connect hostname:5432 -CAfile ca.crt -showcerts
```
{% endcode %}

## Ссылки

[https://serverfault.com/questions/79876/connecting-to-postgresql-with-ssl-using-openssl-s-client](https://serverfault.com/questions/79876/connecting-to-postgresql-with-ssl-using-openssl-s-client)
