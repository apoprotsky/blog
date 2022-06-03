# Bash

## Сохранение в истории временной метки

Для записи в историю команд отметки о времени необходимо задать значение переменной окружения `HISTTIMEFORMAT`. Например, можно значение переменной можно установить в файле `~/.bashrc`

```bash
HISTTIMEFORMAT="%F %T "
```

При таком формате история команд будет выглядеть следующим образом

```bash
  497  2022-06-03 13:53:26 vi ~/.bashrc
  498  2022-06-03 13:53:26 sudo su - root
```

### Ссылки

[https://www.linuxuprising.com/2019/07/bash-history-how-to-show-timestamp-when.html](https://www.linuxuprising.com/2019/07/bash-history-how-to-show-timestamp-when.html)
