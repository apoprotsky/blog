---
description: Пакетный менеджер Debian / Ubuntu
---

# dpkg

## Размер установленных пакетов

Иногда бывает необходимо выяснить сколько занимает дискового пространства установленный пакет или какие из установленных пакетов наиболее крупные.

Получить отсортированный по возрастанию размера список установленных пакетов с указанием их размера в килобайтах можно следующей командой:

```c
dpkg-query -Wf '${Installed-Size}\t${Package}\n' | sort -n
```

Для определения размера интересующего пакета можно отфильтровать вывод с помощью команды `grep`:

```c
dpkg-query -Wf '${Installed-Size}\t${Package}\n' | grep php
```

Для получения десятка самых крупных пакетов можно воспользоваться командой tail:

```c
dpkg-query -Wf '${Installed-Size}\t${Package}\n' | sort -n | tail -n 10
```

## Ссылки

[https://unix.stackexchange.com/questions/40442/which-installed-software-packages-use-the-most-disk-space-on-debian](https://unix.stackexchange.com/questions/40442/which-installed-software-packages-use-the-most-disk-space-on-debian)

