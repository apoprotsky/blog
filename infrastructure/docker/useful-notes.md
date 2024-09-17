# Полезные заметки

## Удаление неиспользуемых образов

Для удаления неиспользуемых образов самым простым способом будет попытка удалить все загруженные образы. Образы, которые используются остановленными или запущенными контейнерами, [Docker](https://www.docker.com) удалить не позволит с такими сообщениями об ошибках:

> Error response from daemon: conflict: unable to delete d79963718228 (must be forced) - image is being used by stopped container 4097c513249b
>
> Error response from daemon: conflict: unable to delete 566260438c26 (cannot be forced) - image is being used by running container 34ab94acf309

Ниже приведен пример команды для [Bash](https://www.gnu.org/software/bash), которая произведет попытку удаления всех загруженных образов

{% code overflow="wrap" %}
```bash
for id in $(docker image ls --format '{{ .ID }}'); do docker image rm ${id}; done
```
{% endcode %}
