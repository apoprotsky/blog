# Управление томами ZFS

Носители информации в `ZFS` организовываются в пулы. Управление пулами описывалось в [этой заметке](zfs-pool-management.md). Поверх пулов организовывается пространство файловой системы - разделы, именуемые в терминологии `ZFS` наборами данных. Управление наборами данных рассмотрим в данной заметке.

## Наборы данных \(dataset\)

### Создание тома

По умолчанию будет создана новая файловая система. Для создания тома \(`volume`\) нужно указать флаг `-V` и размер. Том используется как блочное устройство.

```text
zfs create zroot/home
zfs create zroot/data -V 1G
```

### Удаление тома

```text
zfs destroy zroot/home
```

## Снимки \(snapshot\)

### Создание снимка набора данных

Для создания снимков вложенных наборов данных используется флаг `-r`

```text
zfs snapshot zroot/home@today
```

###  Откат набора данных до состояния снимка

```text
zfs rollback zroot/home@today
```

### Удаление снимка набора данных

```text
zfs destroy zroot/home@today
```

### Пересылка снимка по  ssh

При пересылке полного снимка на принимающей стороне набор данных должен отсутствовать и должен присутствовать при пересылке разности снимков \(флаг `-i`\)

#### Пересылка полного снимка

```text
zfs send zroot/home@today | ssh host zfs recv zbackup/home
```

#### Пересылка полных снимков с рекурсией по вложенным наборам данных

```text
zfs send -R zroot/home@today | ssh host zfs recv -dF zbackup
```

Флаг `-R` определяет рекурсивный проход в `send`  
Флаг `-d` отбрасывает имя пула при приеме данных  
Флаг `-F` воспроизводит операции удаления наборов данных

#### Пересылка разности снимков

```text
zfs sent -i zroot/home@snap1 zroot/home@snap2 | ssh host zfs recv zbackup/home
```

## Ссылки

[https://habrahabr.ru/sandbox/32271/](https://habrahabr.ru/sandbox/32271/)  
[http://docs.oracle.com/cd/E19253-01/819-5461/6n7ht6r4m/index.html](http://docs.oracle.com/cd/E19253-01/819-5461/6n7ht6r4m/index.html)  
[http://docs.oracle.com/cd/E19253-01/820-0836/6nci36qjq/index.html](http://docs.oracle.com/cd/E19253-01/820-0836/6nci36qjq/index.html)[https://www.opennet.ru/tips/2499\_freebsd\_zfs\_replication.shtml](https://www.opennet.ru/tips/2499_freebsd_zfs_replication.shtml)

