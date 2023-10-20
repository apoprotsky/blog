# Полезные заметки

Иногда при работе `PHP`-скриптов возникают не совсем очевидные ошибки. В данной заметке будем собирать проблемы в работе веб-приложений и решения, затрагивающие конфигурацию `PHP`.

## В POST или GET отсутствуют переменные, которые были в запросе

Одна из причин - большое количество переменных. Ограничение определяется параметром `max_input_vars` в `php.ini`. Значение по умолчанию `1000`.

## Ссылки

[http://stackoverflow.com/questions/9399315/how-to-increase-maximum-post-variable-in-php](http://stackoverflow.com/questions/9399315/how-to-increase-maximum-post-variable-in-php)

