# Полезные заметки

## Где используется `secret`?

Получение списка `pod`-ов и используемых в них `secret`-ов, смонтированных как `volume`

{% code overflow="wrap" lineNumbers="true" %}
```shell
kubectl get pods -A -o=custom-columns='NAME:.metadata.name,SECRETS:.spec.volumes[*].secret.secretName'
```
{% endcode %}

Получение списка `pod`-ов и используемых в них `secret`-ов как переменных окружения

{% code overflow="wrap" lineNumbers="true" %}
```
kubectl get pods -A -o=custom-columns='NAME:.metadata.name,SECRETS:.spec.containers[*].env[*].valueFrom.secretKeyRef.name'
```
{% endcode %}

Для получения списка `pod`-ов, в которых используется конкретный `secret`, вывод команд выше можно отфильтровать с помощью `grep`.

## Ссылки

[https://stackoverflow.com/questions/43225591/selecting-array-elements-with-the-custom-columns-kubernetes-cli-output](https://stackoverflow.com/questions/43225591/selecting-array-elements-with-the-custom-columns-kubernetes-cli-output)\
[https://stackoverflow.com/questions/46406596/how-to-identify-unused-secrets-in-kubernetes](https://stackoverflow.com/questions/46406596/how-to-identify-unused-secrets-in-kubernetes)
