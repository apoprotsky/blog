# Управление пулами ZFS

Поскольку `ZFS` - это детище `Sun Microsystems`, впоследствии портированное во многие операционные системы, то управление пулами будет аналогичным.

## Создание пулов

Создание пула из одного диска

```text
zpool create zroot da0
```

Создание пула из двух дисков с увеличением дискового пространства \(`stripe`\)

```text
zpool create zroot da0 da1
```

Создание пула из двух дисков с дублированием данных \(`mirror`\)

```text
zpool create zroot mirror da0 da1
```

## Изменение названия пула

Если пул используется как загрузочный, то операции необходимо выполнять загрузившись с другого носителя.Экспорт под старым названием

```text
zpool export oldname
```

Импортирование с переименованием

```text
zpool import oldpool newpool
```

Если точка монтирования пула указана как `/`, то можно воспользоваться флагом `-R` `/path/to/altroot`. Возможно также понадобится флаг `-f`, если пул использовался в другой операционной системе.

```text
zpool import -R /mnt -f oldpool newpool
```

Экспорт переименованного пула

```text
zpool export newpool
```

И напоследок, импорт пула под новым именем

```text
zpool import newpool
```

## Восстановление работоспособности пула

Замена диска

```text
 zpool replace zroot da0
```

Дополнительным параметром можно указать какой диск использовать для замены

```text
 zpool replace zroot da0 da2
```

## Ссылки

[https://ru.wikipedia.org/wiki/ZFS](https://ru.wikipedia.org/wiki/ZFS)  
[https://forums.freebsd.org/threads/46300/](https://forums.freebsd.org/threads/46300/)

