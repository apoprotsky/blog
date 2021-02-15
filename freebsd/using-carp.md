# Использование CARP

`CARP` \( `Common Address Redundancy Protocol` \) - протокол дублирования общего адреса \( [см. Wikipedia](https://ru.wikipedia.org/wiki/CARP) \), позволяет нескольким хостам использовать один IP-адрес. Протокол часто применяется для увеличения отказоустойчивости, доступности сервисов. Рассмотрим настройку `CARP` в `FreeBSD 10` на примере построения отказоустойчивого сервера доступа \( `BRAS` \).  
В случае использования `NAT` желательна синхронизация таблиц трансляции с помощью `pfsync`, но это тема для отдельной заметки.

## Модуль CARP

Для загрузки модуля при старте системы добавить опцию в `/boot/loader.conf`

{% code title="/boot/loader.conf" %}
```bash
carp_load="YES"
```
{% endcode %}

Также модуль можно внести в состав ядра, собрав его с опцией

```text
device carp
```

## Настройки sysctl

Разрешить `CARP` автоматически обрабатывать пропадания хостов и менять роль.

{% code title="/etc/sysctl.conf" %}
```text
net.inet.carp.allow=1
net.inet.carp.preempt=1
```
{% endcode %}

## Настройки интерфейсов

Для определения принадлежности к группе используется параметр `vhid`. Для определения значимости хоста - `advskew`, от 0 до 240, чем меньше - тем приоритет выше.

Настройка внешних интерфейсов хостов `em0` в `/etc/rc.conf`. Общий адрес `1.1.1.1`, `id` хоста `1`.

{% code title="/etc/rc.conf" %}
```text
#Хост 1
ifconfig_em0="inet 1.1.1.2 netmask 255.255.255.0"
ifconfig_em0_alias0="inet 1.1.1.1 netmask 255.255.255.255 vhid 1 advskew 100 pass carppassword"

#Хост 2
ifconfig_em0="inet 1.1.1.3 netmask 255.255.255.0"
ifconfig_em0_alias0="inet 1.1.1.1 netmask 255.255.255.255 vhid 1 advskew 200 pass carppassword"
```
{% endcode %}

Настройка внутренних интерфейсов хостов `em1` в `/etc/rc.conf`. Общий адрес `10.0.0.1`, `id` хоста `2`.

{% code title="/etc/rc.conf" %}
```text
#Хост 1
ifconfig_em1="inet 10.0.0.2 netmask 255.255.255.0"
ifconfig_em1_alias0="inet 10.0.0.1 netmask 255.255.255.255 vhid 2 advskew 100 pass carppassword" 

#Хост 2
ifconfig_em0="inet 10.0.0.3 netmask 255.255.255.0"
ifconfig_em0_alias0="inet 10.0.0.1 netmask 255.255.255.255 vhid 2 advskew 200 pass carppassword"
```
{% endcode %}

## Мониторинг и работа системы

Для мониторинга состояния интерфейсов используется `ifconfig`

```text
ifconfig em1
em1: flags=8943 metric 0 mtu 1500
...
inet 10.0.0.19 netmask 0xfffff000 broadcast 10.0.15.255
inet 10.0.0.18 netmask 0xffffffff broadcast 10.0.0.18 vhid 2
...
carp: MASTER vhid 2 advbase 1 advskew 100
```

В случае пропадания хоста, выбранного как `MASTER`, второй хост изменит свое состояние с `BACKUP` на `MASTER`. Данные переходы журналируются в `/var/log/messages`.

Также возможна принудительная смена роли на одно из значений `INIT` `MASTER` `BACKUP`

```text
ifconfig em1 vhid 2 state BACKUP
```

