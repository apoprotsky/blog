# Полезные заметки

## Проблемы при синхронизации slave

### Проблема недостаточного размера буферов slave

В случае достаточно длительных разрывов соединения между `master` и slave, `slave`-у необходимо сделать полную синхронизация из-за большого отставания. При этом в журналах на master-е можно наблюдать подобные сообщения:

> 58:M 01 Jan 2021 00:34:09.241 \* Replica 10.10.10.2:6379 asks for synchronization  
> 58:M 01 Jan 2021 00:34:09.241 \* Full resync requested by replica 10.10.10.2:6379  
>   
> 58:M 01 Jan 2021 00:35:08.105 \# Client id=84435 addr=10.10.10.2:43705 fd=108 name= age=311 idle=311 flags=S db=0 sub=0 psub=0 multi=-1 qbuf=0 qbuf-free=0 obl=16384 oll=33199 omem=680712296 events=rw cmd=psync scheduled to be closed ASAP for overcoming of output buffer limits.  
> 58:M 01 Jan 2021 00:35:08.300 \# Connection with replica 10.10.10.2:6379 lost.

### Решение

Необходимо увеличить размер буферов для `slave`-а

Текущее значение можно посмотреть командой

```text
config get client-output-buffer-limit
```

Команда выводит значения для трех классов `normal`, `slave` и `pubsub` в формате

```text
<class> <hard limit> <soft limit> <soft seconds>
```

Для установки нового лимита буферов slave необходимо выполнить команду

```text
config set client-output-buffer-limit "slave 4294967296 2147483648 60"
```

В файле конфигурации допускается использование единиц измерения

{% code title="/etc/redis/redis.conf" %}
```text
client-output-buffer-limit slave 1gb 256mb 60
```
{% endcode %}

### Ссылки

[https://devsday.ru/blog/details/13452](https://devsday.ru/blog/details/13452)

